The Kernel Loader ("KernelLdr"/"Kernelldr") was added in
[8.0.0](8.0.0.md "wikilink"). It is responsible for applying relocations
to the Kernel, and mapping the Kernel's .text/.rodata/.data/.bss at a
random slide.

# Functions

KernelLdr is called immediately by the Kernel's crt0 (after it
deprivileges from EL2 to EL1, if required), with the following
signature:

`   void KernelLdr_Main(uintptr_t kernel_base_address, KernelMap *kernel_map, uintptr_t ini1_base_address);`

## KernelLdr\_Main

First, it clears BSS, and then sets SP = <BSS end>.

``` 
    for (uint64_t *i = __bss_start; i != __bss_end; i++) {
        *i = 0;
    }
    SP = __bss_end;
```

Next, it applies relocations to itself and calls its init array.

``` 
    KernelLdr_ApplyRelocations(&KernelLdr_Main, __dynamic_start);
    KernelLdr_libc_init_array();
```

Then, it calls the function which relocates the kernel, and jumps back
to the kernel entrypoint.

``` 
    // KernelLdr_LoadKernel returns (relocated_kernel_base - original_kernel_base).
    uintptr_t kernel_relocation_offset = KernelLdr_LoadKernel(kernel_base, kernel_map, ini_base);
    
    // finalize called for static page allocator.
    g_InitialPageAllocator.Finalize();
    
    // Jumps back to the kernel code that called KernelLdr_Main.
    ((void (*)(void))(kernel_relocation_offset + LR))();
```

## KernelLdr\_ApplyRelocations

This does standard ELF relocation using .dynamic.

First, it iterates over all entries in .dynamic, extracting .rel.dyn,
.rela.dyn, relent, relatent, relcount, relacount from the relevant
entries.

Then it does the following two loops to apply R\_AARCH64\_RELATIVE
relocations:

``` 
    for (size_t i = 0; i < rel_count; i++) {
        const Elf64_Rel *rel = dyn_rel_start + rel_ent * i;
        while (uint32_t(rel->r_info) != R_AARCH64_RELATIVE) { /* Invalid entry, infloops */ }
        *((Elf64_Addr *)(base_address + rel->r_offset)) += base_address;
    }
```

``` 
    for (size_t i = 0; i < rela_count; i++) {
        const Elf64_Rela *rela = dyn_rela_start + rela_ent * i;
        while (uint32_t(rela->r_info) != R_AARCH64_RELATIVE) { /* Invalid entry, infloops */ }
        *((Elf64_Addr *)(base_address + rela->r_offset)) = base_address + rela->r_addend;
    }
```

## KernelLdr\_libc\_init\_array()

This is just standard libc init array code. .init\_array is empty in all
available binaries.

## KernelLdr\_LoadKernel

First, it backs up the original kernel base, and then relocates the
kernel physically to the upper half of DRAM if enough memory is
available.

``` 
    // Backup kernel_base argument for use later
    original_kernel_base = kernel_base;
    
    // Move kernel elsewhere in DRAM if needed (unused in practice?)
    // This is maybe to support reserving unused memory for a second OS/hypervisor?
    KernelLdr_RelocateKernelPhysically(&kernel_base, &kernel_map);
```

Then it checks all of the kernel map's offsets (and the kernel base) for
page alignment.

``` 
    // Read offsets from the kernel map, save on stack.
    text_offset           = kernel_map->text_offset;
    text_end_offset       = kernel_map->text_end_offset;
    ro_offset             = kernel_map->ro_offset;
    ro_end_offset         = kernel_map->ro_end_offset;
    rw_offset             = kernel_map->rw_offset;
    rw_end_offset         = kernel_map->rw_end_offset;
    bss_offset            = kernel_map->bss_offset;
    ini1_end_offset       = kernel_map->ini1_end_offset;
    dynamic_offset        = kernel_map->dynamic_offset;
    init_array_offset     = kernel_map->init_array_offset;
    init_array_end_offset = kernel_map->init_array_end_offset;

    // Check all offsets are appropriately aligned.
    while (kernel_base & 0xFFF) { }
    while (text_offset & 0xFFF) { }
    while (text_end_offset & 0xFFF) { }
    while (ro_offset & 0xFFF) { }
    while (ro_end_offset & 0xFFF) { }
    while (rw_offset & 0xFFF) { }
    while (rw_end_offset & 0xFFF) { }
```

Next, it relocates the INI1 to its appropriate load address.

``` 
    // If configured to do so, an extra 0x68000 bytes will be reserved for kernel usage.
    reserved_kernel_data_size = KernelLdr_ShouldReserveAdditionalKernelData() ? 0x1790000 : 0x1728000;

    // Calculate address at which to place INI1.
    ini1_end_address   = kernel_base + ini1_end_offset + reserved_kernel_data_size;
    ini1_load_address = ini1_end_address - 0xC00000;

    // Relocate INI1 if destination address isn't the input argument address
    if (ini1_load_address != ini1_address) {
        // Validate INI1 binary has correct magic and valid size.
        INI1Header *ini = (INI1Header *)ini1_address;
        if (ini->magic == MAGIC_INI1 && ini->size <= 0xC00000) {
            memmove(ini1_load_address, ini1_address, ini->size); // NOTE: No ToCToU, ini1->size is cached on stack.
        } else {
            // Invalid INI, place invalid header at load address. This will cause Kernel Panic later.
            memset(ini1_load_address, 0, sizeof(INI1Header));
        }
    }
```

Next, it initializes the MMU with a basic identity mapping for Kernel +
KernelLdr.

``` 
    // Set page table region
    page_table_region = ini1_end_address;
    page_table_region_size = 0x200000;
    g_InitialPageAllocator.Initialize(page_table_region);

    // Initialize new page table, eventually ends up in TTBR1_EL1.
    KInitialPageTable ttbr1_page_table(&g_InitialPageAllocator);

    // Setup MMU with initial identity mapping.
    KernelLdr_MapInitialIdentityMapping(&ttbr1_page_table, kernel_base, rw_end_offset, page_table_region, page_table_region_size, &g_InitialPageAllocator);
```

Next, it generates a random KASLR slide for the Kernel.

``` 
    // Repeatedly try to generate a random slide
    while (true) {
        // Get random value from secure monitor in range
        // This is "probably" KSystemControl::GenerateRandomRange, as in normal kernel
        // However, it's unclear whether KSystemControl is actually included, or whether this is just copy/pasted?
        random_kaslr_slide = KernelLdr_GenerateRandomRange(0xFFFFFF8000000000, 0xFFFFFFFFFFDFFFFF);
        aligned_random_kaslr_slide = random_kaslr_slide & 0xFFFFFFFFFFE00000;
        
        // Calculate end address for kernel with this slide, rounding up.
        random_kernel_end = aligned_random_kaslr_slide + (kernel_base & 0x1FFFFF) + rw_end_offset + 0x1FFFFF) & 0x1FFE00000;
       
        // Validate no overflow, and that the kernel will fit with the slide.
        if (aligned_random_kaslr_slide >= random_kaslr_end || ((random_kaslr_end - 1) > 0xFFFFFFFFFFDFFFFF)) {
            continue;
        }

        // Validate we can map this range without conflicts.
        // NOTE: This is inlined, but code looks same as in older kernel binaries.
        if (!ttbr1_page_table.IsFree(aligned_random_kaslr_slide, random_kernel_end - aligned_random_kaslr_slide)) {
            continue;
        }

        // Valid kaslr slide, so we're done.
        break;
    }
    final_virtual_kernel_base = aligned_random_kaslr_slide | (kernel_base & 0x1FFFFF);
```

Then, it maps the kernel at the final virtual address.

``` 
    // Maps .text as R-X
    attribute = 0x40000000000788;
    ttbr1_page_table.Map(final_virtual_kernel_base + text_offset, text_end_offset - text_offset, kernel_base + text_offset, &attribute, &g_InitialPageAllocator);
    
    // Maps .rodata as R--
    attribute = 0x60000000000788;
    ttbr1_page_table.Map(final_virtual_kernel_base + ro_offset, ro_end_offset - ro_offset, kernel_base + ro_offset, &attribute, &g_InitialPageAllocator);

    // Maps .rwdata and .bss as RW-
    attribute = 0x60000000000708;
    ttbr1_page_table.Map(final_virtual_kernel_base + rw_offset, rw_end_offset - rw_offset, kernel_base + rw_offset, &attribute, &g_InitialPageAllocator);

    // Clears BSS.
    memset(final_kernel_virtual_base + bss_offset, 0, rw_end_offset - bss_offset);
```

Then, it applies the kernel's .dynamic relocations and calls the
kernel's libc .init\_array functions.

``` 
    // Applies all R_AARCH64_RELATIVE relocations.
    KernelLdr_ApplyRelocations(final_kernel_virtual_base, final_kernel_virtual_base + dynamic_offset);
    
    // This is standard libc init_array code, but called for the kernel's binary instead of kernelldr's.
    for (uintptr_t cur_func = final_virtual_kernel_base + init_array_offset; cur_func < final_virtual_kernel_base + init_array_end_offset; cur_func += 8) {
        ((void (*)(void))(*(uint64_t *)cur_func)();
    }
```

Finally, it returns the difference between the kernel's original
physical base address and the relocated kaslr'd virtual base address.

``` 
    return final_virtual_kernel_base - original_kernel_base;
```

## KernelLdr\_MapInitialIdentityMapping

Signature is like

`   void KernelLdr_MapInitialIdentityMapping(KInitialPageTable *ttbr1_page_table, uintptr_t kernel_base, uintptr_t kernel_size, `  
`                                            uintptr_t page_tables_base, uintptr_t page_tables_size, InitialPageAllocator *allocator);`

First, this creates a new page table (eventually ends up in TTBR0\_EL1),
and adds identity mappings for Kernel, KernelLdr, and the Page Table
region to it.

``` 
    // Create new KInitialPageTable
    KInitialPageTable ttbr0_page_table(allocator);

    // Maps kernel with RWX identity mapping.
    attribute = 0x40000000000708;
    ttbr0_page_table.Map(kernel_base, kernel_size, kernel_base, &attribute, allocator);

    // Maps kernel loader with RWX identity mapping.
    attribute = 0x40000000000708;
    ttbr0_page_table.Map(__start, __end - __start, __start, &attribute, allocator);

    // Maps page table region with RW- identity mapping.
    attribute = 0x60000000000708;
    ttbr0_page_table.Map(page_tables_base, page_tables_size, page_tables_base, &attribute, allocator);
```

Next, this sets some system registers.

``` 
    // Set TTBR0/TTBR1 with initial page tables.
    TTBR0_EL1 = ttbr0_page_table.GetL1Table();
    TTBR1_EL1 = ttbr1_page_table.GetL1Table();
    
    // Configure MAIR, TCR. TODO: Document here what bits these are.
    MAIR_EL1 = 0x44FF0400;
    TCR_EL1  = 0x11B5193519;

    // Check what CPU we're running on to configure CPUECTLR, CPUACTLR appropriately.
    manufacture_id = MIDR_EL1;
    implemeter = manufacturer_id >> 24) & 0xFF;
    if (implementer == 0x41) {
        // Implementer ID is 0x41 (ARM Limited).
        architecture = (manufacture_id >> 4)  & 0x0FFF;
        hw_variant   = (manufacture_id >> 20) & 0xF;
        hw_revision  = (manufacture_id >> 0)  & 0xF;
        if (architecture == 0xD07) {
            // Architecture is 0xD07 (Cortex-A57).
            cpuactlr_value = 0x1000000;    // Non-cacheable load forwarding enabled
            cpuectlr_value = 0x1B00000040; // TODO: What is this?
            if (hw_variant == 0 || (hw_variant == 1 && hw_revision <= 1)) {
                // If supported, disable load-pass DMB.
                cpuactlr_value |= 0x800000000000000;
            }
            CPUACTLR_EL1 = cpuactlr_value;
            if (CPUECTLR_EL1 != cpuectlr_value) {
                CPUECTLR_EL1 = cpuectlr_value;
            }
        }
    }
```

Next, the cache is flushed, to ensure that page tables will be
successfully read once the MMU is enabled.

``` 
    KernelLdr_EnsureCacheFlushed();
```

Finally, SCTLR is written to, enabling the MMU.

``` 
    SCTLR_EL1 = 0x34D5D925;
    __dsb_sy();
    __isb();
```

## KernelLdr\_RelocateKernelPhysically

This retrieves memory layout information from the secure monitor, and
adjusts the kernel's physical location if necessary.

``` 
    adjusted_kernel_base = KernelLdr_GetAdjustedKernelPhysicalBase(*p_kernel_base);

    if (adjusted_kernel_base != *p_kernel_base) {
        // Copy data to adjusted destination
        memmove(adjusted_kernel_base, *p_kernel_base, (*p_kernel_map)->data_end_offset);

        // Adjust pointers.
        kernel_base_diff = adjusted_kernel_base - *p_kernel_base;
        *p_kernel_base = (uintptr_t)*p_kernel_base + kernel_base_diff;
        *p_kernel_map  = (uintptr_t)*p_kernel_map  + kernel_base_diff;
    }
```

## KernelLdr\_GetAdjustedKernelPhysicalBase

This sees how much more memory is available than expected, and relocates
the kernel accordingly.

Note: Panic (infloop) happens on any smc call error, this isn't depicted
in pseudocode for brevity reasons.

``` 
    // Gets DRAM size information from Memory Controller
    dram_size_from_mc = (smc_read_write_register(MC_EMEM_CFG, 0, 0) & 0x3FFF) << 20;
    
    // Gets DRAM size information from Secure Monitor KernelConfiguration
    memory_type = (smc_get_config(ConfigItem_KernelConfiguration) >> 16) & 3;
    switch (memory_type) {
        case MemoryType_4GB: // 0
            dram_size_from_kernel_cfg = 0x100000000;
            break;
        case MemoryType_6GB: // 1
            dram_size_from_kernel_cfg = 0x180000000;
            break;
        case MemoryType_8GB: // 2
        default:
            dram_size_from_kernel_cfg = 0x200000000;
            break;
    }
    
    // On normal systems, these should be equal (and kernel will not be relocated).
    if (dram_size_from_mc < 2 * dram_size_from_kernel_cfg) {
        return kernel_base + (dram_size_from_mc - dram_size_from_kernel_cfg) / 2;
    } else {
        return kernel_base;
    }
```

## KernelLdr\_ShouldReserveAdditionalKernelData

This just gets a flag from the KernelConfiguration.

Note: Panic (infloop) happens on any smc call error, this isn't depicted
in pseudocode for brevity reasons.

``` 
    return (smc_get_config(ConfigItem_KernelConfiguration) >> 3) & 1;
```

## KernelLdr\_EnsureCacheFlushed

Note: this is inlined, however it uses instructions that no compiler has
intrinsics for (and looks like hand-written asm), so it's presumably its
own thing.

``` 
    // Invalidate Local Cache
    KernelLdr_InvalidateCacheLocal();
    __dsb_sy();

    // Invalidate Share
    KernelLdr_InvalidateCacheShared();
    __dsb_sy();

    // Invalidate Local Cache again
    KernelLdr_InvalidateCacheLocal();
    __dsb_sy();
    
    // asm { tlbi vmalle1is; }
    __dsb_sy();
    __isb();
```

## KernelLdr\_InvalidateCacheLocal

Standard ARM cache clean code, uses LoUIS + LoC from CLIDR\_EL1.

## KernelLdr\_InvalidateCacheShared

Standard ARM cache clean code, uses LoUIS from CLIDR\_EL1.

## KInitialPageAllocator::KInitialPageAllocator

This sets the allocator's next address to 0 (guessed, since this is done
statically in KernelLoader).

``` 
    constexpr KInitialPageAllocator::KInitialPageAllocator : next_address(0) {}
```

## KInitialPageAllocator::Initialize

This sets the allocator's next address (function inferred as it is
(presumably) inlined and next\_address is (presumably) private).

``` 
    this->next_address = address;
```

## KInitialPageAllocator::Finalize

This just clears the allocator's next address.

``` 
    this->next_address = 0;
```

## KInitialPageAllocator::Allocate

This linearly allocates a page.

``` 
    virtual void *KInitialPageAllocator::Allocate() {
        void *address = reinterpret_cast<void *>(this->next_address);
        if (address == nullptr) {
            // If called on uninitialized allocator, panic by infinite looping
            while (true) {}
        }
        this->next_address += 0x1000;
        memset(address, 0, 0x1000);
        return address;
    }
```

## KInitialPageAllocator::Free

This frees a page (implemented as noop in KernelLoader)

``` 
    virtual void KInitialPageAllocator::Free(void *address) {
        // Does Nothing
    }
```

## KInitialPageTable::KInitialPageTable

NOTE: This constructor is inferred.

    KInitialPageTable::KInitialPageTable(KInitialPageAllocator *allocator) {
        this->l1_table_ptr = allocator->Allocate();
        memset(this->l1_table_ptr, 0, 0x1000);
        this->num_l1_table_entries = 0x200;
    }

## KInitialPageTable::Map

Signature is like

`   KInitialPageTable::Map(uintptr_t virtual_address, size_t size, uintptr_t physical_address, const uint64_t *attribute, InitialPageAllocator *allocator);`

This is just standard aarch64 page table mapping code. New L2/L3 pages
are allocated via allocator-\>Allocate() when needed.

## KInitialPageTable::IsFree

This is just standard aarch64 page table code. Walks the page table,
verifying that all entries it would map for size + range are free.

# Structures

## KernelMap

| Offset | Size | Description             |
| ------ | ---- | ----------------------- |
| 0x0    | 4    | .text offset            |
| 0x4    | 4    | .text end offset        |
| 0x8    | 4    | .rodata end offset      |
| 0xC    | 4    | .rodata end offset      |
| 0x10   | 4    | .rwdata offset          |
| 0x14   | 4    | .rwdata end offset      |
| 0x18   | 4    | .bss offset             |
| 0x1C   | 4    | .bss end offset         |
| 0x20   | 4    | INI1 end offset         |
| 0x24   | 4    | .dynamic end offset     |
| 0x28   | 4    | .init\_array end offset |
| 0x2C   | 4    | .init\_array end offset |
|        |      |                         |

## KInitialPageAllocator

KInitialPageAllocator is just a simple linear allocator.

| Offset | Size | Description   |
| ------ | ---- | ------------- |
| 0x0    | 8    | vtable;       |
| 0x8    | 8    | Next Address; |
|        |      |               |

### KInitialPageAllocator::vtable

| Offset | Size | Description                                                  |
| ------ | ---- | ------------------------------------------------------------ |
| 0x0    | 8    | void \*(\*Allocate)(KInitialPageAllocator \*this);           |
| 0x8    | 8    | void (\*Free)(KInitialPageAllocator \*this, void \*address); |
|        |      |                                                              |

## KInitialPageTable

KInitialPageTable is a very, very stripped-down KPageTable.

Compared to pre-KernelLoader KInitialPageTable, it has slightly reduced
memory footprint.

| Offset | Size | Description                                  |
| ------ | ---- | -------------------------------------------- |
| 0x0    | 8    | Pointer to L1 Table;                         |
| 0x8    | 8    | Number of L1 Table Entries (Normally 0x200); |
|        |      |                                              |

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

    // TODO: Fill this out with pseudocode.

Next, it generates a random KASLR slide for the Kernel.

    // TODO: Fill this out with pseudocode.

Then, it maps the kernel and applies its .dynamic's relocations.

    // TODO: Fill this out with pseudocode.

Then, it calls the kernel's libc .init\_array functions.

    // TODO: Fill this out with pseudocode.

Finally, it returns the difference between the kernel's original
physical base address and the relocated kaslr'd virtual base address.

``` 
    return final_virtual_kernel_base - original_kernel_base;
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

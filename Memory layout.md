# Userspace

The userspace virtual address space has 38 bits. It seems that when the
IPC protocol was designed, it was only 36 bits leading to a weird
encoding format.

There are several regions maintained by the kernel, each one starting at
the upper bits bit37-21 randomized:

  - Main binary region.
  - Heap region.
  - Stack mapping region, available from
    [SVC\#svcGetInfo](SVC#svcGetInfo.md##svcGetInfo "wikilink").

For the stack mapping region, the userland randomizes a page-offset
where to start inside the region. This adds some additional entropy.

Binaries mapped by RO seems to be mapped randomly everywhere in the
entire address space. The random base address for each NRO has bits
37-12 randomized, unlike the main binary region.

For all binaries(main area / NROs), the R-- section is always located
immediately after R-X. The RW- section is always located immediately
after the R-- section. Hence, there's no extra randomization /
guard-pages for these sections.

## TLS

This is the 0x200-byte thread-local-storage, the base address is loaded
via ARM threadid register
tpidrro\_el0.

| Offset | Size  | Description                                           |
| ------ | ----- | ----------------------------------------------------- |
| 0x0    | 0x100 | [IPC](IPC%20Marshalling.md "wikilink") command buffer |
| 0x100  | 0xF8  | ?                                                     |
| 0x1F8  | 0x8   | Address of threadctx+0x58.                            |

## Thread context

This is the structure of the 0x228-byte threadctx used by official
userland
software.

| Offset | Size  | Description                                                           |
| ------ | ----- | --------------------------------------------------------------------- |
| 0x0    | 0xA8  | ?                                                                     |
| 0xA8   | 0x8   | Address of the stack-bottom-mirror which the thread was created with. |
| 0xB0   | 0x8   | Size of the stack.                                                    |
| 0xB8   | 0x178 | ?                                                                     |

# Kernel

` Granule size for TTBR0*_EL1 is 4KB.`  
` TTBR0_EL1 vmem starts at vaddr 0x0.`  
` vmem end-addr for TTBR1_EL1 is 0xffffffffffffffff. vmem start-addr for TTBR1_EL1 is 0xFFFFFFF000000000.`  
` T0SZ = 31. Hence, bit-size of the TTBR0*_EL1 vmem region is 33. (0x0000000200000000)`  
` T1SZ = 28. Hence, bit-size of the TTBR1*_EL1 vmem region is 36. (0x0000001000000000)`  
` `  
` Note: ARM config for TTBR0 is presumably configured for userland later.`  
` `  
` See arm-doc for "Table D4-25 Translation table entry addresses when using the 4KB translation granule".`  
` `  
` See arm-doc for "Overview of VMSAv8-64 address translation using the 4KB translation granule".`  
` `  
` See arm-doc for "Table D4-11 TCR.TnSZ values and IA ranges, 4K granule with no concatenation of tables".`  
` Both TTBR*_EL1 use "Initial lookup level" 1. Therefore, the TTBR*_EL1 tables are level1.`  
` `  
` Due to T*SZ, Stage1/Stage2 translation for the initial table(level1) are the same, except Stage2 uses hard-coded T0SZ.`  
` Basically, the table is accessed as: ((u64*)tablebase)[<IA[y:30]>], where y = (37-T*SZ)+26. That is, starting at bit "y" ending(inclusive) at bit30. For TTBR0*_EL1, y = 32, while for TTBR1_EL1 y = 35.`  
` Hence, for TTBR0, index=((vaddr>>30) & 0x7), and for TTBR1, index=((vaddr>>30) & 0x3f).`

## [2.0.0](2.0.0.md "wikilink")

"Vector Base Address Register (EL1)" = 0xfffffff7ffc50800.

The table for TTBR0 only contains the following:

  - Vmem 0x80000000 is mapped to physmem 0x80000000, using a size loaded
    from a register. This is only done when: "endaddr = 0x7fffffff +
    size; if(endaddr \>= 0x80000001){...}"
      - The size is loaded from: "(u32 \*0x70019050 & 0x3fff) \<\< 20;"
      - The value written to the MMU-table descriptor is: "physaddr |
        val | 0x709;". val is 1\<\<52 when "size\>\>34" is non-zero and
        when "if((physaddr & 0x3c0000000) == 0)", otherwise val=0.

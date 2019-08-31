The Kernel Loader ("KernelLdr"/"Kernelldr") was added in
[8.0.0](8.0.0.md "wikilink"). It is responsible for applying relocations
to the Kernel, and mapping the Kernel's .text/.rodata/.data/.bss at a
random slide.

# Kernel Loader

KernelLdr is called immediately by the Kernel's crt0 (after it
deprivileges from EL2 to EL1, if required), with the following
signature:

`   void KernelLoader_Main(uintptr_t kernel_base_address, KernelMap *kernel_map, uintptr_t ini1_base_address);`

## KernelLoader\_Main

  - TODO: Fill in what KernelLdr does

## Structures

### KernelMap

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
| 0x20   | 4    | INI1 load offset        |
| 0x24   | 4    | .dynamic end offset     |
| 0x28   | 4    | .init\_array end offset |
| 0x2C   | 4    | .init\_array end offset |
|        |      |                         |
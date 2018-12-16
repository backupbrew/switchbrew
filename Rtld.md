rtld, short for “runtime link-editor”, is the first executable code
belonging to the program that the system launches. This serves as the
program entry point and crt0. rtld's entry point is defined to be the
start of its .text section.

rtld is tasked with relocating the [NSOs](NSO.md "wikilink") that were
loaded in to memory by the system loader, at a random base address. To
do this, it requires that binaries include a [module
header](NSO#MOD.md##MOD "wikilink"), and a pointer to it at offset +0x04
in the .text section.

rtld receives two parameters from the system, in X0 and X1. The first
parameter should be null. The second parameter is the handle of the main
thread. See the [entrypoint
arguments](Homebrew%20ABI#Entrypoint%20Arguments.md##Entrypoint_Arguments "wikilink")
section.

rtld initially derives absolute pointers by using the BL instruction to
skip over an offset value, and then accessing and adding X30.

## Functionality

An outline of rtld's functions is below.

  - Check the first parameter. Hangs if set.
  - Clear rtld .bss.

The main function for loading all of the modules now executes.

  - Iterate over the rtld .dynamic section to establish REL, RELA,
    RELENT, RELAENT, RELCOUNT and RELACOUNT.
  - With the above information, process relative relocations
    (R\_AARCH64\_RELATIVE) on rtld.
  - rtld initializes load lists and a module object for itself, which
    formalizes loading of the rtld .dynamic section.
  - Prepare to iterate over all modules. rtld does this by scanning
    memory using
    [svcQueryMemory](SVC#svcQueryMemory.md##svcQueryMemory "wikilink").
    The memory must be R-X and STATIC. If the address matches the rtld
    base address, the module is skipped here.
  - Each valid memory region is read, and must contain 'MOD0' magic at
    offset +0x04. If this check fails, rtld hangs.
  - Read the .dynamic and .bss pointers from the module header. If the
    .bss pointers are unequal, rtld clears the .bss for this module.
  - Initialize a module object for this module, using the same function
    that was used to initialize an object for rtld itself. This object
    is typically stored in the module's .bss, via another pointer in the
    module header.
  - Process relative relocations for this module.
  - Update list pointers for the rtld lists and the module object.
  - Prepare for next iteration - the next memory query address is
    calculated by adding the size of the current memory region to the
    current address.
  - Once all modules are loaded, rtld resolves symbols. The full list of
    supported relocation types is available below. This uses the
    .dynsym, .dynstr and .hash sections.

Once the above function returns, rtld serves as a general initialization
routine for the program.

  - Initializes the standard library “musl”.
  - Initializes the SDK. The second parameter (thread handle) passed to
    rtld is passed to this function.
  - Calls program-defined initialization routine.
  - Calls each module's initialization function.
  - Calls program main().
  - Finalizes the SDK.
  - Jumps to
    [svcExitProcess](SVC#svcExitProcess.md##svcExitProcess "wikilink").

## Relocation types

| Value | Name                   |
| ----- | ---------------------- |
| 257   | R\_AARCH64\_ABS64      |
| 1025  | R\_AARCH64\_GLOB\_DAT  |
| 1026  | R\_AARCH64\_JUMP\_SLOT |
| 1027  | R\_AARCH64\_RELATIVE   |

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

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

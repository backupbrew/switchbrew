This is the 0x200-byte TLS (thread local storage). It's base address is
loaded via ARM threadid register tpidrro\_el0. TLS for multiple threads
are stored in the same page, with the first TLS normally located at
page+0x200, because the first TLS spot is reserved for usermode
exception
handling.

# Structure

| Offset | Size  | Description                                                                                           |
| ------ | ----- | ----------------------------------------------------------------------------------------------------- |
| 0x0    | 0x100 | [IPC](IPC%20Marshalling.md "wikilink") command buffer.                                                |
| 0x100  | 0xF8  | Unknown.                                                                                              |
| 0x1F8  | 0x8   | Pointer to [thread context](Thread%20Local%20Storage#Thread%20context.md##Thread_context "wikilink"). |

# Userland context

## Boot paramter

This is "nn::os::detail::g\_OsBootParamter".

| Offset | Size | Description         |
| ------ | ---- | ------------------- |
| 0x00   | 0x04 | Main thread handle. |
| 0x04   | 0x04 | Always 0.           |
| 0x08   | 0x30 | Empty.              |

## Resource manager storage

This is
"nn::os::detail::g\_OsResourceManagerStorage".

| Offset | Size  | Description                                                                                                                                                                                            |
| ------ | ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 0x00   | 0x04  | Always 0.                                                                                                                                                                                              |
| 0x04   | 0x10  | Process PRNG.                                                                                                                                                                                          |
| 0x14   | 0x04  | Padding.                                                                                                                                                                                               |
| 0x18   | 0x08  | Always set to 0.                                                                                                                                                                                       |
| 0x20   | 0x08  | [AddressSpaceStart](SVC#svcGetInfo.md##svcGetInfo "wikilink") right shifted by 0x0C.                                                                                                                   |
| 0x28   | 0x08  | AddressSpaceEnd ([AddressSpaceStart](SVC#svcGetInfo.md##svcGetInfo "wikilink") + [AddressSpaceSize](SVC#svcGetInfo.md##svcGetInfo "wikilink")) right shifted by 0x0C and aligned to AddressSpaceAlign. |
| 0x30   | 0x08  | AddressSpaceAlign right shifted by 0x0C.                                                                                                                                                               |
| 0x38   | 0x08  | Always 0.                                                                                                                                                                                              |
| 0x40   | 0x08  | Always set to 0.                                                                                                                                                                                       |
| 0x48   | 0x08  | [MapRegionBased](SVC#svcGetInfo.md##svcGetInfo "wikilink") right shifted by 0x0C.                                                                                                                      |
| 0x50   | 0x08  | MapRegionEnd ([MapRegionBased](SVC#svcGetInfo.md##svcGetInfo "wikilink") + [MapRegionSize](SVC#svcGetInfo.md##svcGetInfo "wikilink")) right shifted by 0x0C and aligned to MapRegionAlign.             |
| 0x58   | 0x08  | MapRegionAlign right shifted by 0x0C.                                                                                                                                                                  |
| 0x60   | 0x08  | Always 0.                                                                                                                                                                                              |
| 0x68   | 0x08  | Always 0.                                                                                                                                                                                              |
| 0x70   | 0x1D0 | Main [thread context](Thread%20Local%20Storage#Thread%20context.md##Thread_context "wikilink").                                                                                                        |
| 0x240  | 0x08  | Pointer to main [thread context](Thread%20Local%20Storage#Thread%20context.md##Thread_context "wikilink").                                                                                             |
| 0x248  | 0x08  | Unknown.                                                                                                                                                                                               |
| 0x250  | 0x08  | Unknown.                                                                                                                                                                                               |
| 0x258  | 0x130 | Always empty?                                                                                                                                                                                          |
| 0x388  | 0x08  | Pointer to [resource manager storage](Thread%20Local%20Storage#Resource%20manager%20storage.md##Resource_manager_storage "wikilink") + 0x388.                                                          |
| 0x390  | 0x08  | Pointer to [resource manager storage](Thread%20Local%20Storage#Resource%20manager%20storage.md##Resource_manager_storage "wikilink") + 0x388.                                                          |
| 0x398  | 0x08  | Always 0.                                                                                                                                                                                              |
| 0x3A0  | 0x08  | Always 0.                                                                                                                                                                                              |

## Thread context

This structure is used for describing each thread's context. In the main
thread's case, this structure comes from the [resource manager
storage](Thread%20Local%20Storage#Resource%20manager%20storage.md##Resource_manager_storage "wikilink").

| Offset | Size  | Description                                                                                                   |
| ------ | ----- | ------------------------------------------------------------------------------------------------------------- |
| 0x00   | 0x08  | Pointer to [thread context](Thread%20Local%20Storage#Thread%20context.md##Thread_context "wikilink") + 0x1C8. |
| 0x08   | 0x08  | Unknown.                                                                                                      |
| 0x10   | 0x08  | Pointer to [thread context](Thread%20Local%20Storage#Thread%20context.md##Thread_context "wikilink") + 0x10.  |
| 0x18   | 0x08  | Pointer to [thread context](Thread%20Local%20Storage#Thread%20context.md##Thread_context "wikilink") + 0x10.  |
| 0x20   | 0x20  | Empty.                                                                                                        |
| 0x40   | 0x04  | Thread status.                                                                                                |
| 0x44   | 0x04  | Thread priority minus 0x1C.                                                                                   |
| 0x48   | 0x08  | Thread stack base address.                                                                                    |
| 0x50   | 0x08  | Thread stack base address mirror.                                                                             |
| 0x58   | 0x08  | Thread stack size.                                                                                            |
| 0x60   | 0x08  | Unknown.                                                                                                      |
| 0x68   | 0x08  | Unknown.                                                                                                      |
| 0x70   | 0x08  | Always 0?                                                                                                     |
| 0x78   | 0x08  | Always 0?                                                                                                     |
| 0x80   | 0x08  | Always 0?                                                                                                     |
| 0x88   | 0x100 | Initially empty (contains unknown pointers).                                                                  |
| 0x188  | 0x20  | Thread name.                                                                                                  |
| 0x1A8  | 0x08  | Thread name address.                                                                                          |
| 0x1B0  | 0x04  | Always 0.                                                                                                     |
| 0x1B4  | 0x04  | Always 0.                                                                                                     |
| 0x1B8  | 0x04  | Thread handle.                                                                                                |
| 0x1BC  | 0x04  | Always 0.                                                                                                     |
| 0x1C0  | 0x08  | Thread global mutex.                                                                                          |
| 0x1C8  | 0x08  | Unknown.                                                                                                      |

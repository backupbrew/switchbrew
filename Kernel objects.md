# KAutoObject

Size: 0x10

| Offset | Type | Description    |
| ------ | ---- | -------------- |
| 0      | \*   | Vtable         |
| 8      | u64  | ReferenceCount |

# KSynchronizationObject

Size: 0x20

Inherits from: [\#KAutoObject](#KAutoObject "wikilink")

| Offset | Type                                     | Description    |
| ------ | ---------------------------------------- | -------------- |
| 0      | [\#KAutoObject](#KAutoObject "wikilink") |                |
| 0x10   | u64                                      | ThreadSyncNum  |
| 0x18   | LinkedListNode\*                         | ThreadSyncList |

# KProcess

Size: 0x5B0

Inherits from:
[\#KSynchronizationObject](#KSynchronizationObject "wikilink")

| Offset | Type                                                           | Description   |
| ------ | -------------------------------------------------------------- | ------------- |
| 0      | [\#KSynchronizationObject](#KSynchronizationObject "wikilink") |               |
| 0x28   |                                                                |               |
| 0x38   | [\#KProcessMm](#KProcessMm "wikilink")                         | MemoryManager |
| 0xF0   | u64                                                            | TotalMemUsage |
| 0xF8   | u64                                                            |               |
| ..     | ..                                                             | ..            |
| 0x100  | KLinkedListNode\*                                              | TlsPagesList  |
| ..     | ..                                                             | ..            |
| 0x130  |                                                                | ProcessMutex  |
| ..     | ..                                                             | ..            |
| 0x288  | KProcessHandleTable                                            | HandleTable   |

## KProcessMm

| Offset | Type           | Description       |
| ------ | -------------- | ----------------- |
| 0      | \*             | Vtable            |
| 8      | u64            | AddrSpaceMinAddr  |
| 0x10   | u64            | AddrSpaceMaxAddr  |
| 0x18   | u64            | HeapBaseAddr      |
| 0x20   | u64            | HeapEndAddr       |
| 0x28   | u64            | HeapCurAddr       |
| 0x30   | u64            | MapRegionBaseAddr |
| 0x38   | u64            | MapRegionEnd      |
| 0x40   | u64            | HeapMaxAllocation |
| 0x48   | KRecursiveLock | Mutex             |
| ..     | ..             | ..                |

## KTransferMemory

Size: 0x48

Inherits from: [\#KAutoObject](#KAutoObject "wikilink")

| Offset | Type                                     | Description  |
| ------ | ---------------------------------------- | ------------ |
| 0      | [\#KAutoObject](#KAutoObject "wikilink") |              |
| 0x10   | KMemoryBlockList                         | Blocks       |
| 0x28   | [\#KProcess](#KProcess "wikilink")\*     | OwnerProcess |
| 0x30   | u64                                      | BaseAddress  |
| 0x40   | int                                      | Permission   |
| 0x44   | bool                                     | HasInited    |

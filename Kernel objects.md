# KAutoObject

Size: 0x10

| Offset | Type | Description    |
| ------ | ---- | -------------- |
| 0      | \*   | Vtable         |
| 8      | u64  | ReferenceCount |

# KSynchronizationObject

Size: 0x28

Inherits from:
[\#KAutoObject](#KAutoObject "wikilink")

| Offset | Type                                             | Description    |
| ------ | ------------------------------------------------ | -------------- |
| 0      | [\#KAutoObject](#KAutoObject "wikilink")         |                |
| 0x10   | u64                                              | ThreadSyncNum  |
| 0x18   | [\#KLinkedListNode](#KLinkedListNode "wikilink") | ThreadSyncList |

# KLinkedListNode

Size:
0x10

| Offset | Type                                               | Description |
| ------ | -------------------------------------------------- | ----------- |
| 0      | [\#KLinkedListNode](#KLinkedListNode "wikilink")\* | Prev        |
| 8      | [\#KLinkedListNode](#KLinkedListNode "wikilink")\* | Next        |

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
| 0x100  | [\#KLinkedListNode](#KLinkedListNode "wikilink")\*             | TlsPagesList  |
| ..     | ..                                                             | ..            |
| 0x130  | KRecursiveLock                                                 | ProcessMutex  |
| ..     | ..                                                             | ..            |
| 0x288  | KProcessHandleTable                                            | HandleTable   |

## KProcessMm

| Offset | Type                                         | Description       |
| ------ | -------------------------------------------- | ----------------- |
| 0      | \*                                           | Vtable            |
| 8      | u64                                          | AddrSpaceMinAddr  |
| 0x10   | u64                                          | AddrSpaceMaxAddr  |
| 0x18   | u64                                          | HeapBaseAddr      |
| 0x20   | u64                                          | HeapEndAddr       |
| 0x28   | u64                                          | HeapCurAddr       |
| 0x30   | u64                                          | MapRegionBaseAddr |
| 0x38   | u64                                          | MapRegionEnd      |
| 0x40   | u64                                          | HeapMaxAllocation |
| 0x48   | KRecursiveLock                               | Mutex             |
| 0x50   |                                              |                   |
| 0x60   | [\#KMemoryBlock](#KMemoryBlock "wikilink")\* | MemoryBlockList   |
| ..     | ..                                           | ..                |

## KMemoryBlock

Size:
0x40

| Offset | Type                                         | Description       |
| ------ | -------------------------------------------- | ----------------- |
| 0      | [\#KMemoryBlock](#KMemoryBlock "wikilink")\* | Next              |
| 8      | [\#KMemoryBlock](#KMemoryBlock "wikilink")\* | Prev              |
| 0x10   |                                              |                   |
| 0x18   |                                              |                   |
| 0x20   | u64                                          | BaseAddress       |
| 0x28   | u64                                          | NumOfPages        |
| 0x30   | u32                                          | State             |
| 0x34   | u16                                          | IpcRefCount \[?\] |
| 0x36   | u16                                          | DeviceMapRefCount |
| 0x38   | u8                                           | Permission        |
| 0x39   | u8                                           | UnkAttribute      |
| 0x3A   | u8                                           | Attribute         |

## KMemoryBlockInfo

Size: 0x20

| Offset | Type | Description       |
| ------ | ---- | ----------------- |
| 0      | u64  | BaseAddress       |
| 8      | u64  | Size              |
| 0x10   | u32  | State             |
| 0x14   | u8   | Permission        |
| 0x15   | u8   | Attribute         |
| 0x16   | u8   | UnkAttribute      |
|        |      | Pad               |
| 0x18   | u16  | IpcRefCount \[?\] |
| 0x1A   | u16  | DeviceMapRefCount |

# KTransferMemory

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

# KSharedMemory

Size: 0x40

Inherits from: [\#KAutoObject](#KAutoObject "wikilink")

| Offset | Type                                     | Description  |
| ------ | ---------------------------------------- | ------------ |
| 0      | [\#KAutoObject](#KAutoObject "wikilink") |              |
| 0x10   | KMemoryBlockList                         | Blocks       |
| 0x28   | [\#KProcess](#KProcess "wikilink")\*     | OwnerProcess |
| 0x30   | int                                      | LocalPerm    |
| 0x34   | int                                      | RemotePerm   |
| 0x38   | bool                                     | HasInited    |

# KPort

Size: 0xA8

Inherits from: [\#KAutoObject](#KAutoObject "wikilink")

| Offset | Type                                     | Description   |
| ------ | ---------------------------------------- | ------------- |
| 0      | [\#KAutoObject](#KAutoObject "wikilink") |               |
| 0x10   | [\#KServerPort](#KServerPort "wikilink") | ServerPort    |
| 0x60   | [\#KClientPort](#KClientPort "wikilink") | ClientPort    |
| 0x98   | u64                                      |               |
| 0xA0   | bool                                     | HasInited     |
| 0xA1   | bool                                     | IsLight \[?\] |

## KServerPort

Size: 0x50

Inherits from:
[\#KSynchronizationObject](#KSynchronizationObject "wikilink")

| Offset | Type                                                           | Description |
| ------ | -------------------------------------------------------------- | ----------- |
| 0      | [\#KSynchronizationObject](#KSynchronizationObject "wikilink") |             |
| 0x28   | [\#KLinkedListNode](#KLinkedListNode "wikilink")               |             |
| 0x38   | [\#KLinkedListNode](#KLinkedListNode "wikilink")               |             |
| 0x48   | [\#KPort](#KPort "wikilink")\*                                 | Parent      |

## KClientPort

Size: 0x38

Inherits from:
[\#KSynchronizationObject](#KSynchronizationObject "wikilink")

| Offset | Type                                                           | Description       |
| ------ | -------------------------------------------------------------- | ----------------- |
| 0      | [\#KSynchronizationObject](#KSynchronizationObject "wikilink") |                   |
| 0x28   | ?                                                              |                   |
| 0x2C   | u32                                                            | MaxSessions \[?\] |
| 0x30   | [\#KPort](#KPort "wikilink")\*                                 | Parent            |

# KEvent

Size: 0x70

Inherits from:
[\#KAutoObject](#KAutoObject "wikilink")

| Offset | Type                                           | Description   |
| ------ | ---------------------------------------------- | ------------- |
| 0      | [\#KAutoObject](#KAutoObject "wikilink")       |               |
| 0x10   | [\#KReadableEvent](#KReadableEvent "wikilink") | ReadableEvent |
| 0x48   | [\#KWritableEvent](#KWritableEvent "wikilink") | WritableEvent |
| 0x60   | [\#KProcess](#KProcess "wikilink")\*           | Creator       |
| 0x68   | bool                                           | HasInited     |

## KReadableEvent

Size: 0x38

Inherits from:
[\#KSynchronizationEvent](#KSynchronizationEvent "wikilink")

| Offset | Type                                                           | Description |
| ------ | -------------------------------------------------------------- | ----------- |
| 0      | [\#KSynchronizationObject](#KSynchronizationObject "wikilink") |             |
| 0x28   | bool                                                           |             |
| 0x30   | [\#KEvent](#KEvent "wikilink")\*                               | Parent      |

## KWritableEvent

Size: 0x18

Inherits from: [\#KAutoObject](#KAutoObject "wikilink")

| Offset | Type                                     | Description |
| ------ | ---------------------------------------- | ----------- |
| 0      | [\#KAutoObject](#KAutoObject "wikilink") |             |
| 0x10   | [\#KEvent](#KEvent "wikilink")\*         | Parent      |

## KInterruptEvent

Size: 0x50

Inherits from:
[\#KReadableEvent](#KReadableEvent "wikilink")

| Offset | Type                                           | Description   |
| ------ | ---------------------------------------------- | ------------- |
| 0      | [\#KReadableEvent](#KReadableEvent "wikilink") |               |
| 0x38   |                                                |               |
| 0x48   | u32                                            | IrqId (or -1) |

# KAddressSpace

Size: 0x70

Inherits from: [\#KAutoObject](#KAutoObject "wikilink")

| Offset | Type                                       | Description |
| ------ | ------------------------------------------ | ----------- |
| 0      | [\#KAutoObject](#KAutoObject "wikilink")   |             |
| 0x10   | KRecursiveLock                             | Mutex       |
| 0x18   | [\#KSmmuManager](#KSmmuManager "wikilink") | Manager     |
| 0x58   | u64                                        | BaseAddress |
| 0x60   | u64                                        | Size        |
| 0x68   | bool                                       | HasInited   |

## KSmmuManager

Size: 0x40

| Offset | Type        | Description         |
| ------ | ----------- | ------------------- |
| 0      | u8\[4\]     | PageTableAsids      |
| 8      | void\*\[4\] | PageDirectories     |
| 0x28   | u64         | AttachedDevicesMask |
| 0x30   | u32         | RegVal32Bit         |
| 0x34   | u32         | RegVal32BitEmpty    |
| 0x38   | u32         | RegVal36Bit         |
| 0x3C   | u32         | RegVal36BitEmpty    |

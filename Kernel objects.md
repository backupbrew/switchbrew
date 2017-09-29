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
| 0      | [\#KAutoObject](#KAutoObject "wikilink")         | Inheritance    |
| 0x10   | u64                                              | ThreadSyncNum  |
| 0x18   | [\#KLinkedListNode](#KLinkedListNode "wikilink") | ThreadSyncList |

# KRecursiveLock

Size: 0x8

| Offset | Type | Description |
| ------ | ---- | ----------- |
| 0      | u64  | OwnerTag    |

# KSpinLock

Size: 0x1

| Offset | Type | Description |
| ------ | ---- | ----------- |
| 0      | u8   | IsBusy      |

# KLockedList

Size:
0x28

| Offset | Type                                             | Description |
| ------ | ------------------------------------------------ | ----------- |
| 0      | u64                                              | Count       |
| 8      | [\#KLinkedListNode](#KLinkedListNode "wikilink") | List        |
| 0x18   | [\#KRecursiveLock](#KRecursiveLock "wikilink")   | Mutex       |
| 0x20   | u64                                              | MaxCount    |

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

| Offset | Type                                                                                 | Description                   |
| ------ | ------------------------------------------------------------------------------------ | ----------------------------- |
| 0      | [\#KSynchronizationObject](#KSynchronizationObject "wikilink")                       | Inheritance                   |
| 0x28   |                                                                                      |                               |
| 0x38   | [\#KMemoryManager](#KMemoryManager "wikilink")                                       | MemoryManager                 |
| 0xF0   | u64                                                                                  | TotalMemUsage                 |
| 0xF8   | u64                                                                                  | TlsPagesListCount             |
| 0x100  | [\#KLinkedListNode](#KLinkedListNode "wikilink")                                     | TlsPagesList                  |
| 0x110  | s32                                                                                  | DefaultCpuCore                |
| 0x118  | KDebug\*                                                                             | Debug                         |
| 0x120  | [\#KResourceLimit](#KResourceLimit "wikilink")\*                                     | ResourceLimit                 |
| 0x128  | u32                                                                                  | State                         |
| 0x130  | [\#KRecursiveLock](#KRecursiveLock "wikilink")                                       | ProcessMutex                  |
| 0x138  | [\#KRecursiveLock](#KRecursiveLock "wikilink")                                       | ThreadingMutex                |
| 0x140  | [\#KLinkedListNode](#KLinkedListNode "wikilink")\<[\#KThread](#KThread "wikilink")\> | ThreadArbiterList             |
| 0x150  | KLinkedListNode                                                                      |                               |
| 0x160  | u64\[4\]                                                                             | RandomEntropy                 |
| 0x180  | u8                                                                                   | HasStateChanged               |
| 0x181  | u8                                                                                   | HasInitialized                |
| 0x182  | u8                                                                                   | IsSystem                      |
| 0x183  | u8\[12\]                                                                             | From\_CreateProcessInfo\_0    |
| 0x18F  | u8                                                                                   | InitiallyZero                 |
| 0x190  | u16                                                                                  | NumberOfCreatedThreads        |
| 0x192  | u16                                                                                  | ThreadingRelatedInitiallyZero |
| 0x194  | u32                                                                                  | ProcessFlags                  |
| 0x198  | [\#KProcessCapabilities](#KProcessCapabilities "wikilink")                           | Capabilities                  |
| 0x248  | u64                                                                                  | TitleId                       |
| 0x250  | u64                                                                                  | ProcessId                     |
| 0x258  | u64                                                                                  | CreatedTickstamp              |
| 0x260  | u64                                                                                  | Entrypoint                    |
| 0x268  | u64                                                                                  | CodeMemUsage                  |
| 0x270  | u64                                                                                  | DynamicMemUsage               |
| 0x278  | u64                                                                                  | MaxTotalMemUsage              |
| 0x280  | u64                                                                                  | From\_CreateProcessInfo\_0xC  |
| 0x288  | [\#KProcessHandleTable](#KProcessHandleTable "wikilink")                             | HandleTable                   |
| 0x528  | void\*                                                                               | UsermodeExceptionTlsArea      |
| 0x530  | [\#KLinkedListNode](#KLinkedListNode "wikilink")\<[\#KThread](#KThread "wikilink")\> | ExceptionThreadList           |
| 0x540  | [\#KThread](#KThread "wikilink")\*                                                   | ExceptionThread               |
| 0x548  | [\#KLinkedListNode](#KLinkedListNode "wikilink")\<[\#KThread](#KThread "wikilink")\> | ThreadList                    |
| 0x558  | u32                                                                                  |                               |
| 0x55C  | u32                                                                                  | HasStarted                    |
| 0x560  | u64\[8\]                                                                             |                               |
| 0x5A0  | u64                                                                                  |                               |
| 0x5A8  | u64                                                                                  |                               |

## KProcessCapabilities

Size: 0xB0

| Offset | Type      | Description              |
| ------ | --------- | ------------------------ |
| 0      | u8\[16\]  | SvcAccessMask            |
| 0x10   | u8\[128\] | IrqAccessMask            |
| 0x90   | u64       | AllowedCpuIdBitmask      |
| 0x98   | u64       | AllowedThreadPrioBitmask |
| 0xA0   | u32       | DebuggingFlags           |
| 0xA4   | u32       | HandleTableSize          |
| 0xA8   | u32       | KernelReleaseVersion     |
| 0xAC   | u32       | ApplicationType          |

## KProcessHandleTable

Size:
0x2A0

| Offset | Type                                             | Description    |
| ------ | ------------------------------------------------ | -------------- |
| 0      | [\#KHandleEntry](#KHandleEntry "wikilink")\*     | TablePtr       |
| 8      | [\#KHandleEntry](#KHandleEntry "wikilink")\*     | NextFreeEntry  |
| 0x10   | [\#KHandleEntry](#KHandleEntry "wikilink")\[40\] | InternalTable  |
| 0x290  | u16                                              | Size           |
| 0x292  | u16                                              |                |
| 0x294  | u16                                              | IdCounter      |
| 0x296  | u16                                              | NumActiveSlots |
| 0x298  | [\#KSpinLock](#KSpinLock "wikilink")             | Lock           |

### KHandleEntry

| Offset | Type                                       | Description |
| ------ | ------------------------------------------ | ----------- |
| 0      | u16                                        | HandleId    |
| 2      | u8                                         | ObjectType  |
| 8      | [\#KAutoObject](#KAutoObject "wikilink")\* | Object      |

# KMemoryManager

Size:
0xB8

| Offset | Type                                                     | Description                         |
| ------ | -------------------------------------------------------- | ----------------------------------- |
| 0      | \*                                                       | Vtable                              |
| 8      | u64                                                      | AddrSpaceMinAddr                    |
| 0x10   | u64                                                      | AddrSpaceMaxAddr                    |
| 0x18   | u64                                                      | HeapRegionBaseAddr                  |
| 0x20   | u64                                                      | HeapRegionEndAddr                   |
| 0x28   | u64                                                      | HeapCurAddr                         |
| 0x30   | u64                                                      | MapRegionBaseAddr                   |
| 0x38   | u64                                                      | MapRegionEnd                        |
| 0x40   | u64                                                      | HeapMaxAllocation                   |
| 0x48   | [\#KRecursiveLock](#KRecursiveLock "wikilink")           | Mutex                               |
| 0x50   | [\#KPageTable](#KPageTable "wikilink")                   | PageTable                           |
| 0x60   | [\#KMemoryBlockManager](#KMemoryBlockManager "wikilink") | MemoryBlockManager                  |
| 0x78   | bool                                                     | IsKernel                            |
| 0x79   | bool                                                     | IsSystem                            |
| 0x7A   | bool                                                     | IsAddrSpace36Bit                    |
| 0x7B   | bool                                                     | HasAslr                             |
| 0x7C   | u32                                                      | Is\_0x59\_If\_Cfg12\_Bit0\_ElseZero |
| 0x80   | u32                                                      | Is\_0x5A\_If\_Cfg12\_Bit0\_ElseZero |
| 0x84   | u32                                                      | Is\_0x58\_If\_Cfg12\_Bit0\_ElseZero |
| 0x88   |                                                          |                                     |
| 0x90   |                                                          |                                     |
| 0x98   |                                                          |                                     |
| 0xA0   | u64                                                      | TranslationTableBaseRegister0       |
| 0xA8   | u64                                                      | TranslationControlRegister          |
| 0xB0   | u8                                                       | AsidTagValue                        |

## KPageTable

Size: 0x10

| Offset | Type   | Description       |
| ------ | ------ | ----------------- |
| 0      | void\* | RawPageTablePtr   |
| 8      | bool   |                   |
| 0xC    | u32    | AddrSpaceSizeInGb |

## KMemoryBlockManager

Size:
0x18

| Offset | Type                                         | Description     |
| ------ | -------------------------------------------- | --------------- |
| 0      | [\#KMemoryBlock](#KMemoryBlock "wikilink")\* | MemoryBlockList |
| 8      | u64                                          | MaxAddr         |
| 0x10   | u64                                          | MinAddr         |

## KMemoryBlock

Size:
0x40

| Offset | Type                                                                                           | Description                |
| ------ | ---------------------------------------------------------------------------------------------- | -------------------------- |
| 0      | [\#KLinkedListNode](#KLinkedListNode "wikilink")\<[\#KMemoryBlock](#KMemoryBlock "wikilink")\> | NodeFor\_\_MemoryBlockList |
| 0x10   |                                                                                                |                            |
| 0x18   |                                                                                                |                            |
| 0x20   | u64                                                                                            | BaseAddress                |
| 0x28   | u64                                                                                            | NumOfPages                 |
| 0x30   | u32                                                                                            | State                      |
| 0x34   | u16                                                                                            | IpcRefCount \[?\]          |
| 0x36   | u16                                                                                            | DeviceMapRefCount          |
| 0x38   | u8                                                                                             | Permission                 |
| 0x39   | u8                                                                                             | UnkAttribute               |
| 0x3A   | u8                                                                                             | Attribute                  |

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
| 0x18   | u16  | IpcRefCount \[?\] |
| 0x1A   | u16  | DeviceMapRefCount |

# KTransferMemory

Size: 0x48

Inherits from: [\#KAutoObject](#KAutoObject "wikilink")

| Offset | Type                                     | Description  |
| ------ | ---------------------------------------- | ------------ |
| 0      | [\#KAutoObject](#KAutoObject "wikilink") | Inheritance  |
| 0x10   | KMemoryBlockList                         | Blocks       |
| 0x28   | [\#KProcess](#KProcess "wikilink")\*     | OwnerProcess |
| 0x30   | u64                                      | BaseAddress  |
| 0x38   | KRecursiveLock                           | Mutex        |
| 0x40   | int                                      | Permission   |
| 0x44   | bool                                     | HasInited    |
| 0x45   | bool                                     | IsMapped     |

# KSharedMemory

Size: 0x40

Inherits from: [\#KAutoObject](#KAutoObject "wikilink")

| Offset | Type                                     | Description      |
| ------ | ---------------------------------------- | ---------------- |
| 0      | [\#KAutoObject](#KAutoObject "wikilink") | Inheritance      |
| 0x10   | KMemoryBlockList                         | Blocks           |
| 0x28   | [\#KProcess](#KProcess "wikilink")\*     | OwnerProcess     |
| 0x30   | int                                      | LocalPermission  |
| 0x34   | int                                      | RemotePermission |
| 0x38   | bool                                     | HasInited        |

# KPort

Size: 0xA8

Inherits from: [\#KAutoObject](#KAutoObject "wikilink")

| Offset | Type                                     | Description |
| ------ | ---------------------------------------- | ----------- |
| 0      | [\#KAutoObject](#KAutoObject "wikilink") | Inheritance |
| 0x10   | [\#KServerPort](#KServerPort "wikilink") | ServerSide  |
| 0x60   | [\#KClientPort](#KClientPort "wikilink") | ClientSide  |
| 0x98   | u64                                      |             |
| 0xA0   | bool                                     | HasInited   |
| 0xA1   | bool                                     | IsLight     |

## KServerPort

Size: 0x50

Inherits from:
[\#KSynchronizationObject](#KSynchronizationObject "wikilink")

| Offset | Type                                                           | Description              |
| ------ | -------------------------------------------------------------- | ------------------------ |
| 0      | [\#KSynchronizationObject](#KSynchronizationObject "wikilink") | Inheritance              |
| 0x28   | [\#KLinkedListNode](#KLinkedListNode "wikilink")               | IncomingConnections      |
| 0x38   | [\#KLinkedListNode](#KLinkedListNode "wikilink")               | IncomingLightConnections |
| 0x48   | [\#KPort](#KPort "wikilink")\*                                 | Parent                   |

## KClientPort

Size: 0x38

Inherits from:
[\#KSynchronizationObject](#KSynchronizationObject "wikilink")

| Offset | Type                                                           | Description |
| ------ | -------------------------------------------------------------- | ----------- |
| 0      | [\#KSynchronizationObject](#KSynchronizationObject "wikilink") | Inheritance |
| 0x28   | u32                                                            | NumSessions |
| 0x2C   | u32                                                            | MaxSessions |
| 0x30   | [\#KPort](#KPort "wikilink")\*                                 | Parent      |

# KSession

Size: 0xB0

Inherits from:
[\#KAutoObject](#KAutoObject "wikilink")

| Offset | Type                                           | Description |
| ------ | ---------------------------------------------- | ----------- |
| 0      | [\#KAutoObject](#KAutoObject "wikilink")       | Inheritance |
| 0x10   | [\#KServerSession](#KServerSession "wikilink") | ServerSide  |
| 0x70   | [\#KClientSession](#KClientSession "wikilink") | ClientSide  |
| 0xA8   | bool                                           | HasInited   |

## KServerSession

Size: 0x60

Inherits from:
[\#KSynchronizationObject](#KSynchronizationObject "wikilink")

| Offset | Type                                                           | Description                    |
| ------ | -------------------------------------------------------------- | ------------------------------ |
| 0      | [\#KSynchronizationObject](#KSynchronizationObject "wikilink") | Inheritance                    |
| 0x28   | KLinkedListNode                                                | NodeFor\_\_IncomingConnections |
| 0x38   |                                                                |                                |
| 0x40   | KLinkedListNode                                                |                                |
| 0x50   |                                                                |                                |
| 0x58   |                                                                |                                |

## KClientSession

Size: 0x38

Inherits from: [\#KAutoObject](#KAutoObject "wikilink")

| Offset | Type                                       | Description    |
| ------ | ------------------------------------------ | -------------- |
| 0      | [\#KAutoObject](#KAutoObject "wikilink")   | Inheritance    |
| 0x10   | [\#KSession](#KSession "wikilink")\*       | Parent         |
| 0x18   | bool                                       | HasInited      |
| 0x20   | [\#KClientPort](#KClientPort "wikilink")\* | ParentPort     |
| 0x28   |                                            |                |
| 0x30   | [\#KProcess](#KProcess "wikilink")\*       | CreatorProcess |

# KLightSession

Size: 0xA8

Inherits from:
[\#KAutoObject](#KAutoObject "wikilink")

| Offset | Type                                                     | Description |
| ------ | -------------------------------------------------------- | ----------- |
| 0      | [\#KAutoObject](#KAutoObject "wikilink")                 | Inheritance |
| 0x10   | [\#KLightSessionServer](#KLightSessionServer "wikilink") | ServerSide  |
| 0x68   | [\#KLightSessionClient](#KLightSessionClient "wikilink") | ClientSide  |
| 0xA0   | bool                                                     | HasInited   |

## KLightServerSession

Size: 0x58

Inherits from:
[\#KAutoObject](#KAutoObject "wikilink")

| Offset | Type                                         | Description                         |
| ------ | -------------------------------------------- | ----------------------------------- |
| 0      | [\#KAutoObject](#KAutoObject "wikilink")     | Inheritance                         |
| 0x10   | KLinkedListNode                              | NodeFor\_\_IncomingLightConnections |
| 0x20   | [\#KLightSession](#KLightSession "wikilink") | Parent                              |
| 0x28   | u64\[6\]                                     |                                     |

## KLightClientSession

Size: 0x38

Inherits from:
[\#KAutoObject](#KAutoObject "wikilink")

| Offset | Type                                           | Description    |
| ------ | ---------------------------------------------- | -------------- |
| 0      | [\#KAutoObject](#KAutoObject "wikilink")       | Inheritance    |
| 0x10   | [\#KLightSession](#KLightSession "wikilink")\* | Parent         |
| 0x18   | bool                                           | HasInited      |
| 0x20   | [\#KClientPort](#KClientPort "wikilink")\*     | Port           |
| 0x28   |                                                |                |
| 0x30   | [\#KProcess](#KProcess "wikilink")\*           | CreatorProcess |

# KEvent

Size: 0x70

Inherits from:
[\#KAutoObject](#KAutoObject "wikilink")

| Offset | Type                                           | Description   |
| ------ | ---------------------------------------------- | ------------- |
| 0      | [\#KAutoObject](#KAutoObject "wikilink")       | Inheritance   |
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
| 0      | [\#KSynchronizationObject](#KSynchronizationObject "wikilink") | Inheritance |
| 0x28   | bool                                                           |             |
| 0x30   | [\#KEvent](#KEvent "wikilink")\*                               | Parent      |

## KWritableEvent

Size: 0x18

Inherits from: [\#KAutoObject](#KAutoObject "wikilink")

| Offset | Type                                     | Description |
| ------ | ---------------------------------------- | ----------- |
| 0      | [\#KAutoObject](#KAutoObject "wikilink") | Inheritance |
| 0x10   | [\#KEvent](#KEvent "wikilink")\*         | Parent      |

## KInterruptEvent

Size: 0x50

Inherits from:
[\#KReadableEvent](#KReadableEvent "wikilink")

| Offset | Type                                           | Description   |
| ------ | ---------------------------------------------- | ------------- |
| 0      | [\#KReadableEvent](#KReadableEvent "wikilink") | Inheritance   |
| 0x38   |                                                |               |
| 0x48   | u32                                            | IrqId (or -1) |

# KDeviceAddressSpace

Size: 0x70

Inherits from:
[\#KAutoObject](#KAutoObject "wikilink")

| Offset | Type                                           | Description |
| ------ | ---------------------------------------------- | ----------- |
| 0      | [\#KAutoObject](#KAutoObject "wikilink")       | Inheritance |
| 0x10   | [\#KRecursiveLock](#KRecursiveLock "wikilink") | Mutex       |
| 0x18   | [\#KSmmuManager](#KSmmuManager "wikilink")     | Manager     |
| 0x58   | u64                                            | BaseAddress |
| 0x60   | u64                                            | Size        |
| 0x68   | bool                                           | HasInited   |

\[1.0.0\] It was called KAddressSpace.

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

# KResourceLimit

Size: 0x68

Inherits from:
[\#KAutoObject](#KAutoObject "wikilink")

| Offset | Type                                           | Description  |
| ------ | ---------------------------------------------- | ------------ |
| 0      | [\#KAutoObject](#KAutoObject "wikilink")       | Inheritance  |
| 0x10   | u64\[5\]                                       | CurrentValue |
| 0x38   | u64\[5\]                                       | LimitValue   |
| 0x60   | [\#KRecursiveLock](#KRecursiveLock "wikilink") | Mutex        |

# KPoolManager

Size:
0x380

| Offset | Type                                                | Description       |
| ------ | --------------------------------------------------- | ----------------- |
| 0      | [\#KPoolAllocator](#KPoolAllocator "wikilink")\[3\] | Allocator         |
| 0x348  | [\#KPoolRefManager](#KPoolRefManager "wikilink")    | RefManager        |
| 0x368  | u64                                                 | AllocationCounter |
| 0x370  | u64                                                 |                   |
| 0x378  | [\#KRecursiveLock](#KRecursiveLock "wikilink")      | Mutex             |

## KPoolAllocator

Size: 0x118

| Offset | Type                              | Description |
| ------ | --------------------------------- | ----------- |
| 0      | void\*                            | MemoryBase  |
| 8      | u64                               | MemorySize  |
| 0x10   | s32                               | NumPools    |
| 0x18   | [\#KPool](#KPool "wikilink")\[8\] | Pools       |

### KPool

Size: 0x20

| Offset | Type          | Description            |
| ------ | ------------- | ---------------------- |
| 0      | KPoolHeader\* | FirstFreeChunk         |
| 8      | u64           |                        |
| 0x10   | u64           |                        |
| 0x18   | void\*        | SingletonTableEntryPtr |

## KPoolRefManager

Size:
0x20

| Offset | Type                                         | Description   |
| ------ | -------------------------------------------- | ------------- |
| 0      | [\#KPoolManager](#KPoolManager "wikilink")\* | Parent        |
| 8      | void\*                                       | PoolBase      |
| 0x10   | u64                                          | MaxPage       |
| 0x18   | u16\*                                        | RefCountTable |

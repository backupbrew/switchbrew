# KAutoObject

Size: 0x10

| Offset | Type | Description    |
| ------ | ---- | -------------- |
| 0      | \*   | Vtable         |
| 8      | u32  | ReferenceCount |

# KSynchronizationObject

Size: 0x28

Inherits from:
[\#KAutoObject](#KAutoObject "wikilink")

| Offset | Type                                             | Description    |
| ------ | ------------------------------------------------ | -------------- |
| 0      | [\#KAutoObject](#KAutoObject "wikilink")         | Inheritance    |
| 0x10   | u64                                              | ThreadSyncNum  |
| 0x18   | [\#KLinkedListNode](#KLinkedListNode "wikilink") | ThreadSyncList |

# KMutex

Size: 0x8

| Offset | Type | Description |
| ------ | ---- | ----------- |
| 0      | u64  | OwnerTag    |

# KRecursiveLock

Size: 0x18

| Offset | Type                                | Description |
| ------ | ----------------------------------- | ----------- |
| 0      | [\#KThread](#KThread "wikilink") \* | Owner       |
| 8      | s32                                 | Count       |

# KLockedList

Size:
0x28

| Offset | Type                                             | Description |
| ------ | ------------------------------------------------ | ----------- |
| 0      | u64                                              | Count       |
| 8      | [\#KLinkedListNode](#KLinkedListNode "wikilink") | List        |
| 0x18   | [\#KMutex](#KMutex "wikilink")                   | Mutex       |
| 0x20   | u64                                              | MaxCount    |

# KLinkedListNode

Size:
0x10

| Offset | Type                                               | Description |
| ------ | -------------------------------------------------- | ----------- |
| 0      | [\#KLinkedListNode](#KLinkedListNode "wikilink")\* | Prev        |
| 8      | [\#KLinkedListNode](#KLinkedListNode "wikilink")\* | Next        |

# KThread

\[1.0.0\] Size: 0x620

Inherits from:
[\#KSynchronizationObject](#KSynchronizationObject "wikilink"),
[\#KSchedulerObject0](#KSchedulerObject0 "wikilink"),
[\#KSchedulerObject1](#KSchedulerObject1 "wikilink"),
[\#KSchedulerObject2](#KSchedulerObject2 "wikilink")

<div style="display: inline-block">

| 1.0.0 Offset | Type                                                                     | Description                  |
| ------------ | ------------------------------------------------------------------------ | ---------------------------- |
| 0            | [\#KSynchronizationObject](#KSynchronizationObject "wikilink")           | Inheritance                  |
| 0x28         | KSchedulerObject0                                                        | Inheritance                  |
| 0x48         | KSchedulerObject1                                                        | Inheritance                  |
| 0x58         | KSchedulerObject2                                                        | Inheritance                  |
| 0x70         | KThreadContext                                                           | Context                      |
| 0x2F0        | u64                                                                      | CoreMask                     |
| 0x2F8        | u64                                                                      | CoreMaskOverride             |
| 0x300        | u64                                                                      | ThreadId                     |
| 0x308        | u64                                                                      |                              |
| 0x310        | [\#KSynchronizationObject](#KSynchronizationObject "wikilink")\*         | SignalledObjectPtr           |
| 0x318        | u64                                                                      |                              |
| 0x320        | u64                                                                      |                              |
| 0x328        | u64                                                                      | Entrypoint                   |
| 0x330        | u64                                                                      |                              |
| 0x338        | [\#KProcess\*](#KProcess* "wikilink")                                    | ProcessPtr                   |
| 0x340        | void\*                                                                   | KernelThreadStack            |
| 0x348        | u64                                                                      |                              |
| 0x350        | void\*                                                                   | TlsKernelPtr                 |
| 0x358        | void\*                                                                   | TlsPhysicalPtr               |
| 0x360        | [\#KSynchronizationObject](#KSynchronizationObject "wikilink")\*\[0x40\] | SyncObjects                  |
| 0x560        | u64                                                                      |                              |
| 0x568        | u64                                                                      |                              |
| 0x570        | [\#KSynchronizationObject](#KSynchronizationObject "wikilink")           | SignalledObjectPtr?          |
| 0x578        | KLinkedListNode                                                          |                              |
| 0x588        | KLinkedListNode                                                          |                              |
| 0x598        | KLinkedListNode                                                          | NodeFor\_\_ThreadList        |
| 0x5A8        | KLinkedListNode                                                          | NodeFor\_\_ThreadsOnSameCore |
| 0x5B8        | u64                                                                      |                              |
| 0x5C0        | u64                                                                      |                              |
| 0x5C8        | u64                                                                      |                              |
| 0x5D0        | u64                                                                      |                              |
| 0x5D8        | u64                                                                      |                              |
| 0x5E0        | u32                                                                      |                              |
| 0x5E4        | u32                                                                      | SchedulingFlags\_Default     |
| 0x5E8        | u32                                                                      | WaitSync\_RetVal             |
| 0x5EC        | u32                                                                      |                              |
| 0x5F0        | u32                                                                      | ActualPriority               |
| 0x5F4        | u32                                                                      |                              |
| 0x5F8        | u32                                                                      |                              |
| 0x5FC        | u32                                                                      |                              |
| 0x600        | u32                                                                      | WantedPriority               |
| 0x604        | u32                                                                      | CpuCore                      |
| 0x608        | u8                                                                       | State                        |
| 0x609        | u8                                                                       | IsRunning                    |
| 0x60A        | u8                                                                       |                              |
| 0x60B        | u8                                                                       |                              |
| 0x60C        | u8                                                                       |                              |
| 0x60D        | u8                                                                       |                              |
| 0x60E        | u8                                                                       | HasExited                    |
| 0x60F        | u8                                                                       | HasCpuCoreOverride           |
| ...          | ...                                                                      | ...                          |

# KProcess

\[1.0.0\] Size: 0x5B0

\[2.0.0\] Size: 0x2480

\[3.0.0\] Size: 0x2580

Inherits from:
[\#KSynchronizationObject](#KSynchronizationObject "wikilink")

<div style="display: inline-block">

| 1.0.0 Offset | Type                                                                                 | Description                   |
| ------------ | ------------------------------------------------------------------------------------ | ----------------------------- |
| 0            | [\#KSynchronizationObject](#KSynchronizationObject "wikilink")                       | Inheritance                   |
| 0x28         | KProcessScheduler                                                                    | Scheduler                     |
| 0x38         | [\#KMemoryManager](#KMemoryManager "wikilink")                                       | MemoryManager                 |
| 0xF0         | u64                                                                                  | TotalMemUsage                 |
| 0xF8         | u64                                                                                  | TlsPagesListCount             |
| 0x100        | [\#KLinkedListNode](#KLinkedListNode "wikilink")                                     | TlsPagesList                  |
| 0x110        | s32                                                                                  | DefaultCpuCore                |
| 0x118        | [\#KDebug](#KDebug "wikilink")\*                                                     | Debug                         |
| 0x120        | [\#KResourceLimit](#KResourceLimit "wikilink")\*                                     | ResourceLimit                 |
| 0x128        | u32                                                                                  | State                         |
| 0x130        | [\#KMutex](#KMutex "wikilink")                                                       | ProcessMutex                  |
| 0x138        | [\#KMutex](#KMutex "wikilink")                                                       | ThreadingMutex                |
| 0x140        | [\#KLinkedListNode](#KLinkedListNode "wikilink")\<[\#KThread](#KThread "wikilink")\> | ThreadArbiterList             |
| 0x150        | KLinkedListNode                                                                      |                               |
| 0x160        | u64\[4\]                                                                             | RandomEntropy                 |
| 0x180        | u8                                                                                   | HasStateChanged               |
| 0x181        | u8                                                                                   | HasInitialized                |
| 0x182        | u8                                                                                   | IsSystem                      |
| 0x183        | u8\[12+1\]                                                                           | ProcessName                   |
| 0x190        | u16                                                                                  | NumberOfCreatedThreads        |
| 0x192        | u16                                                                                  | ThreadingRelatedInitiallyZero |
| 0x194        | u32                                                                                  | ProcessFlags                  |
| 0x198        | [\#KProcessCapabilities](#KProcessCapabilities "wikilink")                           | Capabilities                  |
| 0x248        | u64                                                                                  | TitleId                       |
| 0x250        | u64                                                                                  | ProcessId                     |
| 0x258        | u64                                                                                  | CreatedTickstamp              |
| 0x260        | u64                                                                                  | Entrypoint                    |
| 0x268        | u64                                                                                  | CodeMemUsage                  |
| 0x270        | u64                                                                                  | DynamicMemUsage               |
| 0x278        | u64                                                                                  | MaxTotalMemUsage              |
| 0x280        | u32                                                                                  | From\_CreateProcessInfo\_0xC  |
| 0x288        | [\#KProcessHandleTable](#KProcessHandleTable "wikilink")                             | HandleTable                   |
| 0x528        | void\*                                                                               | UsermodeExceptionTlsArea      |
| 0x530        | [\#KLinkedListNode](#KLinkedListNode "wikilink")\<[\#KThread](#KThread "wikilink")\> | ExceptionThreadList           |
| 0x540        | [\#KThread](#KThread "wikilink")\*                                                   | ExceptionThread               |
| 0x548        | [\#KLinkedListNode](#KLinkedListNode "wikilink")\<[\#KThread](#KThread "wikilink")\> | ThreadList                    |
| 0x558        | bool                                                                                 | HasStarted                    |
| 0x55C        | u32                                                                                  | UnusedZero                    |
| 0x560        | u64\[8\]                                                                             | UnusedZeroes                  |
| 0x5A0        | u64                                                                                  | UnusedZero                    |
| 0x5A8        | u64                                                                                  | UnusedZero                    |

</div>

<div style="display: inline-block; vertical-align:top;">

| 2.0.0 Offset | Type                                                                                                   | Description                   |
| ------------ | ------------------------------------------------------------------------------------------------------ | ----------------------------- |
| 0            | [\#KSynchronizationObject](#KSynchronizationObject "wikilink")                                         | Inheritance                   |
| 0x28         | KProcessScheduler                                                                                      | Scheduler                     |
| 0x38         | [\#KMemoryManager](#KMemoryManager "wikilink")                                                         | MemoryManager                 |
| 0x100        | u64                                                                                                    | TotalMemUsage                 |
| 0x108        | u64                                                                                                    | TlsPagesListCount             |
| 0x110        | [\#KLinkedListNode](#KLinkedListNode "wikilink")                                                       | TlsPagesList                  |
| 0x120        | s32                                                                                                    | DefaultCpuCore                |
| 0x128        | [\#KDebug](#KDebug "wikilink")\*                                                                       | Debug                         |
| 0x130        | [\#KResourceLimit](#KResourceLimit "wikilink")\*                                                       | ResourceLimit                 |
| 0x138        | u32                                                                                                    | State                         |
| 0x140        | [\#KMutex](#KMutex "wikilink")                                                                         | ProcessMutex                  |
| 0x148        | [\#KMutex](#KMutex "wikilink")                                                                         | ThreadingMutex                |
| 0x150        | [\#KLinkedListNode](#KLinkedListNode "wikilink")\<[\#KThread](#KThread "wikilink")\>                   | ThreadArbiterList             |
| 0x160        | KLinkedListNode                                                                                        |                               |
| 0x170        | u64\[4\]                                                                                               | RandomEntropy                 |
| 0x190        | u8                                                                                                     | HasStateChanged               |
| 0x191        | u8                                                                                                     | HasInitialized                |
| 0x192        | u8                                                                                                     | IsSystem                      |
| 0x193        | u8\[12+1\]                                                                                             | ProcessName                   |
| 0x1A0        | u16                                                                                                    | NumberOfCreatedThreads        |
| 0x1A2        | u16                                                                                                    | ThreadingRelatedInitiallyZero |
| 0x1A4        | u32                                                                                                    | ProcessFlags                  |
| 0x1A8        | [\#KProcessCapabilities](#KProcessCapabilities "wikilink")                                             | Capabilities                  |
| 0x258        | u64                                                                                                    | TitleId                       |
| 0x260        | u64                                                                                                    | ProcessId                     |
| 0x268        | u64                                                                                                    | CreatedTickstamp              |
| 0x270        | u64                                                                                                    | Entrypoint                    |
| 0x278        | u64                                                                                                    | CodeMemUsage                  |
| 0x280        | u64                                                                                                    | DynamicMemUsage               |
| 0x288        | u64                                                                                                    | MaxTotalMemUsage              |
| 0x290        | u32                                                                                                    | From\_CreateProcessInfo\_0xC  |
| 0x298        | u64\[5\]                                                                                               | Unused \[?\]                  |
| 0x2C0        | [\#KProcessHandleTable](#KProcessHandleTable "wikilink")                                               | HandleTable                   |
| 0x2380       | void\*                                                                                                 | UsermodeExceptionTlsArea      |
| 0x2388       | [\#KLinkedListNode](#KLinkedListNode "wikilink")\<[\#KThread](#KThread "wikilink")\>                   | ExceptionThreadList           |
| 0x2398       | [\#KThread](#KThread "wikilink")\*                                                                     | ExceptionThread               |
| 0x23A0       | [\#KLinkedListNode](#KLinkedListNode "wikilink")\<[\#KThread](#KThread "wikilink")\>                   | ThreadList                    |
| 0x23B0       | [\#KLinkedListNode](#KLinkedListNode "wikilink")\<[\#KSharedMemoryRef](#KSharedMemoryRef "wikilink")\> | MappedSharedMemoriesList      |
| 0x23C0       | bool                                                                                                   | HasStarted                    |
| 0x23C1       | bool                                                                                                   | HasException                  |
| 0x23C4       | u32                                                                                                    | ExceptionEnum0                |
| 0x23C8       | u64                                                                                                    | ExceptionEnum1                |
| 0x23D0       | u64                                                                                                    | ExceptionThreadUnkInfo0       |
| 0x23D8       | u64                                                                                                    | BreakArg0                     |
| 0x23E0       | u64                                                                                                    | BreakArg1                     |
| 0x23E8       | u64                                                                                                    | BreakArg2                     |
| 0x23F0       | u64                                                                                                    | ExceptionThreadUnkInfo1       |
| 0x23F8       | u32                                                                                                    | UnusedZero                    |
| 0x2400       | u64\[8\]                                                                                               | UnusedZeroes                  |
| 0x2440       | u64                                                                                                    | UnusedZero                    |
| 0x2448       | u64                                                                                                    | UnusedZero                    |
| 0x2450       | u64\[6\]                                                                                               | Unused \[?\]                  |

</div>

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

\[1.0.0\] Size: 0x2A0

\[2.0.0\] Size:
0x20C0

<div style="display: inline-block">

| 1.0.0 Offset | Type                                             | Description    |
| ------------ | ------------------------------------------------ | -------------- |
| 0            | [\#KHandleEntry](#KHandleEntry "wikilink")\*     | TablePtr       |
| 8            | [\#KHandleEntry](#KHandleEntry "wikilink")\*     | NextFreeEntry  |
| 0x10         | [\#KHandleEntry](#KHandleEntry "wikilink")\[40\] | InternalTable  |
| 0x290        | u16                                              | Size           |
| 0x292        | u16                                              | MaxUsageAtOnce |
| 0x294        | u16                                              | IdCounter      |
| 0x296        | u16                                              | NumActiveSlots |
| 0x298        | [\#KSpinLock](#KSpinLock "wikilink")             | Lock           |

</div>

<div style="display: inline-block; vertical-align:top;">

| 2.0.0 Offset | Type                                               | Description    |
| ------------ | -------------------------------------------------- | -------------- |
| 0            | [\#KHandleEntry](#KHandleEntry "wikilink")\*       | TablePtr       |
| 8            | [\#KHandleEntry](#KHandleEntry "wikilink")\*       | NextFreeEntry  |
| 0x10         | [\#KHandleEntry](#KHandleEntry "wikilink")\[1024\] | InternalTable  |
| 0x2010       | u16                                                | Size           |
| 0x2012       | u16                                                | MaxUsageAtOnce |
| 0x2014       | u16                                                | IdCounter      |
| 0x2016       | u16                                                | NumActiveSlots |
| 0x2040       | [\#KSpinLock](#KSpinLock "wikilink")               | Lock           |

</div>

### KHandleEntry

\[1.0.0\] Size: 0x10

\[2.0.0\] Size:
8

<div style="display: inline-block">

| 1.0.0 Offset | Type                                       | Description |
| ------------ | ------------------------------------------ | ----------- |
| 0            | u16                                        | HandleId    |
| 2            | u8                                         | ObjectType  |
| 8            | [\#KAutoObject](#KAutoObject "wikilink")\* | Object      |

</div>

<div style="display: inline-block; vertical-align:top;">

| 2.0.0 Offset | Type | Description         |
| ------------ | ---- | ------------------- |
| 0            | u16  | HandleId            |
| 2            | u8   | ObjectType          |
| 4            | u32  | ObjectCompressedPtr |

</div>

### KSpinLock

\[1.0.0\] Size: 0x1

\[2.0.0\] Size: 0x40

<div style="display: inline-block">

| 1.0.0 Offset | Type | Description |
| ------------ | ---- | ----------- |
| 0            | u8   | IsBusy      |

</div>

<div style="display: inline-block; vertical-align:top;">

| 2.0.0 Offset | Type | Description |
| ------------ | ---- | ----------- |
| 0            | u16  |             |
| 0x20         | u16  |             |

</div>

## KSharedMemoryRef

\[2.0.0\] Size:
0x40

| Offset | Type                                                                                                   | Description                         |
| ------ | ------------------------------------------------------------------------------------------------------ | ----------------------------------- |
| 0      | [\#KLinkedListNode](#KLinkedListNode "wikilink")\<[\#KSharedMemoryRef](#KSharedMemoryRef "wikilink")\> | NodeFor\_\_MappedSharedMemoriesList |
| 0x10   | [\#KSharedMemory\*](#KSharedMemory* "wikilink")                                                        | SharedMem                           |
| 0x18   | u64                                                                                                    | InitiallyZero                       |

# KMemoryManager

\[1.0.0\] Size: 0xB8

\[2.0.0\] Size:
0xC8

<div style="display: inline-block">

| 1.0.0 Offset | Type                                                     | Description                         |
| ------------ | -------------------------------------------------------- | ----------------------------------- |
| 0            | \*                                                       | Vtable                              |
| 8            | u64                                                      | AddrSpaceMinAddr                    |
| 0x10         | u64                                                      | AddrSpaceMaxAddr                    |
| 0x18         | u64                                                      | HeapRegionBaseAddr                  |
| 0x20         | u64                                                      | HeapRegionEndAddr                   |
| 0x28         | u64                                                      | HeapCurAddr                         |
| 0x30         | u64                                                      | MapRegionBaseAddr                   |
| 0x38         | u64                                                      | MapRegionEndAddr                    |
| 0x40         | u64                                                      | HeapMaxAllocation                   |
| 0x48         | [\#KMutex](#KMutex "wikilink")                           | Mutex                               |
| 0x50         | [\#KPageTable](#KPageTable "wikilink")                   | PageTable                           |
| 0x60         | [\#KMemoryBlockManager](#KMemoryBlockManager "wikilink") | MemoryBlockManager                  |
| 0x78         | bool                                                     | IsKernel                            |
| 0x79         | bool                                                     | IsSystem                            |
| 0x7A         | bool                                                     | IsAddrSpace36Bit                    |
| 0x7B         | bool                                                     | HasAslr                             |
| 0x7C         | u32                                                      | Is\_0x59\_If\_Cfg12\_Bit0\_ElseZero |
| 0x80         | u32                                                      | Is\_0x5A\_If\_Cfg12\_Bit0\_ElseZero |
| 0x84         | u32                                                      | Is\_0x58\_If\_Cfg12\_Bit0\_ElseZero |
| 0x88         |                                                          |                                     |
| 0x90         |                                                          |                                     |
| 0x98         |                                                          |                                     |
| 0xA0         | u64                                                      | TranslationTableBaseRegister0       |
| 0xA8         | u64                                                      | TranslationControlRegister          |
| 0xB0         | u8                                                       | AsidTagValue                        |

</div>

<div style="display: inline-block; vertical-align:top;">

| 2.0.0 Offset | Type                                                     | Description                         |
| ------------ | -------------------------------------------------------- | ----------------------------------- |
| 0            | \*                                                       | Vtable                              |
| 8            | u64                                                      | AddrSpaceMinAddr                    |
| 0x10         | u64                                                      | AddrSpaceMaxAddr                    |
| 0x18         | u64                                                      | HeapRegionBaseAddr                  |
| 0x20         | u64                                                      | HeapRegionEndAddr                   |
| 0x28         | u64                                                      | HeapCurAddr                         |
| 0x30         | u64                                                      | MapRegionBaseAddr                   |
| 0x38         | u64                                                      | MapRegionEndAddr                    |
| 0x40         | u64                                                      | NewUnknownRegionBaseAddr            |
| 0x48         | u64                                                      | NewUnknownRegionEndAddr             |
| 0x50         | u64                                                      | IoRegionBaseAddr                    |
| 0x58         | u64                                                      | IoRegionEndAddr                     |
| 0x60         | u64                                                      | HeapMaxAllocation                   |
| 0x68         | [\#KMutex](#KMutex "wikilink")                           | Mutex                               |
| 0x70         | [\#KPageTable](#KPageTable "wikilink")                   | PageTable                           |
| 0x80         | [\#KMemoryBlockManager](#KMemoryBlockManager "wikilink") | MemoryBlockManager                  |
| 0x98         | u32                                                      | AddressSpaceWidth (32/36/39)        |
| 0x9C         | bool                                                     | IsKernel                            |
| 0x9D         | bool                                                     | IsSystem                            |
| 0x9E         | bool                                                     | HasAslr                             |
| 0xA0         | u32                                                      | PoolPartition                       |
| 0xA4         | u32                                                      | Is\_0x5A\_If\_Cfg12\_Bit0\_ElseZero |
| 0xA8         | u32                                                      | Is\_0x59\_If\_Cfg12\_Bit0\_ElseZero |
| 0xAC         | u32                                                      | Is\_0x58\_If\_Cfg12\_Bit0\_ElseZero |
| 0xB0         | u64                                                      | TranslationTableBaseRegister0       |
| 0xB8         | u64                                                      | TranslationControlRegister          |
| 0xC0         | u32                                                      | AsidTagValue                        |

</div>

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
| 0x38   | KMutex                                   | Mutex        |
| 0x40   | int                                      | Permission   |
| 0x44   | bool                                     | HasInited    |
| 0x45   | bool                                     | IsMapped     |

# KSharedMemory

\[1.0.0\] Size: 0x40

\[2.0.0\] Size: 0x48

Inherits from:
[\#KAutoObject](#KAutoObject "wikilink")

<div style="display: inline-block;">

| 1.0.0 Offset | Type                                     | Description      |
| ------------ | ---------------------------------------- | ---------------- |
| 0            | [\#KAutoObject](#KAutoObject "wikilink") | Inheritance      |
| 0x10         | KMemoryBlockList                         | Blocks           |
| 0x28         | [\#KProcess](#KProcess "wikilink")\*     | OwnerProcess     |
| 0x30         | int                                      | LocalPermission  |
| 0x34         | int                                      | RemotePermission |
| 0x38         | bool                                     | HasInited        |

</div>

<div style="display: inline-block; vertical-align:top;">

| 2.0.0 Offset | Type                                             | Description        |
| ------------ | ------------------------------------------------ | ------------------ |
| 0            | [\#KAutoObject](#KAutoObject "wikilink")         | Inheritance        |
| 0x10         | KMemoryBlockList                                 | Blocks             |
| 0x28         | [\#KResourceLimit](#KResourceLimit "wikilink")\* | OwnerResourceLimit |
| 0x30         | u64                                              | OwnerProcessPid    |
| 0x38         | int                                              | LocalPermission    |
| 0x3C         | int                                              | RemotePermission   |
| 0x40         | bool                                             | HasInited          |

</div>

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

| Offset | Type                                                                  | Description                    |
| ------ | --------------------------------------------------------------------- | ------------------------------ |
| 0      | [\#KSynchronizationObject](#KSynchronizationObject "wikilink")        | Inheritance                    |
| 0x28   | KLinkedListNode                                                       | NodeFor\_\_IncomingConnections |
| 0x38   | [\#KSession\*](#KSession* "wikilink")                                 | Parent                         |
| 0x40   | KLinkedListNode\<[\#KSessionRequest](#KSessionRequest "wikilink")\*\> | RequestList                    |
| 0x50   | [\#KSessionRequest](#KSessionRequest "wikilink")\*                    | ActiveRequest                  |
| 0x58   |                                                                       |                                |

### KSessionRequest

Size:
0x158

| Offset | Type                                                      | Description            |
| ------ | --------------------------------------------------------- | ---------------------- |
| 0      | \*                                                        | Vtable                 |
| 0x10   | KLinkedListNode                                           | NodeFor\_\_RequestList |
| 0x20   | [\#KBufferDescriptor](#KBufferDescriptor "wikilink")\[8\] | BufferTable            |
| 0x120  | [\#KBufferDescriptor](#KBufferDescriptor "wikilink")\*    | ExternalBufferTable    |
| 0x128  | u8                                                        | NumSendBuffers         |
| 0x129  | u8                                                        | NumRecvBuffers         |
| 0x12A  | u8                                                        | NumExchBuffers         |
| 0x130  | [\#KThread](#KThread "wikilink")\*                        | SenderThread           |
| 0x138  | u64                                                       | InitiallyZero          |
| 0x140  | [\#KWritableEvent](#KWritableEvent "wikilink")\*          | ForAsyncEvent          |
| 0x148  | u64                                                       | CustomCmdbufAddr       |
| 0x150  | u64                                                       | CustomCmdbufSize       |

### KBufferDescriptor

Size: 0x20

| Offset | Type | Description       |
| ------ | ---- | ----------------- |
| 0      | u64  | UserVirtAddr      |
| 8      | u64  | Size              |
| 0x10   | u64  |                   |
| 0x18   | u64  | BufferMemoryState |
|        |      |                   |

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

\[1.0.0\] Size: 0x50

\[2.0.0\] Size: 0x48

Inherits from:
[\#KReadableEvent](#KReadableEvent "wikilink")

<div style="display: inline-block;">

| 1.0.0 Offset | Type                                                   | Description   |
| ------------ | ------------------------------------------------------ | ------------- |
| 0            | [\#KReadableEvent](#KReadableEvent "wikilink")         | Inheritance   |
| 0x38         | [\#KInterruptReceiver](#KInterruptReceiver "wikilink") | Receiver      |
| 0x48         | u32                                                    | IrqId (or -1) |

</div>

<div style="display: inline-block; vertical-align:top;">

| 2.0.0 Offset | Type                                                     | Description     |
| ------------ | -------------------------------------------------------- | --------------- |
| 0            | [\#KReadableEvent](#KReadableEvent "wikilink")           | Inheritance     |
| 0x38         | [\#KInterruptReceiver](#KInterruptReceiver "wikilink")\* | Receiver        |
| 0x40         | u32                                                      | IrqId (or -1)   |
| 0x44         | bool                                                     | IsIrqRegistered |

</div>

### KInterruptReceiver

\[1.0.0\] Size: 0x10 \[2.0.0\] Size: 0x20

<div style="display: inline-block;">

| Offset | Type | Description |
| ------ | ---- | ----------- |
| 0      | \*   | Vtable      |
| 8      | u64  |             |

</div>

<div style="display: inline-block; vertical-align:top;">

| Offset | Type                                               | Description   |
| ------ | -------------------------------------------------- | ------------- |
| 0      | \*                                                 | Vtable        |
| 8      | u64                                                | InitiallyZero |
| 0x10   | [\#KInterruptEvent](#KInterruptEvent "wikilink")\* | IrqEventPtr   |
| 0x18   | s32                                                | IrqId         |

</div>

# KDeviceAddressSpace

Size: 0x70

Inherits from: [\#KAutoObject](#KAutoObject "wikilink")

| Offset | Type                                       | Description |
| ------ | ------------------------------------------ | ----------- |
| 0      | [\#KAutoObject](#KAutoObject "wikilink")   | Inheritance |
| 0x10   | [\#KMutex](#KMutex "wikilink")             | Mutex       |
| 0x18   | [\#KSmmuManager](#KSmmuManager "wikilink") | Manager     |
| 0x58   | u64                                        | BaseAddress |
| 0x60   | u64                                        | Size        |
| 0x68   | bool                                       | HasInited   |

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

Inherits from: [\#KAutoObject](#KAutoObject "wikilink")

| Offset | Type                                     | Description  |
| ------ | ---------------------------------------- | ------------ |
| 0      | [\#KAutoObject](#KAutoObject "wikilink") | Inheritance  |
| 0x10   | u64\[5\]                                 | CurrentValue |
| 0x38   | u64\[5\]                                 | LimitValue   |
| 0x60   | [\#KMutex](#KMutex "wikilink")           | Mutex        |

# KPoolManager

\[1.0.0\] Size: 0x380

\[2.0.0\] Size:
0x450

<div style="display: inline-block;">

| 1.0.0 Offset | Type                                                | Description       |
| ------------ | --------------------------------------------------- | ----------------- |
| 0            | [\#KPoolAllocator](#KPoolAllocator "wikilink")\[3\] | Allocator         |
| 0x348        | [\#KPoolRefManager](#KPoolRefManager "wikilink")    | RefManager        |
| 0x368        | u64                                                 | AllocationCounter |
| 0x370        | u64                                                 |                   |
| 0x378        | [\#KMutex](#KMutex "wikilink")                      | Mutex             |

</div>

<div style="display: inline-block; vertical-align:top;">

| 2.0.0 Offset | Type                                             | Description    |
| ------------ | ------------------------------------------------ | -------------- |
| 0            | [\#KPoolAllocator](#KPoolAllocator "wikilink")   | Allocator0     |
| 0x220        | [\#KPartitionInfo](#KPartitionInfo "wikilink")\* | PartitionInfo0 |
| 0x228        | [\#KPoolAllocator](#KPoolAllocator "wikilink")   | Allocator1     |
| 0x448        | [\#KPartitionInfo](#KPartitionInfo "wikilink")\* | PartitionInfo1 |

</div>

## KPoolAllocator

\[1.0.0\] Size: 0x118

\[2.0.0\] Size: 0x220

<div style="display: inline-block;">

| 1.0.0 Offset | Type                              | Description |
| ------------ | --------------------------------- | ----------- |
| 0            | void\*                            | MemoryBase  |
| 8            | u64                               | MemorySize  |
| 0x10         | s32                               | NumPools    |
| 0x18         | [\#KPool](#KPool "wikilink")\[8\] | Pools       |

</div>

<div style="display: inline-block; vertical-align:top;">

| 2.0.0 Offset | Type                              | Description |
| ------------ | --------------------------------- | ----------- |
| 0            | void\*                            | MemoryBase  |
| 8            | u64                               | MemorySize  |
| 0x10         | [\#KPool](#KPool "wikilink")\[8\] | Pools       |
| 0x210        | s32                               | NumPools    |

</div>

### KPool

\[1.0.0\] Size: 0x20

\[2.0.0\] Size: 0x40

<div style="display: inline-block;">

| 1.0.0 Offset | Type          | Description            |
| ------------ | ------------- | ---------------------- |
| 0            | KPoolHeader\* | FirstFreeChunk         |
| 8            | u64           |                        |
| 0x10         | u64           |                        |
| 0x18         | void\*        | SingletonTableEntryPtr |

</div>

<div style="display: inline-block; vertical-align:top;">

| 2.0.0 Offset | Type                           | Description            |
| ------------ | ------------------------------ | ---------------------- |
| 0            | KPoolHeader\*                  | FirstFreeChunk         |
| 8            | u64                            |                        |
| 0x10         | u64                            |                        |
| 0x18         | void\*                         | SingletonTableEntryPtr |
| 0x20         | [\#KPool](#KPool "wikilink")\* | Parent                 |
| 0x30         | u64\[2\]                       | DmaProtectionKey       |

</div>

## KPoolRefManager

\[1.0.0\] Size:
0x20

| Offset | Type                                         | Description   |
| ------ | -------------------------------------------- | ------------- |
| 0      | [\#KPoolManager](#KPoolManager "wikilink")\* | Parent        |
| 8      | void\*                                       | PoolBase      |
| 0x10   | u64                                          | MaxPage       |
| 0x18   | u16\*                                        | RefCountTable |

# KObjectAllocator

Size: 0x50

| Offset | Type                                     | Description |
| ------ | ---------------------------------------- | ----------- |
| 0      | [\#KLockedList](#KLockedList "wikilink") | LockedList  |
| 0x28   | [\#KSlabHeap](#KSlabHeap "wikilink")     | SlabHeap    |

# KSlabHeap

Size: 0x28

| Offset | Type   | Description      |
| ------ | ------ | ---------------- |
| 0      | void\* | FreeListHead     |
| 0x8    | u64    |                  |
| 0x10   | void\* | HeapPtr          |
| 0x18   | u64    | TotalHeapSize    |
| 0x20   | u64    | SingleObjectSize |

# KPageTableAllocator

Size: 0x30

| Offset | Type   | Description   |
| ------ | ------ | ------------- |
| 0      | u64    |               |
| 0x10   | u16\*  | RefCountTable |
| 0x10   | void\* | BaseAddress   |
| 0x18   | u64    | Size          |
| 0x20   | u64    |               |
| 0x28   | u64    |               |

# KIrqManager

\[1.0.0\] Size: 0x1608

| Offset | Type                                        | Description |
| ------ | ------------------------------------------- | ----------- |
| 0      | [\#KIrqEntry](#KIrqEntry "wikilink")\[32\]  | Core0Irq    |
| 0x200  | [\#KIrqEntry](#KIrqEntry "wikilink")\[32\]  | Core1Irq    |
| 0x400  | [\#KIrqEntry](#KIrqEntry "wikilink")\[32\]  | Core2Irq    |
| 0x600  | [\#KIrqEntry](#KIrqEntry "wikilink")\[32\]  | Core3Irq    |
| 0x800  | [\#KIrqEntry](#KIrqEntry "wikilink")\[224\] | SharedIrqs  |
| 0x1600 | [\#KMutex](#KMutex "wikilink")              | Mutex       |

## KIrqEntry

\[1.0.0\] Size: 0x10

| Offset | Type                                          | Description |
| ------ | --------------------------------------------- | ----------- |
| 0      | [\#KIrqReciever\*](#KIrqReciever* "wikilink") | Receiver    |
| 8      | u8                                            | State0      |
| 9      | u8                                            | State1      |

# KDebug

Size:
0x50

| Offset | Type                                                                                         | Description |
| ------ | -------------------------------------------------------------------------------------------- | ----------- |
| 0      | [\#KSynchronizationObject](#KSynchronizationObject "wikilink")                               | Inheritance |
| 0x28   | [\#KLinkedListNode](#KLinkedListNode "wikilink")\<[\#KDebugEvent](#KDebugEvent "wikilink")\> | EventList   |
| 0x38   | u32                                                                                          | Flags       |
| 0x40   | [\#KProcess](#KProcess "wikilink")\*                                                         | ProcessPtr  |
| 0x48   | [\#KMutex](#KMutex "wikilink")                                                               | Mutex       |

## KDebugEvent

Size:
0x60

| Offset | Type                                                                                         | Description          |
| ------ | -------------------------------------------------------------------------------------------- | -------------------- |
| 0      | [\#KLinkedListNode](#KLinkedListNode "wikilink")\<[\#KDebugEvent](#KDebugEvent "wikilink")\> | NodeFor\_\_EventList |
| 0x10   | u32                                                                                          | EventType            |
| 0x14   | u32                                                                                          | ThreadId             |
| 0x18   | u32                                                                                          | Flags                |
| 0x1C   | u16                                                                                          |                      |
| 0x1E   | bool                                                                                         |                      |
| 0x20   | ...                                                                                          | ...                  |

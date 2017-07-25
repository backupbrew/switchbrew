# System calls

| Id   | Name                                                                               | In                                                                            | Out                                                 |
| ---- | ---------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- | --------------------------------------------------- |
| 0x1  | [\#svcSetHeapSize](#svcSetHeapSize "wikilink")                                     | W1=size                                                                       | W0=result, X1=outaddr                               |
| 0x2  | [\#svcSetMemoryPermission](#svcSetMemoryPermission "wikilink")                     | X0=addr, X1=size, W2=prot                                                     | W0=result                                           |
| 0x3  | [\#svcSetMemoryAttribute](#svcSetMemoryAttribute "wikilink")                       | X0=addr, X1=size, W2=state0, W3=state1                                        | W0=result                                           |
| 0x4  | [\#svcMapMemory](#svcMapMemory "wikilink")                                         | X0=dstaddr, X1=srcaddr, X2=size                                               | W0=result                                           |
| 0x5  | svcUnmapMemory                                                                     | X0=dstaddr, X1=srcaddr, X2=size                                               | W0=result                                           |
| 0x6  | svcQueryMemory                                                                     | X0=meminfo\_ptr, X2=addr                                                      | W0=result, W1=pageinfo                              |
| 0x7  | svcExitProcess                                                                     | None                                                                          |                                                     |
| 0x8  | [\#svcCreateThread](#svcCreateThread "wikilink")                                   | X1=entry, X2=arg, X3=stacktop, W4=prio, W5=processor\_id                      | W0=result, W1=handle                                |
| 0x9  | svcStartThread                                                                     | W0=thread\_handle                                                             | W0=result                                           |
| 0xA  | svcExitThread                                                                      | None                                                                          |                                                     |
| 0xB  | [\#svcSleepThread](#svcSleepThread "wikilink")                                     | X0=nano                                                                       | W0=result                                           |
| 0xC  | svcGetThreadPriority                                                               | W1=thread\_handle                                                             | W0=result, W1=prio                                  |
| 0xD  | svcSetThreadPriority                                                               | W0=thread\_handle, W1=prio                                                    | W0=result                                           |
| 0xE  | svcGetThreadCoreMask                                                               | W2=thread\_handle                                                             | W0=result, W1=out, X2=out                           |
| 0xF  | svcSetThreadCoreMask                                                               | W0=thread\_handle, W1=in, X2=in2                                              | W0=result                                           |
| 0x10 | svcGetCurrentProcessorNumber                                                       | None                                                                          | W0/X0=cpuid                                         |
| 0x11 | svcSignalEvent                                                                     | W0=wevent\_handle                                                             | W0=result                                           |
| 0x12 | svcClearEvent                                                                      | W0=wevent\_or\_revent\_handle                                                 | W0=result                                           |
| 0x13 | [\#svcMapSharedMemory](#svcMapSharedMemory "wikilink")                             | W0=memblk\_handle, X1=addr, X2=size, W3=perm                                  | W0=result                                           |
| 0x14 | svcUnmapSharedMemory                                                               | W0=memblk\_handle, X1=addr, X2=size                                           | W0=result                                           |
| 0x15 | [\#svcCreateTransferMemory](#svcCreateTransferMemory "wikilink")                   | X1=addr, X2=size, W3=perm                                                     | W0=result, W1=handle                                |
| 0x16 | svcCloseHandle                                                                     | W0=handle                                                                     | W0=result                                           |
| 0x17 | svcResetSignal                                                                     | W0=handle                                                                     | W0=result                                           |
| 0x18 | [\#svcWaitSynchronization](#svcWaitSynchronization "wikilink")                     | X1=handles\_ptr, W2=num\_handles. X3=timeout                                  | W0=result, W1=handle\_idx                           |
| 0x19 | svcCancelSynchronization                                                           | W0=handle                                                                     | W0=result                                           |
| 0x1A | svcArbitrateLock                                                                   | W0=cur\_thread\_handle, X1=ptr, W2=req\_thread\_handle                        |                                                     |
| 0x1B | svcArbitrateUnlock                                                                 | X0=ptr                                                                        |                                                     |
| 0x1C | svcWaitProcessWideKeyAtomic                                                        | X0=ptr0, X1=ptr, W2=thread\_handle, X3=timeout                                | W0=result                                           |
| 0x1D | svcSignalProcessWideKey                                                            | X0=ptr, W1=value                                                              | W0=result                                           |
| 0x1E | svcGetSystemTick                                                                   |                                                                               |                                                     |
| 0x1F | svcConnectToNamedPort                                                              | X1=port\_name\_str                                                            | W0=result, W1=handle                                |
| 0x20 | svcSendSyncRequestLight                                                            |                                                                               |                                                     |
| 0x21 | svcSendSyncRequest                                                                 | X0=handle                                                                     | W0=result                                           |
| 0x22 | [\#svcSendSyncRequestWithUserBuffer](#svcSendSyncRequestWithUserBuffer "wikilink") | X0=cmdbufptr, X1=size, X2=handle                                              | W0=result                                           |
| 0x23 | svcSendAsyncRequestWithUserBuffer                                                  |                                                                               |                                                     |
| 0x24 | svcGetProcessId                                                                    |                                                                               |                                                     |
| 0x25 | svcGetThreadId                                                                     | W0=thread\_handle                                                             | W0=result, X1=out                                   |
| 0x26 | svcBreak                                                                           | X0,X1,X2=info                                                                 | ?                                                   |
| 0x27 | svcOutputDebugString                                                               | X0=str, X1=size                                                               |                                                     |
| 0x28 | svcReturnFromException                                                             | X0=result                                                                     |                                                     |
| 0x29 | [\#svcGetInfo](#svcGetInfo "wikilink")                                             | X1=info\_id, X2=handle, X3=info\_sub\_id                                      | W0=result, X1=out                                   |
| 0x2A | svcFlushEntireDataCache                                                            |                                                                               |                                                     |
| 0x2B | svcFlushDataCache                                                                  |                                                                               |                                                     |
| 0x2C | \[ [3.0.0](3.0.0.md "wikilink")+ \] svcMapPhysicalMemory                           |                                                                               |                                                     |
| 0x2D | \[ [3.0.0](3.0.0.md "wikilink")+ \] svcUnmapPhysicalMemory                         |                                                                               |                                                     |
| .... | ?                                                                                  | ?                                                                             | ?                                                   |
| 0x2F | svcGetLastThreadInfo                                                               |                                                                               |                                                     |
| 0x30 | svcGetResourceLimitLimitValue                                                      |                                                                               |                                                     |
| 0x31 | svcGetResourceLimitCurrentValue                                                    |                                                                               |                                                     |
| 0x32 | svcSetThreadActivity                                                               |                                                                               |                                                     |
| 0x33 | svcGetThreadContext3                                                               |                                                                               |                                                     |
| 0x3C | svcDumpInfo                                                                        |                                                                               |                                                     |
| 0x40 | svcCreateSession                                                                   | W2=?, X3=?                                                                    | W0=result, W1=client\_handle, W2=server\_handle     |
| 0x41 | svcAcceptSession                                                                   | W1=port\_handle                                                               | W0=result, W1=session\_handle                       |
| 0x42 | svcReplyAndReceiveLight                                                            |                                                                               |                                                     |
| 0x43 | svcReplyAndReceive                                                                 | X1=ptr\_handles, W2=num\_handles, X3=?, X4=timeout                            | W0=result, W1=handle\_idx                           |
| 0x44 | svcReplyAndReceiveWithUserBuffer                                                   | X1=buf, X2=sz, X3=ptr\_handles, W4=num\_handles, X5=?, X6=timeout             | W0=result, W1=handle\_idx                           |
| 0x45 | svcCreateEvent                                                                     | None                                                                          | W0=result, W1=client\_handle ?, W2=server\_handle ? |
| 0x4D | svcSleepSystem                                                                     |                                                                               |                                                     |
| 0x4E | [\#svcReadWriteRegister](#svcReadWriteRegister "wikilink")                         | X1=reg\_addr, W2=rw\_mask, W3=in\_val                                         | W0=result, W1=out\_val                              |
| 0x4F | svcSetProcessActivity                                                              |                                                                               |                                                     |
| 0x50 | [\#svcCreateSharedMemory](#svcCreateSharedMemory "wikilink")                       | W1=size?, W2=myperm, W3=otherperm                                             | W0=result, W1=handle                                |
| 0x51 | [\#svcMapTransferMemory](#svcMapTransferMemory "wikilink")                         | X0=mirror\_handle, X1=addr, X2=size, W3=perm                                  | W0=result                                           |
| 0x52 | [\#svcUnmapTransferMemory](#svcUnmapTransferMemory "wikilink")                     | W0=mirror\_handle, X1=addr, X2=size                                           | W0=result                                           |
| 0x53 | svcCreateInterruptEvent                                                            | X1=irq\_id, W2=flag                                                           | W0=result, W1=handle                                |
| 0x54 | [\#svcQueryPhysicalAddress](#svcQueryPhysicalAddress "wikilink")                   |                                                                               |                                                     |
| 0x55 | [\#svcQueryIoMapping](#svcQueryIoMapping "wikilink")                               | X0=physaddr, X1=size                                                          | X0=virtaddr                                         |
| 0x56 | svcCreateDeviceAddressSpace                                                        | X1=dev\_addr, X2=dev\_size                                                    | W0=result, W1=handle                                |
| 0x57 | [\#svcAttachDeviceAddressSpace](#svcAttachDeviceAddressSpace "wikilink")           | W0=device, X1=handle                                                          | W0=result                                           |
| 0x58 | [\#svcDetachDeviceAddressSpace](#svcDetachDeviceAddressSpace "wikilink")           | W0=device, X1=handle                                                          | W0=result                                           |
| 0x59 | svcMapDeviceAddressSpaceByForce                                                    | W0=handle, W1=proc\_handle, X2=dev\_addr, X3=dev\_size, X4=map\_addr, W5=perm | W0=result                                           |
| 0x5A | svcMapDeviceAddressSpaceAligned                                                    |                                                                               |                                                     |
| 0x5B | svcMapDeviceAddressSpace                                                           |                                                                               |                                                     |
| 0x5C | svcUnmapDeviceAddressSpace                                                         | W0=handle, W1=proc\_handle, X2=map\_addr, X3=map\_size, W4=perm               | W0=result                                           |
| 0x5D | svcInvalidateProcessDataCache                                                      |                                                                               |                                                     |
| 0x5E | svcStoreProcessDataCache                                                           |                                                                               |                                                     |
| 0x5F | svcFlushProcessDataCache                                                           |                                                                               |                                                     |
| 0x60 | svcDebugActiveProcess                                                              |                                                                               |                                                     |
| 0x61 | svcBreakDebugProcess                                                               |                                                                               |                                                     |
| 0x62 | svcTerminateDebugProcess                                                           |                                                                               |                                                     |
| 0x63 | svcGetDebugEvent                                                                   |                                                                               |                                                     |
| 0x64 | svcContinueDebugEvent                                                              |                                                                               |                                                     |
| 0x65 | svcGetProcessList                                                                  |                                                                               |                                                     |
| 0x66 | svcGetThreadList                                                                   |                                                                               |                                                     |
| 0x67 | svcGetDebugThreadContext                                                           |                                                                               |                                                     |
| 0x68 | svcSetDebugThreadContext                                                           |                                                                               |                                                     |
| 0x69 | svcQueryDebugProcessMemory                                                         |                                                                               |                                                     |
| 0x6A | svcReadDebugProcessMemory                                                          |                                                                               |                                                     |
| 0x6B | svcWriteDebugProcessMemory                                                         |                                                                               |                                                     |
| 0x6C | svcSetHardwareBreakPoint                                                           |                                                                               |                                                     |
| 0x6D | svcGetDebugThreadParam                                                             |                                                                               |                                                     |
| 0x70 | svcCreatePort                                                                      |                                                                               |                                                     |
| 0x71 | svcManageNamedPort                                                                 |                                                                               |                                                     |
| 0x72 | svcConnectToPort                                                                   |                                                                               |                                                     |
| 0x73 | svcSetProcessMemoryPermission                                                      |                                                                               |                                                     |
| 0x74 | svcMapProcessMemory                                                                | X0=srcaddr, W1=process\_handle, X2=dstaddr, X3=size                           | W0=result                                           |
| 0x75 | svcUnmapProcessMemory                                                              | W0=process\_handle, X1=dstaddr, X2=srcaddr, X3=size                           | W0=result                                           |
| 0x76 | svcQueryProcessMemory                                                              |                                                                               |                                                     |
| 0x77 | svcMapProcessCodeMemory                                                            | W0=process\_handle, X2=dstaddr, X2=srcaddr, X3=size                           | W0=result                                           |
| 0x78 | svcUnmapProcessCodeMemory                                                          | W0=process\_handle, X1=dstaddr, X2=srcaddr, X3=size                           | W0=result                                           |
| 0x79 | [\#svcCreateProcess](#svcCreateProcess "wikilink")                                 | X1=procinfo\_ptr, X2=caps\_ptr, W3=cap\_num                                   | W0=result, W1=process\_handle                       |
| 0x7A | svcStartProcess                                                                    |                                                                               |                                                     |
| 0x7B | svcTerminateProcess                                                                |                                                                               |                                                     |
| 0x7C | svcGetProcessInfo                                                                  |                                                                               |                                                     |
| 0x7D | svcCreateResourceLimit                                                             |                                                                               |                                                     |
| 0x7E | svcSetResourceLimitLimitValue                                                      |                                                                               |                                                     |
| 0x7F | svcCallSecureMonitor                                                               |                                                                               |                                                     |

## svcSetHeapSize

Size must be a multiple of 0x2000000. The heap base-address is written
to out.

It allows both extending and shrinking the heap.

## svcSetMemoryPermission

Bit2 of permission (exec) is not allowed.

Setting write-only is not allowed either
(bit1).

## svcSetMemoryAttribute

| State0 | State1 | Action                                                          |
| ------ | ------ | --------------------------------------------------------------- |
| 0      | 0      | Clear bit3 in [\#MemoryAttribute](#MemoryAttribute "wikilink"). |
| 8      | 0      | Clear bit3 in [\#MemoryAttribute](#MemoryAttribute "wikilink"). |
| 8      | 8      | Set bit3 in [\#MemoryAttribute](#MemoryAttribute "wikilink").   |

This might used for switching between cached and non-cached mappings.

## svcMapMemory

Memory is only allowed to be mapped into a special region.

Code can get the range of this region from
[\#svcGetInfo](#svcGetInfo "wikilink").

The source region gets reprotected to ---, and sets bit0 is set in
[\#MemoryAttribute](#MemoryAttribute "wikilink").

## svcCreateThread

Processor\_id must be 0,1,2,3 or -2.

## svcSleepThread

Setting nano=0 means "yield thread".

## svcMapSharedMemory

Maps the block supplied by the handle. The required permissions are
different for the process that created the handle and all other
processes.

## svcCreateTransferMemory

This one reprotects the src block with perms you give it. It also sets
bit0 into [\#MemoryAttribute](#MemoryAttribute "wikilink").

Executable bit perm not allowed.

Closing all handles automatically causes the bit0 in
[\#MemoryAttribute](#MemoryAttribute "wikilink") to clear, and the
permission to reset.

## svcWaitSynchronization

Works with num\_handles \<= 0x40, error on num\_handles == 0.

Does not accept 0xFFFF8001 or 0xFFFF8000 as handles.

## svcSendSyncRequestWithUserBuffer

Size must be 0x1000-aligned.

## svcBreak

When used on retail where inx0 bit31 is clear, the system will throw a
[fatal-error](Error%20codes.md "wikilink"). Otherwise when bit31 is set,
it will return
0.

## svcGetInfo

| Handle type | Id0        | Id1                   | Description                                                                                                                                                        |
| ----------- | ---------- | --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Process     | 0          | 0                     | Core available mask. Always 0xF meaning all 4 cores available.                                                                                                     |
| Process     | 1          | 0                     | Always 0xfffffffff0000000.                                                                                                                                         |
| Process     | 2          | 0                     | Randomized unknown base-address.                                                                                                                                   |
| Process     | 3          | 0                     | Always 0x1000000000.                                                                                                                                               |
| Process     | 4          | 0                     | Heap base. Randomized.                                                                                                                                             |
| Process     | 5          | 0                     | Heap region size. Always 0x180000000.                                                                                                                              |
| Process     | 6          | 0                     | Total memory usage?                                                                                                                                                |
| Process     | 7          | 0                     | Process heap size.                                                                                                                                                 |
| Zero        | 8          | 0                     | Always 0. Used during exception handling.                                                                                                                          |
| Zero        | 9          | 0                     | This creates and returns an ResourceLimit handle. Used by [PM](Process%20Manager%20services.md "wikilink").                                                        |
| Zero        | 10         | \-1, {current coreid} | Unknown. Output data changes each time this SVC is used. Global and core-specific tick-count?                                                                      |
| Zero        | 11         | 0-3                   | Returns random from TRNG. Used to seed usermode PRNGs. Unknown what exactly causes this output to change, however it does change when exiting+launching a process. |
| Process     | 12         | 0                     | Address space start. Always 0x8000000.                                                                                                                             |
| Process     | 13         | 0                     | Address space size. Always 0x7ff8000000.                                                                                                                           |
| Process     | 14         | 0                     | Map region base. Randomized.                                                                                                                                       |
| Process     | 15         | 0                     | Map region size.                                                                                                                                                   |
| Process     | 18         | 0                     | \[ [3.0.0](3.0.0.md "wikilink") +\] Title-id.                                                                                                                      |
| ?           | 0xF0000002 | 0                     | Performance counter related.                                                                                                                                       |

## svcReadWriteRegister

Read/write Tegra hardware registers with a hardcoded whitelist. Input
address is physical-address.

rw\_mask is 0 for reading and -1 for writing.

The whitelist is same for writing as for
reading.

### Registers

| Address    | Register Name                                 | Description                                      |
| ---------- | --------------------------------------------- | ------------------------------------------------ |
| 0x700192E8 | MC\_LATENCY\_ALLOWANCE\_DC\_0\_0              | Latency allowance settings for DC clients        |
| 0x700192EC | MC\_LATENCY\_ALLOWANCE\_DC\_1\_0              | Latency allowance settings for DC clients        |
| 0x700192F0 | MC\_LATENCY\_ALLOWANCE\_DC\_2\_0              | Latency allowance settings for DC clients        |
| 0x700192F4 | MC\_LATENCY\_ALLOWANCE\_DCB\_0\_0             | Latency allowance settings for DCB clients       |
| 0x700192F8 | MC\_LATENCY\_ALLOWANCE\_DCB\_1\_0             | Latency allowance settings for DCB clients       |
| 0x7001941C | MC\_DIS\_PTSA\_RATE\_0                        | DDA rate for dis PTSA                            |
| 0x70019420 | MC\_DIS\_PTSA\_MIN\_0                         | DDA minimum value for direct client dis PTSA.    |
| 0x70019424 | MC\_DIS\_PTSA\_MAX\_0                         | DDA maximum value for direct client dis PTSA.    |
| 0x70019428 | MC\_DISB\_PTSA\_RATE\_0                       | DDA rate for disb PTSA                           |
| 0x7001942C | MC\_DISB\_PTSA\_MIN\_0                        | DDA minimum value for direct client disb PTSA    |
| 0x70019430 | MC\_DISB\_PTSA\_MAX\_0                        | DDA maximum value for direct client disb PTSA    |
| 0x7001944C | MC\_MLL\_MPCORER\_PTSA\_RATE\_0               | DDA rate for mll\_mpcorer PTSA                   |
| 0x7001947C | MC\_RING1\_PTSA\_RATE\_0                      | DDA rate for ring1 PTSA                          |
| 0x70019480 | MC\_RING1\_PTSA\_MIN\_0                       | DDA minimum value for direct client ring1 PTSA   |
| 0x70019484 | MC\_RING1\_PTSA\_MAX\_0                       | DDA maximum value for direct client ring1 PTSA   |
| 0x7001950C | MC\_FTOP\_PTSA\_RATE\_0                       | DDA rate for ftop PTSA                           |
| 0x70019670 | MC\_SEC\_CARVEOUT\_BOM\_0                     | Baseaddress for the SEC carveout address space.  |
| 0x70019674 | MC\_SEC\_CARVEOUT\_SIZE\_MB\_0                | Size in MB for the SEC carveout region           |
| 0x70019690 | MC\_SCALED\_LATENCY\_ALLOWANCE\_DISPLAY0A\_0  | Scaled Latency Allowance settings for DISPLAY0A  |
| 0x70019694 | MC\_SCALED\_LATENCY\_ALLOWANCE\_DISPLAY0AB\_0 | Scaled Latency Allowance settings for DISPLAY0AB |
| 0x70019698 | MC\_SCALED\_LATENCY\_ALLOWANCE\_DISPLAY0B\_0  | Scaled Latency Allowance settings for DISPLAY0B  |
| 0x7001969C | MC\_SCALED\_LATENCY\_ALLOWANCE\_DISPLAY0BB\_0 | Scaled Latency Allowance settings for DISPLAY0BB |
| 0x700196A0 | MC\_SCALED\_LATENCY\_ALLOWANCE\_DISPLAY0C\_0  | Scaled Latency Allowance settings for DISPLAY0C  |
| 0x700196A4 | MC\_SCALED\_LATENCY\_ALLOWANCE\_DISPLAY0CB\_0 | Scaled Latency Allowance settings for DISPLAY0CB |
| 0x70019C5C |                                               |                                                  |

## svcCreateSharedMemory

Other perm can be used to enforce permission 1, 3, or 0x10000000 if
don't care.

## svcMapTransferMemory

The newly mapped pages will have
[\#MemoryState](#MemoryState "wikilink") type 0xE.

You must pass same size and permissions as given in
svcCreateMemoryMirror, otherwise error.

## svcUnmapTransferMemory

Size must match size given in map syscall, otherwise there's an
invalid-size error.

## svcQueryPhysicalAddress

The inverse operation of
[\#svcQueryIoMapping](#svcQueryIoMapping "wikilink").

## svcQueryIoMapping

## svcCreateProcess

Takes a [\#CreateProcessInfo](#CreateProcessInfo "wikilink") as input.

## svcAttachDeviceAddressSpace / svcDetachDeviceAddressSpace

These take a device id and a device address space handle.

| Device | Name   | Description                 |
| ------ | ------ | --------------------------- |
| 0x0A   | APBDMA | Tegra's APB DMA controller. |
|        |        |                             |

# Structures

## CreateProcessInfo

| Offset | Length | Description                                                                                                                                 |
| ------ | ------ | ------------------------------------------------------------------------------------------------------------------------------------------- |
| 0      | 8      |                                                                                                                                             |
| 8      | 2      |                                                                                                                                             |
| 0xA    | 2      |                                                                                                                                             |
| 0x18   | 8      | CodeAddr                                                                                                                                    |
| 0x20   | 4      | CodeNumPages                                                                                                                                |
| 0x24   | 4      | MemoryManagementFlags. Bit0: is\_64bit (maybe?), bit3-1: MMU table size? (0=32-bit, 1=64-bit 0x800000000, 2=64-bit 0x400000000), bit5, bit6 |
| 0x28   | 4      | ResourceLimitHandle                                                                                                                         |
| 0x2C   | 4      |                                                                                                                                             |

## MemoryAttribute

| Bits | Description       |
| ---- | ----------------- |
| 0    | IsBorrowed        |
| 1    | IsIpcMapped \[?\] |
| 2    | IsDeviceMapped    |
| 3    | IsUncached \[?\]  |

## MemoryState

| Bits | Description                                                                                                                                                                |
| ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 7-0  | Type                                                                                                                                                                       |
| 8    | [PermissionChangeAllowed](#svcSetMemoryPermission "wikilink")                                                                                                              |
| 14   | [ProcessPermissionChangeAllowed](#svcSetProcessMemoryPermission "wikilink")                                                                                                |
| 15   | [MapAllowed](#svcMapMemory "wikilink")                                                                                                                                     |
| 16   | [UnmapProcessCodeMemoryAllowed](#svcUnmapProcessCodeMemory "wikilink")                                                                                                     |
| 17   | [TransferMemoryAllowed](#svcCreateTransferMemory "wikilink")                                                                                                               |
| 19   | MapDeviceAllowed ([\#svcMapDeviceAddressSpace](#svcMapDeviceAddressSpace "wikilink") and [\#svcMapDeviceAddressSpaceByForce](#svcMapDeviceAddressSpaceByForce "wikilink")) |
| 20   | [MapDeviceAlignedAllowed](#svcMapDeviceAddressSpaceAligned "wikilink")                                                                                                     |
| 21   | [IpcBufferAllowed](#svcSendSyncRequestWithUserBuffer "wikilink")                                                                                                           |
| 22   | IsCached \[?\]                                                                                                                                                             |
| 23   | [MapProcessAllowed](#svcMapProcessMemory "wikilink")                                                                                                                       |
| 24   | [AttributeChangeAllowed](#svcSetMemoryAttribute "wikilink")                                                                                                                |

| Value        | Type                  | Meaning                                                                                                             |
| ------------ | --------------------- | ------------------------------------------------------------------------------------------------------------------- |
| `0x00000000` | Unmapped              |                                                                                                                     |
| `0x00002001` | IO                    | Mapped by kernel capability parsing in [\#svcCreateProcess](#svcCreateProcess "wikilink").                          |
| `0x00042002` | IO                    | Mapped by kernel capability parsing in [\#svcCreateProcess](#svcCreateProcess "wikilink").                          |
| `0x00DC7E03` | Code static           | Mapped during [\#svcCreateProcess](#svcCreateProcess "wikilink").                                                   |
| `0x01FEBD04` | Code                  | Transition from 0xDC7E03 performed by [\#svcSetProcessMemoryPermission](#svcSetProcessMemoryPermission "wikilink"). |
| `0x017EBD05` | Heap                  | Mapped using [\#svcSetHeapSize](#svcSetHeapSize "wikilink").                                                        |
| `0x00402006` | Shared memory block   | Mapped using [\#svcMapSharedMemory](#svcMapSharedMemory "wikilink").                                                |
| `0x00482907` | Weird mapped memory   | Mapped using [\#svcMapMemory](#svcMapMemory "wikilink").                                                            |
| `0x00DD7E08` | Module code static    | Mapped using [\#svcMapProcessCodeMemory](#svcMapProcessCodeMemory "wikilink").                                      |
| `0x01FFBD09` | Module code mutable   | Transition from 0xDD7E08 performed by [\#svcSetProcessMemoryPermission](#svcSetProcessMemoryPermission "wikilink"). |
| `0x005C3C0B` | Mapped memory         | Mapped using [\#svcMapMemory](#svcMapMemory "wikilink").                                                            |
| `0x0040200C` | Thread local storage  | Mapped during [\#svcCreateThread](#svcCreateThread "wikilink").                                                     |
| `0x015C3C0D` | Weird transfer memory | Mapped using [\#svcMapTransferMemory](#svcMapTransferMemory "wikilink").                                            |
| `0x005C380E` | Transfer memory       | Mapped using [\#svcMapTransferMemory](#svcMapTransferMemory "wikilink").                                            |
| `0x0040380F` | Process memory        | Mapped using [\#svcMapProcessMemory](#svcMapProcessMemory "wikilink").                                              |
| `0x00000010` | Reserved              |                                                                                                                     |

# Exception Handling

There appears to be userland code for handling exceptions, however this
doesn't seem to be executed on retail.

On usermode exception, it jumps to main code binary entrypoint
(main\_binary\_address+0) with X0=exception\_info\_ptr and
X1=exception\_info2\_ptr. On boot, X0 is set to 0 triggering normal crt0
setup.

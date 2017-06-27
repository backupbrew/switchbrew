# System calls

| Id   | Name                                                                               | In                                                                | Out                                                 |
| ---- | ---------------------------------------------------------------------------------- | ----------------------------------------------------------------- | --------------------------------------------------- |
| 0x1  | [\#svcSetHeapSize](#svcSetHeapSize "wikilink")                                     | W1=size                                                           | W0=result, X1=outaddr                               |
| 0x2  | [\#svcSetMemoryPermission](#svcSetMemoryPermission "wikilink")                     | X0=addr, X1=size, W2=prot                                         | W0=result                                           |
| 0x3  | [\#svcSetMemoryAttribute](#svcSetMemoryAttribute "wikilink")                       | X0=addr, X1=size, W2=state0, W3=state1                            | W0=result                                           |
| 0x4  | [\#svcMapMemory](#svcMapMemory "wikilink")                                         | X0=dstaddr, X1=srcaddr, X2=size                                   | W0=result                                           |
| 0x5  | svcUnmapMemory                                                                     | X0=dstaddr, X1=srcaddr, X2=size                                   | W0=result                                           |
| 0x6  | svcQueryMemory                                                                     | X0=meminfo\_ptr, X2=addr                                          | W0=result, W1=pageinfo                              |
| 0x7  | svcExitProcess                                                                     | None                                                              |                                                     |
| 0x8  | [\#svcCreateThread](#svcCreateThread "wikilink")                                   | X1=entry, X2=arg, X3=stacktop, W4=prio, W5=processor\_id          | W0=result, W1=handle                                |
| 0x9  | svcStartThread                                                                     | W0=thread\_handle                                                 |                                                     |
| 0xA  | svcExitThread                                                                      | None                                                              |                                                     |
| 0xB  | [\#svcSleepThread](#svcSleepThread "wikilink")                                     | X0=nano                                                           |                                                     |
| 0xC  | svcGetThreadPriority                                                               | W1=thread\_handle                                                 | W0=result, W1=prio                                  |
| 0xD  | svcSetThreadPriority                                                               | W0=thread\_handle, W1=prio                                        | W0=result                                           |
| 0xE  | svcGetThreadCoreMask                                                               | W2=thread\_handle                                                 | W0=result, W1=out, X2=out                           |
| 0xF  | svcSetThreadCoreMask                                                               | W0=thread\_handle, W1=in, X2=in2                                  | W0=result                                           |
| 0x10 | svcGetCurrentProcessorNumber                                                       | None                                                              | W0/X0=cpuid                                         |
| 0x11 | svcSignalEvent                                                                     | W0=handle                                                         | ?                                                   |
| 0x12 | svcClearEvent                                                                      | W0=handle                                                         | ?                                                   |
| 0x13 | svcMapSharedMemory                                                                 | W0=memblk\_handle, X1=addr, X2=size, W3=perm                      | W0=result                                           |
| 0x14 | svcUnmapSharedMemory                                                               | W0=memblk\_handle, X1=addr, X2=size                               | W0=result                                           |
| 0x15 | [\#svcCreateTransferMemory](#svcCreateTransferMemory "wikilink")                   | X1=addr, X2=size, W3=perm                                         | W0=result, W1=handle                                |
| 0x16 | svcCloseHandle                                                                     | W0=handle                                                         | W0=result                                           |
| 0x17 | svcResetSignal                                                                     | W0=handle                                                         | W0=result                                           |
| 0x18 | [\#svcWaitSynchronization](#svcWaitSynchronization "wikilink")                     | X1=handles\_ptr, W2=num\_handles. X3=timeout                      | W0=result, W1=handle\_idx                           |
| 0x19 | svcCancelSynchronization                                                           | W0=handle                                                         | W0=result                                           |
| 0x1A | svcArbitrateLock                                                                   | W0=cur\_thread\_handle, X1=ptr, W2=req\_thread\_handle            |                                                     |
| 0x1B | svcArbitrateUnlock                                                                 | X0=ptr                                                            |                                                     |
| 0x1C | svcWaitProcessWideKeyAtomic                                                        | X0=ptr0, X1=ptr, W2=thread\_handle, X3=timeout                    | W0=result                                           |
| 0x1D | svc:SignalProcessWideKey                                                           | X0=ptr, W1=value                                                  | W0=result                                           |
| 0x1E | svcGetSystemTick                                                                   |                                                                   |                                                     |
| 0x1F | svcConnectToPort                                                                   | X1=port\_name\_str                                                | W0=result, W1=handle                                |
| 0x20 | svcSendSyncRequestLight                                                            |                                                                   |                                                     |
| 0x21 | svcSendSyncRequest                                                                 | X0=handle                                                         | W0=result                                           |
| 0x22 | [\#svcSendSyncRequestWithUserBuffer](#svcSendSyncRequestWithUserBuffer "wikilink") | X0=cmdbufptr, X1=size, X2=handle                                  | W0=result                                           |
| 0x23 | svcSendAsyncRequestWithUserBuffer                                                  |                                                                   |                                                     |
| 0x24 | svcGetProcessId                                                                    |                                                                   |                                                     |
| 0x25 | svcGetThreadId                                                                     | W0=thread\_handle                                                 | W0=result, X1=out                                   |
| 0x26 | svcBreak                                                                           | X0,X1,X2=info                                                     | ?                                                   |
| 0x27 | svcOutputDebugString                                                               | X0=str, X1=size                                                   |                                                     |
| 0x28 | svcReturnFromException                                                             | X0=result                                                         |                                                     |
| 0x29 | [\#svcGetInfo](#svcGetInfo "wikilink")                                             | X1=info\_id, X2=handle, X3=info\_sub\_id                          | W0=result, X1=out                                   |
| 0x2A | svcFlushEntireDataCache                                                            |                                                                   |                                                     |
| 0x2B | svcFlushDataCache                                                                  |                                                                   |                                                     |
| .... | ?                                                                                  | ?                                                                 | ?                                                   |
| 0x2F | svcGetLastThreadInfo                                                               |                                                                   |                                                     |
| 0x30 | svcGetResourceLimitLimitValue                                                      |                                                                   |                                                     |
| 0x31 | svcGetResourceLimitCurrentValue                                                    |                                                                   |                                                     |
| 0x32 | svcSetThreadActivity                                                               |                                                                   |                                                     |
| 0x33 | svcGetThreadContext3                                                               |                                                                   |                                                     |
| .... | ?                                                                                  | ?                                                                 | ?                                                   |
| 0x3C | svcDumpInfo                                                                        |                                                                   |                                                     |
| .... | ?                                                                                  | ?                                                                 | ?                                                   |
| 0x40 | svcCreateSession                                                                   | W2=?, X3=?                                                        | W0=result, W1=client\_handle, W2=server\_handle     |
| 0x41 | svcAcceptSession                                                                   | W1=port\_handle                                                   | W0=result, W1=session\_handle                       |
| 0x42 | svcReplyAndReceiveLight                                                            |                                                                   |                                                     |
| 0x43 | svcReplyAndReceive                                                                 | X1=ptr\_handles, W2=num\_handles, X3=?, X4=timeout                | W0=result, W1=handle\_idx                           |
| 0x44 | svcReplyAndReceiveWithUserBuffer                                                   | X1=buf, X2=sz, X3=ptr\_handles, W4=num\_handles, X5=?, X6=timeout | W0=result, W1=handle\_idx                           |
| 0x45 | svcCreateEvent                                                                     | None                                                              | W0=result, W1=client\_handle ?, W2=server\_handle ? |
| .... | ?                                                                                  | ?                                                                 | ?                                                   |
| 0x4D | svcSleepSystem                                                                     |                                                                   |                                                     |
| 0x4E | svcReadWriteRegister                                                               |                                                                   |                                                     |
| 0x4F | svcSetProcessActivity                                                              |                                                                   |                                                     |
| 0x50 | svcCreateSharedMemory                                                              | W1=size?, W2=perm0, W3=perm1                                      | W0=result, W1=handle                                |
| 0x51 | [\#svcMapTransferMemory](#svcMapTransferMemory "wikilink")                         | X0=mirror\_handle, X1=addr, X2=size, W3=perm                      | W0=result                                           |
| 0x52 | [\#svcUnmapTransferMemory](#svcUnmapTransferMemory "wikilink")                     | W0=mirror\_handle, X1=addr, X2=size                               | W0=result                                           |
| 0x53 | svcCreateInterruptEvent                                                            |                                                                   |                                                     |
| 0x54 | svcQueryPhysicalAddress                                                            |                                                                   |                                                     |
| 0x55 | svcQueryToMapping                                                                  |                                                                   |                                                     |
| 0x56 | svcCreateDeviceAddressSpace                                                        |                                                                   |                                                     |
| 0x57 | svcAttachDeviceAddressSpace                                                        |                                                                   |                                                     |
| 0x58 | svcDetachDeviceAddressSpace                                                        |                                                                   |                                                     |
| 0x59 | svcMapDeviceAddressSpaceByForce                                                    |                                                                   |                                                     |
| 0x5A | svcMapDeviceAddressSpaceAligned                                                    |                                                                   |                                                     |
| 0x5B | svcMapDeviceAddressSpace                                                           |                                                                   |                                                     |
| 0x5C | svcUnmapDeviceAddressSpace                                                         |                                                                   |                                                     |
| 0x5D | svcInvalidateProcessDataCache                                                      |                                                                   |                                                     |
| 0x5E | svcStoreProcessDataCache                                                           |                                                                   |                                                     |
| 0x5F | svcFlushProcessDataCache                                                           |                                                                   |                                                     |
| 0x60 | svcDebugActiveProcess                                                              |                                                                   |                                                     |
| 0x61 | svcBreakDebugProcess                                                               |                                                                   |                                                     |
| 0x62 | svcTerminateDebugProcess                                                           |                                                                   |                                                     |
| 0x63 | svcGetDebugEvent                                                                   |                                                                   |                                                     |
| 0x64 | svcContinueDebugEvent                                                              |                                                                   |                                                     |
| 0x65 | svcGetProcessList                                                                  |                                                                   |                                                     |
| 0x66 | svcGetThreadList                                                                   |                                                                   |                                                     |
| 0x67 | svcGetDebugThreadContext                                                           |                                                                   |                                                     |
| 0x68 | svcSetDebugThreadContext                                                           |                                                                   |                                                     |
| 0x69 | svcQueryDebugProcessMemory                                                         |                                                                   |                                                     |
| 0x6A | svcReadDebugProcessMemory                                                          |                                                                   |                                                     |
| 0x6B | svcWriteDebugProcessMemory                                                         |                                                                   |                                                     |
| 0x6C | svcSetHardwareBreakPoint                                                           |                                                                   |                                                     |
| 0x6D | svcGetDebugThreadParam                                                             |                                                                   |                                                     |
| .... | ?                                                                                  | ?                                                                 | ?                                                   |
| 0x70 | svcCreatePort                                                                      |                                                                   |                                                     |
| 0x71 | svcManageNamedPort                                                                 |                                                                   |                                                     |
| 0x72 | svcConnectToPort                                                                   |                                                                   |                                                     |
| 0x73 | svcSetProcessMemoryPermission                                                      |                                                                   |                                                     |
| 0x74 | svcMapProcessMemory                                                                |                                                                   |                                                     |
| 0x75 | svcUnmapProcessMemory                                                              |                                                                   |                                                     |
| 0x76 | svcQueryProcessMemory                                                              |                                                                   |                                                     |
| 0x77 | svcMapProcessCodeMemory                                                            |                                                                   |                                                     |
| 0x78 | svcUnmapProcessCodeMemory                                                          |                                                                   |                                                     |
| 0x79 | svcCreateProcess                                                                   |                                                                   |                                                     |
| 0x7A | svcStartProcess                                                                    |                                                                   |                                                     |
| 0x7B | svcTerminateProcess                                                                |                                                                   |                                                     |
| 0x7C | svcGetProcessInfo                                                                  |                                                                   |                                                     |
| 0x7D | svcCreateResourceLimit                                                             |                                                                   |                                                     |
| 0x7E | svcSetResourceLimitLimitValue                                                      |                                                                   |                                                     |
| 0x7F | svcCallSecureMonitor                                                               |                                                                   |                                                     |

## svcSetHeapSize

Size must be a multiple of 0x2000000. The heap base-address is written
to out.

## svcSetMemoryPermission

Bit2 of permission (exec) is not allowed.

Setting write-only is not allowed either
(bit1).

## svcSetMemoryAttribute

| State0 | State1 | Action                                                           |
| ------ | ------ | ---------------------------------------------------------------- |
| 0      | 0      | Clear bit35 in [\#MemoryAttribute](#MemoryAttribute "wikilink"). |
| 8      | 0      | Clear bit35 in [\#MemoryAttribute](#MemoryAttribute "wikilink"). |
| 8      | 8      | Set bit35 in [\#MemoryAttribute](#MemoryAttribute "wikilink").   |

This might used for switching between cached and non-cached mappings.

## svcMapMemory

Memory is only allowed to be mapped into a special region.

Code can get the range of this region from
[\#svcGetInfo](#svcGetInfo "wikilink").

The source region gets reprotected to ---, and sets bit32 is set in
[\#MemoryAttribute](#MemoryAttribute "wikilink").

## svcCreateThread

Processor\_id must be 0,1,2,3 or -2.

## svcSleepThread

Setting nano=0 means "yield thread".

## svcCreateTransferMemory

This one reprotects the src block with perms you give it. It also sets
bit32 into [\#MemoryAttribute](#MemoryAttribute "wikilink").

Executable bit perm not allowed.

Closing all handles automatically causes the bit32 in
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

| Handle type | Id0 | Id1                   | Description                                                                                                                                                        |
| ----------- | --- | --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Process     | 0   | 0                     | Core available mask. Always 0xF meaning all 4 cores available.                                                                                                     |
| Process     | 1   | 0                     | Always 0xfffffffff0000000.                                                                                                                                         |
| Process     | 2   | 0                     | Randomized unknown base-address.                                                                                                                                   |
| Process     | 3   | 0                     | Always 0x1000000000.                                                                                                                                               |
| Process     | 4   | 0                     | Heap base. Randomized.                                                                                                                                             |
| Process     | 5   | 0                     | Heap region size. Always 0x180000000.                                                                                                                              |
| Process     | 6   | 0                     | Total memory usage?                                                                                                                                                |
| Process     | 7   | 0                     | Process heap size.                                                                                                                                                 |
| Zero        | 8   | 0                     | Always 0. Used during exception handling.                                                                                                                          |
| Zero        | 9   | 0                     | This creates and returns an unknown handle.                                                                                                                        |
| Zero        | 10  | \-1, {current coreid} | Unknown. Output data changes each time this SVC is used. Global and core-specific tick-count?                                                                      |
| Zero        | 11  | 0-3                   | Returns random from TRNG. Used to seed usermode PRNGs. Unknown what exactly causes this output to change, however it does change when exiting+launching a process. |
| Process     | 12  | 0                     | Address space start. Always 0x8000000.                                                                                                                             |
| Process     | 13  | 0                     | Address space size. Always 0x7ff8000000.                                                                                                                           |
| Process     | 14  | 0                     | Map region base. Randomized.                                                                                                                                       |
| Process     | 15  | 0                     | Map region size.                                                                                                                                                   |

## svcMapTransferMemory

The newly mapped pages will have
[\#MemoryAttribute](#MemoryAttribute "wikilink") type 0xE.

You must pass same size and permissions as given in
svcCreateMemoryMirror, otherwise error.

## svcUnmapTransferMemory

Size must match size given in map syscall, otherwise there's an
invalid-size error.

## MemoryAttribute

| Lower 8 bits | Type                 | Meaning           |
| ------------ | -------------------- | ----------------- |
| 0x3          | Code static          | .text and .rodata |
| 0x4          | Code                 | .data             |
| 0x5          | Heap                 |                   |
| 0x6          | Shared memory block  |                   |
| 0x8          | Module code static   | .text and .rodata |
| 0x9          | Module code          | .data             |
| 0xB          | Stack mirror         |                   |
| 0xC          | Thread local storage |                   |
| 0xE          | Memory mirror        |                   |
| 0x10         | Reserved             |                   |

Bit32: is\_mirrored Bit34: is\_nv\_locked Bit35: is\_uncached?

# Exception Handling

There appears to be userland code for handling exceptions, however this
doesn't seem to be executed on retail.

On usermode exception, it jumps to main code binary entrypoint
(main\_binary\_address+0) with X0=exception\_info\_ptr and
X1=exception\_info2\_ptr. On boot, X0 is set to 0 triggering normal crt0
setup.

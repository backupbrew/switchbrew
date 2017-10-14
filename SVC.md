\_\_NOTOC\_\_

# System calls

| Id   | Name                                                                               | In                                                                                                  | Out                                                      |
| ---- | ---------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| 0x1  | [\#svcSetHeapSize](#svcSetHeapSize "wikilink")                                     | W1=size                                                                                             | W0=result, X1=outaddr                                    |
| 0x2  | [\#svcSetMemoryPermission](#svcSetMemoryPermission "wikilink")                     | X0=addr, X1=size, W2=prot                                                                           | W0=result                                                |
| 0x3  | [\#svcSetMemoryAttribute](#svcSetMemoryAttribute "wikilink")                       | X0=addr, X1=size, W2=state0, W3=state1                                                              | W0=result                                                |
| 0x4  | [\#svcMapMemory](#svcMapMemory "wikilink")                                         | X0=dstaddr, X1=srcaddr, X2=size                                                                     | W0=result                                                |
| 0x5  | [\#svcUnmapMemory](#svcUnmapMemory "wikilink")                                     | X0=dstaddr, X1=srcaddr, X2=size                                                                     | W0=result                                                |
| 0x6  | [\#svcQueryMemory](#svcQueryMemory "wikilink")                                     | X0=MemoryInfo\*, X2=addr                                                                            | W0=result, W1=PageInfo                                   |
| 0x7  | [\#svcExitProcess](#svcExitProcess "wikilink")                                     | None                                                                                                |                                                          |
| 0x8  | [\#svcCreateThread](#svcCreateThread "wikilink")                                   | X1=entry, X2=arg, X3=stacktop, W4=prio, W5=processor\_id                                            | W0=result, W1=handle                                     |
| 0x9  | [\#svcStartThread](#svcStartThread "wikilink")                                     | W0=thread\_handle                                                                                   | W0=result                                                |
| 0xA  | [\#svcExitThread](#svcExitThread "wikilink")                                       | None                                                                                                |                                                          |
| 0xB  | [\#svcSleepThread](#svcSleepThread "wikilink")                                     | X0=nano                                                                                             | W0=result                                                |
| 0xC  | [\#svcGetThreadPriority](#svcGetThreadPriority "wikilink")                         | W1=thread\_handle                                                                                   | W0=result, W1=prio                                       |
| 0xD  | [\#svcSetThreadPriority](#svcSetThreadPriority "wikilink")                         | W0=thread\_handle, W1=prio                                                                          | W0=result                                                |
| 0xE  | [\#svcGetThreadCoreMask](#svcGetThreadCoreMask "wikilink")                         | W2=thread\_handle                                                                                   | W0=result, W1=out, X2=out                                |
| 0xF  | [\#svcSetThreadCoreMask](#svcSetThreadCoreMask "wikilink")                         | W0=thread\_handle, W1=in, X2=in2                                                                    | W0=result                                                |
| 0x10 | [\#svcGetCurrentProcessorNumber](#svcGetCurrentProcessorNumber "wikilink")         | None                                                                                                | W0/X0=cpuid                                              |
| 0x11 | svcSignalEvent                                                                     | W0=wevent\_handle                                                                                   | W0=result                                                |
| 0x12 | svcClearEvent                                                                      | W0=wevent\_or\_revent\_handle                                                                       | W0=result                                                |
| 0x13 | [\#svcMapSharedMemory](#svcMapSharedMemory "wikilink")                             | W0=memblk\_handle, X1=addr, X2=size, W3=perm                                                        | W0=result                                                |
| 0x14 | svcUnmapSharedMemory                                                               | W0=memblk\_handle, X1=addr, X2=size                                                                 | W0=result                                                |
| 0x15 | [\#svcCreateTransferMemory](#svcCreateTransferMemory "wikilink")                   | X1=addr, X2=size, W3=perm                                                                           | W0=result, W1=handle                                     |
| 0x16 | svcCloseHandle                                                                     | W0=handle                                                                                           | W0=result                                                |
| 0x17 | svcResetSignal                                                                     | W0=handle                                                                                           | W0=result                                                |
| 0x18 | [\#svcWaitSynchronization](#svcWaitSynchronization "wikilink")                     | X1=handles\_ptr, W2=num\_handles. X3=timeout                                                        | W0=result, W1=handle\_idx                                |
| 0x19 | svcCancelSynchronization                                                           | W0=handle                                                                                           | W0=result                                                |
| 0x1A | svcArbitrateLock                                                                   | W0=cur\_thread\_handle, X1=ptr, W2=req\_thread\_handle                                              |                                                          |
| 0x1B | svcArbitrateUnlock                                                                 | X0=ptr                                                                                              |                                                          |
| 0x1C | svcWaitProcessWideKeyAtomic                                                        | X0=ptr0, X1=ptr, W2=thread\_handle, X3=timeout                                                      | W0=result                                                |
| 0x1D | svcSignalProcessWideKey                                                            | X0=ptr, W1=value                                                                                    | W0=result                                                |
| 0x1E | svcGetSystemTick                                                                   |                                                                                                     | X0={value of cntpct\_el0}                                |
| 0x1F | svcConnectToNamedPort                                                              | X1=port\_name\_str                                                                                  | W0=result, W1=handle                                     |
| 0x20 | svcSendSyncRequestLight                                                            |                                                                                                     |                                                          |
| 0x21 | svcSendSyncRequest                                                                 | X0=handle                                                                                           | W0=result                                                |
| 0x22 | [\#svcSendSyncRequestWithUserBuffer](#svcSendSyncRequestWithUserBuffer "wikilink") | X0=cmdbufptr, X1=size, X2=handle                                                                    | W0=result                                                |
| 0x23 | svcSendAsyncRequestWithUserBuffer                                                  |                                                                                                     |                                                          |
| 0x24 | svcGetProcessId                                                                    |                                                                                                     |                                                          |
| 0x25 | svcGetThreadId                                                                     | W0=thread\_handle                                                                                   | W0=result, X1=out                                        |
| 0x26 | svcBreak                                                                           | X0,X1,X2=info                                                                                       | ?                                                        |
| 0x27 | svcOutputDebugString                                                               | X0=str, X1=size                                                                                     |                                                          |
| 0x28 | svcReturnFromException                                                             | X0=result                                                                                           |                                                          |
| 0x29 | [\#svcGetInfo](#svcGetInfo "wikilink")                                             | X1=info\_id, X2=handle, X3=info\_sub\_id                                                            | W0=result, X1=out                                        |
| 0x2A | svcFlushEntireDataCache                                                            |                                                                                                     |                                                          |
| 0x2B | svcFlushDataCache                                                                  |                                                                                                     |                                                          |
| 0x2C | \[3.0.0+\] svcMapPhysicalMemory                                                    |                                                                                                     |                                                          |
| 0x2D | \[3.0.0+\] svcUnmapPhysicalMemory                                                  |                                                                                                     |                                                          |
| .... | ?                                                                                  | ?                                                                                                   | ?                                                        |
| 0x2F | svcGetLastThreadInfo                                                               |                                                                                                     |                                                          |
| 0x30 | svcGetResourceLimitLimitValue                                                      |                                                                                                     |                                                          |
| 0x31 | svcGetResourceLimitCurrentValue                                                    |                                                                                                     |                                                          |
| 0x32 | svcSetThreadActivity                                                               |                                                                                                     |                                                          |
| 0x33 | svcGetThreadContext3                                                               |                                                                                                     |                                                          |
| 0x3C | svcDumpInfo                                                                        |                                                                                                     |                                                          |
| 0x40 | svcCreateSession                                                                   | W2=?, X3=?                                                                                          | W0=result, W1=client\_handle, W2=server\_handle          |
| 0x41 | svcAcceptSession                                                                   | W1=port\_handle                                                                                     | W0=result, W1=session\_handle                            |
| 0x42 | svcReplyAndReceiveLight                                                            |                                                                                                     |                                                          |
| 0x43 | svcReplyAndReceive                                                                 | X1=ptr\_handles, W2=num\_handles, X3=replytarget\_handle(0=none), X4=timeout                        | W0=result, W1=handle\_idx                                |
| 0x44 | svcReplyAndReceiveWithUserBuffer                                                   | X1=buf, X2=sz, X3=ptr\_handles, W4=num\_handles, X5=replytarget\_handle(0=none), X6=timeout         | W0=result, W1=handle\_idx                                |
| 0x45 | svcCreateEvent                                                                     | None                                                                                                | W0=result, W1=client\_handle ?, W2=server\_handle ?      |
| 0x4D | svcSleepSystem                                                                     |                                                                                                     |                                                          |
| 0x4E | [\#svcReadWriteRegister](#svcReadWriteRegister "wikilink")                         | X1=reg\_addr, W2=rw\_mask, W3=in\_val                                                               | W0=result, W1=out\_val                                   |
| 0x4F | svcSetProcessActivity                                                              |                                                                                                     |                                                          |
| 0x50 | [\#svcCreateSharedMemory](#svcCreateSharedMemory "wikilink")                       | W1=size?, W2=myperm, W3=otherperm                                                                   | W0=result, W1=handle                                     |
| 0x51 | [\#svcMapTransferMemory](#svcMapTransferMemory "wikilink")                         | X0=mirror\_handle, X1=addr, X2=size, W3=perm                                                        | W0=result                                                |
| 0x52 | [\#svcUnmapTransferMemory](#svcUnmapTransferMemory "wikilink")                     | W0=mirror\_handle, X1=addr, X2=size                                                                 | W0=result                                                |
| 0x53 | svcCreateInterruptEvent                                                            | X1=irq\_id, W2=flag                                                                                 | W0=result, W1=handle                                     |
| 0x54 | [\#svcQueryPhysicalAddress](#svcQueryPhysicalAddress "wikilink")                   |                                                                                                     |                                                          |
| 0x55 | [\#svcQueryIoMapping](#svcQueryIoMapping "wikilink")                               | X1=physaddr, X2=size                                                                                | W0=result, X1=virtaddr                                   |
| 0x56 | [\#svcCreateDeviceAddressSpace](#svcCreateDeviceAddressSpace "wikilink")           | X1=dev\_as\_start\_addr, X2=dev\_as\_end\_addr                                                      | W0=result, W1=dev\_as\_handle                            |
| 0x57 | [\#svcAttachDeviceAddressSpace](#svcAttachDeviceAddressSpace "wikilink")           | W0=device, X1=dev\_as\_handle                                                                       | W0=result                                                |
| 0x58 | [\#svcDetachDeviceAddressSpace](#svcDetachDeviceAddressSpace "wikilink")           | W0=device, X1=dev\_as\_handle                                                                       | W0=result                                                |
| 0x59 | [\#svcMapDeviceAddressSpaceByForce](#svcMapDeviceAddressSpaceByForce "wikilink")   | W0=dev\_as\_handle, W1=proc\_handle, X2=dev\_map\_addr, X3=dev\_as\_size, X4=dev\_as\_addr, W5=perm | W0=result                                                |
| 0x5A | [\#svcMapDeviceAddressSpaceAligned](#svcMapDeviceAddressSpaceAligned "wikilink")   | W0=dev\_as\_handle, W1=proc\_handle, X2=dev\_map\_addr, X3=dev\_as\_size, X4=dev\_as\_addr, W5=perm | W0=result                                                |
| 0x5B | svcMapDeviceAddressSpace                                                           |                                                                                                     |                                                          |
| 0x5C | [\#svcUnmapDeviceAddressSpace](#svcUnmapDeviceAddressSpace "wikilink")             | W0=dev\_as\_handle, W1=proc\_handle, X2=dev\_map\_addr, X3=dev\_as\_size, X4=dev\_as\_addr          | W0=result                                                |
| 0x5D | svcInvalidateProcessDataCache                                                      |                                                                                                     |                                                          |
| 0x5E | svcStoreProcessDataCache                                                           |                                                                                                     |                                                          |
| 0x5F | svcFlushProcessDataCache                                                           |                                                                                                     |                                                          |
| 0x60 | svcDebugActiveProcess                                                              | X1=pid                                                                                              | W0=result, W1=debug\_handle                              |
| 0x61 | svcBreakDebugProcess                                                               | W0=debug\_handle                                                                                    | W0=result                                                |
| 0x62 | svcTerminateDebugProcess                                                           | W0=debug\_handle                                                                                    | W0=result                                                |
| 0x63 | svcGetDebugEvent                                                                   | X0=DebugEventInfo\*, W1=debug\_handle                                                               | W0=result                                                |
| 0x64 | svcContinueDebugEvent                                                              | W0=debug\_handle, W1=flags, X2=?                                                                    | W0=result                                                |
| 0x65 | svcGetProcessList                                                                  | X1=pids\_out\_ptr, W2=max\_out                                                                      | W0=result, W1=num\_out                                   |
| 0x66 | svcGetThreadList                                                                   | X1=tids\_out\_ptr, W2=max\_out, W3=debug\_handle\_or\_zero                                          | W0=result, X1=num\_out                                   |
| 0x67 | svcGetDebugThreadContext                                                           | X0=ThreadContext\*, X1=debug\_handle, X2=?, W3=?                                                    | W0=result                                                |
| 0x68 | svcSetDebugThreadContext                                                           |                                                                                                     |                                                          |
| 0x69 | svcQueryDebugProcessMemory                                                         | X0=[\#MemoryInfo](#MemoryInfo "wikilink")\*, X2=debug\_handle, X3=addr                              | W0=result, W1=PageInfo                                   |
| 0x6A | svcReadDebugProcessMemory                                                          | X0=buffer\*, X1=debug\_handle, X2=src\_addr, X3=size                                                | W0=result                                                |
| 0x6B | svcWriteDebugProcessMemory                                                         | X0=debug\_handle, X1=buffer\*, X2=dst\_addr, X3=size                                                | W0=result                                                |
| 0x6C | svcSetHardwareBreakPoint                                                           |                                                                                                     |                                                          |
| 0x6D | svcGetDebugThreadParam                                                             | X2=debug\_handle, X3=thread\_id, W4=DebugThreadParam                                                | W0=result, X1=out0, W2=out1                              |
| 0x70 | svcCreatePort                                                                      |                                                                                                     |                                                          |
| 0x71 | svcManageNamedPort                                                                 | X1=name\_ptr, W2=max\_sessions(?)                                                                   | W0=result, W1=serverport\_handle                         |
| 0x72 | svcConnectToPort                                                                   | W1=clientport\_handle                                                                               | W0=result, W1=session\_handle                            |
| 0x73 | svcSetProcessMemoryPermission                                                      | X0=addr, X1=size, W2=perm                                                                           | W0=result                                                |
| 0x74 | [\#svcMapProcessMemory](#svcMapProcessMemory "wikilink")                           | X0=srcaddr, W1=process\_handle, X2=dstaddr, X3=size                                                 | W0=result                                                |
| 0x75 | [\#svcUnmapProcessMemory](#svcUnmapProcessMemory "wikilink")                       | W0=process\_handle, X1=dstaddr, X2=srcaddr, X3=size                                                 | W0=result                                                |
| 0x76 | [\#svcQueryProcessMemory](#svcQueryProcessMemory "wikilink")                       | X0=meminfo\_ptr, W2=process\_handle, X3=addr                                                        | W0=result, W1=pageinfo                                   |
| 0x77 | [\#svcMapProcessCodeMemory](#svcMapProcessCodeMemory "wikilink")                   | W0=process\_handle, X2=dstaddr, X2=srcaddr, X3=size                                                 | W0=result                                                |
| 0x78 | [\#svcUnmapProcessCodeMemory](#svcUnmapProcessCodeMemory "wikilink")               | W0=process\_handle, X1=dstaddr, X2=srcaddr, X3=size                                                 | W0=result                                                |
| 0x79 | [\#svcCreateProcess](#svcCreateProcess "wikilink")                                 | X1=procinfo\_ptr, X2=caps\_ptr, W3=cap\_num                                                         | W0=result, W1=process\_handle                            |
| 0x7A | svcStartProcess                                                                    | W0=process\_handle, W1=main\_thread\_prio, W2=default\_cpuid, W3=main\_thread\_stacksz              | W0=result                                                |
| 0x7B | svcTerminateProcess                                                                | W0=process\_handle                                                                                  | W0=result                                                |
| 0x7C | [\#svcGetProcessInfo](#svcGetProcessInfo "wikilink")                               | W0=process\_handle                                                                                  | W0=result, X1=[\#ProcessState](#ProcessState "wikilink") |
| 0x7D | svcCreateResourceLimit                                                             | None                                                                                                | W0=result, W1=reslimit\_handle                           |
| 0x7E | svcSetResourceLimitLimitValue                                                      | W0=reslimit\_handle, W1=[\#LimitableResource](#LimitableResource "wikilink"), X2=value              | W0=result                                                |
| 0x7F | svcCallSecureMonitor                                                               |                                                                                                     |                                                          |

## svcSetHeapSize

<div style="display: inline-block;">

| Argument | Type                           | Name      |
| -------- | ------------------------------ | --------- |
| (In) W1  | u64                            | `Size`    |
| (Out) W0 | [\#Result](#Result "wikilink") | `Ret`     |
| (Out) X1 | u64                            | `OutAddr` |

</div>

**Description:** Set the process heap to a given `Size`. It can both
extend and shrink the heap.

`Size` must be a multiple of 0x2000000.

On success, the heap base-address (which is fixed by kernel, aslr'd) is
written to `OutAddr`.

\[2.0.0+\] `Size` must be less than 0x18000000.

## svcSetMemoryPermission

**Description:** Change permission of page-aligned memory region.

Bit2 of permission (exec) is not allowed. Setting write-only is not
allowed either (bit1).

This can be used to move back and forth between ---, r-- and rw-.

<div style="display: inline-block;">

| Argument | Type                           | Name   |
| -------- | ------------------------------ | ------ |
| (In) X0  | u64                            | `Addr` |
| (In) X1  | u64                            | `Size` |
| (In) W2  | u64                            | `Prot` |
| (Out) W0 | [\#Result](#Result "wikilink") | `Ret`  |

</div>

## svcSetMemoryAttribute

**Description:** Change attribute of page-aligned memory region.

This is used to turn on/off caching for a given memory area. Useful when
talking to devices such as the GPU.

What happens "under the hood" is the "Memory Attribute Indirection
Register" index is changed from 2 to 3 in the MMU descriptor.

<div style="display: inline-block;">

| Argument | Type                           | Name     |
| -------- | ------------------------------ | -------- |
| (In) X0  | u64                            | `Addr`   |
| (In) X1  | u64                            | `Size`   |
| (In) W2  | u64                            | `State0` |
| (In) W3  | u64                            | `State1` |
| (Out) W0 | [\#Result](#Result "wikilink") | `Ret`    |

</div>

| State0 | State1 | Action                                                          |
| ------ | ------ | --------------------------------------------------------------- |
| 0      | 0      | Clear bit3 in [\#MemoryAttribute](#MemoryAttribute "wikilink"). |
| 8      | 0      | Clear bit3 in [\#MemoryAttribute](#MemoryAttribute "wikilink"). |
| 8      | 8      | Set bit3 in [\#MemoryAttribute](#MemoryAttribute "wikilink").   |

## svcMapMemory

**Description:** Maps a memory range into a different range.

Mainly used for adding guard pages around stack.

Source range gets reprotected to --- (it can no longer be accessed), and
bit0 is set in the source
[\#MemoryAttribute](#MemoryAttribute "wikilink").

If dstaddr \>= LowerTreshold, the dst-range is enforced to be within the
process' "MapRegion". Code can get the range of this region from
[\#svcGetInfo](#svcGetInfo "wikilink") id0=2,3.

In this case, the mapped memory will have state `0x5C3C0B`.

As long as (dstaddr+size) \< LowerThreshold, then you can map anywhere
but the mapped memory will have state `0x482907` instead.

LowerTreshold is 0x80000000 for 36-bit address spaces, and 0x40000000
for 32-bit ones.

\[2.0.0+\] Support for the `0x482907` mappings outside the "MapRegion"
were removed.

<div style="display: inline-block;">

| Argument | Type                           | Name   |
| -------- | ------------------------------ | ------ |
| (In) X0  | u64                            | `Dst`  |
| (In) X1  | u64                            | `Src`  |
| (In) X2  | u64                            | `Size` |
| (Out) W0 | [\#Result](#Result "wikilink") | `Ret`  |

</div>

## svcUnmapMemory

**Description:** Unmaps a region that was previously mapped with
[\#svcMapMemory](#svcMapMemory "wikilink").

It's possible to unmap ranges partially, you don't need to unmap the
entire range "in one go".

The srcaddr/dstaddr must match what was given when the pages were
originally mapped.

<div style="display: inline-block;">

| Argument | Type                           | Name   |
| -------- | ------------------------------ | ------ |
| (In) X0  | u64                            | `Dst`  |
| (In) X1  | u64                            | `Src`  |
| (In) X2  | u64                            | `Size` |
| (Out) W0 | [\#Result](#Result "wikilink") | `Ret`  |

</div>

## svcQueryMemory

**Description:** Query information about an address. Will always fetch
the lowest page-aligned mapping that contains the provided address.

Outputs a [\#MemoryInfo](#MemoryInfo "wikilink") struct.

<div style="display: inline-block;">

| Argument | Type                           | Name        |
| -------- | ------------------------------ | ----------- |
| (In) X0  | MemoryInfo\*                   | `Mem Info`  |
| (In) X2  | u64                            | `Addr`      |
| (Out) W0 | [\#Result](#Result "wikilink") | `Ret`       |
| (Out) W1 | PageInfo                       | `Page Info` |

</div>

## svcExitProcess

**Description:** Exits the current process.

<div style="display: inline-block;">

| Argument   | Type | Name |
| ---------- | ---- | ---- |
| (In) None  |      |      |
| (Out) None |      |      |

</div>

## svcCreateThread

**Description:** Create a thread in the current process.

Processor\_id must be 0,1,2,3 or -2, where -2 uses the default cpuid for
process.

<div style="display: inline-block;">

| Argument | Type                           | Name           |
| -------- | ------------------------------ | -------------- |
| (In) X1  | u64                            | `Entry`        |
| (In) X2  | u64                            | `Arg`          |
| (In) X3  | u64                            | `Stack Top`    |
| (In) W4  | u64                            | `Priority`     |
| (In) W5  | u64                            | `Processor ID` |
| (Out) W0 | [\#Result](#Result "wikilink") | `Ret`          |
| (Out) W1 | Handle                         | `Handle`       |

</div>

## svcStartThread

**Description:** Starts the thread for the provided handle.

<div style="display: inline-block;">

| Argument   | Type | Name     |
| ---------- | ---- | -------- |
| (In) W0    | u64  | `Handle` |
| (Out) None |      |          |

</div>

## svcExitThread

**Description:** Exits the current thread.

<div style="display: inline-block;">

| Argument   | Type | Name |
| ---------- | ---- | ---- |
| (In) None  |      |      |
| (Out) None |      |      |

</div>

## svcSleepThread

**Description:** Sleep for a specified amount of time, or yield thread.

Setting nano=0 means "yield thread".

## svcGetThreadPriority

**Description:** Get priority of provided thread handle.

## svcSetThreadPriority

**Description:** Set priority of provided thread handle.

Priority is a number 0-0x3F. Lower value means higher priority.

## svcGetThreadCoreMask

**Description:** Get affinity mask of provided thread handle.

## svcSetThreadCoreMask

**Description:** Set affinity mask of provided thread handle.

## svcGetCurrentProcessorNumber

**Description:** Get which cpu is executing the current thread.

Cpu-id is an integer in the range 0-3.

<div style="display: inline-block;">

| Argument    | Type | Name     |
| ----------- | ---- | -------- |
| (In) None   |      |          |
| (Out) W0/X0 | u64  | `CPU ID` |

</div>

## svcMapSharedMemory

Maps the block supplied by the handle. The required permissions are
different for the process that created the handle and all other
processes.

Increases reference count for the KSharedMemory object. Thus in order to
release the memory associated with the object, all handles to it must be
closed and all mappings must be unmapped.

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

| Handle type | Id0        | Id1                   | Description                                                                                                 |
| ----------- | ---------- | --------------------- | ----------------------------------------------------------------------------------------------------------- |
| Process     | 0          | 0                     | AllowedCpuIdBitmask                                                                                         |
| Process     | 1          | 0                     | AllowedThreadPrioBitmask                                                                                    |
| Process     | 2          | 0                     | ReservedMapRegionBaseAddress                                                                                |
| Process     | 3          | 0                     | ReservedMapRegionSize                                                                                       |
| Process     | 4          | 0                     | ReservedHeapRegionBaseAddress                                                                               |
| Process     | 5          | 0                     | ReservedHeapRegionSize                                                                                      |
| Process     | 6          | 0                     | TotalMemoryUsage                                                                                            |
| Process     | 7          | 0                     | TotalHeapUsage                                                                                              |
| Zero        | 8          | 0                     | IsCurrentProcessBeingDebugged                                                                               |
| Zero        | 9          | 0                     | Returns ResourceLimit handle for current process. Used by [PM](Process%20Manager%20services.md "wikilink"). |
| Zero        | 10         | \-1, {current coreid} | Unknown. Output data changes each time this SVC is used. Global and core-specific tick-count?               |
| Zero        | 11         | 0-3                   | RandomEntropy from current process. TRNG. Used to seed usermode PRNGs.                                      |
| Process     | 12         | 0                     | \[2.0.0+\] AddressSpaceStart                                                                                |
| Process     | 13         | 0                     | \[2.0.0+\] AddressSpaceSize                                                                                 |
| Process     | 14         | 0                     | \[2.0.0+\] NewReservedRegionStartAddr                                                                       |
| Process     | 15         | 0                     | \[2.0.0+\] NewReservedRegionSize                                                                            |
| Process     | 18         | 0                     | \[3.0.0+\] Title-id.                                                                                        |
| Thread      | 0xF0000002 | 0                     | Performance counter related.                                                                                |

## svcDumpInfo

Does nothing, just returns with registers set to all-zero.

## svcReadWriteRegister

Read/write IO registers with a hardcoded whitelist. Input address is
physical-address and must be aligned to 4.

rw\_mask is 0 for reading and 0xffffffff for writing. You can also write
individual bits by using a mask value.

You can only write to registers inside physical pages 0x70019000 (MC),
0x7001C000 (MC0), 0x7001D000 (MC1), and they all share the same
whitelist.

The whitelist is same for writing as for reading.

The whitelist is:
`0x054, 0x090, 0x094, 0x098, 0x09c, 0x0a0, 0x0a4, 0x0a8, 0x0ac, 0x0b0, 0x0b4, 0x0b8, 0x0bc, 0x0c0, 0x0c4, 0x0c8, 0x0d0, 0x0d4, 0x0d8, 0x0dc, 0x0e0, 0x100, 0x108, 0x10c, 0x118, 0x11c, 0x124, 0x128, 0x12c, 0x130, 0x134, 0x138, 0x13c, 0x158, 0x15c, 0x164, 0x168, 0x16c, 0x170, 0x174, 0x178, 0x17c, 0x200, 0x204, 0x2e4, 0x2e8, 0x2ec, 0x2f4, 0x2f8, 0x310, 0x314, 0x320, 0x328, 0x344, 0x348, 0x370, 0x374, 0x37c, 0x380, 0x390, 0x394, 0x398, 0x3ac, 0x3b8, 0x3bc, 0x3c0, 0x3c4, 0x3d8, 0x3e8, 0x41c, 0x420, 0x424, 0x428, 0x42c, 0x430, 0x44c, 0x47c, 0x480, 0x484, 0x50c, 0x554, 0x558, 0x55c, 0x670, 0x674, 0x690, 0x694, 0x698, 0x69c, 0x6a0, 0x6a4, 0x6c0, 0x6c4, 0x6f0, 0x6f4, 0x960, 0x970, 0x974, 0xa20, 0xa24, 0xb88, 0xb8c, 0xbc4, 0xbc8, 0xbcc, 0xbd0, 0xbd4, 0xbd8, 0xbdc, 0xbe0, 0xbe4, 0xbe8, 0xbec, 0xc00, 0xc5c, 0xcac`

\[2.0.0+\] Whitelist was extended with
`0x4c4, 0x4c8, 0x4cc, 0x584, 0x588, 0x58c.`

\[2.0.0+\] The IO registers in range 0x7000E400 (PMC) size 0xC00 skip
the whitelist, and do a TrustZone call using [SMC](SMC.md "wikilink")
Id1 0xC3000008(ReadWriteRegister).

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

**Description:** Returns a virtual address mapped to a given IO range.

## svcCreateDeviceAddressSpace

**Description:** Creates a virtual address space for binding device
address spaces and returns a handle.

dev\_as\_start\_addr is normally set to 0 and dev\_as\_end\_addr is
normally set to 0xFFFFFFFF.

## svcAttachDeviceAddressSpace

**Description:** Attaches a device address space to a
[device](#DeviceName "wikilink").

## svcDetachDeviceAddressSpace

**Description:** Detaches a device address space from a
[device](#DeviceName "wikilink").

## svcMapDeviceAddressSpaceByForce

**Description:** Maps an attached device address space to an userspace
address.

dev\_map\_addr is the userspace destination address, while dev\_as\_addr
is the source address between dev\_as\_start\_addr and
dev\_as\_end\_addr (passed to
[\#svcCreateDeviceAddressSpace](#svcCreateDeviceAddressSpace "wikilink")).

The userspace destination address must have the
[MapDeviceAllowed](SVC#MemoryState.md##MemoryState "wikilink") bit set.
Bit [IsDeviceMapped](SVC#MemoryAttribute.md##MemoryAttribute "wikilink")
will be set after mapping.

## svcMapDeviceAddressSpaceAligned

**Description:** Maps an attached device address space to an userspace
address.

Same as
[\#svcMapDeviceAddressSpaceByForce](#svcMapDeviceAddressSpaceByForce "wikilink"),
but the userspace destination address must have the
[MapDeviceAlignedAllowed](SVC#MemoryState.md##MemoryState "wikilink")
bit set instead.

## svcUnmapDeviceAddressSpace

**Description:** Unmaps an attached device address space from an
userspace address.

## svcMapProcessMemory

Maps the src address from the supplied process handle into the current
process.

This allows mapping code and rodata with RW- permission.

## svcUnmapProcessMemory

Unmaps what was mapped by
[\#svcMapProcessMemory](#svcMapProcessMemory "wikilink").

## svcQueryProcessMemory

Equivalent to [\#svcQueryMemory](#svcQueryMemory "wikilink") except
takes a process handle.

## svcMapProcessCodeMemory

Takes a process handle, and maps normal heap in that process as
executable code in that process. Used when loading NROs.

## svcUnmapProcessCodeMemory

Unmaps what was mapped by
[\#svcMapProcessCodeMemory](#svcMapProcessCodeMemory "wikilink").

## svcCreateProcess

Takes a [\#CreateProcessInfo](#CreateProcessInfo "wikilink") as input.

## svcGetProcessInfo

Returns an enum with value 0-7.

## Debugging

\[2.0.0+\] Exactly 6 debug SVCs require that
[IsDebugMode](SPL%20services#GetConfig.md##GetConfig "wikilink") is
non-zero. Error 0x4201 is returned otherwise.

  - svcBreakDebugProcess
  - svcContinueDebugEvent
  - svcWriteDebugProcessMemory
  - svcSetDebugThreadContext
  - svcTerminateDebugProcess
  - svcSetHardwareBreakPoint

svcDebugActiveProcess stops execution of the target process, the normal
method for resuming it requires svcContinueDebugEvent(see above).
Closing the debug handle also results in execution being resumed.

# Structures

## DeviceName

| Value | Name                   |
| ----- | ---------------------- |
| 0     | DeviceName\_AFI        |
| 1     | DeviceName\_AVPC       |
| 2     | DeviceName\_DC         |
| 3     | DeviceName\_DCB        |
| 4     | DeviceName\_HC         |
| 5     | DeviceName\_HDA        |
| 6     | DeviceName\_ISP2       |
| 7     | DeviceName\_MSENCNVENC |
| 8     | DeviceName\_NV         |
| 9     | DeviceName\_NV2        |
| 10    | DeviceName\_PPCS       |
| 11    | DeviceName\_SATA       |
| 12    | DeviceName\_VI         |
| 13    | DeviceName\_VIC        |
| 14    | DeviceName\_XUSB\_HOST |
| 15    | DeviceName\_XUSB\_DEV  |
| 16    | DeviceName\_TSEC       |
| 17    | DeviceName\_PPCS1      |
| 18    | DeviceName\_DC1        |
| 19    | DeviceName\_SDMMC1A    |
| 20    | DeviceName\_SDMMC2A    |
| 21    | DeviceName\_SDMMC3A    |
| 22    | DeviceName\_SDMMC4A    |
| 23    | DeviceName\_ISP2B      |
| 24    | DeviceName\_GPU        |
| 25    | DeviceName\_GPUB       |
| 26    | DeviceName\_PPCS2      |
| 27    | DeviceName\_NVDEC      |
| 28    | DeviceName\_APE        |
| 29    | DeviceName\_SE         |
| 30    | DeviceName\_NVJPG      |
| 31    | DeviceName\_HC1        |
| 32    | DeviceName\_SE1        |
| 33    | DeviceName\_AXIAP      |
| 34    | DeviceName\_ETR        |
| 35    | DeviceName\_TSECB      |
| 36    | DeviceName\_TSEC1      |
| 37    | DeviceName\_TSECB1     |
| 38    | DeviceName\_NVDEC1     |

## LimitableResource

| Value | Name                                |
| ----- | ----------------------------------- |
| 0     | LimitableResource\_Memory           |
| 1     | LimitableResource\_Threads          |
| 2     | LimitableResource\_Events           |
| 3     | LimitableResource\_TransferMemories |
| 4     | LimitableResource\_Sessions         |

## CreateProcessInfo

| Offset | Length | Bits   | Description                                        |
| ------ | ------ | ------ | -------------------------------------------------- |
| 0      | 12     |        | ProcessName (doesn't have to be null-terminated)   |
| 0xC    | 4      |        |                                                    |
| 0x10   | 8      |        | TitleId                                            |
| 0x18   | 8      |        | CodeAddr                                           |
| 0x20   | 4      |        | CodeNumPages                                       |
| 0x24   | 4      |        | MmuFlags                                           |
|        |        | Bit0   | Is64bit                                            |
|        |        | Bit3-1 | [\#AddressSpaceType](#AddressSpaceType "wikilink") |
|        |        | Bit4   |                                                    |
|        |        | Bit5   | EnableAslr                                         |
|        |        | Bit6   | IsSystem                                           |
| 0x28   | 4      |        | ResourceLimitHandle                                |
| 0x2C   | 4      |        |                                                    |

### AddressSpaceType

| Type | Name                     | Width | Description                            |
| ---- | ------------------------ | ----- | -------------------------------------- |
| 0    | Normal\_32Bit            | 32    |                                        |
| 1    | Normal\_36Bit            | 36    |                                        |
| 2    | WithoutMap\_32Bit        | 32    | Appears to be missing map region \[?\] |
| 3    | \[2.0.0+\] Normal\_39Bit | 39    |                                        |

## MemoryInfo

| Offset | Length | Description                                                          |
| ------ | ------ | -------------------------------------------------------------------- |
| 0      | 8      | BaseAddress                                                          |
| 8      | 8      | Size                                                                 |
| 0x10   | 4      | MemoryType: lower 8 bits of [\#MemoryState](#MemoryState "wikilink") |
| 0x14   | 4      | [\#MemoryAttribute](#MemoryAttribute "wikilink")                     |
| 0x18   | 4      | Permission (bit0: R, bit1: W, bit2: X)                               |
| 0x1C   | 4      | DeviceRefCount                                                       |
| 0x20   | 4      | IpcRefCount                                                          |
| 0x24   | 4      | Padding: always zero                                                 |

## MemoryAttribute

| Bits | Description                               |
| ---- | ----------------------------------------- |
| 0    | IsBorrowed                                |
| 1    | IsIpcMapped: when IpcRefCount \> 0.       |
| 2    | IsDeviceMapped: when DeviceRefCount \> 0. |
| 3    | IsUncached                                |

## MemoryState

| Bits | Description                                                                                                                                                                |
| ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 7-0  | Type                                                                                                                                                                       |
| 8    | [PermissionChangeAllowed](#svcSetMemoryPermission "wikilink")                                                                                                              |
| 9    | IsUserWritable \[?\]                                                                                                                                                       |
| 10   | IpcSendAllowed\_Type0                                                                                                                                                      |
| 11   | IpcSendAllowed\_Type3                                                                                                                                                      |
| 12   | IpcSendAllowed\_Type1                                                                                                                                                      |
| 14   | [ProcessPermissionChangeAllowed](#svcSetProcessMemoryPermission "wikilink")                                                                                                |
| 15   | [MapAllowed](#svcMapMemory "wikilink")                                                                                                                                     |
| 16   | [UnmapProcessCodeMemoryAllowed](#svcUnmapProcessCodeMemory "wikilink")                                                                                                     |
| 17   | [TransferMemoryAllowed](#svcCreateTransferMemory "wikilink")                                                                                                               |
| 19   | MapDeviceAllowed ([\#svcMapDeviceAddressSpace](#svcMapDeviceAddressSpace "wikilink") and [\#svcMapDeviceAddressSpaceByForce](#svcMapDeviceAddressSpaceByForce "wikilink")) |
| 20   | [MapDeviceAlignedAllowed](#svcMapDeviceAddressSpaceAligned "wikilink")                                                                                                     |
| 21   | [IpcBufferAllowed](#svcSendSyncRequestWithUserBuffer "wikilink")                                                                                                           |
| 22   | IsPoolAllocated/IsReferenceCounted                                                                                                                                         |
| 23   | [MapProcessAllowed](#svcMapProcessMemory "wikilink")                                                                                                                       |
| 24   | [AttributeChangeAllowed](#svcSetMemoryAttribute "wikilink")                                                                                                                |

| Value        | Type                                                           | Meaning                                                                                                             |
| ------------ | -------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| `0x00000000` | Unmapped                                                       |                                                                                                                     |
| `0x00002001` | IO                                                             | Mapped by kernel capability parsing in [\#svcCreateProcess](#svcCreateProcess "wikilink").                          |
| `0x00042002` | Normal                                                         | Mapped by kernel capability parsing in [\#svcCreateProcess](#svcCreateProcess "wikilink").                          |
| `0x00DC7E03` | Code static                                                    | Mapped during [\#svcCreateProcess](#svcCreateProcess "wikilink").                                                   |
| `0x01FEBD04` | Code                                                           | Transition from 0xDC7E03 performed by [\#svcSetProcessMemoryPermission](#svcSetProcessMemoryPermission "wikilink"). |
| `0x017EBD05` | Heap                                                           | Mapped using [\#svcSetHeapSize](#svcSetHeapSize "wikilink").                                                        |
| `0x00402006` | Shared memory block                                            | Mapped using [\#svcMapSharedMemory](#svcMapSharedMemory "wikilink").                                                |
| `0x00482907` | \[1.0.0\] Weird mapped memory                                  | Mapped using [\#svcMapMemory](#svcMapMemory "wikilink").                                                            |
| `0x00DD7E08` | Module code static                                             | Mapped using [\#svcMapProcessCodeMemory](#svcMapProcessCodeMemory "wikilink").                                      |
| `0x01FFBD09` | Module code mutable                                            | Transition from 0xDD7E08 performed by [\#svcSetProcessMemoryPermission](#svcSetProcessMemoryPermission "wikilink"). |
| `0x005C3C0A` | [IPC](IPC%20Marshalling.md "wikilink") buffers                 | IPC buffers with descriptor flags=0.                                                                                |
| `0x005C3C0B` | Mapped memory                                                  | Mapped using [\#svcMapMemory](#svcMapMemory "wikilink").                                                            |
| `0x0040200C` | [Thread local storage](Thread%20Local%20Storage.md "wikilink") | Mapped during [\#svcCreateThread](#svcCreateThread "wikilink").                                                     |
| `0x015C3C0D` | Isolated transfer memory                                       | Mapped using [\#svcMapTransferMemory](#svcMapTransferMemory "wikilink") when the owning process has perm=0.         |
| `0x005C380E` | Transfer memory                                                | Mapped using [\#svcMapTransferMemory](#svcMapTransferMemory "wikilink") when the owning process has perm\!=0.       |
| `0x0040380F` | Process memory                                                 | Mapped using [\#svcMapProcessMemory](#svcMapProcessMemory "wikilink").                                              |
| `0x00000010` | Reserved                                                       |                                                                                                                     |
| `0x005C3811` | [IPC](IPC%20Marshalling.md "wikilink") buffers                 | IPC buffers with descriptor flags=1.                                                                                |
| `0x004C2812` | [IPC](IPC%20Marshalling.md "wikilink") buffers                 | IPC buffers with descriptor flags=3.                                                                                |
| `0x00002013` | Kernel per-thread stack                                        | Mapped in kernel during [\#svcCreateThread](#svcCreateThread "wikilink").                                           |

# Exception handling

There is userland code for handling exceptions, however this doesn't
seem to be executed on retail mode.

When a usermode exception occurs, it jumps to the main code binary
entrypoint (main\_binary\_address + 0 == **\_start**).

During normal boot **\_start** is invoked with X0=0 and
X1=main\_thread\_handle (triggering normal crt0 setup). During an
usermode exception **\_start** is invoked with X0=exception\_info0\_ptr
and X1=exception\_info1\_ptr instead.

The **\_start** method determines whether to boot normally or handle an
exception if X0 is set to 0 or not.

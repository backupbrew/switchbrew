# System calls

| Id   | Name                                                                               | In                                                                                          | Out                                                 |
| ---- | ---------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | --------------------------------------------------- |
| 0x1  | [\#svcSetHeapSize](#svcSetHeapSize "wikilink")                                     | W1=size                                                                                     | W0=result, X1=outaddr                               |
| 0x2  | [\#svcSetMemoryPermission](#svcSetMemoryPermission "wikilink")                     | X0=addr, X1=size, W2=prot                                                                   | W0=result                                           |
| 0x3  | [\#svcSetMemoryAttribute](#svcSetMemoryAttribute "wikilink")                       | X0=addr, X1=size, W2=state0, W3=state1                                                      | W0=result                                           |
| 0x4  | [\#svcMapMemory](#svcMapMemory "wikilink")                                         | X0=dstaddr, X1=srcaddr, X2=size                                                             | W0=result                                           |
| 0x5  | [\#svcUnmapMemory](#svcUnmapMemory "wikilink")                                     | X0=dstaddr, X1=srcaddr, X2=size                                                             | W0=result                                           |
| 0x6  | [\#svcQueryMemory](#svcQueryMemory "wikilink")                                     | X0=MemoryInfo\*, X2=addr                                                                    | W0=result, W1=PageInfo                              |
| 0x7  | [\#svcExitProcess](#svcExitProcess "wikilink")                                     | None                                                                                        |                                                     |
| 0x8  | [\#svcCreateThread](#svcCreateThread "wikilink")                                   | X1=entry, X2=arg, X3=stacktop, W4=prio, W5=processor\_id                                    | W0=result, W1=handle                                |
| 0x9  | [\#svcStartThread](#svcStartThread "wikilink")                                     | W0=thread\_handle                                                                           | W0=result                                           |
| 0xA  | [\#svcExitThread](#svcExitThread "wikilink")                                       | None                                                                                        |                                                     |
| 0xB  | [\#svcSleepThread](#svcSleepThread "wikilink")                                     | X0=nano                                                                                     | W0=result                                           |
| 0xC  | [\#svcGetThreadPriority](#svcGetThreadPriority "wikilink")                         | W1=thread\_handle                                                                           | W0=result, W1=prio                                  |
| 0xD  | [\#svcSetThreadPriority](#svcSetThreadPriority "wikilink")                         | W0=thread\_handle, W1=prio                                                                  | W0=result                                           |
| 0xE  | [\#svcGetThreadCoreMask](#svcGetThreadCoreMask "wikilink")                         | W2=thread\_handle                                                                           | W0=result, W1=out, X2=out                           |
| 0xF  | [\#svcSetThreadCoreMask](#svcSetThreadCoreMask "wikilink")                         | W0=thread\_handle, W1=in, X2=in2                                                            | W0=result                                           |
| 0x10 | [\#svcGetCurrentProcessorNumber](#svcGetCurrentProcessorNumber "wikilink")         | None                                                                                        | W0/X0=cpuid                                         |
| 0x11 | svcSignalEvent                                                                     | W0=wevent\_handle                                                                           | W0=result                                           |
| 0x12 | svcClearEvent                                                                      | W0=wevent\_or\_revent\_handle                                                               | W0=result                                           |
| 0x13 | [\#svcMapSharedMemory](#svcMapSharedMemory "wikilink")                             | W0=memblk\_handle, X1=addr, X2=size, W3=perm                                                | W0=result                                           |
| 0x14 | svcUnmapSharedMemory                                                               | W0=memblk\_handle, X1=addr, X2=size                                                         | W0=result                                           |
| 0x15 | [\#svcCreateTransferMemory](#svcCreateTransferMemory "wikilink")                   | X1=addr, X2=size, W3=perm                                                                   | W0=result, W1=handle                                |
| 0x16 | svcCloseHandle                                                                     | W0=handle                                                                                   | W0=result                                           |
| 0x17 | svcResetSignal                                                                     | W0=handle                                                                                   | W0=result                                           |
| 0x18 | [\#svcWaitSynchronization](#svcWaitSynchronization "wikilink")                     | X1=handles\_ptr, W2=num\_handles. X3=timeout                                                | W0=result, W1=handle\_idx                           |
| 0x19 | svcCancelSynchronization                                                           | W0=handle                                                                                   | W0=result                                           |
| 0x1A | svcArbitrateLock                                                                   | W0=cur\_thread\_handle, X1=ptr, W2=req\_thread\_handle                                      |                                                     |
| 0x1B | svcArbitrateUnlock                                                                 | X0=ptr                                                                                      |                                                     |
| 0x1C | svcWaitProcessWideKeyAtomic                                                        | X0=ptr0, X1=ptr, W2=thread\_handle, X3=timeout                                              | W0=result                                           |
| 0x1D | svcSignalProcessWideKey                                                            | X0=ptr, W1=value                                                                            | W0=result                                           |
| 0x1E | svcGetSystemTick                                                                   |                                                                                             | X0={value of cntpct\_el0}                           |
| 0x1F | svcConnectToNamedPort                                                              | X1=port\_name\_str                                                                          | W0=result, W1=handle                                |
| 0x20 | svcSendSyncRequestLight                                                            |                                                                                             |                                                     |
| 0x21 | svcSendSyncRequest                                                                 | X0=handle                                                                                   | W0=result                                           |
| 0x22 | [\#svcSendSyncRequestWithUserBuffer](#svcSendSyncRequestWithUserBuffer "wikilink") | X0=cmdbufptr, X1=size, X2=handle                                                            | W0=result                                           |
| 0x23 | svcSendAsyncRequestWithUserBuffer                                                  |                                                                                             |                                                     |
| 0x24 | svcGetProcessId                                                                    |                                                                                             |                                                     |
| 0x25 | svcGetThreadId                                                                     | W0=thread\_handle                                                                           | W0=result, X1=out                                   |
| 0x26 | svcBreak                                                                           | X0,X1,X2=info                                                                               | ?                                                   |
| 0x27 | svcOutputDebugString                                                               | X0=str, X1=size                                                                             |                                                     |
| 0x28 | svcReturnFromException                                                             | X0=result                                                                                   |                                                     |
| 0x29 | [\#svcGetInfo](#svcGetInfo "wikilink")                                             | X1=info\_id, X2=handle, X3=info\_sub\_id                                                    | W0=result, X1=out                                   |
| 0x2A | svcFlushEntireDataCache                                                            |                                                                                             |                                                     |
| 0x2B | svcFlushDataCache                                                                  |                                                                                             |                                                     |
| 0x2C | \[ [3.0.0](3.0.0.md "wikilink")+ \] svcMapPhysicalMemory                           |                                                                                             |                                                     |
| 0x2D | \[ [3.0.0](3.0.0.md "wikilink")+ \] svcUnmapPhysicalMemory                         |                                                                                             |                                                     |
| .... | ?                                                                                  | ?                                                                                           | ?                                                   |
| 0x2F | svcGetLastThreadInfo                                                               |                                                                                             |                                                     |
| 0x30 | svcGetResourceLimitLimitValue                                                      |                                                                                             |                                                     |
| 0x31 | svcGetResourceLimitCurrentValue                                                    |                                                                                             |                                                     |
| 0x32 | svcSetThreadActivity                                                               |                                                                                             |                                                     |
| 0x33 | svcGetThreadContext3                                                               |                                                                                             |                                                     |
| 0x3C | svcDumpInfo                                                                        |                                                                                             |                                                     |
| 0x40 | svcCreateSession                                                                   | W2=?, X3=?                                                                                  | W0=result, W1=client\_handle, W2=server\_handle     |
| 0x41 | svcAcceptSession                                                                   | W1=port\_handle                                                                             | W0=result, W1=session\_handle                       |
| 0x42 | svcReplyAndReceiveLight                                                            |                                                                                             |                                                     |
| 0x43 | svcReplyAndReceive                                                                 | X1=ptr\_handles, W2=num\_handles, X3=replytarget\_handle(0=none), X4=timeout                | W0=result, W1=handle\_idx                           |
| 0x44 | svcReplyAndReceiveWithUserBuffer                                                   | X1=buf, X2=sz, X3=ptr\_handles, W4=num\_handles, X5=replytarget\_handle(0=none), X6=timeout | W0=result, W1=handle\_idx                           |
| 0x45 | svcCreateEvent                                                                     | None                                                                                        | W0=result, W1=client\_handle ?, W2=server\_handle ? |
| 0x4D | svcSleepSystem                                                                     |                                                                                             |                                                     |
| 0x4E | [\#svcReadWriteRegister](#svcReadWriteRegister "wikilink")                         | X1=reg\_addr, W2=rw\_mask, W3=in\_val                                                       | W0=result, W1=out\_val                              |
| 0x4F | svcSetProcessActivity                                                              |                                                                                             |                                                     |
| 0x50 | [\#svcCreateSharedMemory](#svcCreateSharedMemory "wikilink")                       | W1=size?, W2=myperm, W3=otherperm                                                           | W0=result, W1=handle                                |
| 0x51 | [\#svcMapTransferMemory](#svcMapTransferMemory "wikilink")                         | X0=mirror\_handle, X1=addr, X2=size, W3=perm                                                | W0=result                                           |
| 0x52 | [\#svcUnmapTransferMemory](#svcUnmapTransferMemory "wikilink")                     | W0=mirror\_handle, X1=addr, X2=size                                                         | W0=result                                           |
| 0x53 | svcCreateInterruptEvent                                                            | X1=irq\_id, W2=flag                                                                         | W0=result, W1=handle                                |
| 0x54 | [\#svcQueryPhysicalAddress](#svcQueryPhysicalAddress "wikilink")                   |                                                                                             |                                                     |
| 0x55 | [\#svcQueryIoMapping](#svcQueryIoMapping "wikilink")                               | X1=physaddr, X2=size                                                                        | W0=result, X1=virtaddr                              |
| 0x56 | svcCreateDeviceAddressSpace                                                        | X1=dev\_addr, X2=dev\_size                                                                  | W0=result, W1=handle                                |
| 0x57 | [\#svcAttachDeviceAddressSpace](#svcAttachDeviceAddressSpace "wikilink")           | W0=device, X1=handle                                                                        | W0=result                                           |
| 0x58 | [\#svcDetachDeviceAddressSpace](#svcDetachDeviceAddressSpace "wikilink")           | W0=device, X1=handle                                                                        | W0=result                                           |
| 0x59 | svcMapDeviceAddressSpaceByForce                                                    | W0=handle, W1=proc\_handle, X2=dev\_addr, X3=dev\_size, X4=map\_addr, W5=perm               | W0=result                                           |
| 0x5A | svcMapDeviceAddressSpaceAligned                                                    | W0=handle, W1=proc\_handle, X2=dev\_addr, X3=dev\_size, X4=map\_addr, W5=perm               | W0=result                                           |
| 0x5B | svcMapDeviceAddressSpace                                                           |                                                                                             |                                                     |
| 0x5C | svcUnmapDeviceAddressSpace                                                         | W0=handle, W1=proc\_handle, X2=map\_addr, X3=map\_size, W4=perm                             | W0=result                                           |
| 0x5D | svcInvalidateProcessDataCache                                                      |                                                                                             |                                                     |
| 0x5E | svcStoreProcessDataCache                                                           |                                                                                             |                                                     |
| 0x5F | svcFlushProcessDataCache                                                           |                                                                                             |                                                     |
| 0x60 | svcDebugActiveProcess                                                              | X1=processID                                                                                | W0=result, W1=out\_debughandle                      |
| 0x61 | svcBreakDebugProcess                                                               |                                                                                             |                                                     |
| 0x62 | svcTerminateDebugProcess                                                           |                                                                                             |                                                     |
| 0x63 | svcGetDebugEvent                                                                   | X0=DebugEventInfo\*, W1=debughandle                                                         | W0=result                                           |
| 0x64 | svcContinueDebugEvent                                                              |                                                                                             |                                                     |
| 0x65 | svcGetProcessList                                                                  |                                                                                             |                                                     |
| 0x66 | svcGetThreadList                                                                   |                                                                                             |                                                     |
| 0x67 | svcGetDebugThreadContext                                                           | X0=ThreadContext\*, X1=debughandle, X2=?, W3=?                                              | W0=result                                           |
| 0x68 | svcSetDebugThreadContext                                                           |                                                                                             |                                                     |
| 0x69 | svcQueryDebugProcessMemory                                                         | X0=MemoryInfo\*, X2=debughandle, X3=addr                                                    | W0=result, W1=PageInfo                              |
| 0x6A | svcReadDebugProcessMemory                                                          | X0=buffer\*, X1=debughandle, X2=src\_addr, X3=size                                          | W0=result                                           |
| 0x6B | svcWriteDebugProcessMemory                                                         | X0=debughandle, X1=buffer\*, X2=dst\_addr, X3=size                                          | W0=result                                           |
| 0x6C | svcSetHardwareBreakPoint                                                           |                                                                                             |                                                     |
| 0x6D | svcGetDebugThreadParam                                                             | X2=debughandle, X3=?, W4=DebugThreadParam                                                   | W0=result, X1=out0, W2=out1                         |
| 0x70 | svcCreatePort                                                                      |                                                                                             |                                                     |
| 0x71 | svcManageNamedPort                                                                 | X1=namestr\*, W2=maxsessions(?)                                                             | W0=result, W1=outhandle                             |
| 0x72 | svcConnectToPort                                                                   | W1=inhandle                                                                                 | W0=result, W1=outhandle                             |
| 0x73 | svcSetProcessMemoryPermission                                                      |                                                                                             |                                                     |
| 0x74 | svcMapProcessMemory                                                                | X0=srcaddr, W1=process\_handle, X2=dstaddr, X3=size                                         | W0=result                                           |
| 0x75 | svcUnmapProcessMemory                                                              | W0=process\_handle, X1=dstaddr, X2=srcaddr, X3=size                                         | W0=result                                           |
| 0x76 | svcQueryProcessMemory                                                              |                                                                                             |                                                     |
| 0x77 | svcMapProcessCodeMemory                                                            | W0=process\_handle, X2=dstaddr, X2=srcaddr, X3=size                                         | W0=result                                           |
| 0x78 | svcUnmapProcessCodeMemory                                                          | W0=process\_handle, X1=dstaddr, X2=srcaddr, X3=size                                         | W0=result                                           |
| 0x79 | [\#svcCreateProcess](#svcCreateProcess "wikilink")                                 | X1=procinfo\_ptr, X2=caps\_ptr, W3=cap\_num                                                 | W0=result, W1=process\_handle                       |
| 0x7A | svcStartProcess                                                                    | W0=proc\_handle, W1=main\_thread\_prio, W2=default\_cpuid, W3=main\_thread\_stacksz         | W0=result                                           |
| 0x7B | svcTerminateProcess                                                                |                                                                                             |                                                     |
| 0x7C | svcGetProcessInfo                                                                  |                                                                                             |                                                     |
| 0x7D | svcCreateResourceLimit                                                             |                                                                                             |                                                     |
| 0x7E | svcSetResourceLimitLimitValue                                                      |                                                                                             |                                                     |
| 0x7F | svcCallSecureMonitor                                                               |                                                                                             |                                                     |

## svcSetHeapSize

**Description:** Set the process heap to a given size. It can both
extend and shrink the heap.

Size must be a multiple of 0x2000000.

On success, the heap base-address (which is fixed by kernel, aslr'd) is
written to outaddr.

## svcSetMemoryPermission

**Description:** Change permission of page-aligned memory region.

Bit2 of permission (exec) is not allowed. Setting write-only is not
allowed either (bit1).

This can be used to move back and forth between ---, r-- and rw-.

## svcSetMemoryAttribute

**Description:** Change attribute of page-aligned memory region.

This is used to turn on/off caching for a given memory area. Useful when
talking to devices such as the GPU.

What happens "under the hood" is the "Memory Attribute Indirection
Register" index is changed from 2 to 3 in the MMU
descriptor.

| State0 | State1 | Action                                                          |
| ------ | ------ | --------------------------------------------------------------- |
| 0      | 0      | Clear bit3 in [\#MemoryAttribute](#MemoryAttribute "wikilink"). |
| 8      | 0      | Clear bit3 in [\#MemoryAttribute](#MemoryAttribute "wikilink"). |
| 8      | 8      | Set bit3 in [\#MemoryAttribute](#MemoryAttribute "wikilink").   |

## svcMapMemory

**Description:** Maps a memory range into a different range.

Useful for adding guard pages around stack.

Source range gets reprotected to --- (it can no longer be accessed), and
bit0 is set in [\#MemoryAttribute](#MemoryAttribute "wikilink").

If dstaddr \>= LowerTreshold, the dst-range is enforced to be within the
process' "MapRegion". Code can get the range of this region from
[\#svcGetInfo](#svcGetInfo "wikilink") id0=2,3.

In this case, the mapped memory will have state `0x482907`.

As long as (dstaddr+size) \< LowerThreshold, then you can map anywhere
but the mapped memory will have state `0x5C3C0B` instead.

LowerTreshold is 0x80000000 for 36-bit address spaces, and 0x40000000
for 32-bit ones.

## svcUnmapMemory

**Description:** Unmaps a region that was previously mapped with
[\#svcMapMemory](#svcMapMemory "wikilink").

It's possible to unmap ranges partially, you don't need to unmap the
entire range "in one go".

The srcaddr/dstaddr must match what was given when the pages were
originally mapped.

## svcQueryMemory

**Description:** Query information about an address. Will always fetch
the lowest page-aligned mapping that contains the provided address.

Outputs a [\#MemoryInfo](#MemoryInfo "wikilink") struct.

## svcExitProcess

**Description:** Exits the current process.

## svcCreateThread

**Description:** Create a thread in the current process.

Processor\_id must be 0,1,2,3 or -2, where -2 uses the default cpuid for
process.

## svcStartThread

**Description:** Starts the thread for the provided handle.

## svcExitThread

**Description:** Exits the current thread.

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
| Process     | 2          | 0                     | MapRegionBaseAddress                                                                                        |
| Process     | 3          | 0                     | MapRegionSize                                                                                               |
| Process     | 4          | 0                     | HeapRegionBaseAddress                                                                                       |
| Process     | 5          | 0                     | HeapRegionSize                                                                                              |
| Process     | 6          | 0                     | TotalMemoryUsage                                                                                            |
| Process     | 7          | 0                     | TotalHeapUsage                                                                                              |
| Zero        | 8          | 0                     | IsCurrentProcessBeingDebugged                                                                               |
| Zero        | 9          | 0                     | Returns ResourceLimit handle for current process. Used by [PM](Process%20Manager%20services.md "wikilink"). |
| Zero        | 10         | \-1, {current coreid} | Unknown. Output data changes each time this SVC is used. Global and core-specific tick-count?               |
| Zero        | 11         | 0-3                   | RandomEntropy from current process. TRNG. Used to seed usermode PRNGs.                                      |
| Process     | 12         | 0                     | \[ [2.0.0](2.0.0.md "wikilink") +\] AddressSpaceStart.                                                      |
| Process     | 13         | 0                     | \[ [2.0.0](2.0.0.md "wikilink") +\] AddressSpaceSize.                                                       |
| Process     | 14         | 0                     | \[ [2.0.0](2.0.0.md "wikilink") +\] MapRegionBased. Randomized.                                             |
| Process     | 15         | 0                     | \[ [2.0.0](2.0.0.md "wikilink") +\] MapRegionSize.                                                          |
| Process     | 18         | 0                     | \[ [3.0.0](3.0.0.md "wikilink") +\] Title-id.                                                               |
| Thread      | 0xF0000002 | 0                     | Performance counter related.                                                                                |

## svcDumpInfo

Does nothing, just returns with registers set to all-zero.

## svcReadWriteRegister

Read/write Tegra hardware registers with a hardcoded whitelist. Input
address is physical-address.

rw\_mask is 0 for reading and -1 for writing.

The whitelist is same for writing as for reading.

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

## svcCreateProcess

Takes a [\#CreateProcessInfo](#CreateProcessInfo "wikilink") as input.

## svcAttachDeviceAddressSpace

**Description:** Attach an address space to a
[device](#DeviceName "wikilink").

## svcDetachDeviceAddressSpace

**Description:** Detach an address space from a
[device](#DeviceName "wikilink").

## Debugging

\[2.0.0+\] Certain debug SVCs require that
[IsDebugMode](SPL%20services#GetConfig.md##GetConfig "wikilink") is
non-zero. Error 0x4201 is returned otherwise. svcWriteDebugProcessMemory
requires this but not svcReadDebugProcessMemory.

# Structures

## DeviceName

| Value | Name        |
| ----- | ----------- |
| 0     | AFI         |
| 1     | AVPC        |
| 2     | DC          |
| 3     | DCB         |
| 4     | HC          |
| 5     | HDA         |
| 6     | ISP2        |
| 7     | MSENC NVENC |
| 8     | NV          |
| 9     | NV2         |
| 10    | PPCS        |
| 11    | SATA        |
| 12    | VI          |
| 13    | VIC         |
| 14    | XUSB\_HOST  |
| 15    | XUSB\_DEV   |
| 16    | TSEC        |
| 17    | PPCS1       |
| 18    | DC1         |
| 19    | SDMMC1A     |
| 20    | SDMMC2A     |
| 21    | SDMMC3A     |
| 22    | SDMMC4A     |
| 23    | ISP2B       |
| 24    | GPU         |
| 25    | GPUB        |
| 26    | PPCS2       |
| 27    | NVDEC       |
| 28    | APE         |
| 29    | SE          |
| 30    | NVJPG       |
| 31    | HC1         |
| 32    | SE1         |
| 33    | AXIAP       |
| 34    | ETR         |
| 35    | TSECB       |
| 36    | TSEC1       |
| 37    | TSECB1      |
| 38    | NVDEC1      |

## CreateProcessInfo

| Offset | Length | Bits   | Description                                                                                                                          |
| ------ | ------ | ------ | ------------------------------------------------------------------------------------------------------------------------------------ |
| 0      | 8      |        |                                                                                                                                      |
| 8      | 2      |        |                                                                                                                                      |
| 0xA    | 2      |        |                                                                                                                                      |
| 0xC    | 4      |        |                                                                                                                                      |
| 0x10   | 8      |        | TitleId                                                                                                                              |
| 0x18   | 8      |        | CodeAddr                                                                                                                             |
| 0x20   | 4      |        | CodeNumPages                                                                                                                         |
| 0x24   | 4      |        | MmuFlags                                                                                                                             |
|        |        | Bit0   | Is64bit                                                                                                                              |
|        |        | Bit3-1 | AddressSpaceType (0=32-bit with map and heap regions, 1=36-bit with map and heap regions, 2=32-bit with heap region only), 3=Invalid |
|        |        | Bit4   |                                                                                                                                      |
|        |        | Bit5   | EnableAslr                                                                                                                           |
|        |        | Bit6   | IsSystem                                                                                                                             |
| 0x28   | 4      |        | ResourceLimitHandle                                                                                                                  |
| 0x2C   | 4      |        |                                                                                                                                      |

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

| Value        | Type                                                           | Meaning                                                                                                             |
| ------------ | -------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| `0x00000000` | Unmapped                                                       |                                                                                                                     |
| `0x00002001` | IO                                                             | Mapped by kernel capability parsing in [\#svcCreateProcess](#svcCreateProcess "wikilink").                          |
| `0x00042002` | Normal                                                         | Mapped by kernel capability parsing in [\#svcCreateProcess](#svcCreateProcess "wikilink").                          |
| `0x00DC7E03` | Code static                                                    | Mapped during [\#svcCreateProcess](#svcCreateProcess "wikilink").                                                   |
| `0x01FEBD04` | Code                                                           | Transition from 0xDC7E03 performed by [\#svcSetProcessMemoryPermission](#svcSetProcessMemoryPermission "wikilink"). |
| `0x017EBD05` | Heap                                                           | Mapped using [\#svcSetHeapSize](#svcSetHeapSize "wikilink").                                                        |
| `0x00402006` | Shared memory block                                            | Mapped using [\#svcMapSharedMemory](#svcMapSharedMemory "wikilink").                                                |
| `0x00482907` | Weird mapped memory                                            | Mapped using [\#svcMapMemory](#svcMapMemory "wikilink").                                                            |
| `0x00DD7E08` | Module code static                                             | Mapped using [\#svcMapProcessCodeMemory](#svcMapProcessCodeMemory "wikilink").                                      |
| `0x01FFBD09` | Module code mutable                                            | Transition from 0xDD7E08 performed by [\#svcSetProcessMemoryPermission](#svcSetProcessMemoryPermission "wikilink"). |
| `0x005C3C0B` | Mapped memory                                                  | Mapped using [\#svcMapMemory](#svcMapMemory "wikilink").                                                            |
| `0x0040200C` | [Thread local storage](Thread%20Local%20Storage.md "wikilink") | Mapped during [\#svcCreateThread](#svcCreateThread "wikilink").                                                     |
| `0x015C3C0D` | Isolated transfer memory                                       | Mapped using [\#svcMapTransferMemory](#svcMapTransferMemory "wikilink") when the owning process has perm=0.         |
| `0x005C380E` | Transfer memory                                                | Mapped using [\#svcMapTransferMemory](#svcMapTransferMemory "wikilink") when the owning process has perm\!=0.       |
| `0x0040380F` | Process memory                                                 | Mapped using [\#svcMapProcessMemory](#svcMapProcessMemory "wikilink").                                              |
| `0x00000010` | Reserved                                                       |                                                                                                                     |

# Exception Handling

There appears to be userland code for handling exceptions, however this
doesn't seem to be executed on retail.

On usermode exception, it jumps to main code binary entrypoint
(main\_binary\_address+0) with X0=exception\_info\_ptr and
X1=exception\_info2\_ptr. On boot, X0 is set to 0 triggering normal crt0
setup.

# System calls

| Id   | Name                                                         | In                                                                | Out                           |
| ---- | ------------------------------------------------------------ | ----------------------------------------------------------------- | ----------------------------- |
| 0x1  | svcSetupHeap                                                 | X1=size                                                           | W0=result, X1=outaddr         |
| 0x2  | [\#svcProtectMemory](#svcProtectMemory "wikilink")           | X0=addr, X1=size, W2=prot                                         | W0=result                     |
| 0x3  | [\#svcSetMemoryState](#svcSetMemoryState "wikilink")         | X0=addr, X1=size, W2=state0, W3=state1                            | W0=result                     |
| 0x4  | [\#svcMirrorStack](#svcMirrorStack "wikilink")               | X0=dstaddr, X1=srcaddr, X2=size                                   | W0=result                     |
| 0x5  | svcUnmirrorStack                                             | X0=dstaddr, X1=srcaddr, X2=size                                   | W0=result                     |
| 0x6  | svcQueryMemory                                               | X0=meminfo\_ptr, X2=addr                                          | W0=result, W1=pageinfo        |
| 0x7  | svcExitProcess                                               | None                                                              |                               |
| 0x8  | [\#svcCreateThread](#svcCreateThread "wikilink")             | X1=entry, X2=arg, X3=stacktop, W4=prio, W5=processor\_id          |                               |
| 0x9  | svcStartThread                                               | W0=thread\_handle                                                 |                               |
| 0xA  | svcExitThread                                                | None                                                              |                               |
| 0xB  | [\#svcSleepThread](#svcSleepThread "wikilink")               | X0=nano                                                           |                               |
| 0xC  | svcGetThreadPriority                                         | W1=thread\_handle                                                 | W0=result, W1=prio            |
| 0xD  | svcSetThreadPriority                                         | W0=thread\_handle, W1=prio                                        | W0=result                     |
| 0xE  | svcGetThreadAffinityMask                                     | W2=thread\_handle                                                 | W0=result, W1=out, X2=out     |
| 0xF  | svcSetThreadAffinityMask                                     | W0=thread\_handle, W1=in, X2=in2                                  | W0=result                     |
| 0x10 | svcGetCurrentProcessorNumber                                 | None                                                              | W0/X0=cpuid                   |
| 0x11 | svcGetMemoryBlockSomethingA?                                 | W0=handle                                                         | ?                             |
| 0x12 | svcGetMemoryBlockSomethingB?                                 | W0=handle                                                         | ?                             |
| 0x13 | svcMapMemoryBlock                                            | W0=memblk\_handle, X1=addr, X2=size, W3=perm                      | W0=result                     |
| 0x14 | svcUnmapMemoryBlock                                          | W0=memblk\_handle, X1=addr, X2=size                               | W0=result                     |
| 0x15 | [\#svcCreateMemoryMirror](#svcCreateMemoryMirror "wikilink") | X1=addr, X2=size, W3=perm                                         | W0=result, W1=handle          |
| 0x16 | svcCloseHandle                                               | W0=handle                                                         | W0=result                     |
| 0x17 | svcClearEvent                                                | W0=handle                                                         | W0=result                     |
| 0x18 | [\#svcWaitEvents](#svcWaitEvents "wikilink")                 | X1=handles\_ptr, X2=num\_handles. X3=timeout                      | W0=result, W1=handle\_idx     |
| 0x19 | svcSignalEvent                                               | W0=handle                                                         | W0=result                     |
| 0x1A | svcLockMutex                                                 | W0=cur\_thread\_handle, X1=ptr, W2=req\_thread\_handle            |                               |
| 0x1B | svcUnlockMutex                                               | X0=ptr                                                            |                               |
| 0x1C | svcCondWait                                                  | X0=ptr0, X1=ptr, W2=thread\_handle, X3=timeout                    | W0=result                     |
| 0x1D | svcCondBroadcast                                             | X0=ptr, W1=value                                                  | W0=result                     |
| .... | ?                                                            | ?                                                                 | ?                             |
| 0x1F | svcConnectToPort                                             | X1=port\_name\_str                                                | W0=result, W1=handle          |
| .... | ?                                                            | ?                                                                 | ?                             |
| 0x21 | svcSendSyncRequest                                           | X0=handle                                                         | W0=result                     |
| 0x22 | svcSendSyncRequestByBuf                                      | X0=cmdbufptr, X1=size, X2=handle                                  | W0=result                     |
| .... | ?                                                            | ?                                                                 | ?                             |
| 0x25 | svcGetThreadId                                               | W0=thread\_handle                                                 | W0=result, X1=out             |
| 0x26 | svcBreak                                                     | X0,X1,X2=info                                                     | ?                             |
| 0x27 | svcOutputDebugString                                         | X0=str, X1=size                                                   |                               |
| 0x28 | svcReturnFromException                                       | X0=result                                                         |                               |
| 0x29 | [\#svcGetInfo](#svcGetInfo "wikilink")                       | X1=info\_id, X2=handle, X3=info\_sub\_id                          | W0=result, X1=out             |
| .... | ?                                                            | ?                                                                 | ?                             |
| 0x40 | ???                                                          | W2=?, X3=?                                                        | W0=result, W1=?, W2=?         |
| 0x41 | svcAcceptSession                                             | W1=port\_handle                                                   | W0=result, W1=session\_handle |
| .... | ?                                                            | ?                                                                 | ?                             |
| 0x43 | svcReplyAndReceive                                           | X1=ptr\_handles, W2=num\_handles, X3=?, X4=timeout                | W0=result, W1=handle\_idx     |
| 0x44 | svcReplyAndReceiveByBuf                                      | X1=buf, X2=sz, X3=ptr\_handles, W4=num\_handles, X5=?, X6=timeout | W0=result, W1=handle\_idx     |
| 0x45 | svcCreateEvent?                                              | None                                                              | W0=result, W1=?, W2=?         |
| .... | ?                                                            | ?                                                                 | ?                             |
| 0x50 | svcCreateMemoryBlock                                         | W1=size?, W2=perm0, W3=perm1                                      | W0=result, W1=handle          |
| 0x51 | [\#svcMapMemoryMirror](#svcMapMemoryMirror "wikilink")       | X0=mirror\_handle, X1=addr, X2=size, W3=perm                      | W0=result                     |
| 0x52 | [\#svcUnmapMemoryMirror](#svcUnmapMemoryMirror "wikilink")   | W0=mirror\_handle, X1=addr, X2=size                               | W0=result                     |

## svcProtectMemory

Bit2 of permission (exec) is not allowed.

Setting write-only is not allowed either
(bit1).

## svcSetMemoryState

| State0 | State1 | Action                                                   |
| ------ | ------ | -------------------------------------------------------- |
| 0      | 0      | Clear bit35 in [\#MemoryState](#MemoryState "wikilink"). |
| 8      | 0      | Clear bit35 in [\#MemoryState](#MemoryState "wikilink"). |
| 8      | 8      | Set bit35 in [\#MemoryState](#MemoryState "wikilink").   |

This might used for switching between cached and non-cached mappings.

## svcMirrorStack

Memory is only allowed to be mapped into a special region.

Code can get the range of this region from
[\#svcGetInfo](#svcGetInfo "wikilink").

The source region gets reprotected to ---, and sets bit32 is set in
[\#MemoryState](#MemoryState "wikilink").

## svcCreateThread

Processor\_id must be 0,1,2,3 or -2.

## svcSleepThread

Setting nano=0 means "yield thread".

## svcCreateMemoryMirror

This one reprotects the src block with perms you give it. It also sets
bit32 into [\#MemoryState](#MemoryState "wikilink").

Executable bit perm not allowed.

Closing the returned handle automatically causes the bit32 in
[\#MemoryState](#MemoryState "wikilink") to clear.

## svcWaitSynchronizationN

Works with num\_handles \<= 0x40, error on num\_handles == 0.

Does not accept 0xFFFF8001 or 0xFFFF8000 as
handles.

## svcGetInfo

| Handle type | Id0 | Id1    | Description                                                    |
| ----------- | --- | ------ | -------------------------------------------------------------- |
| Process     | 0   | 0      | Code available mask. Always 0xF meaning all 4 cores available. |
| Process     | 1   | 0      | Always 0xfffffffff0000000.                                     |
| Process     | 2   | 0      | Randomized unknown base-address.                               |
| Process     | 3   | 0      | Always 0x1000000000.                                           |
| Process     | 4   | 0      | Randomized heap base-address.                                  |
| Process     | 5   | 0      | Always 0x180000000.                                            |
| Process     | 6   | 0      | Total memory usage?                                            |
| Process     | 7   | 0      | Process heap size.                                             |
| Zero        | 8   | 0      | Always 0.                                                      |
| Zero        | 9   | 0      | This creates and returns an unknown handle.                    |
| Zero        | 10  | \-1, 0 | ?                                                              |
| Zero        | 11  | 0-3    | Returns random from TRNG. Used to seed usermode PRNGs.         |
| Process     | 12  | 0      | Always 0x8000000.                                              |
| Process     | 13  | 0      | Always 0x7ff8000000.                                           |
| Process     | 14  | 0      | Start of stack mirror region.                                  |
| Process     | 15  | 0      | Size of stack mirror region.                                   |

## svcMapMemoryMirror

The newly mapped pages will have
[\#MemoryState](#MemoryState "wikilink") type 0xE.

You must pass same size and permissions as given in
svcCreateMemoryMirror, otherwise error.

## svcUnmapMemoryMirror

Size must match size given in map syscall, otherwise there's an
invalid-size error.

## MemoryState

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

Bit32: is\_mirrored

Bit35: is\_uncached?

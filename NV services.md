The Switch makes use of a customized NVIDIA driver.

# nvdrv:a

Main NVIDIA driver service.

| Cmd | Name                                   |
| --- | -------------------------------------- |
| 0   | [\#Open](#Open "wikilink")             |
| 1   | [\#Ioctl](#Ioctl "wikilink")           |
| 2   | [\#Close](#Close "wikilink")           |
| 3   | [\#Initialize](#Initialize "wikilink") |
| 4   | QueryEvent                             |
| 5   | MapSharedMem                           |
| 6   | ?                                      |
| 7   | ?                                      |
| 8   | BindDisplayService                     |
| 9   | ?                                      |

## Open

| Word | Value                          |
| ---- | ------------------------------ |
| 0    | 0x00100004                     |
| 1    | 0x00000008                     |
| 2-4  | Type 5 descriptor: Device path |
| 0-1  | "SFCI"                         |
| 2-3  | Cmd id (0)                     |

## Ioctl

| Word | Value                               |
| ---- | ----------------------------------- |
| 0    | 0x11100004                          |
| 1    | 0x00000C0B                          |
| ?    | Type 0x21 descriptor: Input buffer  |
| ?    | Type 0x22 descriptor: Output buffer |
| 0-1  | "SFCI"                              |
| 2-3  | Cmd id (1)                          |
| 4    | Device fd                           |
| 5    | Ioctl Cmd                           |

## Close

| Word | Value      |
| ---- | ---------- |
| 0    | 0x00000004 |
| 1    | 0x00000009 |
| 0-1  | "SFCI"     |
| 2-3  | Cmd id (2) |
| 4    | Device fd  |

## Initialize

| Word | Value                                   |
| ---- | --------------------------------------- |
| 0    | 0x00000004                              |
| 1    | 0x80000009                              |
| ?    | Handle descriptor: Current process      |
| ?    | Handle descriptor: Shared memory mirror |
| 0-1  | "SFCI"                                  |
| 2-3  | Cmd id (3)                              |
| 4    | Shared memory size                      |

Webkit applet creates the shared memory with perm = 0 and size 0x300000.

## Ioctls

The ioctl number is generated with the following primitive (see Linux
kernel):

`#define _IOC(inout, group, num, len) \`  
`   (inout | ((len & IOCPARM_MASK) << 16) | ((group) << 8) | (num))`

The following table contains known
ioctls.

| Device               | Value      | Description                                   | Notes                                          |
| -------------------- | ---------- | --------------------------------------------- | ---------------------------------------------- |
| /dev/nvhost-\*       | 0xC0??0001 | NVHOST\_IOCTL\_CHANNEL\_SUBMIT                | ?? == size is variable                         |
| /dev/nvhost-\*       | 0xC0080002 | NVHOST\_IOCTL\_CHANNEL\_GET\_SYNCPOINT        |                                                |
| /dev/nvhost-\*       | 0xC0080003 | NVHOST\_IOCTL\_CHANNEL\_GET\_WAITBASE         |                                                |
| /dev/nvhost-\*       | 0xC0080004 | NVHOST\_IOCTL\_CHANNEL\_SET\_TIMEOUT\_EX      |                                                |
| /dev/nvhost-\*       | 0x40040007 |                                               |                                                |
| /dev/nvhost-\*       | 0xC0??0009 | NVHOST\_IOCTL\_CHANNEL\_MAP\_BUFFER           | ?? == size is variable                         |
| /dev/nvhost-\*       | 0xC0??000A | NVHOST\_IOCTL\_CHANNEL\_UNMAP\_BUFFER         | ?? == size is variable                         |
| /dev/nvhost-\*       | 0x00000013 |                                               |                                                |
| /dev/nvhost-ctrl     | 0xC0080014 | NVHOST\_IOCTL\_CTRL\_SYNCPT\_READ             |                                                |
| /dev/nvhost-ctrl     | 0x40040015 | NVHOST\_IOCTL\_CTRL\_SYNCPT\_INCR             |                                                |
| /dev/nvhost-ctrl     | 0xC00C0016 | NVHOST\_IOCTL\_CTRL\_SYNCPT\_WAIT             |                                                |
| /dev/nvhost-ctrl     | 0x40080017 | NVHOST\_IOCTL\_CTRL\_MODULE\_MUTEX            |                                                |
| /dev/nvhost-ctrl     | 0xC0180018 | NVHOST32\_IOCTL\_CTRL\_MODULE\_REGRDWR        |                                                |
| /dev/nvhost-ctrl     | 0xC0100019 | NVHOST\_IOCTL\_CTRL\_SYNCPT\_WAITEX           |                                                |
| /dev/nvhost-ctrl     | 0xC008001A | NVHOST\_IOCTL\_CTRL\_SYNCPT\_READ\_MAX        |                                                |
| /dev/nvhost-ctrl     | 0xC004001C |                                               |                                                |
| /dev/nvhost-ctrl     | 0xC010001D |                                               | NvRmSyncWaitEvent (wait on event?)             |
| /dev/nvhost-ctrl     | 0xC010001E |                                               | NvRmSyncWaitEvent (wait on event?)             |
| /dev/nvhost-ctrl     | 0xC004001F |                                               | NvRmSyncWaitEvent (signal event?)              |
| /dev/nvhost-ctrl     | 0xC0040020 |                                               | NvRmSyncWaitEvent (signal event?)              |
| /dev/nvhost-ctrl     | 0x40080021 | cancel\_wait\_event                           | Cancels all events                             |
| /dev/nvmap           | 0xC0080101 | NVMAP\_IOC\_CREATE                            |                                                |
| /dev/nvmap           | 0x00000102 |                                               | Returns NVERROR 0x02 (not supported)           |
| /dev/nvmap           | 0xC0080103 | NVMAP\_IOC\_FROM\_ID                          |                                                |
| /dev/nvmap           | 0xC0200104 | NVMAP\_IOC\_ALLOC                             |                                                |
| /dev/nvmap           | 0xC0180105 | NVMAP\_IOC\_FREE                              |                                                |
| /dev/nvmap           | 0xC0280106 | NVMAP\_IOC\_MMAP?                             | Returns NVERROR 0x02 (not supported)           |
| /dev/nvmap           | 0xC0280107 | NVMAP\_IOC\_WRITE?                            | Returns NVERROR 0x02 (not supported)           |
| /dev/nvmap           | 0xC0280108 | NVMAP\_IOC\_READ?                             | Returns NVERROR 0x02 (not supported)           |
| /dev/nvmap           | 0xC00C0109 | NVMAP\_IOC\_PARAM                             |                                                |
| /dev/nvmap           | 0xC010010A | NVMAP\_IOC\_PIN\_MULT?                        | Returns NVERROR 0x02 (not supported)           |
| /dev/nvmap           | 0xC010010B | NVMAP\_IOC\_UNPIN\_MULT?                      | Returns NVERROR 0x02 (not supported)           |
| /dev/nvmap           | 0xC008010C | NVMAP\_IOC\_CACHE?                            | Returns NVERROR 0x02 (not supported)           |
| /dev/nvmap           | 0xC004010D |                                               | Returns NVERROR 0x02 (not supported)           |
| /dev/nvmap           | 0xC008010E | NVMAP\_IOC\_GET\_ID                           |                                                |
| /dev/nvmap           | 0xC004010F |                                               | Returns NVERROR 0x02 (not supported)           |
| /dev/nvmap           | 0x40040110 |                                               | Returns NVERROR 0x02 (not supported)           |
| /dev/nvmap           | 0x00000111 |                                               | Returns NVERROR 0x02 (not supported)           |
| /dev/nvhost-as-gpu   | 0x40044101 | NVGPU\_AS\_IOCTL\_BIND\_CHANNEL               |                                                |
| /dev/nvhost-as-gpu   | 0xC0184102 | NVGPU\_AS\_IOCTL\_ALLOC\_SPACE                |                                                |
| /dev/nvhost-as-gpu   | 0xC0104103 | NVGPU\_AS\_IOCTL\_FREE\_SPACE                 |                                                |
| /dev/nvhost-as-gpu   | 0xC0184104 | NVGPU\_AS\_IOCTL\_MAP\_BUFFER                 |                                                |
| /dev/nvhost-as-gpu   | 0xC0084105 | NVGPU\_AS\_IOCTL\_UNMAP\_BUFFER               |                                                |
| /dev/nvhost-as-gpu   | 0xC0284106 | NVGPU\_AS\_IOCTL\_MAP\_BUFFER\_EX             |                                                |
| /dev/nvhost-as-gpu   | 0x40104107 | init\_as\_gpu                                 | Initializes the as-gpu node                    |
| /dev/nvhost-as-gpu   | 0xC0404108 | NVGPU\_AS\_IOCTL\_GET\_VA\_REGIONS?           |                                                |
| /dev/nvhost-as-gpu   | 0x40284109 | init\_as\_gpu\_ex                             | Initializes the as-gpu node (with more params) |
| /dev/nvhost-as-gpu   | 0xC0144114 |                                               |                                                |
| /dev/nvhost-dbg-gpu  | 0x40084401 | NVGPU\_DBG\_GPU\_IOCTL\_BIND\_CHANNEL         |                                                |
| /dev/nvhost-dbg-gpu  | 0xC0??4402 | NVGPU\_DBG\_GPU\_IOCTL\_REG\_OPS              | ?? == size is unknown                          |
| /dev/nvhost-dbg-gpu  | 0x40084403 | NVGPU\_DBG\_GPU\_IOCTL\_EVENTS\_CTRL          |                                                |
| /dev/nvhost-dbg-gpu  | 0x40044404 | NVGPU\_DBG\_GPU\_IOCTL\_POWERGATE             |                                                |
| /dev/nvhost-dbg-gpu  | 0x40044405 | NVGPU\_DBG\_GPU\_IOCTL\_SMPC\_CTXSW\_MODE     |                                                |
| /dev/nvhost-dbg-gpu  | 0xC0184407 | NVGPU\_DBG\_GPU\_IOCTL\_PERFBUF\_MAP          |                                                |
| /dev/nvhost-dbg-gpu  | 0x40084408 | NVGPU\_DBG\_GPU\_IOCTL\_PERFBUF\_UNMAP        |                                                |
| /dev/nvhost-dbg-gpu  | 0x40084409 | NVGPU\_DBG\_GPU\_IOCTL\_PC\_SAMPLING          |                                                |
| /dev/nvhost-ctrl-gpu | 0x80044701 | NVGPU\_GPU\_IOCTL\_ZCULL\_GET\_CTX\_SIZE      |                                                |
| /dev/nvhost-ctrl-gpu | 0x80284702 | NVGPU\_GPU\_IOCTL\_ZCULL\_GET\_INFO           |                                                |
| /dev/nvhost-ctrl-gpu | 0x402C4703 | NVGPU\_GPU\_IOCTL\_ZBC\_SET\_TABLE            |                                                |
| /dev/nvhost-ctrl-gpu | 0xC0344704 | NVGPU\_GPU\_IOCTL\_ZBC\_QUERY\_TABLE          |                                                |
| /dev/nvhost-ctrl-gpu | 0xC0B04705 | NVGPU\_GPU\_IOCTL\_GET\_CHARACTERISTICS       |                                                |
| /dev/nvhost-ctrl-gpu | 0xC0184706 | NVGPU\_GPU\_IOCTL\_GET\_TPC\_MASKS            |                                                |
| /dev/nvhost-ctrl-gpu | 0x40084707 | NVGPU\_GPU\_IOCTL\_OPEN\_CHANNEL              |                                                |
| /dev/nvhost-ctrl-gpu | 0x4008470E |                                               |                                                |
| /dev/nvhost-ctrl-gpu | 0x4010470F |                                               |                                                |
| /dev/nvhost-ctrl-gpu | 0xC0084710 |                                               |                                                |
| /dev/nvhost-ctrl-gpu | 0x80084711 |                                               |                                                |
| /dev/nvhost-ctrl-gpu | 0x80084712 |                                               |                                                |
| /dev/nvhost-ctrl-gpu | 0xC0044713 |                                               |                                                |
| /dev/nvhost-ctrl-gpu | 0x80084714 |                                               |                                                |
| /dev/nvhost-ctrl-gpu | 0x80044715 |                                               |                                                |
| /dev/nvhost-ctrl-gpu | 0x8018471A |                                               |                                                |
| /dev/nvhost-ctrl-gpu | 0xC008471B |                                               |                                                |
| /dev/nvhost-ctrl-gpu | 0xC010471C |                                               |                                                |
| /dev/nvhost-\*       | 0x40044801 | NVGPU\_IOCTL\_CHANNEL\_SET\_NVMAP\_FD         |                                                |
| /dev/nvhost-\*       | 0x40044803 | NVGPU\_IOCTL\_CHANNEL\_SET\_PRIORITY          |                                                |
| /dev/nvhost-\*       | 0x40084805 | NVGPU\_IOCTL\_CHANNEL\_ALLOC\_GPFIFO          |                                                |
| /dev/nvhost-\*       | 0xC0044807 | NVGPU\_IOCTL\_CHANNEL\_CYCLE\_STATS           |                                                |
| /dev/nvhost-\*       | 0xC0184808 | NVGPU\_IOCTL\_CHANNEL\_SUBMIT\_GPFIFO         |                                                |
| /dev/nvhost-\*       | 0xC0104809 | NVGPU\_IOCTL\_CHANNEL\_ALLOC\_OBJ\_CTX        |                                                |
| /dev/nvhost-\*       | 0x4008480A | NVGPU\_IOCTL\_CHANNEL\_FREE\_OBJ\_CTX         |                                                |
| /dev/nvhost-\*       | 0xC010480B | NVGPU\_IOCTL\_CHANNEL\_ZCULL\_BIND            |                                                |
| /dev/nvhost-\*       | 0xC018480C | NVGPU\_IOCTL\_CHANNEL\_SET\_ERROR\_NOTIFIER   |                                                |
| /dev/nvhost-\*       | 0x4004480D | NVGPU\_IOCTL\_CHANNEL\_OPEN                   |                                                |
| /dev/nvhost-\*       | 0x0000480E | NVGPU\_IOCTL\_CHANNEL\_ENABLE                 |                                                |
| /dev/nvhost-\*       | 0x0000480F | NVGPU\_IOCTL\_CHANNEL\_DISABLE                |                                                |
| /dev/nvhost-\*       | 0x00004810 | NVGPU\_IOCTL\_CHANNEL\_PREEMPT                |                                                |
| /dev/nvhost-\*       | 0x00004811 | NVGPU\_IOCTL\_CHANNEL\_FORCE\_RESET           |                                                |
| /dev/nvhost-\*       | 0x40084812 | NVGPU\_IOCTL\_CHANNEL\_EVENTS\_CTRL           |                                                |
| /dev/nvhost-\*       | 0xC0104813 | NVGPU\_IOCTL\_CHANNEL\_CYCLE\_STATS\_SNAPSHOT |                                                |
| /dev/nvhost-\*       | 0x40084714 | set\_user\_address                            | Group ID is wrong (0x47 should be 0x48)        |
| /dev/nvhost-\*       | 0x80084715 | get\_user\_address                            | Group ID is wrong (0x47 should be 0x48)        |
| /dev/nvhost-\*       | 0x80804816 |                                               |                                                |
| /dev/nvhost-\*       | 0xC0104817 |                                               |                                                |
| /dev/nvhost-\*       | 0x40204818 | NVGPU\_IOCTL\_CHANNEL\_ALLOC\_GPFIFO\_EX      |                                                |
| /dev/nvhost-\*       | 0xC0484819 |                                               |                                                |
| /dev/nvhost-\*       | 0xC020481A | NVGPU\_IOCTL\_CHANNEL\_ALLOC\_GPFIFO\_EX2     |                                                |

# nvmemp

NVIDIA memory profiler (this service is not available on retail units).

# mm:u

NVIDIA multimedia (NvMM) platform service.

| Cmd | Name                   |
| --- | ---------------------- |
| 0   | ?                      |
| 1   | ?                      |
| 2   | ?                      |
| 3   | ?                      |
| 4   | module\_init\_clk      |
| 5   | module\_deinit\_clk    |
| 6   | module\_set\_clk\_rate |
| 7   | module\_get\_clk\_rate |

# Errors

Most nvidia driver commands return an error code apart from the normal
return code.

| Cmd    | Name                    |
| ------ | ----------------------- |
| 0      | Success                 |
| 1      | NotImplemented          |
| 2      | NotSupported            |
| 3      | NotInitialized          |
| 4      | BadParameter            |
| 5      | Timeout                 |
| 6      | InsufficientMemory      |
| 7      | ReadOnlyAttribute       |
| 8      | InvalidState            |
| 9      | InvalidAddress          |
| 0xA    | InvalidSize             |
| 0xB    | BadValue                |
| 0xD    | AlreadyAllocated        |
| 0xE    | Busy                    |
| 0xF    | ResourceError           |
| 0x10   | CountMismatch           |
| 0x1000 | Shared memory too small |

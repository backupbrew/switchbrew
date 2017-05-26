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

# Ioctls

The ioctl number is generated with the following primitive (see Linux
kernel):

`#define _IOC(inout, group, num, len) \`  
`   (inout | ((len & IOCPARM_MASK) << 16) | ((group) << 8) | (num))`

The following table contains known
ioctls.

## /dev/nvhost-ctrl

| Value      | Direction | Size | Description                            | Notes                              |
| ---------- | --------- | ---- | -------------------------------------- | ---------------------------------- |
| 0xC0080014 | Inout     | 8    | NVHOST\_IOCTL\_CTRL\_SYNCPT\_READ      |                                    |
| 0x40040015 | In        | 4    | NVHOST\_IOCTL\_CTRL\_SYNCPT\_INCR      |                                    |
| 0xC00C0016 | Inout     | 12   | NVHOST\_IOCTL\_CTRL\_SYNCPT\_WAIT      |                                    |
| 0x40080017 | In        | 8    | NVHOST\_IOCTL\_CTRL\_MODULE\_MUTEX     |                                    |
| 0xC0180018 | Inout     | 24   | NVHOST32\_IOCTL\_CTRL\_MODULE\_REGRDWR |                                    |
| 0xC0100019 | Inout     | 16   | NVHOST\_IOCTL\_CTRL\_SYNCPT\_WAITEX    |                                    |
| 0xC008001A | Inout     | 8    | NVHOST\_IOCTL\_CTRL\_SYNCPT\_READ\_MAX |                                    |
| 0xC004001C | Inout     | 4    |                                        |                                    |
| 0xC010001D | Inout     | 16   |                                        | NvRmSyncWaitEvent (wait on event?) |
| 0xC010001E | Inout     | 16   |                                        | NvRmSyncWaitEvent (wait on event?) |
| 0xC004001F | Inout     | 4    |                                        | NvRmSyncWaitEvent (signal event?)  |
| 0xC0040020 | Inout     | 4    |                                        | NvRmSyncWaitEvent (signal event?)  |
| 0x40080021 | In        | 8    | cancel\_wait\_event                    | Cancels all events                 |

## /dev/nvhost-as-gpu

Each fd opened to this device creates an address space. An address space
is then later bound with a
channel.

| Device             | Direction | Size | Value      | Description                                                             | Notes |
| ------------------ | --------- | ---- | ---------- | ----------------------------------------------------------------------- | ----- |
| /dev/nvhost-as-gpu | In        | 4    | 0x40044101 | NVGPU\_AS\_IOCTL\_BIND\_CHANNEL                                         |       |
| /dev/nvhost-as-gpu | Inout     | 24   | 0xC0184102 | NVGPU\_AS\_IOCTL\_ALLOC\_SPACE                                          |       |
| /dev/nvhost-as-gpu | Inout     | 16   | 0xC0104103 | NVGPU\_AS\_IOCTL\_FREE\_SPACE                                           |       |
| /dev/nvhost-as-gpu | Inout     | 24   | 0xC0184104 | NVGPU\_AS\_IOCTL\_MAP\_BUFFER                                           |       |
| /dev/nvhost-as-gpu | Inout     | 8    | 0xC0084105 | NVGPU\_AS\_IOCTL\_UNMAP\_BUFFER                                         |       |
| /dev/nvhost-as-gpu | Inout     | 40   | 0xC0284106 | NVGPU\_AS\_IOCTL\_MAP\_BUFFER\_EX                                       |       |
| /dev/nvhost-as-gpu | In        | 16   | 0x40104107 | [\#NVGPU\_AS\_IOCTL\_INITIALIZE](#NVGPU_AS_IOCTL_INITIALIZE "wikilink") |       |
| /dev/nvhost-as-gpu | Inout     | 64   | 0xC0404108 | NVGPU\_AS\_IOCTL\_GET\_VA\_REGIONS?                                     |       |
| /dev/nvhost-as-gpu | In        | 40   | 0x40284109 | NVGPU\_AS\_IOCTL\_INITIALIZE\_EX                                        |       |
| /dev/nvhost-as-gpu | Inout     | 20   | 0xC0144114 |                                                                         |       |

### NVGPU\_AS\_IOCTL\_INITIALIZE

` struct {`  
`   u32 __unk;       // in`  
`   u32 __zeroes[3]; // in`  
` };`

## NVGPU\_AS\_IOCTL\_INITIALIZE\_EX

` struct {`  
`   u32 __unk0;      // in`  
`   u32 __pad0;`  
`   u32 __unk1;`  
`   u32 __pad1;`  
`   u64 __unk2;`  
`   u64 __unk3;`  
`   u64 __unk4;`  
` };`

## /dev/nvmap

| Value      | Direction | Size | Description                                             | Notes                |
| ---------- | --------- | ---- | ------------------------------------------------------- | -------------------- |
| 0xC0080101 | Inout     | 8    | [\#NVMAP\_IOC\_CREATE](#NVMAP_IOC_CREATE "wikilink")    |                      |
| 0x00000102 | \-        | 0    | NVMAP\_IOC\_CLAIM                                       | Returns NotSupported |
| 0xC0080103 | Inout     | 8    | [\#NVMAP\_IOC\_FROM\_ID](#NVMAP_IOC_FROM_ID "wikilink") |                      |
| 0xC0200104 | Inout     | 32   | [\#NVMAP\_IOC\_ALLOC](#NVMAP_IOC_ALLOC "wikilink")      |                      |
| 0xC0180105 | Inout     | 24   | [\#NVMAP\_IOC\_FREE](#NVMAP_IOC_FREE "wikilink")        |                      |
| 0xC0280106 | Inout     | 40   | NVMAP\_IOC\_MMAP                                        | Returns NotSupported |
| 0xC0280107 | Inout     | 40   | NVMAP\_IOC\_WRITE                                       | Returns NotSupported |
| 0xC0280108 | Inout     | 40   | NVMAP\_IOC\_READ                                        | Returns NotSupported |
| 0xC00C0109 | Inout     | 12   | [\#NVMAP\_IOC\_PARAM](#NVMAP_IOC_PARAM "wikilink")      |                      |
| 0xC010010A | Inout     | 16   | NVMAP\_IOC\_PIN\_MULT                                   | Returns NotSupported |
| 0xC010010B | Inout     | 16   | NVMAP\_IOC\_UNPIN\_MULT                                 | Returns NotSupported |
| 0xC008010C | Inout     | 8    | NVMAP\_IOC\_CACHE                                       | Returns NotSupported |
| 0xC004010D | Inout     | 4    |                                                         | Returns NotSupported |
| 0xC008010E | Inout     | 8    | [\#NVMAP\_IOC\_GET\_ID](#NVMAP_IOC_GET_ID "wikilink")   |                      |
| 0xC004010F | Inout     | 4    |                                                         | Returns NotSupported |
| 0x40040110 | In        | 4    |                                                         | Returns NotSupported |
| 0x00000111 | \-        | 0    |                                                         | Returns NotSupported |

### NVMAP\_IOC\_CREATE

Creates an nvmap object. Identical to Linux driver.

` struct {`  
`   u32 __size;   // in`  
`   u32 __handle; // out`  
` };`

### NVMAP\_IOC\_FROM\_ID

Get handle to an existing nvmap object. Identical to Linux driver.

` struct {`  
`   u32 __id;     // in`  
`   u32 __handle; // out`  
` };`

### NVMAP\_IOC\_ALLOC

Allocate memory for the nvmap object. Nintendo extended this one with 16
bytes, and changed it from in to inout.

` struct {`  
`   u32 __handle;   // in`  
`   u32 __heapmask; // in`  
`   u32 __flags;    // in (0=read-only, 1=read-write)`  
`   u32 __align;    // in`  
`   u8  __unk0;     // in`  
`   u8  __pad[7];`  
`   u64 __addr;     // in`  
` };`

### NVMAP\_IOC\_FREE

This one is completely custom. Partly because the Linux driver passed
the handle as the ioctl "arg-ptr", and HIPC can't handle that voodoo.

` struct {`  
`   u32 __handle;   // in`  
`   u32 __pad;`  
`   u64 __refcount; // out`  
`   u32 __size;     // out`  
`   u32 __flags;    // out`  
` };`

### NVMAP\_IOC\_PARAM

Returns info about a nvmap object. Identical to Linux driver, but
extended with further params.

` struct {`  
`   u32 __handle; // in`  
`   u32 __param;  // in, 1=SIZE, 2=ALIGNMENT, 3=?, 4=?, 5=UNK0, 6=?`  
`   u32 __result; // out`  
` };`

### NVMAP\_IOC\_GET\_ID

Returns an id for a nvmap object. Identical to Linux driver.

` struct {`  
`   u32 __id;     // out`  
`   u32 __handle; // in`  
` };`

## Channels

Channels are a concept for NVIDIA hardware blocks that share a common
interface.

| Path              | Name |
| ----------------- | ---- |
| /dev/nvhost-gpu   |      |
| /dev/nvhost-vic   |      |
| /dev/nvhost-nvdec |      |
| /dev/nvhost-nvjpg |      |

## Channel Ioctls

| Value      | Size     | Description                                   | Notes |
| ---------- | -------- | --------------------------------------------- | ----- |
| 0xC0??0001 | Variable | NVHOST\_IOCTL\_CHANNEL\_SUBMIT                |       |
| 0xC0080002 | 8        | NVHOST\_IOCTL\_CHANNEL\_GET\_SYNCPOINT        |       |
| 0xC0080003 | 8        | NVHOST\_IOCTL\_CHANNEL\_GET\_WAITBASE         |       |
| 0xC0080004 | 8        | NVHOST\_IOCTL\_CHANNEL\_SET\_TIMEOUT\_EX      |       |
| 0x40040007 | 4        |                                               |       |
| 0xC0??0009 | Variable | NVHOST\_IOCTL\_CHANNEL\_MAP\_BUFFER           |       |
| 0xC0??000A | Variable | NVHOST\_IOCTL\_CHANNEL\_UNMAP\_BUFFER         |       |
| 0x00000013 | 0        |                                               |       |
| 0x40044801 | 4        | NVGPU\_IOCTL\_CHANNEL\_SET\_NVMAP\_FD         |       |
| 0x40044803 | 4        | NVGPU\_IOCTL\_CHANNEL\_SET\_PRIORITY          |       |
| 0x40084805 | 8        | NVGPU\_IOCTL\_CHANNEL\_ALLOC\_GPFIFO          |       |
| 0xC0044807 | 4        | NVGPU\_IOCTL\_CHANNEL\_CYCLE\_STATS           |       |
| 0xC0184808 | 24       | NVGPU\_IOCTL\_CHANNEL\_SUBMIT\_GPFIFO         |       |
| 0xC0104809 | 16       | NVGPU\_IOCTL\_CHANNEL\_ALLOC\_OBJ\_CTX        |       |
| 0x4008480A | 8        | NVGPU\_IOCTL\_CHANNEL\_FREE\_OBJ\_CTX         |       |
| 0xC010480B | 16       | NVGPU\_IOCTL\_CHANNEL\_ZCULL\_BIND            |       |
| 0xC018480C | 24       | NVGPU\_IOCTL\_CHANNEL\_SET\_ERROR\_NOTIFIER   |       |
| 0x4004480D | 4        | NVGPU\_IOCTL\_CHANNEL\_OPEN                   |       |
| 0x0000480E | 0        | NVGPU\_IOCTL\_CHANNEL\_ENABLE                 |       |
| 0x0000480F | 0        | NVGPU\_IOCTL\_CHANNEL\_DISABLE                |       |
| 0x00004810 | 0        | NVGPU\_IOCTL\_CHANNEL\_PREEMPT                |       |
| 0x00004811 | 0        | NVGPU\_IOCTL\_CHANNEL\_FORCE\_RESET           |       |
| 0x40084812 | 8        | NVGPU\_IOCTL\_CHANNEL\_EVENTS\_CTRL           |       |
| 0xC0104813 | 16       | NVGPU\_IOCTL\_CHANNEL\_CYCLE\_STATS\_SNAPSHOT |       |
| 0x80804816 | 128      |                                               |       |
| 0xC0104817 | 16       |                                               |       |
| 0x40204818 | 32       | NVGPU\_IOCTL\_CHANNEL\_ALLOC\_GPFIFO\_EX      |       |
| 0xC0484819 | 72       |                                               |       |
| 0xC020481A | 32       | NVGPU\_IOCTL\_CHANNEL\_ALLOC\_GPFIFO\_EX2     |       |
|            |          |                                               |       |
| 0x40084714 | 8        | set\_user\_address                            |       |
| 0x80084715 | 8        | get\_user\_address                            |       |

## Remaining Ioctls

| Value                | Size       | Description                               | Notes                 |
| -------------------- | ---------- | ----------------------------------------- | --------------------- |
| /dev/nvhost-dbg-gpu  | 0x40084401 | NVGPU\_DBG\_GPU\_IOCTL\_BIND\_CHANNEL     |                       |
| /dev/nvhost-dbg-gpu  | 0xC0??4402 | NVGPU\_DBG\_GPU\_IOCTL\_REG\_OPS          | ?? == size is unknown |
| /dev/nvhost-dbg-gpu  | 0x40084403 | NVGPU\_DBG\_GPU\_IOCTL\_EVENTS\_CTRL      |                       |
| /dev/nvhost-dbg-gpu  | 0x40044404 | NVGPU\_DBG\_GPU\_IOCTL\_POWERGATE         |                       |
| /dev/nvhost-dbg-gpu  | 0x40044405 | NVGPU\_DBG\_GPU\_IOCTL\_SMPC\_CTXSW\_MODE |                       |
| /dev/nvhost-dbg-gpu  | 0xC0184407 | NVGPU\_DBG\_GPU\_IOCTL\_PERFBUF\_MAP      |                       |
| /dev/nvhost-dbg-gpu  | 0x40084408 | NVGPU\_DBG\_GPU\_IOCTL\_PERFBUF\_UNMAP    |                       |
| /dev/nvhost-dbg-gpu  | 0x40084409 | NVGPU\_DBG\_GPU\_IOCTL\_PC\_SAMPLING      |                       |
| /dev/nvhost-ctrl-gpu | 0x80044701 | NVGPU\_GPU\_IOCTL\_ZCULL\_GET\_CTX\_SIZE  |                       |
| /dev/nvhost-ctrl-gpu | 0x80284702 | NVGPU\_GPU\_IOCTL\_ZCULL\_GET\_INFO       |                       |
| /dev/nvhost-ctrl-gpu | 0x402C4703 | NVGPU\_GPU\_IOCTL\_ZBC\_SET\_TABLE        |                       |
| /dev/nvhost-ctrl-gpu | 0xC0344704 | NVGPU\_GPU\_IOCTL\_ZBC\_QUERY\_TABLE      |                       |
| /dev/nvhost-ctrl-gpu | 0xC0B04705 | NVGPU\_GPU\_IOCTL\_GET\_CHARACTERISTICS   |                       |
| /dev/nvhost-ctrl-gpu | 0xC0184706 | NVGPU\_GPU\_IOCTL\_GET\_TPC\_MASKS        |                       |
| /dev/nvhost-ctrl-gpu | 0x40084707 | NVGPU\_GPU\_IOCTL\_OPEN\_CHANNEL          |                       |
| /dev/nvhost-ctrl-gpu | 0x4008470E |                                           |                       |
| /dev/nvhost-ctrl-gpu | 0x4010470F |                                           |                       |
| /dev/nvhost-ctrl-gpu | 0xC0084710 |                                           |                       |
| /dev/nvhost-ctrl-gpu | 0x80084711 |                                           |                       |
| /dev/nvhost-ctrl-gpu | 0x80084712 |                                           |                       |
| /dev/nvhost-ctrl-gpu | 0xC0044713 |                                           |                       |
| /dev/nvhost-ctrl-gpu | 0x80084714 |                                           |                       |
| /dev/nvhost-ctrl-gpu | 0x80044715 |                                           |                       |
| /dev/nvhost-ctrl-gpu | 0x8018471A |                                           |                       |
| /dev/nvhost-ctrl-gpu | 0xC008471B |                                           |                       |
| /dev/nvhost-ctrl-gpu | 0xC010471C |                                           |                       |
|                      |            |                                           |                       |

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

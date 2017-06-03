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
is then later bound with a channel.

Once a nvgpu channel has been bound to an address space it cannot be
unbound. There is no support for allowing an nvgpu channel to change
from one address space to another (or from one to
none).

| Device             | Direction | Size | Value      | Description                                                                       | Notes |
| ------------------ | --------- | ---- | ---------- | --------------------------------------------------------------------------------- | ----- |
| /dev/nvhost-as-gpu | In        | 4    | 0x40044101 | [\#NVGPU\_AS\_IOCTL\_BIND\_CHANNEL](#NVGPU_AS_IOCTL_BIND_CHANNEL "wikilink")      |       |
| /dev/nvhost-as-gpu | Inout     | 24   | 0xC0184102 | [\#NVGPU\_AS\_IOCTL\_ALLOC\_SPACE](#NVGPU_AS_IOCTL_ALLOC_SPACE "wikilink")        |       |
| /dev/nvhost-as-gpu | Inout     | 16   | 0xC0104103 | [\#NVGPU\_AS\_IOCTL\_FREE\_SPACE](#NVGPU_AS_IOCTL_FREE_SPACE "wikilink")          |       |
| /dev/nvhost-as-gpu | Inout     | 24   | 0xC0184104 | [\#NVGPU\_AS\_IOCTL\_MAP\_BUFFER](#NVGPU_AS_IOCTL_MAP_BUFFER "wikilink")          |       |
| /dev/nvhost-as-gpu | Inout     | 8    | 0xC0084105 | [\#NVGPU\_AS\_IOCTL\_UNMAP\_BUFFER](#NVGPU_AS_IOCTL_UNMAP_BUFFER "wikilink")      |       |
| /dev/nvhost-as-gpu | Inout     | 40   | 0xC0284106 | NVGPU\_AS\_IOCTL\_MAP\_BUFFER\_EX                                                 |       |
| /dev/nvhost-as-gpu | In        | 16   | 0x40104107 | [\#NVGPU\_AS\_IOCTL\_INITIALIZE](#NVGPU_AS_IOCTL_INITIALIZE "wikilink")           |       |
| /dev/nvhost-as-gpu | Inout     | 64   | 0xC0404108 | [\#NVGPU\_AS\_IOCTL\_GET\_VA\_REGIONS](#NVGPU_AS_IOCTL_GET_VA_REGIONS "wikilink") |       |
| /dev/nvhost-as-gpu | In        | 40   | 0x40284109 | [\#NVGPU\_AS\_IOCTL\_INITIALIZE\_EX](#NVGPU_AS_IOCTL_INITIALIZE_EX "wikilink")    |       |
| /dev/nvhost-as-gpu | Inout     | 20   | 0xC0144114 |                                                                                   |       |

### NVGPU\_AS\_IOCTL\_BIND\_CHANNEL

Identical to Linux driver.

` struct {`  
`   u32 __fd; // in`  
` };`

### NVGPU\_AS\_IOCTL\_ALLOC\_SPACE

This one reserves pages in the device address space.

` struct {`  
`   u32 __pages;     // in`  
`   u32 __page_size; // in`  
`   u32 __flags;     // in`  
`   u32 __pad;`  
`   union {`  
`     u64 __offset;  // out`  
`     u64 __align;   // in`  
`   };`  
` };`

### NVGPU\_AS\_IOCTL\_FREE\_SPACE

` struct {`  
`   u64 __offset;    // in`  
`   u32 __pages;     // in`  
`   u32 __page_size; // in`  
` };`

### NVGPU\_AS\_IOCTL\_MAP\_BUFFER

Map a memory region in the device address space. Identical to Linux
driver pretty much.

On success, the mapped memory region is locked by having
[SVC\#MemoryState](SVC#MemoryState.md##MemoryState "wikilink") bit34
set.

` struct {`  
`   u32 __flags;        // in, 4 works`  
`   u32 __reserved;`  
`   u32 __nvmap_handle; // in`  
`   u32 __page_size;    // inout, 0 means don't care`  
`   union {`  
`     u64 __offset;     // out`  
`     u64 __align;      // in`  
`   };`  
` };`

### NVGPU\_AS\_IOCTL\_UNMAP\_BUFFER

Doesn't do shit.

### NVGPU\_AS\_IOCTL\_INITIALIZE

Nintendo custom.

` struct {`  
`   u32 __size;       // in (must be aligned to 0x10000; 0=default)`  
`   u32 __zeroes[3];  // in`  
` };`

### NVGPU\_AS\_IOCTL\_GET\_VA\_REGIONS

Nintendo modified to get rid of pointer in
struct.

` struct va_region {`  
`   u64 __offset;`  
`   u32 __page_size;`  
`   u32 __reserved;`  
`   u64 __pages;`  
` };`  
` `  
` struct {`  
`   u64              __not_used;   // (contained output user ptr on linux, ignored)`  
`   u32              __bufsize;    // inout, forced to 2*sizeof(struct va_region)`  
`   u32              __reserved;`  
`   struct va_region __regions[2]; // out`  
` };`

### NVGPU\_AS\_IOCTL\_INITIALIZE\_EX

Nintendo
custom.

` struct {`  
`   u32 __size; // in (must be aligned to 0x10000; 0=default)`  
`   u32 __pad0;`  
`   u32 __unk0; // in`  
`   u32 __pad1;`  
`   u64 __unk1; // in`  
`   u64 __unk2; // in`  
`   u64 __unk3; // in`  
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
`   u32 __flags;    // out, 1=NOT_FREED_YET`  
` };`

### NVMAP\_IOC\_PARAM

Returns info about a nvmap object. Identical to Linux driver, but
extended with further
params.

` struct {`  
`   u32 __handle; // in`  
`   u32 __param;  // in, 1=SIZE, 2=ALIGNMENT, 3=BASE (returns error), 4=HEAP (always 0x40000000), 5=KIND, 6=COMPR (unused)`  
`   u32 __result; // out`  
` };`

### NVMAP\_IOC\_GET\_ID

Returns an id for a nvmap object. Identical to Linux driver.

` struct {`  
`   u32 __id;     // out`  
`   u32 __handle; // in`  
` };`

## /dev/nvhost-ctrl-gpu

This device is for global (context independent) operations on the
gpu.

| Value      | Direction | Size | Description                              | Notes |
| ---------- | --------- | ---- | ---------------------------------------- | ----- |
| 0x80044701 | Out       | 4    | NVGPU\_GPU\_IOCTL\_ZCULL\_GET\_CTX\_SIZE |       |
| 0x80284702 | Out       | 40   | NVGPU\_GPU\_IOCTL\_ZCULL\_GET\_INFO      |       |
| 0x402C4703 | In        | 44   | NVGPU\_GPU\_IOCTL\_ZBC\_SET\_TABLE       |       |
| 0xC0344704 | Inout     | 52   | NVGPU\_GPU\_IOCTL\_ZBC\_QUERY\_TABLE     |       |
| 0xC0B04705 | Inout     | 176  | NVGPU\_GPU\_IOCTL\_GET\_CHARACTERISTICS  |       |
| 0xC0184706 | Inout     | 24   | NVGPU\_GPU\_IOCTL\_GET\_TPC\_MASKS       |       |
| 0x40084707 | In        | 8    | NVGPU\_GPU\_IOCTL\_OPEN\_CHANNEL         |       |
| 0x4008470E | In        | 8    |                                          |       |
| 0x4010470F | In        | 16   |                                          |       |
| 0xC0084710 | Inout     | 8    |                                          |       |
| 0x80084711 | Out       | 8    |                                          |       |
| 0x80084712 | Out       | 8    |                                          |       |
| 0xC0044713 | Inout     | 4    |                                          |       |
| 0x80084714 | Out       | 8    |                                          |       |
| 0x80044715 | Out       | 4    |                                          |       |
| 0x8018471A | Out       | 24   |                                          |       |
| 0xC008471B | Inout     | 8    |                                          |       |
| 0xC010471C | Inout     | 16   |                                          |       |

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

| Value      | Size     | Description                                                                                         | Notes                                |
| ---------- | -------- | --------------------------------------------------------------------------------------------------- | ------------------------------------ |
| 0xC0??0001 | Variable | NVHOST\_IOCTL\_CHANNEL\_SUBMIT                                                                      |                                      |
| 0xC0080002 | 8        | NVHOST\_IOCTL\_CHANNEL\_GET\_SYNCPOINT                                                              |                                      |
| 0xC0080003 | 8        | NVHOST\_IOCTL\_CHANNEL\_GET\_WAITBASE                                                               |                                      |
| 0xC0080004 | 8        | NVHOST\_IOCTL\_CHANNEL\_SET\_TIMEOUT\_EX                                                            |                                      |
| 0x40040007 | 4        |                                                                                                     |                                      |
| 0xC0??0009 | Variable | NVHOST\_IOCTL\_CHANNEL\_MAP\_BUFFER                                                                 |                                      |
| 0xC0??000A | Variable | NVHOST\_IOCTL\_CHANNEL\_UNMAP\_BUFFER                                                               |                                      |
| 0x00000013 | 0        |                                                                                                     |                                      |
| 0x40044801 | 4        | [\#NVGPU\_IOCTL\_CHANNEL\_SET\_NVMAP\_FD](#NVGPU_IOCTL_CHANNEL_SET_NVMAP_FD "wikilink")             |                                      |
| 0x40044803 | 4        | NVGPU\_IOCTL\_CHANNEL\_SET\_PRIORITY                                                                |                                      |
| 0x40084805 | 8        | [\#NVGPU\_IOCTL\_CHANNEL\_ALLOC\_GPFIFO](#NVGPU_IOCTL_CHANNEL_ALLOC_GPFIFO "wikilink")              |                                      |
| 0xC0044807 | 4        | NVGPU\_IOCTL\_CHANNEL\_CYCLE\_STATS                                                                 |                                      |
| 0xC0??4808 | Variable | [\#NVGPU\_IOCTL\_CHANNEL\_SUBMIT\_GPFIFO](#NVGPU_IOCTL_CHANNEL_SUBMIT_GPFIFO "wikilink")            |                                      |
| 0xC0104809 | 16       | [\#NVGPU\_IOCTL\_CHANNEL\_ALLOC\_OBJ\_CTX](#NVGPU_IOCTL_CHANNEL_ALLOC_OBJ_CTX "wikilink")           |                                      |
| 0xC010480B | 16       | NVGPU\_IOCTL\_CHANNEL\_ZCULL\_BIND                                                                  |                                      |
| 0xC018480C | 24       | [\#NVGPU\_IOCTL\_CHANNEL\_SET\_ERROR\_NOTIFIER](#NVGPU_IOCTL_CHANNEL_SET_ERROR_NOTIFIER "wikilink") |                                      |
| 0x4004480D | 4        | [\#NVGPU\_IOCTL\_CHANNEL\_OPEN](#NVGPU_IOCTL_CHANNEL_OPEN "wikilink")                               |                                      |
| 0x0000480E | 0        | [\#NVGPU\_IOCTL\_CHANNEL\_ENABLE](#NVGPU_IOCTL_CHANNEL_ENABLE "wikilink")                           |                                      |
| 0x0000480F | 0        | [\#NVGPU\_IOCTL\_CHANNEL\_DISABLE](#NVGPU_IOCTL_CHANNEL_DISABLE "wikilink")                         |                                      |
| 0x00004810 | 0        | [\#NVGPU\_IOCTL\_CHANNEL\_PREEMPT](#NVGPU_IOCTL_CHANNEL_PREEMPT "wikilink")                         |                                      |
| 0x00004811 | 0        | [\#NVGPU\_IOCTL\_CHANNEL\_FORCE\_RESET](#NVGPU_IOCTL_CHANNEL_FORCE_RESET "wikilink")                |                                      |
| 0x40084812 | 8        | [\#NVGPU\_IOCTL\_CHANNEL\_EVENTS\_CTRL](#NVGPU_IOCTL_CHANNEL_EVENTS_CTRL "wikilink")                |                                      |
| 0xC0104813 | 16       | NVGPU\_IOCTL\_CHANNEL\_CYCLE\_STATS\_SNAPSHOT                                                       |                                      |
| 0x80804816 | 128      |                                                                                                     | Only works when the channel is busy  |
| 0xC0104817 | 16       | [\#NVGPU\_IOCTL\_CHANNEL\_GET\_ERROR](#NVGPU_IOCTL_CHANNEL_GET_ERROR "wikilink")                    |                                      |
| 0x40204818 | 32       | [\#NVGPU\_IOCTL\_CHANNEL\_ALLOC\_GPFIFO\_EX](#NVGPU_IOCTL_CHANNEL_ALLOC_GPFIFO_EX "wikilink")       |                                      |
| 0xC0??4819 | Variable | [\#NVGPU\_IOCTL\_CHANNEL\_SUBMIT\_GPFIFO\_EX](#NVGPU_IOCTL_CHANNEL_SUBMIT_GPFIFO_EX "wikilink")     |                                      |
| 0xC020481A | 32       | [\#NVGPU\_IOCTL\_CHANNEL\_ALLOC\_GPFIFO\_EX2](#NVGPU_IOCTL_CHANNEL_ALLOC_GPFIFO_EX2 "wikilink")     |                                      |
|            |          |                                                                                                     |                                      |
| 0x40084714 | 8        | set\_user\_address                                                                                  | Sets an unknown user context address |
| 0x80084715 | 8        | get\_user\_address                                                                                  | Gets an unknown user context address |

### NVGPU\_IOCTL\_CHANNEL\_SET\_NVMAP\_FD

Binds a nvmap object to this channel. Identical to Linux driver.

` struct {`  
`   u32 __nvmap_fd;     // in`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_ALLOC\_GPFIFO

Allocates gpfifo entries. Identical to Linux driver.

` struct {`  
`   u32 __num_entries;     // in`  
`   u32 __flags;           // in`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_SUBMIT\_GPFIFO

Submits a gpfifo object. Modified to take inline fence objects instead
of a
pointer.

` struct fence {`  
`   u32 __id;`  
`   u32 __value;`  
` };`  
` `  
` struct gpfifo_entry {`  
`   u32 __entry0;`  
`   u32 __entry1;`  
` };`  
` `  
` struct {`  
`   u64 __gpfifo;                     // in (pointer to gpfifo fence structs; ignored)`  
`   u32 __num_entries;                // in (number of fence objects being submitted)`  
`   u32 __flags;                      // in`  
`   struct fence        __fence_out;  // out (returned new fence object for others to wait on)`  
`   struct gpfifo_entry __entries[];  // in (depends on __num_entries)`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_ALLOC\_OBJ\_CTX

Allocates a graphics context object. Modified to ignore object's
ID.

` struct {`  
`   u32 __class_num;    // in (0xB197=2d, 0xB1C0=compute, 0xA140=kepler, 0xB0B5=DMA, 0xB06F=channel_gpfifo)`  
`   u32 __flags;        // in`  
`   u64 __obj_id;       // out (ignored; used for FREE_OBJ_CTX ioctl, which is not supported)`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_SET\_ERROR\_NOTIFIER

Initializes the error notifier for this channel. Identical to Linux
driver.

` struct {`  
`   u64 __offset;    // in`  
`   u64 __size;      // in`  
`   u32 __mem;       // in (nvmap object handle)`  
`   u32 __padding;   // in`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_OPEN

Opens the current channel. Unused and takes an unknown argument.

` struct {`  
`   u32 __unk;    // in (only accepts 0x32, 0x64 or 0x96)`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_ENABLE

Enables the current channel. Identical to Linux driver.

### NVGPU\_IOCTL\_CHANNEL\_DISABLE

Disables the current channel. Identical to Linux driver.

### NVGPU\_IOCTL\_CHANNEL\_PREEMPT

Clears the FIFO pipe for this channel. Identical to Linux driver.

### NVGPU\_IOCTL\_CHANNEL\_FORCE\_RESET

Forces the channel to reset. Identical to Linux driver.

### NVGPU\_IOCTL\_CHANNEL\_EVENTS\_CTRL

Controls event notifications. Modified to take an additional argument.

` struct {`  
`   u32 __cmd;    // in (0=disable, 1=enable, 2=clear)`  
`   u32 __unk;    // in (accepts 1 or 2)`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_GET\_ERROR

Returns the current error notification caught by the error notifier.
Exclusive to the Switch.

` struct {`  
`   u64 __timestamp;    // out (nanoseconds since Jan. 1, 1970)`  
`   u32 __info32;       // out (error code)`  
`   u16 __info16;       // out (additional error info)`  
`   u16 __status;       // out (always 0xFFFF)`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_ALLOC\_GPFIFO\_EX

Allocates gpfifo entries with additional parameters. Exclusive to the
Switch.

` struct {`  
`   u32 __num_entries;     // in`  
`   u32 __flags;           // in`  
`   u32 __unk0;            // in (1 works)`  
`   u32 __unk1;            // in`  
`   u32 __unk2;            // in`  
`   u32 __unk3;            // in`  
`   u32 __unk4;            // in`  
`   u32 __unk5;            // in`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_SUBMIT\_GPFIFO\_EX

Submits a gpfifo object (async version). Exclusive to the
Switch.

` struct fence {`  
`   u32 __id;`  
`   u32 __value;`  
` };`  
  
` struct {`  
`   u64 __gpfifo;              // in (pointer to gpfifo fence structs; ignored)`  
`   u32 __num_entries;         // in (number of fence objects being submitted)`  
`   u32 __flags;               // in`  
`   struct fence __fence_out;  // out (returned new fence object for others to wait on)`  
`   struct fence __fence;      // in (fence objects; depends on __num_entries)`  
`   ...`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_ALLOC\_GPFIFO\_EX2

Allocates gpfifo entries with additional parameters and returns a fence.
Exclusive to the
Switch.

` struct fence {`  
`   u32 __id;`  
`   u32 __value;`  
` };`  
  
` struct {`  
`   u32 __num_entries;         // in`  
`   u32 __flags;               // in`  
`   u32 __unk0;                // in (1 works)`  
`   struct fence __fence_out;  // out`  
`   u32 __unk1;                // in`  
`   u32 __unk2;                // in`  
`   u32 __unk3;                // in`  
` };`

## Remaining Ioctls

| Value               | Size       | Description                               | Notes                 |
| ------------------- | ---------- | ----------------------------------------- | --------------------- |
| /dev/nvhost-dbg-gpu | 0x40084401 | NVGPU\_DBG\_GPU\_IOCTL\_BIND\_CHANNEL     |                       |
| /dev/nvhost-dbg-gpu | 0xC0??4402 | NVGPU\_DBG\_GPU\_IOCTL\_REG\_OPS          | ?? == size is unknown |
| /dev/nvhost-dbg-gpu | 0x40084403 | NVGPU\_DBG\_GPU\_IOCTL\_EVENTS\_CTRL      |                       |
| /dev/nvhost-dbg-gpu | 0x40044404 | NVGPU\_DBG\_GPU\_IOCTL\_POWERGATE         |                       |
| /dev/nvhost-dbg-gpu | 0x40044405 | NVGPU\_DBG\_GPU\_IOCTL\_SMPC\_CTXSW\_MODE |                       |
| /dev/nvhost-dbg-gpu | 0xC0184407 | NVGPU\_DBG\_GPU\_IOCTL\_PERFBUF\_MAP      |                       |
| /dev/nvhost-dbg-gpu | 0x40084408 | NVGPU\_DBG\_GPU\_IOCTL\_PERFBUF\_UNMAP    |                       |
| /dev/nvhost-dbg-gpu | 0x40084409 | NVGPU\_DBG\_GPU\_IOCTL\_PC\_SAMPLING      |                       |
|                     |            |                                           |                       |

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

| Cmd     | Name                 |
| ------- | -------------------- |
| 0       | Success              |
| 1       | NotImplemented       |
| 2       | NotSupported         |
| 3       | NotInitialized       |
| 4       | BadParameter         |
| 5       | Timeout              |
| 6       | InsufficientMemory   |
| 7       | ReadOnlyAttribute    |
| 8       | InvalidState         |
| 9       | InvalidAddress       |
| 0xA     | InvalidSize          |
| 0xB     | BadValue             |
| 0xD     | AlreadyAllocated     |
| 0xE     | Busy                 |
| 0xF     | ResourceError        |
| 0x10    | CountMismatch        |
| 0x1000  | SharedMemoryTooSmall |
| 0x30003 | FileOperationFailed  |
| 0x3000F | IoctlFailed          |

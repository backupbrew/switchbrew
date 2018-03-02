The Switch uses a customized NVIDIA driver.

# nvdrv, nvdrv:a, nvdrv:s, nvdrv:t

This is "nns::nvdrv::INvDrvServices".

Main NVIDIA driver service.

Each service is used by:

  - "nvdrv": regular applications
  - "nvdrv:a": applets
  - "nvdrv:s": sysmodules
  - "nvdrv:t": factory titles

| Cmd | Name                                                           |
| --- | -------------------------------------------------------------- |
| 0   | [\#Open](#Open "wikilink")                                     |
| 1   | [\#Ioctl](#Ioctl "wikilink")                                   |
| 2   | [\#Close](#Close "wikilink")                                   |
| 3   | [\#Initialize](#Initialize "wikilink")                         |
| 4   | [\#QueryEvent](#QueryEvent "wikilink")                         |
| 5   | [\#MapSharedMem](#MapSharedMem "wikilink")                     |
| 6   | [\#GetStatus](#GetStatus "wikilink")                           |
| 7   | [\#ForceSetClientPID](#ForceSetClientPID "wikilink")           |
| 8   | [\#SetClientPID](#SetClientPID "wikilink")                     |
| 9   | [\#DumpGraphicsMemoryInfo](#DumpGraphicsMemoryInfo "wikilink") |
| 10  | \[3.0.0+\]                                                     |
| 11  | \[3.0.0+\] [\#Ioctl2](#Ioctl2 "wikilink")                      |
| 12  | \[3.0.0+\] [\#Ioctl3](#Ioctl3 "wikilink")                      |
| 13  | \[3.0.0+\]                                                     |

## Open

Takes a type-0x5 input buffer for the device-path. Returns the output
32bit **fd** and the u32 **error\_code**.

## Ioctl

Takes a 32bit **fd**, an u32 **ioctl\_cmd**, a type-0x21 input buffer,
and a type-0x22 output buffer. Returns an output u32 (**error\_code**).

The addr/size for send/recv buffers are only set when the associated
direction bit is set in the ioctl cmd (addr/size = 0 otherwise).

## Close

Takes a 32bit **fd**. Returns an output u32 (**error\_code**).

## Initialize

Takes two copy-handles (**current\_process** and **transfer\_memory**)
and an input u32 (**transfer\_memory\_size**). Returns an output u32
(**error\_code**).

Webkit applet creates the transfer-memory with perm = 0 and size
0x300000.

## QueryEvent

Takes two input u32s (**fd** and **event\_id**), with the second word
immediately after the first one. Returns an output u32 (**error\_code**)
and a copy-handle (**event\_handle**).

## MapSharedMem

Takes a copy-handle (**transfer\_memory**) and two input u32s (**fd**
and **nvmap\_handle**). Returns an output u32 (**error\_code**).

## GetStatus

Takes no input. Returns 0x10-bytes and an output u32 (**error\_code**).

## ForceSetClientPID

Takes an input u64 which must [match](IPC%20Marshalling.md "wikilink")
the user-process PID
([AppletResourceUserId](AM%20services.md "wikilink")). Returns an output
u32 (**error\_code**).

## SetClientPID

Takes a PID-descriptor and an u64 which must
[match](IPC%20Marshalling.md "wikilink") the user-process PID
([AppletResourceUserId](AM%20services.md "wikilink")). Returns an output
u32 (**error\_code**).

## DumpGraphicsMemoryInfo

No input or output. Does nothing.

## Cmd10

Takes a copy-handle and an input u32. Returns an output u32
(**error\_code**).

## Ioctl2

Takes a type-0x21 buffer, a type-0x22 buffer, a type-0x21 buffer, and
two input u32s. Returns an output u32 (**error\_code**).

## Ioctl3

Same input/output as Ioctl2, except cmdhdr\_word1 is 0x100B instead of
0xC0B.

## Cmd13

Takes an input u64. No output.

Official user-processes starting with 3.0.0 now use this at the end of
nvdrv service init with value 0x1.

# Ioctls

The ioctl number is generated with the following primitive (see Linux
kernel):

`#define _IOC(inout, group, num, len) \`  
`   (inout | ((len & IOCPARM_MASK) << 16) | ((group) << 8) | (num))`

The following table contains known
ioctls.

## /dev/nvhost-ctrl

| Value      | Direction | Size | Description                                                                                 | Notes |
| ---------- | --------- | ---- | ------------------------------------------------------------------------------------------- | ----- |
| 0xC0080014 | Inout     | 8    | [\#NVHOST\_IOCTL\_CTRL\_SYNCPT\_READ](#NVHOST_IOCTL_CTRL_SYNCPT_READ "wikilink")            |       |
| 0x40040015 | In        | 4    | [\#NVHOST\_IOCTL\_CTRL\_SYNCPT\_INCR](#NVHOST_IOCTL_CTRL_SYNCPT_INCR "wikilink")            |       |
| 0xC00C0016 | Inout     | 12   | [\#NVHOST\_IOCTL\_CTRL\_SYNCPT\_WAIT](#NVHOST_IOCTL_CTRL_SYNCPT_WAIT "wikilink")            |       |
| 0x40080017 | In        | 8    | [\#NVHOST\_IOCTL\_CTRL\_MODULE\_MUTEX](#NVHOST_IOCTL_CTRL_MODULE_MUTEX "wikilink")          |       |
| 0xC0180018 | Inout     | 24   | [\#NVHOST\_IOCTL\_CTRL\_MODULE\_REGRDWR](#NVHOST_IOCTL_CTRL_MODULE_REGRDWR "wikilink")      |       |
| 0xC0100019 | Inout     | 16   | [\#NVHOST\_IOCTL\_CTRL\_SYNCPT\_WAITEX](#NVHOST_IOCTL_CTRL_SYNCPT_WAITEX "wikilink")        |       |
| 0xC008001A | Inout     | 8    | [\#NVHOST\_IOCTL\_CTRL\_SYNCPT\_READ\_MAX](#NVHOST_IOCTL_CTRL_SYNCPT_READ_MAX "wikilink")   |       |
| 0xC183001B | Inout     | 387  | [\#NVHOST\_IOCTL\_CTRL\_GET\_CONFIG](#NVHOST_IOCTL_CTRL_GET_CONFIG "wikilink")              |       |
| 0xC004001C | Inout     | 4    | [\#NVHOST\_IOCTL\_CTRL\_EVENT\_SIGNAL](#NVHOST_IOCTL_CTRL_EVENT_SIGNAL "wikilink")          |       |
| 0xC010001D | Inout     | 16   | [\#NVHOST\_IOCTL\_CTRL\_EVENT\_WAIT](#NVHOST_IOCTL_CTRL_EVENT_WAIT "wikilink")              |       |
| 0xC010001E | Inout     | 16   | [\#NVHOST\_IOCTL\_CTRL\_EVENT\_WAIT\_ASYNC](#NVHOST_IOCTL_CTRL_EVENT_WAIT_ASYNC "wikilink") |       |
| 0xC004001F | Inout     | 4    | [\#NVHOST\_IOCTL\_CTRL\_EVENT\_REGISTER](#NVHOST_IOCTL_CTRL_EVENT_REGISTER "wikilink")      |       |
| 0xC0040020 | Inout     | 4    | [\#NVHOST\_IOCTL\_CTRL\_EVENT\_UNREGISTER](#NVHOST_IOCTL_CTRL_EVENT_UNREGISTER "wikilink")  |       |
| 0x40080021 | In        | 8    | [\#NVHOST\_IOCTL\_CTRL\_EVENT\_KILL](#NVHOST_IOCTL_CTRL_EVENT_KILL "wikilink")              |       |

### NVHOST\_IOCTL\_CTRL\_SYNCPT\_READ

Identical to Linux driver.

` struct {`  
`   __in  u32 id;`  
`   __out u32 value;`  
` };`

### NVHOST\_IOCTL\_CTRL\_SYNCPT\_INCR

Identical to Linux driver.

` struct {`  
`   __in u32 id;`  
` };`

### NVHOST\_IOCTL\_CTRL\_SYNCPT\_WAIT

Identical to Linux driver.

` struct {`  
`   __in u32 id;`  
`   __in u32 thresh;`  
`   __in s32 timeout;`  
` };`

### NVHOST\_IOCTL\_CTRL\_MODULE\_MUTEX

Identical to Linux driver.

` struct {`  
`   __in u32 id;`  
`   __in u32 lock;        // (0==unlock; 1==lock)`  
` };`

### NVHOST\_IOCTL\_CTRL\_MODULE\_REGRDWR

Identical to Linux driver. Uses 32-bit version and doesn't work.

` struct {`  
`   __in u32 id;`  
`   __in u32 num_offsets;`  
`   __in u32 block_size;`  
`   __in u32 offsets;`  
`   __in u32 values;`  
`   __in u32 write;`  
` };`

### NVHOST\_IOCTL\_CTRL\_SYNCPT\_WAITEX

Identical to Linux driver.

` struct {`  
`   __in  u32 id;`  
`   __in  u32 thresh;`  
`   __in  s32 timeout;`  
`   __out u32 value;`  
` };`

### NVHOST\_IOCTL\_CTRL\_SYNCPT\_READ\_MAX

Identical to Linux driver.

` struct {`  
`   __in  u32 id;`  
`   __out u32 value;`  
` };`

### NVHOST\_IOCTL\_CTRL\_GET\_CONFIG

Gets configured settings. Not available in production mode.

` struct {`  
`   __in char domain_str[0x41];       // "nv"`  
`   __in char param_str[0x41];`  
`   __out char config_str[0x101];`  
` };`

### NVHOST\_IOCTL\_CTRL\_EVENT\_SIGNAL

Signals an user event. Exclusive to the Switch.

` struct {`  
`   __in u32 user_event_id;      // ranges from 0x00 to 0x3F`  
` };`

### NVHOST\_IOCTL\_CTRL\_EVENT\_WAIT

Waits on an event. If waiting fails, returns error code 0x05 (Timeout)
and sets **value** to ((**syncpt\_id** \<\< 0x10) | 0x10000000).

Depending on **threshold**, an **user\_event\_id** may be returned for
using with other event
ioctls.

` struct {`  
`   __in    u32 syncpt_id;`  
`   __in    u32 threshold;`  
`   __in    s32 timeout;`  
`   __inout u32 value;           // in=user_event_id (ignored); out=syncpt_value or user_event_id`  
` };`

### NVHOST\_IOCTL\_CTRL\_EVENT\_WAIT\_ASYNC

Waits on an event (async version). If waiting fails, returns error code
0x0B (BadValue).

Depending on **threshold**, an **user\_event\_id** may be returned for
using with other event
ioctls.

` struct {`  
`   __in    u32 syncpt_id;`  
`   __in    u32 threshold;`  
`   __in    u32 timeout;`  
`   __inout u32 value;           // in=user_event_id (ignored); out=syncpt_value or user_event_id`  
` };`

### NVHOST\_IOCTL\_CTRL\_EVENT\_REGISTER

Registers an user event. Exclusive to the Switch.

` struct {`  
`   __in u32 user_event_id;      // ranges from 0x00 to 0x3F`  
` };`

### NVHOST\_IOCTL\_CTRL\_EVENT\_UNREGISTER

Unregisters an user event. Exclusive to the Switch.

` struct {`  
`   __in u32 user_event_id;      // ranges from 0x00 to 0x3F`  
` };`

### NVHOST\_IOCTL\_CTRL\_EVENT\_KILL

Kills user events. Exclusive to the
Switch.

` struct {`  
`   __in u64 user_events;       // 64-bit bitfield where each bit represents one event`  
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
`   __in  u32 size;`  
`   __out u32 handle;`  
` };`

### NVMAP\_IOC\_FROM\_ID

Get handle to an existing nvmap object. Identical to Linux driver.

` struct {`  
`   __in  u32 id;`  
`   __out u32 handle;`  
` };`

### NVMAP\_IOC\_ALLOC

Allocate memory for the nvmap object. Nintendo extended this one with 16
bytes, and changed it from in to inout.

` struct {`  
`   __in u32 handle;`  
`   __in u32 heapmask;`  
`   __in u32 flags;    // (0=read-only, 1=read-write)`  
`   __in u32 align;`  
`   __in u8  kind;`  
`   u8       pad[7];`  
`   __in u64 addr;`  
` };`

### NVMAP\_IOC\_FREE

This one is completely custom. Partly because the Linux driver passed
the handle as the ioctl "arg-ptr", and HIPC can't handle that voodoo.

` struct {`  
`   __in  u32 handle;`  
`   u32       pad;`  
`   __out u64 refcount;`  
`   __out u32 size;`  
`   __out u32 flags;    // 1=NOT_FREED_YET`  
` };`

### NVMAP\_IOC\_PARAM

Returns info about a nvmap object. Identical to Linux driver, but
extended with further
params.

` struct {`  
`   __in  u32 handle;`  
`   __in  u32 param;  // 1=SIZE, 2=ALIGNMENT, 3=BASE (returns error), 4=HEAP (always 0x40000000), 5=KIND, 6=COMPR (unused)`  
`   __out u32 result;`  
` };`

### NVMAP\_IOC\_GET\_ID

Returns an id for a nvmap object. Identical to Linux
driver.

` struct {`  
`   __out u32 id; //~0 indicates error`  
`   __in  u32 handle;`  
` };`

## /dev/nvdisp-ctrl

| Value      | Direction | Size | Description                                      | Notes |
| ---------- | --------- | ---- | ------------------------------------------------ | ----- |
| 0x80040212 | Out       | 4    | TEGRA\_DC\_EXT\_CONTROL\_GET\_NUM\_OUTPUTS       |       |
| 0xC0140213 | Inout     | 20   | TEGRA\_DC\_EXT\_CONTROL\_GET\_OUTPUT\_PROPERTIES |       |
| 0xC1100214 | Inout     | 272  | TEGRA\_DC\_EXT\_CONTROL\_GET\_OUTPUT\_EDID       |       |
| 0xC0040216 | Inout     | 4    | TEGRA\_DC\_EXT\_CONTROL\_SET\_EVENT0             |       |
| 0xC0040217 | Inout     | 4    | TEGRA\_DC\_EXT\_CONTROL\_SET\_EVENT1             |       |
| 0xC0100218 | Inout     | 16   | TEGRA\_DC\_EXT\_CONTROL\_SET\_EVENT2             |       |
| 0xC0100219 | Inout     | 16   | TEGRA\_DC\_EXT\_CONTROL\_SET\_EVENT3             |       |
| 0xC0040220 | Inout     | 4    | TEGRA\_DC\_EXT\_CONTROL\_SET\_EVENT4             |       |
|            |           |      |                                                  |       |

## /dev/nvdisp-disp0, /dev/nvdisp-disp1

| Value      | Direction | Size  | Description                            | Notes |
| ---------- | --------- | ----- | -------------------------------------- | ----- |
| 0x40040201 | In        | 4     | TEGRA\_DC\_EXT\_GET\_WINDOW            |       |
| 0x40040202 | In        | 4     | TEGRA\_DC\_EXT\_PUT\_WINDOW            |       |
| 0xC4C80203 | In        | 1224  | TEGRA\_DC\_EXT\_FLIP                   |       |
| 0x80380204 | Out       | 56    | TEGRA\_DC\_EXT\_GET\_MODE              |       |
| 0x40380205 | Out       | 56    | TEGRA\_DC\_EXT\_SET\_MODE              |       |
| 0x430C0206 | In        | 780   | TEGRA\_DC\_EXT\_SET\_LUT               |       |
| 0x40010207 | In        | 1     | TEGRA\_DC\_EXT\_ENABLE\_DISABLE\_CRC   |       |
| 0x80040208 | Out       | 4     | TEGRA\_DC\_EXT\_GET\_CRC               |       |
| 0x80040209 | Out       | 4     | TEGRA\_DC\_EXT\_GET\_HEAD\_STATUS      |       |
| 0xC038020A | Inout     | 56    | TEGRA\_DC\_EXT\_VALIDATE\_MODE         |       |
| 0x4018020B | In        | 24    | TEGRA\_DC\_EXT\_SET\_CSC               |       |
| 0xC004020C | Inout     | 4     | TEGRA\_DC\_EXT\_GET\_VBLANK\_SYNCPT    |       |
| 0x8040020D | Out       | 64    | TEGRA\_DC\_EXT\_GET\_UNDERFLOWS        |       |
| 0xC99A020E | Inout     | 2458  | TEGRA\_DC\_EXT\_SET\_CMU               |       |
| 0xC004020F | Inout     | 4     | TEGRA\_DC\_EXT\_DPMS                   |       |
| 0x80600210 | Out       | 96    | TEGRA\_DC\_EXT\_GET\_AVI\_INFOFRAME    |       |
| 0x40600211 | In        | 96    | TEGRA\_DC\_EXT\_SET\_AVI\_INFOFRAME    |       |
| 0xEBFC0215 | Inout     | 11260 | TEGRA\_DC\_EXT\_GET\_MODE\_DB          |       |
| 0xC003021A | Inout     | 3     | TEGRA\_DC\_EXT\_PANEL\_GET\_VENDOR\_ID |       |
| 0x803C021B | Out       | 60    | TEGRA\_DC\_EXT\_GET\_MODE2             |       |
| 0x403C021C | In        | 60    | TEGRA\_DC\_EXT\_SET\_MODE2             |       |
| 0xC03C021D | Inout     | 60    | TEGRA\_DC\_EXT\_VALIDATE\_MODE2        |       |
| 0xEF20021E | Inout     | 12064 | TEGRA\_DC\_EXT\_GET\_MODE\_DB2         |       |
| 0xC004021F | Inout     | 4     | TEGRA\_DC\_EXT\_GET\_WINMASK           |       |
|            |           |       |                                        |       |

## /dev/nvcec-ctrl

| Value      | Direction | Size | Description                          | Notes |
| ---------- | --------- | ---- | ------------------------------------ | ----- |
| 0x40010300 | In        | 1    |                                      |       |
| 0x40010301 | In        | 1    | NVCEC\_CTRL\_ENABLE                  |       |
| 0x804C0302 | Out       | 76   | NVCEC\_CTRL\_GET\_PADDR              |       |
| 0x40040303 | In        | 4    | NVCEC\_CTRL\_SET\_LADDR              |       |
| 0xC04C0304 | Inout     | 76   | NVCEC\_CTRL\_WRITE                   |       |
| 0xC04C0305 | Inout     | 76   | NVCEC\_CTRL\_READ                    |       |
| 0x804C0306 | Out       | 76   | NVCEC\_CTRL\_GET\_CONNECTION\_STATUS |       |
| 0x804C0307 | Out       | 76   | NVCEC\_CTRL\_GET\_WRITE\_STATUS      |       |
|            |           |      |                                      |       |

## /dev/nvhdcp\_up-ctrl

| Value      | Direction | Size | Description              | Notes |
| ---------- | --------- | ---- | ------------------------ | ----- |
| 0xC4880401 | Inout     | 1160 | TEGRAIO\_NVHDCP\_READ\_M |       |
| 0xC4880402 | Inout     | 1160 | TEGRAIO\_NVHDCP\_READ\_S |       |
| 0x40010403 | In        | 1    | TEGRAIO\_NVHDCP\_ON\_OFF |       |
|            |           |      |                          |       |

## /dev/nvdcutil-disp0, /dev/nvdcutil-disp1

| Value      | Direction | Size | Description                              | Notes |
| ---------- | --------- | ---- | ---------------------------------------- | ----- |
| 0x40010501 | In        | 1    | NVDCUTIL\_CRC\_ENABLE\_DISABLE           |       |
| 0x40010502 | In        | 1    | NVDCUTIL\_VIRTUAL\_EDID\_ENABLE\_DISABLE |       |
| 0x42040503 | In        | 1056 | NVDCUTIL\_VIRTUAL\_EDID\_SET\_DATA       |       |
| 0x803C0504 | Out       | 60   | NVDCUTIL\_GET\_MODE                      |       |
|            |           |      |                                          |       |

## /dev/nvsched-ctrl

| Value      | Direction | Size | Description                                | Notes |
| ---------- | --------- | ---- | ------------------------------------------ | ----- |
| 0x00000601 | \-        | 0    | NVSCHED\_CTRL\_ENABLE                      |       |
| 0x00000602 | \-        | 0    | NVSCHED\_CTRL\_DISABLE                     |       |
| 0x40180603 | In        | 1056 | NVSCHED\_CTRL\_ADD\_APPLICATION            |       |
| 0x40180604 | In        | 60   | NVSCHED\_CTRL\_UPDATE\_APPLICATION         |       |
| 0x40080605 | In        | 60   | NVSCHED\_CTRL\_REMOVE\_APPLICATION         |       |
| 0x80080606 | Out       | 60   | NVSCHED\_CTRL\_GET\_ID                     |       |
| 0x80080607 | Out       | 60   | NVSCHED\_CTRL\_ADD\_RUNLIST                |       |
| 0x40180608 | In        | 24   | NVSCHED\_CTRL\_UPDATE\_RUNLIST             |       |
| 0x40100609 | In        | 16   | NVSCHED\_CTRL\_LINK\_RUNLIST               |       |
| 0x4010060A | In        | 16   | NVSCHED\_CTRL\_UNLINK\_RUNLIST             |       |
| 0x4008060B | In        | 8    | NVSCHED\_CTRL\_REMOVE\_RUNLIST             |       |
| 0x8001060C | Out       | 1    | NVSCHED\_CTRL\_HAS\_OVERRUN\_EVENT         |       |
| 0x8010060D | Out       | 16   |                                            |       |
| 0x400C060E | In        | 12   | NVSCHED\_CTRL\_PUT\_CONDUCTOR\_FLIP\_FENCE |       |
| 0x4008060F | In        | 8    | NVSCHED\_CTRL\_DETACH\_APPLICATION         |       |
| 0x40100610 | In        | 16   |                                            |       |
| 0x40100611 | In        | 16   |                                            |       |
|            |           |      |                                            |       |

## /dev/nverpt-ctrl

Added in firmware version 3.0.0.

| Value      | Direction | Size | Description | Notes |
| ---------- | --------- | ---- | ----------- | ----- |
| 0xC1280701 | Inout     | 296  |             |       |
| 0xCF580702 | Inout     | 3928 |             |       |
|            |           |      |             |       |

## /dev/nvhost-as-gpu

Each fd opened to this device creates an address space. An address space
is then later bound with a channel.

Once a nvgpu channel has been bound to an address space it cannot be
unbound. There is no support for allowing an nvgpu channel to change
from one address space to another (or from one to
none).

| Value      | Direction | Size     | Description                                                                       | Notes |
| ---------- | --------- | -------- | --------------------------------------------------------------------------------- | ----- |
| 0x40044101 | In        | 4        | [\#NVGPU\_AS\_IOCTL\_BIND\_CHANNEL](#NVGPU_AS_IOCTL_BIND_CHANNEL "wikilink")      |       |
| 0xC0184102 | Inout     | 24       | [\#NVGPU\_AS\_IOCTL\_ALLOC\_SPACE](#NVGPU_AS_IOCTL_ALLOC_SPACE "wikilink")        |       |
| 0xC0104103 | Inout     | 16       | [\#NVGPU\_AS\_IOCTL\_FREE\_SPACE](#NVGPU_AS_IOCTL_FREE_SPACE "wikilink")          |       |
| 0xC0184104 | Inout     | 24       | [\#NVGPU\_AS\_IOCTL\_MAP\_BUFFER](#NVGPU_AS_IOCTL_MAP_BUFFER "wikilink")          |       |
| 0xC0084105 | Inout     | 8        | [\#NVGPU\_AS\_IOCTL\_UNMAP\_BUFFER](#NVGPU_AS_IOCTL_UNMAP_BUFFER "wikilink")      |       |
| 0xC0284106 | Inout     | 40       | [\#NVGPU\_AS\_IOCTL\_MAP\_BUFFER\_EX](#NVGPU_AS_IOCTL_MAP_BUFFER_EX "wikilink")   |       |
| 0x40104107 | In        | 16       | [\#NVGPU\_AS\_IOCTL\_INITIALIZE](#NVGPU_AS_IOCTL_INITIALIZE "wikilink")           |       |
| 0xC0404108 | Inout     | 64       | [\#NVGPU\_AS\_IOCTL\_GET\_VA\_REGIONS](#NVGPU_AS_IOCTL_GET_VA_REGIONS "wikilink") |       |
| 0x40284109 | In        | 40       | [\#NVGPU\_AS\_IOCTL\_INITIALIZE\_EX](#NVGPU_AS_IOCTL_INITIALIZE_EX "wikilink")    |       |
| 0xC0??4114 | Inout     | Variable | [\#NVGPU\_AS\_IOCTL\_REMAP](#NVGPU_AS_IOCTL_REMAP "wikilink")                     |       |

### NVGPU\_AS\_IOCTL\_BIND\_CHANNEL

Identical to Linux driver.

` struct {`  
`   __in u32 fd;`  
` };`

### NVGPU\_AS\_IOCTL\_ALLOC\_SPACE

This one reserves pages in the device address space.

` struct {`  
`   __in u32 pages;`  
`   __in u32 page_size;`  
`   __in u32 flags;`  
`   u32      pad;`  
`   union {`  
`     __out u64 offset;`  
`     __in  u64 align;`  
`   };`  
` };`

### NVGPU\_AS\_IOCTL\_FREE\_SPACE

` struct {`  
`   __in u64 offset;`  
`   __in u32 pages;`  
`   __in u32 page_size;`  
` };`

### NVGPU\_AS\_IOCTL\_MAP\_BUFFER

Map a memory region in the device address space. Identical to Linux
driver pretty much.

On success, the mapped memory region is locked by having
[SVC\#MemoryState](SVC#MemoryState.md##MemoryState "wikilink") bit34
set.

` struct {`  
`   __in    u32 flags;        // bit0: fixed_offset, bit2: cacheable`  
`   u32         pad;`  
`   __in    u32 nvmap_handle;`  
`   __inout u32 page_size;    // 0 means don't care`  
`   union {`  
`     __out u64 offset;`  
`     __in  u64 align;`  
`   };`  
` };`

### NVGPU\_AS\_IOCTL\_MAP\_BUFFER\_EX

Map a memory region in the device address space. Identical to Linux
driver pretty much.

On success, the mapped memory region is locked by having
[SVC\#MemoryState](SVC#MemoryState.md##MemoryState "wikilink") bit34
set.

` struct {`  
`   __in    u32 flags;          // bit0: fixed_offset, bit2: cacheable`  
`   __in    u32 kind;           // -1 is default`  
`   __in    u32 nvmap_handle;`  
`   __inout u32 page_size;      // 0 means don't care`  
`   __in    u64 buffer_offset;`  
`   __in    u64 mapping_size;`  
`   __inout   u64 offset;`  
` };`

### NVGPU\_AS\_IOCTL\_UNMAP\_BUFFER

Unmap a memory region from the device address space.

`struct {`  
`   __in u64 offset;`  
` };`

### NVGPU\_AS\_IOCTL\_INITIALIZE

Nintendo's custom implementation of NVGPU\_GPU\_IOCTL\_ALLOC\_AS
(unavailable).

` struct {`  
`   __in u32 big_page_size;   // depends on GPU's available_big_page_sizes; 0=default`  
`   __in s32 as_fd;           // ignored; passes 0`  
`   __in u32 flags;           // ignored; passes 0`  
`   __in u32 reserved;        // ignored; passes 0`  
` };`

### NVGPU\_AS\_IOCTL\_GET\_VA\_REGIONS

Nintendo modified to get rid of pointer in
struct.

` struct va_region {`  
`   u64 offset;`  
`   u32 page_size;`  
`   u32 pad;`  
`   u64 pages;`  
` };`  
` `  
` struct {`  
`   u64         not_used;   // (contained output user ptr on linux, ignored)`  
`   __inout u32 bufsize;    // forced to 2*sizeof(struct va_region)`  
`   u32         pad;`  
`   __out struct va_region regions[2];`  
` };`

### NVGPU\_AS\_IOCTL\_INITIALIZE\_EX

Nintendo's custom implementation of NVGPU\_GPU\_IOCTL\_ALLOC\_AS
(unavailable) with extra
params.

` struct {`  
`   __in u32 big_page_size;   // depends on GPU's available_big_page_sizes; 0=default`  
`   __in s32 as_fd;           // ignored; passes 0`  
`   __in u32 flags;           // passes 0`  
`   __in u32 reserved;        // ignored; passes 0`  
`   __in u64 unk0;`  
`   __in u64 unk1;`  
`   __in u64 unk2;`  
` };`

### NVGPU\_AS\_IOCTL\_REMAP

Nintendo's custom implementation of address space remapping.

` struct remap_entry {`  
`   __in u16 flags;        // 0 or 4`  
`   __in u16 kind;           `  
`   __in u32 nvmap_handle;`  
`   __in u32 padding;`  
`   __in u32 offset;       // (alloc_space_offset >> 0x10)`  
`   __in u32 pages;        // alloc_space_pages`  
` };`  
  
`struct {`  
`   __in struct remap_entry entries[];`  
`};`

## /dev/nvhost-dbg-gpu

Returns [NotSupported](#Errors "wikilink") on Open unless
nn::settings::detail::GetDebugModeFlag is
set.

| Value      | Direction | Size     | Description                                            | Notes |
| ---------- | --------- | -------- | ------------------------------------------------------ | ----- |
| 0x40084401 | In        | 8        | NVGPU\_DBG\_GPU\_IOCTL\_BIND\_CHANNEL                  |       |
| 0xC0??4402 | Inout     | Variable | NVGPU\_DBG\_GPU\_IOCTL\_REG\_OPS                       |       |
| 0x40084403 | In        | 8        | NVGPU\_DBG\_GPU\_IOCTL\_EVENTS\_CTRL                   |       |
| 0x40044404 | In        | 4        | NVGPU\_DBG\_GPU\_IOCTL\_POWERGATE                      |       |
| 0x40044405 | In        | 4        | NVGPU\_DBG\_GPU\_IOCTL\_SMPC\_CTXSW\_MODE              |       |
| 0xC0184407 | Inout     | 24       | NVGPU\_DBG\_GPU\_IOCTL\_PERFBUF\_MAP                   |       |
| 0x40084408 | In        | 8        | NVGPU\_DBG\_GPU\_IOCTL\_PERFBUF\_UNMAP                 |       |
| 0x40084409 | In        | 8        | NVGPU\_DBG\_GPU\_IOCTL\_PC\_SAMPLING                   |       |
| 0x4008440A | In        | 8        | NVGPU\_DBG\_GPU\_IOCTL\_TIMEOUT                        |       |
| 0x8008440B | Out       | 8        | NVGPU\_DBG\_GPU\_IOCTL\_GET\_TIMEOUT                   |       |
| 0x8004440C | Out       | 4        | NVGPU\_DBG\_GPU\_IOCTL\_GET\_GR\_CONTEXT\_SIZE         |       |
| 0x0000440D | None      | 0        | NVGPU\_DBG\_GPU\_IOCTL\_GET\_GR\_CONTEXT (uses Ioctl3) |       |
|            |           |          |                                                        |       |

## /dev/nvhost-prof-gpu

Returns [NotSupported](#Errors "wikilink") on Open unless
nn::settings::detail::GetDebugModeFlag is set.

| Value | Direction | Size | Description | Notes |
| ----- | --------- | ---- | ----------- | ----- |

## /dev/nvhost-ctrl-gpu

This device is for global (context independent) operations on the
gpu.

| Value      | Direction | Size | Description                                                                                               | Notes |
| ---------- | --------- | ---- | --------------------------------------------------------------------------------------------------------- | ----- |
| 0x80044701 | Out       | 4    | [\#NVGPU\_GPU\_IOCTL\_ZCULL\_GET\_CTX\_SIZE](#NVGPU_GPU_IOCTL_ZCULL_GET_CTX_SIZE "wikilink")              |       |
| 0x80284702 | Out       | 40   | [\#NVGPU\_GPU\_IOCTL\_ZCULL\_GET\_INFO](#NVGPU_GPU_IOCTL_ZCULL_GET_INFO "wikilink")                       |       |
| 0x402C4703 | In        | 44   | [\#NVGPU\_GPU\_IOCTL\_ZBC\_SET\_TABLE](#NVGPU_GPU_IOCTL_ZBC_SET_TABLE "wikilink")                         |       |
| 0xC0344704 | Inout     | 52   | [\#NVGPU\_GPU\_IOCTL\_ZBC\_QUERY\_TABLE](#NVGPU_GPU_IOCTL_ZBC_QUERY_TABLE "wikilink")                     |       |
| 0xC0B04705 | Inout     | 176  | [\#NVGPU\_GPU\_IOCTL\_GET\_CHARACTERISTICS](#NVGPU_GPU_IOCTL_GET_CHARACTERISTICS "wikilink")              |       |
| 0xC0184706 | Inout     | 24   | NVGPU\_GPU\_IOCTL\_GET\_TPC\_MASKS                                                                        |       |
| 0x40084707 | In        | 8    | [\#NVGPU\_GPU\_IOCTL\_FLUSH\_L2](#NVGPU_GPU_IOCTL_FLUSH_L2 "wikilink")                                    |       |
| 0x4008470E | In        | 8    | NVGPU\_GPU\_IOCTL\_SET\_MMUDEBUG\_MODE                                                                    |       |
| 0x4010470F | In        | 16   | NVGPU\_GPU\_IOCTL\_SET\_SM\_DEBUG\_MODE                                                                   |       |
| 0xC0084710 | Inout     | 8    | NVGPU\_GPU\_IOCTL\_WAIT\_FOR\_PAUSE                                                                       |       |
| 0x80084711 | Out       | 8    | NVGPU\_GPU\_IOCTL\_GET\_TPC\_EXCEPTION\_EN\_STATUS                                                        |       |
| 0x80084712 | Out       | 8    | NVGPU\_GPU\_IOCTL\_NUM\_VSMS                                                                              |       |
| 0xC0044713 | Inout     | 4    | NVGPU\_GPU\_IOCTL\_VSMS\_MAPPING                                                                          |       |
| 0x80084714 | Out       | 8    | [\#NVGPU\_GPU\_IOCTL\_ZBC\_GET\_ACTIVE\_SLOT\_MASK](#NVGPU_GPU_IOCTL_ZBC_GET_ACTIVE_SLOT_MASK "wikilink") |       |
| 0x80044715 | Out       | 4    |                                                                                                           |       |
| 0x8018471A | Out       | 24   |                                                                                                           |       |
| 0xC008471B | Inout     | 8    | NVGPU\_GPU\_IOCTL\_GET\_ERROR\_CHANNEL\_USER\_DATA                                                        |       |
| 0xC010471C | Inout     | 16   | NVGPU\_GPU\_IOCTL\_GET\_GPU\_TIME                                                                         |       |
| 0xC108471D | Inout     | 264  | NVGPU\_GPU\_IOCTL\_GET\_CPU\_TIME\_CORRELATION\_INFO                                                      |       |

### NVGPU\_GPU\_IOCTL\_ZCULL\_GET\_CTX\_SIZE

Returns the GPU's ZCULL context size. Identical to Linux driver.

`struct {`  
`   __out u32 size;`  
` };`

### NVGPU\_GPU\_IOCTL\_ZCULL\_GET\_INFO

Returns GPU's ZCULL information. Identical to Linux driver.

`struct {`  
`   __out u32 width_align_pixels;`  
`   __out u32 height_align_pixels;`  
`   __out u32 pixel_squares_by_aliquots;`  
`   __out u32 aliquot_total;`  
`   __out u32 region_byte_multiplier;`  
`   __out u32 region_header_size;`  
`   __out u32 subregion_header_size;`  
`   __out u32 subregion_width_align_pixels;`  
`   __out u32 subregion_height_align_pixels;`  
`   __out u32 subregion_count;`  
` };`

### NVGPU\_GPU\_IOCTL\_ZBC\_SET\_TABLE

Sets the active ZBC table. Identical to Linux driver.

`struct {`  
`   __in u32 color_ds[4];`  
`   __in u32 color_l2[4];`  
`   __in u32 depth;`  
`   __in u32 format;`  
`   __in u32 type;         // 1=color, 2=depth`  
` };`

### NVGPU\_GPU\_IOCTL\_ZBC\_QUERY\_TABLE

Queries the active ZBC table. Identical to Linux driver.

`struct {`  
`   __out u32 color_ds[4];`  
`   __out u32 color_l2[4];`  
`   __out u32 depth;`  
`   __out u32 ref_cnt;`  
`   __out u32 format;`  
`   __out u32 type;`  
`   __inout u32 index_size;`  
` };`

### NVGPU\_GPU\_IOCTL\_GET\_CHARACTERISTICS

Returns the GPU characteristics. Modified to return inline data instead
of using a
pointer.

` struct gpu_characteristics {`  
`   u32 arch;                           // 0x120 (NVGPU_GPU_ARCH_GM200)`  
`   u32 impl;                           // 0xB (NVGPU_GPU_IMPL_GM20B)`  
`   u32 rev;                            // 0xA1 (Revision A1)`  
`   u32 num_gpc;                        // 0x1`  
`   u64 l2_cache_size;                  // 0x40000`  
`   u64 on_board_video_memory_size;     // 0x0 (not used)`  
`   u32 num_tpc_per_gpc;                // 0x2`  
`   u32 bus_type;                       // 0x20 (NVGPU_GPU_BUS_TYPE_AXI)`  
`   u32 big_page_size;                  // 0x20000`  
`   u32 compression_page_size;          // 0x20000`  
`   u32 pde_coverage_bit_count;         // 0x1B`  
`   u32 available_big_page_sizes;       // 0x30000`  
`   u32 gpc_mask;                       // 0x1`  
`   u32 sm_arch_sm_version;             // 0x503 (Maxwell Generation 5.0.3?)`  
`   u32 sm_arch_spa_version;            // 0x503 (Maxwell Generation 5.0.3?)`  
`   u32 sm_arch_warp_count;             // 0x80`  
`   u32 gpu_va_bit_count;               // 0x28`  
`   u32 reserved;                       // NULL`  
`   u64 flags;                          // 0x55`  
`   u32 twod_class;                     // 0x902D (FERMI_TWOD_A)`  
`   u32 threed_class;                   // 0xB197 (MAXWELL_B)`  
`   u32 compute_class;                  // 0xB1C0 (MAXWELL_COMPUTE_B)`  
`   u32 gpfifo_class;                   // 0xB06F (MAXWELL_CHANNEL_GPFIFO_A)`  
`   u32 inline_to_memory_class;         // 0xA140 (KEPLER_INLINE_TO_MEMORY_B)`  
`   u32 dma_copy_class;                 // 0xB0B5 (MAXWELL_DMA_COPY_A)`  
`   u32 max_fbps_count;                 // 0x1`  
`   u32 fbp_en_mask;                    // 0x0 (disabled)`  
`   u32 max_ltc_per_fbp;                // 0x2`  
`   u32 max_lts_per_ltc;                // 0x1`  
`   u32 max_tex_per_tpc;                // 0x0 (not supported)`  
`   u32 max_gpc_count;                  // 0x1`  
`   u32 rop_l2_en_mask_0;               // 0x21D70 (fuse_status_opt_rop_l2_fbp_r)`  
`   u32 rop_l2_en_mask_1;               // 0x0`  
`   u64 chipname;                       // 0x6230326D67 ("gm20b")`  
`   u64 gr_compbit_store_base_hw;       // 0x0 (not supported)`  
` };`  
  
` struct {`  
`   __inout u64 gpu_characteristics_buf_size;   // must not be NULL, but gets overwritten with 0xA0=max_size`  
`   __in    u64 gpu_characteristics_buf_addr;   // ignored, but must not be NULL`  
`   __out struct gpu_characteristics gc;`  
` };`

### NVGPU\_GPU\_IOCTL\_FLUSH\_L2

Flushes the GPU L2
cache.

` struct {`  
`   __in u32 flush;          // l2_flush | l2_invalidate << 1 | fb_flush << 2`  
`   u32      reserved;`  
` };`

### NVGPU\_GPU\_IOCTL\_ZBC\_GET\_ACTIVE\_SLOT\_MASK

Returns the mask value for a ZBC slot.

` struct {`  
`   __out u32 slot;       // always 0x07`  
`   __out u32 mask;`  
` };`

## Channels

Channels are a concept for NVIDIA hardware blocks that share a common
interface.

| Path              | Name                   |
| ----------------- | ---------------------- |
| /dev/nvhost-gpu   |                        |
| /dev/nvhost-vic   | Video Image Compositor |
| /dev/nvhost-nvdec | Video Decoder          |
| /dev/nvhost-nvjpg | JPEG Decoder           |

## Channel Ioctls

| Value      | Size     | Description                                                                                                 | Notes                                |
| ---------- | -------- | ----------------------------------------------------------------------------------------------------------- | ------------------------------------ |
| 0xC0??0001 | Variable | NVHOST\_IOCTL\_CHANNEL\_SUBMIT                                                                              |                                      |
| 0xC0080002 | 8        | NVHOST\_IOCTL\_CHANNEL\_GET\_SYNCPOINT                                                                      |                                      |
| 0xC0080003 | 8        | NVHOST\_IOCTL\_CHANNEL\_GET\_WAITBASE                                                                       |                                      |
| 0xC0080004 | 8        | NVHOST\_IOCTL\_CHANNEL\_SET\_TIMEOUT\_EX                                                                    |                                      |
| 0x40040007 | 4        |                                                                                                             |                                      |
| 0x40080008 | 8        | NVHOST\_IOCTL\_CHANNEL\_SET\_CLK\_RATE                                                                      |                                      |
| 0xC0??0009 | Variable | NVHOST\_IOCTL\_CHANNEL\_MAP\_BUFFER                                                                         |                                      |
| 0xC0??000A | Variable | NVHOST\_IOCTL\_CHANNEL\_UNMAP\_BUFFER                                                                       |                                      |
| 0x00000013 | 0        |                                                                                                             |                                      |
| 0x40044801 | 4        | [\#NVGPU\_IOCTL\_CHANNEL\_SET\_NVMAP\_FD](#NVGPU_IOCTL_CHANNEL_SET_NVMAP_FD "wikilink")                     |                                      |
| 0x40044803 | 4        | NVGPU\_IOCTL\_CHANNEL\_SET\_TIMEOUT                                                                         |                                      |
| 0x40084805 | 8        | [\#NVGPU\_IOCTL\_CHANNEL\_ALLOC\_GPFIFO](#NVGPU_IOCTL_CHANNEL_ALLOC_GPFIFO "wikilink")                      |                                      |
| 0xC0044807 | 4        | NVGPU\_IOCTL\_CHANNEL\_CYCLE\_STATS                                                                         |                                      |
| 0xC0??4808 | Variable | [\#NVGPU\_IOCTL\_CHANNEL\_SUBMIT\_GPFIFO](#NVGPU_IOCTL_CHANNEL_SUBMIT_GPFIFO "wikilink")                    |                                      |
| 0xC0104809 | 16       | [\#NVGPU\_IOCTL\_CHANNEL\_ALLOC\_OBJ\_CTX](#NVGPU_IOCTL_CHANNEL_ALLOC_OBJ_CTX "wikilink")                   |                                      |
| 0xC010480B | 16       | [\#NVGPU\_IOCTL\_CHANNEL\_ZCULL\_BIND](#NVGPU_IOCTL_CHANNEL_ZCULL_BIND "wikilink")                          |                                      |
| 0xC018480C | 24       | [\#NVGPU\_IOCTL\_CHANNEL\_SET\_ERROR\_NOTIFIER](#NVGPU_IOCTL_CHANNEL_SET_ERROR_NOTIFIER "wikilink")         |                                      |
| 0x4004480D | 4        | [\#NVGPU\_IOCTL\_CHANNEL\_SET\_PRIORITY](#NVGPU_IOCTL_CHANNEL_SET_PRIORITY "wikilink")                      |                                      |
| 0x0000480E | 0        | [\#NVGPU\_IOCTL\_CHANNEL\_ENABLE](#NVGPU_IOCTL_CHANNEL_ENABLE "wikilink")                                   |                                      |
| 0x0000480F | 0        | [\#NVGPU\_IOCTL\_CHANNEL\_DISABLE](#NVGPU_IOCTL_CHANNEL_DISABLE "wikilink")                                 |                                      |
| 0x00004810 | 0        | [\#NVGPU\_IOCTL\_CHANNEL\_PREEMPT](#NVGPU_IOCTL_CHANNEL_PREEMPT "wikilink")                                 |                                      |
| 0x00004811 | 0        | [\#NVGPU\_IOCTL\_CHANNEL\_FORCE\_RESET](#NVGPU_IOCTL_CHANNEL_FORCE_RESET "wikilink")                        |                                      |
| 0x40084812 | 8        | [\#NVGPU\_IOCTL\_CHANNEL\_EVENT\_ID\_CONTROL](#NVGPU_IOCTL_CHANNEL_EVENT_ID_CONTROL "wikilink")             |                                      |
| 0xC0104813 | 16       | NVGPU\_IOCTL\_CHANNEL\_CYCLE\_STATS\_SNAPSHOT                                                               |                                      |
| 0x80804816 | 128      | NVGPU\_IOCTL\_CHANNEL\_GET\_ERROR\_INFO                                                                     |                                      |
| 0xC0104817 | 16       | [\#NVGPU\_IOCTL\_CHANNEL\_GET\_ERROR\_NOTIFICATION](#NVGPU_IOCTL_CHANNEL_GET_ERROR_NOTIFICATION "wikilink") |                                      |
| 0x40204818 | 32       | [\#NVGPU\_IOCTL\_CHANNEL\_ALLOC\_GPFIFO\_EX](#NVGPU_IOCTL_CHANNEL_ALLOC_GPFIFO_EX "wikilink")               |                                      |
| 0xC0??4819 | Variable | [\#NVGPU\_IOCTL\_CHANNEL\_SUBMIT\_GPFIFO\_RETRY](#NVGPU_IOCTL_CHANNEL_SUBMIT_GPFIFO_RETRY "wikilink")       |                                      |
| 0xC020481A | 32       | [\#NVGPU\_IOCTL\_CHANNEL\_ALLOC\_GPFIFO\_EX2](#NVGPU_IOCTL_CHANNEL_ALLOC_GPFIFO_EX2 "wikilink")             |                                      |
| 0xC018481B | 24       | (uses Ioctl2)                                                                                               |                                      |
| 0xC018481C | 24       | (uses Ioctl2)                                                                                               |                                      |
|            |          |                                                                                                             |                                      |
| 0x40084714 | 8        | NVGPU\_IOCTL\_CHANNEL\_SET\_USER\_DATA                                                                      | Sets an unknown user context address |
| 0x80084715 | 8        | NVGPU\_IOCTL\_CHANNEL\_GET\_USER\_DATA                                                                      | Gets an unknown user context address |

### NVGPU\_IOCTL\_CHANNEL\_SET\_NVMAP\_FD

Binds a nvmap object to this channel. Identical to Linux driver.

This ioctl is a no-op in the Linux driver, not sure about Switch?

` struct {`  
`   __in u32 nvmap_fd;`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_ALLOC\_GPFIFO

Allocates gpfifo entries. Identical to Linux driver.

` struct {`  
`   __in u32 num_entries;`  
`   __in u32 flags;`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_SUBMIT\_GPFIFO

Submits a gpfifo object. Modified to take inline entry objects instead
of a
pointer.

` struct fence {`  
`   u32 id;`  
`   u32 value;`  
` };`  
` `  
` struct gpfifo_entry {`  
`   u32 entry0;                           // gpu_va_lo`  
`   u32 entry1;                           // gpu_va_hi | (unk_0x02 << 0x08) | (size << 0x0A) | (unk_0x01 << 0x1F)`  
` };`  
` `  
` struct {`  
`   __in u64 gpfifo;                      // (ignored) pointer to gpfifo fence structs`  
`   __in u32 num_entries;                 // number of fence objects being submitted`  
`   __in u32 flags;`  
`   __out struct fence fence_out;         // returned new fence object for others to wait on`  
`   __in  struct gpfifo_entry entries[];  // depends on num_entries`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_ALLOC\_OBJ\_CTX

Allocates a graphics context object. Modified to ignore object's ID.

You can only have one object context allocated at a time. You must have
bound an address space before using
this.

` struct {`  
`   __in  u32 class_num;    // 0x902D=2d, 0xB197=3d, 0xB1C0=compute, 0xA140=kepler, 0xB0B5=DMA, 0xB06F=channel_gpfifo`  
`   __in  u32 flags;`  
`   __out u64 obj_id;       // (ignored) used for FREE_OBJ_CTX ioctl, which is not supported`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_ZCULL\_BIND

Binds a ZCULL context to the channel. Identical to Linux
driver.

`struct {`  
`   __in u64 gpu_va;`  
`   __in u32 mode;         // 0=global, 1=no_ctxsw, 2=separate_buffer, 3=part_of_regular_buf`  
`   __in u32 padding;`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_SET\_ERROR\_NOTIFIER

Initializes the error notifier for this channel. Identical to Linux
driver.

` struct {`  
`   __in u64 offset;`  
`   __in u64 size;`  
`   __in u32 mem;       // nvmap object handle`  
`   __in u32 padding;`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_SET\_PRIORITY

Change channel's priority. Identical to Linux
driver.

` struct {`  
`   __in u32 priority;    // 0x32 is low, 0x64 is medium and 0x96 is high`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_ENABLE

Enables the current channel. Identical to Linux driver.

### NVGPU\_IOCTL\_CHANNEL\_DISABLE

Disables the current channel. Identical to Linux driver.

### NVGPU\_IOCTL\_CHANNEL\_PREEMPT

Clears the FIFO pipe for this channel. Identical to Linux driver.

### NVGPU\_IOCTL\_CHANNEL\_FORCE\_RESET

Forces the channel to reset. Identical to Linux driver.

### NVGPU\_IOCTL\_CHANNEL\_EVENT\_ID\_CONTROL

Controls event notifications.

` struct {`  
`   __in u32 cmd;    // 0=disable, 1=enable, 2=clear`  
`   __in u32 id;`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_GET\_ERROR\_NOTIFICATION

Returns the current error notification caught by the error notifier.
Exclusive to the Switch.

` struct {`  
`   __out   u64 timestamp;    // nanoseconds since Jan. 1, 1970`  
`   __out   u32 info32;       // error code`  
`   __out   u16 info16;       // additional error info`  
`   __inout u16 status;       // always 0xFFFF`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_SUBMIT\_GPFIFO\_RETRY

Allocates gpfifo entries with additional parameters. Exclusive to the
Switch.

` struct {`  
`   __in u32 num_entries;`  
`   __in u32 flags;`  
`   __in u32 unk0;            // 1 works`  
`   __in u32 unk1;`  
`   __in u32 unk2;`  
`   __in u32 unk3;`  
`   __in u32 unk4;`  
`   __in u32 unk5;`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_SUBMIT\_GPFIFO\_EX

Submits a gpfifo object (async version). Exclusive to the
Switch.

` struct {`  
`   u64 __gpfifo;                     // in (pointer to gpfifo fence structs; ignored)`  
`   u32 __num_entries;                // in (number of fence objects being submitted)`  
`   u32 __flags;                      // in`  
`   struct fence        __fence_out;  // out (returned new fence object for others to wait on)`  
`   struct gpfifo_entry __entries[];  // in (depends on __num_entries)`  
` };`

### NVGPU\_IOCTL\_CHANNEL\_ALLOC\_GPFIFO\_EX2

Allocates gpfifo entries with additional parameters and returns a fence.
Exclusive to the Switch.

` struct {`  
`   u32 __num_entries;         // in`  
`   u32 __flags;               // in`  
`   u32 __unk0;                // in (1 works)`  
`   struct fence __fence_out;  // out`  
`   u32 __unk1;                // in`  
`   u32 __unk2;                // in`  
`   u32 __unk3;                // in`  
` };`

# nvmemp

NVIDIA memory profiler (this service is not available on retail units).
/dev/nvhost-ctrl sends the ioctl NVHOST\_IOCTL\_CTRL\_GET\_CONFIG to
check the config "nv\!NV\_MEMORY\_PROFILER". If config\_str returns "1",
the applications attempts to talk to use nvmemp.

| Cmd | Name |
| --- | ---- |
| 0   | Cmd0 |
| 1   | Cmd1 |

# nvdrvdbg

This is "nns::nvdrv::INvDrvDebugFSServices".

| Cmd | Name                               |
| --- | ---------------------------------- |
| 0   | [\#OpenLog](#OpenLog "wikilink")   |
| 1   | [\#CloseLog](#CloseLog "wikilink") |
| 2   | [\#ReadLog](#ReadLog "wikilink")   |

## OpenLog

Takes process handle. Returns an fd.

## CloseLog

Takes fd and closes it.

## ReadLog

Takes fd and reads log into a type-6 buffer.

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
| 0x30004 | DirOperationFailed   |
| 0x3000F | IoctlFailed          |
| 0x30010 | AccessDenied         |
| 0x30013 | FileNotFound         |
| 0xA000E | ModuleNotPresent     |

# Panic

In some cases, a panic may occur. NV forces a crash by doing:

`(void *)0 = 0xCAFE;`

End result is that the system hangs with a white-screen.

## Gpfifo Panic

When the gpfifo data in the gpu\_va buffers specified by the submitted
gpfifo entries is invalid(?), eventually the user-process will be
force-terminated after using the submit-gpfifo ioctl. It's unknown how
exactly this is done.

[Category:Services](Category:Services "wikilink")

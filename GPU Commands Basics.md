## Mapping Memory

First, to map a memory region on the GPU Address Space, caching needs to
be disabled by using
[svcSetMemoryAttribute](SVC#svcSetMemoryAttribute.md##svcSetMemoryAttribute "wikilink").
The Address passed is the Virtual Address of the region that will be
mapped, the size is the region size, and State0/1 are both set to 8 to
disable caching of the memory region. This is done to ensure that the
GPU can actually "see" the data written there, and it doesn't get stuck
on some cache.

Then,
[NVMAP\_IOC\_CREATE](NV%20services#NVMAP%20IOC%20CREATE.md##NVMAP_IOC_CREATE "wikilink")
is used to create a nvmap object with the desired size. After,
[NVMAP\_IOC\_ALLOC](NV%20services#NVMAP%20IOC%20ALLOC.md##NVMAP_IOC_ALLOC "wikilink")
is used to allocate the memory on the GPU Address Space, and map data on
the process Address Space into the GPU Address Space, by passing the
Virtual Address as the input addr parameter, and also the Handle
returned from
[NVMAP\_IOC\_CREATE](NV%20services#NVMAP%20IOC%20CREATE.md##NVMAP_IOC_CREATE "wikilink").
Lastly, the actual mapping is done by using
[NVGPU\_AS\_IOCTL\_MAP\_BUFFER\_EX](NV%20services#NVGPU%20AS%20IOCTL%20MAP%20BUFFER%20EX.md##NVGPU_AS_IOCTL_MAP_BUFFER_EX "wikilink"),
and the GPU Virtual Address is returned on the offset parameter. It's
also possible to manually set the offset where the mapping should be
made on the GPU Address Space, by passing the address on the "offset"
parameter, and setting the bit 0 of the flags parameter to 1. However,
for this to work, the desired GPU Virtual Address needs to be previously
reserved using
[NVGPU\_AS\_IOCTL\_ALLOC\_SPACE](NV%20services#NVGPU%20AS%20IOCTL%20ALLOC%20SPACE.md##NVGPU_AS_IOCTL_ALLOC_SPACE "wikilink").

The above process is used to map all data that will be used by the GPU,
like Textures, Command Lists (a.k.a. Push Buffers), Vertex/Index buffers
and Shaders. They usually have their own mapping, but Command Lists can
share the same mapping.

## FIFO Commands

The GPU implements a variation of Tegra's push buffer format for it's
PFIFO engine. PFIFO is a special engine responsible for receiving user
command lists and routing them to the appropriate engines (2D, 3D, DMA).

Commands are submitted to the GPU's PFIFO engine through
[NVGPU\_IOCTL\_CHANNEL\_SUBMIT\_GPFIFO](NV%20services#NVGPU%20IOCTL%20CHANNEL%20SUBMIT%20GPFIFO.md##NVGPU_IOCTL_CHANNEL_SUBMIT_GPFIFO "wikilink").

This ioctl takes an array of gpfifo entries where each entry points to a
FIFO command list. This list is composed of alternating 32-bit words
containing FIFO commands and their respective arguments.

### Command Structure

| Bits  | Description                                                  |
| ----- | ------------------------------------------------------------ |
| 12-0  | Method                                                       |
| 15-13 | Subchannel                                                   |
| 28-16 | Argument count (in 32-bits Words) or inline data (see below) |
| 31-29 | [Submission mode](#Submission_mode "wikilink")               |

Note: Methods are treated as 4-byte addressable locations, and hence
their numbers are written down multiplied by 4.

Note: The command's arguments, when present, follow the command word
immediately.

#### Submission mode

| Mode | Description                                                                                                                                                                                                                      | Offical name |
| ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ |
| 0    | Increasing mode (old)                                                                                                                                                                                                            |              |
| 1    | Increasing mode - Tells PFIFO to read as much arguments as specified by **argument count**, while automatically incrementing the **method** value. This means that each argument will be written to a different method location. | INCR         |
| 2    | Non-increasing mode (old)                                                                                                                                                                                                        |              |
| 3    | Non-increasing mode - Tells PFIFO to read as much arguments as specified by **argument count**. However, all arguments will be written to the same method location.                                                              | NONINCR      |
| 4    | Inline mode - Tells PFIFO to read **inline data** from bits 28-16 of the command word, thus eliminating the need to pass additional words for the arguments.                                                                     | IMM          |
| 5    | Increase-once mode - Tells PFIFO to read as much arguments as specified by **argument count** and automatically increments the **method** value once only.                                                                       |              |

### Command List

All methods with values \< 0x100 are special and executed by the PFIFO's
DMA puller. The others are forwarded to the engine object currently
bound to a given
subchannel.

| Command    | Method | Subchannel | Arg Count | Mode | Name                                 |
| ---------- | ------ | ---------- | --------- | ---- | ------------------------------------ |
| 0x2001?000 | 0x0000 | Variable   | 1         | 1    | [BindObject](#BindObject "wikilink") |
| 0xA0020E00 | 0x3800 | 0          | 2         | 5    | BeginTransformFeedback               |
| 0xA0030E30 | 0x38C0 | 0          | 3         | 5    | DrawArrays                           |
| 0xA0050E36 | 0x38D8 | 0          | 5         | 5    | DrawElements                         |
| 0xA0020E2E | 0x38B8 | 0          | 2         | 5    | PopDebugGroupId                      |
| 0xA0040E2C | 0x38B0 | 0          | 4         | 5    | PushDebugGroup                       |
| 0x2001054C | 0x1530 | 0          | 1         | 1    | ResetCounter                         |
| 0x8001047F | 0x11FC | 0          | 1         | 4    | ResolveDepthBuffer                   |
| 0x200104C4 | 0x1310 | 0          | 1         | 1    | SetAlphaRef                          |
| 0x200404C7 | 0x131C | 0          | 4         | 1    | SetBlendColor                        |
| 0x2001064F | 0x1BD0 | 0          | 1         | 1    | SetDepthClamp                        |
| 0x200200CD | 0x0334 | 0          | 2         | 1    | SetInnerTessellationLevels           |
| 0x200204EC | 0x13B0 | 0          | 2         | 1    | SetLineWidth                         |
| 0x200400C9 | 0x0324 | 0          | 4         | 1    | SetOuterTessellationLevels           |
| 0x8???0373 | 0x0DCC | 0          | Variable  | 4    | SetPatchSize                         |
| 0x20010546 | 0x1518 | 0          | 1         | 1    | SetPointSize                         |
| 0x20030554 | 0x1550 | 0          | 3         | 1    | SetRenderEnableConditional           |
| 0x200403EF | 0x0FBC | 0          | 4         | 1    | SetSampleMask                        |
| 0x200103D9 | 0x0F64 | 0          | 1         | 1    | SetTiledCacheTileSize                |
| 0x20020047 | 0x011C | 0          | 2         | 1    | SetGraphMacroEntry                   |
| 0xA???0045 | 0x0114 | 0          | Variable  | 5    | SetGraphMacroCode                    |

Note: These still need to be heavily verified and *could* be wrong.

### BindObject

In order to bind an engine object to a specific subchannel, method 0
(BindObject) must be used first. The target subchannel is specified in
bits 15-13 of the command word.

After the engine object is bound to the desired subchannel, setting it's
value in bits 15-13 of any subsequent command word will make PFIFO
forward the command to the target engine.

This method only takes one argument, an [engine
ID](#Engine_IDs "wikilink").

#### Engine IDs

| ID     | Engine                        |
| ------ | ----------------------------- |
| 0x902D | FERMI\_TWOD\_A (2D)           |
| 0xB197 | MAXWELL\_B (3D)               |
| 0xB1C0 | MAXWELL\_COMPUTE\_B           |
| 0xA140 | KEPLER\_INLINE\_TO\_MEMORY\_B |
| 0xB0B5 | MAXWELL\_DMA\_COPY\_A (DMA)   |

### Fences

Command lists can contain fences to ensure that commands are executed on
the correct order, and subsequent commands are only sent when the
previously sent commands were already processed by the GPU. Fences uses
the QUERY\_\* commands, and works like this:

  - First, QUERY\_ADDRESS\_HIGH and QUERY\_ADDRESS\_LOW commands are
    added to the Command List, with the High/Low 32 bits part of the
    64-bits GPU Virtual Address where the fence is located. This GPU
    Virtual Address needs to be mapped to the process Virtual Address
    beforehand.
  - Then, QUERY\_SEQUENCE is added with a sequential number. This number
    is basically a incrementing counter, so the first Command List can
    have QUERY\_SEQUENCE = 1, the next one QUERY\_SEQUENCE = 2, 3, 4...
    and so on.
  - Finally, QUERY\_GET is added and contains the mode and other unknown
    data.

The above commands are added using the [increasing
mode](#Submission_mode "wikilink"), since the Ids for all those 4
registers are sequential.

#### QUERY\_GET Structure

| Bits  | Description |
| ----- | ----------- |
| 1-0   | Mode        |
| 4     | Fence       |
| 15-12 | Unit        |

#### QUERY\_GET Mode

| Value | Mode    |
| ----- | ------- |
| 0     | Write   |
| 1     | Sync    |
| 2     | Write ? |
| 3     | Write ? |

TODO: Move this to a separate page with all GPU Commands with
descriptions. Also figure out what the other values mean.

Some of the other fields are still unknown/unobserved.

Official games will set Mode to 0, Fence to 1 and Unit to 0xF. The
QUERY\_SEQUENCE value is then written by the GPU to the address pointed
to by QUERY\_ADDRESS. On the CPU side, the game code should wait until
the value at the address pointed to by QUERY\_ADDRESS is \>= to the last
written SEQUENCE value. Official code waits for this condition to be
true on a loop, and won't send any further commands before that.

## Vertex Data Submission

Note: This is a observation on how the game Puyo Puyo Tetris sends
textured squares to the GPU.

1.  VERTEX\_ATTRIB\_FORMAT (0-15) are set (only the first 3 are really
    used, the rest are set float, with Size = 1 and offset at 0).
2.  VERTEX\_ARRAY\_FETCH (0) is set with the lower 12 bits set to 0x1c
    (Stride) and bit 12 to 1 (Enabled).
3.  VERTEX\_ARRAY\_START\_HIGH/LOW (0) are set to the GPU Virtual
    Address where the Vertex Data is located.
4.  VERTEX\_ARRAY\_LIMIT\_HIGH/LOW (0) are set to the GPU Virtual
    Address where the Vertex Data is located, plus the Vertex Data size
    in bytes minus 1.
5.  VERTEX\_BEGIN\_GL is used with the primitive type set to
    TRIANGLE\_STRIP.
6.  VERTEX\_BUFFER\_FIRST with value 0 (indicating the index of the
    first primitive to render?).
7.  VERTEX\_BUFFER\_COUNT is set to 4, because the Vertex Buffer with
    the square has 4 vertices.
8.  VERTEX\_END\_GL is used with value 0 (currently unknown what this
    value means).

## References

FIFO engine overview:
[1](https://envytools.readthedocs.io/en/latest/hw/fifo/intro.html)

Method values from the Fermi family GPU (a bit older than the Tegra X1,
but values seems to be mostly the same):
[2](https://github.com/envytools/envytools/blob/master/rnndb/graph/gf100_3d.xml)

Values for some types used on the above XML:
[3](https://github.com/envytools/envytools/blob/master/rnndb/graph/nv_3ddefs.xml)

Command word packing code used on Mesa3d:
[4](https://cgit.freedesktop.org/mesa/mesa/tree/src/gallium/drivers/nouveau/nvc0/nvc0_winsys.h)

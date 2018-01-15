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
virtual address as the input addr parameter, and also the Handle
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

The above process is used to map all data that needs to be sent to the
GPU, like Textures, Command Lists (a.k.a. Push Buffers), Vertex/Index
buffers and Shaders. They usually have their own mapping, but Command
Lists can share the same mapping.

## Commands Submission

Commands are sent to the GPU through
[NVGPU\_IOCTL\_CHANNEL\_SUBMIT\_GPFIFO](NV%20services#NVGPU%20IOCTL%20CHANNEL%20SUBMIT%20GPFIFO.md##NVGPU_IOCTL_CHANNEL_SUBMIT_GPFIFO "wikilink").
This IoCtl command accepts various GpFifo entries, and each GpFifo entry
points to a Command List. The GPU Command List is composed of 32-bits
words, which usually are Command/Argument
pairs.

#### Command Word Structure

| Bits  | Description                                                   |
| ----- | ------------------------------------------------------------- |
| 12-0  | Command/Register Id                                           |
| 15-13 | Sub Channel                                                   |
| 28-16 | Arguments Count (in 32-bits Words) or Inline Data (see below) |
| 31-29 | Mode                                                          |

#### Command Mode

| Mode | Description                                                                                                                                                               |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1    | Sequential Mode - Reads "Argument Count" arguments, while automatically incrementing the Register Id. So, each argument is written to a different register.               |
| 3    | Normal Mode - This is a Command with multiple arguments. Reads "Argument Count" arguments, all belonging to the same Command.                                             |
| 4    | Inline Mode - Bits 16:28 of the Command Word (where Inline Data is located) contains the Value of the argument written to the register. The next Word is another Command. |
| 5    | Unobserved, but is valid too.                                                                                                                                             |

TODO: Find a better name for the "Normal Mode" and figure out what mode
5 is.

Ohter mode values are unobserved.

Note: All Commands/Register Id values are multiples of 4, so they are
divided by 4 when packing, and multiplied by 4 when unpacking.

## Sub Channel binding

All Command Id values \< 0x100 are special and aren't fowarded to the
engines. The command 0 is used to bind engines to Sub Channels, and
needs to be used before commands are submited to the engines.

The command 0 only has one argument, the Engine Id.

#### Engine Ids

| Id     | Engine  |
| ------ | ------- |
| 0x902d | 2D      |
| 0xb197 | 3D      |
| 0xb1c0 | Compute |
| 0xa140 | Kepler  |
| 0xb0b5 | DMA     |

The bits 15-13 of the Command Word contains the Sub Channel index that
should be bound.

After binding the required Sub Channels, then the respective values can
be used on the "Sub Channel" field of the Command Word to talk with the
respective Engines.

## Fences

Command Lists can contain fences to ensure that commands are executed on
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
QUERY\_SEQUENCE value is then written to the address pointed to by
QUERY\_ADDRESS. On the CPU side, the game code should wait until the
value at the address pointed to by QUERY\_ADDRESS is \>= to the last
written SEQUENCE value. Official code waits for this condition to be
true on a loop, and won't send any further commands before that.

## Vertex Data Submission

Note: This is a observation on how the game Puyo Puyo Tetris sends
textured squares to the GPU.

1.  VERTEX\_ATTRIB\_FORMAT (0-15) are set (only the first 3 are really
    used, the rest are set float, with Size = 1 and offset at 0).
2.  VERTEX\_ARRAY\_FETCH (0) is set with the lower 12 bits set to 0x1c
    (Stride) and bit 12 to 1 (Enabled).
3.  VERTEX\_ARRAY\_START\_HIGH/LOW are set to the GPU Virtual Address
    where the Vertex Data is located.
4.  VERTEX\_ARRAY\_LIMIT\_HIGH/LOW are set to the GPU Virtual Address
    where the Vertex Data is located, plus the Vertex Data size in bytes
    minus 1.
5.  VERTEX\_BEGIN\_GL is used with the primitive type set to
    TRIANGLE\_STRIP.
6.  VERTEX\_BUFFER\_FIRST with value 0 (indicating the index of the
    first primitive to render?).
7.  VERTEX\_BUFFER\_COUNT is set to 4, because the Vertex Buffer with
    the square has 4 vertices.
8.  VERTEX\_END\_GL is used with value 0 (currently unknown what this
    value means).

## References

Check out those pages for more useful data.

Register Id values from the Fermi family GPU (a bit older than the Tegra
X1, but values seems to be mostly the same):
[1](https://github.com/envytools/envytools/blob/master/rnndb/graph/gf100_3d.xml)

Values for some types used on the above XML:
[2](https://github.com/envytools/envytools/blob/master/rnndb/graph/nv_3ddefs.xml)

Command Word packing code used on Mesa3d:
[3](https://cgit.freedesktop.org/mesa/mesa/tree/src/gallium/drivers/nouveau/nvc0/nvc0_winsys.h)

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

See the [GPU](GPU.md "wikilink") page for a list of commands, with the
register addresses and their descriptions.

### Command Structure

| Bits  | Description                                                  |
| ----- | ------------------------------------------------------------ |
| 12-0  | Method                                                       |
| 15-13 | Subchannel                                                   |
| 27-16 | Argument count (in 32-bits Words) or inline data (see below) |
| 28?   | Hmm?                                                         |
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

### SetObject

In order to bind an engine object to a specific subchannel, method 0
(SetObject) must be used first. The target subchannel is specified in
bits 15-13 of the command word.

After the engine object is bound to the desired subchannel, setting it's
value in bits 15-13 of any subsequent command word will make PFIFO
forward the command to the target engine.

This method only takes one argument, an [Engine
ID](#Engine_IDs "wikilink").

#### Engine IDs

| ID     | Engine                        |
| ------ | ----------------------------- |
| 0x902D | FERMI\_TWOD\_A (2D)           |
| 0xB197 | MAXWELL\_B (3D)               |
| 0xB1C0 | MAXWELL\_COMPUTE\_B           |
| 0xA140 | KEPLER\_INLINE\_TO\_MEMORY\_B |
| 0xB0B5 | MAXWELL\_DMA\_COPY\_A (DMA)   |

### Macro

Macros are small programs that can be uploaded to the gpu and are
capable of reading and writing to the 3D engine registers on the GPU.
The macros also accepts parameters, stored on a FIFO. Macros can be
called using methods starting at 0xe00, where the first method triggers
the macro execution, and the second one is used to push parameters to
the FIFO, that can be read from the macro program using a instruction
called *parm*. This instruction pops the FIFO and reads the next
parameter, while also allowing programs to use a variable number of
parameters if desired.

The first parameter is written to 0xe00 + n \* 2 (where n is the macro
index), and all subsequent parameters should be pushed to the FIFO using
0xe01 + n \* 2. The first parameter is placed at the general purpose
register R1 in the macro program when execution starts.

Official games uses those macros to conditionally write registers, one
example of such uses is the macro at 0xe24, that is used to set shader
registers (including shader address and binding the c1 Constant Buffer
to the shader). In some cases, it's also used to set registers
unconditionally.

### Fences

Command lists can contain fences to ensure that commands are executed on
the correct order, and subsequent commands are only sent when the
previously sent commands were already processed by the GPU. Fences uses
the QUERY\_\* commands, and works like this:

  - First, register ReportSemaphoreOffset is set to High/Low 32 bits
    part of the 64-bits GPU Virtual Address where the fence is located.
    This GPU Virtual Address needs to be mapped to the process Virtual
    Address beforehand.
  - Then, ReportSemaphorePayload is set with a sequential number. This
    number is basically a incrementing counter, so the first Command
    List can set ReportSemaphorePayload = 1, the next one to 2, then 3,
    4... and so on.
  - Finally, ReportSemaphoreControl is added and contains the mode and
    other unknown data.

The above commands are added using the [increasing
mode](#Submission_mode "wikilink"), since all those 4 registers are
sequential.

Official games will sets Operation to 0 (Release), bit 4 to 1, bits
15-12 (Unit) to 0xF, and bit 28 to 1 (OneWord). The
ReportSemaphorePayload value is then written by the GPU to the address
pointed to by ReportSemaphoreOffset. On the CPU side, the game code
should wait until the value at the address pointed to by
ReportSemaphoreOffset is \>= to the last written value. Official code
waits for this condition to be true on a loop, and won't send any
further commands before that.

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

## Texture View

Texture information such as address, format and size is sent to the GPU
through a structure know as Texture View (a.k.a. Texture Image Control,
or TIC). Each texture that the game uses needs a separate TIC, and those
TICs are written to a table, one after the other. Each [TIC
entry](#TIC_Structure "wikilink") has 0x20 bytes, and is composed of 8
32-bits words where the texture information is packed.

The index of the TIC entries that should be used by the shader is sent
to the GPU with the CB\_POS/CB\_DATA (0) methods. Games usually follows
the following steps to write the TIC entry indexes:

  - Macro 0xe1a is used to set CB\_ADDRESS\_HIGH/LOW registers to the
    GPU Virtual Address of the Constant Buffer set on the register 0x982
    (the *Texture Constant Buffer* index register), and also sets
    CB\_SIZE.
  - CB\_POS is used to set the write offset of the Constant Buffer to n
    \* 4, where *n* is the index of the *Handle* being used on the
    shader program (this index starts at 8, so CB\_POS should be at
    least 8 \* 4 = 0x20).
  - CB\_DATA (0) method is used to write the value into the Constant
    Buffer. The value is a *Handle* where the lower 20 bits is the TIC
    index, and the higher 12 bits is the TSC (Texture Sampler Control)
    index.

The address of a given TIC entry can be calculates as:

`tic_entry_address = tic_base_address + tic_index * 0x20`

Where *tic\_base\_address* is the address written to
TIC\_ADDRESS\_HIGH/LOW (methods 0x1574 and 0x1578), *tic\_index* is the
lower 20 bits of the word written into the Const Buffer with CB\_DATA
(0), and 0x20 is the size of each TIC entry in bytes.

The texture is accessed on the shader using one of the texture sampling
instructions (usually the TEXS instruction). One of the parameters for
this instruction is the *Handle* index. This index start at 8, so the
index 8 will access the handle at 8 \* 4 = 0x20 on the *Texture Constant
Buffer*. Each shader stage has a separate Constant Buffer, so for
fragment shaders, this is located at CB\_ADDRESS + 4 \* CB\_SIZE +
TEXS\_index \* 4 (where the first 4 is the index of the fragment shader
stage, and the second 4 is the size of a word, 4
bytes).

### TIC Structure

| Word | Bits  | Description                                                                                |
| ---- | ----- | ------------------------------------------------------------------------------------------ |
| 0    | 6-0   | [Texture Format](GPU%20Texture%20Formats#Texture%20Formats.md##Texture_Formats "wikilink") |
| 0    | 9-7   | [R Channel Data Type](#Channel_Data_Type "wikilink")                                       |
| 0    | 12-10 | [G Channel Data Type](#Channel_Data_Type "wikilink")                                       |
| 0    | 15-13 | [B Channel Data Type](#Channel_Data_Type "wikilink")                                       |
| 0    | 18-16 | [A Channel Data Type](#Channel_Data_Type "wikilink")                                       |
| 1    | 31-0  | Lower 32-bits of the Texture GPU Virtual Address                                           |
| 2    | 15-0  | Higher 16-bits of the Texture GPU Virtual Address                                          |
| 4    | 15-0  | Texture Width minus 1                                                                      |
| 5    | 15-0  | Texture Height minus 1                                                                     |

#### Channel Data Type

| Value | Type               |
| ----- | ------------------ |
| 1     | SNORM              |
| 2     | UNORM              |
| 3     | SINT               |
| 4     | UINT               |
| 5     | SNORM\_FORCE\_FP16 |
| 6     | UNORM\_FORCE\_FP16 |
| 7     | FLOAT              |

## References

FIFO engine overview:
[1](https://envytools.readthedocs.io/en/latest/hw/fifo/intro.html)

Method values from the Fermi family GPU (a bit older than the Tegra X1,
but values seems to be mostly the same):
[2](https://github.com/envytools/envytools/blob/master/rnndb/graph/gf100_3d.xml)

TIC structure used on a Maxwell GPU:
[3](https://github.com/envytools/envytools/blob/master/rnndb/graph/gm200_texture.xml)

Values for some types used on the above XML:
[4](https://github.com/envytools/envytools/blob/master/rnndb/graph/nv_3ddefs.xml)

Command word packing code used on Mesa3d:
[5](https://cgit.freedesktop.org/mesa/mesa/tree/src/gallium/drivers/nouveau/nvc0/nvc0_winsys.h)

TIC entry pack/write code used on Mesa3d:
[6](https://cgit.freedesktop.org/mesa/mesa/tree/src/gallium/drivers/nouveau/nvc0/nvc0_tex.c#n65)

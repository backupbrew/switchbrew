NSO is the main executable format.

It starts with the "NSO" header and mainly describes .text, .rodata, and
.data segments (like a short-form of ELF program
headers):

# NSO Header

| Offset | Size      | Description                                                                                         |
| ------ | --------- | --------------------------------------------------------------------------------------------------- |
| 0x0    | 4         | Magic "NSO0"                                                                                        |
| 0x4    | 4         |                                                                                                     |
| 0x8    | 4         |                                                                                                     |
| 0xC    | 4         | Flags, bit 0-2: section is compressed, bit 4-6: check section hash when loading                     |
| 0x10   | 0x10 \* 3 | SegmentHeader\[3\]                                                                                  |
| 0x40   | 0x20      | Value of "build id" from ELF's GNU .note section. Contains variable sized digest, up to 32bytes.    |
| 0x60   | 0x4 \* 3  | CompressedSize\[3\]                                                                                 |
| 0x6c   | 0x24      | Padding                                                                                             |
| 0x90   | 8         | .rodata-relative extents of .dynstr                                                                 |
| 0x98   | 8         | .rodata-relative extents of .dynsym                                                                 |
| 0xA0   | 0x20 \* 3 | SHA256 hashes over the decompressed sections using the above byte-sizes: .text, .rodata, and .data. |
| 0x100  |           | Compressed sections                                                                                 |

Most data in Switch binaries are standard ELF structures, however some
are custom. For example, the MOD header is essentially a replacement for
a PT\_DYNAMIC program header.

## SegmentHeader

| Offset | Size | Description               |
| ------ | ---- | ------------------------- |
| 0x0    | 4    | FileOffset                |
| 0x4    | 4    | MemoryOffset              |
| 0x8    | 4    | DecompressedSize          |
| 0xC    | 4    | UnkOffset/UnkSize/BssSize |

## .rodata-relative extent

| Offset | Size | Description        |
| ------ | ---- | ------------------ |
| 0x0    | 4    | RegionRoDataOffset |
| 0x4    | 4    | RegionSize         |

## MOD

All offsets are signed 32bit values relative to the magic field. The
32bits at image base + 4 must point to the magic field. The MOD
structure is designed such that it can be placed at image base and point
to itself. The 2 fields preceding the magic field get copied around with
the structure, even if it is relocated to somewhere besides the image
base. If MOD is not located at image base, the value at offset 4 must
still point to the MOD magic. In the case of .text being at image base,
this implies that the first instruction can only be an unconditional
branch over the offset
literal.

| Offset | Size | Description                                                              |
| ------ | ---- | ------------------------------------------------------------------------ |
| 0x00   | 4    | ZeroPadding                                                              |
| 0x04   | 4    | MagicOffset. Always 8 (so it works when MOD is at image\_base + 0).      |
| 0x08   | 4    | Magic "MOD0"                                                             |
| 0x0C   | 4    | .dynamic offset                                                          |
| 0x10   | 4    | .bss start offset                                                        |
| 0x14   | 4    | .bss end offset                                                          |
| 0x18   | 4    | .eh\_frame\_hdr start offset                                             |
| 0x1C   | 4    | .eh\_frame\_hdr end offset                                               |
| 0x20   | 4    | offset to runtime-generated module object. typically equal to .bss base. |

# Arguments

Loader maps memory and writes the
[arguments](Loader%20services#AddProcessToLaunchQueue.md##AddProcessToLaunchQueue "wikilink")
to {end of rwdata section specified by last SegmentHeader}. Official
processes use argdata\_addr = {page-aligned \_end}. svcQueryMemory is
used by official sw to verify that argdata\_addr is mapped RW, since
this memory is only mapped when arguments are specified via that
command. Afterwards, official sw aligns the argdata\_addr to 4-bytes.
Structure located at
argdata\_addr:

| Offset | Size      | Description                                                                                                                            |
| ------ | --------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x4       | This is the total allocated space relative to argdata\_addr, used for calculating the max size of the argv ptr array. Normally 0x9000? |
| 0x4    | 0x4       | This is the total\_bytesize of the actual argdata string.                                                                              |
| 0x8    | 0x18      | Unused by official sw.                                                                                                                 |
| 0x20   | See above | Actual argdata string.                                                                                                                 |

  - The copy of the args used with the argv array is written by official
    processes to actual\_argdata\_string+actual\_argdata\_size.
  - argv\_ptrarray written by official processes is at
    (args\_copy+actual\_argdata\_size) + 0x9 & ~0x7.

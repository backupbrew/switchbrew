NRO is the executable format for non-[ExeFS](ExeFS.md "wikilink")
binaries.

It starts with the NRO-start structure then the "NRO" header and mainly
describes .text, .rodata, and .data segments (like a short-form of ELF
program headers):

# NRO Start

| Offset | Size | Description                      |
| ------ | ---- | -------------------------------- |
| 0x0    | 0x4  | Unused                           |
| 0x4    | 0x4  | [MOD0](NSO.md "wikilink") offset |
| 0x8    | 0x8  | Padding                          |

# NRO Header

| Offset | Size     | Description                                                                                      |
| ------ | -------- | ------------------------------------------------------------------------------------------------ |
| 0x0    | 4        | Magic "NRO0"                                                                                     |
| 0x4    | 4        | ?                                                                                                |
| 0x8    | 4        | Total NRO filesize                                                                               |
| 0xC    | 4        | ?                                                                                                |
| 0x10   | 0x8 \* 3 | SegmentHeader\[3\]                                                                               |
| 0x28   | 0x4      | bssSize                                                                                          |
| 0x2C   | 0x4      | ?                                                                                                |
| 0x30   | 0x20     | Value of "build id" from ELF's GNU .note section. Contains variable sized digest, up to 32bytes. |
| 0x50   | 0x10     | Padding                                                                                          |
| 0x60   | 0x10     | ?                                                                                                |

## SegmentHeader

| Offset | Size | Description |
| ------ | ---- | ----------- |
| 0x0    | 4    | FileOffset  |
| 0x4    | 4    | Size        |

[Category:File formats](Category:File_formats "wikilink")

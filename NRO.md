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
| 0x0    | 0x4      | Magic "NRO0"                                                                                     |
| 0x4    | 0x4      | NRO Format Version (Always 0)                                                                    |
| 0x8    | 4        | size (Total NRO filesize)                                                                        |
| 0xC    | 0x4      | Flags (Unused)                                                                                   |
| 0x10   | 0x8 \* 3 | SegmentHeader\[3\]                                                                               |
| 0x28   | 0x4      | bssSize                                                                                          |
| 0x2C   | 0x4      | Reserved (Unused)                                                                                |
| 0x30   | 0x20     | Value of "build id" from ELF's GNU .note section. Contains variable sized digest, up to 32bytes. |
| 0x50   | 0x10     | Padding                                                                                          |
| 0x60   | 0x10     | ?                                                                                                |

## SegmentHeader

| Offset | Size | Description |
| ------ | ---- | ----------- |
| 0x0    | 0x4  | FileOffset  |
| 0x4    | 0x4  | Size        |

# Assets

This is an optional custom assets section for homebrew, this is located
at file offset {NroHeader.size}. See also
[switch-tools](https://github.com/switchbrew/switch-tools) for
implementation.

The below offsets are relative to the beginning of the assets section
(AssetHeader).

## AssetHeader

| Offset | Size | Description                                                                                    |
| ------ | ---- | ---------------------------------------------------------------------------------------------- |
| 0x0    | 0x4  | Magic "ASET"                                                                                   |
| 0x4    | 0x4  | Format version, currently 0.                                                                   |
| 0x8    | 0x10 | AssetSection icon. Used by the Homebrew Launcher. Like official icons, this is a 256x256 JPEG. |
| 0x18   | 0x10 | AssetSection [nacp](Control.nacp.md "wikilink"). Used by the Homebrew Launcher.                |
| 0x28   | 0x10 | AssetSection romfs. Can be used by the application.                                            |
|        |      |                                                                                                |

## AssetSection

| Offset | Size | Description                              |
| ------ | ---- | ---------------------------------------- |
| 0x0    | 0x8  | Offset                                   |
| 0x8    | 0x8  | Size, 0 indicates this section is empty. |

[Category:File formats](Category:File_formats "wikilink")

# Metadata file

This is the file that ends in `".cnmt{.nca}"` or `"meta0.ncd"`.

It starts with a
header:

| Offset | Size | Description                                                                                     |
| ------ | ---- | ----------------------------------------------------------------------------------------------- |
| 0x0    | 8    | Title ID                                                                                        |
| 0x8    | 4    |                                                                                                 |
| 0xC    | 1    | Type (see [Title Types](Content%20Manager%20services#Title%20Types.md##Title_Types "wikilink")) |
| 0xD    | 1    |                                                                                                 |
| 0xE    | 2    | Offset to table relative to the end of this 0x20-byte header.                                   |
| 0x10   | 2    | Number of entries                                                                               |
| 0x12   | 14   |                                                                                                 |

An optional header can follow, depending on the title type.

## Application header

| Offset | Size | Description    |
| ------ | ---- | -------------- |
| 0x20   | 8    | Patch title ID |
| 0x28   | 8    |                |

## Patch header

| Offset | Size | Description       |
| ------ | ---- | ----------------- |
| 0x20   | 8    | Original title ID |
| 0x28   | 8    |                   |

## Add-on content header

| Offset | Size | Description          |
| ------ | ---- | -------------------- |
| 0x20   | 8    | Application title ID |
| 0x28   | 8    |                      |

## Content records

Each entry is 0x38
bytes:

| Offset | Size | Description                                                                                                                                              |
| ------ | ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 32   | Hash                                                                                                                                                     |
| 0x20   | 16   | NcaId \[same as first 16-bytes of hash\]                                                                                                                 |
| 0x30   | 6    | Size                                                                                                                                                     |
| 0x36   | 1    | Type (0=meta, 1=program, 2=data, 3=control, 4=offline-manual [html](Internet%20Browser.md "wikilink"), 5=legal [html](Internet%20Browser.md "wikilink")) |
| 0x37   | 1    |                                                                                                                                                          |

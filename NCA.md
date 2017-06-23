# Metadata file

This is the file that ends in `".cnmt.nca"` or `"meta0.ncd"`.

It starts with an
header:

| Offset | Size | Description                                                                                     |
| ------ | ---- | ----------------------------------------------------------------------------------------------- |
| 0x0    | 8    | Patch title id                                                                                  |
| 0x8    | 4    |                                                                                                 |
| 0xC    | 1    | Type (see [Title Types](Content%20Manager%20services#Title%20Types.md##Title_Types "wikilink")) |
| 0xD    | 1    |                                                                                                 |
| 0xE    | 2    | Offset to table                                                                                 |
| 0x10   | 2    | Number of entries                                                                               |
| 0x12   | 14   |                                                                                                 |
| 0x20   | 16   | Original title-id                                                                               |

Each entry is 0x38
bytes:

| Offset | Size | Description                                                  |
| ------ | ---- | ------------------------------------------------------------ |
| 0x0    | 32   | Hash                                                         |
| 0x20   | 16   | NcaId \[same as first 16-bytes of hash\]                     |
| 0x30   | 6    | Size                                                         |
| 0x36   | 1    | Type (0=meta, 1=program, 2=data, 3=control, 4=html, 5=legal) |
| 0x37   | 1    |                                                              |

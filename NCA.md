# Metadata file

This is the file that ends in `".cnmt.nca"` or `"meta0.ncd"`.

It starts with an
header:

| Offset | Size | Description                                                                                     |
| ------ | ---- | ----------------------------------------------------------------------------------------------- |
| 0x0    | 8    | Title id?                                                                                       |
| 0x8    | 4    |                                                                                                 |
| 0xC    | 1    | Type (see [Title Types](Content%20Manager%20services#Title%20Types.md##Title_Types "wikilink")) |
| 0xD    | 1    |                                                                                                 |
| 0xE    | 2    | Offset to table                                                                                 |
| 0x10   | 2    | Number of entries                                                                               |

Each entry is 0x38 bytes:

| Offset | Size | Description                                  |
| ------ | ---- | -------------------------------------------- |
| 0x0    | 32   |                                              |
| 0x20   | 16   | NcaId                                        |
| 0x30   | 6    |                                              |
| 0x36   | 1    | Type (1=program, 3=control, 4=html, 5=legal) |
| 0x37   | 1    |                                              |

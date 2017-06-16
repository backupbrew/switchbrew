This is the format on the files stored on
[SD](SD%20Filesystem.md "wikilink"), unknown if this is used elsewhere.

The data between this header and offset 0x4000 is unused/uninitialized
it appears. The actual content which is encrypted, starts at offset
0x4000 with the size from the header.

When a title is redownloaded/reinstalled, the header and raw content in
NAX0 are completely different except for the magicnum and size-field.

| Offset | Size | Description                                 |
| ------ | ---- | ------------------------------------------- |
| 0x0    | 0x20 | Data appears to be random.                  |
| 0x20   | 0x8  | Magicnum "NAX0"                             |
| 0x28   | 0x20 | Data appears to be random.                  |
| 0x48   | 0x8? | Size of the file relative to offset 0x4000. |

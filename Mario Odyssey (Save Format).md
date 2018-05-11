The save file format for Super Mario Odyssey is in BYAML. The only
difference is the presence of a 16-byte
header

| Offset | Size | Description                                                              |
| ------ | ---- | ------------------------------------------------------------------------ |
| 0x0    | 0x4  | Unknown                                                                  |
| 0x4    | 0x4  | Unknown (seems to always be \`01 00 00 00\`)                             |
| 0x8    | 0x4  | File size (little endian)                                                |
| 0xC    | 0x4  | Unknown (possibly null-terminated? The final byte is seemingly always 0) |
|        |      |                                                                          |

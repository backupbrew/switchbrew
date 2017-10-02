# INI1

| Offset | Type | Description     |
| ------ | ---- | --------------- |
| 0x0    | u32  | Magic "INI1"    |
| 0x4    | u32  | Size            |
| 0x8    | u32  | NumberProcesses |
| 0xC    | u32  | Zero            |

## KIP1

Kernel internal
process?

| Offset | Type                                              | Description  |
| ------ | ------------------------------------------------- | ------------ |
| 0x0    | u32                                               | Magic "KIP1" |
| 0x4    | char\[12\]                                        | Name         |
| 0x10   | u64                                               | TitleId      |
| 0x18   | u32                                               |              |
| 0x1C   | u32                                               |              |
| 0x20   | [\#SectionHeader](#SectionHeader "wikilink")\[3\] | Sections     |
| 0x50   | char\[0x20\]                                      | Padding      |
| 0x70   | u64\[0x20\]                                       | KernelCaps   |

### SectionHeader

| Offset | Type | Description      |
| ------ | ---- | ---------------- |
| 0x0    | u32  | OutOffset        |
| 0x4    | u32  | DecompressedSize |
| 0x8    | u32  | CompressedSize   |
| 0xC    | u32  |                  |

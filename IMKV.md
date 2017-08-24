This is the format for Key Value databases ("imkvdb.arc") found in FS
and NCM savedata archives.

# Archive

| Offset | Size     | Description            |
| ------ | -------- | ---------------------- |
| 0x0    | 0x4      | "IMKV" magic           |
| 0x4    | 0x4      | Reserved? Usually zero |
| 0x8    | 0x4      | Number of entries      |
| 0xC    | Variable | Entries                |

# Entry Format

| Offset         | Size       | Description  |
| -------------- | ---------- | ------------ |
| 0x0            | 0x4        | "IMEN" magic |
| 0x4            | 0x4        | Key size     |
| 0x8            | 0x4        | Value Size   |
| 0xC            | Key Size   | Key          |
| 0xC + Key Size | Value Size | Value        |
|                |            |              |

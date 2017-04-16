# Structure

These have been redesigned from the 3DS so that they fit within a
Aarch64 MOV instruction immediate most of the time (without requiring
the additional MOVK).

| Bits | Field       |
| ---- | ----------- |
| 8-0  | Module      |
| 21-9 | Description |

# Modules

| Value | Name       |
| ----- | ---------- |
| 1     | Kernel     |
| 2     | FS         |
| 9     | RO service |
| 10    | IPC        |
| 11    | IPC        |
| 16    | NS         |
| 21    | SM         |
| 22    | RO user    |
| 124   | Account    |
| 126   | Mii        |
| 203   | HID        |

# Error codes

| Value   | Description | Description                                                   |
| ------- | ----------- | ------------------------------------------------------------- |
| 0xCA01  | 101         | Invalid size (not page-aligned).                              |
| 0xCC01  | 102         | Invalid address (not page-aligned).                           |
| 0xD201  | 105         | Handle-table full.                                            |
| 0xD401  | 106         | Invalid memory state.                                         |
| 0xD801  | 108         | When trying to set executable permission on memory.           |
| 0xE401  | 114         | Invalid handle.                                               |
| 0xE601  | 115         | Syscall copy from user failed.                                |
| 0xEA01  | 117         | Time out? When you give 0 handles to svcWaitSynchronizationN. |
| 0xEE01  | 119         | When you give too many handles to svcWaitSynchronizationN.    |
| 0xFA01  | 125         | Wrong memory permission?                                      |
| 0x10601 | 131         | Port max sessions exceeded                                    |
| 0x7D402 | 1002        | Title-id not found                                            |
| 0x6609  | 51          | Invalid memory state/permission                               |
| 0x6A09  | 53          | Invalid Nrr                                                   |
| 0xA209  | 81          | Unaligned Nrr address                                         |
| 0xA409  | 82          | Bad Nrr size                                                  |
| 0xAA09  | 85          | Bad Nrr address                                               |
| 0x1A80A | 212         | Bad magic (expected 'SFCO')                                   |
| 0x20B   | 1           | Size too big to fit to marshal.                               |
| 0x11A0B | 141         | Went past maximum during marshalling.                         |
| 0x0C15  | 6           | Invalid name (all zeroes)                                     |
| 0x1015  | 8           | Permission denied                                             |
| 0x816   | 4           | Bad Nro magic                                                 |
| 0xC16   | 6           | Bad Nrr magic                                                 |

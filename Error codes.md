# Structure

These have been redesigned from the 3DS so that they fit within a
Aarch64 MOV instruction immediate most of the time (without requiring
the additional MOVK).

| Bits | Field       |
| ---- | ----------- |
| 8-0  | Module      |
| 21-9 | Description |

When a fatal-error is received the error code is outputted using the
following formatter:

` %04d-%04x`

.. where the first code is `2000 + Module`, and the other being
`Description`. Bits \>=22 from the error-code are unused when displaying
fatal-errors, since the Description ends with bit21.

# Modules

| Value | Name                         |
| ----- | ---------------------------- |
| 1     | Kernel                       |
| 2     | FS                           |
| 3     | NVIDIA                       |
| 5     | GameCard                     |
| 9     | RO service                   |
| 10    | CMIF (IPC command interface) |
| 11    | HIPC (IPC)                   |
| 15    | PM                           |
| 16    | NS                           |
| 21    | SM                           |
| 22    | RO userland                  |
| 110   | NIFM                         |
| 114   | Display                      |
| 124   | Account                      |
| 126   | Mii                          |
| 129   | Play Report                  |
| 162   | Userland assert              |
| 168   | Userland crash               |
| 203   | HID                          |

# Error codes

| Value    | Description | Description                                                                                                           |
| -------- | ----------- | --------------------------------------------------------------------------------------------------------------------- |
| 0xCA01   | 101         | Unaligned size                                                                                                        |
| 0xCC01   | 102         | Invalid address (not page-aligned).                                                                                   |
| 0xCE01   | 103         | Address is NULL                                                                                                       |
| 0xD201   | 105         | Handle-table full.                                                                                                    |
| 0xD401   | 106         | Invalid memory state.                                                                                                 |
| 0xD801   | 108         | When trying to set executable permission on memory.                                                                   |
| 0xDC01   | 110         | Stack address outside allowed range                                                                                   |
| 0xE001   | 112         | Invalid thread priority.                                                                                              |
| 0xE201   | 113         | Invalid processor id.                                                                                                 |
| 0xE401   | 114         | Invalid handle.                                                                                                       |
| 0xE601   | 115         | Syscall copy from user failed.                                                                                        |
| 0xE801   | 116         | ID1 outside valid range in svcGetInfo.                                                                                |
| 0xEA01   | 117         | Time out? When you give 0 handles to svcWaitSynchronizationN.                                                         |
| 0xEE01   | 119         | When you give too many handles to svcWaitSynchronizationN.                                                            |
| 0xF001   | 120         | ID0 outside valid range in svcGetInfo.                                                                                |
| 0xF201   | 121         | No such port                                                                                                          |
| 0xF801   | 124         | Unhandled usermode exception                                                                                          |
| 0xFA01   | 125         | Wrong memory permission?                                                                                              |
| 0x10601  | 131         | Port max sessions exceeded                                                                                            |
| 0x10801  | 132         | Out of memory                                                                                                         |
| 0x7D402  | 1002        | Title-id not found                                                                                                    |
| 0x13B002 | 2520        | Gamecard not inserted                                                                                                 |
| 0x171402 | 2954        | Invalid gamecard handle.                                                                                              |
| 0x1A4A02 | 3365        | Out of memory                                                                                                         |
| 0x196002 | 3248        | Out of memory                                                                                                         |
| 0x196202 | 3249        | Out of memory                                                                                                         |
| 0x2EE202 | 6001        | Unknown media-id                                                                                                      |
| 0x2EE602 | 6003        | Path too long                                                                                                         |
| 0x2F5A02 | 6061        | Offset outside storage                                                                                                |
| 0x313802 | 6300        | Operation not supported                                                                                               |
| 0x320002 | 6400        | Permission denied                                                                                                     |
| 0x3EE03  | 503         | Invalid memory mirror                                                                                                 |
| 0xDC05   | 110         | Gamecard not inserted                                                                                                 |
| 0x6609   | 51          | Invalid memory state/permission                                                                                       |
| 0x6A09   | 53          | Invalid NRR                                                                                                           |
| 0xA209   | 81          | Unaligned NRR address                                                                                                 |
| 0xA409   | 82          | Bad NRR size                                                                                                          |
| 0xAA09   | 85          | Bad NRR address                                                                                                       |
| 0x1A80A  | 212         | Bad magic (expected 'SFCO')                                                                                           |
| 0x20B    | 1           | Size too big to fit to marshal.                                                                                       |
| 0x11A0B  | 141         | Went past maximum during marshalling.                                                                                 |
| 0x1900B  | 200         | IPC Query 0 failed.                                                                                                   |
| 0x25A0B  | 301         | Remote process is dead                                                                                                |
| 0x3D60B  | 491         | IPC Query 1 failed.                                                                                                   |
| 0x20F    | 1           | Pid not found                                                                                                         |
| 0x410    | 2           | Can be returned by NS when the input u64 wasn't found in a table.                                                     |
| 0xA05    | 5           | Returned when attempting to mount titles which exist that aren't \*8XX titles, the same way \*8XX titles are mounted. |
| 0x0C15   | 6           | Invalid name (all zeroes)                                                                                             |
| 0x1015   | 8           | Permission denied                                                                                                     |
| 0x816    | 4           | Bad NRO magic                                                                                                         |
| 0xC16    | 6           | Bad NRR magic                                                                                                         |
| 0x287C   | 20          | Argument is NULL                                                                                                      |
| 0x2C7C   | 22          | Argument is invalid                                                                                                   |
| 0x3C7C   | 30          | Bad input buffer size                                                                                                 |
| 0x407C   | 32          | Invalid input buffer                                                                                                  |

# Fatal Errors

| Error     | Description                                                                                                                                                                                        |
| --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2162-0002 | Can be triggered by running [svcBreak](SVC.md "wikilink"). The svcBreak params have no affect on the value of the thrown error-code.                                                               |
| 2168-0000 | Userland ARM undefined instruction exception                                                                                                                                                       |
| 2168-0001 | Userland ARM prefetch-abort due to PC set to non-executable region                                                                                                                                 |
| 2168-0002 | Userland ARM data abort. Also caused by abnormal process termination via [svcExitProcess](SVC.md "wikilink"). Note: directly jumping to nnMain()-retaddr from non-main-thread has the same result. |
| 2168-0003 | Userland PC address not aligned to 4 bytes                                                                                                                                                         |

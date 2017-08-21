This is the 0x200-byte thread-local-storage, the base address is loaded
via ARM threadid register
tpidrro\_el0.

## Structure

| Offset | Size  | Description                                           |
| ------ | ----- | ----------------------------------------------------- |
| 0x0    | 0x100 | [IPC](IPC%20Marshalling.md "wikilink") command buffer |
| 0x100  | 0xF8  | ?                                                     |
| 0x1F8  | 0x8   | Address of threadctx+0x58.                            |

## Userland context

This is the structure of the 0x228-byte threadctx used by official
userland
software.

| Offset | Size  | Description                                                           |
| ------ | ----- | --------------------------------------------------------------------- |
| 0x0    | 0xA8  | ?                                                                     |
| 0xA8   | 0x8   | Address of the stack-bottom-mirror which the thread was created with. |
| 0xB0   | 0x8   | Size of the stack.                                                    |
| 0xB8   | 0x178 | ?                                                                     |

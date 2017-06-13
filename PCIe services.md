# pcie

| Cmd | Name                                   |
| --- | -------------------------------------- |
| 0   | [\#Initialize](#Initialize "wikilink") |

## Initialize

Takes the current process handle (0xFFFF8001).

Returns an event handle and session handle to a
[\#IPCIESubinterface](#IPCIESubinterface "wikilink").

## IPCIESubinterface

| Cmd | Name | Notes                                         |
| --- | ---- | --------------------------------------------- |
| 0   |      | Takes a type-6 buffer. Returns all zeroes.    |
| 1   |      | Always returns 0x1278?                        |
| 2   |      | Always returns 0x1278?                        |
| 3   |      | Takes a type-6 buffer. Always returns 0x1278? |

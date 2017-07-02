# gpio

| Cmd | Name                                                   |
| --- | ------------------------------------------------------ |
| 0   | OpenSessionForDev                                      |
| 1   | [\#OpenSession](#OpenSession "wikilink")               |
| 2   | [\#OpenSessionForTest](#OpenSessionForTest "wikilink") |
| 3   | IsWakeEventActive                                      |
| 4   | GetWakeEventActiveFlagSet                              |
| 5   | SetWakeEventActiveFlagSetForDebug                      |
| 6   |                                                        |

## OpenSession

Same thing as OpenSessionForDev except the descriptor is looked up in a
table:

| Input id | GpioPadName |
| -------- | ----------- |
| 2        | 0x24        |
| 4        | 0xDA        |
| 5        | 0xDB        |
| 6        | 0xDC        |
| 7        | 0x25        |
| 8        | 0x90        |
| 9        | 0x91        |
| ..       | ..          |

## OpenSessionForTest

Same as [\#OpenSession](#OpenSession "wikilink") but panics on failure.

## GpioPadName

| Bits | Description      |
| ---- | ---------------- |
| 7-5  | Controller index |
| 4-3  | Port index       |
| 2-0  | Pin number       |

# i2c

| Cmd | Name | Notes                                   |
| --- | ---- | --------------------------------------- |
| 0   |      | Black screen hang.                      |
| 1   |      | Takes a word. Returns a session handle. |
| 2   |      | Returns a u8/bool.                      |
| 3   |      | Black screen hang.                      |

# i2c:pcv

# uart

| Cmd | Name | Notes                                                                                    |
| --- | ---- | ---------------------------------------------------------------------------------------- |
| 0   |      | Returns a u8/bool.                                                                       |
| 1   |      | Returns a u8/bool.                                                                       |
| 2   |      | Returns a u8/bool.                                                                       |
| 3   |      | Returns a u8/bool.                                                                       |
| 4   |      | Takes marshalled arguments.                                                              |
| 5   |      | Takes marshalled arguments.                                                              |
| 6   |      | Returns a handle to an IPC session [\#IUartSubinterface](#IUartSubinterface "wikilink"). |

## IUartSubinterface

| Cmd | Name | Notes                      |
| --- | ---- | -------------------------- |
| 0   |      | Takes marshalled arguments |
| 1   |      | Takes marshalled arguments |
| 2   |      |                            |
| 3   |      | Takes marshalled arguments |
| 4   |      | Returns 2x u64. Both zero. |

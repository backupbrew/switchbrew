# gpio

| Cmd | Name                                                   |
| --- | ------------------------------------------------------ |
| 0   | [\#OpenSessionForDev](#OpenSessionForDev "wikilink")   |
| 1   | [\#OpenSession](#OpenSession "wikilink")               |
| 2   | [\#OpenSessionForTest](#OpenSessionForTest "wikilink") |
| 3   | IsWakeEventActive                                      |
| 4   | GetWakeEventActiveFlagSet                              |
| 5   | SetWakeEventActiveFlagSetForDebug                      |
| 6   |                                                        |

## OpenSessionForDev

Takes a raw GpioPadDescriptor and returns a
[\#IPadSession](#IPadSession "wikilink") session for it.

## OpenSession

Same thing as OpenSessionForDev except the descriptor is looked up in
the table below. Returns an [\#IPadSession](#IPadSession "wikilink")
session.

| GpioPadName | GpioPadDescriptor |
| ----------- | ----------------- |
| 2           | 0x24              |
| 4           | 0xDA              |
| 5           | 0xDB              |
| 6           | 0xDC              |
| 7           | 0x25              |
| 8           | 0x90              |
| 9           | 0x91              |
| ..          | ..                |

## OpenSessionForTest

Same as [\#OpenSession](#OpenSession "wikilink") but panics on failure.

## IPadSession

| Cmd | Name                 |
| --- | -------------------- |
| 0   | SetDirection         |
| 1   | GetDirection         |
| 2   | SetInterruptMode     |
| 3   | GetInterruptMode     |
| 4   | SetInterruptEnable   |
| 5   | GetInterruptEnable   |
| 6   | GetInterruptStatus   |
| 7   | ClearInterruptStatus |
| 8   | SetValue             |
| 9   | GetValue             |
| 10  | BindInterrupt        |
| 11  | UnbindInterrupt      |
| 12  | SetDebounceEnabled   |
| 13  | GetDebounceEnabled   |
| 14  | SetDebounceTime      |
| 15  | GetDebounceTime      |

## GpioPadDescriptor

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

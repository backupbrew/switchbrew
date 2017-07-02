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

| GpioPadName | GpioPadDescriptor | Description |
| ----------- | ----------------- | ----------- |
| 1           | 0xCC              |             |
| 2           | 0x24              |             |
| 4           | 0xDA              |             |
| 5           | 0xDB              |             |
| 6           | 0xDC              |             |
| 7           | 0x25              |             |
| 8           | 0x90              |             |
| 9           | 0x91              |             |
| 0xA         | 0x96              |             |
| 0xB         | 0x97              |             |
| 0xD         | 6                 |             |
| 0xE         | 0x78              |             |
| 0xF         | 0x93              |             |
| 0x10        | 0x7D              |             |
| 0x11        | 0x7C              |             |
| 0x12        | 0x7B              |             |
| 0x13        | 0x7A              |             |
| 0x14        | 0xBC              |             |
| 0x15        | 0xAE              |             |
| 0x17        | 0xB9              |             |
| 0x18        | 0xBD              |             |
| 0x19        | 0xBE              | Volume key  |
| 0x1A        | 0xBF              | Volume key  |
| 0x1B        | 0xC0              |             |
| 0x1C        | 0xC1              |             |
| 0x1D        | 0xA9              |             |
| 0x1E        | 0xAA              |             |
| 0x20        | 0xAD              |             |
| 0x21        | 0xC8              |             |
| 0x22        | 0xCA              |             |
| 0x23        | 0xCB              |             |
| 0x24        | 0x4F              |             |
| 0x25        | 0x50              |             |
| 0x26        | 0x51              |             |
| 0x27        | 0x52              |             |
| 0x28        | 0x54              |             |
| 0x29        | 0x56              |             |
| 0x2A        | 0x57              |             |
| ..          | ..                |             |

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

# gpio

This is "nn::gpio::IManager".

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

| GpioPadName | GpioPadDescriptor | Tegra (port, pin) | Usage                          | Direction | Used by                                                    |
| ----------- | ----------------- | ----------------- | ------------------------------ | --------- | ---------------------------------------------------------- |
| 1           | 0xCC              | Z, 4              |                                |           |                                                            |
| 2           | 0x24              | E, 4              | SDCard Power                   | Out       | [Filesystem services](Filesystem%20services.md "wikilink") |
| 4           | 0xDA              | BB, 2             |                                |           |                                                            |
| 5           | 0xDB              | BB, 3             | GcAsic Power?                  | Out       | [Filesystem services](Filesystem%20services.md "wikilink") |
| 6           | 0xDC              | BB, 4             |                                |           |                                                            |
| 7           | 0x25              | E, 5              |                                |           |                                                            |
| 8           | 0x90              | S, 0              |                                | In        | [HID services](HID%20services.md "wikilink")               |
| 9           | 0x91              | S, 1              |                                |           |                                                            |
| 0xA         | 0x96              | S, 6              | Power supply monitor related.  | 1         | [PTM services](PTM%20services.md "wikilink")               |
| 0xB         | 0x97              | S, 7              |                                |           |                                                            |
| 0xD         | 6                 | A, 6              | Battery event monitor related. | 1         | [PTM services](PTM%20services.md "wikilink")               |
| 0xE         | 0x78              | P, 0              |                                |           |                                                            |
| 0xF         | 0x93              | S, 3              | GcAsic Irq?                    | In        | [Filesystem services](Filesystem%20services.md "wikilink") |
| 0x10        | 0x7D              | P, 5              |                                |           |                                                            |
| 0x11        | 0x7C              | P, 4              |                                |           |                                                            |
| 0x12        | 0x7B              | P, 3              |                                |           |                                                            |
| 0x13        | 0x7A              | P, 2              |                                |           |                                                            |
| 0x14        | 0xBC              | X, 4              |                                |           |                                                            |
| 0x15        | 0xAE              | V, 6              |                                |           |                                                            |
| 0x17        | 0xB9              | X, 1              |                                | In        | [HID services](HID%20services.md "wikilink")               |
| 0x18        | 0xBD              | X, 5              |                                | Out       | [HID services](HID%20services.md "wikilink")               |
| 0x19        | 0xBE              | X, 6              | Volume key                     | In        | [Boot2](Boot2.md "wikilink")                               |
| 0x1A        | 0xBF              | X, 7              | Volume key                     | In        | [Boot2](Boot2.md "wikilink")                               |
| 0x1B        | 0xC0              | Y, 0              | Power supply monitor related.  | 0         | [PTM services](PTM%20services.md "wikilink")               |
| 0x1C        | 0xC1              | Y, 1              |                                |           |                                                            |
| 0x1D        | 0xA9              | V, 1              |                                |           |                                                            |
| 0x1E        | 0xAA              | V, 2              |                                |           |                                                            |
| 0x1F        | 0x55              |                   | Charger watchdog related.      | 1         | [PTM services](PTM%20services.md "wikilink")               |
| 0x20        | 0xAD              | V, 5              |                                |           |                                                            |
| 0x21        | 0xC8              | Z, 0              | Power supply monitor related.  | 0         | [PTM services](PTM%20services.md "wikilink")               |
| 0x22        | 0xCA              | Z, 2              |                                |           |                                                            |
| 0x23        | 0xCB              | Z, 3              |                                |           |                                                            |
| 0x24        | 0x4F              | J, 7              |                                |           |                                                            |
| 0x25        | 0x50              | K, 0              |                                |           |                                                            |
| 0x26        | 0x51              | K, 1              |                                |           |                                                            |
| 0x27        | 0x52              | K, 2              |                                |           |                                                            |
| 0x28        | 0x54              | K, 4              |                                |           |                                                            |
| 0x29        | 0x56              | K, 6              |                                |           |                                                            |
| 0x2A        | 0x57              | K, 7              |                                |           |                                                            |
| 0x2B        | 0x53              | K, 3              |                                |           |                                                            |
| 0x2C        | 0xE3              | CC, 3             |                                |           |                                                            |
| 0x2D        | 0x38              | H, 0              |                                |           |                                                            |
| 0x2E        | 0x39              | H, 1              |                                |           |                                                            |
| 0x2F        | 0x3B              | H, 3              |                                |           |                                                            |
| 0x30        | 0x3D              | H, 5              |                                |           |                                                            |
| 0x31        | 0x3F              | H, 7              |                                |           |                                                            |
| 0x32        | 0x40              | I, 0              |                                |           |                                                            |
| 0x33        | 0x41              | I, 1              |                                |           |                                                            |
| 0x34        | 0x3E              | H, 6              |                                |           |                                                            |
| 0x35        | 0xE2              | CC, 2             |                                |           |                                                            |
| 0x36        | 0xE4              | CC, 4             | Battery event monitor related. | 1         | [PTM services](PTM%20services.md "wikilink")               |
| 0x37        | 0x3A              | H, 2              |                                |           |                                                            |
| 0x38        | 0xC9              | Z, 1              | SDCard Card Detect             | In        | [Filesystem services](Filesystem%20services.md "wikilink") |
| 0x39        | 0x4D              | J, 5              | Charger watchdog related.      | 1         | [PTM services](PTM%20services.md "wikilink")               |
| 0x3A        | 0x58              | L, 0              | Charger watchdog related.      | 1         | [PTM services](PTM%20services.md "wikilink")               |
| 0x3B        | 0x3E              | H, 6              |                                |           |                                                            |
| 0x3C        | 0x26              | E, 6              |                                |           |                                                            |
| 0x3D        | \-1               |                   |                                |           |                                                            |
| 0x3E        | 0x33              | G, 3              |                                |           |                                                            |
| 0x3F        | 0x1C              | D, 4              |                                |           |                                                            |
| 0x40        | 0xD9              | BB, 1             |                                |           |                                                            |
| 0x41        | 0x0C              | B, 4              |                                |           |                                                            |
| 0x42        | 0x0D              | B, 5              |                                |           |                                                            |
| 0x43        | 0x21              | E, 1              |                                |           |                                                            |
| 0x44        | 0x27              | E, 7              |                                |           |                                                            |
| 0x45        | 0x92              | S, 2              |                                |           |                                                            |
| 0x46        | 0x95              | S, 5              |                                |           |                                                            |
| 0x47        | 0x98              | T, 0              |                                |           |                                                            |
| 0x48        | 0x10              | C, 0              |                                |           |                                                            |
| 0x49        | 0x11              | C, 1              |                                |           |                                                            |
| 0x4A        | 0x12              | C, 2              |                                |           |                                                            |
| 0x4B        | 0x42              | I, 2              |                                |           |                                                            |
| 0x4C        | 0xE6              | CC, 6             |                                |           |                                                            |

## OpenSessionForTest

Same as [\#OpenSession](#OpenSession "wikilink") but panics on failure.

## IPadSession

This is "nn::gpio::IPadSession".

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

This is "nn::i2c::IManager".

| Cmd | Name              |
| --- | ----------------- |
| 0   | OpenSessionForDev |
| 1   | OpenSession       |
| 2   | HasDevice         |
| 3   | HasDeviceForDev   |

## II2cSession

This is "nn::i2c::ISession".

| Cmd | Name               |
| --- | ------------------ |
| 0   |                    |
| 1   |                    |
| 2   |                    |
| 3   | Send               |
| 4   | Receive            |
| 5   | ExecuteCommandList |

# i2c:pcv

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |
| 10  |      |
| 11  |      |
| 12  |      |

# uart

This is "nn::uart::IManager".

| Cmd | Name            | Notes                       |
| --- | --------------- | --------------------------- |
| 0   |                 | Returns a u8/bool.          |
| 1   |                 | Returns a u8/bool.          |
| 2   |                 | Returns a u8/bool.          |
| 3   |                 | Returns a u8/bool.          |
| 4   |                 | Takes marshalled arguments. |
| 5   |                 | Takes marshalled arguments. |
| 6   | GetIPortSession |                             |
| 7   |                 |                             |
| 8   |                 |                             |
|     |                 |                             |

## IPortSession

This is "nn::uart::IPortSession".

| Cmd | Name | Notes                      |
| --- | ---- | -------------------------- |
| 0   |      | Takes marshalled arguments |
| 1   |      | Takes marshalled arguments |
| 2   |      |                            |
| 3   |      | Takes marshalled arguments |
| 4   |      | Returns 2x u64. Both zero. |
| 5   |      |                            |
| 6   |      |                            |
| 7   |      |                            |
|     |      |                            |

# pwm

This is "nn::pwm::IManager".

| Cmd | Name              |
| --- | ----------------- |
| 0   | OpenSessionForDev |
| 1   | OpenSession       |

## IChannelSession

This is "nn::pwm::IChannelSession".

| Cmd | Name       |
| --- | ---------- |
| 0   | SetPeriod  |
| 1   | GetPeriod  |
| 2   | SetDuty    |
| 3   | GetDuty    |
| 4   | SetEnabled |
| 5   | GetEnabled |

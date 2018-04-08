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
| 6   | SetWakePinDebugMode                                    |
| 7   | \[5.0.0+\] [\#OpenSession2](#OpenSession2 "wikilink")  |
| 8   | \[5.0.0+\] IsWakeEventActive2                          |
| 9   | \[5.0.0+\] SetWakeEventActiveFlagSetForDebug2          |

## OpenSessionForDev

Takes a raw GpioPadDescriptor and returns a
[\#IPadSession](#IPadSession "wikilink") session for it.

## OpenSession

Same thing as OpenSessionForDev except the descriptor is looked up in
the table below. Returns an [\#IPadSession](#IPadSession "wikilink")
session.

| GpioPadName | GpioPadDescriptor | Tegra (port, pin) | Usage                                                       | Direction | Used by                                                                                              |
| ----------- | ----------------- | ----------------- | ----------------------------------------------------------- | --------- | ---------------------------------------------------------------------------------------------------- |
| 0x01        | 0xCC              | Z, 4              | rt5639 power                                                | Out       | [Audio services](Audio%20services.md "wikilink"), [Fatal services](Fatal%20services.md "wikilink")   |
| 0x02        | 0x24              | E, 4              | SDCard Power                                                | Out       | [Filesystem services](Filesystem%20services.md "wikilink")                                           |
| 0x03        | 0x3C              | H, 4              | BT\_RST\_PH4                                                | Out       | [Bluetooth services](Bluetooth%20services.md "wikilink")                                             |
| 0x04        | 0xDA              | BB, 2             |                                                             |           |                                                                                                      |
| 0x05        | 0xDB              | BB, 3             | GcAsic Power                                                | Out       | [Filesystem services](Filesystem%20services.md "wikilink")                                           |
| 0x06        | 0xDC              | BB, 4             | Headphone Detect                                            | In        | [Audio services](Audio%20services.md "wikilink")                                                     |
| 0x07        | 0x25              | E, 5              |                                                             |           |                                                                                                      |
| 0x08        | 0x90              | S, 0              | DebugPadDriver                                              | In        | [HID services](HID%20services.md "wikilink")                                                         |
| 0x09        | 0x91              | S, 1              |                                                             |           |                                                                                                      |
| 0x0A        | 0x96              | S, 6              | bq24192 Charge Enable                                       | Out       | [PTM services](PTM%20services.md "wikilink")                                                         |
| 0x0B        | 0x97              | S, 7              |                                                             |           |                                                                                                      |
| 0x0C        | 0x26              | E, 6              | joycon(L) NwcpDriver0.GpioMonitorTask0 (insertion)          | In        | [HID services](HID%20services.md "wikilink")                                                         |
| 0x0D        | 0x05              | A, 5              | Fan enable (normal)                                         | Out       | [PTM services](PTM%20services.md "wikilink")                                                         |
| 0x0E        | 0x78              | P, 0              | SDMMC3\_CLK\_PP0?                                           |           |                                                                                                      |
| 0x0F        | 0x93              | S, 3              | GcAsic irq                                                  | In        | [Filesystem services](Filesystem%20services.md "wikilink")                                           |
| 0x10        | 0x7D              | P, 5              | SDMMC3\_DAT0\_PP5?                                          |           |                                                                                                      |
| 0x11        | 0x7C              | P, 4              | SDMMC3\_DAT1\_PP4?                                          |           |                                                                                                      |
| 0x12        | 0x7B              | P, 3              | SDMMC3\_DAT2\_PP3?                                          |           |                                                                                                      |
| 0x13        | 0x7A              | P, 2              | SDMMC3\_DAT3\_PP2?                                          |           |                                                                                                      |
| 0x14        | 0xBC              | X, 4              |                                                             |           |                                                                                                      |
| 0x15        | 0xAE              | V, 6              |                                                             | In        | [Audio services](Audio%20services.md "wikilink")                                                     |
| 0x16        | 0xBA              | X, 2              | MOTION\_INT\_PX2?                                           |           |                                                                                                      |
| 0x17        | 0xB9              | X, 1              | Touchscreen irq (TOUCH\_INT\_PX1) (unused - polled instead) | In        | [HID services](HID%20services.md "wikilink")                                                         |
| 0x18        | 0xBD              | X, 5              | Power Button (BUTTON\_POWER\_ON\_PX5)                       | In        |                                                                                                      |
| 0x19        | 0xBE              | X, 6              | Volume Up (BUTTON\_VOL\_UP\_PX6)                            | In        | [Boot2](Boot2.md "wikilink"), [Audio services](Audio%20services.md "wikilink")                       |
| 0x1A        | 0xBF              | X, 7              | Volume Down (BUTTON\_VOL\_DOWN\_PX7)                        | In        | [Boot2](Boot2.md "wikilink"), [Audio services](Audio%20services.md "wikilink")                       |
| 0x1B        | 0xC0              | Y, 0              | max17050 irq                                                | In        | [PTM services](PTM%20services.md "wikilink")                                                         |
| 0x1C        | 0xC1              | Y, 1              | BUTTON\_HOME\_PY1                                           | In        |                                                                                                      |
| 0x1D        | 0xA9              | V, 1              | Backlight (LCD\_BL\_EN\_PV1)                                | Out       | [NV services](NV%20services.md "wikilink"), [Backlight services](Backlight%20services.md "wikilink") |
| 0x1E        | 0xAA              | V, 2              | Backlight (LCD\_RST\_PV2)                                   | Out       | [NV services](NV%20services.md "wikilink")                                                           |
| 0x1F        | 0x55              | K, 5              | bq24192 OTG charge select                                   | Out       | [PTM services](PTM%20services.md "wikilink"), [USB services](USB%20services.md "wikilink")           |
| 0x20        | 0xAD              | V, 5              | PD related                                                  | Out       | [USB services](USB%20services.md "wikilink")                                                         |
| 0x21        | 0xC8              | Z, 0              | bq24192 irq                                                 | In        | [PTM services](PTM%20services.md "wikilink")                                                         |
| 0x22        | 0xCA              | Z, 2              |                                                             |           |                                                                                                      |
| 0x23        | 0xCB              | Z, 3              |                                                             |           |                                                                                                      |
| 0x24        | 0x4F              | J, 7              | Touchscreen reset                                           | Out       | [HID services](HID%20services.md "wikilink")                                                         |
| 0x25        | 0x50              | K, 0              |                                                             |           |                                                                                                      |
| 0x26        | 0x51              | K, 1              |                                                             |           |                                                                                                      |
| 0x27        | 0x52              | K, 2              |                                                             |           |                                                                                                      |
| 0x28        | 0x54              | K, 4              | bm92t36 irq                                                 | In        | [USB services](USB%20services.md "wikilink")                                                         |
| 0x29        | 0x56              | K, 6              |                                                             |           |                                                                                                      |
| 0x2A        | 0x57              | K, 7              |                                                             |           |                                                                                                      |
| 0x2B        | 0x53              | K, 3              | joycon(R) NwcpDriver1.NwcpCharger                           | Out       | [HID services](HID%20services.md "wikilink")                                                         |
| 0x2C        | 0xE3              | CC, 3             | joycon(L) NwcpDriver0.NwcpCharger                           | Out       | [HID services](HID%20services.md "wikilink")                                                         |
| 0x2D        | 0x38              | H, 0              | WIFI\_EN\_PH0?                                              |           |                                                                                                      |
| 0x2E        | 0x39              | H, 1              | WIFI\_RST\_PH1                                              | Out       | [Wlan services](Wlan%20services.md "wikilink"), [PCIe services](PCIe%20services.md "wikilink")       |
| 0x2F        | 0x3B              | H, 3              | AP\_WAKE\_BT\_PH3                                           | Out       | [Bluetooth services](Bluetooth%20services.md "wikilink")                                             |
| 0x30        | 0x3D              | H, 5              |                                                             |           |                                                                                                      |
| 0x31        | 0x3F              | H, 7              |                                                             |           |                                                                                                      |
| 0x32        | 0x40              | I, 0              | Backlight +5V                                               | Out       | [NV services](NV%20services.md "wikilink")                                                           |
| 0x33        | 0x41              | I, 1              | Backlight -5V                                               | Out       | [NV services](NV%20services.md "wikilink")                                                           |
| 0x34        | 0x3E              | H, 6              | joycon(R) NwcpDriver1.GpioMonitorTask0 (insertion)          | In        | [HID services](HID%20services.md "wikilink")                                                         |
| 0x35        | 0xE2              | CC, 2             |                                                             |           |                                                                                                      |
| 0x36        | 0xE4              | CC, 4             | Fan enable (high power)                                     | Out       | [PTM services](PTM%20services.md "wikilink")                                                         |
| 0x37        | 0x3A              | H, 2              |                                                             |           |                                                                                                      |
| 0x38        | 0xC9              | Z, 1              | SDCard Card Detect                                          | In        | [Filesystem services](Filesystem%20services.md "wikilink")                                           |
| 0x39        | 0x4D              | J, 5              | bq24192 OTG charge select                                   | Out       | [PTM services](PTM%20services.md "wikilink"), [USB services](USB%20services.md "wikilink")           |
| 0x3A        | 0x58              | L, 0              | bq24192 OTG charge select                                   | Out       | [PTM services](PTM%20services.md "wikilink"), [USB services](USB%20services.md "wikilink")           |
| 0x3B        | 0x3E              | H, 6              |                                                             |           |                                                                                                      |
| 0x3C        | 0x26              | E, 6              |                                                             |           |                                                                                                      |
| 0x3D        | \-1               |                   |                                                             |           |                                                                                                      |
| 0x3E        | 0x33              | G, 3              | joycon(R) NwcpDriver1.GpioMonitorTask1                      | In        | [HID services](HID%20services.md "wikilink")                                                         |
| 0x3F        | 0x1C              | D, 4              | joycon(L) NwcpDriver0.GpioMonitorTask1                      | In        | [HID services](HID%20services.md "wikilink")                                                         |
| 0x40        | 0xD9              | BB, 1             |                                                             |           |                                                                                                      |
| 0x41        | 0x0C              | B, 4              | Lid Closed (unused)                                         |           |                                                                                                      |
| 0x42        | 0x0D              | B, 5              |                                                             |           |                                                                                                      |
| 0x43        | 0x21              | E, 1              | USB power                                                   | Out       | [USB services](USB%20services.md "wikilink")                                                         |
| 0x44        | 0x27              | E, 7              |                                                             |           |                                                                                                      |
| 0x45        | 0x92              | S, 2              |                                                             |           |                                                                                                      |
| 0x46        | 0x95              | S, 5              | USB root port 4 power                                       | Out       | [USB services](USB%20services.md "wikilink")                                                         |
| 0x47        | 0x98              | T, 0              | USB root port 3 power                                       | Out       | [USB services](USB%20services.md "wikilink")                                                         |
| 0x48        | 0x10              | C, 0              | HdmiHotplug                                                 | Out       | [NV services](NV%20services.md "wikilink")                                                           |
| 0x49        | 0x11              | C, 1              | USB root port 2 power                                       | Out       | [USB services](USB%20services.md "wikilink")                                                         |
| 0x4A        | 0x12              | C, 2              | HdmiHotplug                                                 | Out       | [NV services](NV%20services.md "wikilink")                                                           |
| 0x4B        | 0x42              | I, 2              |                                                             |           |                                                                                                      |
| 0x4C        | 0xE6              | CC, 6             |                                                             |           |                                                                                                      |
| \--         | 0xE1              | CC, 1             | HdmiHotplug (HDMI\_INT\_DP\_HPD\_PCC1)                      | In        | [NV services](NV%20services.md "wikilink")                                                           |

## OpenSessionForTest

Same as [\#OpenSession](#OpenSession "wikilink") but panics on failure.

## OpenSession2

Same as [\#OpenSession](#OpenSession "wikilink") but takes a
**DeviceCode** instead of a **GpioPadName**.

## IPadSession

This is "nn::gpio::IPadSession".

| Cmd | Name                             |
| --- | -------------------------------- |
| 0   | SetDirection                     |
| 1   | GetDirection                     |
| 2   | SetInterruptMode                 |
| 3   | GetInterruptMode                 |
| 4   | SetInterruptEnable               |
| 5   | GetInterruptEnable               |
| 6   | GetInterruptStatus               |
| 7   | ClearInterruptStatus             |
| 8   | SetValue                         |
| 9   | GetValue                         |
| 10  | BindInterrupt                    |
| 11  | UnbindInterrupt                  |
| 12  | SetDebounceEnabled               |
| 13  | GetDebounceEnabled               |
| 14  | SetDebounceTime                  |
| 15  | GetDebounceTime                  |
| 16  | \[4.0.0+\] SetValueForSleepState |

## GpioPadDescriptor

| Bits | Description      |
| ---- | ---------------- |
| 7-5  | Controller index |
| 4-3  | Port index       |
| 2-0  | Pin number       |

# i2c, i2c:pcv

This is "nn::i2c::IManager".

| Cmd | Name              |
| --- | ----------------- |
| 0   | OpenSessionForDev |
| 1   | OpenSession       |
| 2   | HasDevice         |
| 3   | HasDeviceForDev   |

## Known Devices

| Name | Port:Addr | 10bit? | Speed  | Max Retries | Retry Delay | Usage                                 | Used by                                                                                            |
| ---- | --------- | ------ | ------ | ----------- | ----------- | ------------------------------------- | -------------------------------------------------------------------------------------------------- |
| 0    | 0:52      | N      | 100000 | 0           | 0           | DebugPadDriver                        | [HID services](HID%20services.md "wikilink")                                                       |
| 1    | 2:49      | N      | 400000 | 0           | 0           | STM touchscreen                       | [HID services](HID%20services.md "wikilink")                                                       |
| 2    | 0:4c      | N      | 100000 | 0           | 0           | TI Temperature Sensor (tmp451)        | [PTM services](PTM%20services.md "wikilink")                                                       |
| 3    | 0:4c      | N      | 100000 | 0           | 0           | duplicate, unused entry?              |                                                                                                    |
| 4    | 0:1c      | N      | 100000 | 0           | 0           | Audio codec (rt5639)                  | [Audio services](Audio%20services.md "wikilink"), [Fatal services](Fatal%20services.md "wikilink") |
| 5    | 4:68      | N      | 400000 | 3           | 5000000     | max77620\_rtc0, max77620\_irq0        | [PCV services](PCV%20services.md "wikilink")                                                       |
| 6    | 4:3c      | N      | 400000 | 3           | 5000000     | PMIC (max77620), max77620\_irq0       | [PCV services](PCV%20services.md "wikilink")                                                       |
| 7    | 4:1b      | N      | 400000 | 3           | 5000000     | max77621\_cpu                         | [PCV services](PCV%20services.md "wikilink")                                                       |
| 8    | 4:1c      | N      | 400000 | 3           | 5000000     | max77621\_gpu                         | [PCV services](PCV%20services.md "wikilink")                                                       |
| 9    | 0:6b      | N      | 100000 | 3           | 5000000     | TI Charger (bq24192)                  | [PTM services](PTM%20services.md "wikilink")                                                       |
| 10   | 0:36      | N      | 100000 | 3           | 5000000     | Maxim Fuel Gauge (max17050)           | [PCV services](PCV%20services.md "wikilink"), [PTM services](PTM%20services.md "wikilink")         |
| 11   | 0:18      | N      | 100000 | 3           | 5000000     | USB-PD controller (rohm bm92t36)      | [USB services](USB%20services.md "wikilink")                                                       |
| 12   | 1:40      | N      | 400000 | 3           | 5000000     |                                       |                                                                                                    |
| 13   | 1:41      | N      | 400000 | 3           | 5000000     |                                       |                                                                                                    |
| 14   | 1:44      | N      | 400000 | 3           | 5000000     |                                       |                                                                                                    |
| 15   | 1:45      | N      | 400000 | 3           | 5000000     |                                       |                                                                                                    |
| 16   | 1:46      | N      | 400000 | 3           | 5000000     |                                       |                                                                                                    |
| 17   | 1:47      | N      | 400000 | 3           | 5000000     |                                       |                                                                                                    |
| 18   | 1:29      | N      | 400000 | 3           | 5000000     | rohm ambient light sensor (bh1730fvc) | [Backlight services](Backlight%20services.md "wikilink")                                           |
| 19   | 1:48      | N      | 400000 | 3           | 5000000     |                                       |                                                                                                    |
| 20   | 1:49      | N      | 400000 | 3           | 5000000     |                                       |                                                                                                    |
| 21   | 1:4a      | N      | 400000 | 3           | 5000000     |                                       |                                                                                                    |
| 22   | 1:4b      | N      | 400000 | 3           | 5000000     |                                       |                                                                                                    |
| 23   | 1:4d      | N      | 400000 | 3           | 5000000     |                                       |                                                                                                    |
| 24   | 3:50      | N      | 100000 | 0           | 0           | DisplayHdmiHotplugHandler             | [NV services](NV%20services.md "wikilink")                                                         |
| 25   | 3:54      | N      | 100000 | 0           | 0           | DisplayHdmiHotplugHandler             | [NV services](NV%20services.md "wikilink")                                                         |
| 26   | 3:3a      | N      | 100000 | 0           | 0           | DisplayHdmiHotplugHandler             | [NV services](NV%20services.md "wikilink")                                                         |

This table is believed to be complete - entries with empty "Used by"
column haven't been seen being used (devices not present on switch?).

## II2cSession

This is "nn::i2c::ISession".

| Cmd | Name                   |
| --- | ---------------------- |
| 0   | Send                   |
| 1   | Receive                |
| 2   | ExecuteCommandList     |
| 10  | SendAuto               |
| 11  | ReceiveAuto            |
| 12  | ExecuteCommandListAuto |

# uart

This is "nn::uart::IManager".

| Cmd | Name                         |
| --- | ---------------------------- |
| 0   | DoesUartExist                |
| 1   | DoesUartExistForTest         |
| 2   | SetUartBaudrate              |
| 3   | SetUartBaudrateForTest       |
| 4   | IsSomethingUartValid         |
| 5   | IsSomethingUartValidForTest  |
| 6   | GetSession                   |
| 7   | IsSomethingUartValid2        |
| 8   | IsSomethingUartValid2ForTest |

## IPortSession

This is "nn::uart::IPortSession".

| Cmd | Name               | Notes                      |
| --- | ------------------ | -------------------------- |
| 0   | OpenSession        | Takes marshalled arguments |
| 1   | OpenSessionForTest | Takes marshalled arguments |
| 2   |                    |                            |
| 3   |                    | Takes marshalled arguments |
| 4   |                    | Returns 2x u64. Both zero. |
| 5   |                    |                            |
| 6   |                    |                            |
| 7   |                    |                            |
|     |                    |                            |

### Port Mapping

OpenSession translates user IDs to to the uart port index.

OpenSessionForTest takes the port index verbatim.

| Name | Port   | Usage     |
| ---- | ------ | --------- |
| 1    | UART-D | Bluetooth |
| 2    | UART-B | Joycon(R) |
| 3    | UART-C | Joycon(L) |
|      |        |           |

# pwm

This is "nn::pwm::IManager".

| Cmd | Name              |
| --- | ----------------- |
| 0   | OpenSessionForDev |
| 1   | OpenSession       |

## Known Channels

| Name | Interface     | Usage     | Used by                                                                                              |
| ---- | ------------- | --------- | ---------------------------------------------------------------------------------------------------- |
| 1    | PWM Channel 1 | Fan       | [PTM services](PTM%20services.md "wikilink")                                                         |
| 2    | PWM Channel 0 | Backlight | [Backlight services](Backlight%20services.md "wikilink"), [NV services](NV%20services.md "wikilink") |
| 3    | PMC Blinker   |           |                                                                                                      |

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

# pinmux

This is "nn::pinmux::IManager".

| Cmd | Name        |
| --- | ----------- |
| 0   | OpenSession |

## ISession

This is "nn::pinmux::ISession".

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |

# sasbus

This is "nn::sasbus::IManager".

| Cmd | Name        |
| --- | ----------- |
| 0   | OpenSession |

## ISession

This is "nn::sasbus::ISession".

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |
| 3   |      |

[Category:Services](Category:Services "wikilink")

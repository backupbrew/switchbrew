# gpio

This is "nn::gpio::IManager".

| Cmd | Name                                                   |
| --- | ------------------------------------------------------ |
| 0   | [\#OpenSessionForDev](#OpenSessionForDev "wikilink")   |
| 1   | [\#OpenSession](#OpenSession "wikilink")               |
| 2   | [\#OpenSessionForTest](#OpenSessionForTest "wikilink") |
| 3   | \[1.0.0-6.2.0\] IsWakeEventActive                      |
| 4   | \[1.0.0-6.2.0\] GetWakeEventActiveFlagSet              |
| 5   | \[1.0.0-6.2.0\] SetWakeEventActiveFlagSetForDebug      |
| 6   | SetWakePinDebugMode                                    |
| 7   | \[5.0.0+\] [\#OpenSession2](#OpenSession2 "wikilink")  |
| 8   | \[5.0.0+\] IsWakeEventActive2                          |
| 9   | \[5.0.0+\] SetWakeEventActiveFlagSetForDebug2          |
| 10  | \[6.0.0+\]                                             |

## Known Devices

| GpioPadName     | GpioPadDescriptor | DeviceCode | Tegra (port, pin) | Usage                                                                                               | Direction | Used by                                                                                              |
| --------------- | ----------------- | ---------- | ----------------- | --------------------------------------------------------------------------------------------------- | --------- | ---------------------------------------------------------------------------------------------------- |
| 0x01            | 0xCC              | 0x33000002 | Z, 4              | Audio Codec (ALC5639) Power (CODEC\_LDO\_EN\_TEMP)                                                  | Out       | [Audio services](Audio%20services.md "wikilink"), [Fatal services](Fatal%20services.md "wikilink")   |
| 0x02            | 0x24              | 0x3C000001 | E, 4              | SDCard Power (POW\_SD\_EN)                                                                          | Out       | [PCV services](PCV%20services.md "wikilink")                                                         |
| 0x03            | 0x3C              | 0x37000002 | H, 4              | Bluetooth Reset (BT\_RST\_PH4)                                                                      | Out       | [Bluetooth Driver services](Bluetooth%20Driver%20services.md "wikilink")                             |
| 0x04            | 0xDA              | 0xC9000402 | BB, 2             | Secondary Boot Device Configration (RAM\_CODE3)                                                     | In        |                                                                                                      |
| 0x05            | 0xDB              | 0x3C000402 | BB, 3             | GcAsic Reset (GC\_RST)                                                                              | Out       | [Filesystem services](Filesystem%20services.md "wikilink")                                           |
| 0x06            | 0xDC              | 0x33000003 | BB, 4             | Audio Codec (ALC5639) Alert (CODEC\_ALERT)                                                          | In        | [Audio services](Audio%20services.md "wikilink")                                                     |
| 0x07            | 0x25              | 0x3C000401 | E, 5              | GcAsic Power (POW\_GC)                                                                              | Out       |                                                                                                      |
| 0x08            | 0x90              | 0x350000CA | S, 0              | Debug Pad Detect (DEBUG\_CONTROLLER\_DET)                                                           | In        | [HID services](HID%20services.md "wikilink")                                                         |
| 0x09            | 0x91              | 0x39000407 | S, 1              | Battery Charge Status (BATT\_CHG\_STATUS)                                                           | In        |                                                                                                      |
| 0x0A            | 0x96              | 0x39000003 | S, 6              | Charger IC (BQ24193) Charge Enable (BATT\_CHG\_ENABLE\_N)                                           | Out       | [PTM services](PTM%20services.md "wikilink")                                                         |
| 0x0B            | 0x97              | 0x3D000002 | S, 7              | Fan Tachometer (FAN\_TACH)                                                                          | In        |                                                                                                      |
| 0x0C            | 0x26              | 0x3500040B | E, 6              | Joy-Con(L) IsAttached (insertion, Joy-Con pin 5/console TX, pulled low on insert?) (EXTCON\_DET\_S) | In        | [HID services](HID%20services.md "wikilink")                                                         |
| 0x0D            | 0x05              | 0x39000401 | A, 5              | Fan Power (normal) (VDD50A\_EN)                                                                     | Out       | [PTM services](PTM%20services.md "wikilink")                                                         |
| 0x0E            | 0x78              | 0xCA000402 | P, 0              | SDEV Coax Select (SDEV\_COAX\_SEL\_1)                                                               | In        |                                                                                                      |
| 0x0F            | 0x93              | 0x3C000403 | S, 3              | GcAsic Card Detect (GC\_CD)                                                                         | In        | [Filesystem services](Filesystem%20services.md "wikilink")                                           |
| 0x10            | 0x7D              | 0xC900040B | P, 5              | PROD\_TYPE\_0                                                                                       | In        |                                                                                                      |
| 0x11            | 0x7C              | 0xC900040C | P, 4              | PROD\_TYPE\_1                                                                                       | In        |                                                                                                      |
| 0x12            | 0x7B              | 0xC900040D | P, 3              | PROD\_TYPE\_2                                                                                       | In        |                                                                                                      |
| 0x13            | 0x7A              | 0xC900040E | P, 2              | PROD\_TYPE\_3                                                                                       | In        |                                                                                                      |
| 0x14            | 0xBC              | 0x3E000002 | X, 4              | Temperature Sensor (TEMP\_ALERT)                                                                    | In        |                                                                                                      |
| 0x15            | 0xAE              | 0x33000004 | V, 6              | Audio Codec (ALC5639) Headphone Detect (CODEC\_HP\_DET\_IRQ)                                        | In        | [Audio services](Audio%20services.md "wikilink")                                                     |
| 0x16            | 0xBA              | 0x35000041 | X, 2              | MOTION\_INT\_PX2                                                                                    | In        |                                                                                                      |
| 0x17            | 0xB9              | 0x35000036 | X, 1              | TouchPanel IRQ (TP\_IRQ) (unused - polled instead)                                                  | In        | [HID services](HID%20services.md "wikilink")                                                         |
| 0x18            | 0xBD              | 0x35000001 | X, 5              | Power Button (BUTTON\_POWER\_ON\_PX5)                                                               | In        |                                                                                                      |
| 0x19            | 0xBE              | 0x35000002 | X, 6              | Volume Up (BUTTON\_VOL\_UP\_PX6)                                                                    | In        | [Boot2](Boot2.md "wikilink"), [Audio services](Audio%20services.md "wikilink")                       |
| 0x1A            | 0xBF              | 0x35000003 | X, 7              | Volume Down (BUTTON\_VOL\_DOWN\_PX7)                                                                | In        | [Boot2](Boot2.md "wikilink"), [Audio services](Audio%20services.md "wikilink")                       |
| 0x1B            | 0xC0              | 0x39000034 | Y, 0              | Fuel Gauge IC (MAX17050) IRQ (BATT\_MGIC\_IRQ)                                                      | In        | [PTM services](PTM%20services.md "wikilink")                                                         |
| 0x1C            | 0xC1              | 0x35000004 | Y, 1              | Recovery Mode Key (BUTTON\_HOME\_PY1)                                                               | In        |                                                                                                      |
| 0x1D            | 0xA9              | 0x3400003E | V, 1              | Backlight Enable (LCD\_BL\_EN\_PV1)                                                                 | Out       | [NV services](NV%20services.md "wikilink"), [Backlight services](Backlight%20services.md "wikilink") |
| 0x1E            | 0xAA              | 0x34000033 | V, 2              | Backlight Reset (LCD\_RST\_PV2)                                                                     | Out       | [NV services](NV%20services.md "wikilink")                                                           |
| 0x1F            | 0x55              | 0x040000CC | K, 5              | USB-PD Controller (RHOM BM92T30MWV) VCONN Power (PD\_VCONN\_EN)                                     | Out       | [PTM services](PTM%20services.md "wikilink"), [USB services](USB%20services.md "wikilink")           |
| 0x20            | 0xAD              | 0x040000CA | V, 5              | USB-PD Controller (RHOM BM92T30MWV) Reset (PD\_RST)                                                 | Out       | [USB services](USB%20services.md "wikilink")                                                         |
| 0x21            | 0xC8              | 0x39000002 | Z, 0              | Charger IC (BQ24193) IRQ (BQ24193\_IRQ)                                                             | In        | [PTM services](PTM%20services.md "wikilink")                                                         |
| 0x22            | 0xCA              | 0xCA000401 | Z, 2              | SDEV Coax Select (SDEV\_COAX\_SEL\_0)                                                               | In        |                                                                                                      |
| 0x23            | 0xCB              | 0x3C000003 | Z, 3              | SDCard Write Protect (SD\_WP)                                                                       | In        |                                                                                                      |
| 0x24            | 0x4F              | 0x35000035 | J, 7              | TouchPanel Reset (TP\_RST)                                                                          | Out       | [HID services](HID%20services.md "wikilink")                                                         |
| 0x25            | 0x50              | 0x37000401 | K, 0              | BT\_GPIO\_2                                                                                         | In        |                                                                                                      |
| 0x26            | 0x51              | 0x37000402 | K, 1              | BT\_GPIO\_3                                                                                         | In        |                                                                                                      |
| 0x27            | 0x52              | 0x37000403 | K, 2              | BT\_GPIO\_4                                                                                         | In        |                                                                                                      |
| 0x28            | 0x54              | 0x040000CB | K, 4              | USB-PD Controller (RHOM BM92T30MWV) IRQ (PD\_IRQ)                                                   | In        | [USB services](USB%20services.md "wikilink")                                                         |
| 0x29            | 0x56              | 0x3E000003 | K, 6              | POW\_VCPU\_INT                                                                                      | In        |                                                                                                      |
| 0x2A            | 0x57              | 0x3E000004 | K, 7              | MAX77621\_GPU\_INT                                                                                  | In        |                                                                                                      |
| 0x2B            | 0x53              | 0x35000402 | K, 3              | Joy-Con(R) Charge Detect (EXTCON\_CHG\_U)                                                           | Out       | [HID services](HID%20services.md "wikilink")                                                         |
| 0x2C            | 0xE3              | 0x3500040C | CC, 3             | Joy-Con(L) Charge Detect (EXTCON\_CHG\_S)                                                           | Out       | [HID services](HID%20services.md "wikilink")                                                         |
| 0x2D            | 0x38              | 0x38000003 | H, 0              | WIFI\_RF\_DISABLE                                                                                   | Out       |                                                                                                      |
| 0x2E            | 0x39              | 0x38000002 | H, 1              | WiFi Reset (WIFI\_RST\_PH1)                                                                         | Out       | [WLAN services](WLAN%20services.md "wikilink"), [PCIe services](PCIe%20services.md "wikilink")       |
| 0x2F            | 0x3B              | 0x37000003 | H, 3              | AP\_WAKE\_BT\_PH3                                                                                   | Out       | [Bluetooth Driver services](Bluetooth%20Driver%20services.md "wikilink")                             |
| 0x30            | 0x3D              | 0x37000004 | H, 5              | BT\_WAKE\_AP                                                                                        | In        |                                                                                                      |
| 0x31            | 0x3F              | 0x37000404 | H, 7              | BT\_GPIO\_5                                                                                         | Out       |                                                                                                      |
| 0x32            | 0x40              | 0x34000034 | I, 0              | Backlight +5V (LCD\_VDD\_P\_EN)                                                                     | Out       | [NV services](NV%20services.md "wikilink")                                                           |
| 0x33            | 0x41              | 0x34000035 | I, 1              | Backlight -5V (LCD\_VDD\_N\_EN)                                                                     | Out       | [NV services](NV%20services.md "wikilink")                                                           |
| 0x34            | 0x3E              | 0x35000401 | H, 6              | Joy-Con(R) IsAttached (insertion, Joy-Con pin 5/console TX, pulled low on insert?) (EXTCON\_DET\_U) | In        | [HID services](HID%20services.md "wikilink")                                                         |
| 0x35            | 0xE2              | 0xC9000401 | CC, 2             | Secondary Boot Device Configration (RAM\_CODE2)                                                     | In        |                                                                                                      |
| 0x36            | 0xE4              | 0x39000402 | CC, 4             | Fan Power (high) (VDD50B\_EN)                                                                       | Out       | [PTM services](PTM%20services.md "wikilink")                                                         |
| 0x37            | 0x3A              | 0x38000004 | H, 2              | WIFI\_WAKE\_HOST                                                                                    | In        |                                                                                                      |
| 0x38            | 0xC9              | 0x3C000002 | Z, 1              | SDCard Card Detect (SD\_CD)                                                                         | In        | [Filesystem services](Filesystem%20services.md "wikilink")                                           |
| 0x39            | 0x4D              | 0x39000404 | J, 5              | Charger IC (BQ24193) OTG Charge Select (OTG\_FET\_1)                                                | Out       | [PTM services](PTM%20services.md "wikilink"), [USB services](USB%20services.md "wikilink")           |
| 0x3A            | 0x58              | 0x39000405 | L, 0              | Charger IC (BQ24193) OTG Charge Select (OTG\_FET\_2)                                                | Out       | [PTM services](PTM%20services.md "wikilink"), [USB services](USB%20services.md "wikilink")           |
| 0x3B            | 0x3E              | 0x35000403 | H, 6              | Joy-Con(R) Wake Detect (EXTCON\_DET\_U)                                                             | In        |                                                                                                      |
| 0x3C            | 0x26              | 0x3500040D | E, 6              | Joy-Con(L) Wake Detect (EXTCON\_DET\_S)                                                             | In        |                                                                                                      |
| 0x3D            | \-1               | 0x39000406 |                   |                                                                                                     |           |                                                                                                      |
| 0x3E            | 0x33              | 0x35000404 | G, 3              | Joy-Con(R) CTS (checked low) (EXT\_UART2\_CTS)                                                      | In        | [HID services](HID%20services.md "wikilink")                                                         |
| 0x3F            | 0x1C              | 0x3500040E | D, 4              | Joy-Con(L) CTS (checked low) (EXT\_UART3\_CTS)                                                      | In        | [HID services](HID%20services.md "wikilink")                                                         |
| 0x40            | 0xD9              | 0x39000408 | BB, 1             | 5V Step-Down Regulator Power (5V\_STEPDOWN\_EN)                                                     | Out       | (SDEV only)                                                                                          |
| 0x41            | 0x0C              | 0x04000401 | B, 4              | USB Root Port 2 Over Current (USB\_B2\_OC)                                                          | In        | [USB services](USB%20services.md "wikilink") (SDEV only)                                             |
| 0x42            | 0x0D              | 0x39000409 | B, 5              | 5V Step-Down Regulator Power Good Flag (5V\_STEPDOWN\_PG)                                           | In        | (SDEV only)                                                                                          |
| 0x43            | 0x21              | 0x04000402 | E, 1              | USB Power (USB\_A\_EN)                                                                              | Out       | [USB services](USB%20services.md "wikilink") (SDEV only)                                             |
| 0x44            | 0x27              | 0x04000403 | E, 7              | USB Power Flag (USB\_A\_FLAG)                                                                       | In        | [USB services](USB%20services.md "wikilink") (SDEV only)                                             |
| 0x45            | 0x92              | 0x04000404 | S, 2              | USB Root Port 3 Over Current (USB\_B3\_OC)                                                          | In        | [USB services](USB%20services.md "wikilink") (SDEV only)                                             |
| 0x46            | 0x95              | 0x04000405 | S, 5              | USB Root Port 3 Power (USB\_B3\_EN)                                                                 | Out       | [USB services](USB%20services.md "wikilink") (SDEV only)                                             |
| 0x47            | 0x98              | 0x04000406 | T, 0              | USB Root Port 2 Power (USB\_B2\_EN)                                                                 | Out       | [USB services](USB%20services.md "wikilink") (SDEV only)                                             |
| 0x48            | 0x10              | 0x34000004 | C, 0              | HDMI 5V (HDMI\_5V\_EN)                                                                              | Out       | \[2.0.0+\] [NV services](NV%20services.md "wikilink") (SDEV only)                                    |
| 0x49            | 0x11              | 0x04000407 | C, 1              | USB Root Port 1 Power (USB\_B1\_EN)                                                                 | Out       | [USB services](USB%20services.md "wikilink") (SDEV only)                                             |
| 0x4A            | 0x12              | 0x34000005 | C, 2              | HDMI/Power Delivery Switch (HDMI\_PD\_TR\_EN)                                                       | Out       | [NV services](NV%20services.md "wikilink") (SDEV only)                                               |
| 0x4B            | 0x42              | 0x3D000003 | I, 2              | Fan Enable (FAN\_EN)                                                                                | Out       | [PTM services](PTM%20services.md "wikilink")                                                         |
| 0x4C            | 0xE6              | 0x04000408 | CC, 6             | USB Root Port 1 Over Current (USB\_B1\_OC)                                                          | In        | [USB services](USB%20services.md "wikilink") (SDEV only)                                             |
| \[2.0.0+\] 0x4D | 0xAC              | 0x3D000001 | V, 4              | Fan Pulse-Width Modulation Control (PWM\_FAN)                                                       | Out       | [PTM services](PTM%20services.md "wikilink")                                                         |
| \[2.0.0+\] 0x4E | 0xE1              | 0x34000006 | CC, 1             | HDMI Hot Plug Detect (HDMI\_INT\_DP\_HPD\_PCC1)                                                     | In        | [NV services](NV%20services.md "wikilink") (SDEV only)                                               |
| \[5.0.0+\] 0x4F | 0x56              | 0x3E000003 | K, 6              | MAX77812\_IRQ                                                                                       |           |                                                                                                      |
| \[6.0.0+\] 0x50 | 0x20              | 0xCA000001 | E, 0              |                                                                                                     |           |                                                                                                      |
| \[6.0.0+\] 0x51 | 0x21              | 0xCA000002 | E, 1              |                                                                                                     |           |                                                                                                      |
| \[6.0.0+\] 0x52 | 0x22              | 0xCA000003 | E, 2              |                                                                                                     |           |                                                                                                      |
| \[6.0.0+\] 0x53 | 0x23              | 0xCA000004 | E, 3              |                                                                                                     |           |                                                                                                      |
| \[6.0.0+\] 0x54 | 0x4C              | 0x36000004 | J, 4              | NFC\_IRQ                                                                                            |           |                                                                                                      |
| \[6.0.0+\] 0x55 | 0x57              | 0x36000003 | K, 7              | NFC\_RST                                                                                            |           |                                                                                                      |
| \[6.0.0+\] 0x56 | 0x94              | 0x35000415 | S, 4              | MCU\_IRQ                                                                                            |           |                                                                                                      |
| \[6.0.0+\] 0x57 | 0x98              | 0x35000416 | T, 0              | MCU\_BOOT                                                                                           |           |                                                                                                      |
| \[6.0.0+\] 0x58 | 0x99              | 0x35000417 | T, 1              | MCU\_RST                                                                                            |           |                                                                                                      |
| \[6.0.0+\] 0x59 | 0xBB              | 0x39000403 | X, 3              | Fan Power (5V3) (VDD5V3\_EN)                                                                        |           | [PTM services](PTM%20services.md "wikilink")                                                         |
| \[6.0.0+\] 0x5A | 0xE5              | 0x35000418 | CC, 5             | MCU\_POR                                                                                            |           |                                                                                                      |
| \[6.0.0+\] 0x5B | 0xAB              | 0x35000005 | V, 3              |                                                                                                     |           |                                                                                                      |
| \[6.0.0+\] 0x5C | 0x4E              | 0x36000002 | J, 6              |                                                                                                     |           |                                                                                                      |
| \[7.0.0+\] -    | 0x32              | 0x35000406 | G, 2              | Joy-Con(R) RTS                                                                                      |           |                                                                                                      |
| \[7.0.0+\] -    | 0x1B              | 0x35000410 | D, 3              | Joy-Con(L) RTS                                                                                      |           |                                                                                                      |
| \[7.0.0+\] -    | 0x17              | 0x3500041B |                   |                                                                                                     |           |                                                                                                      |
| \[7.0.0+\] -    | 0x18              | 0x3500041C |                   |                                                                                                     |           |                                                                                                      |
| \[7.0.0+\] -    | 0x15              | 0x3500041D |                   |                                                                                                     |           |                                                                                                      |
| \[7.0.0+\] -    | 0x16              | 0x3500041E |                   |                                                                                                     |           |                                                                                                      |
| \[8.0.0+\] -    | 0x27              | 0x35000415 | S, 4              | MCU\_IRQ (duplicate)                                                                                |           |                                                                                                      |

## GpioPadDescriptor

| Bits | Description      |
| ---- | ---------------- |
| 7-5  | Controller index |
| 4-3  | Port index       |
| 2-0  | Pin number       |

## OpenSessionForDev

Takes a raw [\#GpioPadDescriptor](#GpioPadDescriptor "wikilink") and
returns a [\#IPadSession](#IPadSession "wikilink") session for it.

## OpenSession

Same thing as [\#OpenSessionForDev](#OpenSessionForDev "wikilink")
except it takes a **GpioPadName** which is then converted to a
[\#GpioPadDescriptor](#GpioPadDescriptor "wikilink"). Returns an
[\#IPadSession](#IPadSession "wikilink") session.

## OpenSessionForTest

Same as [\#OpenSession](#OpenSession "wikilink") but panics on failure.

## OpenSession2

Same as [\#OpenSession](#OpenSession "wikilink") but takes a
**DeviceCode** instead of a **GpioPadName** and an u32 **DeviceUnk**.

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
| 17  | \[6.0.0+\] GetValueForSleepState |

# i2c, i2c:pcv

This is "nn::i2c::IManager".

| Cmd               | Name                                                  |
| ----------------- | ----------------------------------------------------- |
| 0                 | [OpenSessionForDev](#OpenSessionForDev_2 "wikilink")  |
| 1                 | [OpenSession](#OpenSession_2 "wikilink")              |
| \[1.0.0-5.1.0\] 2 | [HasDevice](#HasDevice "wikilink")                    |
| \[1.0.0-5.1.0\] 3 | [HasDeviceForDev](#HasDeviceForDev "wikilink")        |
| 4                 | \[6.0.0+\] [OpenSession2](#OpenSession2_2 "wikilink") |

## Known Devices

| Name          | DeviceCode | Port:Addr | Is10bit | Speed  | Max Retries | Retry Delay | Usage                                            | Used by                                                                                                                                          |
| ------------- | ---------- | --------- | ------- | ------ | ----------- | ----------- | ------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| 0             | 0x350000C9 | 0:52      | N       | 100000 | 0           | 0           | DebugPadDriver                                   | [HID services](HID%20services.md "wikilink"), [PCV services](PCV%20services.md "wikilink")                                                       |
| 1             | 0x35000033 | 2:49      | N       | 400000 | 0           | 0           | TouchPanel                                       | [HID services](HID%20services.md "wikilink"), [PCV services](PCV%20services.md "wikilink")                                                       |
| 2             | 0x3E000001 | 0:4c      | N       | 100000 | 0           | 0           | Temperature Sensor (TMP451 or NCT72)             | [PTM services](PTM%20services.md "wikilink"), [PCV services](PCV%20services.md "wikilink")                                                       |
| 3             | 0x3E000001 | 0:4c      | N       | 100000 | 0           | 0           | Temperature Sensor (TMP451 or NCT72) (duplicate) | [PTM services](PTM%20services.md "wikilink"), [PCV services](PCV%20services.md "wikilink")                                                       |
| 4             | 0x33000001 | 0:1c      | N       | 100000 | 0           | 0           | Audio Codec (ALC5639)                            | [Audio services](Audio%20services.md "wikilink"), [Fatal services](Fatal%20services.md "wikilink"), [PCV services](PCV%20services.md "wikilink") |
| 5             | 0x3B000001 | 4:68      | N       | 400000 | 3           | 5000000     | PMIC RTC (max77620\_rtc0), max77620\_irq0        | [PCV services](PCV%20services.md "wikilink")                                                                                                     |
| 6             | 0x3A000001 | 4:3c      | N       | 400000 | 3           | 5000000     | PMIC (MAX77620), max77620\_irq0                  | [PCV services](PCV%20services.md "wikilink")                                                                                                     |
| 7             | 0x3A000003 | 4:1b      | N       | 400000 | 3           | 5000000     | Sub-PMIC for CPU (max77621\_cpu)                 | [PCV services](PCV%20services.md "wikilink")                                                                                                     |
| 8             | 0x3A000004 | 4:1c      | N       | 400000 | 3           | 5000000     | Sub-PMIC for GPU (max77621\_gpu)                 | [PCV services](PCV%20services.md "wikilink")                                                                                                     |
| 9             | 0x39000001 | 0:6b      | N       | 100000 | 3           | 5000000     | Charger IC (BQ24193)                             | [PTM services](PTM%20services.md "wikilink")                                                                                                     |
| 10            | 0x39000033 | 0:36      | N       | 100000 | 3           | 5000000     | Fuel Gauge IC (MAX17050)                         | [PTM services](PTM%20services.md "wikilink"), [PCV services](PCV%20services.md "wikilink")                                                       |
| 11            | 0x040000C9 | 0:18      | N       | 100000 | 3           | 5000000     | USB-PD controller (RHOM BM92T30MWV)              | [USB services](USB%20services.md "wikilink"), [PCV services](PCV%20services.md "wikilink")                                                       |
| 12            | 0x3F000401 | 1:40      | N       | 400000 | 3           | 5000000     | Power Monitor (ina226\_V\_VDD15V0-HB)            | Factory testing, [PCV services](PCV%20services.md "wikilink")                                                                                    |
| 13            | 0x3F000001 | 1:41      | N       | 400000 | 3           | 5000000     | Power Monitor (ina226\_V\_VSYS-CPU-DS)           | Factory testing, [PCV services](PCV%20services.md "wikilink")                                                                                    |
| 14            | 0x3F000002 | 1:44      | N       | 400000 | 3           | 5000000     | Power Monitor (ina226\_V\_VSYS-GPU-DS)           | Factory testing, [PCV services](PCV%20services.md "wikilink")                                                                                    |
| 15            | 0x3F000003 | 1:45      | N       | 400000 | 3           | 5000000     | Power Monitor (ina226\_V\_VSYS-DDR-DS)           | Factory testing, [PCV services](PCV%20services.md "wikilink")                                                                                    |
| 16            | 0x3F000402 | 1:46      | N       | 400000 | 3           | 5000000     | Power Monitor (ina226\_V\_VSYS-AP)               | Factory testing, [PCV services](PCV%20services.md "wikilink")                                                                                    |
| 17            | 0x3F000403 | 1:47      | N       | 400000 | 3           | 5000000     | Power Monitor (ina226\_V\_VSYS-BL-DS)            | Factory testing, [PCV services](PCV%20services.md "wikilink")                                                                                    |
| 18            | 0x35000047 | 1:29      | N       | 400000 | 3           | 5000000     | Ambient Light Sensor (BH1730)                    | [Backlight services](Backlight%20services.md "wikilink"), [PCV services](PCV%20services.md "wikilink")                                           |
| 19            | 0x3F000404 | 1:48      | N       | 400000 | 3           | 5000000     | Power Monitor (ina226\_CORE)                     | Factory testing, [PCV services](PCV%20services.md "wikilink")                                                                                    |
| 20            | 0x3F000405 | 1:49      | N       | 400000 | 3           | 5000000     | Power Monitor (ina226\_Soc-1V8)                  | Factory testing, [PCV services](PCV%20services.md "wikilink")                                                                                    |
| 21            | 0x3F000406 | 1:4a      | N       | 400000 | 3           | 5000000     | Power Monitor (ina226\_LPDDR4-1V8)               | Factory testing, [PCV services](PCV%20services.md "wikilink")                                                                                    |
| 22            | 0x3F000407 | 1:4b      | N       | 400000 | 3           | 5000000     | Power Monitor (ina226\_REG1V32)                  | Factory testing, [PCV services](PCV%20services.md "wikilink")                                                                                    |
| 23            | 0x3F000408 | 1:4d      | N       | 400000 | 3           | 5000000     | Power Monitor (ina226\_VDD3V3-SYS)               | Factory testing, [PCV services](PCV%20services.md "wikilink")                                                                                    |
| \[2.0.0+\] 24 | 0x34000001 | 3:50      | N       | 100000 | 0           | 0           | HDMI DDC                                         | [NV services](NV%20services.md "wikilink"), [PCV services](PCV%20services.md "wikilink")                                                         |
| \[2.0.0+\] 25 | 0x34000002 | 3:54      | N       | 100000 | 0           | 0           | HDMI SCDC                                        | [NV services](NV%20services.md "wikilink"), [PCV services](PCV%20services.md "wikilink")                                                         |
| \[2.0.0+\] 26 | 0x34000003 | 3:3a      | N       | 100000 | 0           | 0           | HDMI HDCP                                        | [NV services](NV%20services.md "wikilink"), [PCV services](PCV%20services.md "wikilink")                                                         |
| \[4.0.0+\] 27 | 0x3A000005 | 4:a4      | N       | 400000 | 0           | 0           | Fan (Fan53528)                                   | [PCV services](PCV%20services.md "wikilink")                                                                                                     |
| \[4.0.0+\] 28 | 0x3A000002 | 4:31      | N       | 400000 | 0           | 0           | PMIC (Max77812)                                  | [PCV services](PCV%20services.md "wikilink")                                                                                                     |
| \[4.0.0+\] 29 | 0x3A000002 | 4:33      | N       | 400000 | 0           | 0           | PMIC (Max77812)                                  | [PCV services](PCV%20services.md "wikilink")                                                                                                     |
| \[4.0.0+\] 30 | 0x3F000409 | 1:4e      | N       | 400000 | 3           | 5000000     | Power Monitor (ina226\_V\_VDD-DDR-0V6)           | Factory testing, [PCV services](PCV%20services.md "wikilink")                                                                                    |
| \[8.0.0+\] 31 | 0x36000001 | 1:08      | N       | 400000 | 3           | 5000000     |                                                  | [PCV services](PCV%20services.md "wikilink")                                                                                                     |

## OpenSessionForDev

Takes an u32 **port**, an u16 **addr**, an **AddressingMode** (1 for
10-bit, 0 otherwise) and a **SpeedMode** (400000 or 100000). Returns a
[\#II2cSession](#II2cSession "wikilink") session.

## OpenSession

Takes an **I2cDevice** and returns a
[\#II2cSession](#II2cSession "wikilink") session for it.

## HasDevice

Takes an **I2cDevice** and returns true if the device exists or false
otherwise.

## HasDeviceForDev

Takes an u32 **port**, an u16 **addr**, an **AddressingMode** (1 for
10-bit, 0 otherwise) and a **SpeedMode** (400000 or 100000). Returns
true if the device exists or false otherwise.

## OpenSession2

Same as [OpenSession](#OpenSession_2 "wikilink") but takes a
**DeviceCode** instead of a **I2cDevice**.

## II2cSession

This is "nn::i2c::ISession".

| Cmd               | Name                                                           |
| ----------------- | -------------------------------------------------------------- |
| \[1.0.0-5.1.0\] 0 | Send                                                           |
| \[1.0.0-5.1.0\] 1 | Receive                                                        |
| \[1.0.0-5.1.0\] 2 | ExecuteCommandList                                             |
| 10                | [\#SendAuto](#SendAuto "wikilink")                             |
| 11                | ReceiveAuto                                                    |
| 12                | [\#ExecuteCommandListAuto](#ExecuteCommandListAuto "wikilink") |
| 13                | \[6.0.0+\]                                                     |

## SendAuto

Takes bytes to write in either a static buffer or a receive buffer,
returns an error code for success

## ExecuteCommandListAuto

Takes a command list from either a static buffer or a receive buffer,
returns data in either a static (or recieve?) buffer.

### Commands

  - 0x40 \[u8 len\] <bytes> - Write bytes to device
  - 0xC1 \[u8 len\] - Receive bytes from device

# uart

This is "nn::uart::IManager".

| Cmd | Name                                                       |
| --- | ---------------------------------------------------------- |
| 0   | [\#DoesUartExist](#DoesUartExist "wikilink")               |
| 1   | DoesUartExistForTest                                       |
| 2   | [\#IsUartBaudrateValid](#IsUartBaudrateValid "wikilink")   |
| 3   | IsUartBaudrateValidForTest                                 |
| 4   | [\#IsSomethingUartValid](#IsSomethingUartValid "wikilink") |
| 5   | IsSomethingUartValidForTest                                |
| 6   | [\#GetSession](#GetSession "wikilink")                     |
| 7   | IsSomethingUartValid2                                      |
| 8   | IsSomethingUartValid2ForTest                               |
| 9   | \[7.0.0+\] IsSomethingUartValid3                           |
| 10  | \[7.0.0+\] IsSomethingUartValid3ForTest                    |

## DoesUartExist

Takes a u32 [\#UartPort](#UartPort "wikilink") and returns boolean
success value

## IsUartBaudrateValid

Takes a u32 [\#UartPort](#UartPort "wikilink") and a u32 baudrate and
returns boolean success value

## IsSomethingUartValid

Takes a u32 [\#UartPort](#UartPort "wikilink") and returns boolean
success value

## GetSession

Takes a u32 [\#UartPort](#UartPort "wikilink") and returns an
[\#IPortSession](#IPortSession "wikilink")

## UartPort

| Name | Port   | Usage      |
| ---- | ------ | ---------- |
| 1    | UART-D | Bluetooth  |
| 2    | UART-B | Joy-Con(R) |
| 3    | UART-C | Joy-Con(L) |

## IPortSession

This is "nn::uart::IPortSession".

| Cmd | Name               |
| --- | ------------------ |
| 0   | OpenSession        |
| 1   | OpenSessionForTest |
| 2   |                    |
| 3   |                    |
| 4   |                    |
| 5   |                    |
| 6   |                    |
| 7   |                    |

\[7.0.0+\] OpenSession/OpenSessionForTest now takes an additional
0x8-bytes of input.

### Port Mapping

OpenSession translates user IDs to to the
[\#UartPort](#UartPort "wikilink") index.

OpenSessionForTest takes the port index verbatim.

# pwm

This is "nn::pwm::IManager".

| Cmd | Name              |
| --- | ----------------- |
| 0   | OpenSessionForDev |
| 1   | OpenSession       |
| 2   | \[6.0.0+\]        |

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
| 6   | \[6.0.0+\] |
| 7   | \[6.0.0+\] |

# pinmux

This is "nn::pinmux::IManager".

| Cmd | Name        |
| --- | ----------- |
| 0   | OpenSession |

## ISession

This is "nn::pinmux::ISession".

| Cmd | Name                            |
| --- | ------------------------------- |
| 0   | SetPinAssignment                |
| 1   | GetPinAssignment                |
| 2   | SetPinAssignmentForHardwareTest |

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

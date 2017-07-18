# spl:

| Cmd | Name                                           | Notes |
| --- | ---------------------------------------------- | ----- |
| 0   | [\#GetConfig](#GetConfig "wikilink")           |       |
| 1   |                                                |       |
| 2   | [\#KeyGen0](#KeyGen0 "wikilink")               |       |
| 3   |                                                |       |
| 4   | Aes128Ctr                                      |       |
| 5   | [\#SetConfig](#SetConfig "wikilink")           |       |
| 7   |                                                |       |
| 9   |                                                |       |
| 10  |                                                |       |
| 11  | [\#GetDevunitFlag](#GetDevunitFlag "wikilink") |       |
| 12  | KeyGen1                                        |       |
| 13  | [\#EncDec0](#EncDec0 "wikilink")               |       |
| 14  | KeyGen2                                        |       |
| 15  |                                                |       |
| 16  |                                                |       |
| 17  | EncDec1                                        |       |
| 18  | EncDec2                                        |       |
| 19  |                                                |       |
| 20  |                                                |       |
| 21  |                                                |       |
| 22  |                                                |       |
| 23  | GetSplWaitEvent                                |       |

## GetConfig

Takes an input word (ConfigItem), and returns a u64 with the config
params.

| ConfigItem | Name                             |
| ---------- | -------------------------------- |
| 2          | MemoryConfiguration              |
| 5          | HardwareType (0=Icosa, 1=Copper) |
| 7          | IsRecoveryBoot                   |
| 8          | DeviceId (byte7 clear).          |
| 9          | BootReason                       |
| 11         | AllowSkippingNrrSignatures       |
| 13         | BatteryProfile?                  |

Output from this when used by [NIM](NIM%20services.md "wikilink") must
match the [set:cal](Settings%20services.md "wikilink") DeviceId with
byte7 cleared, otherwise NIM will panic.

[RO](Loader%20services.md "wikilink") checks id11, if set then skipping
NRR rsa signatures is allowed.

## KeyGen0

Takes 16-bytes as input and two u32s. Outputs random-looking 16-bytes.

Same input gives same output. Output changes when system is rebooted.

## SetConfig

Takes two input words, a ConfigItem and the value to set.

| ConfigItem | Name             |
| ---------- | ---------------- |
| 13         | Battery profile? |

## GetDevunitFlag

No input params.

Returns an u8 flag for whether the system is devunit. Output flag is 0
on retail.

## EncDec0

Last SPL cmd used by [SSL](SSL%20services.md "wikilink")-sysmodule for
TLS client-privk.

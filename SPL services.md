# spl:

| Cmd | Name                                           | Notes                  |
| --- | ---------------------------------------------- | ---------------------- |
| 0   | [\#GetConfig](#GetConfig "wikilink")           |                        |
| 1   |                                                | Unknown marshalling.   |
| 2   | [\#ScrambleKeyA](#ScrambleKeyA "wikilink")     |                        |
| 3   |                                                | Always returns 0x2D1A? |
| 4   | [\#ScrambleKeyB](#ScrambleKeyB "wikilink")     |                        |
| 5   |                                                | Always returns 0x41A?  |
| 7   |                                                |                        |
| 9   |                                                |                        |
| 10  |                                                |                        |
| 11  | [\#GetDevunitFlag](#GetDevunitFlag "wikilink") |                        |
| 12  |                                                |                        |
| 13  |                                                |                        |
| 14  |                                                |                        |
| 15  |                                                |                        |
| 16  |                                                |                        |
| 17  |                                                |                        |
| 18  |                                                |                        |
| 19  |                                                |                        |
| 20  |                                                |                        |
| 21  |                                                |                        |
| 22  |                                                |                        |
| 23  |                                                |                        |

## GetConfig

Takes an input word (ConfigItem), and returns a u64 with the config
params.

| ConfigItem | Name                                  |
| ---------- | ------------------------------------- |
| 5          | HardwareType (0=Icosa, 1=Copper)      |
| 8          | 64bit DeviceId with byte7 clear.      |
| 11         | Allow skipping RSA signatures on NRR. |

Output from this when used by [NIM](NIM%20services.md "wikilink") must
match the [set:cal](Settings%20services.md "wikilink") DeviceId with
byte7 cleared, otherwise NIM will panic.

[RO](Loader%20services.md "wikilink") checks id11, if set then skipping
NRR rsa signatures is allowed.

## ScrambleKeyA

Takes 16-bytes as input and two u32s. Outputs random-looking 16-bytes.

Same input gives same output. Output changes when system is rebooted.

## ScrambleKeyB

Behaves similar to [\#ScrambleKeyA](#ScrambleKeyA "wikilink"), but with
different output.

Also console unique. This is not the inverse operation of
[\#ScrambleKeyA](#ScrambleKeyA "wikilink").

## GetDevunitFlag

No input params.

Returns an u8 flag for whether the system is devunit. Output flag is 0
on retail.

## Cmd13

Last SPL cmd used by [SSL](SSL%20services.md "wikilink")-sysmodule for
TLS client-privk.

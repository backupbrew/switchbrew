# spl:

| Cmd | Name                                           | Notes                  |
| --- | ---------------------------------------------- | ---------------------- |
| 0   |                                                |                        |
| 1   |                                                | Unknown marshalling.   |
| 2   | [\#ScrambleKeyA](#ScrambleKeyA "wikilink")     |                        |
| 3   |                                                | Always returns 0x2D1A? |
| 4   | [\#ScrambleKeyB](#ScrambleKeyB "wikilink")     |                        |
| 5   |                                                | Always returns 0x41A?  |
| 11  | [\#GetDevunitFlag](#GetDevunitFlag "wikilink") |                        |

## Cmd0

Takes input word, and returns u64.

  - Input val8: 64bit DeviceId with byte7 clear. Output from this when
    used by [NIM](NIM%20servers.md "wikilink") must match the
    [set:cal](Settings%20services.md "wikilink") DeviceId with byte7
    cleared, otherwise NIM will panic.

## ScrambleKeyA

Takes 16-bytes as input and two u32s. Outputs random-looking 16-bytes.

Same input gives same output. Console unique.

## ScrambleKeyB

Behaves similar to [\#ScrambleKeyA](#ScrambleKeyA "wikilink"), but with
different output.

Also console unique. This is not the inverse operation of
[\#ScrambleKeyA](#ScrambleKeyA "wikilink").

## GetDevunitFlag

No input params.

Returns an u8 flag for whether the system is devunit it seems. Output
flag is 0 on retail.

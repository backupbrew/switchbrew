# spl:

| Cmd | Name                                           | Notes                              |
| --- | ---------------------------------------------- | ---------------------------------- |
| 0   |                                                | Takes input word, and returns u64. |
| 1   |                                                | Unknown marshalling.               |
| 2   | [\#ScrambleKeyA](#ScrambleKeyA "wikilink")     |                                    |
| 3   |                                                | Always returns 0x2D1A?             |
| 4   | [\#ScrambleKeyB](#ScrambleKeyB "wikilink")     |                                    |
| 5   |                                                | Always returns 0x41A?              |
| 11  | [\#GetDevunitFlag](#GetDevunitFlag "wikilink") |                                    |

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

Returns an u8 flag for whether the system is devunit it seems.

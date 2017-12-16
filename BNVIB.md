BNVIB is the vibration file for the HD Rumble in the Joy-Con or Pro
Controller.

| Offset | Size | Description                                                         |
| ------ | ---- | ------------------------------------------------------------------- |
| 0x00   | 0x01 | Vibration Type (see [Vibration Types](#Vibration_Types "wikilink")) |
| 0x04   | 0x01 | Magic number (0x03)                                                 |
| 0x06   | ?    | Vibration Data                                                      |

The size of a sample is 4 bytes. The sample rate is in
milliseconds.

# Vibration Types

| Value | Description                                                                                  |
| ----- | -------------------------------------------------------------------------------------------- |
| 0x04  | Normal vibration (Vibrate 1 time) (see [Normal Vibration](#Normal_Vibration "wikilink"))     |
| 0x0C  | Loop vibration (see [Loop Vibration](#Loop_Vibration "wikilink"))                            |
| 0x10  | Loop and wait vibration (see [Loop and Wait Vibration](#Loop_and_Wait_Vibration "wikilink")) |

## Normal Vibration

| Offset | Size    | Description                   |
| ------ | ------- | ----------------------------- |
| 0x00   | 0x02    | Sample rate (LE)              |
| 0x02   | 0x04    | Vibration size (vibsize) (LE) |
| 0x06   | vibsize | Samples                       |

## Loop Vibration

| Offset | Size    | Description                   |
| ------ | ------- | ----------------------------- |
| 0x00   | 0x02    | Sample rate (LE)              |
| 0x02   | 0x04    | Loop start (LE)               |
| 0x06   | 0x04    | Loop end (LE)                 |
| 0x0A   | 0x04    | Vibration size (vibsize) (LE) |
| 0x0E   | vibsize | Samples                       |

## Loop and Wait Vibration

| Offset | Size    | Description                   |
| ------ | ------- | ----------------------------- |
| 0x00   | 0x02    | Sample rate (LE)              |
| 0x02   | 0x04    | Loop start (LE)               |
| 0x06   | 0x04    | Loop end (LE)                 |
| 0x0A   | 0x04    | Loop wait (LE)                |
| 0x0E   | 0x04    | Vibration size (vibsize) (LE) |
| 0x13   | vibsize | Samples                       |

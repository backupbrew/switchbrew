The Joy-Cons use bluetooth or a wired connection to communicate with the
console, depending if they are physically connected to it or not.  
dekuNukem has started RE on the protocols used
[1](https://github.com/dekuNukem/Nintendo_Switch_Reverse_Engineering).

## Firmware

The firmware of the Joy-Cons seems to be generic across all instances.
Details such as the handedness of the controller and the color is just
indicated in a configuration part of the flash. Judging by quick glance
at the firmware, it's probably identical to that used on the Pro
Controller as well.

| Controller          | 1.0.0                                       |
| ------------------- | ------------------------------------------- |
| Joy-Con Left (Blue) | [flash dump](:File:pad.L.bin.md "wikilink") |
| Joy-Con Right (Red) | [flash dump](:File:pad.R.bin.md "wikilink") |

The flash is in a patch-ram format. Tools for dealing with it are
available [2](https://github.com/shuffle2/nxpad). A dump of the ROM
region (taken while firmware was running) can be found
[here](:File:bcm20734%20rom.bin.md "wikilink"). Note this is the same
SoC used on the other controller models, as well.

## Left & Right Separate Joy-con

When paired directly to a computer over bluetooth, the joy-con both
provide identical HID input report descriptor. This does not appear to
include motion controls, IR data, or NFC. They both behave as detached
single-player controllers.

HID Input Report Descriptor (Hexadecimal):

    00000000: 05010905 A1010601 FF852109 21750895  ....¡...ÿ…!.!u.•
    00000010: 30810285 30093075 08953081 02853109  0..…0.0u.•0..…1.
    00000020: 31750896 69018102 85320932 75089669  1u.–i...…2.2u.–i
    00000030: 01810285 33093375 08966901 8102853F  ...…3.3u.–i...…?
    00000040: 05091901 29101500 25017501 95108102  ....)...%.u.•...
    00000050: 05010939 15002507 75049501 81420509  ...9..%.u.•..B..
    00000060: 75049501 81010501 09300931 09330934  u.•......0.1.3.4
    00000070: 16000027 FFFF0000 75109504 81020601  ...'ÿÿ..u.•.....
    00000080: FF850109 01750895 30910285 10091075  ÿ…...u.•0‘.…...u
    00000090: 08953091 02851109 11750895 30910285  .•0‘.…...u.•0‘.…
    000000A0: 12091275 08953091 02C0               ...u.•0‘.À

| Parsed Bytes                  | Description                                                                        |
| ----------------------------- | ---------------------------------------------------------------------------------- |
| 0x05, 0x01,                   | Usage Page (Generic Desktop Ctrls)                                                 |
| 0x09, 0x05,                   | Usage (Game Pad)                                                                   |
| 0xA1, 0x01,                   | Collection (Application)                                                           |
| 0x06, 0x01, 0xFF,             | Usage Page (Vendor Defined 0xFF01)                                                 |
| 0x85, 0x21,                   | Report ID (33)                                                                     |
| 0x09, 0x21,                   | Usage (0x21)                                                                       |
| 0x75, 0x08,                   | Report Size (8)                                                                    |
| 0x95, 0x30,                   | Report Count (48)                                                                  |
| 0x81, 0x02,                   | Input (Data,Var,Abs,No Wrap,Linear,Preferred State,No Null Position)               |
| 0x85, 0x30,                   | Report ID (48)                                                                     |
| 0x09, 0x30,                   | Usage (0x30)                                                                       |
| 0x75, 0x08,                   | Report Size (8)                                                                    |
| 0x95, 0x30,                   | Report Count (48)                                                                  |
| 0x81, 0x02,                   | Input (Data,Var,Abs,No Wrap,Linear,Preferred State,No Null Position)               |
| 0x85, 0x31,                   | Report ID (49)                                                                     |
| 0x09, 0x31,                   | Usage (0x31)                                                                       |
| 0x75, 0x08,                   | Report Size (8)                                                                    |
| 0x96, 0x69, 0x01,             | Report Count (361)                                                                 |
| 0x81, 0x02,                   | Input (Data,Var,Abs,No Wrap,Linear,Preferred State,No Null Position)               |
| 0x85, 0x32,                   | Report ID (50)                                                                     |
| 0x09, 0x32,                   | Usage (0x32)                                                                       |
| 0x75, 0x08,                   | Report Size (8)                                                                    |
| 0x96, 0x69, 0x01,             | Report Count (361)                                                                 |
| 0x81, 0x02,                   | Input (Data,Var,Abs,No Wrap,Linear,Preferred State,No Null Position)               |
| 0x85, 0x33,                   | Report ID (51)                                                                     |
| 0x09, 0x33,                   | Usage (0x33)                                                                       |
| 0x75, 0x08,                   | Report Size (8)                                                                    |
| 0x96, 0x69, 0x01,             | Report Count (361)                                                                 |
| 0x81, 0x02,                   | Input (Data,Var,Abs,No Wrap,Linear,Preferred State,No Null Position)               |
| 0x85, 0x3F,                   | Report ID (63)                                                                     |
| 0x05, 0x09,                   | Usage Page (Button)                                                                |
| 0x19, 0x01,                   | Usage Minimum (0x01)                                                               |
| 0x29, 0x10,                   | Usage Maximum (0x10)                                                               |
| 0x15, 0x00,                   | Logical Minimum (0)                                                                |
| 0x25, 0x01,                   | Logical Maximum (1)                                                                |
| 0x75, 0x01,                   | Report Size (1)                                                                    |
| 0x95, 0x10,                   | Report Count (16)                                                                  |
| 0x81, 0x02,                   | Input (Data,Var,Abs,No Wrap,Linear,Preferred State,No Null Position)               |
| 0x05, 0x01,                   | Usage Page (Generic Desktop Ctrls)                                                 |
| 0x09, 0x39,                   | Usage (Hat switch)                                                                 |
| 0x15, 0x00,                   | Logical Minimum (0)                                                                |
| 0x25, 0x07,                   | Logical Maximum (7)                                                                |
| 0x75, 0x04,                   | Report Size (4)                                                                    |
| 0x95, 0x01,                   | Report Count (1)                                                                   |
| 0x81, 0x42,                   | Input (Data,Var,Abs,No Wrap,Linear,Preferred State,Null State)                     |
| 0x05, 0x09,                   | Usage Page (Button)                                                                |
| 0x75, 0x04,                   | Report Size (4)                                                                    |
| 0x95, 0x01,                   | Report Count (1)                                                                   |
| 0x81, 0x01,                   | Input (Const,Array,Abs,No Wrap,Linear,Preferred State,No Null Position)            |
| 0x05, 0x01,                   | Usage Page (Generic Desktop Ctrls)                                                 |
| 0x09, 0x30,                   | Usage (X)                                                                          |
| 0x09, 0x31,                   | Usage (Y)                                                                          |
| 0x09, 0x33,                   | Usage (Rx)                                                                         |
| 0x09, 0x34,                   | Usage (Ry)                                                                         |
| 0x16, 0x00, 0x00,             | Logical Minimum (0)                                                                |
| 0x27, 0xFF, 0xFF, 0x00, 0x00, | Logical Maximum (65534)                                                            |
| 0x75, 0x10,                   | Report Size (16)                                                                   |
| 0x95, 0x04,                   | Report Count (4)                                                                   |
| 0x81, 0x02,                   | Input (Data,Var,Abs,No Wrap,Linear,Preferred State,No Null Position)               |
| 0x06, 0x01, 0xFF,             | Usage Page (Vendor Defined 0xFF01)                                                 |
| 0x85, 0x01,                   | Report ID (1)                                                                      |
| 0x09, 0x01,                   | Usage (0x01)                                                                       |
| 0x75, 0x08,                   | Report Size (8)                                                                    |
| 0x95, 0x30,                   | Report Count (48)                                                                  |
| 0x91, 0x02,                   | Output (Data,Var,Abs,No Wrap,Linear,Preferred State,No Null Position,Non-volatile) |
| 0x85, 0x10,                   | Report ID (16)                                                                     |
| 0x09, 0x10,                   | Usage (0x10)                                                                       |
| 0x75, 0x08,                   | Report Size (8)                                                                    |
| 0x95, 0x30,                   | Report Count (48)                                                                  |
| 0x91, 0x02,                   | Output (Data,Var,Abs,No Wrap,Linear,Preferred State,No Null Position,Non-volatile) |
| 0x85, 0x11,                   | Report ID (17)                                                                     |
| 0x09, 0x11,                   | Usage (0x11)                                                                       |
| 0x75, 0x08,                   | Report Size (8)                                                                    |
| 0x95, 0x30,                   | Report Count (48)                                                                  |
| 0x91, 0x02,                   | Output (Data,Var,Abs,No Wrap,Linear,Preferred State,No Null Position,Non-volatile) |
| 0x85, 0x12,                   | Report ID (18)                                                                     |
| 0x09, 0x12,                   | Usage (0x12)                                                                       |
| 0x75, 0x08,                   | Report Size (8)                                                                    |
| 0x95, 0x30,                   | Report Count (48)                                                                  |
| 0x91, 0x02,                   | Output (Data,Var,Abs,No Wrap,Linear,Preferred State,No Null Position,Non-volatile) |
| 0xC0,                         | End Collection                                                                     |

## Colors

HEX codes for the colors shown in the "Controllers" menu of the Switch
UI can be found in a Joy-con SPI dump starting at offset 0x6050. Body
color is first followed by button color and each is 3 bytes long. These
values are able to be re-written with any HEX color value to make the
Joy-cons show up as different colors in the UI. The following is a list
of official HEX colors recovered from SPI dumps.

| Color Name  | Body HEX | Button HEX |
| ----------- | -------- | ---------- |
| Gray        | \#828282 | \#0F0F0F   |
| Neon Red    | \#FF3C28 | \#1E0A0A   |
| Neon Blue   | \#0AB9E6 | \#001E1E   |
| Neon Yellow | \#E6FF00 | \#142800   |
| Neon Green  | \#1EDC00 | \#002800   |
| Neon Pink   | \#FF3278 | \#28001E   |
| Mario Red   | \#E10F00 | \#280A0A   |

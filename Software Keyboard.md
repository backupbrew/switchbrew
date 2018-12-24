The software keyboard (swkbd) expects to be passed three
[IStorages](AM%20services#IStorage.md##IStorage "wikilink"). See also
[AM\_services\#Library\_Applets](AM%20services#Library%20Applets.md##Library_Applets "wikilink").

The below is for normal swkbd usage. There's also InlineKeyboard (added
post-1.0.0), which doesn't run in the foreground and has completely
different input/output
[IStorages](AM%20services#IStorage.md##IStorage "wikilink"). It also
doesn't seem to display on the screen (or is optional at least): the
user-process can get the gfx data via
[Display\_services](Display%20services.md "wikilink").

## Library Applet Versions

| System Version | Value    |
| -------------- | -------- |
|                | 0x0..0x1 |
|                | 0x2      |
|                | 0x3..4   |
| \[1.0.0+\]     | 0x5      |
| \[2.0.0+\]     | 0x10006  |
| \[3.0.0+\]     | 0x30007  |
| \[4.0.0+\]     | 0x40008  |
| \[5.0.0+\]     | 0x50009  |

## KeyboardConfig

The second IStorage passed to this applet should contain the
configuration for the
keyboard.

| Offset | Size | Typical Value | Notes                                                                                                                                              |
| ------ | ---- | ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 4    |               | Type                                                                                                                                               |
| 0x4    | 18   | 0             | UTF-16 text displayed in the submit button                                                                                                         |
| 0x16   | 2    | 0             | UTF-16 "left optional symbol key"                                                                                                                  |
| 0x18   | 2    | 0             | UTF-16 "right optional symbol key"                                                                                                                 |
| 0x1A   | 1    | 0             | Enables dictionary usage when non-zero (including the system dictionary).                                                                          |
| 0x1C   | 4    | 0             | Key set disable bitmask                                                                                                                            |
| 0x20   | 4    | 1             | Initial cursor position (0 = start of string, 1 = end of string)                                                                                   |
| 0x24   | 130  | u""           | UTF-16 header text                                                                                                                                 |
| 0xA6   | 258  | u""           | UTF-16 sub text                                                                                                                                    |
| 0x1A8  | 514  | u""           | UTF-16 guide text                                                                                                                                  |
| 0x3AC  | 4    | 0             | stringLenMax                                                                                                                                       |
| 0x3B0  | 4    | 0             | stringLenMaxExt. When non-zero, specifies the max string length. When the input is too long, swkbd will display an icon and disable the ok-button. |
| 0x3B4  | 4    | 0             | Password flag (0 = not password, 1 = password)                                                                                                     |
| 0x3B8  | 4    | 1             | textDrawType                                                                                                                                       |
| 0x3BC  | 2    | 1             | Return button flag (0 = disable, non-zero = enable)                                                                                                |
| 0x3BE  | 1    | 1             | Blur background (0 = no, 1 = yes)                                                                                                                  |
| 0x3C0  | 4    | 20            | Offset of initial string in work buffer (or 0)                                                                                                     |
| 0x3C4  | 4    | 0             | Size of initial string in work buffer (bytes)                                                                                                      |
| 0x3C8  | 4    | 2024          | Offset of user dictionary in work buffer (or 0)                                                                                                    |
| 0x3CC  | 4    | 0             | Length of user dictionary (number of entries)                                                                                                      |
| 0x3D0  | 1    | 0             | [\#Text check](#Text_check "wikilink") enable                                                                                                      |
| 0x3D8  | 8    | 0             | [\#Text check](#Text_check "wikilink") callback function address. Not sure why this is included here                                               |
| 0x3E0  | 8    | \-1           |                                                                                                                                                    |
| 0x3E8  | 8    | \-1           |                                                                                                                                                    |
| 0x3F0  | 8    | \-1           |                                                                                                                                                    |
| 0x3F8  | 8    | \-1           |                                                                                                                                                    |

This struct is 0x3E0-bytes with version 0x5. Starting with version
0x30007 this struct is 0x400-bytes.

The 0x20-bytes at offset 0x3E0 is -1 normally, except for DownloadCodes.

Each entry in the user dictionary is 100 bytes long.

stringLenMax: When the input is too long, swkbd will stop accepting more
input until text is deleted via the B button (Backspace).

## Type

  - 0: Normal keyboard.
  - 1: Number pad. The buttons at the bottom left/right are only
    available when the characters at offset 0x16/0x18 are set.
  - 2: QWERTY (and variants) keyboard only.

## textDrawType

If the length limit (stringLenMax) is 1..32, the type specified by
textDrawType will be used. Otherwise, type1 will be used.

  - 0: The text will be displayed on a line. Also enables displaying the
    Header and Sub text.
  - 1: The text will be displayed in a box.
  - 2: Used for DownloadCodes on 5.0.0+.

### Key Set Disable Bitmask

Various bits in this field disable certain keys on the keyboard. This
list is incomplete.

    0x02: disable ' '
    0x04: disable '@'
    0x08: disable '%'
    0x10: disable '/'
    0x20: disable '\'
    0x40: disable numbers
    0x80: Used for DownloadCodes.
    0x100: Used for UserNames. Disables '@', '%', and '\'.

## Work Buffer

This is the third IStorage passed to this applet. It is a transfer
memory storage. The transfer memory should have size 0x1000 (0xd000 in
certain cases) and permissions 0.

The layout of the work buffer doesn't seem to matter as long as the
offsets in the [\#KeyboardConfig](#KeyboardConfig "wikilink") are
adjusted, but official code lays it out like this.

Prior to version 0x5, offset 0x0 size 0x14(20) is a header (size 0x10
for version \<=0x2).

| Offset         | Size    | Notes                 |
| -------------- | ------- | --------------------- |
| 20 (decimal)   | Unknown | UTF-16 initial string |
| 2024 (decimal) | Unknown | User dictionary       |

## Text Check

If text checking is enabled in
[\#KeyboardConfig](#KeyboardConfig "wikilink"), text will be checked
when the submit button is pressed. First, swkbd sends the text via
PushInteractiveOutData. Normally size 0x7D4 is allocated for the string.

| Offset | Size     | Notes       |
| ------ | -------- | ----------- |
| 0x0    | 0x8      | Buffer size |
| 0x8    | Variable | UTF-16 text |
|        |          |             |

The application then has an opportunity to validate or reject the text.
It creates a new IStorage, writes the response to it, and sends it via
PushInteractiveInData. This storage is 0x7D8-bytes.

| Offset | Size     | Notes                                        |
| ------ | -------- | -------------------------------------------- |
| 0x0    | 0x4      | TextCheckResult                              |
| 0x4    | Variable | UTF-16 error message (shown in a dialog box) |
|        |          |                                              |

TextCheckResult:

  - 0: Success, valid string.
  - 1: Failure, invalid string. Error message is displayed in a
    message-box, pressing OK will return to swkbd again.
  - 2: Failure, invalid string. Error message is displayed in a
    message-box, pressing Cancel will return to swkbd again, while
    pressing OK will continue as if the text was valid.
  - 3: Failure, invalid string. With value 3 and above, swkbd will
    silently not accept the string, without displaying any error.

## Output

When either the submit button is pressed and input has been validated,
or the user cancels the text entry, swkbd will push its response and
exit. The response IStorage has the following format. This storage is
0x7D8-bytes.

| Offset | Size     | Notes                            |
| ------ | -------- | -------------------------------- |
| 0x0    | 0x4      | Result code (0 = OK, 1 = Cancel) |
| 0x4    | Variable | UTF-16 text                      |
|        |          |                                  |

[Category:Library Applets](Category:Library_Applets "wikilink")

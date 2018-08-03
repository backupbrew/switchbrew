The software keyboard expects to be passed three
[IStorages](AM%20services#IStorage.md##IStorage "wikilink") via
[PushInData](AM%20services#ILibraryAppletAccessor.md##ILibraryAppletAccessor "wikilink").

## Common Arguments

The first IStorage passed to this applet should contain the common
library applet arguments. This is populated by
`nn::la::CommonArgumentsWriter` and has the following
format.

| Offset | Size | Typical Value | Notes                                                                                      |
| ------ | ---- | ------------- | ------------------------------------------------------------------------------------------ |
| 0x0    | 4    | 1             | Version field?                                                                             |
| 0x4    | 4    | 0x20          | Size field?                                                                                |
| 0x8    | 4    | 5             | Unknown                                                                                    |
| 0xC    | 4    | 0             | Theme color                                                                                |
| 0x10   | 1    | 0             | Unknown                                                                                    |
| 0x18   | 8    | N/A           | System tick (see [svcGetSystemTick](SVC#svcGetSystemTick.md##svcGetSystemTick "wikilink")) |
| 0x20   |      |               | End of struct                                                                              |

## KeyboardConfig

The second IStorage passed to this applet should contain the
configuration for the
keyboard.

| Offset | Size | Typical Value | Notes                                                                                                |
| ------ | ---- | ------------- | ---------------------------------------------------------------------------------------------------- |
| 0x0    | 4    | 2             |                                                                                                      |
| 0x4    | 18   | u"OK"         | UTF-16 text displayed in the submit button                                                           |
| 0x16   | 2    | 0             | UTF-16 "left optional symbol key"                                                                    |
| 0x18   | 2    | 0             | UTF-16 "right optional symbol key"                                                                   |
| 0x1A   | 1    | 0             |                                                                                                      |
| 0x1C   | 4    | 0             | Key set disable bitmask                                                                              |
| 0x20   | 4    | 1             | Initial cursor position (0 = start of string, 1 = end of string)                                     |
| 0x24   | 130  | u""           | UTF-16 header text                                                                                   |
| 0xA6   | 258  | u""           | UTF-16 sub text                                                                                      |
| 0x1A8  | 514  | u""           | UTF-16 guide text                                                                                    |
| 0x3AC  | 4    | 0             | String length limit (defaults to 500?)                                                               |
| 0x3B0  | 4    | 0             |                                                                                                      |
| 0x3B4  | 4    | 0             | Password flag (0 = not password, 1 = password)                                                       |
| 0x3B8  | 4    | 1             |                                                                                                      |
| 0x3BC  | 2    | 1             |                                                                                                      |
| 0x3BE  | 1    | 1             | Draw background (0 = no, 1 = yes)                                                                    |
| 0x3C0  | 4    | 20            | Offset of initial string in work buffer (or 0)                                                       |
| 0x3C4  | 4    | 0             | Size of initial string in work buffer (bytes)                                                        |
| 0x3C8  | 4    | 2024          | Offset of user dictionary in work buffer (or 0)                                                      |
| 0x3CC  | 4    | 0             | Length of user dictionary (number of entries)                                                        |
| 0x3D0  | 1    | 0             | [\#Text check](#Text_check "wikilink") enable                                                        |
| 0x3D8  | 8    | 0             | [\#Text check](#Text_check "wikilink") callback function address. Not sure why this is included here |
| 0x3E0  |      |               | End of struct                                                                                        |

If the length limit is \<= 32, the text entry box will be a single row
and show the header/sub text. Otherwise, it will use multiple rows and
the header/sub text will not be shown.

Each entry in the user dictionary is 100 bytes long.

### Key Set Disable Bitmask

Various bits in this field disable certain keys on the keyboard. This
list is incomplete.

    0x02: disable ' '
    0x04: disable '@'
    0x08: disable '%'
    0x10: disable '\' and '/'
    0x40: disable numbers
    0x80: used for download codes

## Work Buffer

This is the third IStorage passed to this applet. It is a transfer
memory storage. The transfer memory should have size 0x1000 (0xd000 in
certain cases) and permissions 0.

The layout of the work buffer doesn't seem to matter as long as the
offsets in the [\#KeyboardConfig](#KeyboardConfig "wikilink") are
adjusted, but official code lays it out like this.

| Offset         | Size    | Notes                 |
| -------------- | ------- | --------------------- |
| 20 (decimal)   | Unknown | UTF-16 initial string |
| 2024 (decimal) | Unknown | User dictionary       |

## Text Check

If text checking is enabled in
[\#KeyboardConfig](#KeyboardConfig "wikilink"), text will be checked
when the submit button is pressed. First, swkbd sends the text via
PushInteractiveOutData.

| Offset | Size     | Notes           |
| ------ | -------- | --------------- |
| 0x0    | 0x4      | Buffer size     |
| 0x4    | Variable | UTF-16 text     |
| 0x7d4  |          | Size of storage |

The application then has an opportunity to validate or reject the text.
It creates a new IStorage, writes the response to it, and sends it via
PushInteractiveInData.

| Offset | Size     | Notes                                        |
| ------ | -------- | -------------------------------------------- |
| 0x0    | 0x4      | Status (0 = OK, 1 = bad)                     |
| 0x4    | Variable | UTF-16 error message (shown in a dialog box) |
| 0x7d4  |          | Size of storage                              |

## Output

When either the submit button is pressed and input has been validated,
or the user cancels the text entry, swkbd will push its response and
exit. The response IStorage has the following format.

| Offset | Size     | Notes                            |
| ------ | -------- | -------------------------------- |
| 0x0    | 0x4      | Result code (0 = OK, 1 = Cancel) |
| 0x4    | Variable | UTF-16 text                      |
| 0x7d8  |          | Size of storage                  |

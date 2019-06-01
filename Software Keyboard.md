The software keyboard (swkbd) expects to be passed three
[IStorages](AM%20services#IStorage.md##IStorage "wikilink"). See also
[AM\_services\#Library\_Applets](AM%20services#Library%20Applets.md##Library_Applets "wikilink").

The below is for normal swkbd usage, see the
[\#InlineKeyboard](#InlineKeyboard "wikilink") section for
InlineKeyboard.

With version 0x6000B+ after pushing all other storage: when
[\#CustomizedDictionarySet](#CustomizedDictionarySet "wikilink") was
setup where buffer addr/size is set and total\_entries is non-zero,
[Applet\_Manager\_services\#CreateHandleStorage](Applet%20Manager%20services#CreateHandleStorage.md##CreateHandleStorage "wikilink")
will be used to create TransferMemory storage which is then pushed.

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
| \[6.0.0+\]     | 0x6000B  |
| \[8.0.0+\]     | 0x8000D  |

## KeyboardConfig

The second IStorage passed to this applet should contain the
configuration for the keyboard.

| Offset | Size | Typical Value | Notes                                                                                                                                              |
| ------ | ---- | ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 4    |               | Type                                                                                                                                               |
| 0x4    | 18   | 0             | UTF-16 text displayed in the submit button                                                                                                         |
| 0x16   | 2    | 0             | UTF-16 "left optional symbol key"                                                                                                                  |
| 0x18   | 2    | 0             | UTF-16 "right optional symbol key"                                                                                                                 |
| 0x1A   | 1    | 0             | Enables dictionary usage when non-zero (including the system dictionary).                                                                          |
| 0x1C   | 4    | 0             | [\#Key Set Disable Bitmask](#Key_Set_Disable_Bitmask "wikilink")                                                                                   |
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

Before version 0x6000B:

| Offset | Size | Typical Value | Notes                                                                                                                                                                             |
| ------ | ---- | ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x3D8  | 8    | 0             | [\#Text check](#Text_check "wikilink") callback function address. Removed with the struct used by 0x6000B+.                                                                       |
| 0x3E0  | 0x20 | \-1           | When set and enabled via textDrawType, controls displayed text grouping (inserts spaces, without affecting output string). Used for DownloadCodes, otherwise this is -1 normally. |

Version 0x6000B+:

| Offset | Size | Typical Value | Notes                                                                                                                                                                             |
| ------ | ---- | ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x3D4  | 0x20 | \-1           | When set and enabled via textDrawType, controls displayed text grouping (inserts spaces, without affecting output string). Used for DownloadCodes, otherwise this is -1 normally. |
| 0x3F4  | 0xC0 | 0             | [\#CustomizedDictionarySet](#CustomizedDictionarySet "wikilink") array data.                                                                                                      |
| 0x4B4  | 0x1  | 0             | Total array entries for [\#CustomizedDictionarySet](#CustomizedDictionarySet "wikilink").                                                                                         |
| 0x4B5  | 0x1  | 0             | \[8.0.0+\] Unknown                                                                                                                                                                |
| 0x4B6  | 0xD  | 0             | Padding                                                                                                                                                                           |
| 0x4C3  | 0x1  | 0             | \[8.0.0+\] Trigger                                                                                                                                                                |
| 0x4C4  | 0x4  | 0             | Padding                                                                                                                                                                           |

Struct sizes:

  - Initial version: 0x3E0-bytes.
  - Version 0x30007+: 0x400-bytes.
  - Version 0x6000B+: 0x4C8-bytes.

Each entry in the user dictionary is 100 bytes long.

stringLenMax: When the input is too long, swkbd will stop accepting more
input until text is deleted via the B button (Backspace).

### Type

  - 0: Normal keyboard.
  - 1: Number pad. The buttons at the bottom left/right are only
    available when the characters at offset 0x16/0x18 are set.
  - 2: QWERTY (and variants) keyboard only.

### textDrawType

If the length limit (stringLenMax) is 1..32, the type specified by
textDrawType will be used. Otherwise, type1 will be used.

  - 0: The text will be displayed on a line. Also enables displaying the
    Header and Sub text.
  - 1: The text will be displayed in a box.
  - 2: Used for DownloadCodes on 5.0.0+. Enables using the data starting
    at offset 0x3E0.

### Key Set Disable Bitmask

Various bits in this u32 field disable certain keys on the keyboard.

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

## InlineKeyboard

This doesn't run in the foreground and has completely different
input/output
[IStorages](AM%20services#IStorage.md##IStorage "wikilink"). This is
essentially an asynchronous version of the regular swkbd. Whether it
displays on the screen is controlled by the user-process. The
user-process can also get the gfx data via
[Display\_services](Display%20services.md "wikilink"). InlineKeyboard
was added with 2.0.0, however it wasn't added to sdk-nso until the
version corresponding to sysver 3.x (even though 2.0.0 system titles use
it).

### InitializeArg

| Offset | Size | Notes                                                                                                                                |
| ------ | ---- | ------------------------------------------------------------------------------------------------------------------------------------ |
| 0x0    | 0x4  | Unknown, normally 0.                                                                                                                 |
| 0x4    | 0x1  | Controls the LibraryAppletMode when launching the applet. Non-zero indicates LibraryAppletMode=0x1, otherwise LibraryAppletMode=0x3. |
| 0x5    | 0x1  | Set to 0x1 with \[5.0.0+\] in a separate init func by official sw, originally set to value 0.                                        |
| 0x6    | 0x2  | Padding                                                                                                                              |

### AppearArg

| Offset | Size | Notes                                                                                                                                           |
| ------ | ---- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x4  | Initialized to value 0x2.                                                                                                                       |
| 0x4    | 0x12 | UTF-16 string okButtonText                                                                                                                      |
| 0x16   | 2    | UTF-16 "left optional symbol key"                                                                                                               |
| 0x18   | 2    | UTF-16 "right optional symbol key"                                                                                                              |
| 0x1A   | 0x1  | Enables dictionary usage when non-zero (including the system dictionary).                                                                       |
| 0x1B   | 0x1  |                                                                                                                                                 |
| 0x1C   | 0x4  | [\#Key Set Disable Bitmask](#Key_Set_Disable_Bitmask "wikilink")                                                                                |
| 0x20   | 0x4  | s32, Unknown. Initialized to value -1.                                                                                                          |
| 0x24   | 0x4  | s32, Unknown. Initialized to value -1.                                                                                                          |
| 0x28   | 0x1  | Return button flag (0 = disable, non-zero = enable)                                                                                             |
| 0x29   | 0x2  |                                                                                                                                                 |
| 0x2B   | 0x1  |                                                                                                                                                 |
| 0x2C   | 0x4  | \[4.0.0+\] [\#CalcArg](#CalcArg "wikilink") flags bitmask 0x1000. In this field, bitmask 0x10000000 is used for DirectionalButtonAssignEnabled. |
| 0x30   | 0x1  | Initialized to value 1.                                                                                                                         |
| 0x31   | 0x17 |                                                                                                                                                 |

The above struct is cleared to 0 during initialization, besides the
fields specified otherwise.

\[6.0.0+\] Flags bitmask 0x10000 is set when
[\#CalcArg](#CalcArg "wikilink") trigger is set.

### CalcArg

| Offset | Size  | Flags bitmask                  | Notes                                                                                                                                                     |
| ------ | ----- | ------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x4   |                                | Set to 0x30000.                                                                                                                                           |
| 0x4    | 0x2   |                                | Size of this struct.                                                                                                                                      |
| 0x6    | 0x1   |                                | Unknown, set to value 0x1.                                                                                                                                |
| 0x7    | 0x1   |                                | Unknown, set to value 0x1.                                                                                                                                |
| 0x8    | 0x8   |                                | Flags                                                                                                                                                     |
| 0x10   | 0x8   | 0x1                            | [\#InitializeArg](#InitializeArg "wikilink")                                                                                                              |
| 0x18   | 0x4   | 0x2                            | float volume                                                                                                                                              |
| 0x1C   | 0x4   | 0x10                           | s32 cursorPos                                                                                                                                             |
| 0x20   | 0x48  |                                | [\#AppearArg](#AppearArg "wikilink")                                                                                                                      |
| 0x68   | 0x3F4 | 0x8                            | InputText UTF-16 string                                                                                                                                   |
| 0x45C  | 0x1   | 0x20                           | utf8Mode                                                                                                                                                  |
| 0x45D  | 0x1   |                                | Unknown                                                                                                                                                   |
| 0x45E  | 0x1   | 0x8000                         | \[5.0.0+\] enableBackspace                                                                                                                                |
| 0x45F  | 0x3   |                                | Unknown                                                                                                                                                   |
| 0x462  | 0x1   | 0x200                          | keytopAsFloating                                                                                                                                          |
| 0x463  | 0x1   | 0x100                          | footerScalable                                                                                                                                            |
| 0x464  | 0x1   | 0x100                          | alphaEnabledInInputMode                                                                                                                                   |
| 0x465  | 0x1   | 0x100                          | inputModeFadeType                                                                                                                                         |
| 0x466  | 0x1   | 0x200                          | disableTouch                                                                                                                                              |
| 0x467  | 0x1   | 0x800                          | disableUSBKeyboard                                                                                                                                        |
| 0x468  | 0x5   |                                | Unknown                                                                                                                                                   |
| 0x46D  | 0x2   |                                |                                                                                                                                                           |
| 0x46F  | 0x1   |                                |                                                                                                                                                           |
| 0x470  | 0x4   | 0x200                          | float keytopScale0                                                                                                                                        |
| 0x474  | 0x4   | 0x200                          | float keytopScale1                                                                                                                                        |
| 0x478  | 0x4   | 0x200                          | float keytopTranslate0                                                                                                                                    |
| 0x47C  | 0x4   | 0x200                          | float keytopTranslate1                                                                                                                                    |
| 0x480  | 0x4   | 0x100                          | float keytopBgAlpha                                                                                                                                       |
| 0x484  | 0x4   | 0x100                          | float footerBgAlpha                                                                                                                                       |
| 0x488  | 0x4   | 0x200                          | float balloonScale                                                                                                                                        |
| 0x48C  | 0x4   |                                | float, unknown                                                                                                                                            |
| 0x490  | 0xC   |                                |                                                                                                                                                           |
| 0x49C  | 0x1   | Enable=0x2000, disable=0x4000. | \[5.0.0+\] SeGroup (sound effect)                                                                                                                         |
| 0x49D  | 0x1   |                                | \[6.0.0+\] u8 triggerFlag, for [\#AppearArg](#AppearArg "wikilink"). Enables using the trigger field when set, this is only set when trigger is non-zero. |
| 0x49E  | 0x2   |                                | \[6.0.0+\] u8 trigger, for [\#AppearArg](#AppearArg "wikilink"). Official sw currently only uses value 0.                                                 |
| 0x49F  | 0x1   |                                | Padding                                                                                                                                                   |
|        |       |                                |                                                                                                                                                           |

This is 0x4A0-bytes.

All floats except for keytopTranslate0/keytopTranslate1 are initialized
to value 1.0f.

The applet-specific IStorage for data input is the
[\#InitializeArg](#InitializeArg "wikilink") within this struct.

### Runtime

Once the applet is running, official sw can call a func which does the
following:

  - Checks whether the applet exited via an event, then handles exit if
    so and returns.
  - Otherwise:
      - If the Flags field in the [\#CalcArg](#CalcArg "wikilink") state
        is non-zero, sends a Calc [\#Request](#Request "wikilink") then
        clears the Flags field.
      - Enters a loop which pops each applet Interactive output
        IStorage, reads 2 u32s from the [\#Reply](#Reply "wikilink")
        storage and processes the reply.
      - The u32 from offset 0x0 from the last processed storage is then
        returned as the retval.

### Request

| RequestCommand | Data Size | Name                        | Notes                                                                                                           |
| -------------- | --------- | --------------------------- | --------------------------------------------------------------------------------------------------------------- |
| 0x4            | 0x0       | Finalize                    |                                                                                                                 |
| 0x6            | Varies    | SetUserWordInfo             |                                                                                                                 |
| 0x7            | 0x70      | SetCustomizeDic             |                                                                                                                 |
| 0xA            | 0x4A0     | Calc                        | Data is [\#CalcArg](#CalcArg "wikilink").                                                                       |
| 0xB            | 0xD0      | SetCustomizedDictionaries   | Data is [\#CustomizedDictionarySet](#CustomizedDictionarySet "wikilink") with an additional 2-bytes of padding. |
| 0xC            | 0x0       | UnsetCustomizedDictionaries |                                                                                                                 |
| 0xD            | 0x1       | \[8.0.0+\]                  | Takes an input u8 bool which controls whether ChangedString\*V2 or ChangedString\* replies should be used.      |
| 0xE            | 0x1       | \[8.0.0+\]                  | Takes an input u8 bool which controls whether MovedCursor\*V2 or MovedCursor\* replies should be used.          |

Requests are sent via an applet Interactive input IStorage: the u32 at
offset 0x0 is the RequestCommand, and the rest of the storage is the
request-specific data. While swkbd supports other requests, official sw
only uses requests 0x4, 0x7, and 0xA.

### Reply

| ReplyType          | Data Size   | Name                        | Notes                                                                                               |
| ------------------ | ----------- | --------------------------- | --------------------------------------------------------------------------------------------------- |
| 0x0                | 0x1         | FinishedInitialize          | Reply data is ignored by the user-process.                                                          |
| 0x1 / default case | 0x0         |                             | Official sw has no handling for this besides just closing the storage.                              |
| 0x2                | 0x3FC       | ChangedString               |                                                                                                     |
| 0x3                | 0x3F4       | MovedCursor                 |                                                                                                     |
| 0x4                | 0x3F4       | MovedTab                    |                                                                                                     |
| 0x5                | 0x3F0       | DecidedEnter                |                                                                                                     |
| 0x6                | 0x0         | DecidedCancel               |                                                                                                     |
| 0x7                | 0x7E4       | ChangedStringUtf8           |                                                                                                     |
| 0x8                | 0x7DC       | MovedCursorUtf8             |                                                                                                     |
| 0x9                | 0x7D8       | DecidedEnterUtf8            |                                                                                                     |
| 0xA                | 0x0         | UnsetCustomizeDic           | Official sw clears a flag related to CustomizeDic, then runs the same handling code as 0x1/default. |
| 0xB                | 0x0         | ReleasedUserWordInfo        |                                                                                                     |
| 0xC                | 0x0         | UnsetCustomizedDictionaries | \[6.0.0+\] Official sw handles this the same as UnsetCustomizeDic.                                  |
| 0xD                | 0x7E4 + 0x1 | ChangedStringV2             | \[8.0.0+\]                                                                                          |
| 0xE                | 0x7DC + 0x1 | MovedCursorV2               | \[8.0.0+\]                                                                                          |
| 0xF                | 0x3FC + 0x1 | ChangedStringUtf8V2         | \[8.0.0+\]                                                                                          |
| 0x10               | 0x3F4 + 0x1 | MovedCursorUtf8V2           | \[8.0.0+\]                                                                                          |
|                    |             |                             |                                                                                                     |

See [\#Runtime](#Runtime "wikilink"). In the storage, the first u32 is
the State, while the second u32 is the ReplyType. The rest is the
reply-specific data.

The replies with name "\*Utf8" contain an UTF-8 string in the reply
data, while the other replies contain an UTF-16 string. These are
identical besides the string encoding.

Reply data format:

  - ChangedString\*: +0 = string. Last 0x10-bytes: 4 u32s, where the
    first one is the length of the string in characters, without
    NUL-terminator. The last u32 is cursorPos. The other 2 fields are
    s32s.
  - MovedCursor\*: +0 = string. Last 0x8-bytes: 2 u32s, where the first
    one is the stringLen, and the second one is cursorPos.
  - DecidedEnter\*: +0 = string. The last u32 is the stringLen.
  - \*V2: See above. Last byte: u8 bool, passed to the callback as
    `flag==0`.

## CustomizedDictionarySet

| Offset | Size          | Description                                           |
| ------ | ------------- | ----------------------------------------------------- |
| 0x0    | 0x8           | 0x1000-byte aligned buffer address.                   |
| 0x8    | 0x4           | 0x1000-byte aligned buffer size.                      |
| 0xC    | 0x18\*4(0xC0) | Array of 0x18 entries, where each entry is 0x8-bytes. |
| 0xCC   | 0x2           | u16 total\_entries                                    |

This was added with \[6.0.0+\]. This struct is 0xCE-bytes.

[Category:Library Applets](Category:Library_Applets "wikilink")

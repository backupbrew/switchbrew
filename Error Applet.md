This is the applet presented when a title displays an error message. See
[AM\_services\#Library\_Applets](AM%20services#Library%20Applets.md##Library_Applets "wikilink").

All errors displayed by this applet get logged and can be viewed under
'Settings' \> 'Support' \> 'Error History'.

On pre-5.0.0 the specified LanguageCode has to be valid, otherwise a
fatal-error is thrown. With \[5.0.0+\] it will use en-US when the
LanguageCode is invalid.

## ErrorContext

| Offset | Size  | Description |
| ------ | ----- | ----------- |
| 0x0    | 0x200 | ?           |

## ErrorCommonHeader

| Offset | Size | Description                                                                                                                        |
| ------ | ---- | ---------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x1  | u8 type                                                                                                                            |
| 0x1    | 0x1  | u8 unk\_x1                                                                                                                         |
| 0x2    | 0x3  | ?                                                                                                                                  |
| 0x5    | 0x1  | \[4.0.0+\] u8 contextFlag. When set indicates that an additional storage is pushed for [\#ErrorContext](#ErrorContext "wikilink"). |
| 0x6    | 0x1  | u8 resultFlag. ErrorCommonArg: When clear, ErrorCode is used, otherwise the applet generates the error-code from res.              |
| 0x7    | 0x1  | ?                                                                                                                                  |

## ErrorCommonArg

| Offset | Size | Description                          |
| ------ | ---- | ------------------------------------ |
| 0x0    | 0x8  | ErrorCommonHeader                    |
| 0x8    | 0x8  | [\#ErrorCode](#ErrorCode "wikilink") |
| 0x10   | 0x4  | Result res                           |

## SystemErrorArg

| Offset | Size  | Description                                                                                                                 |
| ------ | ----- | --------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x8   | ErrorCommonHeader. type=1.                                                                                                  |
| 0x8    | 0x8   | [\#ErrorCode](#ErrorCode "wikilink")                                                                                        |
| 0x10   | 0x8   | [LanguageCode](Settings%20services.md "wikilink")                                                                           |
| 0x18   | 0x800 | UTF-8 string dialogMessage                                                                                                  |
| 0x818  | 0x800 | UTF-8 string fullscreenMessage, displayed when the user clicks on "Details". When not set this disables displaying Details. |

This struct is
0x1018-bytes.

## ApplicationErrorArg

| Offset | Size  | Description                                                                                                                 |
| ------ | ----- | --------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x8   | ErrorCommonHeader. type=2 and unk\_x1=1.                                                                                    |
| 0x8    | 0x4   | u32 errorNumber. Raw decimal error number which is displayed in the dialog.                                                 |
| 0xC    | 0x8   | [LanguageCode](Settings%20services.md "wikilink")                                                                           |
| 0x14   | 0x800 | UTF-8 string dialogMessage                                                                                                  |
| 0x814  | 0x800 | UTF-8 string fullscreenMessage, displayed when the user clicks on "Details". When not set this disables displaying Details. |

This struct is 0x1014-bytes.

## ErrorCode

This is an u64 containing the [error-code](Error%20codes.md "wikilink"):
the low u32 is the module portion which is normally set to `module
+ 2000`, and the high u32 is the error description.

## ResultBacktrace

| Offset | Size                | Description       |
| ------ | ------------------- | ----------------- |
| 0x0    | 0x4                 | s32 total entries |
| 0x4    | 0x4\*total\_entries | Array of Result   |

## Usage

User-processes should push a common arguments struct (version=0) as well
as the Arg struct. Once the applet finishes running successfully, it may
return an output storage in some cases. An u8 status value is located at
+1, where non-zero indicates error.

[Category:Library Applets](Category:Library_Applets "wikilink")

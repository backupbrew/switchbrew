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

| Offset | Size | Description                                                                                                                                                                                                                                                    |
| ------ | ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x1  | u8 type                                                                                                                                                                                                                                                        |
| 0x1    | 0x1  | u8 jumpFlag. When clear, this indicates WithoutJump.                                                                                                                                                                                                           |
| 0x2    | 0x3  | ?                                                                                                                                                                                                                                                              |
| 0x5    | 0x1  | u8 contextFlag. When set with type=0, indicates that an additional storage is pushed for [\#ResultBacktrace](#ResultBacktrace "wikilink"). \[4.0.0+\]: When set indicates that an additional storage is pushed for [\#ErrorContext](#ErrorContext "wikilink"). |
| 0x6    | 0x1  | u8 resultFlag. [\#ErrorCommonArg](#ErrorCommonArg "wikilink"): When clear, ErrorCode is used, otherwise the applet generates the error-code from res.                                                                                                          |
| 0x7    | 0x1  | u8 contextFlag2. Similar to contextFlag except for [\#ErrorCommonArg](#ErrorCommonArg "wikilink"), indicating [\#ErrorContext](#ErrorContext "wikilink") is used.                                                                                              |

## ErrorCommonArg

| Offset | Size | Description                          |
| ------ | ---- | ------------------------------------ |
| 0x0    | 0x8  | ErrorCommonHeader                    |
| 0x8    | 0x8  | [\#ErrorCode](#ErrorCode "wikilink") |
| 0x10   | 0x4  | Result res                           |

## ErrorPctlArg

| Offset | Size | Description                |
| ------ | ---- | -------------------------- |
| 0x0    | 0x8  | ErrorCommonHeader. type=4. |
| 0x8    | 0x4  | Result res                 |

This struct is 0xC-bytes. Used instead of
[\#ErrorCommonArg](#ErrorCommonArg "wikilink") where a Result error
would have been displayed with type=0, for module=PCTL errors with desc
100-119. For this the applet will display the following dialog (without
report logging): "This software is restricted by Parental Controls".

## ErrorEulaData

| Offset | Size    | Description |
| ------ | ------- | ----------- |
| 0x0    | 0x20000 | data        |

## ErrorEulaArg

| Offset | Size | Description                                     |
| ------ | ---- | ----------------------------------------------- |
| 0x0    | 0x8  | ErrorCommonHeader. jumpFlag = 1.                |
| 0x8    | 0x4  | [RegionCode](Settings%20services.md "wikilink") |

This struct is 0xC-bytes.

  - Eula: ErrorCommonHeader.type = 3. Displays the EULA.
  - SystemUpdateEula: ErrorCommonHeader.type = 8. Displays the
    system-update EULA. Uses an additional IStorage containing
    [\#ErrorEulaData](#ErrorEulaData "wikilink"), from
    [Applet\_Manager\_services\#CreateTransferMemoryStorage](Applet%20Manager%20services#CreateTransferMemoryStorage.md##CreateTransferMemoryStorage "wikilink")
    with flag=false.

## ErrorRecordArg

| Offset | Size | Description                               |
| ------ | ---- | ----------------------------------------- |
| 0x0    | 0x8  | ErrorCommonHeader. type=5 and jumpFlag=1. |
| 0x8    | 0x8  | [\#ErrorCode](#ErrorCode "wikilink")      |
| 0x10   | 0x8  | u64 POSIX timestamp                       |

The applet does not log an error report for this. Used by
[qlaunch](Qlaunch.md "wikilink") for viewing previously logged errors
via the "View the Error"
button.

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
| 0x0    | 0x8   | ErrorCommonHeader. type=2 and jumpFlag=1.                                                                                   |
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

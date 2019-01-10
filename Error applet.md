The error applet is used to display an error result by several titles
and applets. (AppletId 0xE)

Depending on the type, the applet will display the error in several
ways.

It takes two input storages: common arguments and a custom storage.

## Error applet types

### Error (common one)

Takes a CommonArgs storage with version 0.

#### Custom storage

Unknown exact size, using size 20 seems to work fine.

The type (byte 0 of this storage) is
0.

| Offset | Size    | Typical Value | Notes                                            |
| ------ | ------- | ------------- | ------------------------------------------------ |
| 0x10   | 4 (u32) | 0 (2000-0000) | Result code, same Result used everywhere in HOS. |

The error will display error code 2000-0000 if the Result is not set.
The text is the default one.

### SystemError

Takes a CommonArgs storage with version 0.

#### Custom storage

SDK uses size 4120 for this storage.

The type (byte 0 of this storage) is
1.

| Offset | Size    | Typical Value | Notes                                                                       |
| ------ | ------- | ------------- | --------------------------------------------------------------------------- |
| 0x8    | 8 (u64) | 0 (0000-0000) | ErrorCode (not Result like in normal errors) of the error to use.           |
| 0x18   | 0x800   | \-            | String of the text to be shown as a short description of the error.         |
| 0x818  | 0x800   | \-            | String of the text to be shown as a more detailed description of the error. |

If the first text is not specified but the second one is, the applet
will directly load the "Details" display with the second error text.

If both texts are set, the applet will load the dialog with "Close" and
"Details" options, and will load the display mentiones above after
selecting "Details".

If no ErrorCode is supplied, the applet will use 0000-0000.

### ApplicationError

Apparently similar to SystemError, has type (byte 0 of the second
storage) 258, with almost same offsets.

More info needs to be added about this type.

The error applet is used to display an error result by several titles
and applets. (AppletId 0xE)

A dialog is displayed with the error code at the top, and with support
text plus a support page link in the dialog.

It takes two input storages: common arguments and a custom storage.

## Common arguments

Version 0 according to official usage.

## Error storage

Has size 20.

Apparently, the layout is changed by setting different values to the
first byte.

The error code is an u32/Result located at offset 16.

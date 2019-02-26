This is the applet presented when a title displays an error message. See
[AM\_services\#Library\_Applets](AM%20services#Library%20Applets.md##Library_Applets "wikilink").
The error applet expects three
[IStorage](AM%20services#IStorage.md##IStorage "wikilink") inputs and no
output.

## ErrorConfig

This has size 0x1018 and contains the error code, a short description of
the error and a more detailed description of the error, displayed when
the user clicks on "Details". Typically, all unused values can be set to
zero. The first should be set to 1 if a custom error message is to be
displayed. Otherwise, a default error message will be shown.

The error code is stored at offsets 0x8, containing the first part of
the code, and 0xC, containing the second part of the code. Those values
are expected to be u64's.

The short description of the error is stored as a char\* at offset 0x18,
the long description of the error is stored as a char\* at offset 0x818.

## Usage

User-processes should push a common arguments struct as well as the
typical ErrorConfig struct. Since the error applet doesn't have any
output, user-processes can then directly join the applet and wait for it
to finish.

[Category:Library Applets](Category:Library_Applets "wikilink")

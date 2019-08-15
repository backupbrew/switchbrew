This is the applet presented when launching a game that allows the user
to select a user.

See
[AM\_services\#Library\_Applets](AM%20services#Library%20Applets.md##Library_Applets "wikilink").
The profile selector expects a two
[IStorage](AM%20services#IStorage.md##IStorage "wikilink") inputs and a
single [IStorage](AM%20services#IStorage.md##IStorage "wikilink")
output.

## UserSelectionConfig

This has size 0xA0 and seems to only affect the UI display. Typical
value is all zero with byte 0x96 equal to 0x01. Setting the first byte
to 1 will make the applet display in order to create a new user.
"starter" sets the first byte to 5 in order to display initial user
setup.

## Result

This is 0x18-bytes.

| Offset | Size | Notes                             |
| ------ | ---- | --------------------------------- |
| 0x0    | 0x8  | Result (0 = Success, 2 = Failure) |
| 0x8    | 0x10 | UUID of selected user             |
|        |      |                                   |

## Usage

User-processes should push a common arguments struct and the typical
UserSelectionConfig struct as well. After pushing in the data and
calling start, user-processes should wait upon the PopOutDataEvent and
then pop a single IStorage to obtain the result structure described
above.

[Category:Library Applets](Category:Library_Applets "wikilink")

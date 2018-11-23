This is the UX presented when launching a game that allows the user to
select a user.

The profile selector expects a two
[IStorage](AM%20services#IStorage.md##IStorage "wikilink") inputs and a
single [IStorage](AM%20services#IStorage.md##IStorage "wikilink")
output.

The first IStorage is identical to [Common
Arguments](Software%20Keyboard#Common%20Arguments.md##Common_Arguments "wikilink")
from swkbd.

## UserSelectionConfig

This has size 0xA0 and seems to only affect the UI display. Typical
value is all zero with byte 0x96 equal to 0x01

## Result

| Offset | Size | Notes                             |
| ------ | ---- | --------------------------------- |
| 0x0    | 0x8  | Result (0 = Success, 2 = Failure) |
| 0x8    | 0x10 | UUID of selected user             |
| 0x18   |      | End of Struct                     |

## Usage

Homebrew should push a common arguments struct and the typical
UserSelectionConfig struct as well. After pushing in the data and
calling start, homebrew should wait upon the PopOutDataEvent and then
pop a single IStorage to obtain the result structure described above.

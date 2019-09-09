This is the Album (`PhotoViewer`) applet launched by Home Menu. See
[AM\_services\#Library\_Applets](AM%20services#Library%20Applets.md##Library_Applets "wikilink").

## Usage

User-processes should push a common arguments struct (version=0x10000)
as well as `u8 arg`. See below for the commonargs PlayStartupSound flag
value. After starting the applet, official sw immediately closes it (no
output storage is handled).

| Name                           | Arg value | PlayStartupSound | Description                                                                                                          |
| ------------------------------ | --------- | ---------------- | -------------------------------------------------------------------------------------------------------------------- |
| `ShowAlbumFiles`               | 0         | false            | Only displays AlbumFiles associated with the title which launched the Album applet, with the filter button disabled. |
| `ShowAllAlbumFiles`            | 1         | false            | Displays all AlbumFiles, with filtering allowed.                                                                     |
| `ShowAllAlbumFilesForHomeMenu` | 2         | true             | Similar to ShowAllAlbumFiles.                                                                                        |

[Category:Library Applets](Category:Library_Applets "wikilink")

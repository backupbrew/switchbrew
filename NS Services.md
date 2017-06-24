This is the Switch equivalent of
[this](https://3dbrew.org/wiki/NS_and_APT_Services).

# ns:am

| Cmd  | Name                                                                     |
| ---- | ------------------------------------------------------------------------ |
| 0    | [\#GetTitlesInfo](#GetTitlesInfo "wikilink")                             |
| 1    |                                                                          |
| 2    |                                                                          |
| 3    |                                                                          |
| 4    |                                                                          |
| 5    |                                                                          |
| 6    |                                                                          |
| 7    |                                                                          |
| 8    |                                                                          |
| 9    |                                                                          |
| 11   |                                                                          |
| 13   |                                                                          |
| 16   |                                                                          |
| 17   |                                                                          |
| 19   |                                                                          |
| 21   | [\#GetTitlePatchContentNcaPath](#GetTitlePatchContentNcaPath "wikilink") |
| 22   |                                                                          |
| 23   |                                                                          |
| 25   |                                                                          |
| 27   |                                                                          |
| 30   |                                                                          |
| 31   |                                                                          |
| 33   |                                                                          |
| 35   |                                                                          |
| 36   |                                                                          |
| 37   |                                                                          |
| 38   |                                                                          |
| 39   |                                                                          |
| 40   |                                                                          |
| 41   |                                                                          |
| 42   |                                                                          |
| 43   |                                                                          |
| 44   |                                                                          |
| 45   |                                                                          |
| 46   |                                                                          |
| 47   | [\#GetFreeSpace](#GetFreeSpace "wikilink")                               |
| 48   | [\#GetTotalSpace](#GetTotalSpace "wikilink")                             |
| 49   |                                                                          |
| 52   |                                                                          |
| 53   |                                                                          |
| 54   |                                                                          |
| 55   |                                                                          |
| 56   |                                                                          |
| 57   |                                                                          |
| 58   |                                                                          |
| 59   |                                                                          |
| 60   | GetLanguageIdFromString                                                  |
| 61   |                                                                          |
| 62   |                                                                          |
| 63   |                                                                          |
| 64   |                                                                          |
| 65   |                                                                          |
| 100  | InitializeNXFileSystem?                                                  |
| 101  | ? Seems to wipe filesystem but keeps some data (savegames? users?)       |
| 102  |                                                                          |
| 200  |                                                                          |
| 201  |                                                                          |
| 210  |                                                                          |
| 220  |                                                                          |
| 300  |                                                                          |
| 301  |                                                                          |
| 302  |                                                                          |
| 303  |                                                                          |
| 304  |                                                                          |
| 305  |                                                                          |
| 306  |                                                                          |
| 307  |                                                                          |
| 401  |                                                                          |
| 402  |                                                                          |
| 403  |                                                                          |
| 404  |                                                                          |
| 405  |                                                                          |
| 502  |                                                                          |
| 503  |                                                                          |
| 504  |                                                                          |
| 600  |                                                                          |
| 601  | [\#GetTitleInfo1](#GetTitleInfo1 "wikilink")                             |
| 602  |                                                                          |
| 603  |                                                                          |
| 604  |                                                                          |
| 605  | Used same way as [\#GetTitleInfo1](#GetTitleInfo1 "wikilink").           |
| 700  |                                                                          |
| 701  |                                                                          |
| 702  |                                                                          |
| 703  |                                                                          |
| 704  |                                                                          |
| 705  |                                                                          |
| 800  |                                                                          |
| 801  |                                                                          |
| 900  |                                                                          |
| 901  |                                                                          |
| 902  |                                                                          |
| 903  |                                                                          |
| 904  |                                                                          |
| 905  |                                                                          |
| 906  |                                                                          |
| 907  |                                                                          |
| 908  |                                                                          |
| 1000 |                                                                          |
| 1001 |                                                                          |
| 1200 |                                                                          |
| 1300 |                                                                          |
| 1301 |                                                                          |
| 1302 |                                                                          |
| 1400 |                                                                          |
| 1500 |                                                                          |
| 1501 |                                                                          |
| 1502 |                                                                          |
| 1503 |                                                                          |
| 1600 |                                                                          |
| 1700 |                                                                          |
| 1800 |                                                                          |
| 1801 |                                                                          |
| 1802 |                                                                          |

## GetTitlePatchContentNcaPath

Takes a 0x16-type output buffer, an u8 [type](NCA.md "wikilink"), and an
u64 titleID.

The input titleID is used with the application-title table like various
other cmds, anything not in that table can't be used with this.

Returns a string path for the specified type of patch content with this
titleID, otherwise returns regular-application paths when update-title
not installed. Returns an error when the specified type of content
doesn't exist for this title. Starts with
"@{SdCardContent,UserContent}://" and ends in ".nca".

For gamecard content, the output path is: "@GcS00000002:/<NcaId>.nca".
NCA-type0 with gamecard returns 0 with an empty output string.

The output string is then used by the user-process with
[FS](Filesystem%20services.md "wikilink") to mount the content.

## GetFreeSpace

Takes an input media-id that must be 5.

Returns the u64 from
[Content\_Manager\_services\#IContentStorage](Content%20Manager%20services#IContentStorage.md##IContentStorage "wikilink")
cmd22.

## GetTotalSpace

Takes an input media-id that must be 5.

Returns the u64 from
[Content\_Manager\_services\#IContentStorage](Content%20Manager%20services#IContentStorage.md##IContentStorage "wikilink")
cmd23.

## GetTitlesInfo

Takes a type-6 output buffer and an u64.

Returns an array of title-info entries using the specified offset and
size. No input titleID is passed to this.

## GetTitleInfo1

Returns 0x10-byte entries using the specified titleID starting at the
specified u32 entryindex. Can only return game titles. The second entry
if any is the update-title usually. When the input entryindex is \>=
totalentries, this will return 0 with out\_entrycount=0.

Entry
structure:

| Offset | Size | Description                                                                                          |
| ------ | ---- | ---------------------------------------------------------------------------------------------------- |
| 0x0    | 0x1  | u8 "type". [Title type](Content%20Manager%20services.md "wikilink") (String is from web-applet)      |
| 0x1    | 0x1  | u8 "installedStorage" / [StorageId](Filesystem%20services.md "wikilink") (String is from web-applet) |
| 0x2    | 0x1  | Unknown. Non-zero with output from cmd 605, differs for app/update titles.                           |
| 0x3    | 0x1  | Padding                                                                                              |
| 0x4    | 0x4  | u32 Title-version                                                                                    |
| 0x8    | 0x8  | u64 titleID                                                                                          |

# ns:su

# ns:dev

| Cmd | Name           |
| --- | -------------- |
| 0   | LaunchTitle    |
| 1   | TerminateTitle |
| 2   |                |
| 3   |                |
| 4   |                |
| 5   |                |
| 6   |                |
| 7   |                |
| 8   |                |
| 9   |                |

# Enums

### AppletId

| ID   | Description                                                                                                                                                          |
| ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x02 | Unknown (throws fatal error 2128-0203)                                                                                                                               |
| 0x03 | Unknown (throws fatal error 2128-0203)                                                                                                                               |
| 0x04 | Unknown (throws fatal error 2128-0203)                                                                                                                               |
| 0x0C | Unknown (blinks the screen)                                                                                                                                          |
| 0x0D | Unknown (displays "Checking for free space...")                                                                                                                      |
| 0x0E | ErrorApplet                                                                                                                                                          |
| 0x0F | NetworkSelect                                                                                                                                                        |
| 0x10 | PlayerSelect                                                                                                                                                         |
| 0x11 | Swkbd (on-screen keyboard)                                                                                                                                           |
| 0x13 | [WebApplet](Internet%20Browser.md "wikilink") From WebApplet string: "aInfo.appletId == ::nn::applet::AppletId\_LibraryAppletWeb".                                   |
| 0x14 | Ec ([ShopN](Internet%20Browser.md "wikilink")) From ShopN string: "aInfo.appletId == ::nn::applet::AppletId\_LibraryAppletShop".                                     |
| 0x15 | Album                                                                                                                                                                |
| 0x18 | [Whitelisted](Internet%20Browser.md "wikilink") web-applet (From whitelisted web-applet string: "aInfo.appletId == ::nn::applet::AppletId\_LibraryAppletLoginShare") |
| 0x19 | [WifiWebAuth](Internet%20Browser.md "wikilink") (From browser string: "aInfo.appletId == ::nn::applet::AppletId\_LibraryAppletWifiWebAuth")                          |

This seems to be the equivalent of
[this](https://3dbrew.org/wiki/NS_and_APT_Services#AppIDs).

### ShimKind

This is from strings and code in the [
web-applets](Internet%20Browser.md "wikilink").

This indicates the type of web-applet.

| shimKind value | Description       |
| -------------- | ----------------- |
| 2              | LoginApplet       |
| 4              | ShareApplet       |
| 5              | WebApplet         |
| 6              | WifiWebAuthApplet |
| 7              | LobbyApplet       |

[Category:Services](Category:Services "wikilink")

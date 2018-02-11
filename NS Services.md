# aoc:u

This is "nn::aocsrv::detail::IAddOnContentManager".

| Cmd | Name                                 |
| --- | ------------------------------------ |
| 0   | CountAddOnContentByApplicationId     |
| 1   | ListAddOnContentByApplicationId      |
| 2   | CountAddOnContent                    |
| 3   | ListAddOnContent                     |
| 4   | GetAddOnContentBaseIdByApplicationId |
| 5   | GetAddOnContentBaseId                |
| 6   | PrepareAddOnContentByApplicationId   |
| 7   | PrepareAddOnContent                  |
|     |                                      |

# ns:am

| Cmd  | Name                                                                     |
| ---- | ------------------------------------------------------------------------ |
| 0    | [\#ListApplicationRecord](#ListApplicationRecord "wikilink")             |
| 1    |                                                                          |
| 2    | GetApplicationRecordUpdateSystemEvent                                    |
| 3    | SubmitArpData                                                            |
| 4    |                                                                          |
| 5    |                                                                          |
| 6    |                                                                          |
| 7    |                                                                          |
| 8    | IsApplicationEntityMovable                                               |
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
| 30   | GetIAsyncValue                                                           |
| 31   | GetIAsyncResult                                                          |
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
| 44   | GetSdCardMountStatusChangedEvent                                         |
| 45   | GetGameCardAttachmentEvent                                               |
| 46   | GetGameCardAttachmentInfo                                                |
| 47   | [\#GetFreeSpace](#GetFreeSpace "wikilink")                               |
| 48   | [\#GetTotalSpace](#GetTotalSpace "wikilink")                             |
| 49   | GetSdCardRemovedEvent                                                    |
| 52   | GetGameCardUpdateDetectionEvent                                          |
| 53   |                                                                          |
| 54   |                                                                          |
| 55   | GetApplicationDesiredLanguage                                            |
| 56   |                                                                          |
| 57   |                                                                          |
| 58   |                                                                          |
| 59   | ConvertApplicationLanguageToLanguageCode                                 |
| 60   | [\#GetLanguageIdFromString](#GetLanguageIdFromString "wikilink")         |
| 61   |                                                                          |
| 62   | GetIGameCardStopper                                                      |
| 63   | IsSystemProgramInstalled                                                 |
| 64   |                                                                          |
| 65   | GetIRequestServerStopper                                                 |
| 100  | ResetToFactorySettings                                                   |
| 101  | ResetToFactorySettingsWithoutUserSaveData                                |
| 102  | DeleteUserContent2                                                       |
| 200  |                                                                          |
| 201  |                                                                          |
| 210  |                                                                          |
| 220  |                                                                          |
| 300  | GetApplicationShellEvent                                                 |
| 301  | PopApplicationShellEventInfo                                             |
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

For gamecard content, the output path is: "@GcSXXXXXXXX:/<NcaId>.nca".
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

## GetLanguageIdFromString

Takes an input u8 pointer for the resulting Id to be written to and a
string represented as a u64 (i.e 0x53552D6E65 for 'en-US').

Returns 0 if an ID was successfully found, otherwise returns 0x25810.

## ListApplicationRecord

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

This is "nn::ns::detail::ISystemUpdateInterface".

| Cmd | Name                    |
| --- | ----------------------- |
| 0   |                         |
| 1   | GetISystemUpdateControl |
| 2   |                         |
| 3   |                         |
| 4   |                         |
| 5   |                         |
| 6   |                         |
| 9   | GetNsSuWaitEvent        |
| 10  |                         |
| 11  |                         |
| 12  |                         |
| 13  |                         |
|     |                         |

# ns:dev

This is
"nn::ns::detail::IDevelopInterface".

| Cmd | Name                                                             |
| --- | ---------------------------------------------------------------- |
| 0   | [\#LaunchTitle](#LaunchTitle "wikilink")                         |
| 1   | [\#TerminateTitleByPid](#TerminateTitleByPid "wikilink")         |
| 2   | [\#TerminateTitleByTitleId](#TerminateTitleByTitleId "wikilink") |
| 3   | [\#GetNsDevWaitEvent](#GetNsDevWaitEvent "wikilink")             |
| 4   | [\#GetNsDevEventType](#GetNsDevEventType "wikilink")             |
| 5   | [\#TerminateCrashingTitle](#TerminateCrashingTitle "wikilink")   |
| 6   | [\#InstallTitle](#InstallTitle "wikilink")                       |
| 7   | SetEventState6                                                   |
| 8   | SetEventState                                                    |
|     |                                                                  |

## LaunchTitle

Wrapper for "pm:shell"
[LaunchProcess](Process%20Manager%20services#LaunchProcess.md##LaunchProcess "wikilink").

## TerminateTitleByPid

Wrapper for "pm:shell"
[TerminateTitleByPid](Process%20Manager%20services#TerminateTitleByPid.md##TerminateTitleByPid "wikilink").

## TerminateTitleByTitleId

Wrapper for "pm:shell"
[TerminateTitleByTitleId](Process%20Manager%20services#TerminateTitleByTitleId.md##TerminateTitleByTitleId "wikilink").

## GetNsDevWaitEvent

Wrapper for "pm:shell"
[GetProcessEventWaiter](Process%20Manager%20services#GetProcessEventWaiter.md##GetProcessEventWaiter "wikilink").

## GetNsDevEventType

Wrapper for "pm:shell"
[GetProcessEventType](Process%20Manager%20services#GetProcessEventType.md##GetProcessEventType "wikilink").

## TerminateCrashingTitle

Calls "pm:shell"
[GetCrashingProcessPid](Process%20Manager%20services#GetCrashingProcessPid.md##GetCrashingProcessPid "wikilink")
and sends PID to
[TerminateTitleByPid](Process%20Manager%20services#TerminateTitleByPid.md##TerminateTitleByPid "wikilink").

## InstallTitle

Calls
[IPathResolverForStorage](NCM%20services#IPathResolverForStorage.md##IPathResolverForStorage "wikilink")
Set...NcaPath functions.

[Category:Services](Category:Services "wikilink")

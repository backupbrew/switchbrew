# aoc:u

This is "nn::aocsrv::detail::IAddOnContentManager".

| Cmd | Name                                                                          |
| --- | ----------------------------------------------------------------------------- |
| 0   | \[1.0.0-6.2.0\] CountAddOnContentByApplicationId                              |
| 1   | \[1.0.0-6.2.0\] ListAddOnContentByApplicationId                               |
| 2   | CountAddOnContent                                                             |
| 3   | ListAddOnContent                                                              |
| 4   | \[1.0.0-6.2.0\] GetAddOnContentBaseIdByApplicationId                          |
| 5   | GetAddOnContentBaseId                                                         |
| 6   | \[1.0.0-6.2.0\] PrepareAddOnContentByApplicationId                            |
| 7   | PrepareAddOnContent                                                           |
| 8   | \[4.0.0+\] GetAddOnContentListChangedEvent                                    |
| 100 | \[7.0.0+\] [CreateEcPurchasedEventManager](#IPurchaseEventManager "wikilink") |

## IPurchaseEventManager

This is "nn::ec::IPurchaseEventManager".

| Cmd | Name                            |
| --- | ------------------------------- |
| 0   | SetDefaultDeliveryTarget        |
| 1   | SetDeliveryTarget               |
| 2   | GetPurchasedEventReadableHandle |
| 3   | PopPurchasedProductInfo         |

# ns:am

This is "nn::ns::detail::IApplicationManagerInterface".

\[3.0.0+\] This service was replaced by
[ns:am2](#ns:am2,_ns:ec,_ns:rid,_ns:rt,_ns:web "wikilink").

| Cmd  | Name                                                                                               |
| ---- | -------------------------------------------------------------------------------------------------- |
| 0    | [\#ListApplicationRecord](#ListApplicationRecord "wikilink")                                       |
| 1    | GenerateApplicationRecordCount                                                                     |
| 2    | GetApplicationRecordUpdateSystemEvent                                                              |
| 3    | GetApplicationViewDeprecated                                                                       |
| 4    | DeleteApplicationEntity                                                                            |
| 5    | DeleteApplicationCompletely                                                                        |
| 6    | IsAnyApplicationEntityRedundant                                                                    |
| 7    | DeleteRedundantApplicationEntity                                                                   |
| 8    | IsApplicationEntityMovable                                                                         |
| 9    | MoveApplicationEntity                                                                              |
| 11   | CalculateApplicationOccupiedSize                                                                   |
| 16   | PushApplicationRecord                                                                              |
| 17   | ListApplicationRecordContentMeta                                                                   |
| 18   |                                                                                                    |
| 19   | [\#LaunchApplication](#LaunchApplication "wikilink")                                               |
| 21   | [\#GetApplicationContentPath](#GetApplicationContentPath "wikilink")                               |
| 22   | TerminateApplication                                                                               |
| 23   | \[2.0.0+\] ResolveApplicationContentPath                                                           |
| 26   | BeginInstallApplication                                                                            |
| 27   | DeleteApplicationRecord                                                                            |
| 30   | RequestApplicationUpdateInfo                                                                       |
| 31   | RequestUpdateApplication                                                                           |
| 32   | CancelApplicationDownload                                                                          |
| 33   | ResumeApplicationDownload                                                                          |
| 34   |                                                                                                    |
| 35   | UpdateVersionList                                                                                  |
| 36   | PushLaunchVersion                                                                                  |
| 37   | ListRequiredVersion                                                                                |
| 38   | CheckApplicationLaunchVersion                                                                      |
| 39   | CheckApplicationLaunchRights                                                                       |
| 40   | GetApplicationLogoData                                                                             |
| 41   | CalculateApplicationDownloadRequiredSize                                                           |
| 42   | CleanupSdCard                                                                                      |
| 43   | CheckSdCardMountStatus                                                                             |
| 44   | GetSdCardMountStatusChangedEvent                                                                   |
| 45   | GetGameCardAttachmentEvent                                                                         |
| 46   | GetGameCardAttachmentInfo                                                                          |
| 47   | [\#GetTotalSpaceSize](#GetTotalSpaceSize "wikilink")                                               |
| 48   | [\#GetFreeSpaceSize](#GetFreeSpaceSize "wikilink")                                                 |
| 49   | GetSdCardRemovedEvent                                                                              |
| 52   | GetGameCardUpdateDetectionEvent                                                                    |
| 53   | DisableApplicationAutoDelete                                                                       |
| 54   | EnableApplicationAutoDelete                                                                        |
| 55   | [\#GetApplicationDesiredLanguage](#GetApplicationDesiredLanguage "wikilink")                       |
| 56   | SetApplicationTerminateResult                                                                      |
| 57   | ClearApplicationTerminateResult                                                                    |
| 58   | GetLastSdCardMountUnexpectedResult                                                                 |
| 59   | ConvertApplicationLanguageToLanguageCode                                                           |
| 60   | [\#ConvertLanguageCodeToApplicationLanguage](#ConvertLanguageCodeToApplicationLanguage "wikilink") |
| 61   | GetBackgroundDownloadStressTaskInfo                                                                |
| 62   | GetGameCardStopper                                                                                 |
| 63   | IsSystemProgramInstalled                                                                           |
| 64   | \[2.0.0+\] StartApplyDeltaTask                                                                     |
| 65   | \[2.0.0+\] GetRequestServerStopper                                                                 |
| 100  | ResetToFactorySettings                                                                             |
| 101  | ResetToFactorySettingsWithoutUserSaveData                                                          |
| 102  | \[2.0.0+\] ResetToFactorySettingsForRefurbishment                                                  |
| 200  | CalculateUserSaveDataStatistics                                                                    |
| 201  | DeleteUserSaveDataAll                                                                              |
| 210  | DeleteUserSystemSaveData                                                                           |
| 220  | UnregisterNetworkServiceAccount                                                                    |
| 300  | GetApplicationShellEvent                                                                           |
| 301  | PopApplicationShellEventInfo                                                                       |
| 302  | LaunchLibraryApplet                                                                                |
| 303  | TerminateLibraryApplet                                                                             |
| 304  | LaunchSystemApplet                                                                                 |
| 305  | TerminateSystemApplet                                                                              |
| 306  | LaunchOverlayApplet                                                                                |
| 307  | TerminateOverlayApplet                                                                             |
| 400  | [\#GetApplicationControlData](#GetApplicationControlData "wikilink")                               |
| 401  | InvalidateAllApplicationControlCache                                                               |
| 402  | RequestDownloadApplicationControlData                                                              |
| 403  | GetMaxApplicationControlCacheCount                                                                 |
| 404  | \[2.0.0+\] InvalidateApplicationControlCache                                                       |
| 405  | \[2.0.0+\] ListApplicationControlCacheEntryInfo                                                    |
| 502  | \[2.0.0+\] RequestCheckGameCardRegistration                                                        |
| 503  | \[2.0.0+\] RequestGameCardRegistrationGoldPoint                                                    |
| 504  | \[2.0.0+\] RequestRegisterGameCard                                                                 |
| 600  | \[2.0.0+\] CountApplicationContentMeta                                                             |
| 601  | \[2.0.0+\] [\#ListApplicationContentMetaStatus](#ListApplicationContentMetaStatus "wikilink")      |
| 602  | \[2.0.0+\] ListAvailableAddOnContent                                                               |
| 603  | \[2.0.0+\] GetOwnedApplicationContentMetaStatus                                                    |
| 604  | \[2.0.0+\] RegisterContentsExternalKey                                                             |
| 605  | \[2.0.0+\] ListApplicationContentMetaStatusWithRightsCheck                                         |
| 700  | \[2.0.0+\] PushDownloadTaskList                                                                    |
| 701  | \[2.0.0+\] ClearTaskStatusList                                                                     |
| 702  | \[2.0.0+\] RequestDownloadTaskList                                                                 |
| 703  | \[2.0.0+\] RequestEnsureDownloadTask                                                               |
| 704  | \[2.0.0+\] ListDownloadTaskStatus                                                                  |
| 705  | \[2.0.0+\] RequestDownloadTaskListData                                                             |
| 800  | \[2.0.0+\] RequestVersionList                                                                      |
| 801  | \[2.0.0+\] ListVersionList                                                                         |
| 900  | \[2.0.0+\] GetApplicationRecord                                                                    |
| 901  | \[2.0.0+\] GetApplicationRecordProperty                                                            |
| 902  | \[2.0.0+\] EnableApplicationAutoUpdate                                                             |
| 903  | \[2.0.0+\] DisableApplicationAutoUpdate                                                            |
| 904  | \[2.0.0+\] TouchApplication                                                                        |
| 905  | \[2.0.0+\] RequestApplicationUpdate                                                                |
| 906  | \[2.0.0+\] IsApplicationUpdateRequested                                                            |
| 907  | \[2.0.0+\] WithdrawApplicationUpdateRequest                                                        |
| 908  | \[2.0.0+\] ListApplicationRecordInstalledContentMeta                                               |
| 1000 | \[2.0.0+\] RequestVerifyApplicationDeprecated                                                      |
| 1001 | \[2.0.0+\] CorruptApplicationForDebug                                                              |
| 1200 | \[2.0.0+\] [\#NeedsUpdateVulnerability](#NeedsUpdateVulnerability "wikilink")                      |
| 1300 | \[2.0.0+\] IsAnyApplicationEntityInstalled                                                         |
| 1301 | \[2.0.0+\] DeleteApplicationContentEntities                                                        |
| 1302 | \[2.0.0+\] CleanupUnrecordedApplicationEntity                                                      |
| 1400 | \[2.0.0+\] PrepareShutdown                                                                         |
| 1500 | \[2.0.0+\] FormatSdCard                                                                            |
| 1501 | \[2.0.0+\] NeedsSystemUpdateToFormatSdCard                                                         |
| 1502 | \[2.0.0+\] GetLastSdCardFormatUnexpectedResult                                                     |
| 1503 | \[2.0.0+\]                                                                                         |
| 1600 | \[2.0.0+\] GetSystemSeedForPseudoDeviceId                                                          |
| 1700 | \[2.0.0+\] ListApplicationDownloadingContentMeta                                                   |
| 1800 | \[2.0.0+\] IsNotificationSetupCompleted                                                            |
| 1801 | \[2.0.0+\] GetLastNotificationInfoCount                                                            |
| 1802 | \[2.0.0+\] ListLastNotificationInfo                                                                |

## ListApplicationRecord

Takes a type-6 output buffer and an u32 entry\_offset.

Returns an array of title-info entries using the specified offset and
size. No input titleID is passed to this.

### Application Record Format

| Offset | Size | Description                                                                 |
| ------ | ---- | --------------------------------------------------------------------------- |
| 0x0    | 0x8  | Title ID                                                                    |
| 0x8    | 0x1  | Type? (Known values: 2=Installing?, 3=Gamecard?, 4=Installed?)              |
| 0x9    | 0x1  | Unknown, usually 0x02                                                       |
| 0xA    | 0x6  | Unknown, usually zeros?                                                     |
| 0x10   | 0x1  | Unknown, seems to change between reboots and removing/reinserting gamecards |
| 0x11   | 0x7  | Unknown, usually zeros?                                                     |

## LaunchApplication

Takes an input u64 titleID, returns an output u64 PID.

Launches an application title which is registered with NS.

## GetApplicationContentPath

Takes a 0x16-type output buffer, an u8 [title
type](NCM%20services#Title%20Types.md##Title_Types "wikilink"), and an
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

## GetTotalSpaceSize

Takes an input media-id that must be 5.

Returns the u64 from
[Content\_Manager\_services\#IContentStorage](Content%20Manager%20services#IContentStorage.md##IContentStorage "wikilink")
cmd22.

## GetFreeSpaceSize

Takes an input media-id that must be 5.

Returns the u64 from
[Content\_Manager\_services\#IContentStorage](Content%20Manager%20services#IContentStorage.md##IContentStorage "wikilink")
cmd23.

## GetApplicationDesiredLanguage

Takes an input u8 language-bitmask, returns an output u8
[control.nacp](Control.nacp.md "wikilink") langentry index.

User-processes generate the language-bitmask with the following for all
16 lang-entries: `if(<either string in langentry[i] is
non-empty>)bitmask |= 1<<i`

## ConvertLanguageCodeToApplicationLanguage

Takes an input u8 pointer for the resulting Id to be written to and a
string represented as a u64 (i.e 0x53552D6E65 for 'en-US').

Returns 0 if an ID was successfully found, otherwise returns 0x25810.

## GetApplicationControlData

Takes an input u8 flag, an u64 titleID, and a type-0x6 output buffer.
Returns an output u32 for actual\_size. Official user-processes use
buffer size 0x24000. [qlaunch](Qlaunch.md "wikilink") only uses flag
value 0x1.

Loads cached [control.nacp](Control.nacp.md "wikilink") to buf+0 and the
cached icon to buf+0x4000. Returns an error if the buffer is too small.

## ListApplicationContentMetaStatus

Returns 0x10-byte entries using the specified titleID starting at the
specified u32 entryindex. Can only return game titles. The second entry
if any is the update-title usually. When the input entryindex is \>=
totalentries, this will return 0 with out\_entrycount=0.

Entry structure:

| Offset | Size | Description                                                                                          |
| ------ | ---- | ---------------------------------------------------------------------------------------------------- |
| 0x0    | 0x1  | u8 "type". [Title type](Content%20Manager%20services.md "wikilink") (String is from web-applet)      |
| 0x1    | 0x1  | u8 "installedStorage" / [StorageId](Filesystem%20services.md "wikilink") (String is from web-applet) |
| 0x2    | 0x1  | Unknown. Non-zero with output from cmd 605, differs for app/update titles.                           |
| 0x3    | 0x1  | Padding                                                                                              |
| 0x4    | 0x4  | u32 Title-version                                                                                    |
| 0x8    | 0x8  | u64 titleID                                                                                          |

# ns:am2, ns:ec, ns:rid, ns:rt, ns:web

These services are all, at the top level,
"nn::ns::detail::IServiceGetterInterface". These commands check a state
field for a command-specific bit and returns an error if not set, this
is likely a permissions check for service+command.

| Cmd  | Name                                                                                                                             |
| ---- | -------------------------------------------------------------------------------------------------------------------------------- |
| 7988 | \[6.0.0+\] Returns an output [\#IDynamicRightsInterface](#IDynamicRightsInterface "wikilink").                                   |
| 7989 | \[5.1.0+\] Returns an output [\#IReadOnlyApplicationControlDataInterface](#IReadOnlyApplicationControlDataInterface "wikilink"). |
| 7991 | \[5.0.0+\] Returns an output [\#IReadOnlyApplicationRecordInterface](#IReadOnlyApplicationRecordInterface "wikilink").           |
| 7992 | \[4.0.0+\] [GetECommerceInterface](#IECommerceInterface "wikilink")                                                              |
| 7993 | \[4.0.0+\] [GetApplicationVersionInterface](#IApplicationVersionInterface "wikilink")                                            |
| 7994 | [GetFactoryResetInterface](#IFactoryResetInterface "wikilink")                                                                   |
| 7995 | [GetAccountProxyInterface](#IAccountProxyInterface "wikilink")                                                                   |
| 7996 | [GetApplicationManagerInterface](#IApplicationManagerInterface "wikilink")                                                       |
| 7997 | [GetDownloadTaskInterface](#IDownloadTaskInterface "wikilink")                                                                   |
| 7998 | [GetContentManagementInterface](#IContentManagementInterface "wikilink")                                                         |
| 7999 | [GetDocumentInterface](#IDocumentInterface "wikilink")                                                                           |
|      |                                                                                                                                  |

### IAccountProxyInterface

This is "nn::ns::detail::IAccountProxyInterface".

| Cmd | Name              |
| --- | ----------------- |
| 0   | CreateUserAccount |
|     |                   |

### IApplicationManagerInterface

This is "nn::ns::detail::IApplicationManagerInterface".

| Cmd                  | Name                                                                                               |
| -------------------- | -------------------------------------------------------------------------------------------------- |
| 0                    | [\#ListApplicationRecord](#ListApplicationRecord "wikilink")                                       |
| 1                    | GenerateApplicationRecordCount                                                                     |
| 2                    | GetApplicationRecordUpdateSystemEvent                                                              |
| 3                    | GetApplicationViewDeprecated                                                                       |
| 4                    | DeleteApplicationEntity                                                                            |
| 5                    | DeleteApplicationCompletely                                                                        |
| 6                    | IsAnyApplicationEntityRedundant                                                                    |
| 7                    | DeleteRedundantApplicationEntity                                                                   |
| 8                    | IsApplicationEntityMovable                                                                         |
| 9                    | MoveApplicationEntity                                                                              |
| 11                   | CalculateApplicationOccupiedSize                                                                   |
| 16                   | PushApplicationRecord                                                                              |
| 17                   | ListApplicationRecordContentMeta                                                                   |
| 19                   | \[1.0.0-5.1.0\] LaunchApplicationOld                                                               |
| 21                   | [\#GetApplicationContentPath](#GetApplicationContentPath "wikilink")                               |
| 22                   | TerminateApplication                                                                               |
| 23                   | ResolveApplicationContentPath                                                                      |
| 26                   | BeginInstallApplication                                                                            |
| 27                   | DeleteApplicationRecord                                                                            |
| 30                   | RequestApplicationUpdateInfo                                                                       |
| \[1.0.0-3.0.2\] 31   |                                                                                                    |
| 32                   | CancelApplicationDownload                                                                          |
| 33                   | ResumeApplicationDownload                                                                          |
| 35                   | UpdateVersionList                                                                                  |
| 36                   | PushLaunchVersion                                                                                  |
| 37                   | ListRequiredVersion                                                                                |
| 38                   | CheckApplicationLaunchVersion                                                                      |
| \[1.0.0-6.2.0\] 39   | CheckApplicationLaunchRights                                                                       |
| 40                   | GetApplicationLogoData                                                                             |
| 41                   | CalculateApplicationDownloadRequiredSize                                                           |
| 42                   | CleanupSdCard                                                                                      |
| 43                   | CheckSdCardMountStatus                                                                             |
| 44                   | GetSdCardMountStatusChangedEvent                                                                   |
| 45                   | GetGameCardAttachmentEvent                                                                         |
| 46                   | GetGameCardAttachmentInfo                                                                          |
| 47                   | [\#GetTotalSpaceSize](#GetTotalSpaceSize "wikilink")                                               |
| 48                   | [\#GetFreeSpaceSize](#GetFreeSpaceSize "wikilink")                                                 |
| 49                   | GetSdCardRemovedEvent                                                                              |
| 52                   | GetGameCardUpdateDetectionEvent                                                                    |
| 53                   | DisableApplicationAutoDelete                                                                       |
| 54                   | EnableApplicationAutoDelete                                                                        |
| 55                   | GetApplicationDesiredLanguage                                                                      |
| 56                   | SetApplicationTerminateResult                                                                      |
| 57                   | ClearApplicationTerminateResult                                                                    |
| 58                   | GetLastSdCardMountUnexpectedResult                                                                 |
| 59                   | ConvertApplicationLanguageToLanguageCode                                                           |
| 60                   | [\#ConvertLanguageCodeToApplicationLanguage](#ConvertLanguageCodeToApplicationLanguage "wikilink") |
| 61                   | GetBackgroundDownloadStressTaskInfo                                                                |
| 62                   | GetGameCardStopper                                                                                 |
| 63                   | IsSystemProgramInstalled                                                                           |
| 64                   | StartApplyDeltaTask                                                                                |
| 65                   | GetRequestServerStopper                                                                            |
| 66                   | \[3.0.0+\] GetBackgroundApplyDeltaStressTaskInfo                                                   |
| 67                   | \[3.0.0+\] CancelApplicationApplyDelta                                                             |
| 68                   | \[3.0.0+\] ResumeApplicationApplyDelta                                                             |
| 69                   | \[3.0.0+\] CalculateApplicationApplyDeltaRequiredSize                                              |
| 70                   | \[3.0.0+\] ResumeAll                                                                               |
| 71                   | \[3.0.0+\] GetStorageSize                                                                          |
| 80                   | \[3.0.0+\] RequestDownloadApplication                                                              |
| 81                   | \[3.0.0+\] RequestDownloadAddOnContent                                                             |
| 82                   | \[3.0.0+\] DownloadApplication                                                                     |
| \[4.0.0-6.2.0\] 83   | CheckApplicationResumeRights                                                                       |
| 84                   | \[4.0.0+\] GetDynamicCommitEvent                                                                   |
| 85                   | \[4.0.0+\] RequestUpdateApplication2                                                               |
| 86                   | \[4.0.0+\] EnableApplicationCrashReport                                                            |
| 87                   | \[4.0.0+\] IsApplicationCrashReportEnabled                                                         |
| 90                   | \[4.0.0+\] BoostSystemMemoryResourceLimit                                                          |
| 91                   | \[5.0.0+\] DeprecatedLaunchApplication                                                             |
| 92                   | \[5.0.0+\] GetRunningApplicationProgramId                                                          |
| 93                   | \[5.0.0+\] GetMainApplicationProgramIndex                                                          |
| 94                   | \[6.0.0+\] LaunchApplication                                                                       |
| 95                   | \[6.0.0+\] GetApplicationLaunchInfo                                                                |
| 96                   | \[6.0.0+\] AcquireApplicationLaunchInfo                                                            |
| 97                   | \[6.0.0+\] GetMainApplicationProgramIndexByApplicationLaunchInfo                                   |
| 98                   | \[6.0.0+\] EnableApplicationAllThreadDumpOnCrash                                                   |
| 99                   | \[8.0.0+\]                                                                                         |
| 100                  | ResetToFactorySettings                                                                             |
| 101                  | ResetToFactorySettingsWithoutUserSaveData                                                          |
| 102                  | ResetToFactorySettingsForRefurbishment                                                             |
| 200                  | CalculateUserSaveDataStatistics                                                                    |
| 201                  | DeleteUserSaveDataAll                                                                              |
| 210                  | DeleteUserSystemSaveData                                                                           |
| 211                  | \[6.0.0+\] DeleteSaveData                                                                          |
| 220                  | UnregisterNetworkServiceAccount                                                                    |
| 221                  | \[6.0.0+\] UnregisterNetworkServiceAccountWithUserSaveDataDeletion                                 |
| 300                  | GetApplicationShellEvent                                                                           |
| 301                  | PopApplicationShellEventInfo                                                                       |
| 302                  | LaunchLibraryApplet                                                                                |
| 303                  | TerminateLibraryApplet                                                                             |
| 304                  | LaunchSystemApplet                                                                                 |
| 305                  | TerminateSystemApplet                                                                              |
| 306                  | LaunchOverlayApplet                                                                                |
| 307                  | TerminateOverlayApplet                                                                             |
| 400                  | GetApplicationControlData                                                                          |
| 401                  | InvalidateAllApplicationControlCache                                                               |
| 402                  | RequestDownloadApplicationControlData                                                              |
| 403                  | GetMaxApplicationControlCacheCount                                                                 |
| 404                  | InvalidateApplicationControlCache                                                                  |
| 405                  | ListApplicationControlCacheEntryInfo                                                               |
| 406                  | \[6.0.0+\] GetApplicationControlProperty                                                           |
| 407                  | \[8.0.0+\]                                                                                         |
| 408                  | \[8.0.0+\]                                                                                         |
| 502                  | RequestCheckGameCardRegistration                                                                   |
| 503                  | RequestGameCardRegistrationGoldPoint                                                               |
| 504                  | RequestRegisterGameCard                                                                            |
| 505                  | \[3.0.0+\] GetGameCardMountFailureEvent                                                            |
| 506                  | \[3.0.0+\] IsGameCardInserted                                                                      |
| 507                  | \[3.0.0+\] EnsureGameCardAccess                                                                    |
| 508                  | \[3.0.0+\] GetLastGameCardMountFailureResult                                                       |
| 509                  | \[5.0.0+\] ListApplicationIdOnGameCard                                                             |
| 600                  | CountApplicationContentMeta                                                                        |
| 601                  | [\#ListApplicationContentMetaStatus](#ListApplicationContentMetaStatus "wikilink")                 |
| 602                  | \[2.0.0-5.1.0\] ListAvailableAddOnContent                                                          |
| 603                  | GetOwnedApplicationContentMetaStatus                                                               |
| 604                  | RegisterContentsExternalKey                                                                        |
| 605                  | ListApplicationContentMetaStatusWithRightsCheck                                                    |
| 606                  | \[3.0.0+\] GetContentMetaStorage                                                                   |
| 607                  | \[6.0.0+\] ListAvailableAddOnContent                                                               |
| 700                  | PushDownloadTaskList                                                                               |
| 701                  | ClearTaskStatusList                                                                                |
| 702                  | RequestDownloadTaskList                                                                            |
| 703                  | RequestEnsureDownloadTask                                                                          |
| 704                  | ListDownloadTaskStatus                                                                             |
| 705                  | RequestDownloadTaskListData                                                                        |
| 800                  | RequestVersionList                                                                                 |
| 801                  | ListVersionList                                                                                    |
| 802                  | \[3.0.0+\] RequestVersionListData                                                                  |
| 900                  | GetApplicationRecord                                                                               |
| 901                  | GetApplicationRecordProperty                                                                       |
| 902                  | EnableApplicationAutoUpdate                                                                        |
| 903                  | DisableApplicationAutoUpdate                                                                       |
| 904                  | TouchApplication                                                                                   |
| 905                  | RequestApplicationUpdate                                                                           |
| 906                  | IsApplicationUpdateRequested                                                                       |
| 907                  | WithdrawApplicationUpdateRequest                                                                   |
| 908                  | ListApplicationRecordInstalledContentMeta                                                          |
| 909                  | \[3.0.0+\] WithdrawCleanupAddOnContentsWithNoRightsRecommendation                                  |
| 910                  | \[5.0.0+\] HasApplicationRecord                                                                    |
| 911                  | \[5.1.0+\] SetPreInstalledApplication                                                              |
| 912                  | \[5.1.0+\] ClearPreInstalledApplicationFlag                                                        |
| 1000                 | RequestVerifyApplicationDeprecated                                                                 |
| 1001                 | CorruptApplicationForDebug                                                                         |
| 1002                 | \[3.0.0+\] RequestVerifyAddOnContentsRights                                                        |
| 1003                 | \[5.0.0+\] RequestVerifyApplication                                                                |
| 1004                 | \[5.0.0+\] CorruptContentForDebug                                                                  |
| 1200                 | [\#NeedsUpdateVulnerability](#NeedsUpdateVulnerability "wikilink")                                 |
| 1300                 | IsAnyApplicationEntityInstalled                                                                    |
| 1301                 | DeleteApplicationContentEntities                                                                   |
| 1302                 | CleanupUnrecordedApplicationEntity                                                                 |
| 1303                 | \[3.0.0+\] CleanupAddOnContentsWithNoRights                                                        |
| 1304                 | \[3.0.0+\] DeleteApplicationContentEntity                                                          |
| 1308                 | \[5.0.0+\] DeleteApplicationCompletelyForDebug                                                     |
| 1309                 | \[6.0.0+\] CleanupUnavailableAddOnContents                                                         |
| 1400                 | PrepareShutdown                                                                                    |
| 1500                 | FormatSdCard                                                                                       |
| 1501                 | NeedsSystemUpdateToFormatSdCard                                                                    |
| 1502                 | GetLastSdCardFormatUnexpectedResult                                                                |
| 1504                 | \[3.0.0+\] InsertSdCard                                                                            |
| 1505                 | \[3.0.0+\] RemoveSdCard                                                                            |
| 1600                 | GetSystemSeedForPseudoDeviceId                                                                     |
| 1601                 | \[3.0.0+\] ResetSystemSeedForPseudoDeviceId                                                        |
| 1700                 | ListApplicationDownloadingContentMeta                                                              |
| 1701                 | \[3.0.0+\] GetApplicationView                                                                      |
| 1702                 | \[3.0.0+\] GetApplicationDownloadTaskStatus                                                        |
| 1703                 | \[4.0.0+\] GetApplicationViewDownloadErrorContext                                                  |
| 1704                 | \[8.0.0+\]                                                                                         |
| 1800                 | IsNotificationSetupCompleted                                                                       |
| 1801                 | GetLastNotificationInfoCount                                                                       |
| 1802                 | ListLastNotificationInfo                                                                           |
| 1803                 | \[3.0.0+\] ListNotificationTask                                                                    |
| 1900                 | \[3.0.0+\] IsActiveAccount                                                                         |
| 1901                 | \[4.0.0+\] RequestDownloadApplicationPrepurchasedRights                                            |
| 1902                 | \[5.0.0+\] GetApplicationTicketInfo                                                                |
| 2000                 | \[4.0.0+\] GetSystemDeliveryInfo                                                                   |
| 2001                 | \[4.0.0+\] SelectLatestSystemDeliveryInfo                                                          |
| 2002                 | \[4.0.0+\] VerifyDeliveryProtocolVersion                                                           |
| 2003                 | \[4.0.0+\] GetApplicationDeliveryInfo                                                              |
| 2004                 | \[4.0.0+\] HasAllContentsToDeliver                                                                 |
| 2005                 | \[4.0.0+\] CompareApplicationDeliveryInfo                                                          |
| 2006                 | \[4.0.0+\] CanDeliverApplication                                                                   |
| 2007                 | \[4.0.0+\] ListContentMetaKeyToDeliverApplication                                                  |
| 2008                 | \[4.0.0+\] NeedsSystemUpdateToDeliverApplication                                                   |
| 2009                 | \[4.0.0+\] EstimateRequiredSize                                                                    |
| 2010                 | \[4.0.0+\] RequestReceiveApplication                                                               |
| 2011                 | \[4.0.0+\] CommitReceiveApplication                                                                |
| 2012                 | \[4.0.0+\] GetReceiveApplicationProgress                                                           |
| 2013                 | \[4.0.0+\] RequestSendApplication                                                                  |
| 2014                 | \[4.0.0+\] GetSendApplicationProgress                                                              |
| 2015                 | \[4.0.0+\] CompareSystemDeliveryInfo                                                               |
| 2016                 | \[4.0.0+\] ListNotCommittedContentMeta                                                             |
| 2017                 | \[4.0.0+\] RecoverDownloadTask                                                                     |
| 2018                 | \[5.0.0+\] GetApplicationDeliveryInfoHash                                                          |
| 2050                 | \[6.0.0+\] GetApplicationRightsOnClient                                                            |
| 2100                 | \[6.0.0+\] GetApplicationTerminateResult                                                           |
| 2101                 | \[6.0.0+\] GetRawApplicationTerminateResult                                                        |
| 2150                 | \[6.0.0+\] CreateRightsEnvironment                                                                 |
| 2151                 | \[6.0.0+\] DestroyRightsEnvironment                                                                |
| 2152                 | \[6.0.0+\] ActivateRightsEnvironment                                                               |
| 2153                 | \[6.0.0+\] DeactivateRightsEnvironment                                                             |
| 2154                 | \[6.0.0+\] ForceActivateRightsContextForExit                                                       |
| 2155                 | \[7.0.0+\] UpdateRightsEnvironmentStatus                                                           |
| 2160                 | \[6.0.0+\] AddTargetApplicationToRightsEnvironment                                                 |
| 2161                 | \[6.0.0+\] SetUsersToRightsEnvironment                                                             |
| 2170                 | \[6.0.0+\] GetRightsEnvironmentStatus                                                              |
| 2171                 | \[6.0.0+\] GetRightsEnvironmentStatusChangedEvent                                                  |
| 2180                 | \[6.0.0+\] RequestExtendExpirationInRightsEnvironment                                              |
| 2181                 | \[6.0.0+\] GetResultOfExtendExpirationInRightsEnvironment                                          |
| 2182                 | \[6.0.0+\] SetActiveRightsContextUsingStateToRightsEnvironment                                     |
| 2190                 | \[6.0.0+\] GetRightsEnvironmentHandleForApplication                                                |
| 2199                 | \[6.0.0+\] GetRightsEnvironmentCountForDebug                                                       |
| 2200                 | \[6.0.0+\] GetGameCardApplicationCopyIdentifier                                                    |
| 2201                 | \[6.0.0+\] GetInstalledApplicationCopyIdentifier                                                   |
| \[6.0.0-6.2.0\] 2250 | RequestReportActiveELicence                                                                        |
| 2300                 | \[6.0.0+\] ListEventLog                                                                            |
| 2350                 | \[7.0.0+\]                                                                                         |
| 2400                 | \[8.0.0+\]                                                                                         |
| 2401                 | \[8.0.0+\]                                                                                         |
| 2402                 | \[8.0.0+\]                                                                                         |
| 2403                 | \[8.0.0+\]                                                                                         |
| 2404                 | \[8.0.0+\]                                                                                         |
| 2500                 | \[8.0.0+\]                                                                                         |
|                      |                                                                                                    |

\[4.0.0+\] RequestDownloadAddOnContent now takes an additional 8-bytes
of input.

#### Cmd99

No input/output.

This is used by AM cmd
[LaunchDevMenu](Applet%20Manager%20services#LaunchDevMenu.md##LaunchDevMenu "wikilink").

This uses [system-settings](System%20Settings.md "wikilink")
`ns.applet!devmenu_id` and `ns.applet!devoverlaydisp_id`, which only
exists on devunits.

### IApplicationVersionInterface

This is "nn::ns::detail::IApplicationVersionInterface".

This was added with \[4.0.0+\].

| Cmd  | Name                         |
| ---- | ---------------------------- |
| 0    | GetLaunchRequiredVersion     |
| 1    | UpgradeLaunchRequiredVersion |
| 35   | UpdateVersionList            |
| 36   | PushLaunchVersion            |
| 37   | ListRequiredVersion          |
| 800  | RequestVersionList           |
| 801  | ListVersionList              |
| 802  | RequestVersionListData       |
| 1000 | PerformAutoUpdate            |
|      |                              |

### IContentManagerInterface

This is "nn::ns::detail::IContentManagementInterface".

| Cmd | Name                                            |
| --- | ----------------------------------------------- |
| 11  | CalculateApplicationOccupiedSize                |
| 43  | CheckSdCardMountStatus                          |
| 47  | GetTotalSpaceSize                               |
| 48  | GetFreeSpaceSize                                |
| 600 | CountApplicationContentMeta                     |
| 601 | ListApplicationContentMetaStatus                |
| 605 | ListApplicationContentMetaStatusWithRightsCheck |
| 607 | IsAnyApplicationRunning                         |
|     |                                                 |

### IDocumentInterface

This is "nn::ns::detail::IDocumentInterface".

| Cmd | Name                                      |
| --- | ----------------------------------------- |
| 21  | GetApplicationContentPath                 |
| 23  | ResolveApplicationContentPath             |
| 92  | \[5.0.0+\] GetRunningApplicationProgramId |
|     |                                           |

### IDownloadTaskInterface

This is "nn::ns::detail::IDownloadTaskInterface".

| Cmd | Name                                               |
| --- | -------------------------------------------------- |
| 701 | ClearTaskStatusList                                |
| 702 | RequestDownloadTaskList                            |
| 703 | RequestEnsureDownloadTask                          |
| 704 | ListDownloadTaskStatus                             |
| 705 | RequestDownloadTaskListData                        |
| 706 | \[4.0.0+\] TryCommitCurrentApplicationDownloadTask |
| 707 | \[4.0.0+\] EnableAutoCommit                        |
| 708 | \[4.0.0+\] DisableAutoCommit                       |
| 709 | \[4.0.0+\] TriggerDynamicCommitEvent               |
|     |                                                    |

### IReadOnlyApplicationRecordInterface

This is "nn::ns::detail::IReadOnlyApplicationRecordInterface".

This was added with \[5.0.0+\].

| Cmd | Name                 | Notes                                                                                      |
| --- | -------------------- | ------------------------------------------------------------------------------------------ |
| 0   | HasApplicationRecord | Same as [\#IApplicationManagerInterface](#IApplicationManagerInterface "wikilink") cmd 910 |

### IReadOnlyApplicationControlDataInterface

This is "nn::ns::detail::IReadOnlyApplicationControlDataInterface".

This was added with \[5.1.0+\].

| Cmd | Name                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| 0   | [\#GetApplicationControlData](#GetApplicationControlData "wikilink")                               | Same as [\#IApplicationManagerInterface](#IApplicationManagerInterface "wikilink") cmd 400 |
| 1   | [\#GetApplicationDesiredLanguage](#GetApplicationDesiredLanguage "wikilink")                       | Same as [\#IApplicationManagerInterface](#IApplicationManagerInterface "wikilink") cmd 55  |
| 2   | ConvertApplicationLanguageToLanguageCode                                                           | Same as [\#IApplicationManagerInterface](#IApplicationManagerInterface "wikilink") cmd 59  |
| 3   | [\#ConvertLanguageCodeToApplicationLanguage](#ConvertLanguageCodeToApplicationLanguage "wikilink") | Same as [\#IApplicationManagerInterface](#IApplicationManagerInterface "wikilink") cmd 60  |

### IDynamicRightsInterface

This is "nn::ns::detail::IDynamicRightsInterface".

This was added with \[6.0.0+\].

| Cmd | Name       | Notes |
| --- | ---------- | ----- |
| 0   |            |       |
| 1   |            |       |
| 4   |            |       |
| 5   |            |       |
| 6   |            |       |
| 7   |            |       |
| 8   |            |       |
| 9   | \[7.0.0+\] |       |
| 10  | \[7.0.0+\] |       |
| 11  | \[7.0.0+\] |       |
| 12  | \[8.0.0+\] |       |
| 13  | \[8.0.0+\] |       |
|     |            |       |

### IECommerceInterface

This is "nn::ns::detail::IECommerceInterface".

This was added with \[4.0.0+\].

| Cmd | Name                                                 | Notes                                                                                        |
| --- | ---------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| 0   | RequestLinkDevice                                    | Takes a total of 0x10-bytes of input, returns an [\#IAsyncResult](#IAsyncResult "wikilink"). |
| 1   | \[6.0.0+\] RequestCleanupAllPreInstalledApplications | No input, returns an [\#IAsyncResult](#IAsyncResult "wikilink").                             |
| 2   | \[6.0.0+\] RequestCleanupPreInstalledApplication     | Takes a total of 0x8-bytes of input, returns an [\#IAsyncResult](#IAsyncResult "wikilink").  |
| 3   | \[6.0.0+\] RequestSyncRights                         | No input, returns an [\#IAsyncResult](#IAsyncResult "wikilink").                             |
| 4   | \[6.0.0+\] RequestUnlinkDevice                       | Takes a total of 0x10-bytes of input, returns an [\#IAsyncResult](#IAsyncResult "wikilink"). |
| 5   | \[6.1.0+\] RequestRevokeAllELicense                  | Takes a total of 0x10-bytes of input, returns an [\#IAsyncResult](#IAsyncResult "wikilink"). |

### IFactoryResetInterface

This is "nn::ns::detail::IFactoryResetInterface".

| Cmd | Name                                      |
| --- | ----------------------------------------- |
| 100 | ResetToFactorySettings                    |
| 101 | ResetToFactorySettingsWithoutUserSaveData |
| 102 | ResetToFactorySettingsForRefurbishment    |
|     |                                           |

# ns:vm

This is "nn::ns::detail::IVulnerabilityManagerInterface".

| Cmd  | Name                                                                                        |
| ---- | ------------------------------------------------------------------------------------------- |
| 1200 | \[3.0.0+\] [\#NeedsUpdateVulnerability](#NeedsUpdateVulnerability "wikilink")               |
| 1201 | \[4.0.0+\] [\#UpdateSafeSystemVersionForDebug](#UpdateSafeSystemVersionForDebug "wikilink") |
| 1202 | \[4.0.0+\] [\#GetSafeSystemVersion](#GetSafeSystemVersion "wikilink")                       |
|      |                                                                                             |

## NeedsUpdateVulnerability

No input, returns an output u8 bool flag.

Web-applets use this command to check if the system needs an update.

## UpdateSafeSystemVersionForDebug

Takes an input u64 **titleID** and an u32 **version**.

This command is not available for retail units. On a debug unit, if the
[system setting](System%20Settings.md "wikilink")
`vulnerability!enable_debug` is set, this mounts the system savegame
[0x8000000000000049](Flash%20Filesystem#System%20Savegames.md##System_Savegames "wikilink")
as "ns\_ssversion:/", opens the file "ns\_ssversion:/entry" and writes
the supplied **titleID** and **version** in it.

Finally, it calls
[OpenContentMetaDatabase](NCM%20services#ncm.md##ncm "wikilink") with
[StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink") 3,
then calls
[GetLatestContentMetaKey](NCM%20services#IContentMetaDatabase.md##IContentMetaDatabase "wikilink")
with the supplied **titleID** and compares the version field from the
returned [Content Meta
Record](CNMT#Content%20Meta%20Records.md##Content_Meta_Records "wikilink")
with the supplied **version**.

If the supplied **version** is higher than the one in NCM's database,
the value returned by
[NeedsUpdateVulnerability](NS%20Services#NeedsUpdateVulnerability.md##NeedsUpdateVulnerability "wikilink")
is set to "true".

## GetSafeSystemVersion

No input, returns a 0x10 byte array with the cached contents of
"ns\_ssversion:/entry" (u64 **titleID**, u32 **version** and u32
**policy** from `vulnerability!needs_update_vulnerability_policy`).

# ns:su

This is "nn::ns::detail::ISystemUpdateInterface".

| Cmd                | Name                                                        |
| ------------------ | ----------------------------------------------------------- |
| 0                  | GetBackgroundNetworkUpdateState                             |
| 1                  | [OpenSystemUpdateControl](#ISystemUpdateControl "wikilink") |
| 2                  | NotifyExFatDriverRequired                                   |
| 3                  | ClearExFatDriverStatusForDebug                              |
| 4                  | RequestBackgroundNetworkUpdate                              |
| 5                  | NotifyBackgroundNetworkUpdate                               |
| 6                  | NotifyExFatDriverDownloadedForDebug                         |
| 9                  | GetSystemUpdateNotificationEventForContentDelivery          |
| 10                 | NotifySystemUpdateForContentDelivery                        |
| 11                 | \[3.0.0+\] PrepareShutdown                                  |
| \[3.0.0-3.0.2\] 12 |                                                             |
| \[3.0.0-3.0.2\] 13 |                                                             |
| \[3.0.0-3.0.2\] 14 |                                                             |
| \[3.0.0-3.0.2\] 15 |                                                             |
| 16                 | \[4.0.0+\] DestroySystemUpdateTask                          |
| 17                 | \[4.0.0+\] RequestSendSystemUpdate                          |
| 18                 | \[4.0.0+\] GetSendSystemUpdateProgress                      |
|                    |                                                             |

## ISystemUpdateControl

| Cmd | Name                                                                 |
| --- | -------------------------------------------------------------------- |
| 0   | [\#HasDownloaded](#HasDownloaded "wikilink")                         |
| 1   | RequestCheckLatestUpdate                                             |
| 2   | RequestDownloadLatestUpdate                                          |
| 3   | [\#GetDownloadProgress](#GetDownloadProgress "wikilink")             |
| 4   | [\#ApplyDownloadedUpdate](#ApplyDownloadedUpdate "wikilink")         |
| 5   | RequestPrepareCardUpdate                                             |
| 6   | GetPrepareCardUpdateProgress                                         |
| 7   | HasPreparedCardUpdate                                                |
| 8   | ApplyCardUpdate                                                      |
| 9   | [\#GetDownloadedEulaDataSize](#GetDownloadedEulaDataSize "wikilink") |
| 10  | [\#GetDownloadedEulaData](#GetDownloadedEulaData "wikilink")         |
| 11  | SetupCardUpdate                                                      |
| 12  | GetPreparedCardUpdateEulaDataSize                                    |
| 13  | GetPreparedCardUpdateEulaData                                        |
| 14  | \[4.0.0+\] SetupCardUpdateViaSystemUpdater                           |
| 15  | \[4.0.0+\] HasReceived                                               |
| 16  | \[4.0.0+\] RequestReceiveSystemUpdate                                |
| 17  | \[4.0.0+\] GetReceiveProgress                                        |
| 18  | \[4.0.0+\] ApplyReceivedUpdate                                       |
| 19  | \[4.0.0+\] GetReceivedEulaDataSize                                   |
| 20  | \[4.0.0+\] GetReceivedEulaData                                       |
| 21  | \[4.0.0+\] SetupToReceiveSystemUpdate                                |
| 22  | \[6.0.0+\] RequestCheckLatestUpdateIncludesRebootlessUpdate          |

### HasDownloaded

No input, returns an output u8 bool flag.

Gets whether a network sysupdate was downloaded, with install pending.

Uses [nim](NIM%20services.md "wikilink") ListSystemUpdateTask and
[nim](NIM%20services.md "wikilink") GetSystemUpdateTaskInfo. When
ListSystemUpdateTask successfully returns a task and
GetSystemUpdateTaskInfo is successful, the output flag is set to:
`*((u8*)(taskinfo+0) == 0x3`. Otherwise, flag=0.

This always returns 0, however this will assert if
GetSystemUpdateTaskInfo fails with ret\!=0x3C89.

### GetDownloadProgress

No input, returns a 0x10-byte output struct.

Similar to [\#HasDownloaded](#HasDownloaded "wikilink") except instead
of a flag, this returns the 0x10-bytes from taskinfo+8. The output
struct is cleared when the task(info) isn't available.

### ApplyDownloadedUpdate

No input/output.

Runs code similar to [\#HasDownloaded](#HasDownloaded "wikilink"),
throwing an error if a network sysupdate isn't ready for install. Then
the sysupdate is installed:

  - Uses ListSystemUpdateTask again, then
    [nim](NIM%20services.md "wikilink") IsExFatDriverIncluded. Runs
    ExFat handling when the output flag is set.
  - The two flags in
    [Flash\_Filesystem\#System\_Update\_Control](Flash%20Filesystem#System%20Update%20Control.md##System_Update_Control "wikilink")
    are set to 1.
  - Uses [nim](NIM%20services.md "wikilink") CommitSystemUpdateTask and
    [nim](NIM%20services.md "wikilink") DestroySystemUpdateTask.
  - Installs FIRM.

### GetDownloadedEulaDataSize

Takes a type-0x15 input buffer **path**, returns an output u64
**filesize**.

Runs code similar to [\#HasDownloaded](#HasDownloaded "wikilink"),
throwing an error if a network sysupdate isn't ready for install.

Uses ListSystemUpdateTask again. Then
[nim](NIM%20services.md "wikilink") GetDownloadedSystemDataPath, with
the output ContentPath being used to mount the EULA title with FS.

Then "<mountname>:/\<**path**\>" is opened, gets the **filesize**, then
runs cleanup.

### GetDownloadedEulaData

Takes a type-0x15 input buffer **path** and a type-0x6 output buffer,
returns an output u64 **filesize**.

Similar to
[\#GetDownloadedEulaDataSize](#GetDownloadedEulaDataSize "wikilink")
except this reads the file instead, using the specified output buffer
with size=filesize. This will throw an error if the filesize is larger
than the buffer size.

# IAsyncValue

This is "nn::ns::detail::IAsyncValue".

| Cmd | Name       |
| --- | ---------- |
| 0   |            |
| 1   |            |
| 2   |            |
| 3   | \[4.0.0+\] |

Cmd3: No input/output, takes a type-0x16 output buffer.

# IAsyncResult

This is "nn::ns::detail::IAsyncResult".

| Cmd | Name       |
| --- | ---------- |
| 0   |            |
| 1   |            |
| 2   | \[4.0.0+\] |

Cmd2: No input/output, takes a type-0x16 output buffer.

# ns:dev

This is "nn::ns::detail::IDevelopInterface".

| Cmd | Name                                                                                               |
| --- | -------------------------------------------------------------------------------------------------- |
| 0   | [\#LaunchProgram](#LaunchProgram "wikilink")                                                       |
| 1   | [\#TerminateProcess](#TerminateProcess "wikilink")                                                 |
| 2   | [\#TerminateProgram](#TerminateProgram "wikilink")                                                 |
| 4   | [\#GetShellEvent](#GetShellEvent "wikilink")                                                       |
| 5   | [\#GetShellEventInfo](#GetShellEventInfo "wikilink")                                               |
| 6   | [\#TerminateApplication](#TerminateApplication "wikilink")                                         |
| 7   | [\#PrepareLaunchProgramFromHost](#PrepareLaunchProgramFromHost "wikilink")                         |
| 8   | [\#LaunchApplicationForDevelop](#LaunchApplicationForDevelop "wikilink")                           |
| 9   | [\#LaunchApplicationWithStorageIdForDevelop](#LaunchApplicationWithStorageIdForDevelop "wikilink") |
| 10  | \[6.0.0+\] TerminateApplication2                                                                   |
| 11  | \[6.0.0+\] GetRunningApplicationProcessIdForDevelop                                                |
| 12  | \[6.0.0+\] SetCurrentApplicationRightsEnvironmentCanBeActiveForDevelop                             |

## LaunchProgram

Wrapper for "pm:shell"
[LaunchProcess](Process%20Manager%20services#LaunchProcess.md##LaunchProcess "wikilink").

## TerminateProcess

Wrapper for "pm:shell"
[TerminateTitleByPid](Process%20Manager%20services#TerminateTitleByPid.md##TerminateTitleByPid "wikilink").

## TerminateProgram

Wrapper for "pm:shell"
[TerminateTitleByTitleId](Process%20Manager%20services#TerminateTitleByTitleId.md##TerminateTitleByTitleId "wikilink").

## GetShellEvent

Wrapper for "pm:shell"
[GetProcessEventWaiter](Process%20Manager%20services#GetProcessEventWaiter.md##GetProcessEventWaiter "wikilink").

## GetShellEventInfo

Wrapper for "pm:shell"
[GetProcessEventType](Process%20Manager%20services#GetProcessEventType.md##GetProcessEventType "wikilink").

## TerminateApplication

Calls "pm:shell"
[GetCrashingProcessPid](Process%20Manager%20services#GetCrashingProcessPid.md##GetCrashingProcessPid "wikilink")
and sends PID to
[TerminateTitleByPid](Process%20Manager%20services#TerminateTitleByPid.md##TerminateTitleByPid "wikilink").

## PrepareLaunchProgramFromHost

Takes a type-0x5 input buffer containing the
[ContentPath](Filesystem%20services.md "wikilink"), returns an output
0x10-byte struct.

Calls
[IPathResolverForStorage](NCM%20services#IPathResolverForStorage.md##IPathResolverForStorage "wikilink")
Set...NcaPath functions.

## LaunchApplicationForDevelop

Takes an input u32
[LaunchFlags](Process%20Manager%20services#LaunchFlags.md##LaunchFlags "wikilink")
and u64 titleID, returns an output u64 PID.

Same as LaunchApplicationWithStorageId except the last two params passed
to the internal vtable funcptr call are value 0x6, instead of from the
command input.

## LaunchApplicationWithStorageIdForDevelop

Takes 2 input u8s, an u32
[LaunchFlags](Process%20Manager%20services#LaunchFlags.md##LaunchFlags "wikilink"),
and an u64 titleID. Returns an output u64 PID.

Launches an application title which is registered with NS.

[Category:Services](Category:Services "wikilink")

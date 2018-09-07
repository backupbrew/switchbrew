# aoc:u

This is "nn::aocsrv::detail::IAddOnContentManager".

| Cmd | Name                                       |
| --- | ------------------------------------------ |
| 0   | CountAddOnContentByApplicationId           |
| 1   | ListAddOnContentByApplicationId            |
| 2   | CountAddOnContent                          |
| 3   | ListAddOnContent                           |
| 4   | GetAddOnContentBaseIdByApplicationId       |
| 5   | GetAddOnContentBaseId                      |
| 6   | PrepareAddOnContentByApplicationId         |
| 7   | PrepareAddOnContent                        |
| 8   | \[4.0.0+\] GetAddOnContentListChangedEvent |

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
| 1200 | \[2.0.0+\] NeedsUpdateVulnerability                                                                |
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
size. No input titleID is passed to
this.

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

# ns:am2, ns:ec, ns:rid, ns:rt, ns:web

These services are all, at the top level,
"nn::ns::detail::IServiceGetterInterface". These commands check a state
field for a command-specific bit and returns an error if not set, this
is likely a permissions check for
service+command.

| Cmd  | Name                                                                       |
| ---- | -------------------------------------------------------------------------- |
| 7992 | [GetECommerceInterface](#IECommerceInterface "wikilink")                   |
| 7993 | [GetApplicationVersionInterface](#IApplicationVersionInterface "wikilink") |
| 7994 | [GetFactoryResetInterface](#IFactoryResetInterface "wikilink")             |
| 7995 | [GetAccountProxyInterface](#IAccountProxyInterface "wikilink")             |
| 7996 | [GetApplicationManagerInterface](#IApplicationManagerInterface "wikilink") |
| 7997 | [GetDownloadTaskInterface](#IDownloadTaskInterface "wikilink")             |
| 7998 | [GetContentManagementInterface](#IContentManagementInterface "wikilink")   |
| 7999 | [GetDocumentInterface](#IDocumentInterface "wikilink")                     |
|      |                                                                            |

### IAccountProxyInterface

This is "nn::ns::detail::IAccountProxyInterface".

| Cmd | Name              |
| --- | ----------------- |
| 0   | CreateUserAccount |
|     |                   |

### IApplicationManagerInterface

This is
"nn::ns::detail::IApplicationManagerInterface".

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
| 19   | \[1.0.0-5.1.0\] [\#LaunchApplication](#LaunchApplication "wikilink")                               |
| 21   | [\#GetApplicationContentPath](#GetApplicationContentPath "wikilink")                               |
| 22   | TerminateApplication                                                                               |
| 23   | ResolveApplicationContentPath                                                                      |
| 26   | BeginInstallApplication                                                                            |
| 27   | DeleteApplicationRecord                                                                            |
| 30   | RequestApplicationUpdateInfo                                                                       |
| 32   | CancelApplicationDownload                                                                          |
| 33   | ResumeApplicationDownload                                                                          |
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
| 55   | GetApplicationDesiredLanguage                                                                      |
| 56   | SetApplicationTerminateResult                                                                      |
| 57   | ClearApplicationTerminateResult                                                                    |
| 58   | GetLastSdCardMountUnexpectedResult                                                                 |
| 59   | ConvertApplicationLanguageToLanguageCode                                                           |
| 60   | [\#ConvertLanguageCodeToApplicationLanguage](#ConvertLanguageCodeToApplicationLanguage "wikilink") |
| 61   | GetBackgroundDownloadStressTaskInfo                                                                |
| 62   | GetGameCardStopper                                                                                 |
| 63   | IsSystemProgramInstalled                                                                           |
| 64   | StartApplyDeltaTask                                                                                |
| 65   | GetRequestServerStopper                                                                            |
| 66   | GetBackgroundApplyDeltaStressTaskInfo                                                              |
| 67   | CancelApplicationApplyDelta                                                                        |
| 68   | ResumeApplicationApplyDelta                                                                        |
| 69   | CalculateApplicationApplyDeltaRequiredSize                                                         |
| 70   | ResumeAll                                                                                          |
| 71   | GetStorageSize                                                                                     |
| 80   | RequestDownloadApplication                                                                         |
| 81   | RequestDownloadAddOnContent                                                                        |
| 82   | DownloadApplication                                                                                |
| 83   | CheckApplicationResumeRights                                                                       |
| 84   | GetDynamicCommitEvent                                                                              |
| 85   | RequestUpdateApplication2                                                                          |
| 86   | EnableApplicationCrashReport                                                                       |
| 87   | IsApplicationCrashReportEnabled                                                                    |
| 90   | BoostSystemMemoryResourceLimit                                                                     |
| 91   | \[5.0.0+\]                                                                                         |
| 92   | \[5.0.0+\]                                                                                         |
| 93   | \[5.0.0+\]                                                                                         |
| 94   | \[6.0.0+\] LaunchApplication2                                                                      |
| 95   | \[6.0.0+\]                                                                                         |
| 96   | \[6.0.0+\]                                                                                         |
| 97   | \[6.0.0+\]                                                                                         |
| 98   | \[6.0.0+\]                                                                                         |
| 100  | ResetToFactorySettings                                                                             |
| 101  | ResetToFactorySettingsWithoutUserSaveData                                                          |
| 102  | ResetToFactorySettingsForRefurbishment                                                             |
| 200  | CalculateUserSaveDataStatistics                                                                    |
| 201  | DeleteUserSaveDataAll                                                                              |
| 210  | DeleteUserSystemSaveData                                                                           |
| 211  | \[6.0.0+\]                                                                                         |
| 220  | UnregisterNetworkServiceAccount                                                                    |
| 221  | \[6.0.0+\]                                                                                         |
| 300  | GetApplicationShellEvent                                                                           |
| 301  | PopApplicationShellEventInfo                                                                       |
| 302  | LaunchLibraryApplet                                                                                |
| 303  | TerminateLibraryApplet                                                                             |
| 304  | LaunchSystemApplet                                                                                 |
| 305  | TerminateSystemApplet                                                                              |
| 306  | LaunchOverlayApplet                                                                                |
| 307  | TerminateOverlayApplet                                                                             |
| 400  | GetApplicationControlData                                                                          |
| 401  | InvalidateAllApplicationControlCache                                                               |
| 402  | RequestDownloadApplicationControlData                                                              |
| 403  | GetMaxApplicationControlCacheCount                                                                 |
| 404  | InvalidateApplicationControlCache                                                                  |
| 405  | ListApplicationControlCacheEntryInfo                                                               |
| 406  | \[6.0.0+\]                                                                                         |
| 502  | RequestCheckGameCardRegistration                                                                   |
| 503  | RequestGameCardRegistrationGoldPoint                                                               |
| 504  | RequestRegisterGameCard                                                                            |
| 505  | GetGameCardMountFailureEvent                                                                       |
| 506  | IsGameCardInserted                                                                                 |
| 507  | EnsureGameCardAccess                                                                               |
| 508  | GetLastGameCardMountFailureResult                                                                  |
| 509  | ListApplicationIdOnGameCard                                                                        |
| 600  | CountApplicationContentMeta                                                                        |
| 601  | [\#ListApplicationContentMetaStatus](#ListApplicationContentMetaStatus "wikilink")                 |
| 602  | \[2.0.0-5.1.0\] ListAvailableAddOnContent                                                          |
| 603  | GetOwnedApplicationContentMetaStatus                                                               |
| 604  | RegisterContentsExternalKey                                                                        |
| 605  | ListApplicationContentMetaStatusWithRightsCheck                                                    |
| 606  | GetContentMetaStorage                                                                              |
| 607  | \[6.0.0+\]                                                                                         |
| 700  | PushDownloadTaskList                                                                               |
| 701  | ClearTaskStatusList                                                                                |
| 702  | RequestDownloadTaskList                                                                            |
| 703  | RequestEnsureDownloadTask                                                                          |
| 704  | ListDownloadTaskStatus                                                                             |
| 705  | RequestDownloadTaskListData                                                                        |
| 800  | RequestVersionList                                                                                 |
| 801  | ListVersionList                                                                                    |
| 802  | RequestVersionListData                                                                             |
| 900  | GetApplicationRecord                                                                               |
| 901  | GetApplicationRecordProperty                                                                       |
| 902  | EnableApplicationAutoUpdate                                                                        |
| 903  | DisableApplicationAutoUpdate                                                                       |
| 904  | TouchApplication                                                                                   |
| 905  | RequestApplicationUpdate                                                                           |
| 906  | IsApplicationUpdateRequested                                                                       |
| 907  | WithdrawApplicationUpdateRequest                                                                   |
| 908  | ListApplicationRecordInstalledContentMeta                                                          |
| 909  | WithdrawCleanupAddOnContentsWithNoRightsRecommendation                                             |
| 910  | \[6.0.0+\]                                                                                         |
| 911  | \[6.0.0+\]                                                                                         |
| 912  | \[6.0.0+\]                                                                                         |
| 1000 | RequestVerifyApplicationDeprecated                                                                 |
| 1001 | CorruptApplicationForDebug                                                                         |
| 1002 | RequestVerifyAddOnContentsRights                                                                   |
| 1003 | RequestVerifyApplication                                                                           |
| 1004 | CorruptContentForDebug                                                                             |
| 1200 | NeedsUpdateVulnerability                                                                           |
| 1300 | IsAnyApplicationEntityInstalled                                                                    |
| 1301 | DeleteApplicationContentEntities                                                                   |
| 1302 | CleanupUnrecordedApplicationEntity                                                                 |
| 1303 | CleanupAddOnContentsWithNoRights                                                                   |
| 1304 | DeleteApplicationContentEntity                                                                     |
| 1305 | \[?.?.?-5.1.0\] TryDeleteRunningApplicationEntity                                                  |
| 1306 | \[?.?.?-5.1.0\] TryDeleteRunningApplicationCompletely                                              |
| 1307 | \[?.?.?-5.1.0\] TryDeleteRunningApplicationContentEntities                                         |
| 1308 | \[6.0.0+\]                                                                                         |
| 1309 | \[6.0.0+\]                                                                                         |
| 1400 | PrepareShutdown                                                                                    |
| 1500 | FormatSdCard                                                                                       |
| 1501 | NeedsSystemUpdateToFormatSdCard                                                                    |
| 1502 | GetLastSdCardFormatUnexpectedResult                                                                |
| 1504 | InsertSdCard                                                                                       |
| 1505 | RemoveSdCard                                                                                       |
| 1600 | GetSystemSeedForPseudoDeviceId                                                                     |
| 1601 | ResetSystemSeedForPseudoDeviceId                                                                   |
| 1700 | ListApplicationDownloadingContentMeta                                                              |
| 1701 | GetApplicationView                                                                                 |
| 1702 | GetApplicationDownloadTaskStatus                                                                   |
| 1703 | GetApplicationViewDownloadErrorContext                                                             |
| 1800 | IsNotificationSetupCompleted                                                                       |
| 1801 | GetLastNotificationInfoCount                                                                       |
| 1802 | ListLastNotificationInfo                                                                           |
| 1803 | ListNotificationTask                                                                               |
| 1900 | IsActiveAccount                                                                                    |
| 1901 | RequestDownloadApplicationPrepurchasedRights                                                       |
| 1902 | GetApplicationTicketInfo                                                                           |
| 2000 | GetSystemDeliveryInfo                                                                              |
| 2001 | SelectLatestSystemDeliveryInfo                                                                     |
| 2002 | VerifyDeliveryProtocolVersion                                                                      |
| 2003 | GetApplicationDeliveryInfo                                                                         |
| 2004 | HasAllContentsToDeliver                                                                            |
| 2005 | CompareApplicationDeliveryInfo                                                                     |
| 2006 | CanDeliverApplication                                                                              |
| 2007 | ListContentMetaKeyToDeliverApplication                                                             |
| 2008 | NeedsSystemUpdateToDeliverApplication                                                              |
| 2009 | EstimateRequiredSize                                                                               |
| 2010 | RequestReceiveApplication                                                                          |
| 2011 | CommitReceiveApplication                                                                           |
| 2012 | GetReceiveApplicationProgress                                                                      |
| 2013 | RequestSendApplication                                                                             |
| 2014 | GetSendApplicationProgress                                                                         |
| 2015 | CompareSystemDeliveryInfo                                                                          |
| 2016 | ListNotCommittedContentMeta                                                                        |
| 2017 | CreateDownloadTask                                                                                 |
| 2018 | \[6.0.0+\]                                                                                         |
| 2050 | \[6.0.0+\]                                                                                         |
| 2100 | \[6.0.0+\]                                                                                         |
| 2101 | \[6.0.0+\]                                                                                         |
| 2150 | \[6.0.0+\]                                                                                         |
| 2151 | \[6.0.0+\]                                                                                         |
| 2152 | \[6.0.0+\]                                                                                         |
| 2153 | \[6.0.0+\]                                                                                         |
| 2154 | \[6.0.0+\]                                                                                         |
| 2160 | \[6.0.0+\]                                                                                         |
| 2161 | \[6.0.0+\]                                                                                         |
| 2170 | \[6.0.0+\]                                                                                         |
| 2171 | \[6.0.0+\]                                                                                         |
| 2180 | \[6.0.0+\]                                                                                         |
| 2181 | \[6.0.0+\]                                                                                         |
| 2182 | \[6.0.0+\]                                                                                         |
| 2190 | \[6.0.0+\]                                                                                         |
| 2199 | \[6.0.0+\]                                                                                         |
| 2200 | \[6.0.0+\]                                                                                         |
| 2201 | \[6.0.0+\]                                                                                         |
| 2250 | \[6.0.0+\]                                                                                         |
| 2300 | \[6.0.0+\]                                                                                         |
|      |                                                                                                    |

### IApplicationVersionInterface

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

| Cmd | Name                          |
| --- | ----------------------------- |
| 21  | GetApplicationContentPath     |
| 23  | ResolveApplicationContentPath |
|     |                               |

### IDownloadTaskInterface

This is "nn::ns::detail::IDownloadTaskInterface".

| Cmd | Name                                    |
| --- | --------------------------------------- |
| 701 | ClearTaskStatusList                     |
| 702 | RequestDownloadTaskList                 |
| 703 | RequestEnsureDownloadTask               |
| 704 | ListDownloadTaskStatus                  |
| 705 | RequestDownloadTaskListData             |
| 706 | TryCommitCurrentApplicationDownloadTask |
| 707 | EnableAutoCommit                        |
| 708 | DisableAutoCommit                       |
| 709 | TriggerDynamicCommitEvent               |
|     |                                         |

### IECommerceInterface

| Cmd | Name              |
| --- | ----------------- |
| 0   | RequestLinkDevice |
|     |                   |

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

| Cmd  | Name                                       |
| ---- | ------------------------------------------ |
| 1200 | \[3.0.0+\] NeedsUpdateVulnerability        |
| 1201 | \[4.0.0+\] UpdateSafeSystemVersionForDebug |
| 1202 | \[4.0.0+\] GetSafeSystemVersion            |
|      |                                            |

# ns:su

This is "nn::ns::detail::ISystemUpdateInterface".

| Cmd | Name                                                        |
| --- | ----------------------------------------------------------- |
| 0   | GetBackgroundNetworkUpdateState                             |
| 1   | [OpenSystemUpdateControl](#ISystemUpdateControl "wikilink") |
| 2   | NotifyExFatDriverRequired                                   |
| 3   | ClearExFatDriverStatusForDebug                              |
| 4   | RequestBackgroundNetworkUpdate                              |
| 5   | NotifyBackgroundNetworkUpdate                               |
| 6   | NotifyExFatDriverDownloadedForDebug                         |
| 9   | GetSystemUpdateNotificationEventForContentDelivery          |
| 10  | NotifySystemUpdateForContentDelivery                        |
| 11  | PrepareShutdown                                             |
| 16  | DestroySystemUpdateTask                                     |
| 17  | RequestSendSystemUpdate                                     |
| 18  | GetSendSystemUpdateProgress                                 |
|     |                                                             |

## ISystemUpdateControl

| Cmd | Name                              |
| --- | --------------------------------- |
| 0   | HasDownloaded                     |
| 1   | RequestCheckLatestUpdate          |
| 2   | RequestDownloadLatestUpdate       |
| 3   | GetDownloadProgress               |
| 4   | ApplyDownloadedUpdate             |
| 5   | RequestPrepareCardUpdate          |
| 6   | GetPrepareCardUpdateProgress      |
| 7   | HasPreparedCardUpdate             |
| 8   | ApplyCardUpdate                   |
| 9   | GetDownloadedEulaDataSize         |
| 10  | GetDownloadedEulaData             |
| 11  | SetupCardUpdate                   |
| 12  | GetPreparedCardUpdateEulaDataSize |
| 13  | GetPreparedCardUpdateEulaData     |
| 14  | SetupCardUpdateViaSystemUpdater   |
| 15  | HasReceived                       |
| 16  | RequestReceiveSystemUpdate        |
| 17  | GetReceiveProgress                |
| 18  | ApplyReceivedUpdate               |
| 19  | GetReceivedEulaDataSize           |
| 20  | GetReceivedEulaData               |
| 21  | SetupToReceiveSystemUpdate        |
|     |                                   |

# ns:dev

This is
"nn::ns::detail::IDevelopInterface".

| Cmd | Name                                                                           |
| --- | ------------------------------------------------------------------------------ |
| 0   | [\#LaunchProgram](#LaunchProgram "wikilink")                                   |
| 1   | [\#TerminateProcess](#TerminateProcess "wikilink")                             |
| 2   | [\#TerminateProgram](#TerminateProgram "wikilink")                             |
| 4   | [\#GetShellEventHandle](#GetShellEventHandle "wikilink")                       |
| 5   | [\#GetShellEventInfo](#GetShellEventInfo "wikilink")                           |
| 6   | [\#TerminateApplication](#TerminateApplication "wikilink")                     |
| 7   | [\#PrepareLaunchProgramFromHost](#PrepareLaunchProgramFromHost "wikilink")     |
| 8   | [\#LaunchApplication](#LaunchApplication_2 "wikilink")                         |
| 9   | [\#LaunchApplicationWithStorageId](#LaunchApplicationWithStorageId "wikilink") |
|     |                                                                                |

## LaunchProgram

Wrapper for "pm:shell"
[LaunchProcess](Process%20Manager%20services#LaunchProcess.md##LaunchProcess "wikilink").

## TerminateProcess

Wrapper for "pm:shell"
[TerminateTitleByPid](Process%20Manager%20services#TerminateTitleByPid.md##TerminateTitleByPid "wikilink").

## TerminateProgram

Wrapper for "pm:shell"
[TerminateTitleByTitleId](Process%20Manager%20services#TerminateTitleByTitleId.md##TerminateTitleByTitleId "wikilink").

## GetShellEventHandle

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

## LaunchApplication

Takes an input u32
[launch\_flags](Process%20Manager%20services.md "wikilink") and u64
titleID, returns an output u64 PID.

Same as LaunchApplicationWithStorageId except the last two params passed
to the internal vtable funcptr call are value 0x6, instead of from the
command input.

## LaunchApplicationWithStorageId

Takes 2 input u8s, an u32
[launch\_flags](Process%20Manager%20services.md "wikilink"), and an u64
titleID. Returns an output u64 PID.

Launches an application title which is registered with NS.

[Category:Services](Category:Services "wikilink")

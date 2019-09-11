# friend:u, friend:v, friend:m, friend:s, friend:a

This is "nn::friends::detail::ipc::IServiceCreator".

| Cmd | Name                                         | Notes                                                                                         |
| --- | -------------------------------------------- | --------------------------------------------------------------------------------------------- |
| 0   | CreateFriendService                          | Returns an [\#IFriendService](#IFriendService "wikilink").                                    |
| 1   | \[2.0.0+\] CreateNotificationService         | Takes an input userID and returns [\#INotificationService](#INotificationService "wikilink"). |
| 2   | \[4.0.0+\] CreateDaemonSuspendSessionService | Returns an [\#IDaemonSuspendSessionService](#IDaemonSuspendSessionService "wikilink").        |

## IFriendService

This is "nn::friends::detail::ipc::IFriendService".

| Cmd   | Name                                                     |
| ----- | -------------------------------------------------------- |
| 0     | GetCompletionEvent                                       |
| 1     | Cancel                                                   |
| 10100 | GetFriendListIds                                         |
| 10101 | GetFriendList                                            |
| 10102 | UpdateFriendInfo                                         |
| 10110 | GetFriendProfileImage                                    |
| 10200 | SendFriendRequestForApplication                          |
| 10211 | AddFacedFriendRequestForApplication                      |
| 10400 | GetBlockedUserListIds                                    |
| 10500 | GetProfileList                                           |
| 10600 | DeclareOpenOnlinePlaySession                             |
| 10601 | DeclareCloseOnlinePlaySession                            |
| 10610 | UpdateUserPresence                                       |
| 10700 | GetPlayHistoryRegistrationKey                            |
| 10701 | GetPlayHistoryRegistrationKeyWithNetworkServiceAccountId |
| 10702 | AddPlayHistory                                           |
| 11000 | GetProfileImageUrl                                       |
| 20100 | GetFriendCount                                           |
| 20101 | GetNewlyFriendCount                                      |
| 20102 | GetFriendDetailedInfo                                    |
| 20103 | SyncFriendList                                           |
| 20104 | RequestSyncFriendList                                    |
| 20110 | LoadFriendSetting                                        |
| 20200 | GetReceivedFriendRequestCount                            |
| 20201 | GetFriendRequestList                                     |
| 20300 | GetFriendCandidateList                                   |
| 20301 | \[3.0.0+\] GetNintendoNetworkIdInfo                      |
| 20302 | \[5.0.0+\] GetSnsAccountLinkage                          |
| 20303 | \[5.0.0+\] GetSnsAccountProfile                          |
| 20304 | \[5.0.0+\] GetSnsAccountFriendList                       |
| 20400 | GetBlockedUserList                                       |
| 20401 | SyncBlockedUserList                                      |
| 20500 | GetProfileExtraList                                      |
| 20501 | GetRelationship                                          |
| 20600 | GetUserPresenceView                                      |
| 20700 | GetPlayHistoryList                                       |
| 20701 | GetPlayHistoryStatistics                                 |
| 20800 | LoadUserSetting                                          |
| 20801 | SyncUserSetting                                          |
| 20900 | RequestListSummaryOverlayNotification                    |
| 21000 | GetExternalApplicationCatalog                            |
| 22000 | \[9.0.0+\] GetReceivedFriendInvitationList               |
| 22001 | \[9.0.0+\] GetReceivedFriendInvitationDetailedInfo       |
| 22010 | \[9.0.0+\] GetReceivedFriendInvitationCountCache         |
| 30100 | DropFriendNewlyFlags                                     |
| 30101 | DeleteFriend                                             |
| 30110 | DropFriendNewlyFlag                                      |
| 30120 | ChangeFriendFavoriteFlag                                 |
| 30121 | ChangeFriendOnlineNotificationFlag                       |
| 30200 | SendFriendRequest                                        |
| 30201 | SendFriendRequestWithApplicationInfo                     |
| 30202 | CancelFriendRequest                                      |
| 30203 | AcceptFriendRequest                                      |
| 30204 | RejectFriendRequest                                      |
| 30205 | ReadFriendRequest                                        |
| 30210 | GetFacedFriendRequestRegistrationKey                     |
| 30211 | AddFacedFriendRequest                                    |
| 30212 | CancelFacedFriendRequest                                 |
| 30213 | GetFacedFriendRequestProfileImage                        |
| 30214 | GetFacedFriendRequestProfileImageFromPath                |
| 30215 | SendFriendRequestWithExternalApplicationCatalogId        |
| 30216 | ResendFacedFriendRequest                                 |
| 30217 | \[3.0.0+\] SendFriendRequestWithNintendoNetworkIdInfo    |
| 30300 | \[5.0.0+\] GetSnsAccountLinkPageUrl                      |
| 30301 | \[5.0.0+\] UnlinkSnsAccount                              |
| 30400 | BlockUser                                                |
| 30401 | BlockUserWithApplicationInfo                             |
| 30402 | UnblockUser                                              |
| 30500 | GetProfileExtraFromFriendCode                            |
| 30700 | DeletePlayHistory                                        |
| 30810 | ChangePresencePermission                                 |
| 30811 | ChangeFriendRequestReception                             |
| 30812 | ChangePlayLogPermission                                  |
| 30820 | IssueFriendCode                                          |
| 30830 | ClearPlayLog                                             |
| 30900 | \[9.0.0+\] SendFriendInvitation                          |
| 30910 | \[9.0.0+\] ReadFriendInvitation                          |
| 49900 | DeleteNetworkServiceAccountCache                         |

## INotificationService

This is "nn::friends::detail::ipc::INotificationService".

| Cmd | Name                | Notes                          |
| --- | ------------------- | ------------------------------ |
| 0   | \[2.0.0+\] GetEvent | Returns an output event handle |
| 1   | \[2.0.0+\] Clear    |                                |
| 2   | \[2.0.0+\] Pop      |                                |

## IDaemonSuspendSessionService

This is "nn::friends::detail::ipc::IDaemonSuspendSessionService".

| Cmd | Name       |
| --- | ---------- |
| 0   | \[4.0.0+\] |
| 1   | \[4.0.0+\] |
| 2   | \[4.0.0+\] |
| 3   | \[4.0.0+\] |
| 4   | \[4.0.0+\] |

# nd:app

This is "nn::nd::detail::IServiceForApplication".

This was added with \[5.0.0+\] and removed with \[6.0.0+\].

| Cmd | Name                              |
| --- | --------------------------------- |
| 0   | GetReceivableNeighborInfoCountMax |
| 10  | IsNeighborDetectionEnabled        |

# nd:sys

This is "nn::nd::detail::IServiceForSystem".

This was added with \[5.0.0+\] and removed with \[6.0.0+\].

| Cmd | Name                                        |
| --- | ------------------------------------------- |
| 0   | GetReceivableNeighborInfoCountMax           |
| 10  | IsNeighborDetectionEnabled                  |
| 200 | SetSystemData                               |
| 201 | ClearSystemData                             |
| 203 | GetReceivableNeighborInfoCountForSystem     |
| 204 | ReceiveNeighborInfoForSystem                |
| 205 | SetSender                                   |
| 206 | GetSender                                   |
| 207 | CreateScannerForSystem                      |
| 208 | CreateReceiveEventHolderForSystem           |
| 223 | EnableNeighborDetection                     |
| 224 | DisableNeighborDetection                    |
| 226 | EnablePowerSave                             |
| 227 | DisablePowerSave                            |
| 228 | IsPowerSaveEnabled                          |
| 232 | ClearBlockedUsers                           |
| 233 | GetBlockedUserCount                         |
| 234 | BlockUserByLocalUserId                      |
| 235 | BlockUserByNetworkUserId                    |
| 236 | UnblockUserByLocalUserId                    |
| 237 | UnblockUserByNetworkUserId                  |
| 240 | DeleteApplication                           |
| 250 | InitializeApplicationInfo                   |
| 260 | CreateAccountSystemSaveDataAccessSuppressor |
| 300 | AddReceivedNeighborInfoForSystemForDebug    |
| 301 | GetSendDataForDebug                         |
| 302 | ClearReceiveCounterForDebug                 |
| 303 | GetNextReceiveCounterForDebug               |
| 304 | ListBlockedUsersForDebug                    |
| 305 | RefreshSendDataIdForDebug                   |
| 306 | ReloadFwdbgSettingsForDebug                 |
| 307 | EnableApplicationForDebug                   |
| 308 | GetNextReceiveCountersForDebug              |
| 309 | ListApplicationInfoForDebug                 |
| 310 | SetApplicationDataForDebug                  |
| 400 | GetNetworkUserId                            |
| 401 | DeleteNetworkUserId                         |

# InAppScreenName

| Offset | Size | Description                                       |
| ------ | ---- | ------------------------------------------------- |
| 0x0    | 0x40 | UTF-8 string, NUL-terminated.                     |
| 0x40   | 0x8  | [LanguageCode](Settings%20services.md "wikilink") |

This is "nn::friends::InAppScreenName". This is a 0x48-byte struct.

[Category:Services](Category:Services "wikilink")

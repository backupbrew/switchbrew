# nim

This is "nn::nim::detail::INetworkInstallManager".

| Cmd | Name                                                             |
| --- | ---------------------------------------------------------------- |
| 0   | CreateSystemUpdateTask                                           |
| 1   | [\#DestroySystemUpdateTask](#DestroySystemUpdateTask "wikilink") |
| 2   | [\#ListSystemUpdateTask](#ListSystemUpdateTask "wikilink")       |
| 3   | RequestSystemUpdateTaskRun                                       |
| 4   | GetSystemUpdateTaskInfo                                          |
| 5   | CommitSystemUpdateTask                                           |
| 6   | CreateNetworkInstallTask                                         |
| 7   | DestroyNetworkInstallTask                                        |
| 8   | ListNetworkInstallTask                                           |
| 9   | RequestNetworkInstallTaskRun                                     |
| 10  | GetNetworkInstallTaskInfo                                        |
| 11  | CommitNetworkInstallTask                                         |
| 12  | RequestLatestSystemUpdateMeta                                    |
| 14  | ListApplicationNetworkInstallTask                                |
| 15  | ListNetworkInstallTaskContentMeta                                |
| 16  | RequestLatestVersion                                             |
| 17  | SetNetworkInstallTaskAttribute                                   |
| 18  | AddNetworkInstallTaskContentMeta                                 |
| 19  | GetDownloadedSystemDataPath                                      |
| 20  | CalculateNetworkInstallTaskRequiredSize                          |
| 21  | IsExFatDriverIncluded                                            |
| 22  | GetBackgroundDownloadStressTaskInfo                              |
| 23  | \[2.0.0+\] RequestDeviceAuthenticationToken                      |
| 24  | \[2.0.0+\] RequestGameCardRegistrationStatus                     |
| 25  | \[2.0.0+\] RequestRegisterGameCard                               |
| 26  | \[2.0.0+\] RequestRegisterNotificationToken                      |
| 27  | \[2.0.0+\] RequestDownloadTaskList                               |
| 28  | \[2.0.0+\] RequestApplicationControl                             |
| 29  | \[2.0.0+\] RequestLatestApplicationControl                       |
| 30  | \[2.0.0+\] RequestVersionList                                    |
| 31  | \[2.0.0+\] CreateApplyDeltaTask                                  |
| 32  | \[2.0.0+\] DestroyApplyDeltaTask                                 |
| 33  | \[2.0.0+\] ListApplicationApplyDeltaTask                         |
| 34  | \[2.0.0+\] RequestApplyDeltaTaskRun                              |
| 35  | \[2.0.0+\] GetApplyDeltaTaskInfo                                 |
| 36  | \[2.0.0+\] ListApplyDeltaTask                                    |
| 37  | \[2.0.0+\] CommitApplyDeltaTask                                  |
| 38  | \[2.0.0+\] CalculateApplyDeltaTaskRequiredSize                   |
| 39  | \[2.0.0+\] PrepareShutdown                                       |
| 40  | \[2.0.0+\] ListApplyDeltaTask2                                   |
| 41  | \[2.0.0+\] ClearNotEnoughSpaceStateOfApplyDeltaTask              |
| 42  | \[3.0.0+\]                                                       |
| 43  | \[3.0.0+\]                                                       |
| 44  | \[3.0.0+\]                                                       |
| 45  | \[3.0.0+\]                                                       |
| 46  | \[3.0.0+\]                                                       |
| 47  | \[4.0.0+\]                                                       |
| 48  | \[4.0.0+\]                                                       |
| 49  | \[4.0.0+\]                                                       |
| 50  | \[4.0.0+\]                                                       |
| 51  | \[4.0.0+\]                                                       |
| 52  | \[4.0.0+\]                                                       |
| 53  | \[4.0.0+\]                                                       |
| 54  | \[4.0.0+\]                                                       |
| 55  | \[4.0.0+\]                                                       |
| 56  | \[4.0.0+\]                                                       |
| 57  | \[4.0.0+\]                                                       |
| 58  | \[4.0.0+\]                                                       |
| 59  | \[4.0.0+\]                                                       |
| 60  | \[4.0.0+\]                                                       |
| 61  | \[4.0.0+\]                                                       |
| 62  | \[4.0.0+\]                                                       |
| 63  | \[4.0.0+\]                                                       |
| 64  | \[4.0.0+\]                                                       |
| 65  | \[4.0.0+\]                                                       |
| 66  | \[4.0.0+\]                                                       |
| 67  | \[4.0.0+\]                                                       |
| 68  | \[4.0.0+\]                                                       |
| 69  | \[4.0.0+\]                                                       |
| 70  | \[4.0.0+\]                                                       |
| 71  | \[4.0.0+\]                                                       |
| 72  | \[4.0.0+\]                                                       |
| 73  | \[4.0.0+\]                                                       |
| 74  | \[4.0.0+\]                                                       |
| 75  | \[4.0.0+\]                                                       |
| 76  | \[4.0.0+\]                                                       |
| 77  | \[4.0.0+\]                                                       |
| 78  | \[4.0.0+\]                                                       |
| 79  | \[4.0.0+\]                                                       |
| 80  | \[4.0.0+\]                                                       |
| 81  | \[4.0.0+\]                                                       |
| 82  | \[4.0.0+\]                                                       |
| 83  | \[4.0.0+\]                                                       |
| 84  | \[5.0.0+\]                                                       |
| 85  | \[5.0.0+\]                                                       |
| 86  | \[5.0.0+\]                                                       |
| 87  | \[6.0.0+\]                                                       |
| 88  | \[6.0.0+\]                                                       |
| 89  | \[6.0.0+\]                                                       |
| 90  | \[6.0.0+\]                                                       |
| 91  | \[6.0.0+\]                                                       |
| 92  | \[6.0.0+\]                                                       |
| 93  | \[6.0.0+\]                                                       |
| 94  | \[6.0.0+\]                                                       |
| 95  | \[6.0.0+\]                                                       |
| 96  | \[6.0.0+\]                                                       |
| 97  | \[6.0.0+\]                                                       |
| 98  | \[6.0.0+\]                                                       |
| 99  | \[7.0.0+\]                                                       |

\[3.0.0+\] GetSystemUpdateTaskInfo now returns an additional 0x10-bytes
of output. GetNetworkInstallTaskInfo now returns an additional
0x18-bytes of output. GetApplyDeltaTaskInfo now returns an additional
0x10-bytes of output.

\[8.0.0+\] Cmd76 now takes an additional 0x8-bytes of input.

## DestroySystemUpdateTask

Takes a 0x10-byte input struct, from the output of ListSystemUpdateTask.

## ListSystemUpdateTask

Takes a type-0x6 output buffer, for an array of 0x10-byte entries.
Returns an u32 for total output entries.

Doesn't return anything on a v2.1 system where sysupdate domains are
blocked.

# nim:shp

This is "nn::nim::detail::IShopServiceManager".

| Cmd | Name                                                                                                           |
| --- | -------------------------------------------------------------------------------------------------------------- |
| 0   | RequestDeviceAuthenticationToken                                                                               |
| 1   | \[3.0.0+\] RequestCachedDeviceAuthenticationToken                                                              |
| 100 | RequestRegisterDeviceAccount                                                                                   |
| 101 | RequestUnregisterDeviceAccount                                                                                 |
| 102 | RequestDeviceAccountStatus                                                                                     |
| 103 | GetDeviceAccountInfo                                                                                           |
| 104 | RequestDeviceRegistrationInfo                                                                                  |
| 105 | RequestTransferDeviceAccount                                                                                   |
| 106 | \[3.0.0+\] RequestSyncRegistration                                                                             |
| 107 | \[3.0.0+\] IsOwnDeviceId                                                                                       |
| 200 | RequestRegisterNotificationToken                                                                               |
| 300 | RequestUnlinkDevice                                                                                            |
| 301 | RequestUnlinkDeviceIntegrated                                                                                  |
| 302 | RequestLinkDevice                                                                                              |
| 303 | HasDeviceLink                                                                                                  |
| 304 | \[4.0.0+\] RequestUnlinkDeviceAll                                                                              |
| 305 | \[4.0.0+\] RequestCreateVirtualAccount                                                                         |
| 306 | \[4.0.0+\] RequestDeviceLinkStatus                                                                             |
| 400 | GetAccountByVirtualAccount                                                                                     |
| 401 | \[6.0.0+\]                                                                                                     |
| 500 | RequestSyncTicket                                                                                              |
| 501 | RequestDownloadTicket                                                                                          |
| 502 | \[4.0.0+\] RequestDownloadTicketForPrepurchasedContents. \[6.0.0+\]: Now takes an additional 4-bytes of input. |

# nim:eca

This is "nn::nim::detail::IShopServiceAccessServerInterface".

| Cmd | Name                                |
| --- | ----------------------------------- |
| 0   | CreateServerInterface               |
| 1   | \[6.0.0+\] RefreshDebugAvailability |
| 2   | \[6.0.0+\] ClearDebugResponse       |
| 3   | \[6.0.0+\] RegisterDebugResponse    |

## IShopServiceAccessServer

This is "nn::nim::detail::IShopServiceAccessServer".

| Cmd | Name                    |
| --- | ----------------------- |
| 0   | CreateAccessorInterface |

### IShopServiceAccessor

This is "nn::nim::detail::IShopServiceAccessor".

| Cmd | Name                 |
| --- | -------------------- |
| 0   | CreateAsyncInterface |

#### IShopServiceAsync

This is "nn::nim::detail::IShopServiceAsync".

| Cmd | Name         |
| --- | ------------ |
| 0   | Cancel       |
| 1   | GetSize      |
| 2   | Read         |
| 3   | GetErrorCode |
| 4   | Request      |
| 5   | Prepare      |

# nim:ecas

This is "nn::nim::detail::IShopServiceAccessSystemInterface".

This was added with \[7.0.0+\].

| Cmd | Name                    |
| --- | ----------------------- |
| 0   | RegisterSpecialClient   |
| 1   | UnregisterSpecialClient |

# ntc

This is "nn::ntc::detail::<service::IStaticService>".

| Cmd | Name                                      |
| --- | ----------------------------------------- |
| 0   | OpenEnsureNetworkClockAvailabilityService |
| 100 | \[3.0.0+\] SuspendAutonomicTimeCorrection |
| 101 | \[3.0.0+\] ResumeAutonomicTimeCorrection  |

Network-time-sync uses the "\<...\>/time" HTTPS URL listed in the below
Network section. This just returns an UTC Unix time string.

## IEnsureNetworkClockAvailabilityService

This is
"nn::ntc::detail::<service::IEnsureNetworkClockAvailabilityService>".

| Cmd | Name                       |
| --- | -------------------------- |
| 0   | StartTask                  |
| 1   | GetFinishNotificationEvent |
| 2   | GetResult                  |
| 3   | Cancel                     |
| 4   | IsProcessing               |
| 5   | \[3.0.0+\] GetServerTime   |

[Category:Services](Category:Services "wikilink")

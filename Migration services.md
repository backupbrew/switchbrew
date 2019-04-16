Migration is a sysmodule designed for handling the new Switch to Switch
transfer system.

# mig:usr

This is
"nn::migration::user::IService"

| Cmd  | Name                                                                                                                                    |
| ---- | --------------------------------------------------------------------------------------------------------------------------------------- |
| 10   | TryGetLastMigrationInfo                                                                                                                 |
| 100  | CreateServer                                                                                                                            |
| 101  | ResumeServer                                                                                                                            |
| 200  | CreateClient                                                                                                                            |
| 201  | ResumeClient                                                                                                                            |
| 1001 | \[8.0.0+\] ? (Takes a total of 8-bytes of input, returns an [IAsyncNetworkServiceLicenseKindContext](Account%20services.md "wikilink")) |
| 1010 | \[7.0.0+\]                                                                                                                              |
| 1100 | \[7.0.0+\]                                                                                                                              |
| 1101 | \[7.0.0+\]                                                                                                                              |
| 1200 | \[7.0.0+\]                                                                                                                              |
| 1201 | \[7.0.0+\]                                                                                                                              |

## IServer

This is "nn::migration::user::IServer"

| Cmd | Name                     |
| --- | ------------------------ |
| 0   | GetUid                   |
| 1   | GetServerProfile         |
| 100 | PrepareAsync             |
| 101 | GetConnectionRequirement |
| 200 | WaitConnectionAsync      |
| 201 | GetClientProfile         |
| 202 | AcceptConnectionAsync    |
| 203 | DeclineConnectionAsync   |
| 210 | \[8.0.0+\]               |
| 300 | ProcessTransferAsync     |
| 400 | CompleteAsync            |
| 500 | Abort                    |
| 998 | \[8.0.0+\]               |
| 999 | \[8.0.0+\]               |
|     |                          |

## IClient

This is "nn::migration::user::IClient"

| Cmd | Name                                     |
| --- | ---------------------------------------- |
| 0   | GetClientProfile                         |
| 10  | CreateLoginSession                       |
| 11  | GetNetworkServiceAccountId               |
| 12  | GetUserNickname                          |
| 13  | GetUserProfileImage                      |
| 100 | PrepareAsync                             |
| 101 | GetConnectionRequirement                 |
| 200 | ScanServersAsync                         |
| 201 | ListServers                              |
| 210 | ConnectByServerIdAsync                   |
| 220 | \[8.0.0+\]                               |
| 221 | \[8.0.0+\]                               |
| 300 | GetStorageShortfall                      |
| 301 | GetTotalTransferInfo                     |
| 302 | GetImmigrantUid                          |
| 310 | GetCurrentTransferInfo                   |
| 311 | GetCurrentRelatedApplications            |
| 320 | TransferNextAsync                        |
| 350 | SuspendAsync                             |
| 400 | CompleteAsync                            |
| 500 | Abort                                    |
| 996 | \[8.0.0+\]                               |
| 997 | \[8.0.0+\]                               |
| 998 | \[8.0.0+\]                               |
| 999 | DebugSynchronizeStateInFinalizationAsync |
|     |                                          |

## IAsyncContext

This is "nn::migration::user::IAsyncContext"

| Cmd | Name           |
| --- | -------------- |
| 0   | GetSystemEvent |
| 1   | Cancel         |
| 2   | HasDone        |
| 3   | GetResult      |
|     |                |

## IServer

This is "nn::migration::savedata::IServer".

This was added with \[7.0.0+\].

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |
| 100 |      |
| 101 |      |
| 200 |      |
| 201 |      |
| 300 |      |
| 400 |      |
| 500 |      |
|     |      |

## IClient

This is "nn::migration::savedata::IClient".

This was added with \[7.0.0+\].

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 100 |      |
| 200 |      |
| 201 |      |
| 210 |      |
| 300 |      |
| 301 |      |
| 302 |      |
| 303 |      |
| 310 |      |
| 320 |      |
| 350 |      |
| 400 |      |
| 500 |      |
| 999 |      |
|     |      |

[Category:Services](Category:Services "wikilink")

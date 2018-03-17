Migration is a sysmodule designed for handling the new Switch to Switch
transfer system.

# mig:usr

This is "nn::migration::user::IService"

| Cmd | Name                    |
| --- | ----------------------- |
| 10  | TryGetLastMigrationInfo |
| 100 | CreateServer            |
| 101 | ResumeServer            |
| 200 | CreateClient            |
| 201 | ResumeClient            |
|     |                         |

## IServer

"nn::migration::user::IServer"

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
| 300 | ProcessTransferAsync     |
| 400 | CompleteAsync            |
| 500 | Abort                    |
|     |                          |

## IClient

"nn::migration::user::IClient"

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
| 300 | GetStorageShortfall                      |
| 301 | GetTotalTransferInfo                     |
| 302 | GetImmigrantUid                          |
| 310 | GetCurrentTransferInfo                   |
| 311 | GetCurrentRelatedApplications            |
| 320 | TransferNextAsync                        |
| 350 | SuspendAsync                             |
| 400 | CompleteAsync                            |
| 500 | Abort                                    |
| 999 | DebugSynchronizeStateInFinalizationAsync |
|     |                                          |

## IAsyncContext

"nn::migration::user::IAsyncContext"

| Cmd | Name           |
| --- | -------------- |
| 0   | GetSystemEvent |
| 1   | Cancel         |
| 2   | HasDone        |
| 3   | GetResult      |
|     |                |

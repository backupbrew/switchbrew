BCAT (Background Content Asymmetric synchronized delivery and
Transmission) encompasses a set of content download/upload related
services.

# bcat:a, bcat:m, bcat:u, bcat:s

These are "nn::bcat::detail::ipc::IServiceCreator".

| Cmd | Name                                               |
| --- | -------------------------------------------------- |
| 0   | CreateBcatService                                  |
| 1   | CreateDeliveryCacheStorageService                  |
| 2   | CreateDeliveryCacheStorageServiceWithApplicationId |

Equivalent to 3DS BOSS(SpotPass). See
[here](BCAT%20Content%20Container.md "wikilink") for
BCAT-content-container.

## IBcatService

This is
"nn::bcat::detail::ipc::IBcatService".

| Cmd   | Name                                                                                                    |
| ----- | ------------------------------------------------------------------------------------------------------- |
| 10100 | RequestSyncDeliveryCache                                                                                |
| 10101 | \[5.0.0+\] RequestSyncDeliveryCacheWithDirectoryName                                                    |
| 10200 | \[5.0.0+\] CancelSyncDeliveryCacheRequest                                                               |
| 20100 | RequestSyncDeliveryCacheWithApplicationId                                                               |
| 20101 | \[5.0.0+\] RequestSyncDeliveryCacheWithApplicationIdAndDirectoryName                                    |
| 20300 | \[8.0.0+\] [\#GetDeliveryCacheStorageUpdateNotifier](#GetDeliveryCacheStorageUpdateNotifier "wikilink") |
| 20301 | \[8.0.0+\] [\#RequestSuspendDeliveryTask](#RequestSuspendDeliveryTask "wikilink")                       |
| 30100 | SetPassphrase                                                                                           |
| 30200 | RegisterDeliveryTask                                                                                    |
| 30201 | UnregisterDeliveryTask                                                                                  |
| 30202 | BlockDeliveryTask                                                                                       |
| 30203 | UnblockDeliveryTask                                                                                     |
| 30300 | \[8.0.0+\] RegisterSystemApplicationDeliveryTasks                                                       |
| 90100 | GetDeliveryTaskList                                                                                     |
| 90200 | GetDeliveryList                                                                                         |
| 90201 | ClearDeliveryCacheStorage                                                                               |
| 90202 | \[8.0.0+\] ClearDeliveryTaskSubscriptionStatus                                                          |
| 90300 | GetPushNotificationLog                                                                                  |

### GetDeliveryCacheStorageUpdateNotifier

Takes a total of 8-bytes of input, returns an
[\#INotifierService](#INotifierService "wikilink").

### RequestSuspendDeliveryTask

Takes a total of 8-bytes of input, returns an
[\#IDeliveryTaskSuspensionService](#IDeliveryTaskSuspensionService "wikilink").

### IDeliveryCacheProgressService

This is "nn::bcat::detail::ipc::IDeliveryCacheProgressService".

| Cmd | Name     |
| --- | -------- |
| 0   | GetEvent |
| 1   | GetImpl  |

## IDeliveryCacheStorageService

This is "nn::bcat::detail::ipc::IDeliveryCacheStorageService".

| Cmd | Name                            |
| --- | ------------------------------- |
| 0   | CreateFileService               |
| 1   | CreateDirectoryService          |
| 10  | EnumerateDeliveryCacheDirectory |

### IDeliveryCacheFileService

This is "nn::bcat::detail::ipc::IDeliveryCacheFileService".

| Cmd | Name      |
| --- | --------- |
| 0   | Open      |
| 1   | Read      |
| 2   | GetSize   |
| 3   | GetDigest |

### IDeliveryCacheDirectoryService

This is "nn::bcat::detail::ipc::IDeliveryCacheDirectoryService".

| Cmd | Name     |
| --- | -------- |
| 0   | Open     |
| 1   | Read     |
| 2   | GetCount |

### INotifierService

This is "nn::bcat::detail::ipc::INotifierService".

Added with \[8.0.0+\].

| Cmd | Name     | Notes |
| --- | -------- | ----- |
| 0   | GetEvent |       |

### IDeliveryTaskSuspensionService

This is "nn::bcat::detail::ipc::IDeliveryTaskSuspensionService".

Added with \[8.0.0+\].

| Cmd | Name     | Notes |
| --- | -------- | ----- |
| 0   | GetEvent |       |

# news:a, news:c, news:m, news:p, news:v

These are
"nn::news::detail::ipc::IServiceCreator".

| Cmd | Name | Notes                                                                                    |
| --- | ---- | ---------------------------------------------------------------------------------------- |
| 0   |      | No input, returns an [\#INewsService](#INewsService "wikilink").                         |
| 1   |      | No input, returns an [\#INewlyArrivedEventHolder](#INewlyArrivedEventHolder "wikilink"). |
| 2   |      | No input, returns an [\#INewsDataService](#INewsDataService "wikilink").                 |
| 3   |      | No input, returns an [\#INewsDatabaseService](#INewsDatabaseService "wikilink").         |
| 4   |      | No input, returns an [\#IOverwriteEventHolder](#IOverwriteEventHolder "wikilink").       |

## INewsService

This is
"nn::news::detail::ipc::INewsService".

| Cmd   | Name                                                                                                                                     |
| ----- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| 10100 |                                                                                                                                          |
| 20100 |                                                                                                                                          |
| 30100 |                                                                                                                                          |
| 30101 |                                                                                                                                          |
| 30110 | \[6.0.0+\]                                                                                                                               |
| 30200 |                                                                                                                                          |
| 30201 | \[8.0.0+\]                                                                                                                               |
| 30300 |                                                                                                                                          |
| 30400 |                                                                                                                                          |
| 30500 | \[8.0.0+\] ? (Takes a total of 8-bytes of input, a handle, and a type-0x9 input buffer, returns an [\#IUnknown2](#IUnknown2 "wikilink")) |
| 40100 |                                                                                                                                          |
| 40101 |                                                                                                                                          |
| 40200 |                                                                                                                                          |
| 40201 |                                                                                                                                          |
| 90100 |                                                                                                                                          |

## INewlyArrivedEventHolder

This is "nn::news::detail::ipc::INewlyArrivedEventHolder".

| Cmd | Name |
| --- | ---- |
| 0   |      |

## INewsDataService

This is "nn::news::detail::ipc::INewsDataService".

| Cmd  | Name       |
| ---- | ---------- |
| 0    |            |
| 1    |            |
| 2    |            |
| 3    |            |
| 1001 | \[6.0.0+\] |

## INewsDatabaseService

This is "nn::news::detail::ipc::INewsDatabaseService".

| Cmd  | Name       |
| ---- | ---------- |
| 0    |            |
| 1    |            |
| 2    |            |
| 3    |            |
| 4    |            |
| 5    |            |
| 1000 | \[6.0.0+\] |

## IOverwriteEventHolder

This is "nn::news::detail::ipc::IOverwriteEventHolder".

| Cmd | Name |
| --- | ---- |
| 0   |      |

## IUnknown2

This was added with \[8.0.0+\].

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |
| 3   |      |

# prepo:a, prepo:a2, prepo:m, prepo:u, prepo:s

These are
"nn::prepo::detail::ipc::IPrepoService".

| Cmd                   | Name                                                            |
| --------------------- | --------------------------------------------------------------- |
| 10100                 | SaveReportOld (\[1.0.0-5.1.0\] SaveReport)                      |
| 10101                 | SaveReportWithUserOld (\[1.0.0-5.1.0\] SaveReportWithUser)      |
| 10102                 | \[6.0.0+\] SaveReport                                           |
| 10103                 | \[6.0.0+\] SaveReportWithUser                                   |
| 10200                 | RequestImmediateTransmission                                    |
| 10300                 | GetTransmissionStatus                                           |
| 20100                 | SaveSystemReport                                                |
| 20101                 | SaveSystemReportWithUser                                        |
| 20200                 | \[4.0.0+\] SetOperationMode                                     |
| 30100                 | ClearStorage                                                    |
| 30200                 | \[6.0.0+\] ClearStatistics                                      |
| 30300                 | \[6.0.0+\] GetStorageUsage                                      |
| 30400                 | \[6.0.0+\] GetStatistics                                        |
| 30401                 | \[6.0.0+\] GetThroughputHistory                                 |
| 30500                 | \[6.0.0+\] GetLastUploadError                                   |
| 40100                 | IsUserAgreementCheckEnabled                                     |
| 40101                 | SetUserAgreementCheckEnabled                                    |
| 90100                 | \[6.0.0+\] ReadAllReportFiles (\[1.0.0-5.1.0\] GetStorageUsage) |
| \[5.0.0-5.1.0\] 90200 |                                                                 |
| \[5.0.0-5.1.0\] 90201 |                                                                 |
| \[5.0.0-5.1.0\] 90300 |                                                                 |

## Data reporting

The "Play Report" (prepo) service uploads system and user information to
a cloud server. This includes the following fields:

`sys_info`  
`data`  
`application_id`  
`event_id`  
`operation_mode`  
`lc_recorded_at (followed by a timestamp)`  
`nc_recorded_at (followed by a timestamp)`  
`nsa_id`  
`os_version`

And the contents of the following file:

`is_user_agreement_check_enabled.bin`

All the information is periodically uploaded to the following URL:  
\* https://receive-%.dg.srv.nintendo.net/post

It also checks the validity of the device's authentication token using
the following URL:  
\* https://dauth-%.ndas.srv.nintendo.net/v1/device\_auth\_token

[Category:Services](Category:Services "wikilink")

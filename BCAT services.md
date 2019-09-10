BCAT (Background Content Asymmetric synchronized delivery and
Transmission) encompasses a set of content download/upload related
services.

# bcat:a, bcat:m, bcat:u, bcat:s

These are "nn::bcat::detail::ipc::IServiceCreator".

These were added with \[2.0.0+\].

| Cmd               | Name                                                | Notes                                                                                                                 |
| ----------------- | --------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| 0                 | CreateBcatService                                   | Takes an input u64 ProcessId, returns an [\#IBcatService](#IBcatService "wikilink")                                   |
| 1                 | CreateDeliveryCacheStorageService                   | Takes an input u64 ProcessId, returns an [\#IDeliveryCacheStorageService](#IDeliveryCacheStorageService "wikilink")   |
| 2                 | CreateDeliveryCacheStorageServiceWithApplicationId  | Takes an input u64 TitleId, returns an [\#IDeliveryCacheStorageService](#IDeliveryCacheStorageService "wikilink")     |
| \[2.0.0-2.3.0\] 3 | CreateDeliveryCacheProgressService                  | Takes an input u64 ProcessId, returns an [\#IDeliveryCacheProgressService](#IDeliveryCacheProgressService "wikilink") |
| \[2.0.0-2.3.0\] 4 | CreateDeliveryCacheProgressServiceWithApplicationId | Takes an input u64 TitleId, returns an [\#IDeliveryCacheProgressService](#IDeliveryCacheProgressService "wikilink")   |

Equivalent to 3DS BOSS(SpotPass). See
[here](BCAT%20Content%20Container.md "wikilink") for
BCAT-content-container.

## IBcatService

This is "nn::bcat::detail::ipc::IBcatService".

This was added with \[2.0.0+\].

| Cmd   | Name                                                                                                    |
| ----- | ------------------------------------------------------------------------------------------------------- |
| 10100 | [\#RequestSyncDeliveryCache](#RequestSyncDeliveryCache "wikilink")                                      |
| 10101 | \[5.0.0+\] RequestSyncDeliveryCacheWithDirectoryName                                                    |
| 10200 | \[5.0.0+\] CancelSyncDeliveryCacheRequest                                                               |
| 20100 | [\#RequestSyncDeliveryCacheWithApplicationId](#RequestSyncDeliveryCacheWithApplicationId "wikilink")    |
| 20101 | \[5.0.0+\] RequestSyncDeliveryCacheWithApplicationIdAndDirectoryName                                    |
| 20300 | \[8.0.0+\] [\#GetDeliveryCacheStorageUpdateNotifier](#GetDeliveryCacheStorageUpdateNotifier "wikilink") |
| 20301 | \[8.0.0+\] [\#RequestSuspendDeliveryTask](#RequestSuspendDeliveryTask "wikilink")                       |
| 20400 | \[9.0.0+\] RegisterSystemApplicationDeliveryTask                                                        |
| 20401 | \[9.0.0+\] UnregisterSystemApplicationDeliveryTask                                                      |
| 30100 | SetPassphrase                                                                                           |
| 30101 | \[2.0.0-2.3.0\]                                                                                         |
| 30102 | \[2.0.0-2.3.0\]                                                                                         |
| 30200 | \[3.0.0+\] RegisterDeliveryTask                                                                         |
| 30201 | \[3.0.0+\] UnregisterDeliveryTask                                                                       |
| 30202 | \[3.0.0+\] BlockDeliveryTask                                                                            |
| 30203 | \[3.0.0+\] UnblockDeliveryTask                                                                          |
| 30300 | \[8.0.0+\] RegisterSystemApplicationDeliveryTasks                                                       |
| 90100 | GetDeliveryTaskList                                                                                     |
| 90200 | [\#GetDeliveryList](#GetDeliveryList "wikilink")                                                        |
| 90201 | \[3.0.0+\] ClearDeliveryCacheStorage                                                                    |
| 90202 | \[8.0.0+\] ClearDeliveryTaskSubscriptionStatus                                                          |
| 90300 | \[3.0.0+\] GetPushNotificationLog                                                                       |

### RequestSyncDeliveryCache

No input/output.

\[3.0.0+\] Now returns an
[\#IDeliveryCacheProgressService](#IDeliveryCacheProgressService "wikilink").

### RequestSyncDeliveryCacheWithApplicationId

Takes a total of 8-bytes of input, no output.

\[3.0.0+\] Now takes an additional 8-bytes of input, and returns an
[\#IDeliveryCacheProgressService](#IDeliveryCacheProgressService "wikilink").

### GetDeliveryCacheStorageUpdateNotifier

Takes a total of 8-bytes of input, returns an
[\#INotifierService](#INotifierService "wikilink").

### RequestSuspendDeliveryTask

Takes a total of 8-bytes of input, returns an
[\#IDeliveryTaskSuspensionService](#IDeliveryTaskSuspensionService "wikilink").

### GetDeliveryList

Takes a type-0x6 output buffer, returns a total of 4-bytes of output.

\[3.0.0+\] Now takes a total of 8-bytes of input, and returns an
additional 4-bytes of output.

### IDeliveryCacheProgressService

This is "nn::bcat::detail::ipc::IDeliveryCacheProgressService".

This was added with \[2.0.0+\].

| Cmd | Name     |
| --- | -------- |
| 0   | GetEvent |
| 1   | GetImpl  |

## IDeliveryCacheStorageService

This is "nn::bcat::detail::ipc::IDeliveryCacheStorageService".

This was added with \[2.0.0+\].

| Cmd | Name                            |
| --- | ------------------------------- |
| 0   | CreateFileService               |
| 1   | CreateDirectoryService          |
| 10  | EnumerateDeliveryCacheDirectory |

### IDeliveryCacheFileService

This is "nn::bcat::detail::ipc::IDeliveryCacheFileService".

This was added with \[2.0.0+\].

| Cmd | Name      |
| --- | --------- |
| 0   | Open      |
| 1   | Read      |
| 2   | GetSize   |
| 3   | GetDigest |

### IDeliveryCacheDirectoryService

This is "nn::bcat::detail::ipc::IDeliveryCacheDirectoryService".

This was added with \[2.0.0+\].

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

These are "nn::news::detail::ipc::IServiceCreator".

On \[1.0.0\] these are "nn::news::detail::ipc::INewsService", see
[\#INewsService](#INewsService "wikilink").

| Cmd | Name                          | Notes                                                                                    |
| --- | ----------------------------- | ---------------------------------------------------------------------------------------- |
| 0   | CreateNewsService             | No input, returns an [\#INewsService](#INewsService "wikilink").                         |
| 1   | CreateNewlyArrivedEventHolder | No input, returns an [\#INewlyArrivedEventHolder](#INewlyArrivedEventHolder "wikilink"). |
| 2   | CreateNewsDataService         | No input, returns an [\#INewsDataService](#INewsDataService "wikilink").                 |
| 3   | CreateNewsDatabaseService     | No input, returns an [\#INewsDatabaseService](#INewsDatabaseService "wikilink").         |
| 4   | CreateOverwriteEventHolder    | No input, returns an [\#IOverwriteEventHolder](#IOverwriteEventHolder "wikilink").       |

## INewsService

This is "nn::news::detail::ipc::INewsService".

| Cmd             | Name                                                                                                                                     |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| 10100           | PostLocalNews                                                                                                                            |
| 20100           | SetPassphrase                                                                                                                            |
| 30100           | GetSubscriptionStatus                                                                                                                    |
| 30101           | \[3.0.0+\] GetTopicList                                                                                                                  |
| 30110           | \[6.0.0+\]                                                                                                                               |
| 30200           | IsSystemUpdateRequired                                                                                                                   |
| 30201           | \[8.0.0+\]                                                                                                                               |
| 30300           | RequestImmediateReception                                                                                                                |
| 30400           | \[3.0.0+\] DecodeArchiveFile                                                                                                             |
| 30500           | \[8.0.0+\] ? (Takes a total of 8-bytes of input, a handle, and a type-0x9 input buffer, returns an [\#IUnknown2](#IUnknown2 "wikilink")) |
| \[1.0.0\] 30900 | (No input, returns an [\#INewlyArrivedEventHolder](#INewlyArrivedEventHolder "wikilink"))                                                |
| \[1.0.0\] 30901 | (No input, returns an [\#INewsDataService](#INewsDataService "wikilink"))                                                                |
| \[1.0.0\] 30902 | (No input, returns an [\#INewsDatabaseService](#INewsDatabaseService "wikilink"))                                                        |
| 40100           | SetSubscriptionStatus                                                                                                                    |
| 40101           | \[3.0.0+\] RequestAutoSubscription                                                                                                       |
| 40200           | ClearStorage                                                                                                                             |
| 40201           | ClearSubscriptionStatusAll                                                                                                               |
| 90100           | GetNewsDatabaseDump                                                                                                                      |

## INewlyArrivedEventHolder

This is "nn::news::detail::ipc::INewlyArrivedEventHolder".

| Cmd | Name |
| --- | ---- |
| 0   | Get  |

## INewsDataService

This is "nn::news::detail::ipc::INewsDataService".

| Cmd  | Name                          |
| ---- | ----------------------------- |
| 0    | Open                          |
| 1    | OpenWithNewsRecordV1          |
| 2    | Read                          |
| 3    | GetSize                       |
| 1001 | \[6.0.0+\] OpenWithNewsRecord |

## INewsDatabaseService

This is "nn::news::detail::ipc::INewsDatabaseService".

| Cmd  | Name                           |
| ---- | ------------------------------ |
| 0    | GetListV1                      |
| 1    | Count                          |
| 2    | CountWithKey                   |
| 3    | UpdateIntegerValue             |
| 4    | UpdateIntegerValueWithAddition |
| 5    | UpdateStringValue              |
| 1000 | \[6.0.0+\] GetList             |

## IOverwriteEventHolder

This is "nn::news::detail::ipc::IOverwriteEventHolder".

| Cmd | Name |
| --- | ---- |
| 0   | Get  |

## IUnknown2

This was added with \[8.0.0+\].

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |
| 3   |      |

# prepo:a, prepo:a2, prepo:m, prepo:u, prepo:s

These are "nn::prepo::detail::ipc::IPrepoService".

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
| 40100                 | \[2.0.0+\] IsUserAgreementCheckEnabled                          |
| 40101                 | \[2.0.0+\] SetUserAgreementCheckEnabled                         |
| 90100                 | \[6.0.0+\] ReadAllReportFiles (\[1.0.0-5.1.0\] GetStorageUsage) |
| \[1.0.0\] 90101       |                                                                 |
| \[1.0.0\] 90102       |                                                                 |
| \[5.0.0-5.1.0\] 90200 | GetStatistics                                                   |
| \[5.0.0-5.1.0\] 90201 | GetThroughputHistory                                            |
| \[5.0.0-5.1.0\] 90300 | GetLastUploadError                                              |

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

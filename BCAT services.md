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

| Cmd   | Name                                                                 |
| ----- | -------------------------------------------------------------------- |
| 10100 | RequestSyncDeliveryCache                                             |
| 10101 | \[5.0.0+\] RequestSyncDeliveryCacheWithDirectoryName                 |
| 10200 | \[5.0.0+\] CancelSyncDeliveryCacheRequest                            |
| 20100 | RequestSyncDeliveryCacheWithApplicationId                            |
| 20101 | \[5.0.0+\] RequestSyncDeliveryCacheWithApplicationIdAndDirectoryName |
| 30100 | SetPassphrase                                                        |
| 30200 | RegisterBackgroundDeliveryTask                                       |
| 30201 | UnregisterBackgroundDeliveryTask                                     |
| 30202 | BlockDeliveryTask                                                    |
| 30203 | UnblockDeliveryTask                                                  |
| 90100 | EnumerateBackgroundDeliveryTask                                      |
| 90200 | GetDeliveryList                                                      |
| 90201 | ClearDeliveryCacheStorage                                            |
| 90300 | GetPushNotificationLog                                               |

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

# news:a, news:c, news:m, news:p, news:v

These are "nn::<news::detail>::ipc::IServiceCreator".

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |
| 3   |      |
| 4   |      |

# prepo:a, prepo:m, prepo:u, prepo:s

These are "nn::prepo::detail::ipc::IPrepoService".

| Cmd   | Name                            |
| ----- | ------------------------------- |
| 10100 | SaveReport                      |
| 10101 | SaveReportWithUser              |
| 10200 | RequestImmediateTransmission    |
| 10300 | GetTransmissionStatus           |
| 20100 | SaveSystemReport                |
| 20200 | \[4.0.0+\] SetOperationMode     |
| 20101 | SaveSystemReportWithUser        |
| 30100 | ClearStorage                    |
| 40100 | IsUserAgreementCheckEnabled     |
| 40101 | SetUserAgreementCheckEnabled    |
| 90100 | GetStorageUsage                 |
| 90200 | \[5.0.0+\] GetStatistics        |
| 90201 | \[5.0.0+\] GetThroughputHistory |
| 90300 | \[5.0.0+\] GetLastUploadError   |

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

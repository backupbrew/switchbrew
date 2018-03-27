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

# news:a, news:c, news:m, news:p, news:v

These are "nn::news::detail::ipc::IServiceCreator".

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

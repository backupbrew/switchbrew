PCTL handles all parental controls management.

# pctl:s, pctl:r, pctl:a, pctl

These are "nn::pctl::detail::ipc::IParentalControlServiceFactory".

| Cmd | Name                                      |
| --- | ----------------------------------------- |
| 0   | CreateService                             |
| 1   | \[4.0.0+\] CreateServiceWithoutInitialize |

## IParentalControlService

This is "nn::pctl::detail::ipc::IParentalControlService".

| Cmd  | Name                                                                        |
| ---- | --------------------------------------------------------------------------- |
| 1    | \[4.0.0+\] Initialize                                                       |
| 1001 | CheckFreeCommunicationPermission                                            |
| 1002 | ConfirmLaunchApplicationPermission                                          |
| 1003 | ConfirmResumeApplicationPermission                                          |
| 1004 | ConfirmSnsPostPermission                                                    |
| 1005 | ConfirmSystemSettingsPermission                                             |
| 1006 | IsRestrictionTemporaryUnlocked                                              |
| 1007 | RevertRestrictionTemporaryUnlocked                                          |
| 1008 | EnterRestrictedSystemSettings                                               |
| 1009 | LeaveRestrictedSystemSettings                                               |
| 1010 | IsRestrictedSystemSettingsEntered                                           |
| 1011 | RevertRestrictedSystemSettingsEntered                                       |
| 1012 | GetRestrictedFeatures                                                       |
| 1013 | \[4.0.0+\] ConfirmStereoVisionPermission                                    |
| 1014 | \[5.0.0+\] ConfirmPlayableApplicationVideoOld                               |
| 1015 | \[5.0.0+\] ConfirmPlayableApplicationVideo                                  |
| 1016 | \[6.0.0+\] ConfirmShowNewsPermission                                        |
| 1031 | IsRestrictionEnabled                                                        |
| 1032 | GetSafetyLevel                                                              |
| 1033 | SetSafetyLevel                                                              |
| 1034 | GetSafetyLevelSettings                                                      |
| 1035 | GetCurrentSettings                                                          |
| 1036 | SetCustomSafetyLevelSettings                                                |
| 1037 | GetDefaultRatingOrganization                                                |
| 1038 | SetDefaultRatingOrganization                                                |
| 1039 | GetFreeCommunicationApplicationListCount                                    |
| 1042 | AddToFreeCommunicationApplicationList                                       |
| 1043 | DeleteSettings                                                              |
| 1044 | GetFreeCommunicationApplicationList                                         |
| 1045 | UpdateFreeCommunicationApplicationList                                      |
| 1046 | DisableFeaturesForReset                                                     |
| 1047 | \[3.0.0+\] NotifyApplicationDownloadStarted                                 |
| 1048 | \[6.0.0+\] NotifyNetworkProfileCreated                                      |
| 1061 | \[4.0.0+\] ConfirmStereoVisionRestrictionConfigurable                       |
| 1062 | \[4.0.0+\] GetStereoVisionRestriction                                       |
| 1063 | \[4.0.0+\] SetStereoVisionRestriction                                       |
| 1064 | \[5.0.0+\] ResetConfirmedStereoVisionPermission                             |
| 1065 | \[5.0.0+\] [\#IsStereoVisionPermitted](#IsStereoVisionPermitted "wikilink") |
| 1201 | UnlockRestrictionTemporarily                                                |
| 1202 | UnlockSystemSettingsRestriction                                             |
| 1203 | SetPinCode                                                                  |
| 1204 | [\#GenerateInquiryCode](#GenerateInquiryCode "wikilink")                    |
| 1205 | [\#CheckMasterKey](#CheckMasterKey "wikilink")                              |
| 1206 | GetPinCodeLength                                                            |
| 1207 | GetPinCodeChangedEvent                                                      |
| 1208 | \[4.0.0+\] GetPinCode                                                       |
| 1403 | IsPairingActive                                                             |
| 1406 | GetSettingsLastUpdated                                                      |
| 1411 | GetPairingAccountInfo                                                       |
| 1421 | GetAccountNickname                                                          |
| 1424 | GetAccountState                                                             |
| 1425 | \[6.0.0+\] RequestPostEvents                                                |
| 1432 | GetSynchronizationEvent                                                     |
| 1451 | StartPlayTimer                                                              |
| 1452 | StopPlayTimer                                                               |
| 1453 | IsPlayTimerEnabled                                                          |
| 1454 | GetPlayTimerRemainingTime                                                   |
| 1455 | IsRestrictedByPlayTimer                                                     |
| 1456 | GetPlayTimerSettings                                                        |
| 1457 | GetPlayTimerEventToRequestSuspension                                        |
| 1458 | \[4.0.0+\] IsPlayTimerAlarmDisabled                                         |
| 1471 | NotifyWrongPinCodeInputManyTimes                                            |
| 1472 | CancelNetworkRequest                                                        |
| 1473 | GetUnlinkedEvent                                                            |
| 1474 | ClearUnlinkedEvent                                                          |
| 1601 | DisableAllFeatures                                                          |
| 1602 | PostEnableAllFeatures                                                       |
| 1603 | IsAllFeaturesDisabled                                                       |
| 1901 | DeleteFromFreeCommunicationApplicationListForDebug                          |
| 1902 | ClearFreeCommunicationApplicationListForDebug                               |
| 1903 | \[5.0.0+\] GetExemptApplicationListCountForDebug                            |
| 1904 | \[5.0.0+\] GetExemptApplicationListForDebug                                 |
| 1905 | \[5.0.0+\] UpdateExemptApplicationListForDebug                              |
| 1906 | \[5.0.0+\] AddToExemptApplicationListForDebug                               |
| 1907 | \[5.0.0+\] DeleteFromExemptApplicationListForDebug                          |
| 1908 | \[5.0.0+\] ClearExemptApplicationListForDebug                               |
| 1941 | DeletePairing                                                               |
| 1951 | SetPlayTimerSettingsForDebug                                                |
| 1952 | GetPlayTimerSpentTimeForTest                                                |
| 1953 | \[4.0.0+\] SetPlayTimerAlarmDisabledForDebug                                |
| 2001 | RequestPairingAsync                                                         |
| 2002 | FinishRequestPairing                                                        |
| 2003 | AuthorizePairingAsync                                                       |
| 2004 | FinishAuthorizePairing                                                      |
| 2005 | RetrievePairingInfoAsync                                                    |
| 2006 | FinishRetrievePairingInfo                                                   |
| 2007 | UnlinkPairingAsync                                                          |
| 2008 | FinishUnlinkPairing                                                         |
| 2009 | GetAccountMiiImageAsync                                                     |
| 2010 | FinishGetAccountMiiImage                                                    |
| 2011 | GetAccountMiiImageContentTypeAsync                                          |
| 2012 | FinishGetAccountMiiImageContentType                                         |
| 2013 | SynchronizeParentalControlSettingsAsync                                     |
| 2014 | FinishSynchronizeParentalControlSettings                                    |
| 2015 | FinishSynchronizeParentalControlSettingsWithLastUpdated                     |
| 2016 | \[5.0.0+\] RequestUpdateExemptionListAsync                                  |

### IsStereoVisionPermitted

No input, returns an output u8 bool. True indicates that VrMode is
allowed, false otherwise.

## GenerateInquiryCode

This cmd takes no input, and produces 0x20 bytes of raw output
containing snprintf("%02d%08llu", 10, \[inquiry\_rnd\]) on \<=
[3.0.0](3.0.0.md "wikilink"). This changed on
[3.0.1](3.0.1.md "wikilink") to produce "11(...)" instead of "10(...)".

The random number generation relies on TinyMT.

## CheckMasterKey

This cmd takes the 0x20 bytes produced by GenerateInquiryCode, and an
0x20 byte X descriptor containing snprintf("%08llu", master\_key), and
returns a bool 00 if the master key is not valid, and 01 if it is.

Master Keys are validated as follows on \<=
[3.0.0](3.0.0.md "wikilink"): first, svcSleepThread(1000000000LL) is
called to introduce a delay to prevent brute force attacks. Then,
strlen(master\_key) is called -- if this is not 8, 0 is returned. Next,
the inquiry code is regenerated and snprintf("%02d%08llu", 10,
generated\_inquiry\_rnd) is compared to the inquiry data passed in as an
argument. If this doesn't match, 0 is returned. Then,
hmac-sha256(snprintf("%02d%08llu", 10, generated\_inquiry\_rnd)) is
called using hardcoded keydata, and the master key argument is compared
to snprintf("%08llu", (hmac\_result & 0xFFFFFFFFFFFF) % 100000000). If
this matches, 1 is returned, otherwise 0 is returned.

On [3.0.1](3.0.1.md "wikilink") this was changed to use different
hardcoded keydata, and to pass 11 as the snprintf argument instead of
10.

[Category:Services](Category:Services "wikilink")

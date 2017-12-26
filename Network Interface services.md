# nifm:a

This is
"nn::nifm::detail::IStaticService".

## IStaticService

| Cmd | Name                                                      | Notes                                                        |
| --- | --------------------------------------------------------- | ------------------------------------------------------------ |
| 4   | CreateGeneralService (\[3.0.0+\] CreateGeneralServiceOld) | Returns an [\#IGeneralService](#IGeneralService "wikilink"). |
| 5   | \[3.0.0+\] CreateGeneralService                           | Returns an [\#IGeneralService](#IGeneralService "wikilink"). |
|     |                                                           |                                                              |

### IGeneralService

| Cmd | Name                                                                      | Notes                                                        |
| --- | ------------------------------------------------------------------------- | ------------------------------------------------------------ |
| 1   | GetClientId                                                               |                                                              |
| 2   | CreateScanRequest                                                         | Returns an [\#IScanRequest](#IScanRequest "wikilink").       |
| 4   | CreateRequest                                                             | Returns an [\#IRequest](#IRequest "wikilink").               |
| 5   | GetCurrentNetworkProfile                                                  |                                                              |
| 6   | EnumerateNetworkInterfaces                                                |                                                              |
| 7   | EnumerateNetworkProfiles                                                  |                                                              |
| 8   | GetNetworkProfile                                                         |                                                              |
| 9   | SetNetworkProfile                                                         |                                                              |
| 10  | RemoveNetworkProfile                                                      |                                                              |
| 11  | \[1.0.0-3.0.2\] GetScanData \[4.0.0+\] GetScanDataOld                     |                                                              |
| 12  | GetCurrentIpAddress                                                       |                                                              |
| 13  | \[1.0.0-3.0.2\] GetCurrentAccessPoint \[4.0.0+\] GetCurrentAccessPointOld |                                                              |
| 14  | CreateTemporaryNetworkProfile                                             | Returns an [\#INetworkProfile](#INetworkProfile "wikilink"). |
| 15  | GetCurrentIpConfigInfo                                                    |                                                              |
| 16  | SetWirelessCommunicationEnabled                                           |                                                              |
| 17  | IsWirelessCommunicationEnabled                                            |                                                              |
| 18  | GetInternetConnectionStatus                                               |                                                              |
| 19  | SetEthernetCommunicationEnabled                                           |                                                              |
| 20  | IsEthernetCommunicationEnabled                                            |                                                              |
| 21  | IsAnyInternetRequestAccepted                                              |                                                              |
| 22  | IsAnyForegroundRequestAccepted                                            |                                                              |
| 23  | PutToSleep                                                                |                                                              |
| 24  | WakeUp                                                                    |                                                              |
| 25  | GetSsidListVersion                                                        |                                                              |
| 26  | SetExclusiveClient                                                        |                                                              |
| 27  | GetDefaultIpSetting                                                       |                                                              |
| 28  | SetDefaultIpSetting                                                       |                                                              |
| 29  | SetWirelessCommunicationEnabledForTest                                    |                                                              |
| 30  | SetEthernetCommunicationEnabledForTest                                    |                                                              |
| 31  | \[2.0.0+\] GetTelemetorySystemEventReadableHandle                         |                                                              |
| 32  | \[2.0.0+\] GetTelemetryInfo                                               |                                                              |
| 33  | \[2.0.0+\] ConfirmSystemAvailability                                      |                                                              |
| 34  | \[4.0.0+\] SetBackgroundRequestEnabled                                    |                                                              |
| 35  | \[4.0.0+\] GetScanData                                                    |                                                              |
| 36  | \[4.0.0+\] GetCurrentAccessPoint                                          |                                                              |
| 37  | \[4.0.0+\] Shutdown                                                       |                                                              |
|     |                                                                           |                                                              |

#### IScanRequest

| Cmd | Name                         |
| --- | ---------------------------- |
| 0   | Submit                       |
| 1   | IsProcessing                 |
| 2   | GetResult                    |
| 3   | GetSystemEventReadableHandle |
|     |                              |

#### IRequest

| Cmd | Name                            |
| --- | ------------------------------- |
| 0   | GetRequestState                 |
| 1   | GetResult                       |
| 2   | GetSystemEventReadableHandles   |
| 3   | Cancel                          |
| 4   | Submit                          |
| 5   | SetRequirement                  |
| 6   | SetRequirementPreset            |
| 8   | SetPriority                     |
| 9   | SetNetworkProfileId             |
| 10  | SetRejectable                   |
| 11  | SetConnectionConfirmationOption |
| 12  | SetPersistent                   |
| 13  | SetInstant                      |
| 14  | SetSustainable                  |
| 15  | SetRawPriority                  |
| 16  | SetGreedy                       |
| 17  | SetSharable                     |
| 18  | SetRequirementByRevision        |
| 19  | GetRequirement                  |
| 20  | GetRevision                     |
| 21  | GetAppletInfo                   |
| 22  | GetAdditionalInfo               |
| 23  | SetKeptInSleep                  |
| 24  | RegisterSocketDescriptor        |
| 25  | UnregisterSocketDescriptor      |
|     |                                 |

#### INetworkProfile

| Cmd | Name                            |
| --- | ------------------------------- |
| 0   | Update                          |
| 1   | Persist (\[3.0.0+\] PersistOld) |
| 2   | \[3.0.0+\] Persist              |
|     |                                 |

# nifm:s

Same as [nifm:a](#nifm:a "wikilink").

# nifm:u

Same as [nifm:a](#nifm:a "wikilink").

[Category:Services](Category:Services "wikilink")

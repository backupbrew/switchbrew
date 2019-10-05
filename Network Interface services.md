# nifm:a, nifm:s, nifm:u

These are "nn::nifm::detail::IStaticService".

Max sessions: nifm:a = 0x2, nifm:s = 0x10, nifm:u = 0x5.

nifm:u = User, nifm:s = System, and nifm:a =
Admin.

| Cmd | Name                                                                                                    | Notes |
| --- | ------------------------------------------------------------------------------------------------------- | ----- |
| 4   | [\#CreateGeneralServiceOld](#CreateGeneralServiceOld "wikilink") (\[1.0.0-2.3.0\] CreateGeneralService) |       |
| 5   | \[3.0.0+\] [\#CreateGeneralService](#CreateGeneralService "wikilink")                                   |       |

## CreateGeneralServiceOld

No input, returns an [\#IGeneralService](#IGeneralService "wikilink").

## CreateGeneralService

Takes a PID and an input u64 reserved\_pid, returns an
[\#IGeneralService](#IGeneralService "wikilink").

## IGeneralService

This is
"nn::nifm::detail::IGeneralService".

| Cmd | Name                                                             | Notes                                                        |
| --- | ---------------------------------------------------------------- | ------------------------------------------------------------ |
| 1   | GetClientId                                                      |                                                              |
| 2   | CreateScanRequest                                                | Returns an [\#IScanRequest](#IScanRequest "wikilink").       |
| 4   | CreateRequest                                                    | Returns an [\#IRequest](#IRequest "wikilink").               |
| 5   | GetCurrentNetworkProfile                                         |                                                              |
| 6   | EnumerateNetworkInterfaces                                       |                                                              |
| 7   | EnumerateNetworkProfiles                                         |                                                              |
| 8   | GetNetworkProfile                                                |                                                              |
| 9   | SetNetworkProfile                                                |                                                              |
| 10  | RemoveNetworkProfile                                             |                                                              |
| 11  | GetScanDataOld (\[1.0.0-3.0.2\] GetScanData)                     |                                                              |
| 12  | GetCurrentIpAddress                                              |                                                              |
| 13  | GetCurrentAccessPointOld (\[1.0.0-3.0.2\] GetCurrentAccessPoint) |                                                              |
| 14  | CreateTemporaryNetworkProfile                                    | Returns an [\#INetworkProfile](#INetworkProfile "wikilink"). |
| 15  | GetCurrentIpConfigInfo                                           |                                                              |
| 16  | SetWirelessCommunicationEnabled                                  |                                                              |
| 17  | IsWirelessCommunicationEnabled                                   |                                                              |
| 18  | GetInternetConnectionStatus                                      |                                                              |
| 19  | SetEthernetCommunicationEnabled                                  |                                                              |
| 20  | IsEthernetCommunicationEnabled                                   |                                                              |
| 21  | IsAnyInternetRequestAccepted                                     |                                                              |
| 22  | IsAnyForegroundRequestAccepted                                   |                                                              |
| 23  | PutToSleep                                                       |                                                              |
| 24  | WakeUp                                                           |                                                              |
| 25  | GetSsidListVersion                                               |                                                              |
| 26  | SetExclusiveClient                                               |                                                              |
| 27  | GetDefaultIpSetting                                              |                                                              |
| 28  | SetDefaultIpSetting                                              |                                                              |
| 29  | SetWirelessCommunicationEnabledForTest                           |                                                              |
| 30  | SetEthernetCommunicationEnabledForTest                           |                                                              |
| 31  | \[2.0.0+\] GetTelemetorySystemEventReadableHandle                |                                                              |
| 32  | \[2.0.0+\] GetTelemetryInfo                                      |                                                              |
| 33  | \[2.0.0+\] ConfirmSystemAvailability                             |                                                              |
| 34  | \[4.0.0+\] SetBackgroundRequestEnabled                           |                                                              |
| 35  | \[4.0.0+\] GetScanData                                           |                                                              |
| 36  | \[4.0.0+\] GetCurrentAccessPoint                                 |                                                              |
| 37  | \[4.0.0+\] Shutdown                                              |                                                              |
| 38  | \[6.0.0+\] GetAllowedChannels                                    |                                                              |
| 39  | \[8.0.0+\] NotifyApplicationSuspended                            |                                                              |
| 40  | \[8.0.0+\] SetAcceptableNetworkTypeFlag                          |                                                              |
| 41  | \[8.0.0+\] GetAcceptableNetworkTypeFlag                          |                                                              |
| 42  | \[8.0.0+\] NotifyConnectionStateChanged                          |                                                              |
| 43  | \[9.0.0+\] SetWowlDelayedWakeTime                                |                                                              |

### IScanRequest

This is "nn::nifm::detail::IScanRequest".

| Cmd | Name                         |
| --- | ---------------------------- |
| 0   | Submit                       |
| 1   | IsProcessing                 |
| 2   | GetResult                    |
| 3   | GetSystemEventReadableHandle |
| 4   | \[6.0.0+\] SetChannels       |

### IRequest

This is "nn::nifm::detail::IRequest". This represents an application or
sysmodule's request to bring a network
up.

| Cmd | Name                                                                             |
| --- | -------------------------------------------------------------------------------- |
| 0   | [\#GetRequestState](#GetRequestState "wikilink")                                 |
| 1   | [\#GetResult](#GetResult "wikilink")                                             |
| 2   | [\#GetSystemEventReadableHandles](#GetSystemEventReadableHandles "wikilink")     |
| 3   | [\#Cancel](#Cancel "wikilink")                                                   |
| 4   | [\#Submit](#Submit "wikilink")                                                   |
| 5   | [\#SetRequirement](#SetRequirement "wikilink")                                   |
| 6   | SetRequirementPreset                                                             |
| 8   | SetPriority                                                                      |
| 9   | SetNetworkProfileId                                                              |
| 10  | SetRejectable                                                                    |
| 11  | [\#SetConnectionConfirmationOption](#SetConnectionConfirmationOption "wikilink") |
| 12  | [\#SetPersistent](#SetPersistent "wikilink")                                     |
| 13  | SetInstant                                                                       |
| 14  | SetSustainable                                                                   |
| 15  | SetRawPriority                                                                   |
| 16  | SetGreedy                                                                        |
| 17  | SetSharable                                                                      |
| 18  | SetRequirementByRevision                                                         |
| 19  | [\#GetRequirement](#GetRequirement "wikilink")                                   |
| 20  | GetRevision                                                                      |
| 21  | GetAppletInfo                                                                    |
| 22  | GetAdditionalInfo                                                                |
| 23  | \[3.0.0+\] SetKeptInSleep                                                        |
| 24  | \[3.0.0+\] RegisterSocketDescriptor                                              |
| 25  | \[3.0.0+\] UnregisterSocketDescriptor                                            |

#### GetRequestState

| Number | Description                     |
| ------ | ------------------------------- |
| 1      | Not yet submitted or error      |
| 2      | Pending (sdk calls this OnHold) |
| 3      | Connected                       |

#### GetResult

If the request enters state 1, this command can be used to determine
why. It responds with the nice networking error codes that there are
support pages for.

#### GetSystemEventReadableHandles

Returns two event handles. The first one signals when the RequestState
changes.

#### Cancel

Cancels the request to bring the network up.

#### Submit

Submits the request to bring the network up. Call this after configuring
the request.

#### SetRequirement

Takes a total of 0x20-bytes of input, no output.

\[3.0.0+\] Takes an additional 4-bytes of input.

#### SetConnectionConfirmationOption

Set how to verify the internet connection.

| Option | Description                                      |
| ------ | ------------------------------------------------ |
| 0      |                                                  |
| 1      |                                                  |
| 2      | "Local" network (does not check for working DNS) |
| 3      |                                                  |
| 4      | Default                                          |
| 5      |                                                  |
|        |                                                  |

#### SetPersistent

If this is set, when the network connection is lost, rather than causing
the request to enter state 1, it will instead enter state 2 and attempt
to bring the network back up again.

#### GetRequirement

No input, returns a total of 0x20-bytes of output.

\[3.0.0+\] Returns an additional 4-bytes of output.

### INetworkProfile

This is "nn::nifm::detail::INetworkProfile".

| Cmd | Name                                 |
| --- | ------------------------------------ |
| 0   | Update                               |
| 1   | PersistOld (\[1.0.0-2.3.0\] Persist) |
| 2   | \[3.0.0+\] Persist                   |

[Category:Services](Category:Services "wikilink")

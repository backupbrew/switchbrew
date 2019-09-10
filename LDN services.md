LDN handles all local network communication.

# ldn:m

This is "nn::ldn::detail::IMonitorServiceCreator".

| Cmd | Name                                                       |
| --- | ---------------------------------------------------------- |
| 0   | [\#CreateMonitorService](#CreateMonitorService "wikilink") |

## CreateMonitorService

Returns an [\#IMonitorService](#IMonitorService "wikilink").

## IMonitorService

This is "nn::ldn::detail::IMonitorService".

| Cmd | Name                           |
| --- | ------------------------------ |
| 0   | GetStateForMonitor             |
| 1   | GetNetworkInfoForMonitor       |
| 2   | GetIpv4AddressForMonitor       |
| 3   | GetDisconnectReasonForMonitor  |
| 4   | GetSecurityParameterForMonitor |
| 5   | GetNetworkConfigForMonitor     |
| 100 | InitializeMonitor              |
| 101 | FinalizeMonitor                |

# ldn:s

This is "nn::ldn::detail::ISystemServiceCreator".

| Cmd | Name                                                                                         |
| --- | -------------------------------------------------------------------------------------------- |
| 0   | [\#CreateSystemLocalCommunicationService](#CreateSystemLocalCommunicationService "wikilink") |

## CreateSystemLocalCommunicationService

Returns an
[\#ISystemLocalCommunicationService](#ISystemLocalCommunicationService "wikilink").

## ISystemLocalCommunicationService

This is "nn::ldn::detail::ISystemLocalCommunicationService".

| Cmd | Name                                        |
| --- | ------------------------------------------- |
| 0   | GetState                                    |
| 1   | GetNetworkInfo                              |
| 2   | GetIpv4Address                              |
| 3   | GetDisconnectReason                         |
| 4   | GetSecurityParameter                        |
| 5   | GetNetworkConfig                            |
| 100 | AttachStateChangeEvent                      |
| 101 | GetNetworkInfoLatestUpdate                  |
| 102 | Scan                                        |
| 103 | ScanPrivate                                 |
| 104 | \[5.0.0+\] SetWirelessControllerRestriction |
| 200 | OpenAccessPoint                             |
| 201 | CloseAccessPoint                            |
| 202 | CreateNetwork                               |
| 203 | CreateNetworkPrivate                        |
| 204 | DestroyNetwork                              |
| 205 | Reject                                      |
| 206 | SetAdvertiseData                            |
| 207 | SetStationAcceptPolicy                      |
| 208 | AddAcceptFilterEntry                        |
| 209 | ClearAcceptFilter                           |
| 300 | OpenStation                                 |
| 301 | CloseStation                                |
| 302 | Connect                                     |
| 303 | ConnectPrivate                              |
| 304 | Disconnect                                  |
| 400 | InitializeSystem                            |
| 401 | FinalizeSystem                              |
| 402 | \[4.0.0+\] SetOperationMode                 |
| 403 | \[7.0.0+\] InitializeSystem2                |

# ldn:u

This is "nn::ldn::detail::IUserServiceCreator".

| Cmd | Name                                                                                     |
| --- | ---------------------------------------------------------------------------------------- |
| 0   | [\#CreateUserLocalCommunicationService](#CreateUserLocalCommunicationService "wikilink") |

## CreateUserLocalCommunicationService

Returns an
[\#IUserLocalCommunicationService](#IUserLocalCommunicationService "wikilink").

## IUserLocalCommunicationService

This is "nn::ldn::detail::IUserLocalCommunicationService".

| Cmd | Name                                        |
| --- | ------------------------------------------- |
| 0   | GetState                                    |
| 1   | GetNetworkInfo                              |
| 2   | GetIpv4Address                              |
| 3   | GetDisconnectReason                         |
| 4   | GetSecurityParameter                        |
| 5   | GetNetworkConfig                            |
| 100 | AttachStateChangeEvent                      |
| 101 | GetNetworkInfoLatestUpdate                  |
| 102 | Scan                                        |
| 103 | ScanPrivate                                 |
| 104 | \[5.0.0+\] SetWirelessControllerRestriction |
| 200 | OpenAccessPoint                             |
| 201 | CloseAccessPoint                            |
| 202 | CreateNetwork                               |
| 203 | CreateNetworkPrivate                        |
| 204 | DestroyNetwork                              |
| 205 | Reject                                      |
| 206 | SetAdvertiseData                            |
| 207 | SetStationAcceptPolicy                      |
| 208 | AddAcceptFilterEntry                        |
| 209 | ClearAcceptFilter                           |
| 300 | OpenStation                                 |
| 301 | CloseStation                                |
| 302 | Connect                                     |
| 303 | ConnectPrivate                              |
| 304 | Disconnect                                  |
| 400 | Initialize                                  |
| 401 | Finalize                                    |
| 402 | \[7.0.0+\] Initialize2                      |

# lp2p:app, lp2p:sys

These are "nn::lp2p::detail::IServiceCreator".

These were added with \[9.0.0+\].

| Cmd | Name                        |
| --- | --------------------------- |
| 0   | CreateNetworkService        |
| 8   | CreateNetworkServiceMonitor |

## INetworkService

This is "nn::lp2p::detail::INetworkService".

| Cmd  | Name |
| ---- | ---- |
| 0    |      |
| 256  |      |
| 264  |      |
| 272  |      |
| 280  |      |
| 288  |      |
| 296  |      |
| 304  |      |
| 312  |      |
| 320  |      |
| 512  |      |
| 768  |      |
| 776  |      |
| 784  |      |
| 1536 |      |
| 1544 |      |
| 1552 |      |

## INetworkServiceMonitor

This is "nn::lp2p::detail::INetworkServiceMonitor".

| Cmd  | Name |
| ---- | ---- |
| 0    |      |
| 256  |      |
| 264  |      |
| 272  |      |
| 280  |      |
| 288  |      |
| 296  |      |
| 304  |      |
| 312  |      |
| 320  |      |
| 512  |      |
| 768  |      |
| 776  |      |
| 784  |      |
| 1536 |      |
| 1544 |      |
| 1552 |      |

[Category:Services](Category:Services "wikilink")

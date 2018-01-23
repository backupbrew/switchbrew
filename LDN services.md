LDN handles all local network communication.

# ldn:m

This is
"nn::ldn::detail::IMonitorServiceCreator".

| Cmd | Name              | Notes                                                        |
| --- | ----------------- | ------------------------------------------------------------ |
| 0   | GetMonitorService | Returns an [\#IMonitorService](#IMonitorService "wikilink"). |
|     |                   |                                                              |

## IMonitorService

This is "nn::ldn::detail::IMonitorService".

| Cmd | Name          |
| --- | ------------- |
| 0   | GetNifmStatus |
| 1   |               |
| 2   |               |
| 3   |               |
| 4   |               |
| 5   |               |
| 100 | StartMonitor  |
| 101 | StopMonitor   |
|     |               |

# ldn:s

This is
"nn::ldn::detail::ISystemServiceCreator".

| Cmd | Name                               | Notes                                                                                          |
| --- | ---------------------------------- | ---------------------------------------------------------------------------------------------- |
| 0   | GetSystemLocalCommunicationService | Returns an [\#ISystemLocalCommunicationService](#ISystemLocalCommunicationService "wikilink"). |
|     |                                    |                                                                                                |

## ISystemLocalCommunicationService

This is "nn::ldn::detail::ISystemLocalCommunicationService".

| Cmd | Name             |
| --- | ---------------- |
| 0   |                  |
| 1   | GetNetworkInfo   |
| 2   |                  |
| 3   |                  |
| 4   |                  |
| 5   |                  |
| 100 | GetUnkWaitEvent  |
| 101 |                  |
| 102 |                  |
| 103 |                  |
| 200 | OpenAccessPoint  |
| 201 | CloseAccessPoint |
| 202 |                  |
| 203 |                  |
| 204 | DestroyNetwork   |
| 205 |                  |
| 206 |                  |
| 207 |                  |
| 208 |                  |
| 209 |                  |
| 300 | OpenStation      |
| 301 | CloseStation     |
| 302 |                  |
| 303 |                  |
| 304 | Disconnect       |
| 400 | InitializeSystem |
| 401 | TerminateSystem  |
|     |                  |

# ldn:u

This is
"nn::ldn::detail::IUserServiceCreator".

| Cmd | Name                             | Notes                                                                                      |
| --- | -------------------------------- | ------------------------------------------------------------------------------------------ |
| 0   | GetUserLocalCommunicationService | Returns an [\#IUserLocalCommunicationService](#IUserLocalCommunicationService "wikilink"). |
|     |                                  |                                                                                            |

## IUserLocalCommunicationService

This is "nn::ldn::detail::IUserLocalCommunicationService".

Same as
[\#ISystemLocalCommunicationService](#ISystemLocalCommunicationService "wikilink").

[Category:Services](Category:Services "wikilink")

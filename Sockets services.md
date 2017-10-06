# bsd:u / bsd:s

| Cmd | Name                        |
| --- | --------------------------- |
| 0   | RegisterClient (Initialize) |
| 1   | StartMonitoring             |
| 2   | Socket                      |
| 3   | SocketExempt                |
| 4   | Open                        |
| 5   | Select                      |
| 6   | Poll                        |
| 7   | Sysctl                      |
| 8   | Recv                        |
| 9   | RecvFrom                    |
| 10  | Send                        |
| 11  | SendTo                      |
| 12  | Accept                      |
| 13  | Bind                        |
| 14  | Connect                     |
| 15  | GetPeerName                 |
| 16  | GetSockName                 |
| 17  | GetSockOpt                  |
| 18  | Listen                      |
| 19  | Ioctl                       |
| 20  | Fcntl                       |
| 21  | SetSockOpt                  |
| 22  | Shutdown                    |
| 23  | ShutdownAllSockets          |
| 24  | Write                       |
| 25  | Read                        |
| 26  | Close                       |
| 27  | DuplicateSocket             |
| 28  | GetResourceStatistics       |
| 29  | \[3.0.0+\] RecvMMsg         |
| 30  | \[3.0.0+\] SendMMsg         |

# sfdnsres

| Cmd | Name                   |
| --- | ---------------------- |
| 0   | SetDnsAddressesPrivate |
| 1   | GetDnsAddressPrivate   |
| 2   | GetHostByName          |
| 3   | GetHostByAddr          |
| 4   | GetHostStringError     |
| 5   | GetGaiStringError      |
| 6   | GetAddrInfo            |
| 7   | GetNameInfo            |
| 8   | RequestCancelHandle    |
| 9   | CancelSocketCall       |

# nsd:u / nsd:a

| Cmd | Name                      |
| --- | ------------------------- |
| 10  | GetSettingName            |
| 11  | GetEnvironmentIdentifier  |
| 12  | GetDeviceId               |
| 13  | DeleteSettings            |
| 14  | ImportSettings            |
| 20  | Resolve                   |
| 21  | ResolveEx                 |
| 30  | GetNasServiceSetting      |
| 31  | GetNasServiceSettingEx    |
| 40  | GetNasRequestFqdn         |
| 41  | GetNasRequestFqdnEx       |
| 42  | GetNasApiFqdn             |
| 43  | GetNasApiFqdnEx           |
| 50  | GetCurrentSetting         |
| 60  | ReadSaveDataFromFsForTest |
| 61  | WriteSaveDataToFsForTest  |
| 62  | DeleteSaveDataOfFsForTest |

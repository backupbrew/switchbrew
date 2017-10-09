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

| Cmd | Name                                     |
| --- | ---------------------------------------- |
| 0   | SetDnsAddressesPrivate                   |
| 1   | GetDnsAddressPrivate                     |
| 2   | GetHostByName                            |
| 3   | GetHostByAddr                            |
| 4   | GetHostStringError                       |
| 5   | GetGaiStringError                        |
| 6   | [\#GetAddrInfo](#GetAddrInfo "wikilink") |
| 7   | GetNameInfo                              |
| 8   | RequestCancelHandle                      |
| 9   | CancelSocketCall                         |

### GetAddrInfo

Takes three type 5 buffers (host, port, and hints), and a type 6 buffer
(the output addrinfos). Also takes a u8 (padded to 4 bytes so the next
raw parameter can align), a u32, and a u64. The u8 is a boolean for
whether to enable "nsd resolve" (1) or not (0). Not sure what the u32
is. It seems to either come from a parameter to `GetAddrInfo` or be
zero. The u64 is most likely a placeholder for the server to copy the
PID into and should be zero. Both hints and the output buffer contain
serialized addrinfo chains. The hints buffer is sized 0x400 bytes long
by default, and the output buffer 0x1000 bytes.

### Addrinfo Serialization Format

Each struct addrinfo in the linked list is serialized according to this
format and then written to the buffer. All numbers are in network byte
order.

| Size (bytes)                  | Name          | Notes                              |
| ----------------------------- | ------------- | ---------------------------------- |
| 4                             | Magic         | Needs to be 0xBEEFCAFE. Seriously. |
| 4                             | ai\_flags     |                                    |
| 4                             | ai\_family    |                                    |
| 4                             | ai\_socktype  |                                    |
| 4                             | ai\_protocol  |                                    |
| 4                             | ai\_addrlen   |                                    |
| ai\_addrlen ? ai\_addrlen : 4 | ai\_addr      |                                    |
| null-terminated string        | ai\_canonname |                                    |

If `ai_addrlen` is zero, `ai_addr` will occupy 4 bytes.

| Size (bytes) | Name     | Notes |
| ------------ | -------- | ----- |
| 4            | ai\_addr |       |

If `ai_family` is recognized as AF\_INET6 (28) or AF\_INET (2),
`ai_addr` is read as `struct sockaddr_in` or `struct sockaddr_in6`.
Otherwise, it's just read as `u8[ai_addrlen]`.

The list should be terminated with a sentinel four-byte zero value.

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

TMA (Target Manager) acts as a debugging sysmodule for development kits.
This system module is loaded in retail units, but remains unused.

These services are inaccessible on retail units. However, all [System
Applets](Title%20list#System%20Applets.md##System_Applets "wikilink")
have permission to access them (see
[NPDM\#Service\_Access\_Control](NPDM#Service%20Access%20Control.md##Service_Access_Control "wikilink")).

# htc

This is "nn::tma::IHtcManager".

| Cmd | Name                                |
| --- | ----------------------------------- |
| 0   | GetEnvironmentVariable              |
| 1   | GetEnvironmentVariableLength        |
| 2   | BindHostConnectionEvent             |
| 3   | BindHostDisconnectionEvent          |
| 4   | BindHostConnectionEventForSystem    |
| 5   | BindHostDisconnectionEventForSystem |

# htcs

This is "nn::tma::IHtcsManager".

| Cmd | Name               |
| --- | ------------------ |
| 0   |                    |
| 1   |                    |
| 2   |                    |
| 3   |                    |
| 4   |                    |
| 5   |                    |
| 6   |                    |
| 7   |                    |
| 8   |                    |
| 9   |                    |
| 10  | GetPeerNameAny     |
| 11  | GetDefaultHostName |
| 12  | CreateSocketOld    |
| 13  | CreateSocket       |
| 100 | RegisterProcessId  |
| 101 | MonitorManager     |

## ISocket

This is "nn::tma::ISocket".

| Cmd | Name     |
| --- | -------- |
| 0   | Close    |
| 1   | Connect  |
| 2   | Bind     |
| 3   | Listen   |
| 4   | Accept   |
| 5   | Recv     |
| 6   | Send     |
| 7   | Shutdown |
| 8   | Fcntl    |

# htc:tenv

This is "nn::htc::tenv::IServiceManager".

| Cmd | Name                |
| --- | ------------------- |
| 0   | GetServiceInterface |

## IService

This is "nn::htc::tenv::IService".

| Cmd | Name                       |
| --- | -------------------------- |
| 0   | GetVariable                |
| 1   | GetVariableLength          |
| 2   | WaitUntilVariableAvailable |

[Category:Services](Category:Services "wikilink")

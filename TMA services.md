TMA (Target Manager Agent) acts as a debugging sysmodule for development
kits. This system module is loaded in retail units, but remains unused.

These services are inaccessible on retail units. However, all [System
Applets](Title%20list#System%20Applets.md##System_Applets "wikilink")
have permission to access them (see
[NPDM\#Service\_Access\_Control](NPDM#Service%20Access%20Control.md##Service_Access_Control "wikilink")).

TMA makes a few sets of services available. One set (the "htc" family),
is aimed around managing Host/Target Connections. "htc" allows
orchestrating the switch\<-\>pc connection, "htc:tenv" allows retrieving
information about the target's environment from the host, and "htcs"
provides an interface for managing sockets on PC from the Switch. htcs
is used primarily to host services on PC ports with actual management
code running on Switch. The other service ("file\_io") manages HostIO, a
mechanism by which the Switch can read files present on the Host PC.
When a host is connected, FS will attempt to read data via file\_io when
@Host:/ content paths are used, or when fsp-srv-\>OpenHostFileSystem()
is used to open an IFileSystem to the Host PC. Nintendo's implementation
only supports Windows, and FS will explicitly check for the presence of
a "C:/" drive to detect this.

# htc

This is "nn::tma::IHtcManager".

| Cmd | Name                                   |
| --- | -------------------------------------- |
| 0   | GetEnvironmentVariable                 |
| 1   | GetEnvironmentVariableLength           |
| 2   | BindHostConnectionEvent                |
| 3   | BindHostDisconnectionEvent             |
| 4   | BindHostConnectionEventForSystem       |
| 5   | BindHostDisconnectionEventForSystem    |
| 6   | \[3.0.0+\] GetBridgeIpAddress          |
| 7   | \[3.0.0+\] GetBridgePort               |
| 8   | \[3.0.0+\] SetCradleAttached           |
| 9   | \[4.0.0+\] GetBridgeSubnetMask         |
| 10  | \[4.0.0+\] GetBridgeMacAddress         |
| 11  | \[6.0.0+\] GetWorkingDirectoryPath     |
| 12  | \[6.0.0+\] GetWorkingDirectoryPathSize |
| 13  | \[6.0.0+\] RunOnHostStart              |
| 14  | \[9.0.0+\] RunOnHostResults            |

# htcs

This is "nn::tma::IHtcsManager".

| Cmd | Name               |
| --- | ------------------ |
| 0   | Socket             |
| 1   | Close              |
| 2   | Connect            |
| 3   | Bind               |
| 4   | Listen             |
| 5   | Accept             |
| 6   | Recv               |
| 7   | Send               |
| 8   | Shutdown           |
| 9   | Fcntl              |
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

# file\_io

This is "nn::tma::IFileManager".

This service is not normally present on retail units.

| Cmd | Name                                               | Notes                                                             |
| --- | -------------------------------------------------- | ----------------------------------------------------------------- |
| 0   | [\#OpenFile](#OpenFile "wikilink")                 | returns an [\#IFileAccessor](#IFileAccessor "wikilink")           |
| 1   | [\#FileExists](#FileExists "wikilink")             |                                                                   |
| 2   | [\#DeleteFile](#DeleteFile "wikilink")             |                                                                   |
| 3   | [\#RenameFile](#RenameFile "wikilink")             |                                                                   |
| 4   | [\#GetIOType](#GetIOType "wikilink")               |                                                                   |
| 5   | [\#OpenDirectory](#OpenDirectory "wikilink")       | returns an [\#IDirectoryAccessor](#IDirectoryAccessor "wikilink") |
| 6   | [\#DirectoryExists](#DirectoryExists "wikilink")   |                                                                   |
| 7   | [\#CreateDirectory](#CreateDirectory "wikilink")   |                                                                   |
| 8   | [\#DeleteDirectory](#DeleteDirectory "wikilink")   |                                                                   |
| 9   | [\#RenameDirectory](#RenameDirectory "wikilink")   |                                                                   |
| 10  | [\#CreateFile](#CreateFile "wikilink")             |                                                                   |
| 11  | [\#GetFileTimeStamp](#GetFileTimeStamp "wikilink") |                                                                   |
| 12  | GetCaseSensitivePath                               |                                                                   |

### OpenFile

Takes in an input X descriptor "Path" and a u32 "OpenMode", returns a
[\#IFileAccessor](#IFileAccessor "wikilink") interface.

### FileExists

Takes in an input X descriptor "Path", and returns an output bool.

### DeleteFile

Takes in an input X descriptor "Path".

### RenameFile

Takes in an input X descriptor "SrcPath" and an input X descriptor
"DstPath".

### GetIOType

Takes in an input X descriptor "Path", returns an output int
"EntryType".

### OpenDirectory

Takes in an input X descriptor "Path" and a u32 "OpenMode", returns a
[\#IDirectoryAccessor](#IDirectoryAccessor "wikilink") interface.

### DirectoryExists

Takes in an input X descriptor "Path", and returns an output bool.

### CreateDirectory

Takes in an input X descriptor "Path".

### DeleteDirectory

Takes in an input X descriptor "Path" and an input bool "IsRecursive".

### RenameDirectory

Takes in an input X descriptor "SrcPath" and an input X descriptor
"DstPath".

### CreateFile

Takes in an input X descriptor "Path" and an input s64 "Size".

### GetFileTimeStamp

Takes in an input X descriptor "Path", and returns 3 output u64s
("CreatedTime", "AccessedTime", "ModifiedTime").

## IFileAccessor

This is "nn::tma::IFileAccessor".

| Cmd | Name               |
| --- | ------------------ |
| 0   | ReadFile           |
| 1   | WriteFile          |
| 2   | GetFileSize        |
| 3   | SetFileSize        |
| 4   | FlushFile          |
| 5   | SetPriorityForFile |
| 6   | GetPriorityForFile |

### ReadFile

Takes in an input s64 "Offset", an input ReadOption, and a NonSecure B
descriptor "OutBuffer", and returns a s64 "BytesRead".

### WriteFile

Takes in an input s64 "Offset", an input WriteOption, and a NonSecure A
descriptor "InBuffer".

### GetFileSize

Takes no input, and returns a s64 "FileSize".

### SetFileSize

Takes an s64 "FileSize".

### FlushFile

Takes no input, returns no output.

### SetPriorityForFile

Takes an input s32 "Priority".

### GetPriorityForFile

Takes no input, returns an s32 "Priority".

## IDirectoryAccessor

This is "nn::tma::IDirectoryAccessor".

| Cmd | Name                                                             |
| --- | ---------------------------------------------------------------- |
| 0   | [\#GetEntryCount](#GetEntryCount "wikilink")                     |
| 1   | [\#ReadDirectory](#ReadDirectory "wikilink")                     |
| 2   | [\#SetPriorityForDirectory](#SetPriorityForDirectory "wikilink") |
| 3   | [\#GetPriorityForDirectory](#GetPriorityForDirectory "wikilink") |

### GetEntryCount

Takes no input, returns an s64 "EntryCount".

### ReadDirectory

Takes an input B descriptor "OutEntryBuffer", returns an s64
"NumEntriesRead"

### SetPriorityForDirectory

Takes an input s32 "Priority".

### GetPriorityForDirectory

Takes no input, returns an s32 "Priority".

[Category:Services](Category:Services "wikilink")

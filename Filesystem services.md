# fsp-srv

| Cmd  | Name                                                                                   |
| ---- | -------------------------------------------------------------------------------------- |
| 1    | [\#Initialize](#Initialize "wikilink")                                                 |
| 2    | MountRomFs                                                                             |
| 7    | Returns an [\#IFileSystem](#IFileSystem "wikilink").                                   |
| 8    | MountContent                                                                           |
| 11   | Returns an [\#IFileSystem](#IFileSystem "wikilink").                                   |
| 12   | OpenBisPartition                                                                       |
| 13   |                                                                                        |
| 17   | OpenHostFileSystemImpl                                                                 |
| 18   | MountSdCard                                                                            |
| 19   | FormatSdCard                                                                           |
| 21   | DeleteSaveData                                                                         |
| 22   |                                                                                        |
| 23   | CreateSystemSaveData                                                                   |
| 24   | RegisterSaveDataAtomicDeletion                                                         |
| 25   |                                                                                        |
| 26   | FormatSdCardDryRun                                                                     |
| 27   |                                                                                        |
| 30   | OpenGameCardStorage?                                                                   |
| 31   | MountGameCardPartition                                                                 |
| 51   | Returns an [\#IFileSystem](#IFileSystem "wikilink").                                   |
| 52   | MountSystemSaveData                                                                    |
| 53   | Returns an [\#IFileSystem](#IFileSystem "wikilink").                                   |
| 58   | ReadSaveDataFileSystemExtraData                                                        |
| 59   |                                                                                        |
| 60   | Returns an [\#ISaveDataInfoReader](#ISaveDataInfoReader "wikilink").                   |
| 61   | OpenSaveDataIterator                                                                   |
| 80   | OpenFileDirectly?                                                                      |
| 100  | MountImageDirectory                                                                    |
| 110  | Returns an [\#IFileSystem](#IFileSystem "wikilink").                                   |
| 200  | OpenRomFsStorage                                                                       |
| 202  | OpenDataStorageByDataId                                                                |
| 203  | Returns an [\#IStorage](#IStorage "wikilink").                                         |
| 400  | [\#OpenDeviceOperator](#OpenDeviceOperator "wikilink")                                 |
| 500  | [\#OpenSdCardDetectionEventNotifier](#OpenSdCardDetectionEventNotifier "wikilink")     |
| 501  | [\#OpenGameCardDetectionEventNotifier](#OpenGameCardDetectionEventNotifier "wikilink") |
| 600  |                                                                                        |
| 601  |                                                                                        |
| 602  |                                                                                        |
| 603  |                                                                                        |
| 604  |                                                                                        |
| 605  |                                                                                        |
| 606  |                                                                                        |
| 607  | RegisterExternalKey                                                                    |
| 608  | UnregisterExternalKey                                                                  |
| 609  |                                                                                        |
| 620  |                                                                                        |
| 800  |                                                                                        |
| 1000 |                                                                                        |
| 1001 |                                                                                        |
| 1002 |                                                                                        |
| 1003 | DisableAutoSaveDataCreation                                                            |
| 1004 |                                                                                        |
| 1005 | GetGlobalAccessLogMode                                                                 |
| 1006 | OutputAccessLogToSdCard                                                                |

## Initialize

| Word | Value              |
| ---- | ------------------ |
| 0    | 0x00000004         |
| 1    | 0x8000000E         |
| 2    | 0x00000001         |
| 0-1  | Pid                |
| 0    | Always. 0x18000001 |
| 1    | Always. 0          |
| 2    | "SCFI"             |
| 3    | 0x00000001         |
| 4    | Always 0.          |

## OpenDeviceOperator

This command returns a session to a port implementing the
[\#IDeviceOperator](#IDeviceOperator "wikilink") interface.

## OpenSdCardDetectionEventNotifier

This command returns a session to a port implementing the
[\#IEventNotifier](#IEventNotifier "wikilink") interface.

## OpenGameCardDetectionEventNotifier

This command returns a session to a port implementing the
[\#IEventNotifier](#IEventNotifier "wikilink") interface.

# IStorage

This is the interface for a raw device, usually a block device.

| Cmd | Name   |
| --- | ------ |
| 0   | Read   |
| 1   | Write? |
| 2   |        |
| 3   |        |
| 4   |        |

# IFileSystem

There are two main implementations of this interface:

  - **RomFS**: Filesystem implementation statically linked in the
    binary. Uses an [\#IStorage](#IStorage "wikilink") interface as
    underlying raw device.
  - **IPC proxy**: Used for all non-RomFS filesystems. In this case,
    actual filesystem implementation is in the FS process.

| Cmd | Name                       |
| --- | -------------------------- |
| 0   | CreateFile                 |
| 1   | DeleteFile                 |
| 2   | CreateDirectory            |
| 3   | DeleteDirectory?           |
| 4   | DeleteDirectoryRecursively |
| 5   | RenameFile                 |
| 6   | MoveDirectory?             |
| 7   | GetEntryType               |
| 8   | OpenFile                   |
| 9   | OpenDirectory              |
| 10  | CommitSaveData             |
| 11  |                            |
| 12  |                            |

# IDirectory

| Cmd | Name               |
| --- | ------------------ |
| 0   | ReadEntries        |
| 1   | GetNumberOfEntries |

# IFile

| Cmd | Name  |
| --- | ----- |
| 0   | Read  |
| 1   | Write |
| 2   | Flush |
| 3   |       |
| 4   |       |

# ISaveDataInfoReader

# IDeviceOperator

| Cmd | Name                           |
| --- | ------------------------------ |
| 0   | IsSdCardInserted               |
| 1   |                                |
| 2   | GetSdCardCid                   |
| 3   |                                |
| 4   |                                |
| 5   |                                |
| 6   |                                |
| 101 |                                |
| 110 |                                |
| 111 |                                |
| 112 |                                |
| 113 |                                |
| 114 |                                |
| 200 | IsGameCardInserted             |
| 201 |                                |
| 202 | GetGameCardHandle              |
| 203 | GetGameCardUpdatePartitionInfo |
| 204 |                                |
| 205 | GetGameCardAttribute           |
| 206 | GetGameCardDeviceCertificate   |
| 207 |                                |
| 208 |                                |
| 209 |                                |
| 210 |                                |
| 211 |                                |
| 212 |                                |
| 213 |                                |
| 214 |                                |
| 215 |                                |
| 216 |                                |
| 300 |                                |
| 301 |                                |

# IEventNotifier

| Cmd | Name      |
| --- | --------- |
| 0   | BindEvent |

# StorageId

| Value | Name       |
| ----- | ---------- |
| 0     | None       |
| 1     | Host       |
| 2     | GameCard   |
| 3     | NandSystem |
| 4     | NandUser   |
| 5     | SdCard     |

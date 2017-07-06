# fsp-ldr

| Cmd | Name          |
| --- | ------------- |
| 0   | MountCode     |
| 1   | IsCodeMounted |

# fsp-pr

| Cmd | Name               |
| --- | ------------------ |
| 0   | SetFsPermissions   |
| 1   | ClearFsPermissions |

# fsp-srv

| Cmd  | Name                                                                                   |
| ---- | -------------------------------------------------------------------------------------- |
| 0    | MountApplicationPackage                                                                |
| 1    | [\#Initialize](#Initialize "wikilink")                                                 |
| 2    | MountRomFs                                                                             |
| 7    | [\#MountContent7](#MountContent7 "wikilink")                                           |
| 8    | [\#MountContent](#MountContent "wikilink")                                             |
| 11   | [\#MountBis](#MountBis "wikilink")                                                     |
| 12   | [\#OpenBisPartition](#OpenBisPartition "wikilink")                                     |
| 13   | InvalidateBisCache                                                                     |
| 17   | OpenHostFileSystemImpl                                                                 |
| 18   | MountSdCard                                                                            |
| 19   | FormatSdCard                                                                           |
| 21   | DeleteSaveData                                                                         |
| 22   | [\#CreateSaveData](#CreateSaveData "wikilink")                                         |
| 23   | [\#CreateSystemSaveData](#CreateSystemSaveData "wikilink")                             |
| 24   | RegisterSaveDataAtomicDeletion                                                         |
| 25   |                                                                                        |
| 26   | FormatSdCardDryRun                                                                     |
| 27   |                                                                                        |
| 30   | OpenGameCardPartition                                                                  |
| 31   | MountGameCardPartition                                                                 |
| 51   | [\#MountSavedata](#MountSavedata "wikilink")                                           |
| 52   | [\#MountSystemSaveData](#MountSystemSaveData "wikilink")                               |
| 53   | Returns an [\#IFileSystem](#IFileSystem "wikilink").                                   |
| 58   | ReadSaveDataFileSystemExtraData                                                        |
| 59   |                                                                                        |
| 60   | OpenSaveDataInfoReader                                                                 |
| 61   | OpenSaveDataIterator                                                                   |
| 80   | OpenSaveDataThumbnailFile                                                              |
| 100  | MountImageDirectory                                                                    |
| 110  | [\#MountContentStorage](#MountContentStorage "wikilink")                               |
| 200  | OpenHost                                                                               |
| 202  | OpenDataStorageByDataId                                                                |
| 203  | Returns an [\#IStorage](#IStorage "wikilink").                                         |
| 400  | [\#OpenDeviceOperator](#OpenDeviceOperator "wikilink")                                 |
| 500  | [\#OpenSdCardDetectionEventNotifier](#OpenSdCardDetectionEventNotifier "wikilink")     |
| 501  | [\#OpenGameCardDetectionEventNotifier](#OpenGameCardDetectionEventNotifier "wikilink") |
| 600  | SetCurrentPosixTime                                                                    |
| 601  | QuerySaveDataTotalSize                                                                 |
| 602  | VerifySaveData                                                                         |
| 603  | CorruptSaveDataForDebug                                                                |
| 604  | CreatePaddingFile                                                                      |
| 605  | DeleteAllPaddingFiles                                                                  |
| 606  |                                                                                        |
| 607  | RegisterExternalKey                                                                    |
| 608  | UnregisterExternalKey                                                                  |
| 609  |                                                                                        |
| 620  |                                                                                        |
| 800  |                                                                                        |
| 1000 | SetBisRootForHost                                                                      |
| 1001 |                                                                                        |
| 1002 | SetSaveDataRootPath                                                                    |
| 1003 | DisableAutoSaveDataCreation                                                            |
| 1004 | SetGlobalAccessLogMode                                                                 |
| 1005 | GetGlobalAccessLogMode                                                                 |
| 1006 | OutputAccessLogToSdCard                                                                |

## MountApplicationPackage

Presumably about the same as MountContent except this uses the titleID
associated with the FS session?

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

## MountContent7

Takes an input u32 ([NCA](NCA.md "wikilink")-type) and an u64 title-id.
Web-applet loads the u32 from u32\_table\[inparam\]. Only type4 is
usable with this?

Returns an [\#IFileSystem](#IFileSystem "wikilink").

Note: web-applet strings refer to both this cmd and the below
"MountContent" as "MountContent".

## MountContent

Takes a type-0x19 input buffer, an in32, and an input title-id.

The in32 must be 5 if the NCA type is 0 (control).

The input buffer is the output string path from nsam
[GetContentNcaPath](NS%20Services#GetContentNcaPath.md##GetContentNcaPath "wikilink").

Returns an [\#IFileSystem](#IFileSystem "wikilink").

May return errors when attempting to access NCA-paths for an
update-title with a gamecard, when the gamecard isn't inserted. May
return error 0x7D402 in some cases with update-titles. Non-val2 in32
values with NCA-type1 are unusable, even for normal titles.

## MountBis

Takes a type-0x19 input buffer string and a u32 Bis partitionID(see
below). Official user-process code sets instr\[0\] = 0 normally.

Returns an [\#IFileSystem](#IFileSystem "wikilink").

Only partitionIDs for FAT partitions are usable with this, otherwise
error 0x2EE202 is returned. Seems to be about the same as
[\#OpenBisPartition](#OpenBisPartition "wikilink") except this mounts
the partition filesystem instead of allowing direct access to the
partition sectors.

## OpenBisPartition

Takes a u32 partition ID, returns 0x2EE202 for partitions which do not
exist, 0x320002 for partitions which cannot be opened and a valid
[\#IStorage](#IStorage "wikilink") handle otherwise.

## CreateSaveData

Takes a 0x40-byte Save-struct entry, a 0x40-byte SaveCreate-struct
entry, and a 0x10-byte input struct.

Only the first 0x5-bytes in the 0x10-byte struct are initialized:
all-zero when automatically creating savedata during savecommon mount by
official user-processes. In the dedicated save-creation code in official
user-processes: +0 u32 = 0x40060, +4 u8 = 1.

Creates regular savedata.

## CreateSystemSaveData

Takes a 0x40-byte Save-struct entry and a 0x40-byte SaveCreate-struct
entry.

Creates savedata in the SYSTEM [NAND](Flash%20Filesystem.md "wikilink")
partition.

## MountSaveData

Takes an input u8 and a 0x40-byte Save-struct entry. Official
user-process code is only known to use value 1 for the u8.

Returns an [\#IFileSystem](#IFileSystem "wikilink").

## MountSystemSaveData

Takes an input u8 and a 0x40-byte Save-struct entry. Web-applet only
uses value0 for the input u8.

Returns an [\#IFileSystem](#IFileSystem "wikilink").

Mounts savedata in the SYSTEM [NAND](Flash%20Filesystem.md "wikilink")
partition.

## MountContentStorage

Takes a [\#ContentStorageId](#ContentStorageId "wikilink"). Invalid
values return 0x2EE202.

Returns an [\#IFileSystem](#IFileSystem "wikilink") with NCA files. The
read data from these files is identical to the data read by
[Content\_Manager\_services\#ReadEntryRaw](Content%20Manager%20services#ReadEntryRaw.md##ReadEntryRaw "wikilink").

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

| Cmd | Name    | Arguments                                      |
| --- | ------- | ---------------------------------------------- |
| 0   | Read    | Takes a type-0x46 buffer, an offset and length |
| 1   | Write   |                                                |
| 2   | Flush   |                                                |
| 3   | SetSize |                                                |
| 4   | GetSize | None                                           |

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
| 3   | DeleteDirectory            |
| 4   | DeleteDirectoryRecursively |
| 5   | RenameFile                 |
| 6   | RenameDirectory            |
| 7   | GetEntryType               |
| 8   | OpenFile                   |
| 9   | OpenDirectory              |
| 10  | Commit                     |
| 11  | GetFreeSpaceSize           |
| 12  | GetTotalSpaceSize          |

# IDirectory

| Cmd | Name          |
| --- | ------------- |
| 0   | Read          |
| 1   | GetEntryCount |

# IFile

| Cmd | Name    |
| --- | ------- |
| 0   | Read    |
| 1   | Write   |
| 2   | Flush   |
| 3   | SetSize |
| 4   | GetSize |

# ISaveDataInfoReader

# IDeviceOperator

| Cmd | Name                                                                           |
| --- | ------------------------------------------------------------------------------ |
| 0   | IsSdCardInserted                                                               |
| 1   | GetSdCardSpeedMode                                                             |
| 2   | GetSdCardCid                                                                   |
| 3   |                                                                                |
| 4   |                                                                                |
| 5   |                                                                                |
| 6   |                                                                                |
| 100 | GetMmcCid                                                                      |
| 101 | GetMmcSpeedMode                                                                |
| 110 | EraseMmc                                                                       |
| 111 | GetMmcPartitionSize                                                            |
| 112 |                                                                                |
| 113 |                                                                                |
| 114 |                                                                                |
| 200 | IsGameCardInserted                                                             |
| 201 | EraseGameCard                                                                  |
| 202 | GetGameCardHandle                                                              |
| 203 | [\#GetGameCardUpdatePartitionInfo](#GetGameCardUpdatePartitionInfo "wikilink") |
| 204 | FinalizeGameCardDriver                                                         |
| 205 | GetGameCardAttribute                                                           |
| 206 | GetGameCardDeviceCertificate                                                   |
| 207 | GetGameCardAsicInfo                                                            |
| 208 | GetGameCardIdSet                                                               |
| 209 | WriteToGameCard                                                                |
| 210 | SetVerifyWriteEnalbleFlag                                                      |
| 211 | GetGameCardImageHash                                                           |
| 212 |                                                                                |
| 213 |                                                                                |
| 214 |                                                                                |
| 215 |                                                                                |
| 216 |                                                                                |
| 300 | SetSpeedEmulationMode                                                          |
| 301 | GetSpeedEmulationMode                                                          |

## GetGameCardUpdatePartitionInfo

Returns a titleID and the title-version for it.

  - Output u32 with ARMS-gamecard: title-version v131162. This is the
    title-version for [2.1.0](2.1.0.md "wikilink"), which is the
    sysupdate included with this gamecard. Launch-day gamecards return
    title-version v450.
  - Output u64 with ARMS-gamecard: titleID 0100000000000816.

[NS](NS%20Services.md "wikilink") appears to only use this with
[Content\_Manager\_services\#GetTitleIdInfo](Content%20Manager%20services#GetTitleIdInfo.md##GetTitleIdInfo "wikilink")
and
[Content\_Manager\_services\#GetUpdateTitleList](Content%20Manager%20services#GetUpdateTitleList.md##GetUpdateTitleList "wikilink")
with storageid=nandsys, for checking whether a sysupdate is required.

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

# ContentStorageId

| Value | Name       |
| ----- | ---------- |
| 0     | NandSystem |
| 1     | NandUser   |
| 2     | SdCard     |

# BisPartitionID

  - 0: Raw NAND sectors access for MMC
    [boot](Flash%20Filesystem.md "wikilink") partition 0.
  - 10: Raw NAND sectors access for MMC
    [boot](Flash%20Filesystem.md "wikilink") partition 1.
  - Rest: see
[here](Flash%20Filesystem.md "wikilink").

# Save Struct

| Offset | Size | Description                                                                                                                                                                                             |
| ------ | ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x8  | 0 for SystemSaveData. SaveData: 0 can be used for accessing the savedata associated with the current FS session titleID, otherwise when set this is the titleID associated with the savedata to access. |
| 0x8    | 0x10 | userID for user-specific savedata(saveuser) when set, otherwise when zero this indicates the common savedata(savecommon).                                                                               |
| 0x18   | 0x8  | u64 [saveID](Flash%20Filesystem.md "wikilink"). 0 for SaveData.                                                                                                                                         |
| 0x20   | 0x8  | 0 for SystemSaveData. 1 for SaveData.                                                                                                                                                                   |
| 0x28   | 0x8  | 0 for SystemSaveData/SaveData.                                                                                                                                                                          |
| 0x30   | 0x8  | 0 for SystemSaveData/SaveData.                                                                                                                                                                          |
| 0x38   | 0x8  | 0 for SystemSaveData/SaveData.                                                                                                                                                                          |

Total size is
0x40-bytes.

# SaveCreate Struct

| Offset | Size | Description                                                                                                                                                                                  |
| ------ | ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x8  | [IVFC](Savegames.md "wikilink") level4 size?                                                                                                                                                 |
| 0x8    | 0x8  | Same as offset 0x0 normally?                                                                                                                                                                 |
| 0x10   | 0x8  | 0x4000 for SystemSaveData/SaveData. [IVFC](Savegames.md "wikilink") level4 block-size in bytes?                                                                                              |
| 0x18   | 0x8  | Official user-processes only uses 0 here for SystemSaveData/SaveData. For the dedicated save-creation code with SaveData, this value comes from an input param with official user-processes. |
| 0x20   | 0x4  | ?                                                                                                                                                                                            |
| 0x24   | 0x1  | Official user-processes only uses 0 here for SystemSaveData, 1 for SaveData.                                                                                                                 |
| 0x25   | 0x1  | 0 for SystemSaveData/SaveData.                                                                                                                                                               |
| 0x26   | 0x1A | Not initialized for SystemSaveData/SaveData.                                                                                                                                                 |

Total size is 0x40-bytes.

[Category:Services](Category:Services "wikilink")

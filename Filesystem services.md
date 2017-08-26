# fsp-ldr

| Cmd | Name          | Arguments                                                       | Notes                                                |
| --- | ------------- | --------------------------------------------------------------- | ---------------------------------------------------- |
| 0   | MountCode     | u64 TID + X descriptor [\#ContentPath](#ContentPath "wikilink") | Returns an [\#IFileSystem](#IFileSystem "wikilink"). |
| 1   | IsCodeMounted | u64 PID                                                         | Returns a bool (1 if code is mounted).               |

# fsp-pr

| Cmd | Name                          | Arguments                                                                                                                                                           | Notes                                                                                                                              |
| --- | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| 0   | SetFsPermissions              | u8 storageID, u32 PID, u64 TID, ACI0\_buf\_size, ACID\_buf\_size + two A descriptors (the 0x1C FS-access control from ACI0 + the 0x2C FS-access control from ACID). | Actual FS permissions are set to (ACI0\_perms & ACID\_perms). Will panic(svcBreak) when buffer sizes from ipc-rawdata are invalid. |
| 1   | ClearFsPermissions            | u32 PID to clear                                                                                                                                                    |                                                                                                                                    |
| 256 | SetEnabledProgramVerification | bool enabled                                                                                                                                                        |                                                                                                                                    |

## SetEnabledProgramVerification

Seems to sets a global flag to inputval & 1.

When the flag is zero, it will set ret=0 instead of ret={error} when
verifying a RSA signature fails. This RSA signature seems to be the
signature in the [NPDM](NPDM.md "wikilink") ACID. It then skips
verifying what seems to be the second signature in the [NCA
header](NCA%20Format.md "wikilink"). Note that if verifying the NPDM(?)
signature is successful, and verifying that second signature fails, it
will throw an error and
abort.

# fsp-srv

| Cmd  | Name                                                                                   | Required permissions-type and func |
| ---- | -------------------------------------------------------------------------------------- | ---------------------------------- |
| 0    | MountApplicationPackage (FS-module v2.x cmdhandler only supports cmds \>=1)            |                                    |
| 1    | [\#Initialize](#Initialize "wikilink")                                                 |                                    |
| 2    | MountRomFs                                                                             |                                    |
| 7    | [\#MountContent7](#MountContent7 "wikilink")                                           |                                    |
| 8    | [\#MountContent](#MountContent "wikilink")                                             |                                    |
| 11   | [\#MountBis](#MountBis "wikilink")                                                     |                                    |
| 12   | [\#OpenBisPartition](#OpenBisPartition "wikilink")                                     |                                    |
| 13   | InvalidateBisCache                                                                     |                                    |
| 17   | OpenHostFileSystemImpl                                                                 |                                    |
| 18   | MountSdCard                                                                            |                                    |
| 19   | FormatSdCard                                                                           |                                    |
| 21   | [\#DeleteSaveData](#DeleteSaveData "wikilink")                                         |                                    |
| 22   | [\#CreateSaveData](#CreateSaveData "wikilink")                                         |                                    |
| 23   | [\#CreateSystemSaveData](#CreateSystemSaveData "wikilink")                             |                                    |
| 24   | RegisterSaveDataAtomicDeletion                                                         |                                    |
| 25   |                                                                                        |                                    |
| 26   | FormatSdCardDryRun                                                                     |                                    |
| 27   |                                                                                        |                                    |
| 30   | [\#OpenGameCardPartition](#OpenGameCardPartition "wikilink")                           |                                    |
| 31   | [\#MountGameCardPartition](#MountGameCardPartition "wikilink")                         |                                    |
| 51   | [\#MountSaveData](#MountSaveData "wikilink")                                           |                                    |
| 52   | [\#MountSystemSaveData](#MountSystemSaveData "wikilink")                               |                                    |
| 53   | Returns an [\#IFileSystem](#IFileSystem "wikilink").                                   |                                    |
| 58   | ReadSaveDataFileSystemExtraData                                                        |                                    |
| 59   | WriteSaveDataFileSystemExtraData                                                       |                                    |
| 60   | OpenSaveDataInfoReader                                                                 |                                    |
| 61   | OpenSaveDataIterator                                                                   |                                    |
| 80   | OpenSaveDataThumbnailFile                                                              |                                    |
| 100  | MountImageDirectory                                                                    |                                    |
| 110  | [\#MountContentStorage](#MountContentStorage "wikilink")                               |                                    |
| 200  | OpenHost                                                                               |                                    |
| 202  | [\#OpenDataStorageByDataId](#OpenDataStorageByDataId "wikilink")                       |                                    |
| 203  | Returns an [\#IStorage](#IStorage "wikilink").                                         |                                    |
| 400  | [\#OpenDeviceOperator](#OpenDeviceOperator "wikilink")                                 |                                    |
| 500  | [\#OpenSdCardDetectionEventNotifier](#OpenSdCardDetectionEventNotifier "wikilink")     |                                    |
| 501  | [\#OpenGameCardDetectionEventNotifier](#OpenGameCardDetectionEventNotifier "wikilink") |                                    |
| 600  | SetCurrentPosixTime                                                                    |                                    |
| 601  | QuerySaveDataTotalSize                                                                 |                                    |
| 602  | [\#VerifySaveData](#VerifySaveData "wikilink")                                         |                                    |
| 603  | CorruptSaveDataForDebug                                                                |                                    |
| 604  | CreatePaddingFile                                                                      |                                    |
| 605  | DeleteAllPaddingFiles                                                                  |                                    |
| 606  | GetRightsId                                                                            |                                    |
| 607  | RegisterExternalKey                                                                    |                                    |
| 608  | UnregisterExternalKey                                                                  |                                    |
| 609  |                                                                                        |                                    |
| 620  | SetSdCardEncryptionSeed                                                                |                                    |
| 800  | GetAndClearFileSystemProxyErrorInfo                                                    |                                    |
| 1000 | SetBisRootForHost                                                                      |                                    |
| 1001 | SetSaveDataSize                                                                        |                                    |
| 1002 | SetSaveDataRootPath                                                                    |                                    |
| 1003 | DisableAutoSaveDataCreation                                                            |                                    |
| 1004 | [\#SetGlobalAccessLogMode](#SetGlobalAccessLogMode "wikilink")                         | 0x10, 1                            |
| 1005 | [\#GetGlobalAccessLogMode](#GetGlobalAccessLogMode "wikilink")                         | None                               |
| 1006 | [\#OutputAccessLogToSdCard](#OutputAccessLogToSdCard "wikilink")                       | None                               |

## Permissions

Each time permissions are checked, the [process-obj](#fsp-pr "wikilink")
is loaded using the session PID, then a func is called with the
permissions-type. The func retval is checked, then the permissions
[error](Error%20codes.md "wikilink") is thrown if needed.

Internally in that process-obj load func, it will load the obj as normal
when the PID is \>6, otherwise it will use a fixed obj. If not done
already, that fixed obj will be initialized using fixed input data, via
the same code used internally by [\#fsp-pr](#fsp-pr "wikilink").

In general this func uses the input permissions-type to determine what
mask value to use. That value is masked with the
[permissions](NPDM.md "wikilink") from the above process-obj. When the
result is 0, 0 is returned, otherwise non-zero is returned. The default
non-zero retval is basically 0x3.

Panic is triggered when the input type is \>{max value} /
invalid.

Func0:

| Type(s)                            | Mask               | Non-zero retval | Notes                                                                                                                           |
| ---------------------------------- | ------------------ | --------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| 0xA 0xD 0x16 0x1F 0x20 0x21 0x22   | 0x8000000000000080 | Default         |                                                                                                                                 |
| 0x15 0x17 0x18 0x19 0x1A 0x1B 0x1C | 0x8000000000010080 | Default         |                                                                                                                                 |
| 0x0 0x1 0x2 0x3 0x4 0x5            | 0x8000000000000801 | 0x1             |                                                                                                                                 |
| 0x9 0x1D 0x1E                      | 0x8000000000000084 | Default         |                                                                                                                                 |
| 0xB 0xC                            | 0x8000000000008080 | Default         |                                                                                                                                 |
| 0xE 0x23                           | 0xC000000000200000 | Default         |                                                                                                                                 |
| 0x12 0x13                          | 0x8000000000000020 | Default         |                                                                                                                                 |
| 0x6                                |                    |                 | In this case it appears the func returns retval & 0xff, where retval = {bit0=0, bit1..bit63=obj\_permissions starting at bit0}? |
| 0x7                                | 0x8000000000000800 | Default         |                                                                                                                                 |
| 0x8                                | 0x8000000000001000 | Default         |                                                                                                                                 |
| 0xF                                | 0x8000000000000010 | Default         |                                                                                                                                 |
| 0x10                               | 0x8000000000040020 | Default         |                                                                                                                                 |
| 0x11                               | 0x8000000000000028 | Default         |                                                                                                                                 |
| 0x14                               | 0x8000000000010082 | Default         |                                                                                                                                 |
| 0x24                               | 0x8000000000000100 | Default         |                                                                                                                                 |
| 0x25                               | 0x8000000000100008 | 0x1             |                                                                                                                                 |
| 0x26                               | 0xC000000000400000 | Default         |                                                                                                                                 |

Func1(non-zero retval is always 0x1):

| Type(s)   | Mask               | Notes   |
| --------- | ------------------ | ------- |
| 0x0 0x1   | 0x8000000000000080 |         |
| 0x2 0x3   | 0x8000000000000010 |         |
| 0x4 0x5   | 0x8000000000000200 |         |
| 0x7 0xB   | 0x8000000000000060 |         |
| 0xC 0x1A  | 0x8000000000004020 |         |
| 0x10 0x11 | 0x8000000000080000 |         |
| 0x6       | 0x8000000000002020 |         |
| 0x8       | 0x8000000000000028 |         |
| 0x9       | 0x8000000000000020 |         |
| 0xA       | 0x8000000000004028 |         |
| 0xD       | 0x8000000000020000 |         |
| 0xE       | 0x8000000000000400 |         |
| 0xF       | 0x8000000000004060 |         |
| 0x13      | 0xC000000000800000 |         |
| 0x14      | 0xC000000001000000 |         |
| 0x15      | 0xC000000002000000 |         |
| 0x16      | 0x8000000004000000 |         |
| 0x17      | 0x8000000008000000 |         |
| 0x18      | 0x8000000010000000 |         |
| 0x19      | 0x8000000000000800 |         |
| 0x12      |                    | Invalid |

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

## DeleteSaveData

Takes an input u64.

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

## OpenGameCardPartition

Takes an input u32 (partition ID), and returns an
[\#IStorage](#IStorage "wikilink") for the
[partition](Gamecard%20Format.md "wikilink").

## MountGameCardPartition

Takes two input u32s, with the second u32 located at +4 in rawdata after
the first u32.

Returns an [\#IFileSystem](#IFileSystem "wikilink").

Mounts a gamecard [partition](Gamecard%20Partition.md "wikilink").

## MountSaveData

Takes an input u8 and a 0x40-byte Save-struct entry. Official
user-process code is only known to use value 1 for the u8.

Returns an [\#IFileSystem](#IFileSystem "wikilink").

Permissions aren't checked until the specified save is successfully
found.

Only one process can mount a given savedata at any given time (this
includes systemsavedata).

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

## OpenDataStorageByDataId

Takes a [\#StorageId](#StorageId "wikilink") and a TitleID.

Returns a [domain object
ID](IPC%20Marshalling#Domain%20message.md##Domain_message "wikilink")
implementing the [\#IStorage](#IStorage "wikilink") interface for data
archives.

## OpenDeviceOperator

This command returns a session to a port implementing the
[\#IDeviceOperator](#IDeviceOperator "wikilink") interface.

## OpenSdCardDetectionEventNotifier

This command returns a session to a port implementing the
[\#IEventNotifier](#IEventNotifier "wikilink") interface.

## OpenGameCardDetectionEventNotifier

This command returns a session to a port implementing the
[\#IEventNotifier](#IEventNotifier "wikilink") interface.

## VerifySaveData

Takes an unknown input u64 and a type-0x6 output buffer.

The input u64 high-byte must be non-zero, otherwise an
[error](Error%20codes.md "wikilink") is returned(0xE02).

## SetGlobalAccessLogMode

Takes an input u32.

## GetGlobalAccessLogMode

Returns an output u32.

GlobalAccessLogMode is normally 0.

## OutputAccessLogToSdCard

Takes a type-0x5 input buffer.

The input buffer is the string to output to the log. User-processes
normally include a newline at the end.

User-processes only use this when the value previously loaded from
[\#GetGlobalAccessLogMode](#GetGlobalAccessLogMode "wikilink") has bit1
set.

GetGlobalAccessLogMode and OutputAccessLogToSdCard are usable without
special permissions, however SetGlobalAccessLogMode requires that. When
bit1 in GlobalAccessLogMode is clear, FS-module will just return 0 for
OutputAccessLogToSdCard. However even with that set the log doesn't show
up SD, unknown why.

The input buffer is written to the "$FsAccessLog:/FsAccessLog.txt" file,
where "$FsAccessLog" is the SD-card mount-name. It's written to the
current end of the file(appended).

# IStorage

This is the interface for a raw device, usually a block device.

| Cmd | Name    | Arguments                                      |
| --- | ------- | ---------------------------------------------- |
| 0   | Read    | Takes a type-0x46 buffer, an offset and length |
| 1   | Write   | Takes a type-0x45 buffer, an offset and length |
| 2   | Flush   | None                                           |
| 3   | SetSize | Takes a size                                   |
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

## Commit

Like [3DS](https://3dbrew.org/wiki/FS:ControlArchive), this has to be
used after writing to savedata for the changes to take affect.

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
| 3   | GetSdCardUserAreaSize                                                          |
| 4   | GetSdCardProtectedAreaSize                                                     |
| 5   | GetAndClearSdCardErrorInfo                                                     |
| 6   |                                                                                |
| 100 | GetMmcCid                                                                      |
| 101 | GetMmcSpeedMode                                                                |
| 110 | EraseMmc                                                                       |
| 111 | GetMmcPartitionSize                                                            |
| 112 | GetMmcPatrolCount                                                              |
| 113 | GetAndClearMmcErrorInfo                                                        |
| 114 | GetMmcExtendedCsd                                                              |
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
| 212 | GetGameCardErrorInfo                                                           |
| 213 |                                                                                |
| 214 | GetGameCardCid                                                                 |
| 215 |                                                                                |
| 216 |                                                                                |
| 217 | \[2.1.0+\] Returns 0x40-bytes of output data.                                  |
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

# ContentPath

These are the 0x300 paths to NCA files for the various filesystems FS
can access, beginning with @. They're passed via X descriptors, and
returned via various
[ncm/lr](Location%20Resolver%20services.md "wikilink") commands.

| Path           | Notes                                   |
| -------------- | --------------------------------------- |
| @GcApp         | Gamecard App partition (Partition 2)    |
| @GcS00000001   | Gamecard Contents.                      |
| @SdCardContent | Installed SD card contents              |
| @Sdcard        | Raw SD card partition                   |
| @SystemContent | NandSystem partition.                   |
| @upp           | Gamecard update partition (Partition 0) |
| @UserContent   | NandUser partition.                     |

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
| 0x8    | 0x10 | userID for user-specific savedata(saveuser) when set, otherwise when zero this indicates the common savedata(savecommon). This is loaded from [Account\_services](Account%20services.md "wikilink").    |
| 0x18   | 0x8  | u64 [saveID](Flash%20Filesystem.md "wikilink"). 0 for SaveData.                                                                                                                                         |
| 0x20   | 0x8  | ContentStorageId? 0 for SystemSaveData. 1 for SaveData. 2 for DeviceSaveData(with official user-processes all other fields are 0 for DeviceSaveData).                                                   |
| 0x28   | 0x8  | 0 for SystemSaveData/SaveData.                                                                                                                                                                          |
| 0x30   | 0x8  | 0 for SystemSaveData/SaveData.                                                                                                                                                                          |
| 0x38   | 0x8  | 0 for SystemSaveData/SaveData.                                                                                                                                                                          |

Total size is
0x40-bytes.

# SaveCreate Struct

| Offset | Size | Description                                                                                                                                                                                                                                                                                                       |
| ------ | ---- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x8  | [IVFC](Savegames.md "wikilink") level4 size?                                                                                                                                                                                                                                                                      |
| 0x8    | 0x8  | Same as offset 0x0 normally? Hard-coded to 0x80000 for BcatSaveData.                                                                                                                                                                                                                                              |
| 0x10   | 0x8  | 0x4000 for SystemSaveData/SaveData/DeviceSaveData/BcatSaveData. [IVFC](Savegames.md "wikilink") level4 block-size in bytes?                                                                                                                                                                                       |
| 0x18   | 0x8  | Official user-processes only uses 0 here for SystemSaveData/SaveData. For the dedicated save-creation code with SaveData/DeviceSaveData, this value comes from an input param with official user-processes. For BcatSaveData, this is the hard-coded [titleID](Title%20list.md "wikilink") of the bcat-sysmodule. |
| 0x20   | 0x4  | Written using an input param for official user-processes. Hard-coded 0 for BcatSaveData.                                                                                                                                                                                                                          |
| 0x24   | 0x1  | Official user-processes only uses 0 here for SystemSaveData, 1 for SaveData/DeviceSaveData/BcatSaveData.                                                                                                                                                                                                          |
| 0x25   | 0x1  | 0 for SystemSaveData/SaveData.                                                                                                                                                                                                                                                                                    |
| 0x26   | 0x1A | Not initialized for SystemSaveData/SaveData.                                                                                                                                                                                                                                                                      |

Total size is 0x40-bytes.

# DeviceSaveData

This is accessed using the same commands for SaveData with the same
input u8, the only difference compared to SaveData is the Save-struct.

# BcatSaveData

This is accessed using the same commands for SaveData with the same
input u8. The Save-struct is the same as DeviceSaveData, except that the
titleID field is set to <input titleID>. See above regarding
SaveCreate-struct.

The 0x10-byte struct passed to
[\#CreateSaveData](#CreateSaveData "wikilink") has the first 0x5-bytes
set to all-zero.

[Category:Services](Category:Services "wikilink")

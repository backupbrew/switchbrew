# fsp-ldr

This is
"nn::fssrv::sf::IFileSystemProxyForLoader".

| Cmd | Name                  | Arguments                                                           | Notes                                                |
| --- | --------------------- | ------------------------------------------------------------------- | ---------------------------------------------------- |
| 0   | MountCode             | u64 TitleId + X descriptor [\#ContentPath](#ContentPath "wikilink") | Returns an [\#IFileSystem](#IFileSystem "wikilink"). |
| 1   | IsCodeMounted         | u64 ProcessId                                                       | Returns a bool (1 if code is mounted).               |
| 2   | \[4.0.0+\] Initialize | PID descriptor                                                      |                                                      |

# fsp-pr

This is
"nn::fssrv::sf::IProgramRegistry".

| Cmd | Name                                                                         | Notes |
| --- | ---------------------------------------------------------------------------- | ----- |
| 0   | [\#SetFsPermissions](#SetFsPermissions "wikilink")                           |       |
| 1   | [\#ClearFsPermissions](#ClearFsPermissions "wikilink")                       |       |
| 2   | \[4.0.0+\] Initialize                                                        |       |
| 256 | [\#SetEnabledProgramVerification](#SetEnabledProgramVerification "wikilink") |       |

## SetFsPermissions

Takes a storageID, a pid, a titleID, a 0x1C type-A buffer for the [ FS
Access
Header](NPDM#FS%20Access%20Header.md##FS_Access_Header "wikilink"), and
a 0x2C type-A buffer for the [ FS Access
Control](NPDM#FS%20Access%20Control.md##FS_Access_Control "wikilink")

Final FS permissions are stored as (ACI0\_perms & ACID\_perms). Will
panic(svcBreak) when buffer sizes from ipc-rawdata are invalid.

## ClearFsPermissions

Takes a pid. Removes registered FS permissions for that PID.

## SetEnabledProgramVerification

Seems to sets a global flag to inputval & 1.

When the flag is zero, it will set ret=0 instead of ret={error} when
verifying a RSA signature fails. This RSA signature seems to be the
signature in the [NPDM](NPDM.md "wikilink") ACID. It then skips
verifying what seems to be the second signature in the [NCA
header](NCA%20Format.md "wikilink"). Note that if verifying the NPDM(?)
signature is successful, and verifying that second signature fails, it
will throw an error and abort.

# fsp-srv

This is
"nn::fssrv::sf::IFileSystemProxy".

| Cmd  | Name                                                                                   |
| ---- | -------------------------------------------------------------------------------------- |
| 0    | \[1.0.0\] [\#MountContent](#MountContent "wikilink")                                   |
| 1    | [\#Initialize](#Initialize "wikilink")                                                 |
| 2    | OpenDataFileSystemByCurrentProcess                                                     |
| 7    | \[2.0.0+\] [\#MountContent7](#MountContent7 "wikilink")                                |
| 8    | \[2.0.0+\] [\#MountContent](#MountContent "wikilink")                                  |
| 9    | \[3.0.0+\] OpenDataFileSystemByApplicationId                                           |
| 11   | [\#MountBis](#MountBis "wikilink")                                                     |
| 12   | [\#OpenBisPartition](#OpenBisPartition "wikilink")                                     |
| 13   | InvalidateBisCache                                                                     |
| 17   | OpenHostFileSystemImpl                                                                 |
| 18   | MountSdCard                                                                            |
| 19   | \[2.0.0+\] FormatSdCard                                                                |
| 21   | [\#DeleteSaveData](#DeleteSaveData "wikilink")                                         |
| 22   | [\#CreateSaveData](#CreateSaveData "wikilink")                                         |
| 23   | [\#CreateSystemSaveData](#CreateSystemSaveData "wikilink")                             |
| 24   | RegisterSaveDataAtomicDeletion                                                         |
| 25   | \[2.0.0+\] DeleteSaveDataWithSpaceId                                                   |
| 26   | \[2.0.0+\] FormatSdCardDryRun                                                          |
| 27   | \[2.0.0+\] IsExFatSupported                                                            |
| 28   | \[4.0.0+\] DeleteSystemSaveData                                                        |
| 30   | [\#OpenGameCardPartition](#OpenGameCardPartition "wikilink")                           |
| 31   | [\#MountGameCardPartition](#MountGameCardPartition "wikilink")                         |
| 32   | \[3.0.0+\] ExtendSaveData                                                              |
| 51   | [\#MountSaveData](#MountSaveData "wikilink")                                           |
| 52   | [\#MountSystemSaveData](#MountSystemSaveData "wikilink")                               |
| 53   | \[2.0.0+\] MountSaveDataReadOnly                                                       |
| 57   | \[3.0.0+\] ReadSaveDataFileSystemExtraDataWithSpaceId                                  |
| 58   | ReadSaveDataFileSystemExtraData                                                        |
| 59   | \[2.0.0+\] WriteSaveDataFileSystemExtraData                                            |
| 60   | OpenSaveDataInfoReader                                                                 |
| 61   | OpenSaveDataIterator                                                                   |
| 80   | OpenSaveDataThumbnailFile                                                              |
| 81   | \[4.0.0+\] OpenSaveDataTransferManager                                                 |
| 100  | MountImageDirectory                                                                    |
| 110  | [\#MountContentStorage](#MountContentStorage "wikilink")                               |
| 200  | OpenDataStorageByCurrentProcess                                                        |
| 201  | \[3.0.0+\] OpenDataStorageByApplicationId                                              |
| 202  | [\#OpenDataStorageByDataId](#OpenDataStorageByDataId "wikilink")                       |
| 203  | Returns an [\#IStorage](#IStorage "wikilink")                                          |
| 400  | [\#OpenDeviceOperator](#OpenDeviceOperator "wikilink")                                 |
| 500  | [\#OpenSdCardDetectionEventNotifier](#OpenSdCardDetectionEventNotifier "wikilink")     |
| 501  | [\#OpenGameCardDetectionEventNotifier](#OpenGameCardDetectionEventNotifier "wikilink") |
| 600  | \[1.0.0-3.0.2\] SetCurrentPosixTime                                                    |
| 601  | QuerySaveDataTotalSize                                                                 |
| 602  | [\#VerifySaveData](#VerifySaveData "wikilink")                                         |
| 603  | CorruptSaveDataForDebug                                                                |
| 604  | CreatePaddingFile                                                                      |
| 605  | DeleteAllPaddingFiles                                                                  |
| 606  | \[2.0.0+\] GetRightsId                                                                 |
| 607  | \[2.0.0+\] RegisterExternalKey                                                         |
| 608  | \[2.0.0+\] UnregisterExternalKey                                                       |
| 609  | \[2.0.0+\] GetRightsIdByPath                                                           |
| 610  | \[3.0.0+\] GetRightsIdByPath2 (returns extra byte)                                     |
| 611  | \[4.0.0+\] SetCurrentPosixTime                                                         |
| 612  | \[4.0.0+\] GetFreeSpaceSize                                                            |
| 613  | \[4.0.0+\]                                                                             |
| 614  | \[4.0.0+\]                                                                             |
| 620  | \[2.0.0+\] [\#SetSdCardEncryptionSeed](#SetSdCardEncryptionSeed "wikilink")            |
| 630  | \[4.0.0+\] SetSdCardAccessibility                                                      |
| 631  | \[4.0.0+\] IsSdCardAccessible                                                          |
| 640  | \[4.0.0+\] IsSignedSystemPartitionOnSdCardValid                                        |
| 800  | \[2.0.0+\] GetAndClearFileSystemProxyErrorInfo                                         |
| 1000 | SetBisRootForHost                                                                      |
| 1001 | SetSaveDataSize                                                                        |
| 1002 | SetSaveDataRootPath                                                                    |
| 1003 | DisableAutoSaveDataCreation                                                            |
| 1004 | [\#SetGlobalAccessLogMode](#SetGlobalAccessLogMode "wikilink")                         |
| 1005 | [\#GetGlobalAccessLogMode](#GetGlobalAccessLogMode "wikilink")                         |
| 1006 | [\#OutputAccessLogToSdCard](#OutputAccessLogToSdCard "wikilink")                       |
| 1007 | \[4.0.0+\] RegisterUpdatePartition                                                     |
| 1008 | \[4.0.0+\] MountRegisteredUpdatePartition                                              |
| 1009 | \[4.0.0+\]                                                                             |
| 1100 | \[4.0.0+\] OverrideSaveDataTransferTokenSignVerificationKey                            |

## Permissions

Every time permissions are checked, the process registration
[\#fsp-pr](#fsp-pr "wikilink") is loaded using the session processID.
The permission data is populated with data from the
[NPDM](NPDM.md "wikilink"),

If the processID is \<= 6 (which happens only for built-in sysmodules),
it will use a hardcoded registration data. The default mask in this case
is 0x8000000000000000.

Note that the functions check whether or not at least one bit is set in
the mask. This means that, you don't need to set 0xFFFFFFFFFFFFFFFF to
get all permissions: it suffices to set 0x8000000000000000.

If the code were to request an invalid input type, panic. But this never
happens.

### RwPermissions

| Type(s) | Mask               | Name                  | Value | Used by                                                                                                                                                                    |
| ------- | ------------------ | --------------------- | ----- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0     | 0x8000000000000801 | MountContentType2     | 1     | [\#MountContent](#MountContent "wikilink")                                                                                                                                 |
| 0x1     | 0x8000000000000801 | MountContentType5     | 1     | [\#MountContent](#MountContent "wikilink")                                                                                                                                 |
| 0x2     | 0x8000000000000801 | MountContentType3     | 1     | [\#MountContent](#MountContent "wikilink")                                                                                                                                 |
| 0x3     | 0x8000000000000801 | MountContentType4     | 1     | [\#MountContent](#MountContent "wikilink")                                                                                                                                 |
| 0x4     | 0x8000000000000801 | MountContentType6     | 1     | [\#MountContent](#MountContent "wikilink")                                                                                                                                 |
| 0x5     | 0x8000000000000801 | MountContentType7     | 1     | [\#MountContent](#MountContent "wikilink")                                                                                                                                 |
| 0x6     | 0x8000000000000000 |                       | 3     |                                                                                                                                                                            |
| 0x7     | 0x8000000000000800 | ContentStorageAccess  | 3     | [\#MountContentStorage](#MountContentStorage "wikilink")                                                                                                                   |
| 0x8     | 0x8000000000001000 | ImageDirectoryAccess  | 3     | [\#MountImageDirectory](#MountImageDirectory "wikilink")                                                                                                                   |
| 0x9     | 0x8000000000000084 | MountBisType28        | 3     | [\#MountBis](#MountBis "wikilink")                                                                                                                                         |
| 0xA     | 0x8000000000000080 | MountBisType29        | 3     | [\#MountBis](#MountBis "wikilink")                                                                                                                                         |
| 0xB     | 0x8000000000008080 | MountBisType30        | 3     | [\#MountBis](#MountBis "wikilink")                                                                                                                                         |
| 0xC     | 0x8000000000008080 | MountBisType31        | 3     | [\#MountBis](#MountBis "wikilink")                                                                                                                                         |
| 0xD     | 0x8000000000000080 |                       | 3     |                                                                                                                                                                            |
| 0xE     | 0xC000000000200000 | SdCardAccess          | 3     | [\#MountSdCard](#MountSdCard "wikilink")                                                                                                                                   |
| 0xF     | 0x8000000000000010 | GameCardUser          | 3     | [\#MountGameCardPartition](#MountGameCardPartition "wikilink")                                                                                                             |
| 0x10    | 0x8000000000040020 | SaveDataAccess0       | 3     | [\#MountSaveData](#MountSaveData "wikilink")                                                                                                                               |
| 0x11    | 0x8000000000000028 | SystemSaveDataAccess0 | 3     | [\#MountSystemSaveData](#MountSystemSaveData "wikilink")                                                                                                                   |
| 0x12    | 0x8000000000000020 | SaveDataAccess1       | 3     | [\#MountSaveData](#MountSaveData "wikilink")                                                                                                                               |
| 0x13    | 0x8000000000000020 | SystemSaveDataAccess1 | 3     | [\#MountSystemSaveData](#MountSystemSaveData "wikilink")                                                                                                                   |
| 0x14    | 0x8000000000010082 | BisPartition0         | 3     | [\#OpenBisPartition](#OpenBisPartition "wikilink")                                                                                                                         |
| 0x15    | 0x8000000000010080 | BisPartition10        | 3     | [\#OpenBisPartition](#OpenBisPartition "wikilink")                                                                                                                         |
| 0x17    | 0x8000000000010080 | BisPartition20        | 3     | [\#OpenBisPartition](#OpenBisPartition "wikilink")                                                                                                                         |
| 0x18    | 0x8000000000010080 | BisPartition21        | 3     | [\#OpenBisPartition](#OpenBisPartition "wikilink")                                                                                                                         |
| 0x19    | 0x8000000000010080 | BisPartition22        | 3     | [\#OpenBisPartition](#OpenBisPartition "wikilink")                                                                                                                         |
| 0x1A    | 0x8000000000010080 | BisPartition23        | 3     | [\#OpenBisPartition](#OpenBisPartition "wikilink")                                                                                                                         |
| 0x1B    | 0x8000000000010080 | BisPartition24        | 3     | [\#OpenBisPartition](#OpenBisPartition "wikilink")                                                                                                                         |
| 0x1C    | 0x8000000000010080 | BisPartition25        | 3     | [\#OpenBisPartition](#OpenBisPartition "wikilink")                                                                                                                         |
| 0x16    | 0x8000000000000080 | BisPartition26        | 3     | [\#OpenBisPartition](#OpenBisPartition "wikilink")                                                                                                                         |
| 0x1D    | 0x8000000000000084 | BisPartition27        | 3     | [\#OpenBisPartition](#OpenBisPartition "wikilink")                                                                                                                         |
| 0x1E    | 0x8000000000000084 | BisPartition28        | 3     | [\#OpenBisPartition](#OpenBisPartition "wikilink")                                                                                                                         |
| 0x1F    | 0x8000000000000080 | BisPartition29        | 3     | [\#OpenBisPartition](#OpenBisPartition "wikilink")                                                                                                                         |
| 0x20    | 0x8000000000000080 | BisPartition30        | 3     | [\#OpenBisPartition](#OpenBisPartition "wikilink")                                                                                                                         |
| 0x21    | 0x8000000000000080 | BisPartition31        | 3     | [\#OpenBisPartition](#OpenBisPartition "wikilink")                                                                                                                         |
| 0x22    | 0x8000000000000080 | BisPartition32        | 3     | [\#OpenBisPartition](#OpenBisPartition "wikilink")                                                                                                                         |
| 0x23    | 0xC000000000200000 |                       | 3     |                                                                                                                                                                            |
| 0x24    | 0x8000000000000100 | GameCard\_System      | 3     | [\#OpenGameCardPartition](#OpenGameCardPartition "wikilink"), [\#EraseGameCard](#EraseGameCard "wikilink") (bit1), [\#WriteToGameCard](#WriteToGameCard "wikilink") (bit1) |
| 0x25    | 0x8000000000100008 | MountContent\_System  | 1     | [\#MountContent](#MountContent "wikilink"), [\#OpenDataStorageByDataId](#OpenDataStorageByDataId "wikilink")                                                               |
| 0x26    | 0xC000000000400000 | HostAccess            | 3     | [\#OpenHostFileSystemImpl](#OpenHostFileSystemImpl "wikilink")                                                                                                             |

### BoolPermissions

| Type(s)         | Mask               | Name                       | Used by                                                                                                                                                |
| --------------- | ------------------ | -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 0x0             | 0x8000000000000080 | BisCache                   | [\#InvalidateBisCache](#InvalidateBisCache "wikilink")                                                                                                 |
| 0x1             | 0x8000000000000080 | EraseMmc                   | [\#EraseMmc](#EraseMmc "wikilink")                                                                                                                     |
| 0x2             | 0x8000000000000010 | GameCardCertificate        | [\#GetGameCardDeviceCertificate](#GetGameCardDeviceCertificate "wikilink")                                                                             |
| 0x3             | 0x8000000000000010 | GameCardIdSet              | [\#GetGameCardIdSet](#GetGameCardIdSet "wikilink")                                                                                                     |
| 0x4             | 0x8000000000000200 | GameCardDriver             | [\#FinalizeGameCardDriver](#FinalizeGameCardDriver "wikilink")                                                                                         |
| 0x5             | 0x8000000000000200 | GameCardAsic               | [\#GetGameCardAsicInfo](#GetGameCardAsicInfo "wikilink")                                                                                               |
| 0x6             | 0x8000000000002020 | SaveDataCreate             | [\#CreateSaveData](#CreateSaveData "wikilink")                                                                                                         |
| 0x7             | 0x8000000000000060 | SaveDataDelete0            | [\#DeleteSaveData](#DeleteSaveData "wikilink"), [\#RegisterSaveDataAtomicDeletion](#RegisterSaveDataAtomicDeletion "wikilink")                         |
| 0x8             | 0x8000000000000028 | SystemSaveDataCreate0      | [\#CreateSystemSaveData](#CreateSystemSaveData "wikilink")                                                                                             |
| 0x9             | 0x8000000000000020 | SystemSaveDataCreate1      | [\#CreateSystemSaveData](#CreateSystemSaveData "wikilink")                                                                                             |
| 0xA             | 0x8000000000004028 | SaveDataDelete1            | [\#DeleteSaveData](#DeleteSaveData "wikilink"), [\#RegisterSaveDataAtomicDeletion](#RegisterSaveDataAtomicDeletion "wikilink")                         |
| 0xB             | 0x8000000000000060 | SaveDataIterators0         | [\#OpenSaveDataIterator](#OpenSaveDataIterator "wikilink"), [\#OpenSaveDataInfoIterator](#OpenSaveDataInfoIterator "wikilink")                         |
| 0xC             | 0x8000000000004020 | SaveDataIterators1         | [\#OpenSaveDataIterator](#OpenSaveDataIterator "wikilink"), [\#OpenSaveDataInfoIterator](#OpenSaveDataInfoIterator "wikilink")                         |
| 0xD             | 0x8000000000020000 | SaveThumbnails             | [\#OpenSaveDataThumbnailFile](#OpenSaveDataThumbnailFile "wikilink")                                                                                   |
| 0xE             | 0x8000000000000400 | PosixTime                  | [\#SetCurrentPosixTime](#SetCurrentPosixTime "wikilink")                                                                                               |
| 0xF             | 0x8000000000004060 | SaveDataExtraData          | [\#ReadSaveDataFileSystemExtraData](#ReadSaveDataFileSystemExtraData "wikilink")                                                                       |
| 0x10            | 0x8000000000080000 | GlobalMode                 | [\#SetGlobalAccessMode](#SetGlobalAccessMode "wikilink")                                                                                               |
| 0x11            | 0x8000000000080000 | SpeedEmulation             | [\#SetSpeedEmulationMode](#SetSpeedEmulationMode "wikilink")                                                                                           |
| 0x12            | Invalid            |                            |                                                                                                                                                        |
| 0x13            | 0xC000000000800000 | PaddingFiles               | [\#CreatePaddingFile](#CreatePaddingFile "wikilink"), [\#DeletePaddingFiles](#DeletePaddingFiles "wikilink")                                           |
| 0x14            | 0xC000000001000000 | SaveData\_Debug            | [\#CorruptSaveDataForDebug](#CorruptSaveDataForDebug "wikilink")                                                                                       |
| 0x15            | 0xC000000002000000 | SaveData\_SystemManagement | [\#CreateSaveData](#CreateSaveData "wikilink"), [\#MountSaveData](#MountSaveData "wikilink"), [\#SetSaveDataRootPath](#SetSaveDataRootPath "wikilink") |
| \[2.0.0+\] 0x16 | 0x8000000004000000 |                            |                                                                                                                                                        |
| \[2.0.0+\] 0x17 | 0x8000000008000000 |                            |                                                                                                                                                        |
| \[2.0.0+\] 0x18 | 0x8000000010000000 |                            |                                                                                                                                                        |
| \[2.0.0+\] 0x19 | 0x8000000000000800 |                            |                                                                                                                                                        |
| \[2.0.0+\] 0x1A | 0x8000000000004020 |                            |                                                                                                                                                        |

## Initialize

Takes a pid-descriptor.

## MountContent7

Takes an input u32 (same as [\#MountContent](#MountContent "wikilink"))
and an u64 title-id. Web-applet loads the u32 from
u32\_table\[inparam\]. The in32 must be 4.

Returns an [\#IFileSystem](#IFileSystem "wikilink").

Note: web-applet strings refer to both this cmd and the below
"MountContent" as "MountContent".

## MountContent

Takes a type-0x19 input buffer, an in32, and an input title-id.

The in32 must be 5 if the NCA type is 0 (control).

The in32 must be 2..7.

The input buffer is the output string path from nsam
[GetContentNcaPath](NS%20Services#GetContentNcaPath.md##GetContentNcaPath "wikilink").

Returns an [\#IFileSystem](#IFileSystem "wikilink").

May return errors when attempting to access NCA-paths for an
update-title with a gamecard, when the gamecard isn't inserted. May
return error 0x7D402 in some cases with update-titles. Non-val2 in32
values with NCA-type1 are unusable, even for normal titles.

The official "MountApplicationPackage" func uses this with in64=0 and
in32=7.

After the in32-specific permissions are checked, it then gets the func
retval for permissions-type 0x25 and func0.

When in32=5, it uses in64=0xffffffffffffffff internally, otherwise it
checks if in64 is set to 0xffffffffffffffff then throws an error if so.
When the in64 used internally is not 0xffffffffffffffff, it's compared
with the NCA titleID, then an error is thrown on mismatch.

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

## InvalidateBisCache

Seems to invalidate the Bis cache for MBR/GPT after overwriting that
data via the OpenBisPartition IStorage. Used by
[SystemInitializer](SystemInitializer.md "wikilink").

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

## SetSdCardEncryptionSeed

Takes 0x10-bytes of input.

Appears to be used to load the seed into FS-module state, since
FS-module itself doesn't seem to have file-reading code to handle this
itself.

[NS](NS%20Services.md "wikilink")-module uses this with data read from a
file.

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

When bit1 in GlobalAccessLogMode is clear, FS-module will just return 0
for OutputAccessLogToSdCard. However even with that set the log doesn't
show up SD, unknown why.

The input buffer is written to the "$FsAccessLog:/FsAccessLog.txt" file,
where "$FsAccessLog" is the SD-card mount-name. It's written to the
current end of the file(appended).

# IStorage

This is "nn::fssrv::sf::IStorage".

This is the interface for a raw device, usually a block
device.

| Cmd | Name                    | Arguments                                      |
| --- | ----------------------- | ---------------------------------------------- |
| 0   | Read                    | Takes a type-0x46 buffer, an offset and length |
| 1   | Write                   | Takes a type-0x45 buffer, an offset and length |
| 2   | Flush                   | None                                           |
| 3   | SetSize                 | Takes a size                                   |
| 4   | GetSize                 | None                                           |
| 5   | \[4.0.0+\] OperateRange |                                                |

# IFileSystem

This is "nn::fssrv::sf::IFileSystem".

There are two main implementations of this interface:

  - **RomFS**: Filesystem implementation statically linked in the
    binary. Uses an [\#IStorage](#IStorage "wikilink") interface as
    underlying raw device.
  - **IPC proxy**: Used for all non-RomFS filesystems. In this case,
    actual filesystem implementation is in the FS process.

| Cmd | Name                                                 |
| --- | ---------------------------------------------------- |
| 0   | CreateFile                                           |
| 1   | DeleteFile                                           |
| 2   | CreateDirectory                                      |
| 3   | DeleteDirectory                                      |
| 4   | DeleteDirectoryRecursively                           |
| 5   | RenameFile                                           |
| 6   | RenameDirectory                                      |
| 7   | [\#GetEntryType](#GetEntryType "wikilink")           |
| 8   | OpenFile                                             |
| 9   | [\#OpenDirectory](#OpenDirectory "wikilink")         |
| 10  | [\#Commit](#Commit "wikilink")                       |
| 11  | [\#GetFreeSpaceSize](#GetFreeSpaceSize "wikilink")   |
| 12  | [\#GetTotalSpaceSize](#GetTotalSpaceSize "wikilink") |
| 13  | CleanDirectoryRecursively \[3.0.0+\]                 |
| 14  | GetFileTimeStampRaw \[3.0.0+\]                       |
| 15  | \[4.0.0+\] QueryEntry                                |

## GetEntryType

Takes a type-0x9 input buffer for the path and returns
[\#DirectoryEntryType](#DirectoryEntryType "wikilink") as an output u32.

## OpenDirectory

Takes a type-0x9 input buffer for the path and an u64 **filter\_flags**.
**filter\_flags** controls what type of entries are read by the
[\#IDirectory](#IDirectory "wikilink"): bitmask 0x1 = directories,
bitmask 0x2 = files.

## Commit

Like [3DS](https://3dbrew.org/wiki/FS:ControlArchive), this has to be
used after writing to savedata for the changes to take affect.

## GetFreeSpaceSize

Takes a type-0x9 input buffer for the path and returns an output
byte-size u64 for the total free space with this FS.

## GetTotalSpaceSize

Takes a type-0x9 input buffer for the path and returns an output
byte-size u64 for the total space available with this FS(free+used).

# IDirectory

This is "nn::fssrv::sf::IDirectory".

| Cmd | Name                                         |
| --- | -------------------------------------------- |
| 0   | [\#Read](#Read "wikilink")                   |
| 1   | [\#GetEntryCount](#GetEntryCount "wikilink") |

## Read

Takes a type-0x6 output buffer and an input u64. Unknown what the u64 is
for, doesn't(?) seem to affect output. Returns an output u64(?) for the
total number of read entries, this is 0 when no more entries are
available.

The output buffer contains the read array of
[\#DirectoryEntry](#DirectoryEntry "wikilink"). This doesn't include
entries for "." and "..".

## GetEntryCount

Returns an u64 for the total number of readable
entries.

# DirectoryEntry

| Offset | Size  | Description                                            |
| ------ | ----- | ------------------------------------------------------ |
| 0x0    | 0x300 | Path                                                   |
| 0x300  | 0x4   | ?                                                      |
| 0x304  | 0x1   | [\#DirectoryEntryType](#DirectoryEntryType "wikilink") |
| 0x305  | 0x3   | Padding?                                               |
| 0x308  | 0x8?  | Filesize, 0 for directories.                           |

# DirectoryEntryType

s8 type: 0 = directory, 1 = file.

# IFile

This is "nn::fssrv::sf::IFile".

| Cmd | Name       |
| --- | ---------- |
| 0   | Read       |
| 1   | Write      |
| 2   | Flush      |
| 3   | SetSize    |
| 4   | GetSize    |
| 5   | \[4.0.0+\] |

# ISaveDataInfoReader

This is "nn::fssrv::sf::ISaveDataInfoReader".

| Cmd | Name |
| --- | ---- |
| 0   |      |

# IDeviceOperator

This is
"nn::fssrv::sf::IDeviceOperator".

| Cmd | Name                                                                           |
| --- | ------------------------------------------------------------------------------ |
| 0   | IsSdCardInserted                                                               |
| 1   | GetSdCardSpeedMode                                                             |
| 2   | \[2.0.0+\] GetSdCardCid                                                        |
| 3   | \[2.0.0+\] GetSdCardUserAreaSize                                               |
| 4   | \[2.0.0+\] GetSdCardProtectedAreaSize                                          |
| 5   | \[2.0.0+\] GetAndClearSdCardErrorInfo                                          |
| 100 | GetMmcCid                                                                      |
| 101 | GetMmcSpeedMode                                                                |
| 110 | EraseMmc                                                                       |
| 111 | GetMmcPartitionSize                                                            |
| 112 | \[2.0.0+\] GetMmcPatrolCount                                                   |
| 113 | \[2.0.0+\] GetAndClearMmcErrorInfo                                             |
| 114 | \[2.0.0+\] GetMmcExtendedCsd                                                   |
| 115 | \[4.0.0+\] SuspendMmcPatrol                                                    |
| 116 | \[4.0.0+\] ResumeMmcPatrol                                                     |
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
| 212 | \[2.0.0+\] GetGameCardErrorInfo                                                |
| 213 | \[2.0.0+\] EraseAndWriteParamDirectly                                          |
| 214 | \[2.0.0+\] ReadParamDirectly                                                   |
| 215 | \[2.0.0+\] ForceEraseGameCard                                                  |
| 216 | \[2.0.0+\] GetGameCardErrorInfo                                                |
| 217 | \[2.1.0+\] GetGameCardErrorReportInfo                                          |
| 218 | \[3.0.0+\]                                                                     |
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

This is "nn::fssrv::sf::IEventNotifier".

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
| @SystemContent |                                         |
| @UserContent   |                                         |
| @SdCardContent |                                         |
| @CalibFile     |                                         |
| @Safe          |                                         |
| @User          |                                         |
| @System        |                                         |
| @Sdcard        |                                         |
| @Host          |                                         |
| @GcApp         | Gamecard App partition (Partition 2)    |
| @GcS00000001   | Gamecard Contents.                      |
| @upp           | Gamecard update partition (Partition 0) |

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

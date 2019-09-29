# fsp-ldr

This is "nn::fssrv::sf::IFileSystemProxyForLoader".

| Cmd | Name                                                            |
| --- | --------------------------------------------------------------- |
| 0   | [\#OpenCodeFileSystem](#OpenCodeFileSystem "wikilink")          |
| 1   | [\#IsArchivedProgram](#IsArchivedProgram "wikilink")            |
| 2   | \[4.0.0+\] [\#SetCurrentProcess](#SetCurrentProcess "wikilink") |

## OpenCodeFileSystem

Takes an u64 TitleId and a [\#ContentPath](#ContentPath "wikilink").
Returns an [\#IFileSystem](#IFileSystem "wikilink").

## IsArchivedProgram

Takes an u64 ProcessId. Returns a bool (1 if the process id's
[\#ContentPath](#ContentPath "wikilink") ends in ".nca").

## SetCurrentProcess

Takes a PID descriptor.

# fsp-pr

This is "nn::fssrv::sf::IProgramRegistry".

| Cmd | Name                                                                         |
| --- | ---------------------------------------------------------------------------- |
| 0   | [\#RegisterProgram](#RegisterProgram "wikilink")                             |
| 1   | [\#UnregisterProgram](#UnregisterProgram "wikilink")                         |
| 2   | \[4.0.0+\] [\#SetCurrentProcess](#SetCurrentProcess "wikilink")              |
| 256 | [\#SetEnabledProgramVerification](#SetEnabledProgramVerification "wikilink") |

## RegisterProgram

Takes a storageID, a pid, a titleID, a 0x1C type-A buffer for the [ FS
Access
Header](NPDM#FS%20Access%20Header.md##FS_Access_Header "wikilink"), and
a 0x2C type-A buffer for the [ FS Access
Control](NPDM#FS%20Access%20Control.md##FS_Access_Control "wikilink")

Final FS permissions are stored as (ACI0\_perms & ACID\_perms). Will
panic(svcBreak) when buffer sizes from ipc-rawdata are invalid.

## UnregisterProgram

Takes a pid. Removes registered FS permissions for that PID.

## SetEnabledProgramVerification

Seems to sets a global flag to inputval & 1.

When the flag is zero, it will set ret=0 instead of ret={error} when
verifying the fixed-key [NPDM](NPDM.md "wikilink") ACID signature fails.
This also skips verifying the [NCA Header](NCA%20Format.md "wikilink")
signature using the ACID key. Note that if verifying the fixed-key ACID
signature is successful, and verifying the ACID-key NCA header signature
fails, it will throw an error and abort.

# fsp-srv

This is "nn::fssrv::sf::IFileSystemProxy".

| Cmd  | Name                                                                                                                          |
| ---- | ----------------------------------------------------------------------------------------------------------------------------- |
| 0    | \[1.0.0\] [\#OpenFileSystem](#OpenFileSystem "wikilink")                                                                      |
| 1    | [\#SetCurrentProcess](#SetCurrentProcess "wikilink")                                                                          |
| 2    | OpenDataFileSystemByCurrentProcess                                                                                            |
| 7    | \[2.0.0+\] [\#OpenFileSystemWithPatch](#OpenFileSystemWithPatch "wikilink")                                                   |
| 8    | \[2.0.0+\] [\#OpenFileSystemWithId](#OpenFileSystemWithId "wikilink")                                                         |
| 9    | \[3.0.0+\] OpenDataFileSystemByProgramId                                                                                      |
| 11   | [\#OpenBisFileSystem](#OpenBisFileSystem "wikilink")                                                                          |
| 12   | [\#OpenBisStorage](#OpenBisStorage "wikilink")                                                                                |
| 13   | InvalidateBisCache                                                                                                            |
| 17   | OpenHostFileSystem                                                                                                            |
| 18   | OpenSdCardFileSystem                                                                                                          |
| 19   | \[2.0.0+\] FormatSdCardFileSystem                                                                                             |
| 21   | [\#DeleteSaveDataFileSystem](#DeleteSaveDataFileSystem "wikilink")                                                            |
| 22   | [\#CreateSaveDataFileSystem](#CreateSaveDataFileSystem "wikilink")                                                            |
| 23   | [\#CreateSaveDataFileSystemBySystemSaveDataId](#CreateSaveDataFileSystemBySystemSaveDataId "wikilink")                        |
| 24   | RegisterSaveDataFileSystemAtomicDeletion                                                                                      |
| 25   | \[2.0.0+\] DeleteSaveDataFileSystemBySaveDataSpaceId                                                                          |
| 26   | \[2.0.0+\] FormatSdCardDryRun                                                                                                 |
| 27   | \[2.0.0+\] IsExFatSupported                                                                                                   |
| 28   | \[4.0.0+\] DeleteSaveDataFileSystemBySaveDataAttribute                                                                        |
| 30   | [\#OpenGameCardStorage](#OpenGameCardStorage "wikilink")                                                                      |
| 31   | [\#OpenGameCardFileSystem](#OpenGameCardFileSystem "wikilink")                                                                |
| 32   | \[3.0.0+\] ExtendSaveDataFileSystem                                                                                           |
| 33   | \[5.0.0+\] DeleteCacheStorage                                                                                                 |
| 34   | \[5.0.0+\] GetCacheStorageSize                                                                                                |
| 35   | \[6.0.0+\] [\#CreateSaveDataFileSystemWithHashSalt](#CreateSaveDataFileSystemWithHashSalt "wikilink")                         |
| 36   | \[9.0.0+\] OpenHostFileSystemWithOption                                                                                       |
| 51   | [\#OpenSaveDataFileSystem](#OpenSaveDataFileSystem "wikilink")                                                                |
| 52   | [\#OpenSaveDataFileSystemBySystemSaveDataId](#OpenSaveDataFileSystemBySystemSaveDataId "wikilink")                            |
| 53   | \[2.0.0+\] OpenReadOnlySaveDataFileSystem                                                                                     |
| 57   | \[3.0.0+\] [\#ReadSaveDataFileSystemExtraDataBySaveDataSpaceId](#ReadSaveDataFileSystemExtraDataBySaveDataSpaceId "wikilink") |
| 58   | [\#ReadSaveDataFileSystemExtraData](#ReadSaveDataFileSystemExtraData "wikilink")                                              |
| 59   | \[2.0.0+\] WriteSaveDataFileSystemExtraData                                                                                   |
| 60   | [\#OpenSaveDataInfoReader](#OpenSaveDataInfoReader "wikilink")                                                                |
| 61   | [\#OpenSaveDataInfoReaderBySaveDataSpaceId](#OpenSaveDataInfoReaderBySaveDataSpaceId "wikilink")                              |
| 62   | \[5.0.0+\] OpenSaveDataInfoReaderOnlyCacheStorage                                                                             |
| 64   | \[5.0.0+\] OpenSaveDataInternalStorageFileSystem                                                                              |
| 65   | \[5.0.0+\] UpdateSaveDataMacForDebug                                                                                          |
| 66   | \[5.0.0+\] WriteSaveDataFileSystemExtraDataWithMask                                                                           |
| 67   | \[6.0.0+\] [\#FindSaveDataWithFilter](#FindSaveDataWithFilter "wikilink")                                                     |
| 68   | \[6.0.0+\] [\#OpenSaveDataInfoReaderWithFilter](#OpenSaveDataInfoReaderWithFilter "wikilink")                                 |
| 69   | \[8.0.0+\] ReadSaveDataFileSystemExtraDataBySaveDataAttribute                                                                 |
| 70   | \[8.0.0+\] WriteSaveDataFileSystemExtraDataBySaveDataAttribute                                                                |
| 80   | OpenSaveDataMetaFile                                                                                                          |
| 81   | \[4.0.0+\] [\#OpenSaveDataTransferManager](#OpenSaveDataTransferManager "wikilink")                                           |
| 82   | \[5.0.0+\] [\#OpenSaveDataTransferManagerVersion2](#OpenSaveDataTransferManagerVersion2 "wikilink")                           |
| 83   | \[6.0.0+\] [\#OpenSaveDataTransferProhibiter](#OpenSaveDataTransferProhibiter "wikilink")                                     |
| 84   | \[6.0.0+\] [\#ListAccessibleSaveDataOwnerId](#ListAccessibleSaveDataOwnerId "wikilink")                                       |
| 85   | \[9.0.0+\] [\#OpenSaveDataTransferManagerForSaveDataRepair](#OpenSaveDataTransferManagerForSaveDataRepair "wikilink")         |
| 100  | OpenImageDirectoryFileSystem                                                                                                  |
| 110  | [\#OpenContentStorageFileSystem](#OpenContentStorageFileSystem "wikilink")                                                    |
| 120  | \[6.0.0+\] [\#OpenCloudBackupWorkStorageFileSystem](#OpenCloudBackupWorkStorageFileSystem "wikilink")                         |
| 130  | \[7.0.0+\] [\#OpenCustomStorageFileSystem](#OpenCustomStorageFileSystem "wikilink")                                           |
| 200  | OpenDataStorageByCurrentProcess                                                                                               |
| 201  | \[3.0.0+\] OpenDataStorageByProgramId                                                                                         |
| 202  | [\#OpenDataStorageByDataId](#OpenDataStorageByDataId "wikilink")                                                              |
| 203  | OpenPatchDataStorageByCurrentProcess                                                                                          |
| 204  | \[7.0.0+\] [\#OpenDataFileSystemWithProgramIndex](#OpenDataFileSystemWithProgramIndex "wikilink")                             |
| 205  | \[7.0.0+\] [\#OpenDataStorageWithProgramIndex](#OpenDataStorageWithProgramIndex "wikilink")                                   |
| 400  | [\#OpenDeviceOperator](#OpenDeviceOperator "wikilink")                                                                        |
| 500  | [\#OpenSdCardDetectionEventNotifier](#OpenSdCardDetectionEventNotifier "wikilink")                                            |
| 501  | [\#OpenGameCardDetectionEventNotifier](#OpenGameCardDetectionEventNotifier "wikilink")                                        |
| 510  | \[5.0.0+\] OpenSystemDataUpdateEventNotifier                                                                                  |
| 511  | \[5.0.0+\] NotifySystemDataUpdateEvent                                                                                        |
| 520  | \[6.0.0+\] [\#SimulateDeviceDetectionEvent](#SimulateDeviceDetectionEvent "wikilink")                                         |
| 600  | \[1.0.0-3.0.2\] SetCurrentPosixTime                                                                                           |
| 601  | QuerySaveDataTotalSize                                                                                                        |
| 602  | [\#VerifySaveDataFileSystem](#VerifySaveDataFileSystem "wikilink")                                                            |
| 603  | CorruptSaveDataFileSystem                                                                                                     |
| 604  | CreatePaddingFile                                                                                                             |
| 605  | DeleteAllPaddingFiles                                                                                                         |
| 606  | \[2.0.0+\] GetRightsId                                                                                                        |
| 607  | \[2.0.0+\] RegisterExternalKey                                                                                                |
| 608  | \[2.0.0+\] UnregisterAllExternalKey                                                                                           |
| 609  | \[2.0.0+\] GetRightsIdByPath                                                                                                  |
| 610  | \[3.0.0+\] GetRightsIdAndKeyGenerationByPath                                                                                  |
| 611  | \[4.0.0+\] SetCurrentPosixTimeWithTimeDifference                                                                              |
| 612  | \[4.0.0+\] GetFreeSpaceSizeForSaveData                                                                                        |
| 613  | \[4.0.0+\] VerifySaveDataFileSystemBySaveDataSpaceId                                                                          |
| 614  | \[4.0.0+\] CorruptSaveDataFileSystemBySaveDataSpaceId                                                                         |
| 615  | \[5.0.0+\] QuerySaveDataInternalStorageTotalSize                                                                              |
| 616  | \[6.0.0+\] [\#GetSaveDataCommitId](#GetSaveDataCommitId "wikilink")                                                           |
| 617  | \[7.0.0+\] UnregisterExternalKey                                                                                              |
| 620  | \[2.0.0+\] [\#SetSdCardEncryptionSeed](#SetSdCardEncryptionSeed "wikilink")                                                   |
| 630  | \[4.0.0+\] SetSdCardAccessibility                                                                                             |
| 631  | \[4.0.0+\] IsSdCardAccessible                                                                                                 |
| 640  | \[4.0.0-7.0.1\] IsSignedSystemPartitionOnSdCardValid                                                                          |
| 700  | \[5.0.0+\] [\#OpenAccessFailureDetectionEventNotifier](#OpenAccessFailureDetectionEventNotifier "wikilink")                   |
| 701  | \[5.0.0+\] GetAccessFailureDetectionEvent                                                                                     |
| 702  | \[5.0.0+\] IsAccessFailureDetected                                                                                            |
| 710  | \[5.0.0+\] ResolveAccessFailure                                                                                               |
| 720  | \[5.0.0+\] AbandonAccessFailure                                                                                               |
| 800  | \[2.0.0+\] GetAndClearErrorInfo                                                                                               |
| 810  | \[7.0.0+\] RegisterProgramIndexMapInfo                                                                                        |
| 1000 | SetBisRootForHost                                                                                                             |
| 1001 | [\#SetSaveDataSize](#SetSaveDataSize "wikilink")                                                                              |
| 1002 | [\#SetSaveDataRootPath](#SetSaveDataRootPath "wikilink")                                                                      |
| 1003 | DisableAutoSaveDataCreation                                                                                                   |
| 1004 | [\#SetGlobalAccessLogMode](#SetGlobalAccessLogMode "wikilink")                                                                |
| 1005 | [\#GetGlobalAccessLogMode](#GetGlobalAccessLogMode "wikilink")                                                                |
| 1006 | [\#OutputAccessLogToSdCard](#OutputAccessLogToSdCard "wikilink")                                                              |
| 1007 | \[4.0.0+\] RegisterUpdatePartition                                                                                            |
| 1008 | \[4.0.0+\] OpenRegisteredUpdatePartition                                                                                      |
| 1009 | \[4.0.0+\] GetAndClearMemoryReportInfo                                                                                        |
| 1010 | \[5.1.0-6.2.0\] SetDataStorageRedirectTarget                                                                                  |
| 1011 | \[7.0.0+\] [\#GetProgramIndexForAccessLog](#GetProgramIndexForAccessLog "wikilink")                                           |
| 1012 | \[9.0.0+\] GetFsStackUsage                                                                                                    |
| 1013 | \[9.0.0+\] UnsetSaveDataRootPath                                                                                              |
| 1100 | \[4.0.0+\] OverrideSaveDataTransferTokenSignVerificationKey                                                                   |
| 1110 | \[6.0.0+\] CorruptSaveDataFileSystemByOffset                                                                                  |
| 1200 | \[6.0.0+\] [\#OpenMultiCommitManager](#OpenMultiCommitManager "wikilink")                                                     |

## Permissions

Every time permissions are checked, the process registration
[\#fsp-pr](#fsp-pr "wikilink") is loaded using the session processID.
The permission data is populated with data from the
[NPDM](NPDM.md "wikilink").

If the processID is \<= 6 (which happens only for built-in sysmodules),
it will use a hardcoded registration data. The default mask in this case
is 0x8000000000000000.

Note that the functions check whether or not at least one bit is set in
the mask. This means that, you don't need to set 0xFFFFFFFFFFFFFFFF to
get all permissions: it suffices to set 0x8000000000000000.

If the code were to request an invalid input type, panic. But this never
happens.

The output values for [\#ReadWrite](#ReadWrite "wikilink")
CanMountRegisteredUpdatePartition and [\#Call](#Call "wikilink")
CanRegisterUpdatePartition are masked with the cached value of
[DebugMode](SMC#IsDebugMode.md##IsDebugMode "wikilink").

### ReadWrite

<table>
<thead>
<tr class="header">
<th><p>AccessibilityType</p></th>
<th><p>Mask</p></th>
<th><p>Name</p></th>
<th><p>Value</p></th>
<th><p>Used by</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x0</p></td>
<td><p>0x8000000000000801</p></td>
<td><p>CanMountLogo</p></td>
<td><p>1</p></td>
<td><p><a href="#OpenFileSystem" title="wikilink">#OpenFileSystem</a>, <a href="#OpenFileSystemWithPatch" title="wikilink">#OpenFileSystemWithPatch</a>, <a href="#OpenFileSystemWithId" title="wikilink">#OpenFileSystemWithId</a></p></td>
</tr>
<tr class="even">
<td><p>0x1</p></td>
<td><p>0x8000000000000801</p></td>
<td><p>CanMountContentMeta</p></td>
<td><p>1</p></td>
<td><p><a href="#OpenFileSystem" title="wikilink">#OpenFileSystem</a>, <a href="#OpenFileSystemWithPatch" title="wikilink">#OpenFileSystemWithPatch</a>, <a href="#OpenFileSystemWithId" title="wikilink">#OpenFileSystemWithId</a></p></td>
</tr>
<tr class="odd">
<td><p>0x2</p></td>
<td><p>0x8000000000000801</p></td>
<td><p>CanMountContentControl</p></td>
<td><p>1</p></td>
<td><p><a href="#OpenFileSystem" title="wikilink">#OpenFileSystem</a>, <a href="#OpenFileSystemWithPatch" title="wikilink">#OpenFileSystemWithPatch</a>, <a href="#OpenFileSystemWithId" title="wikilink">#OpenFileSystemWithId</a></p></td>
</tr>
<tr class="even">
<td><p>0x3</p></td>
<td><p>0x8000000000000801</p></td>
<td><p>CanMountContentManual</p></td>
<td><p>1</p></td>
<td><p><a href="#OpenFileSystem" title="wikilink">#OpenFileSystem</a>, <a href="#OpenFileSystemWithPatch" title="wikilink">#OpenFileSystemWithPatch</a>, <a href="#OpenFileSystemWithId" title="wikilink">#OpenFileSystemWithId</a></p></td>
</tr>
<tr class="odd">
<td><p>0x4</p></td>
<td><p>0x8000000000000801</p></td>
<td><p>CanMountContentData</p></td>
<td><p>1</p></td>
<td><p><a href="#OpenFileSystem" title="wikilink">#OpenFileSystem</a>, <a href="#OpenFileSystemWithPatch" title="wikilink">#OpenFileSystemWithPatch</a>, <a href="#OpenFileSystemWithId" title="wikilink">#OpenFileSystemWithId</a></p></td>
</tr>
<tr class="even">
<td><p>0x5</p></td>
<td><p>0x8000000000000801</p></td>
<td><p>CanMountApplicationPackage</p></td>
<td><p>1</p></td>
<td><p><a href="#OpenFileSystem" title="wikilink">#OpenFileSystem</a>, <a href="#OpenFileSystemWithPatch" title="wikilink">#OpenFileSystemWithPatch</a>, <a href="#OpenFileSystemWithId" title="wikilink">#OpenFileSystemWithId</a></p></td>
</tr>
<tr class="odd">
<td><p>0x6</p></td>
<td><p>0x8000000000000000</p></td>
<td><p>CanMountSaveDataStorage</p></td>
<td><p>3</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>0x7</p></td>
<td><p>0x8000000000000800</p></td>
<td><p>CanMountContentStorage</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenContentStorageFileSystem" title="wikilink">#OpenContentStorageFileSystem</a></p></td>
</tr>
<tr class="odd">
<td><p>0x8</p></td>
<td><p>0x8000000000001000</p></td>
<td><p>CanMountImageAndVideoStorage</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenImageDirectoryFileSystem" title="wikilink">#OpenImageDirectoryFileSystem</a></p></td>
</tr>
<tr class="even">
<td><p>0x9</p></td>
<td><p>0x8000000200000000<br />
([1.0.0-5.1.0] 0x8000000000000084)</p></td>
<td><p>CanMountCloudBackupWorkStorage</p></td>
<td><p>3</p></td>
<td><p>OpenCloudBackupWorkStorageFileSystem</p></td>
</tr>
<tr class="odd">
<td><p>0xA</p></td>
<td><p>0x8000000000000000<br />
([7.0.0-7.0.1] 0x4000000000000000)<br />
([6.0.0-6.2.0] 0x8000000000000084)<br />
([1.0.0-5.1.0] 0x8000000000000080)</p></td>
<td><p>CanMountCustomStorage0</p></td>
<td><p>3</p></td>
<td><p>OpenCustomStorageFileSystem</p></td>
</tr>
<tr class="even">
<td><p>0xB</p></td>
<td><p>0x8000000000000084<br />
([6.0.0-6.2.0] 0x8000000000000080)<br />
([1.0.0-5.1.0] 0x8000000000008080)</p></td>
<td><p>CanMountBisCalibrationFile</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenBisFileSystem" title="wikilink">#OpenBisFileSystem</a></p></td>
</tr>
<tr class="odd">
<td><p>0xC</p></td>
<td><p>0x8000000000000080<br />
([1.0.0-6.2.0] 0x8000000000008080)</p></td>
<td><p>CanMountBisSafeMode</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenBisFileSystem" title="wikilink">#OpenBisFileSystem</a></p></td>
</tr>
<tr class="even">
<td><p>0xD</p></td>
<td><p>0x8000000000008080<br />
([1.0.0-5.1.0] 0x8000000000000080)</p></td>
<td><p>CanMountBisUser</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenBisFileSystem" title="wikilink">#OpenBisFileSystem</a></p></td>
</tr>
<tr class="odd">
<td><p>0xE</p></td>
<td><p>0x8000000000008080<br />
([3.0.0-6.2.0] 0x8000000000000080)<br />
([1.0.0-2.3.0] 0xC000000000200000)</p></td>
<td><p>CanMountBisSystem</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenBisFileSystem" title="wikilink">#OpenBisFileSystem</a></p></td>
</tr>
<tr class="even">
<td><p>0xF</p></td>
<td><p>0x8000000000000080<br />
([3.0.0-5.1.0] 0xC000000000200000)<br />
([1.0.0-2.3.0] 0x8000000000000010)</p></td>
<td><p>CanMountBisSystemProperEncryption</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenBisFileSystem" title="wikilink">#OpenBisFileSystem</a></p></td>
</tr>
<tr class="odd">
<td><p>0x10</p></td>
<td><p>0x8000000000000080<br />
([6.0.0-6.2.0] 0xC000000000200000<br />
([3.0.0-5.1.0] 0x8000000000000010)<br />
([1.0.0-2.3.0] 0x8000000000040020)</p></td>
<td><p>CanMountBisSystemProperPartition</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenBisFileSystem" title="wikilink">#OpenBisFileSystem</a></p></td>
</tr>
<tr class="even">
<td><p>0x11</p></td>
<td><p>0xC000000000200000<br />
([6.0.0-6.2.0] 0x8000000000000010)<br />
([3.0.0-5.1.0] 0x8000000000040020)<br />
([1.0.0-2.3.0] 0x8000000000000028)</p></td>
<td><p>CanMountSdCard</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenSdCardFileSystem" title="wikilink">#OpenSdCardFileSystem</a></p></td>
</tr>
<tr class="odd">
<td><p>0x12</p></td>
<td><p>0x8000000000000010<br />
([6.0.0-6.2.0] 0x8000000000040020)<br />
([3.0.0-5.1.0] 0x8000000000000028)<br />
([1.0.0-2.3.0] 0x8000000000000020)</p></td>
<td><p>CanMountGameCard</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenGameCardFileSystem" title="wikilink">#OpenGameCardFileSystem</a></p></td>
</tr>
<tr class="even">
<td><p>0x13</p></td>
<td><p>0x8000000000040020<br />
([6.0.0-6.2.0] 0x8000000000000028)<br />
([1.0.0-5.1.0] 0x8000000000000020)</p></td>
<td><p>CanMountDeviceSaveData</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenSaveDataFileSystem" title="wikilink">#OpenSaveDataFileSystem</a></p></td>
</tr>
<tr class="odd">
<td><p>0x14</p></td>
<td><p>0x8000000000000028<br />
([3.0.0-6.2.0] 0x8000000000000020)<br />
([1.0.0-2.3.0] 0x8000000000010082)</p></td>
<td><p>CanMountSystemSaveData</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenSaveDataFileSystemBySystemSaveDataId" title="wikilink">#OpenSaveDataFileSystemBySystemSaveDataId</a></p></td>
</tr>
<tr class="even">
<td><p>0x15</p></td>
<td><p>0x8000000000000020<br />
([3.0.0-5.1.0] 0x8000000000010082)<br />
([1.0.0-2.3.0] 0x8000000000010080)</p></td>
<td><p>CanMountOthersSaveData</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenSaveDataFileSystem" title="wikilink">#OpenSaveDataFileSystem</a></p></td>
</tr>
<tr class="odd">
<td><p>0x16</p></td>
<td><p>0x8000000000000020<br />
([6.0.0-6.2.0] 0x8000000000010082)<br />
([1.0.0-5.1.0] 0x8000000000010080)</p></td>
<td><p>CanMountOthersSystemSaveData</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenSaveDataFileSystemBySystemSaveDataId" title="wikilink">#OpenSaveDataFileSystemBySystemSaveDataId</a></p></td>
</tr>
<tr class="even">
<td><p>0x17</p></td>
<td><p>0x8000000000010082<br />
([6.0.0-6.2.0] 0x8000000000010080)<br />
([3.0.0-5.1.0] 0x8000000000000080)<br />
([1.0.0-2.3.0] 0x8000000000010080)</p></td>
<td><p>CanOpenBisPartitionBootPartition1Root</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenBisStorage" title="wikilink">#OpenBisStorage</a></p></td>
</tr>
<tr class="odd">
<td><p>0x18</p></td>
<td><p>0x8000000000010080<br />
([6.0.0-6.2.0] 0x8000000000000080)<br />
([1.0.0-5.1.0] 0x8000000000010080)</p></td>
<td><p>CanOpenBisPartitionBootPartition2Root</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenBisStorage" title="wikilink">#OpenBisStorage</a></p></td>
</tr>
<tr class="even">
<td><p>0x19</p></td>
<td><p>0x8000000000000080<br />
([6.0.0-6.2.0] 0x8000000000010080)</p></td>
<td><p>CanOpenBisPartitionUserDataRoot</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenBisStorage" title="wikilink">#OpenBisStorage</a></p></td>
</tr>
<tr class="odd">
<td><p>0x1A</p></td>
<td><p>0x8000000000010080</p></td>
<td><p>CanOpenBisPartitionBootConfigAndPackage2Part1</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenBisStorage" title="wikilink">#OpenBisStorage</a></p></td>
</tr>
<tr class="even">
<td><p>0x1B</p></td>
<td><p>0x8000000000010080</p></td>
<td><p>CanOpenBisPartitionBootConfigAndPackage2Part2</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenBisStorage" title="wikilink">#OpenBisStorage</a></p></td>
</tr>
<tr class="odd">
<td><p>0x1C</p></td>
<td><p>0x8000000000010080</p></td>
<td><p>CanOpenBisPartitionBootConfigAndPackage2Part3</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenBisStorage" title="wikilink">#OpenBisStorage</a></p></td>
</tr>
<tr class="even">
<td><p>0x1D</p></td>
<td><p>0x8000000000010080<br />
([1.0.0-2.3.0] 0x8000000000000084)</p></td>
<td><p>CanOpenBisPartitionBootConfigAndPackage2Part4</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenBisStorage" title="wikilink">#OpenBisStorage</a></p></td>
</tr>
<tr class="odd">
<td><p>0x1E</p></td>
<td><p>0x8000000000010080<br />
([1.0.0-5.1.0] 0x8000000000000084)</p></td>
<td><p>CanOpenBisPartitionBootConfigAndPackage2Part5</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenBisStorage" title="wikilink">#OpenBisStorage</a></p></td>
</tr>
<tr class="even">
<td><p>0x1F</p></td>
<td><p>0x8000000000010080<br />
([6.0.0-6.2.0] 0x8000000000000084)<br />
([1.0.0-2.3.0] 0x8000000000000080)</p></td>
<td><p>CanOpenBisPartitionBootConfigAndPackage2Part6</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenBisStorage" title="wikilink">#OpenBisStorage</a></p></td>
</tr>
<tr class="odd">
<td><p>0x20</p></td>
<td><p>0x8000000000000084<br />
([1.0.0-5.1.0] 0x8000000000000080)</p></td>
<td><p>CanOpenBisPartitionCalibrationBinary</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenBisStorage" title="wikilink">#OpenBisStorage</a></p></td>
</tr>
<tr class="even">
<td><p>0x21</p></td>
<td><p>0x8000000000000084<br />
([6.0.0-6.2.0] 0x8000000000000080)</p></td>
<td><p>CanOpenBisPartitionCalibrationFile</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenBisStorage" title="wikilink">#OpenBisStorage</a></p></td>
</tr>
<tr class="odd">
<td><p>0x22</p></td>
<td><p>0x8000000000000080</p></td>
<td><p>CanOpenBisPartitionSafeMode</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenBisStorage" title="wikilink">#OpenBisStorage</a></p></td>
</tr>
<tr class="even">
<td><p>0x23</p></td>
<td><p>0x8000000000000080<br />
([1.0.0-2.3.0] 0xC000000000200000)</p></td>
<td><p>CanOpenBisPartitionUser</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenBisStorage" title="wikilink">#OpenBisStorage</a></p></td>
</tr>
<tr class="odd">
<td><p>0x24</p></td>
<td><p>0x8000000000000080<br />
([1.0.0-2.3.0] 0x8000000000000100)</p></td>
<td><p>CanOpenBisPartitionSystem</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenBisStorage" title="wikilink">#OpenBisStorage</a></p></td>
</tr>
<tr class="even">
<td><p>0x25</p></td>
<td><p>0x8000000000000080<br />
([3.0.0-5.1.0] 0xC000000000200000)<br />
([1.0.0-2.3.0] 0x8000000000100008)</p></td>
<td><p>CanOpenBisPartitionSystemProperEncryption</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenBisStorage" title="wikilink">#OpenBisStorage</a></p></td>
</tr>
<tr class="odd">
<td><p>0x26</p></td>
<td><p>0x8000000000000080<br />
([6.0.0-6.2.0] 0xC000000000200000)<br />
([3.0.0-5.1.0] 0x8000000000000100)<br />
([1.0.0-2.3.0] 0xC000000000400000)</p></td>
<td><p>CanOpenBisPartitionSystemProperPartition</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenBisStorage" title="wikilink">#OpenBisStorage</a></p></td>
</tr>
<tr class="even">
<td><p>[3.0.0+] 0x27</p></td>
<td><p>0xC000000000200000<br />
([6.0.0-6.2.0] 0x8000000000000100)<br />
([3.0.0-5.1.0] 0x8000000000100008)</p></td>
<td><p>CanOpenSdCardStorage</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>[3.0.0+] 0x28</p></td>
<td><p>0x8000000000000100<br />
([6.0.0-6.2.0] 0x8000000000100008)<br />
([3.0.0-5.1.0] 0xC000000000400000)</p></td>
<td><p>CanOpenGameCardStorage</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenGameCardStorage" title="wikilink">#OpenGameCardStorage</a>, <a href="#EraseGameCard" title="wikilink">#EraseGameCard</a> (bit1), <a href="#WriteToGameCard" title="wikilink">#WriteToGameCard</a> (bit1), <a href="#GetGameCardErrorInfo" title="wikilink">#GetGameCardErrorInfo</a> (bit1), <a href="#EraseAndWriteParamDirectly" title="wikilink">#EraseAndWriteParamDirectly</a> (bit1), <a href="#ReadParamDirectly" title="wikilink">#ReadParamDirectly</a> (bit1), <a href="#ForceEraseGameCard" title="wikilink">#ForceEraseGameCard</a> (bit1)</p></td>
</tr>
<tr class="even">
<td><p>[4.0.0+] 0x29</p></td>
<td><p>0x8000000000100008<br />
([6.0.0-6.2.0] 0xC000000000400000)<br />
([4.0.0-5.1.0] 0x8000000000010000)</p></td>
<td><p>CanMountSystemDataPrivate</p></td>
<td><p>1</p></td>
<td><p><a href="#OpenFileSystem" title="wikilink">#OpenFileSystem</a>, <a href="#OpenDataStorageByDataId" title="wikilink">#OpenDataStorageByDataId</a></p></td>
</tr>
<tr class="odd">
<td><p>[5.0.0+] 0x2A</p></td>
<td><p>0xC000000000400000<br />
([6.0.0-6.2.0] 0x8000000000010000)<br />
([5.0.0-5.1.0] 0x8000000000000000)</p></td>
<td><p>CanMountHost</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenHostFileSystem" title="wikilink">#OpenHostFileSystem</a></p></td>
</tr>
<tr class="even">
<td><p>[6.0.0+] 0x2B</p></td>
<td><p>0x8000000000010000<br />
([6.0.0-6.2.0] 0x8000000000000000)</p></td>
<td><p>CanMountRegisteredUpdatePartition</p></td>
<td><p>1</p></td>
<td><p><a href="#OpenRegisteredUpdatePartition" title="wikilink">#OpenRegisteredUpdatePartition</a></p></td>
</tr>
<tr class="odd">
<td><p>[7.0.0+] 0x2C</p></td>
<td><p>0x8000000000000000</p></td>
<td><p>CanOpenSaveDataInternalStorage</p></td>
<td><p>3</p></td>
<td><p><a href="#OpenSaveDataInternalStorageFileSystem" title="wikilink">#OpenSaveDataInternalStorageFileSystem</a></p></td>
</tr>
<tr class="even">
<td><p>[7.0.0+] 0x2D</p></td>
<td><p>0x0000000000000000</p></td>
<td><p>CanNotMountCustomStorage</p></td>
<td><p>3</p></td>
<td><p>OpenCustomStorageFileSystem</p></td>
</tr>
</tbody>
</table>

### Call

<table>
<thead>
<tr class="header">
<th><p>OperationType</p></th>
<th><p>Mask</p></th>
<th><p>Name</p></th>
<th><p>Used by</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x0</p></td>
<td><p>0x8000000000000080</p></td>
<td><p>CanInvalidateBisCache</p></td>
<td><p><a href="#InvalidateBisCache" title="wikilink">#InvalidateBisCache</a></p></td>
</tr>
<tr class="even">
<td><p>0x1</p></td>
<td><p>0x8000000000000080</p></td>
<td><p>CanEraseMmc</p></td>
<td><p>EraseMmc</p></td>
</tr>
<tr class="odd">
<td><p>0x2</p></td>
<td><p>0x8000000000000010</p></td>
<td><p>CanGetGameCardDeviceCertificate</p></td>
<td><p>GetGameCardDeviceCertificate</p></td>
</tr>
<tr class="even">
<td><p>0x3</p></td>
<td><p>0x8000000000000010</p></td>
<td><p>CanGetGameCardIdSet</p></td>
<td><p>GetGameCardIdSet</p></td>
</tr>
<tr class="odd">
<td><p>0x4</p></td>
<td><p>0x8000000000000200</p></td>
<td><p>CanFinalizeGameCardDriver</p></td>
<td><p>FinalizeGameCardDriver</p></td>
</tr>
<tr class="even">
<td><p>0x5</p></td>
<td><p>0x8000000000000200</p></td>
<td><p>CanGetGameCardAsicInfo</p></td>
<td><p>GetGameCardAsicInfo</p></td>
</tr>
<tr class="odd">
<td><p>0x6</p></td>
<td><p>0x8000000000002020</p></td>
<td><p>CanCreateSaveData</p></td>
<td><p><a href="#CreateSaveDataFileSystem" title="wikilink">#CreateSaveDataFileSystem</a></p></td>
</tr>
<tr class="even">
<td><p>0x7</p></td>
<td><p>0x8000000000000060</p></td>
<td><p>CanDeleteSaveData</p></td>
<td><p><a href="#DeleteSaveDataFileSystem" title="wikilink">#DeleteSaveDataFileSystem</a>, RegisterSaveDataFileSystemAtomicDeletion</p></td>
</tr>
<tr class="odd">
<td><p>0x8</p></td>
<td><p>0x8000000000000028</p></td>
<td><p>CanCreateSystemSaveData</p></td>
<td><p>CreateSaveDataFileSystemBySystemSaveDataId</p></td>
</tr>
<tr class="even">
<td><p>0x9</p></td>
<td><p>0x8000000000000020</p></td>
<td><p>CanCreateOthersSystemSaveData</p></td>
<td><p>CreateSaveDataFileSystemBySystemSaveDataId</p></td>
</tr>
<tr class="odd">
<td><p>0xA</p></td>
<td><p>0x8000000000004028</p></td>
<td><p>CanDeleteSystemSaveData</p></td>
<td><p><a href="#DeleteSaveDataFileSystem" title="wikilink">#DeleteSaveDataFileSystem</a>, RegisterSaveDataFileSystemAtomicDeletion</p></td>
</tr>
<tr class="even">
<td><p>0xB</p></td>
<td><p>0x8000000000000060</p></td>
<td><p>CanOpenSaveDataInfoReader</p></td>
<td><p><a href="#OpenSaveDataInfoReaderBySaveDataSpaceId" title="wikilink">#OpenSaveDataInfoReaderBySaveDataSpaceId</a>, <a href="#OpenSaveDataInfoReader" title="wikilink">#OpenSaveDataInfoReader</a></p></td>
</tr>
<tr class="odd">
<td><p>0xC</p></td>
<td><p>0x8000000000004020</p></td>
<td><p>CanOpenSaveDataInfoReaderForSystem</p></td>
<td><p><a href="#OpenSaveDataInfoReaderBySaveDataSpaceId" title="wikilink">#OpenSaveDataInfoReaderBySaveDataSpaceId</a>, <a href="#OpenSaveDataInfoReader" title="wikilink">#OpenSaveDataInfoReader</a></p></td>
</tr>
<tr class="even">
<td><p>0xD</p></td>
<td><p>0x8000000000000040<br />
([1.0.0-5.1.0] 0x8000000000020000)</p></td>
<td><p>CanOpenSaveDataInfoReaderForInternal</p></td>
<td><p><a href="#OpenSaveDataInfoReaderWithFilter" title="wikilink">#OpenSaveDataInfoReaderWithFilter</a></p></td>
</tr>
<tr class="odd">
<td><p>0xE</p></td>
<td><p>0x8000000000020000<br />
([1.0.0-5.1.0] 0x8000000000000400)</p></td>
<td><p>CanOpenSaveDataMetaFile</p></td>
<td><p>OpenSaveDataMetaFile</p></td>
</tr>
<tr class="even">
<td><p>0xF</p></td>
<td><p>0x8000000000000400<br />
([1.0.0-5.1.0] 0x8000000000004060)</p></td>
<td><p>CanSetCurrentPosixTime</p></td>
<td><p>SetCurrentPosixTime, SetCurrentPosixTimeWithTimeDifference</p></td>
</tr>
<tr class="odd">
<td><p>0x10</p></td>
<td><p>0x8000000000004060<br />
([1.0.0-5.1.0] 0x8000000000080000)</p></td>
<td><p>CanReadSaveDataFileSystemExtraData</p></td>
<td><p><a href="#ReadSaveDataFileSystemExtraData" title="wikilink">#ReadSaveDataFileSystemExtraData</a></p></td>
</tr>
<tr class="even">
<td><p>0x11</p></td>
<td><p>0x8000000000080000</p></td>
<td><p>CanSetGlobalAccessLogMode</p></td>
<td><p><a href="#SetGlobalAccessLogMode" title="wikilink">#SetGlobalAccessLogMode</a></p></td>
</tr>
<tr class="odd">
<td><p>0x12</p></td>
<td><p>0x8000000000080000<br />
([1.0.0-5.1.0] Invalid)</p></td>
<td><p>CanSetSpeedEmulationMode</p></td>
<td><p>SetSpeedEmulationMode</p></td>
</tr>
<tr class="even">
<td><p>0x13</p></td>
<td><p>Invalid<br />
([1.0.0-5.1.0] 0xC000000000800000)</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>0x14</p></td>
<td><p>0xC000000000800000<br />
([1.0.0-5.1.0] 0xC000000001000000)</p></td>
<td><p>CanFillBis</p></td>
<td><p>CreatePaddingFile, DeleteAllPaddingFiles</p></td>
</tr>
<tr class="even">
<td><p>0x15</p></td>
<td><p>0xC000000001000000<br />
([5.0.0-5.1.0] 0x8000000001000060)<br />
([1.0.0-4.1.0] 0xC000000002000000)</p></td>
<td><p>CanCorruptSaveData</p></td>
<td><p>CorruptSaveDataFileSystem, CorruptSaveDataFileSystemBySaveDataSpaceId</p></td>
</tr>
<tr class="odd">
<td><p>[2.0.0+] 0x16</p></td>
<td><p>0x8000000001000060<br />
([5.0.0-5.1.0] 0x8000000000000060)<br />
([2.0.0-4.1.0] 0x8000000004000000)</p></td>
<td><p>CanCorruptSystemSaveData</p></td>
<td><p>CorruptSaveDataFileSystem, CorruptSaveDataFileSystemBySaveDataSpaceId</p></td>
</tr>
<tr class="even">
<td><p>[2.0.0+] 0x17</p></td>
<td><p>0x8000000000000060<br />
([5.0.0-5.1.0] 0xC000000002000000)<br />
([2.0.0-4.1.0] 0x8000000008000000)</p></td>
<td><p>CanVerifySaveData</p></td>
<td><p><a href="#VerifySaveDataFileSystem" title="wikilink">#VerifySaveDataFileSystem</a>, VerifySaveDataFileSystemBySaveDataSpaceId</p></td>
</tr>
<tr class="odd">
<td><p>[2.0.0+] 0x18</p></td>
<td><p>0xC000000002000000<br />
([5.0.0-5.1.0] 0x8000000004000000)<br />
([2.0.0-4.1.0] 0x8000000010000000)</p></td>
<td><p>CanDebugSaveData</p></td>
<td><p><a href="#CreateSaveDataFileSystem" title="wikilink">#CreateSaveDataFileSystem</a>, <a href="#OpenSaveDataFileSystem" title="wikilink">#OpenSaveDataFileSystem</a>, <a href="#SetSaveDataRootPath" title="wikilink">#SetSaveDataRootPath</a></p></td>
</tr>
<tr class="even">
<td><p>[2.0.0+] 0x19</p></td>
<td><p>0x8000000004000000<br />
([5.0.0-5.1.0] 0x8000000008000000)<br />
([2.0.0-4.1.0] 0x8000000000000800)</p></td>
<td><p>CanFormatSdCard</p></td>
<td><p>FormatSdCardFileSystem</p></td>
</tr>
<tr class="odd">
<td><p>[2.0.0+] 0x1A</p></td>
<td><p>0x8000000008000000<br />
([5.0.0-5.1.0] 0x8000000010000000)<br />
([2.0.0-4.1.0] 0x8000000000004020)</p></td>
<td><p>CanGetRightsId</p></td>
<td><p>GetRightsId, GetRightsIdAndKeyGenerationByPath, GetRightsIdByPath</p></td>
</tr>
<tr class="even">
<td><p>[3.0.0+] 0x1B</p></td>
<td><p>0x8000000010000000<br />
([5.0.0-5.1.0] 0x8000000000000800)<br />
([3.0.0-4.1.0] 0x8000000000002020)</p></td>
<td><p>CanRegisterExternalKey</p></td>
<td><p>RegisterExternalKey, UnregisterAllExternalKey</p></td>
</tr>
<tr class="odd">
<td><p>[3.0.0+] 0x1C</p></td>
<td><p>0x8000000000000800<br />
([5.0.0-5.1.0] 0x8000000000004020)<br />
([3.0.0-4.1.0] 0x8000000000000028)</p></td>
<td><p>CanSetEncryptionSeed</p></td>
<td><p><a href="#SetSdCardEncryptionSeed" title="wikilink">#SetSdCardEncryptionSeed</a></p></td>
</tr>
<tr class="even">
<td><p>[4.0.0+] 0x1D</p></td>
<td><p>0x8000000000000020<br />
([5.0.0-5.1.0] 0x8000000000000000)<br />
([4.0.0-4.1.0] 0x8000000020000000)</p></td>
<td><p>CanWriteSaveDataFileSystemExtraDataTimeStamp</p></td>
<td><p>WriteSaveDataFileSystemExtraData, WriteSaveDataFileSystemExtraDataWithMask</p></td>
</tr>
<tr class="odd">
<td><p>[4.0.0+] 0x1E</p></td>
<td><p>0x8000000000004020<br />
([5.0.0-5.1.0] 0x8000000000002020)<br />
([4.0.0-4.1.0] 0x8000000040000000)</p></td>
<td><p>CanWriteSaveDataFileSystemExtraDataFlags</p></td>
<td><p>WriteSaveDataFileSystemExtraData, WriteSaveDataFileSystemExtraDataWithMask</p></td>
</tr>
<tr class="even">
<td><p>[4.0.0+] 0x1F</p></td>
<td><p>0x8000000000000020<br />
([5.0.0-5.1.0] 0x8000000000000028)<br />
([4.0.0-4.1.0] 0x8000000000000000)</p></td>
<td><p>CanWriteSaveDataFileSystemExtraDataCommitId</p></td>
<td><p>WriteSaveDataFileSystemExtraData, WriteSaveDataFileSystemExtraDataWithMask</p></td>
</tr>
<tr class="odd">
<td><p>[4.0.0+] 0x20</p></td>
<td><p>0x8000000000000000<br />
([5.0.0-5.1.0] 0x8000000020000000)<br />
([4.0.0-4.1.0] 0x8000000000000000)</p></td>
<td><p>CanWriteSaveDataFileSystemExtraDataAll</p></td>
<td><p>WriteSaveDataFileSystemExtraData, WriteSaveDataFileSystemExtraDataWithMask</p></td>
</tr>
<tr class="even">
<td><p>[5.0.0+] 0x21</p></td>
<td><p>0x8000000000002020<br />
([1.0.0-5.1.0] 0x8000000040000000)</p></td>
<td><p>CanExtendSaveData</p></td>
<td><p>ExtendSaveDataFileSystem</p></td>
</tr>
<tr class="odd">
<td><p>[5.0.0+] 0x22</p></td>
<td><p>0x8000000000000028<br />
([1.0.0-5.1.0] 0x0000000080000002)</p></td>
<td><p>CanExtendSystemSaveData</p></td>
<td><p>ExtendSaveDataFileSystem</p></td>
</tr>
<tr class="even">
<td><p>[5.0.0+] 0x23</p></td>
<td><p>0x8000000020000000<br />
([1.0.0-5.1.0] 0x8000000000000000)</p></td>
<td><p>CanRegisterUpdatePartition</p></td>
<td><p>RegisterUpdatePartition</p></td>
</tr>
<tr class="odd">
<td><p>[5.0.0+] 0x24</p></td>
<td><p>0x8000000040000000<br />
([1.0.0-5.1.0] 0x8000000000000000)</p></td>
<td><p>CanOpenSaveDataTransferManager</p></td>
<td><p><a href="#OpenSaveDataTransferManager" title="wikilink">#OpenSaveDataTransferManager</a></p></td>
</tr>
<tr class="even">
<td><p>[5.0.0+] 0x25</p></td>
<td><p>0x8000000200000000<br />
([1.0.0-5.1.0] 0x8000000080200000)</p></td>
<td><p>CanOpenSaveDataTransferManagerVersion2</p></td>
<td><p><a href="#OpenSaveDataTransferManagerVersion2" title="wikilink">#OpenSaveDataTransferManagerVersion2</a></p></td>
</tr>
<tr class="odd">
<td><p>[5.0.0+] 0x26</p></td>
<td><p>0x8000000200000000<br />
([6.0.0-8.1.0] 0x8000000200002000)<br />
([5.0.0-5.1.0] 0x8000000080000110)</p></td>
<td><p>CanOpenSaveDataTransferManagerForSaveDataRepair</p></td>
<td><p>OpenSaveDataTransferManagerForSaveDataRepair</p></td>
</tr>
<tr class="even">
<td><p>[5.0.0+] 0x27</p></td>
<td><p>0x8000000000000000<br />
([8.0.0-8.1.0] 0x8000000240002000)<br />
([6.0.0-7.0.1] 0x8000000200002000)<br />
([5.0.0-5.1.0] 0x8000000000100008)</p></td>
<td><p>CanOpenSaveDataTransferManagerForSaveDataRepairTool</p></td>
<td><p>OpenSaveDataTransferManagerForSaveDataRepair</p></td>
</tr>
<tr class="odd">
<td><p>[5.0.0+] 0x28</p></td>
<td><p>0x8000000200002000<br />
([6.0.0-8.1.0] 0x8000000000000000)<br />
([5.0.0-5.1.0] 0x8000000080010000)</p></td>
<td><p>CanOpenOpenSaveDataTransferProhibiter</p></td>
<td><p><a href="#OpenSaveDataTransferProhibiter" title="wikilink">#OpenSaveDataTransferProhibiter</a></p></td>
</tr>
<tr class="even">
<td><p>[5.0.0+] 0x29</p></td>
<td><p>0x8000000240002000<br />
([6.0.0-8.1.0] 0x8000000000000000)<br />
([5.0.0-5.1.0] 0x0000000080000001)</p></td>
<td><p>CanListAccessibleSaveDataOwnerId</p></td>
<td><p><a href="#ListAccessibleSaveDataOwnerId" title="wikilink">#ListAccessibleSaveDataOwnerId</a></p></td>
</tr>
<tr class="odd">
<td><p>[5.0.0+] 0x2A</p></td>
<td><p>0x8000000000000000<br />
([6.0.0-8.1.0] 0x8000000080200000)<br />
([5.0.0-5.1.0] 0x0000000080000001)</p></td>
<td><p>CanControlMmcPatrol</p></td>
<td><p>SuspendMmcPatrol, ResumeMmcPatrol</p></td>
</tr>
<tr class="even">
<td><p>[5.0.0+] 0x2B</p></td>
<td><p>0x8000000000000000<br />
([6.0.0-8.1.0] 0x8000000080000110)<br />
([5.0.0-5.1.0] 0x0000000080000001)</p></td>
<td><p>CanOverrideSaveDataTransferTokenSignVerificationKey</p></td>
<td><p>OverrideSaveDataTransferTokenSignVerificationKey</p></td>
</tr>
<tr class="odd">
<td><p>[5.0.0+] 0x2C</p></td>
<td><p>0x8000000080200000<br />
([6.0.0-8.1.0] 0x8000000000100008)<br />
([5.0.0-5.1.0] 0x0000000080000001)</p></td>
<td><p>CanOpenSdCardDetectionEventNotifier</p></td>
<td><p><a href="#OpenSdCardDetectionEventNotifier" title="wikilink">#OpenSdCardDetectionEventNotifier</a></p></td>
</tr>
<tr class="even">
<td><p>[5.0.0+] 0x2D</p></td>
<td><p>0x8000000080000110<br />
([6.0.0-8.1.0] 0x8000000000010000)<br />
([5.0.0-5.1.0] 0x0000000080000001)</p></td>
<td><p>CanOpenGameCardDetectionEventNotifier</p></td>
<td><p><a href="#OpenGameCardDetectionEventNotifier" title="wikilink">#OpenGameCardDetectionEventNotifier</a></p></td>
</tr>
<tr class="odd">
<td><p>[5.0.0+] 0x2E</p></td>
<td><p>0x8000000000100008<br />
([6.0.0-8.1.0] 0x8000000100000000)<br />
([5.0.0-5.1.0] 0x8000000040000000)</p></td>
<td><p>CanOpenSystemDataUpdateEventNotifier</p></td>
<td><p>OpenSystemDataUpdateEventNotifier</p></td>
</tr>
<tr class="even">
<td><p>[5.0.0+] 0x2F</p></td>
<td><p>0x8000000000010000<br />
([6.0.0-8.1.0] 0x8000000100000000)<br />
([5.0.0-5.1.0] 0x8000000080200000)</p></td>
<td><p>CanNotifySystemDataUpdateEvent</p></td>
<td><p>NotifySystemDataUpdateEvent</p></td>
</tr>
<tr class="odd">
<td><p>[5.1.0+] 0x30</p></td>
<td><p>0x8000000100000000<br />
([5.1.0-6.0.0] 0x8000000080080000)</p></td>
<td><p>CanOpenAccessFailureDetectionEventNotifier</p></td>
<td><p><a href="#OpenAccessFailureDetectionEventNotifier" title="wikilink">#OpenAccessFailureDetectionEventNotifier</a></p></td>
</tr>
<tr class="even">
<td><p>[6.0.0+] 0x31</p></td>
<td><p>0x8000000100000000</p></td>
<td><p>CanGetAccessFailureDetectionEvent</p></td>
<td><p>GetAccessFailureDetectionEvent</p></td>
</tr>
<tr class="odd">
<td><p>[6.0.0+] 0x32</p></td>
<td><p>0x8000000100000000</p></td>
<td><p>CanIsAccessFailureDetected</p></td>
<td><p>IsAccessFailureDetected</p></td>
</tr>
<tr class="even">
<td><p>[6.0.0+] 0x33</p></td>
<td><p>0x8000000100000000<br />
([6.0.0-8.1.0] 0x8000000040000000)</p></td>
<td><p>CanResolveAccessFailure</p></td>
<td><p>ResolveAccessFailure</p></td>
</tr>
<tr class="odd">
<td><p>[6.0.0+] 0x34</p></td>
<td><p>0x8000000100000000<br />
([6.0.0-8.1.0] 0x8000000200000020)</p></td>
<td><p>CanAbandonAccessFailure</p></td>
<td><p>AbandonAccessFailure</p></td>
</tr>
<tr class="even">
<td><p>[6.0.0+] 0x35</p></td>
<td><p>0x8000000040000000<br />
([6.0.0-8.1.0] 0x8000000000200000)</p></td>
<td><p>CanQuerySaveDataInternalStorageTotalSize</p></td>
<td><p>QuerySaveDataInternalStorageTotalSize</p></td>
</tr>
<tr class="odd">
<td><p>[6.0.0+] 0x36</p></td>
<td><p>0x8000000200000020<br />
([6.0.0-8.1.0] 0x4000000000000000)</p></td>
<td><p>CanGetSaveDataCommitId</p></td>
<td><p><a href="#GetSaveDataCommitId" title="wikilink">#GetSaveDataCommitId</a></p></td>
</tr>
<tr class="even">
<td><p>[6.0.0+] 0x37</p></td>
<td><p>0x8000000000200000<br />
([7.0.0-8.1.0] 0x8000000000000000)<br />
([6.0.0-6.2.0] 0x8000000000080000)</p></td>
<td><p>CanSetSdCardAccessibility</p></td>
<td><p>SetSdCardAccessibility</p></td>
</tr>
<tr class="odd">
<td><p>[6.0.0+] 0x38</p></td>
<td><p>0x4000000000000000<br />
([7.0.0-8.1.0] 0x8000000400000000)<br />
([6.0.0-6.2.0] 0x8000000000000000)</p></td>
<td><p>CanSimulateDevice</p></td>
<td><p>SimulateDeviceDetectionEvent, SetSimulationEvent, ClearSimulationEvent</p></td>
</tr>
<tr class="even">
<td><p>[8.0.0+] 0x39</p></td>
<td><p>0x8000000000000000<br />
([8.0.0-8.1.0] 0x8000000000000010)</p></td>
<td><p>CanCreateSaveDataWithHashSalt</p></td>
<td><p><a href="#CreateSaveDataFileSystem" title="wikilink">#CreateSaveDataFileSystem</a>, <a href="#CreateSaveDataFileSystemWithHashSalt" title="wikilink">#CreateSaveDataFileSystemWithHashSalt</a></p></td>
</tr>
<tr class="odd">
<td><p>[9.0.0+] 0x3A</p></td>
<td><p>0x8000000400000000</p></td>
<td><p>CanRegisterProgramIndexMapInfo</p></td>
<td><p>RegisterProgramIndexMapInfo</p></td>
</tr>
<tr class="even">
<td><p>[9.0.0+] 0x3B</p></td>
<td><p>0x8000000000000010</p></td>
<td><p>CanChallengeCardExistence</p></td>
<td><p>ChallengeCardExistence</p></td>
</tr>
<tr class="odd">
<td><p>[9.0.0+] 0x3C</p></td>
<td><p>0x8000000800000000</p></td>
<td><p>CanCreateOwnSaveData</p></td>
<td><p><a href="#CreateSaveDataFileSystem" title="wikilink">#CreateSaveDataFileSystem</a>, CreateSaveDataFileSystemWithHashSalt</p></td>
</tr>
<tr class="even">
<td><p>[9.0.0+] 0x3D</p></td>
<td><p>0x8000000800000000</p></td>
<td><p>CanReadOwnSaveDataFileSystemExtraData</p></td>
<td><p><a href="#ReadSaveDataFileSystemExtraData" title="wikilink">#ReadSaveDataFileSystemExtraData</a></p></td>
</tr>
<tr class="odd">
<td><p>[9.0.0+] 0x3E</p></td>
<td><p>0x8000000800000000</p></td>
<td><p>CanExtendOwnSaveData</p></td>
<td><p>ExtendSaveDataFileSystem</p></td>
</tr>
<tr class="even">
<td><p>[9.0.0+] 0x3F</p></td>
<td><p>0x8000000800000000</p></td>
<td><p>CanOpenOwnSaveDataTransferProhibiter</p></td>
<td><p><a href="#OpenSaveDataTransferProhibiter" title="wikilink">#OpenSaveDataTransferProhibiter</a></p></td>
</tr>
<tr class="odd">
<td><p>[9.0.0+] 0x40</p></td>
<td><p>0x8000000800000000</p></td>
<td><p>CanFindOwnSaveDataWithFilter</p></td>
<td><p><a href="#FindSaveDataWithFilter" title="wikilink">#FindSaveDataWithFilter</a></p></td>
</tr>
</tbody>
</table>

## OpenFileSystem

Takes a type-0x19 input buffer (ContentPath) and a
[\#FileSystemType](#FileSystemType "wikilink") as parameters. Returns an
[\#IFileSystem](#IFileSystem "wikilink").

\[2.0.0+\] This function was removed.

## SetCurrentProcess

Takes a pid-descriptor.

## OpenFileSystemWithPatch

Takes an input [\#FileSystemType](#FileSystemType "wikilink") and an u64
title-id. Returns an [\#IFileSystem](#IFileSystem "wikilink").

Web-applet loads the [\#FileSystemType](#FileSystemType "wikilink")
(which must be **ContentManual**) from u32\_table\[inparam\].

Note: web-applet strings refer to both this cmd and
[\#OpenFileSystemWithId](#OpenFileSystemWithId "wikilink") as
"MountContent", but official nn\_sf\_sync symbols use "OpenXX" names.

## OpenFileSystemWithId

Takes a type-0x19 input buffer, an
[\#FileSystemType](#FileSystemType "wikilink") and an u64 title-id.
Returns an [\#IFileSystem](#IFileSystem "wikilink").

The [\#IFileSystem](#IFileSystem "wikilink") must be **ContentMeta** if
the NCA type is 0 (control).

The input buffer is the output string path from
[GetApplicationContentPath](NS%20Services#GetApplicationContentPath.md##GetApplicationContentPath "wikilink").

May return errors when attempting to access NCA-paths for an
update-title with a gamecard, when the gamecard isn't inserted. May
return error 0x7D402 in some cases with update-titles. Non-val2 in32
values with NCA-type1 are unusable, even for normal titles.

The official "MountApplicationPackage" func uses this with in64=0 and
[\#FileSystemType](#FileSystemType "wikilink") **ApplicationPackage**.

After the [\#FileSystemType](#FileSystemType "wikilink") specific
permissions are checked, it then gets the func retval for
permissions-type 0x25 and func0.

When [\#FileSystemType](#FileSystemType "wikilink") is **ContentMeta**,
it uses in64=0xffffffffffffffff internally, otherwise it checks if in64
is set to 0xffffffffffffffff then throws an error if so. When the in64
used internally is not 0xffffffffffffffff, it's compared with the NCA
titleID, then an error is thrown on mismatch.

## OpenBisFileSystem

Takes a type-0x19 input buffer string and a u32 [Bis
partitionID](Flash%20Filesystem.md "wikilink"). Official user-process
code sets instr\[0\] = 0 normally. Returns an
[\#IFileSystem](#IFileSystem "wikilink").

Only partitionIDs for FAT partitions are usable with this, otherwise
error 0x2EE202 is returned. Seems to be about the same as
[\#OpenBisStorage](#OpenBisStorage "wikilink") except this mounts the
partition filesystem instead of allowing direct access to the partition
sectors.

## OpenBisStorage

Takes a u32 partition ID, returns 0x2EE202 for partitions which do not
exist, 0x320002 for partitions which cannot be opened and a valid
[\#IStorage](#IStorage "wikilink") handle otherwise.

## InvalidateBisCache

Seems to invalidate the Bis cache for MBR/GPT after overwriting that
data via the OpenBisStorage IStorage. Used by
[SystemInitializer](SystemInitializer.md "wikilink").

## DeleteSaveDataFileSystem

Takes an input u64.

## CreateSaveDataFileSystem

Takes a 0x40-byte Save-struct entry, a 0x40-byte SaveCreate-struct
entry, and a 0x10-byte input struct.

Only the first 0x5-bytes in the 0x10-byte struct are initialized:
all-zero when automatically creating savedata during savecommon mount by
official user-processes. In the dedicated save-creation code in official
user-processes: +0 u32 = 0x40060, +4 u8 = 1.

Creates regular savedata.

## CreateSaveDataFileSystemBySystemSaveDataId

Takes a 0x40-byte Save-struct entry and a 0x40-byte SaveCreate-struct
entry.

Creates savedata in the SYSTEM [NAND](Flash%20Filesystem.md "wikilink")
partition.

## OpenGameCardStorage

Takes two input u32s (gamecard handle, partition ID), and returns an
[\#IStorage](#IStorage "wikilink") for the
[partition](Gamecard%20Format.md "wikilink").

## OpenGameCardFileSystem

Takes two input u32s, with the second u32 located at +4 in rawdata after
the first u32. Returns an [\#IFileSystem](#IFileSystem "wikilink").

Mounts a [gamecard partition](Gamecard%20Partition.md "wikilink").

## CreateSaveDataFileSystemWithHashSalt

Takes a total of 0xB0-bytes of input, no output.

## OpenSaveDataFileSystem

Takes an input u8 [\#SaveDataSpaceId](#SaveDataSpaceId "wikilink") and a
0x40-byte Save-struct entry. Official user-process code is only known to
use value 1 for the u8.

Returns an [\#IFileSystem](#IFileSystem "wikilink").

Permissions aren't checked until the specified save is successfully
found.

Only one process (specifically only one
[\#IFileSystem](#IFileSystem "wikilink") session) can mount a given
savedata at any given time (this includes SystemSaveData).

## OpenSaveDataFileSystemBySystemSaveDataId

Takes an input u8 [\#SaveDataSpaceId](#SaveDataSpaceId "wikilink") and a
0x40-byte Save-struct entry. Web-applet only uses value0 for the input
u8.

Returns an [\#IFileSystem](#IFileSystem "wikilink").

Mounts savedata in the SYSTEM [NAND](Flash%20Filesystem.md "wikilink")
partition.

## ReadSaveDataFileSystemExtraDataBySaveDataSpaceId

Takes an input u8 [\#SaveDataSpaceId](#SaveDataSpaceId "wikilink"), an
input u64 saveID, and a type-0x6 output buffer containing the
[\#SaveDataFileSystemExtraData](#SaveDataFileSystemExtraData "wikilink").

## ReadSaveDataFileSystemExtraData

Takes an input u64 saveID and a type-0x6 output buffer containing the
[\#SaveDataFileSystemExtraData](#SaveDataFileSystemExtraData "wikilink").

## OpenSaveDataInfoReader

No input, returns an output
[\#ISaveDataInfoReader](#ISaveDataInfoReader "wikilink").

## OpenSaveDataInfoReaderBySaveDataSpaceId

Takes an input u8 [\#SaveDataSpaceId](#SaveDataSpaceId "wikilink"),
returns an output
[\#ISaveDataInfoReader](#ISaveDataInfoReader "wikilink").

## FindSaveDataWithFilter

Takes a total of 0x50-bytes of input, returns 8-bytes of output and a
type-0x6 output buffer.

## OpenSaveDataInfoReaderWithFilter

Takes a total of 0x50-bytes of input, returns an
[\#ISaveDataInfoReader](#ISaveDataInfoReader "wikilink").

## OpenSaveDataTransferManager

No input, returns an
[\#ISaveDataTransferManager](#ISaveDataTransferManager "wikilink").

## OpenSaveDataTransferManagerVersion2

No input, returns an
[\#ISaveDataTransferManagerWithDivision](#ISaveDataTransferManagerWithDivision "wikilink").

## OpenSaveDataTransferProhibiter

Takes an input u64, returns an
[\#ISaveDataTransferProhibiter](#ISaveDataTransferProhibiter "wikilink").

## ListAccessibleSaveDataOwnerId

Takes a total of 0x10-bytes of input, returns 4-bytes of output and a
type-0x6 output buffer.

## OpenSaveDataTransferManagerForSaveDataRepair

No input, returns an output
[\#ISaveDataTransferManagerForSaveDataRepair](#ISaveDataTransferManagerForSaveDataRepair "wikilink").

## OpenContentStorageFileSystem

Takes a [\#ContentStorageId](#ContentStorageId "wikilink"). Invalid
values return 0x2EE202.

Returns an [\#IFileSystem](#IFileSystem "wikilink") with NCA files. The
read data from these files is identical to the data read by
[NCM\_services\#ReadContentIdFile](NCM%20services#ReadContentIdFile.md##ReadContentIdFile "wikilink").

## OpenCloudBackupWorkStorageFileSystem

Takes 4-bytes of input, returns an
[\#IFileSystem](#IFileSystem "wikilink").

## OpenCustomStorageFileSystem

Takes a [\#CustomStorageId](#CustomStorageId "wikilink"). Invalid values
return 0x2EE202.

Returns an [\#IFileSystem](#IFileSystem "wikilink") from either
User:/CustomStorage0 or Sdcard:/Nintendo/CustomStorage0. If on the SD
card, an AesXtsFileSystem is created using a key source specifically for
custom storage.

## OpenDataStorageByDataId

Takes a [\#StorageId](#StorageId "wikilink") and a TitleID.

Returns a [domain object
ID](IPC%20Marshalling#Domain%20message.md##Domain_message "wikilink")
implementing the [\#IStorage](#IStorage "wikilink") interface for data
archives.

## OpenDataFileSystemWithProgramIndex

Takes an input u8, returns an [\#IFileSystem](#IFileSystem "wikilink").

## OpenDataStorageWithProgramIndex

Takes an input u8, returns an [\#IStorage](#IStorage "wikilink").

## OpenDeviceOperator

This command returns a session to a port implementing the
[\#IDeviceOperator](#IDeviceOperator "wikilink") interface.

## OpenSdCardDetectionEventNotifier

This command returns a session to a port implementing the
[\#IEventNotifier](#IEventNotifier "wikilink") interface.

## OpenGameCardDetectionEventNotifier

This command returns a session to a port implementing the
[\#IEventNotifier](#IEventNotifier "wikilink") interface.

## SimulateDeviceDetectionEvent

Takes a total of 0xC-bytes of input, no output.

## VerifySaveDataFileSystem

Takes an unknown input u64 and a type-0x6 output buffer.

The input u64 high-byte must be non-zero, otherwise an
[error](Error%20codes.md "wikilink") is returned(0xE02).

## GetSaveDataCommitId

Takes an input u8 and u64, returns an output u64.

## SetSdCardEncryptionSeed

Takes in the 0x10 byte SD card encryption seed, and loads it into
FS-module state.

[NS](NS%20Services.md "wikilink")-module reads the 0x10 bytes from
SdCard:/Nintendo/Contents/private, and compares them to the first 0x10
bytes of the ns\_appman:/private (in [system
savedata](Flash%20Filesystem#System%20Savegames.md##System_Savegames "wikilink")
0x8000000000000043). If they match, NS calls this command using bytes
0x10-0x20 from ns\_appman:/private. The rest of this file (0x1F0 bytes
total) is (usually/always?) all-zero (however in some cases the byte at
offset 0x20 is value 0x1).

## OpenAccessFailureDetectionEventNotifier

Takes 8-bytes of input and returns an
[\#IEventNotifier](#IEventNotifier "wikilink").

\[8.0.0+\] Now takes an additional 8-bytes of input.

## SetSaveDataSize

Takes two input u64s "size" and "journal\_size", and writes them to
fsp-srv object member variables.

These variables are normally initialized with 32 MiB (0x2000000) and 16
MiB (0x1000000), respectively.

These variables don't seem to be actually used anywhere else (?)

## SetSaveDataRootPath

Takes an input path, and does
snprintf(<fsp-srv object>-\>m\_save\_data\_root\_path, FS\_MAX\_PATH-1,
"/%s", input\_path);

This path is normally all-zero. When this path is non-zero, the internal
OpenSaveDataFileSystem function will create a
DirectorySaveDataFileSystem if the target save is a user-save + a
directory exists, instead of the normal savedata filesystem object.

## SetGlobalAccessLogMode

Takes an input u32.

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

## GetProgramIndexForAccessLog

No input, returns two 32-bit values "version" and "program\_index".

## OpenMultiCommitManager

No input, returns an output
[\#IMultiCommitManager](#IMultiCommitManager "wikilink").

# IStorage

This is "nn::fssrv::sf::IStorage".

This is the interface for a raw device, usually a block device.

| Cmd | Name                             |
| --- | -------------------------------- |
| 0   | [\#Read](#Read "wikilink")       |
| 1   | [\#Write](#Write "wikilink")     |
| 2   | [\#Flush](#Flush "wikilink")     |
| 3   | [\#SetSize](#SetSize "wikilink") |
| 4   | [\#GetSize](#GetSize "wikilink") |
| 5   | \[4.0.0+\] OperateRange          |

## Read

Takes a type-0x46 buffer, an offset and length.

## Write

Takes a type-0x45 buffer, an offset and length.

## Flush

No input.

## SetSize

Takes a size.

## GetSize

Returns a size.

# IFileSystem

This is "nn::fssrv::sf::IFileSystem".

There are two main implementations of this interface:

  - **RomFS**: Filesystem implementation statically linked in the
    binary. Uses an [\#IStorage](#IStorage "wikilink") interface as
    underlying raw device.
  - **IPC proxy**: Used for all non-RomFS filesystems. In this case,
    actual filesystem implementation is in the FS process.

| Cmd | Name                                                                            |
| --- | ------------------------------------------------------------------------------- |
| 0   | CreateFile                                                                      |
| 1   | DeleteFile                                                                      |
| 2   | CreateDirectory                                                                 |
| 3   | DeleteDirectory                                                                 |
| 4   | DeleteDirectoryRecursively                                                      |
| 5   | RenameFile                                                                      |
| 6   | RenameDirectory                                                                 |
| 7   | [\#GetEntryType](#GetEntryType "wikilink")                                      |
| 8   | [\#OpenFile](#OpenFile "wikilink")                                              |
| 9   | [\#OpenDirectory](#OpenDirectory "wikilink")                                    |
| 10  | [\#Commit](#Commit "wikilink")                                                  |
| 11  | [\#GetFreeSpaceSize](#GetFreeSpaceSize "wikilink")                              |
| 12  | [\#GetTotalSpaceSize](#GetTotalSpaceSize "wikilink")                            |
| 13  | \[3.0.0+\] [\#CleanDirectoryRecursively](#CleanDirectoryRecursively "wikilink") |
| 14  | \[3.0.0+\] [\#GetFileTimeStampRaw](#GetFileTimeStampRaw "wikilink")             |
| 15  | \[4.0.0+\] QueryEntry                                                           |

## GetEntryType

Takes a type-0x9 input buffer for the path and returns
[\#DirectoryEntryType](#DirectoryEntryType "wikilink") as an output u32.

## OpenFile

Takes a type-0x19 input buffer for the path, and an u32 **mode**.
**mode** controls how the file is opened, based on which bits are set:

  - When bit 0 is set, the file is Readable: you can use the Read
    operation.
  - When bit 1 is set, the file is Writable: you can use the Write
    operation.
  - When bit 2 is set, the file is Appendable: unless this bit is set,
    you will not be able to write beyond the end of a file (such writes
    will result in an error 0x307202)

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

## CleanDirectoryRecursively

Takes a type-0x9 input buffer for the path and clears the contents of
the directory specified in the path.

## GetFileTimeStampRaw

Takes a type-0x19 input buffer for the path and returns a 0x20-byte
struct. This contains 3 u64s and an u8.

# IDirectory

This is "nn::fssrv::sf::IDirectory".

| Cmd | Name                                         |
| --- | -------------------------------------------- |
| 0   | [\#Read](#Read "wikilink")                   |
| 1   | [\#GetEntryCount](#GetEntryCount "wikilink") |

## Read

Takes a type-0x6 output buffer. Returns an output u64(?) for the total
number of read entries, this is 0 when no more entries are available.

The output buffer contains the read array of
[\#DirectoryEntry](#DirectoryEntry "wikilink"). This doesn't include
entries for "." and "..".

## GetEntryCount

Returns an u64 for the total number of readable entries.

# DirectoryEntry

This is "nn::fs::DirectoryEntry".

| Offset | Size  | Description                                                 |
| ------ | ----- | ----------------------------------------------------------- |
| 0x0    | 0x301 | Path                                                        |
| 0x301  | 0x1   | File attributes (bit 0 = is directory; bit 1 = archive bit) |
| 0x302  | 0x2   | Padding?                                                    |
| 0x304  | 0x1   | [\#DirectoryEntryType](#DirectoryEntryType "wikilink")      |
| 0x305  | 0x3   | Padding?                                                    |
| 0x308  | 0x8   | Filesize, 0 for directories.                                |

# DirectoryEntryType

This is "nn::fs::DirectoryEntryType".

An s8 value indicating a directory entry type. The current values are:

| Value | Description |
| ----- | ----------- |
| 0     | Directory   |
| 1     | File        |

# IFile

This is "nn::fssrv::sf::IFile".

| Cmd | Name                    |
| --- | ----------------------- |
| 0   | Read                    |
| 1   | Write                   |
| 2   | Flush                   |
| 3   | SetSize                 |
| 4   | GetSize                 |
| 5   | \[4.0.0+\] OperateRange |

# ISaveDataInfoReader

This is "nn::fssrv::sf::ISaveDataInfoReader".

| Cmd | Name                                               |
| --- | -------------------------------------------------- |
| 0   | [\#ReadSaveDataInfo](#ReadSaveDataInfo "wikilink") |

## ReadSaveDataInfo

Takes a type-0x6 output buffer. Returns an output u64 for total output
entries. This buffer contains an array of
[\#SaveDataInfo](#SaveDataInfo "wikilink").

This is used to get [\#SaveDataInfo](#SaveDataInfo "wikilink") for all
savedata on the system (or all savedata for the current
[\#SaveDataSpaceId](#SaveDataSpaceId "wikilink")). When used multiple
times, it will resume reading where it left off, until no more entries
are available (in that case the out u64 is value 0).

# IDeviceOperator

This is "nn::fssrv::sf::IDeviceOperator".

| Cmd | Name                                                                              |
| --- | --------------------------------------------------------------------------------- |
| 0   | IsSdCardInserted                                                                  |
| 1   | GetSdCardSpeedMode                                                                |
| 2   | \[2.0.0+\] GetSdCardCid                                                           |
| 3   | \[2.0.0+\] GetSdCardUserAreaSize                                                  |
| 4   | \[2.0.0+\] GetSdCardProtectedAreaSize                                             |
| 5   | \[2.0.0+\] GetAndClearSdCardErrorInfo                                             |
| 100 | GetMmcCid                                                                         |
| 101 | GetMmcSpeedMode                                                                   |
| 110 | EraseMmc                                                                          |
| 111 | GetMmcPartitionSize                                                               |
| 112 | \[2.0.0+\] GetMmcPatrolCount                                                      |
| 113 | \[2.0.0+\] GetAndClearMmcErrorInfo                                                |
| 114 | \[2.0.0+\] GetMmcExtendedCsd                                                      |
| 115 | \[4.0.0+\] SuspendMmcPatrol                                                       |
| 116 | \[4.0.0+\] ResumeMmcPatrol                                                        |
| 200 | IsGameCardInserted                                                                |
| 201 | EraseGameCard                                                                     |
| 202 | GetGameCardHandle                                                                 |
| 203 | [\#GetGameCardUpdatePartitionInfo](#GetGameCardUpdatePartitionInfo "wikilink")    |
| 204 | FinalizeGameCardDriver                                                            |
| 205 | GetGameCardAttribute                                                              |
| 206 | GetGameCardDeviceCertificate                                                      |
| 207 | GetGameCardAsicInfo                                                               |
| 208 | GetGameCardIdSet                                                                  |
| 209 | WriteToGameCardDirectly                                                           |
| 210 | SetVerifyWriteEnalbleFlag                                                         |
| 211 | GetGameCardImageHash                                                              |
| 212 | \[2.0.0+\] GetGameCardDeviceIdForProdCard                                         |
| 213 | \[2.0.0+\] EraseAndWriteParamDirectly                                             |
| 214 | \[2.0.0+\] ReadParamDirectly                                                      |
| 215 | \[2.0.0+\] ForceEraseGameCard                                                     |
| 216 | \[2.0.0+\] GetGameCardErrorInfo                                                   |
| 217 | \[2.1.0+\] GetGameCardErrorReportInfo                                             |
| 218 | \[3.0.0+\] GetGameCardDeviceId                                                    |
| 219 | \[8.0.0+\] ChallengeCardExistence                                                 |
| 220 | \[9.0.0+\] GetGameCardCompatibilityType                                           |
| 300 | SetSpeedEmulationMode                                                             |
| 301 | GetSpeedEmulationMode                                                             |
| 400 | \[5.0.0+\] SuspendSdmmcControl                                                    |
| 401 | \[5.0.0+\] ResumeSdmmcControl                                                     |
| 402 | \[6.0.0+\] [\#GetSdmmcConnectionStatus](#GetSdmmcConnectionStatus "wikilink")     |
| 500 | \[6.0.0+\] [\#SetDeviceSimulationEvent](#SetDeviceSimulationEvent "wikilink")     |
| 501 | \[6.0.0+\] [\#ClearDeviceSimulationEvent](#ClearDeviceSimulationEvent "wikilink") |

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

## GetSdmmcConnectionStatus

Takes a total of 4-bytes of input, returns a total of 8-bytes of output.

## SetDeviceSimulationEvent

Takes a total of 0x14-bytes of input, no output.

## ClearDeviceSimulationEvent

Takes a total of 4-bytes of input, no output.

# IEventNotifier

This is "nn::fssrv::sf::IEventNotifier".

| Cmd | Name                                           |
| --- | ---------------------------------------------- |
| 0   | [\#GetEventHandle](#GetEventHandle "wikilink") |

## GetEventHandle

No input, returns an output Event handle. With official sw the
EventClearMode is user-specified.

# ISaveDataTransferManager

This is "nn::fssrv::sf::ISaveDataTransferManager".

This was added with [4.0.0](4.0.0.md "wikilink").

| Cmd | Name                                                       |
| --- | ---------------------------------------------------------- |
| 0   | [\#GetChallenge](#GetChallenge "wikilink")                 |
| 16  | [\#SetToken](#SetToken "wikilink")                         |
| 32  | [\#OpenSaveDataExporter](#OpenSaveDataExporter "wikilink") |
| 64  | [\#OpenSaveDataImporter](#OpenSaveDataImporter "wikilink") |

## GetChallenge

No input/output, takes a type-0x6 output buffer.

## SetToken

No input/output, takes a type-0x5 input buffer.

## OpenSaveDataExporter

Takes an input u8 [\#SaveDataSpaceId](#SaveDataSpaceId "wikilink") and
u64, returns an [\#ISaveDataExporter](#ISaveDataExporter "wikilink").

## OpenSaveDataImporter

Takes an input u8 [\#SaveDataSpaceId](#SaveDataSpaceId "wikilink") and a
0x10-byte userID, and a type-0x5 input buffer. Returns an output u64 and
an [\#ISaveDataImporter](#ISaveDataImporter "wikilink").

# ISaveDataTransferManagerForSaveDataRepair

This is "nn::fssrv::sf::ISaveDataTransferManagerForSaveDataRepair".

This was added with [9.0.0](9.0.0.md "wikilink").

| Cmd | Name                                                                                           |
| --- | ---------------------------------------------------------------------------------------------- |
| 0   | [\#GetChallenge](#GetChallenge "wikilink")                                                     |
| 16  | [\#SetKeyPackage](#SetKeyPackage "wikilink")                                                   |
| 80  | [\#OpenSaveDataExporterAndGetEncryptedKey](#OpenSaveDataExporterAndGetEncryptedKey "wikilink") |
| 81  | [\#PrepareOpenSaveDataImporter](#PrepareOpenSaveDataImporter "wikilink")                       |
| 90  | [\#OpenSaveDataImporter](#OpenSaveDataImporter "wikilink")                                     |
| 91  | [\#OpenSaveDataImporter2](#OpenSaveDataImporter2 "wikilink")                                   |
| 100 | [\#OpenSaveDataExporterWithKey](#OpenSaveDataExporterWithKey "wikilink")                       |
| 110 | [\#OpenSaveDataImporterWithKey](#OpenSaveDataImporterWithKey "wikilink")                       |

## SetKeyPackage

No input/output, takes a type-0x5 input buffer.

## OpenSaveDataExporterAndGetEncryptedKey

Takes a total of 0x10-bytes of input and a type-0x1A output buffer to
receive a RsaEncryptedKey. Returns an
[\#ISaveDataDivisionExporter](#ISaveDataDivisionExporter "wikilink").

## PrepareOpenSaveDataImporter

Takes a type-0x1A output buffer to receive a RsaEncryptedKey.

## OpenSaveDataImporter

Takes a total of 0x18-bytes of input and two type-0x5 input buffers,
returns an
[\#ISaveDataDivisionImporter](#ISaveDataDivisionImporter "wikilink").

## OpenSaveDataImporter2

Takes a total of 0x18-bytes of input and a type-0x5 input buffer,
returns an
[\#ISaveDataDivisionImporter](#ISaveDataDivisionImporter "wikilink").

## OpenSaveDataExporterWithKey

Takes a total of 0x20-bytes of input, returns an
[\#ISaveDataDivisionExporter](#ISaveDataDivisionExporter "wikilink").

## OpenSaveDataImporterWithKey

Takes a total of 0x28-bytes of input and a type-0x5 input buffer,
returns an
[\#ISaveDataDivisionImporter](#ISaveDataDivisionImporter "wikilink").

# ISaveDataExporter

This is "nn::fssrv::sf::ISaveDataExporter".

This was added with [4.0.0](4.0.0.md "wikilink").

| Cmd | Name                                             |
| --- | ------------------------------------------------ |
| 0   | [\#GetSaveDataInfo](#GetSaveDataInfo "wikilink") |
| 1   | [\#GetRestSize](#GetRestSize "wikilink")         |
| 16  | [\#Pull](#Pull "wikilink")                       |
| 17  | [\#PullInitialData](#PullInitialData "wikilink") |

## GetSaveDataInfo

No input/output, takes a type-0x1A
[\#SaveDataInfo](#SaveDataInfo "wikilink") output buffer.

The actual name for this is the SaveDataExporter constructor. This is
used automatically after
[\#OpenSaveDataExporter](#OpenSaveDataExporter "wikilink") by official
sw.

## GetRestSize

No input, returns an output u64.

## Pull

Takes a type-0x6 output buffer, returns an output u64.

## PullInitialData

No input/output, takes a type-0x6 output buffer.

# ISaveDataImporter

This is "nn::fssrv::sf::ISaveDataImporter".

This was added with [4.0.0](4.0.0.md "wikilink").

| Cmd | Name                                             |
| --- | ------------------------------------------------ |
| 0   | [\#GetSaveDataInfo](#GetSaveDataInfo "wikilink") |
| 1   | [\#GetRestSize](#GetRestSize "wikilink")         |
| 16  | [\#Push](#Push "wikilink")                       |
| 17  | [\#Finalize](#Finalize "wikilink")               |

## GetSaveDataInfo

No input/output, takes a type-0x1A
[\#GetSaveDataInfo](#GetSaveDataInfo "wikilink") output buffer.

The actual name for this is the SaveDataImporter constructor. This is
used automatically after
[\#OpenSaveDataImporter](#OpenSaveDataImporter "wikilink") by official
sw.

## GetRestSize

No input, returns an output u64.

## Push

No input/output, takes a type-0x5 input buffer.

## Finalize

No input/output.

# ISaveDataTransferManagerWithDivision

This is "nn::fssrv::sf::ISaveDataTransferManagerWithDivision".

This was added with [5.0.0](5.0.0.md "wikilink").

| Cmd                                                                                       | Name                                                                                                              |
| ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| 0                                                                                         | [\#GetChallenge](#GetChallenge "wikilink")                                                                        |
| 16                                                                                        | [\#SetKeySeedPackage](#SetKeySeedPackage "wikilink")                                                              |
| 32                                                                                        | [\#OpenSaveDataExporter](#OpenSaveDataExporter "wikilink")                                                        |
| 33                                                                                        | [\#OpenSaveDataExporterForDiffExport](#OpenSaveDataExporterForDiffExport "wikilink")                              |
| 34                                                                                        | \[6.0.0+\] [\#OpenSaveDataExporterByContext](#OpenSaveDataExporterByContext "wikilink")                           |
| 64                                                                                        | \[5.0.0-5.1.0\] OpenSaveDataImporter                                                                              |
| \[6.0.0+\] [\#OpenSaveDataImporterDeprecated](#OpenSaveDataImporterDeprecated "wikilink") |                                                                                                                   |
| 65                                                                                        | [\#OpenSaveDataImporterForDiffImport](#OpenSaveDataImporterForDiffImport "wikilink")                              |
| 66                                                                                        | \[6.0.0+\] [\#OpenSaveDataImporterForDuplicateDiffImport](#OpenSaveDataImporterForDuplicateDiffImport "wikilink") |
| 67                                                                                        | \[6.0.0+\] [\#OpenSaveDataImporter](#OpenSaveDataImporter "wikilink")                                             |
| 68                                                                                        | \[6.0.0+\] [\#OpenSaveDataImporterByContext](#OpenSaveDataImporterByContext "wikilink")                           |
| 69                                                                                        | \[6.0.0+\] [\#CancelSuspendingImport](#CancelSuspendingImport "wikilink")                                         |

## GetChallenge

No input/output, takes a type-0x6 output buffer containing the
**Challenge**.

## SetKeySeedPackage

No input/output, takes a type-0x5 input buffer containing the
**KeySeedPackage**.

## OpenSaveDataExporter

Takes an input u8 [\#SaveDataSpaceId](#SaveDataSpaceId "wikilink") and
u64. Returns an
[\#ISaveDataDivisionExporter](#ISaveDataDivisionExporter "wikilink").

## OpenSaveDataExporterForDiffExport

Takes an input u8 [\#SaveDataSpaceId](#SaveDataSpaceId "wikilink"), an
u64, and a type-0x5 input buffer
[\#InitialDataVersion2](#InitialDataVersion2 "wikilink"). Returns an
[\#ISaveDataDivisionExporter](#ISaveDataDivisionExporter "wikilink").

## OpenSaveDataExporterByContext

No input/output, takes a type-0x5 input buffer, returns an
[\#ISaveDataDivisionExporter](#ISaveDataDivisionExporter "wikilink").

## OpenSaveDataImporterDeprecated

Takes an input u8 [\#SaveDataSpaceId](#SaveDataSpaceId "wikilink"), a
0x10-byte userID, and a type-0x5 input buffer
[\#InitialDataVersion2](#InitialDataVersion2 "wikilink"). Returns an
[\#ISaveDataDivisionImporter](#ISaveDataDivisionImporter "wikilink").

## OpenSaveDataImporterForDiffImport

Takes an input u8 [\#SaveDataSpaceId](#SaveDataSpaceId "wikilink"), an
u64, and a type-0x5 input buffer
[\#InitialDataVersion2](#InitialDataVersion2 "wikilink"), returns an
[\#ISaveDataDivisionImporter](#ISaveDataDivisionImporter "wikilink").

## OpenSaveDataImporterForDuplicateDiffImport

Takes an input u8 and an u64, and a type-0x5 input buffer, returns an
[\#ISaveDataDivisionImporter](#ISaveDataDivisionImporter "wikilink").

## OpenSaveDataImporter

Takes an input u8, an u8(bool), a 0x10-byte struct, and a type-0x5 input
buffer, returns an
[\#ISaveDataDivisionImporter](#ISaveDataDivisionImporter "wikilink").

## OpenSaveDataImporterByContext

No input/output, takes a type-0x5 input buffer, returns an
[\#ISaveDataDivisionImporter](#ISaveDataDivisionImporter "wikilink").

## CancelSuspendingImport

Takes an input u64 and a 0x10-byte struct, no output.

# ISaveDataDivisionExporter

This is "nn::fssrv::sf::ISaveDataDivisionExporter".

This was added with [5.0.0](5.0.0.md "wikilink").

| Cmd | Name                                                                                      |
| --- | ----------------------------------------------------------------------------------------- |
| 0   | [\#SetDivisionCount](#SetDivisionCount "wikilink")                                        |
| 1   | \[6.0.0+\] [\#GetSaveDataInfo](#GetSaveDataInfo "wikilink")                               |
| 16  | [\#OpenSaveDataDiffChunkIterator](#OpenSaveDataDiffChunkIterator "wikilink")              |
| 48  | [\#OpenSaveDataChunkExporter](#OpenSaveDataChunkExporter "wikilink")                      |
| 64  | \[6.0.0-8.1.0\] [\#FinalizeFullExport](#FinalizeFullExport "wikilink")                    |
| 65  | \[6.0.0-8.1.0\] [\#FinalizeDiffExport](#FinalizeDiffExport "wikilink")                    |
| 66  | \[6.0.0+\] [\#CancelExport](#CancelExport "wikilink")                                     |
| 67  | \[6.0.0+\] [\#SuspendExport](#SuspendExport "wikilink")                                   |
| 70  | \[6.0.0+\] [\#GetKeySeed](#GetKeySeed "wikilink")                                         |
| 71  | \[6.0.0+\] [\#GetInitialDataMac](#GetInitialDataMac "wikilink")                           |
| 72  | \[6.0.0+\] [\#FinalizeExport](#FinalizeExport "wikilink")                                 |
| 73  | \[9.0.0+\] [\#GetInitialDataMacKeyGeneration](#GetInitialDataMacKeyGeneration "wikilink") |
| 80  | \[6.0.0+\] [\#GetImportInitialDataAad](#GetImportInitialDataAad "wikilink")               |
| 81  | \[6.0.0+\] [\#SetExportInitialDataAad](#SetExportInitialDataAad "wikilink")               |
| 96  | \[6.0.0+\] [\#GetReportInfo](#GetReportInfo "wikilink")                                   |

## SetDivisionCount

Takes an input u32, no output.

## OpenSaveDataChunkExporter

Takes an input u32, returns an
[\#ISaveDataChunkExporter](#ISaveDataChunkExporter "wikilink").

## FinalizeFullExport

No input, returns two 0x10-byte output structs.

## FinalizeDiffExport

No input, returns an output 0x10-byte struct.

## CancelExport

No input/output.

## SuspendExport

No input/output, takes a type-0x6 output buffer.

## GetKeySeed

No input, returns an output 0x10-byte struct.

## GetInitialDataMac

No input, returns an output 0x10-byte struct.

## FinalizeExport

No input/output.

## SetExportInitialDataAad

Takes an input 0x20-byte struct, no output.

# ISaveDataDivisionImporter

This is "nn::fssrv::sf::ISaveDataDivisionImporter".

This was added with [5.0.0](5.0.0.md "wikilink").

| Cmd | Name                                                                         |
| --- | ---------------------------------------------------------------------------- |
| 0   | \[6.0.0+\] [\#GetSaveDataInfo](#GetSaveDataInfo "wikilink")                  |
| 16  | [\#OpenSaveDataDiffChunkIterator](#OpenSaveDataDiffChunkIterator "wikilink") |
| 32  | [\#InitializeImport](#InitializeImport "wikilink")                           |
| 33  | [\#FinalizeImport](#FinalizeImport "wikilink")                               |
| 34  | \[6.0.0+\] [\#CancelImport](#CancelImport "wikilink")                        |
| 35  | \[6.0.0+\] [\#GetImportContext](#GetImportContext "wikilink")                |
| 36  | \[6.0.0+\] [\#SuspendImport](#SuspendImport "wikilink")                      |
| 48  | [\#OpenSaveDataChunkImporter](#OpenSaveDataChunkImporter "wikilink")         |
| 64  | \[6.0.0+\] [\#GetImportInitialDataAad](#GetImportInitialDataAad "wikilink")  |
| 80  | \[6.0.0+\] [\#GetReportInfo](#GetReportInfo "wikilink")                      |

## GetSaveDataInfo

No input/output, takes a type-0x6 output buffer.

## OpenSaveDataDiffChunkIterator

No input, returns an
[\#ISaveDataChunkIterator](#ISaveDataChunkIterator "wikilink").

## InitializeImport

No input, returns an output u64.

## FinalizeImport

No input/output.

## CancelImport

No input/output.

## GetImportContext

No input/output, takes a type-0x6 output buffer.

## SuspendImport

No input/output.

## OpenSaveDataChunkImporter

Takes an input u32, returns an
[\#ISaveDataChunkImporter](#ISaveDataChunkImporter "wikilink").

## GetImportInitialDataAad

No input, returns an output 0x20-byte struct.

## GetReportInfo

No input, returns an output 0x20-byte struct.

# ISaveDataChunkIterator

This is "nn::fssrv::sf::ISaveDataChunkIterator".

This was added with [5.0.0](5.0.0.md "wikilink").

| Cmd | Name                         |
| --- | ---------------------------- |
| 0   | [\#Next](#Next "wikilink")   |
| 1   | [\#IsEnd](#IsEnd "wikilink") |
| 16  | [\#GetId](#GetId "wikilink") |

## Next

No input/output.

## IsEnd

No input, returns an output u8.

## GetId

No input, returns an output u32.

# ISaveDataChunkExporter

This is "nn::fssrv::sf::ISaveDataChunkExporter".

This was added with [5.0.0](5.0.0.md "wikilink").

| Cmd | Name                                                              |
| --- | ----------------------------------------------------------------- |
| 0   | [\#Pull](#Pull "wikilink")                                        |
| 16  | \[6.0.0+\] [\#GetRestRawDataSize](#GetRestRawDataSize "wikilink") |

## Pull

Takes an input u64 and a type-0x6 output buffer, returns an output u64.

## GetRestRawDataSize

No input, returns an output u64.

# ISaveDataChunkImporter

This is "nn::fssrv::sf::ISaveDataChunkImporter".

This was added with [5.0.0](5.0.0.md "wikilink").

| Cmd | Name                       |
| --- | -------------------------- |
| 0   | [\#Push](#Push "wikilink") |

## Push

Takes an input u64 and a type-0x5 input buffer, no output.

# ISaveDataTransferProhibiter

This was added with [6.0.0](6.0.0.md "wikilink").

This doesn't seem to handle any commands (?).

# IMultiCommitManager

This was added with [6.0.0](6.0.0.md "wikilink").

| Cmd | Name                           |
| --- | ------------------------------ |
| 1   | [\#Add](#Add "wikilink")       |
| 2   | [\#Commit](#Commit "wikilink") |

## Add

Takes an input [\#IFilesystem](#IFilesystem "wikilink"), no output.

## Commit

No input/output.

# FileSystemType

| Value | Name               |
| ----- | ------------------ |
| 0     | Code               |
| 1     | Data               |
| 2     | Logo               |
| 3     | ContentControl     |
| 4     | ContentManual      |
| 5     | ContentMeta        |
| 6     | ContentData        |
| 7     | ApplicationPackage |
| 8     | RegisteredUpdate   |

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

This is "nn::fs::ContentStorageId".

| Value | Name   |
| ----- | ------ |
| 0     | System |
| 1     | User   |
| 2     | SdCard |

# SaveDataSpaceId

This is "nn::fs::SaveDataSpaceId".

| Value | Name                    |
| ----- | ----------------------- |
| 0     | System                  |
| 1     | User                    |
| 2     | SdSystem                |
| 100   | \[3.0.0+\] ProperSystem |

Determines the storage where the savedata is stored.

# SaveDataType

| Value | Name                        |
| ----- | --------------------------- |
| 0     | SystemSaveData              |
| 1     | SaveData                    |
| 2     | BcatDeliveryCacheStorage    |
| 3     | DeviceSaveData              |
| 4     | \[3.0.0+\] TemporaryStorage |
| 5     | \[3.0.0+\] CacheStorage     |

# ImageDirectoryId

This is "nn::fs::ImageDirectoryId".

| Value | Name   |
| ----- | ------ |
| 0     | Nand   |
| 1     | SdCard |

# CloudBackupWorkStorageId

This is "nn::fs::CloudBackupWorkStorageId".

| Value | Name   |
| ----- | ------ |
| 0     | Nand   |
| 1     | SdCard |

# CustomStorageId

This is "nn::fs::CustomStorageId".

| Value | Name   |
| ----- | ------ |
| 0     | Nand   |
| 1     | SdCard |

# ContentPath

These are the 0x300 paths to NCA files for the various filesystems FS
can access, beginning with @. They're passed via X descriptors, and
returned via various
[ncm/lr](Location%20Resolver%20services.md "wikilink") commands.

| Path                  | Notes                                                                                                                           |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| @SystemContent        |                                                                                                                                 |
| @UserContent          |                                                                                                                                 |
| @SdCardContent        |                                                                                                                                 |
| @CalibFile            |                                                                                                                                 |
| @Safe                 |                                                                                                                                 |
| @User                 |                                                                                                                                 |
| @System               |                                                                                                                                 |
| @Sdcard               |                                                                                                                                 |
| @Host                 |                                                                                                                                 |
| @GcApp                | Gamecard App partition (Partition 2)                                                                                            |
| @GcXYYYYYYYY          | Gamecard Contents. X is the partition type (U - Update, N - Normal, S - Secure). Y is the gamecard handle as a 32-bit hex value |
| @upp                  | Gamecard update partition (Partition 0)                                                                                         |
| \[4.0.0+\] @RegUpdate | Registered update partition                                                                                                     |

# Save Struct

This is "nn::fs::SaveDataAttribute".

| Offset | Size | Description                                                                                                                                                                                             |
| ------ | ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x8  | 0 for SystemSaveData. SaveData: 0 can be used for accessing the savedata associated with the current FS session titleID, otherwise when set this is the titleID associated with the savedata to access. |
| 0x8    | 0x10 | userID for user-specific savedata(saveuser) when set, otherwise when zero this indicates the common savedata(savecommon). This is loaded from [Account\_services](Account%20services.md "wikilink").    |
| 0x18   | 0x8  | u64 [saveID](Flash%20Filesystem.md "wikilink"). 0 for SaveData.                                                                                                                                         |
| 0x20   | 0x1  | [\#SaveDataType](#SaveDataType "wikilink")                                                                                                                                                              |
| 0x21   | 0x1  | Save data 'rank' or 'precedence'. 0 if this save data is considered the primary save data. 1 if it's considered the secondary save data.                                                                |
| 0x22   | 0x2  | Save data index                                                                                                                                                                                         |
| 0x24   | 0x4  | Padding                                                                                                                                                                                                 |
| 0x28   | 0x8  | 0 for SystemSaveData/SaveData.                                                                                                                                                                          |
| 0x30   | 0x8  | 0 for SystemSaveData/SaveData.                                                                                                                                                                          |
| 0x38   | 0x8  | 0 for SystemSaveData/SaveData.                                                                                                                                                                          |

Total size is 0x40-bytes.

For DeviceSaveData, this struct is all-zero except for the
[\#SaveDataType](#SaveDataType "wikilink") field.

# SaveCreate Struct

| Offset | Size | Description                                                                                                                                                                                                                                                                                                                           |
| ------ | ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x8  | Save data size.                                                                                                                                                                                                                                                                                                                       |
| 0x8    | 0x8  | Save data journal size.                                                                                                                                                                                                                                                                                                               |
| 0x10   | 0x8  | Save data block size. 0x4000 for SystemSaveData/SaveData/DeviceSaveData/BcatSaveData.                                                                                                                                                                                                                                                 |
| 0x18   | 0x8  | Save data owner id. Official user-processes only uses 0 here for SystemSaveData/SaveData. For the dedicated save-creation code with SaveData/DeviceSaveData, this value comes from an input param with official user-processes. For BcatSaveData, this is the hard-coded [titleID](Title%20list.md "wikilink") of the bcat-sysmodule. |
| 0x20   | 0x4  | Save data flags. Written using an input param for official user-processes. Hard-coded 0 for BcatSaveData.                                                                                                                                                                                                                             |
| 0x24   | 0x1  | [\#SaveDataSpaceId](#SaveDataSpaceId "wikilink"). Official user-processes only uses 0 here for SystemSaveData, 1 for SaveData/DeviceSaveData/BcatSaveData.                                                                                                                                                                            |
| 0x25   | 0x1  | Unknown. 0 for SystemSaveData/SaveData.                                                                                                                                                                                                                                                                                               |
| 0x26   | 0x1A | Not initialized for SystemSaveData/SaveData.                                                                                                                                                                                                                                                                                          |

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
[\#CreateSaveDataFileSystem](#CreateSaveDataFileSystem "wikilink") has
the first 0x5-bytes set to all-zero.

# SaveDataInfo

| Offset | Size | Description                                                                                                                              |
| ------ | ---- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x8  | Unknown saveID                                                                                                                           |
| 0x8    | 0x1  | [\#SaveDataSpaceId](#SaveDataSpaceId "wikilink")                                                                                         |
| 0x9    | 0x1  | [\#SaveDataType](#SaveDataType "wikilink")                                                                                               |
| 0xA    | 0x6  | Padding?                                                                                                                                 |
| 0x10   | 0x10 | userID                                                                                                                                   |
| 0x20   | 0x8  | saveID, 0 for regular SaveData.                                                                                                          |
| 0x28   | 0x8  | Application titleID, for regular SaveData.                                                                                               |
| 0x30   | 0x8  | Raw saveimage size                                                                                                                       |
| 0x38   | 0x2  | Save data index                                                                                                                          |
| 0x3A   | 0x1  | Save data 'rank' or 'precedence'. 0 if this save data is considered the primary save data. 1 if it's considered the secondary save data. |
| 0x3B   | 0x25 | Unknown. Usually zeros?                                                                                                                  |

This is a 0x60-byte struct.

# SaveDataFileSystemExtraData

This is a 0x200-byte struct. Appears to match
[Savegames\#Extra\_data](Savegames#Extra%20data.md##Extra_data "wikilink").

# InitialDataVersion2

This is a 0x8210-byte struct used by
[\#ISaveDataTransferManagerWithDivision](#ISaveDataTransferManagerWithDivision "wikilink").

[Category:Services](Category:Services "wikilink")

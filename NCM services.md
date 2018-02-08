NCM contains services for internal file path and content management.

# Location Resolver services

## lr

This is
"nn::lr::ILocationResolverManager".

| Cmd | Name                            | Arguments                                                             | Notes |
| --- | ------------------------------- | --------------------------------------------------------------------- | ----- |
| 0   | GetLocationResolver             | [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink") |       |
| 1   | GetRegisteredLocationResolver   | None                                                                  |       |
| 2   | CheckStorage                    | [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink") |       |
| 3   | GetAddOnContentLocationResolver | None                                                                  |       |

The only sysmodules which use this service are
[FS](Filesystem%20services.md "wikilink"),
[Loader](Loader%20services.md "wikilink"), and
[NS](NS%20Services.md "wikilink"). [boot2](Boot2.md "wikilink") has
access but doesn't use it.

### ILocationResolver

This is
"nn::lr::ILocationResolver".

| Cmd | Name                  | Arguments                                                                                          | Notes                                                                                                           |
| --- | --------------------- | -------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| 0   | GetProgramNcaPath     | u64 TID + C descriptor                                                                             | Used for [NCA-type1](NCA%20Content%20FS#NCA-type1.md##NCA-type1 "wikilink").                                    |
| 1   | SetProgramNcaPath     | u64 TID + X descriptor [ContentPath](Filesystem%20services#ContentPath.md##ContentPath "wikilink") | Used for [NCA-type1](NCA%20Content%20FS#NCA-type1.md##NCA-type1 "wikilink").                                    |
| 2   | GetUserControlNcaPath | u64 TID + C descriptor                                                                             | Used for [NCA-type3](NCA%20Content%20FS#NCA-type3.md##NCA-type3 "wikilink") (gamecard only?).                   |
| 3   | GetDocHtmlNcaPath     | u64 TID + C descriptor                                                                             | Used for [NCA-type4](NCA%20Content%20FS#NCA-type4.md##NCA-type4 "wikilink").                                    |
| 4   | GetControlNcaPath     | u64 TID + C descriptor                                                                             | Used for [NCA-type3](NCA%20Content%20FS#NCA-type3.md##NCA-type3 "wikilink"). Stubbed, only returns error 0x608. |
| 5   | SetControlNcaPath     | u64 TID + X descriptor [ContentPath](Filesystem%20services#ContentPath.md##ContentPath "wikilink") | Used for [NCA-type3](NCA%20Content%20FS#NCA-type3.md##NCA-type3 "wikilink").                                    |
| 6   | SetDocHtmlNcaPath     | u64 TID + X descriptor [ContentPath](Filesystem%20services#ContentPath.md##ContentPath "wikilink") | Used for [NCA-type4](NCA%20Content%20FS#NCA-type4.md##NCA-type4 "wikilink").                                    |
| 7   | GetInfoHtmlNcaPath    | u64 TID + C descriptor                                                                             | Used for [NCA-type5](NCA%20Content%20FS#NCA-type5.md##NCA-type5 "wikilink").                                    |
| 8   | SetInfoHtmlNcaPath    | u64 TID + X descriptor [ContentPath](Filesystem%20services#ContentPath.md##ContentPath "wikilink") | Used for [NCA-type5](NCA%20Content%20FS#NCA-type5.md##NCA-type5 "wikilink").                                    |
| 9   | ClearLocationResolver | None                                                                                               | Clears all NCA paths set.                                                                                       |

These get-commands load the
[ContentPath](Filesystem%20services.md "wikilink") from linked-lists in
memory using the input titleID. The set-commands add a new entry to the
list, if a matching entry is found it's removed first.
ClearLocationResolver frees all entries in all of these linked-lists.
The ContentPath is only used with memcpy() here with size=0x300, nothing
more.

The set commands always return 0. When the get-commands fail to find an
entry for the specified titleID, 0x408 is returned for
GetProgramNcaPath, while the rest of the commands return 0xA08.

### IRegisteredLocationResolver

This is
"nn::lr::IRegisteredLocationResolver".

| Cmd | Name                  | Arguments                                                                                          | Notes                                                                        |
| --- | --------------------- | -------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| 0   | GetPatchType0NcaPath  | u64 TID + C descriptor                                                                             | Used for [NCA-type1](NCA%20Content%20FS#NCA-type1.md##NCA-type1 "wikilink"). |
| 1   | SetPatchType0NcaPath  | u64 TID + X descriptor [ContentPath](Filesystem%20services#ContentPath.md##ContentPath "wikilink") |                                                                              |
| 2   | RegisterPatchTitle0   | u64 TID                                                                                            |                                                                              |
| 3   | SetPatchTitle0NcaPath | u64 TID + X descriptor [ContentPath](Filesystem%20services#ContentPath.md##ContentPath "wikilink") |                                                                              |
| 4   | GetPatchType1NcaPath  | u64 TID + C descriptor                                                                             |                                                                              |
| 5   | SetPatchType1NcaPath  | u64 TID + X descriptor [ContentPath](Filesystem%20services#ContentPath.md##ContentPath "wikilink") |                                                                              |
| 6   | RegisterPatchTitle1   | u64 TID                                                                                            |                                                                              |
| 7   | SetPatchTitle1NcaPath | u64 TID + X descriptor [ContentPath](Filesystem%20services#ContentPath.md##ContentPath "wikilink") |                                                                              |

### IAddOnContentLocationResolver

This is
"nn::lr::IAddOnContentLocationResolver".

| Cmd | Name                              | Arguments                                                                       | Notes                              |
| --- | --------------------------------- | ------------------------------------------------------------------------------- | ---------------------------------- |
| 0   | GetAddOnContentNcaPath            | u64 TID + C descriptor                                                          |                                    |
| 1   | RegisterAddOnContent              | [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink") + u64 TID |                                    |
| 2   | ClearAddOnContentLocationResolver | None                                                                            | Clears all registered titles here. |

# Content Manager services

## ncm

This is
"nn::ncm::IContentManager".

| Cmd | Name                                | Notes                                                                          |
| --- | ----------------------------------- | ------------------------------------------------------------------------------ |
| 0   | MountOrInitializeStorageForMediaId  |                                                                                |
| 1   | MountOrInitializeDatabaseForMediaId |                                                                                |
| 2   | GetStorageEntryTypeForMediaId       |                                                                                |
| 3   | GetDatabaseEntryTypeForMediaId      |                                                                                |
| 4   | GetIContentStorage                  | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink"). |
| 5   | GetIContentMetaDatabase             | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink"). |
| 8   | DeleteDatabaseForMediaId            |                                                                                |
| 9   | MountStorageForMediaId              |                                                                                |
| 10  | UnmountStorageForMediaId            |                                                                                |
| 11  | MountDatabaseForMediaId             |                                                                                |
| 12  | UnmountDatabaseForMediaId           |                                                                                |

All of the above cmds takes a u8 as input.

### IContentStorage

This is
"nn::ncm::IContentStorage".

| Cmd | Name                                                   | Notes                                                                                                                                                                     |
| --- | ------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0   | [\#GetRootEntry](#GetRootEntry "wikilink")             |                                                                                                                                                                           |
| 1   |                                                        | Takes two 0x10-sized entries, and a u64.                                                                                                                                  |
| 2   | DeletePlaceholderEntry                                 | Takes a 0x10-sized entry.                                                                                                                                                 |
| 3   | GetEntryType                                           | Takes a 0x10-sized entry, returns a bool/u8.                                                                                                                              |
| 4   | WritePlaceholderEntry                                  | Takes a [\#NcaID](#NcaID "wikilink"), a u64-offset, and type-5 array.                                                                                                     |
| 5   | MovePlaceholderToRegistered                            | Takes two 0x10-sized entries.                                                                                                                                             |
| 6   | DeleteContent?                                         | Takes a 0x10-sized entry.                                                                                                                                                 |
| 7   | IsNcaEntryValid                                        | Takes a [\#NcaID](#NcaID "wikilink"), returns a bool.                                                                                                                     |
| 8   | GetPath                                                | Takes a [\#NcaID](#NcaID "wikilink"). Returns a [Content Path](Filesystem%20services#ContentPath.md##ContentPath "wikilink").                                             |
| 9   | GetPlaceholderPath                                     | Takes a [\#NcaID](#NcaID "wikilink"). Returns a [Content Path](Filesystem%20services#ContentPath.md##ContentPath "wikilink").                                             |
| 10  | CleanPlaceholderDirectory                              | Deletes the Placeholder directory.                                                                                                                                        |
| 11  | GetPlaceholderEntries                                  | This is like [\#GetEntries](#GetEntries "wikilink"), but for the Placeholder directory.                                                                                   |
| 12  | [\#GetNumberOfEntries](#GetNumberOfEntries "wikilink") |                                                                                                                                                                           |
| 13  | [\#GetEntries](#GetEntries "wikilink")                 |                                                                                                                                                                           |
| 14  | [\#GetEntrySize](#GetEntrySize "wikilink")             |                                                                                                                                                                           |
| 15  | CloseStorage                                           | Closes/Flushes all resources for the storage, and causes all future IPC commands to the current session to return error 0xC805.                                           |
| 16  |                                                        | Takes three 0x10-sized entries.                                                                                                                                           |
| 17  | SetPlaceholderSize                                     | Takes a [\#NcaID](#NcaID "wikilink"), and a u64 size                                                                                                                      |
| 18  | [\#ReadEntryRaw](#ReadEntryRaw "wikilink")             |                                                                                                                                                                           |
| 19  | GetPlaceholderRightsID                                 | Gets the Rights ID for the [\#NcaID](#NcaID "wikilink")'s placeholder path.                                                                                               |
| 20  | GetRegisteredRightsID                                  | Gets the Rights ID for the [\#NcaID](#NcaID "wikilink")'s registered path                                                                                                 |
| 21  | WriteRegisteredPathForDebug                            | Takes a [\#NcaID](#NcaID "wikilink"), a u64 size, and a type 5 buffer. On debug units, writes the buffer to the NCA's registered path. On retail units, this just aborts. |
| 22  | GetFreeSpace                                           |                                                                                                                                                                           |
| 23  | GetTotalSpace                                          |                                                                                                                                                                           |

#### GetRootEntry

Returns an entry of 16 completely random-looking bytes. It is not
possible to read this entry.

Changes on reboot?

#### GetNumberOfEntries

Writes the total number of entries which can be read by GetEntries, to
cmdreply <SFCO_offset>+0x10.

#### GetEntries

Takes an output buffer, u32 offset and gets all entries starting at that
offset. Returns number of entries read.

Each entry is a [\#NcaID](#NcaID "wikilink").

The total read entries is exactly the same as the number of "<hex>.nca"
directories in the storage FS(or at least under the "registered"
directory?).

#### GetEntrySize

Takes a [\#NcaID](#NcaID "wikilink") as input.

Returns the total size readable by ReadEntryRaw. This is the same as the
size-field in the [NAX0](NAX0.md "wikilink") "<NcaID>.nca/00" file.

#### ReadEntryRaw

Takes an output buffer, a [\#NcaID](#NcaID "wikilink") as input, and a
u64 file offset.

Returns encrypted looking data from the content in the
[NAX0](NAX0.md "wikilink"). Doesn't match the encrypted raw data in the
[NAX0](NAX0.md "wikilink") "<NcaID>.nca/00" file. Seems to be at least
one crypto layer below the initial NAX0 layer, since the data doesn't
change after NAX0 recreation.

Manually modifying the content in the NAX0(starting at offset 0x4000)
results in different output data being returned by this cmd. Changing
any data within the first 0x10-bytes results in the entire 0x10-byte
block changing. Likewise for offset 0x4010 size 0x1, entire 0x10-byte
block at 0x4010 changes. Changing the first 0x20-bytes at 0x4000 to
zeros has the same combined changed output, as when offset 0x4000 size
0x10 and offset 0x4010 size 0x10 were changed to zeros separately.
Output BlockA and BlockB are completely different, where the raw NAX0
data for those blocks are all-zero.

Overwriting the entire raw NAX0 content with zeros results in output
data which doesn't seem to have any duplicate blocks/data. When changing
the previously mentioned raw content for the first 8 blocks to
last-block-byte = 1\<\<i, where i is 0-7, none of the changed output
blocks match any output blocks from the previously mentioned
output(all-zero raw content).

This implies that that an AES mode is being used which isn't CTR, where
changing data in one block doesn't affect other blocks.

See GetEntrySize for the total size readable with this.

### IContentMetaDatabase

This is
"nn::ncm::IContentMetaDatabase".

| Cmd | Name                                                   | Notes                                                                                                                         |
| --- | ------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------- |
| 0   | InsertContentEntry?                                    | Takes a 0x10-sized entry, a type-5 buffer and a u64.                                                                          |
| 1   |                                                        | Takes a 0x10-sized entry, a type-6 buffer and a u64. Returns a u64.                                                           |
| 2   |                                                        | Takes a 0x10-sized entry.                                                                                                     |
| 3   | UpdateContentEntry                                     | Takes a [meta record entry](NCA#Meta%20records.md##Meta_records "wikilink") and a u8. Returns a [\#NcaID](#NcaID "wikilink"). |
| 4   |                                                        | Takes a type-6 buffer, each entry being 24 bytes, 0x10-sized entry and a u32. Returns a u32.                                  |
| 5   | Iterate                                                | Takes a type-6 buffer, each entry being 16 bytes, a 0x10-sized entry, and a u32. Returns a u32.                               |
| 6   | [\#GetTitleIdInfo](#GetTitleIdInfo "wikilink")         |                                                                                                                               |
| 7   | [\#GetTitleList](#GetTitleList "wikilink")             | Takes a type-6 buffer, each entry being 24 bytes, and a u8/bool. Returns two u32's.                                           |
| 8   |                                                        | Takes a 0x10-sized entry. Returns a bool/u8.                                                                                  |
| 9   |                                                        | Takes a type-5 buffer, each entry being 16 bytes. Returns a bool/u8.                                                          |
| 10  |                                                        | Takes a 0x10-sized entry. Returns a u64.                                                                                      |
| 11  |                                                        | Takes a 0x10-sized entry. Returns a u32.                                                                                      |
| 12  |                                                        | Takes a 0x10-sized entry. Returns a u64.                                                                                      |
| 13  |                                                        | Void.                                                                                                                         |
| 14  |                                                        | Takes a type-6 byte buffer, and a type-5 buffer with each entry being 16 bytes.                                               |
| 15  | EndIteration                                           | Void.                                                                                                                         |
| 16  |                                                        | Takes two 0x10-sized entries. Returns a bool/u8.                                                                              |
| 17  | [\#GetUpdateTitleList](#GetUpdateTitleList "wikilink") |                                                                                                                               |
| 18  |                                                        | Takes a 0x10-sized entry. Returns a bool/u8.                                                                                  |
| 19  |                                                        | Takes a 0x10-sized entry. Returns a u32.                                                                                      |

#### GetTitleIdInfo

Takes a u64 title-id as input, returns same title-id together with info
struct.

`struct title_info {`  
`  u32  version;`  
`  u8   type;`  
`  u8   pad[3];`  
`};`

#### GetTitleList

Each 24-byte entries is as follows:

` u64    title_id_update;`  
` struct title_info info;`  
` u64    title_id;`

#### GetUpdateTitleList

Takes a type-6 output buffer, each entry being 0x10-byte bytes, a u32
entryoffset and a 0x10-sized entry. Returns a u32 for
total\_read\_entries.

The input entry is the output entry from
[\#GetTitleIdInfo](#GetTitleIdInfo "wikilink") starting at the TID. The
output 0x10-bytes entries are the same as the output from
[\#GetTitleIdInfo](#GetTitleIdInfo "wikilink") starting at the TID.
However, "pad\[0\]" is used for something else it seems?(0 for
everything except for TID
[010000000000081B](Title%20list.md "wikilink"), where it's 1)

See
[NCA\#Meta\_records](NCA#Meta%20records.md##Meta_records "wikilink").

This reads the titlelist stored in the specified title, normally a title
with title-type 3, which is sysupdate-title 0100000000000816. Returns 0
with total\_read\_entries=0 when used with other title(s).

### NcaID

This is a 0x10-byte entry. This is originally from the hex portion of
"<hex>.nca" directory-names from this storage FS(like
[SD](SD%20Filesystem.md "wikilink")).

The NcaID is the same as the first 0x10-bytes from the calculated SHA256
hash, from hashing the entire output from
ReadEntryRaw.

### Enums

#### Title Types

| Value | Description                                                                                                                                                                      |
| ----- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x01  | System Programs ([System Modules](Title%20list#System%20Modules.md##System_Modules "wikilink") or [System Applets](Title%20list#System%20Applets.md##System_Applets "wikilink")) |
| 0x02  | [System Data Archives](Title%20list#System%20Data%20Archives.md##System_Data_Archives "wikilink")                                                                                |
| 0x03  | System Update                                                                                                                                                                    |
| 0x04  | [Firmware package A](Title%20list.md "wikilink")                                                                                                                                 |
| 0x05  | [Firmware package B](Title%20list.md "wikilink")                                                                                                                                 |
| 0x80  | Regular application                                                                                                                                                              |
| 0x81  | Update title                                                                                                                                                                     |
| 0x82  | Add-on content                                                                                                                                                                   |
| 0x83  | Delta title                                                                                                                                                                      |
|       |                                                                                                                                                                                  |

## ncm:v

[Category:Services](Category:Services "wikilink")

NCM contains services for internal file path and content management.

# Location Resolver services

## lr

This is
"nn::lr::ILocationResolverManager".

| Cmd | Name                                       | Arguments                                                             | Notes |
| --- | ------------------------------------------ | --------------------------------------------------------------------- | ----- |
| 0   | GetLocationResolver                        | [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink") |       |
| 1   | GetRegisteredLocationResolver              | None                                                                  |       |
| 2   | CheckStorage                               | [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink") |       |
| 3   | \[2.0.0+\] GetAddOnContentLocationResolver | None                                                                  |       |

The only sysmodules which use this service are
[FS](Filesystem%20services.md "wikilink"),
[Loader](Loader%20services.md "wikilink"), and
[NS](NS%20Services.md "wikilink"). [boot2](Boot2.md "wikilink") has
access but doesn't use it.

### ILocationResolver

This is
"nn::lr::ILocationResolver".

| Cmd | Name                                                                      |
| --- | ------------------------------------------------------------------------- |
| 0   | [\#GetProgramNcaPath](#GetProgramNcaPath "wikilink")                      |
| 1   | [\#SetProgramNcaPath](#SetProgramNcaPath "wikilink")                      |
| 2   | [\#GetUserControlNcaPath](#GetUserControlNcaPath "wikilink")              |
| 3   | [\#GetDocHtmlNcaPath](#GetDocHtmlNcaPath "wikilink")                      |
| 4   | [\#GetControlNcaPath](#GetControlNcaPath "wikilink")                      |
| 5   | [\#SetControlNcaPath](#SetControlNcaPath "wikilink")                      |
| 6   | [\#SetDocHtmlNcaPath](#SetDocHtmlNcaPath "wikilink")                      |
| 7   | [\#GetInfoHtmlNcaPath](#GetInfoHtmlNcaPath "wikilink")                    |
| 8   | [\#SetInfoHtmlNcaPath](#SetInfoHtmlNcaPath "wikilink")                    |
| 9   | [\#ClearLocationResolver](#ClearLocationResolver "wikilink")              |
| 10  | \[5.0.0+\] [\#SetProgramNcaPath2](#SetProgramNcaPath2 "wikilink")         |
| 11  | \[5.0.0+\] [\#ClearLocationResolver2](#ClearLocationResolver2 "wikilink") |
| 12  | \[5.0.0+\] [\#DeleteProgramNcaPath](#DeleteProgramNcaPath "wikilink")     |
| 13  | \[5.0.0+\] [\#DeleteControlNcaPath](#DeleteControlNcaPath "wikilink")     |
| 14  | \[5.0.0+\] [\#DeleteDocHtmlNcaPath](#DeleteDocHtmlNcaPath "wikilink")     |
| 15  | \[5.0.0+\] [\#DeleteInfoHtmlNcaPath](#DeleteInfoHtmlNcaPath "wikilink")   |

If the supplied
[StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink") is
1 (Host), a different set of internal functions is used to handle these
commands. In this more restricted set of functions, GetControlNcaPath is
stubbed and only returns error 0x608.

The Get\* commands load the
[ContentPath](Filesystem%20services.md "wikilink") from linked-lists'
[entries](#Location_List_Entry "wikilink") in memory using the input
TitleID. When the command fails to find an entry for the specified
TitleID, 0x408 is returned for GetProgramNcaPath and 0xA08 is returned
for the rest.

The Set\* commands always return 0 and add a new entry to the list. If a
matching entry is found, it's removed first.

#### GetProgramNcaPath

Takes an u64 **TitleID** and a C descriptor. Used for
[NCA-type1](NCA%20Content%20FS#NCA-type1.md##NCA-type1 "wikilink").

#### SetProgramNcaPath

Takes an u64 **TitleID** and a X descriptor with a
[ContentPath](Filesystem%20services#ContentPath.md##ContentPath "wikilink").
Used for
[NCA-type1](NCA%20Content%20FS#NCA-type1.md##NCA-type1 "wikilink").

Inserts a new [entry](#Location_List_Entry "wikilink") with **flag** set
to 0.

#### GetUserControlNcaPath

Takes an u64 **TitleID** and a C descriptor. Used for
[NCA-type3](NCA%20Content%20FS#NCA-type3.md##NCA-type3 "wikilink").

#### GetDocHtmlNcaPath

Takes an u64 **TitleID** and a C descriptor. Used for
[NCA-type4](NCA%20Content%20FS#NCA-type4.md##NCA-type4 "wikilink").

#### GetControlNcaPath

Takes an u64 **TitleID** and a C descriptor. Used for
[NCA-type3](NCA%20Content%20FS#NCA-type3.md##NCA-type3 "wikilink").

#### SetControlNcaPath

Takes an u64 **TitleID** and a X descriptor with a
[ContentPath](Filesystem%20services#ContentPath.md##ContentPath "wikilink").
Used for
[NCA-type3](NCA%20Content%20FS#NCA-type3.md##NCA-type3 "wikilink").

Inserts a new [entry](#Location_List_Entry "wikilink") with **flag** set
to 1.

#### SetDocHtmlNcaPath

Takes an u64 **TitleID** and a X descriptor with a
[ContentPath](Filesystem%20services#ContentPath.md##ContentPath "wikilink").
Used for
[NCA-type4](NCA%20Content%20FS#NCA-type4.md##NCA-type4 "wikilink").

Inserts a new [entry](#Location_List_Entry "wikilink") with **flag** set
to 1.

#### GetInfoHtmlNcaPath

Takes an u64 **TitleID** and a C descriptor. Used for
[NCA-type5](NCA%20Content%20FS#NCA-type5.md##NCA-type5 "wikilink").

#### SetInfoHtmlNcaPath

Takes an u64 **TitleID** and a X descriptor with a
[ContentPath](Filesystem%20services#ContentPath.md##ContentPath "wikilink").
Used for
[NCA-type5](NCA%20Content%20FS#NCA-type5.md##NCA-type5 "wikilink").

Inserts a new [entry](#Location_List_Entry "wikilink") with **flag** set
to 1.

#### ClearLocationResolver

Takes no input. Frees all linked-lists' entries that have **flag** set
to 0.

#### SetProgramNcaPath2

Same as [SetProgramNcaPath](#SetProgramNcaPath "wikilink"), but inserts
a new [entry](#Location_List_Entry "wikilink") with **flag** set to 1.

#### ClearLocationResolver2

Takes no input. Frees all linked-lists' entries that have **flag** set
to 1.

#### DeleteProgramNcaPath

Takes an u64 **TitleID**. Used for
[NCA-type1](NCA%20Content%20FS#NCA-type1.md##NCA-type1 "wikilink").

Removes the [entry](#Location_List_Entry "wikilink") that matches the
input TitleID.

#### DeleteControlNcaPath

Takes an u64 **TitleID**. Used for
[NCA-type3](NCA%20Content%20FS#NCA-type3.md##NCA-type3 "wikilink").

Removes the [entry](#Location_List_Entry "wikilink") that matches the
input TitleID.

#### DeleteDocHtmlNcaPath

Takes an u64 **TitleID**. Used for
[NCA-type4](NCA%20Content%20FS#NCA-type4.md##NCA-type4 "wikilink").

Removes the [entry](#Location_List_Entry "wikilink") that matches the
input TitleID.

#### DeleteInfoHtmlNcaPath

Takes an u64 **TitleID**. Used for
[NCA-type5](NCA%20Content%20FS#NCA-type5.md##NCA-type5 "wikilink").

Removes the [entry](#Location_List_Entry "wikilink") that matches the
input TitleID.

### IRegisteredLocationResolver

This is "nn::lr::IRegisteredLocationResolver".

This works like [\#ILocationResolver](#ILocationResolver "wikilink"),
but only two types of NCA paths can be gotten/set. In addition, each
type has a fallback path that can be set for a single title ID at a
time.

| Cmd | Name                                        | Arguments                                                                                              | Notes                                                                                          |
| --- | ------------------------------------------- | ------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------- |
| 0   | GetPatchType0NcaPath                        | u64 TitleID + C descriptor                                                                             | Used for [NCA-type1](NCA%20Content%20FS#NCA-type1.md##NCA-type1 "wikilink").                   |
| 1   | RegisterPatchType0FallbackPath              | u64 TitleID + X descriptor [ContentPath](Filesystem%20services#ContentPath.md##ContentPath "wikilink") | Sets the Type 0 fallback TID and path to the provided arguments.                               |
| 2   | UnregisterPatchType0FallbackPath            | u64 TitleID                                                                                            | If the Type 0 fallback TID is == argument TID, unregisters the fallback path. Otherwise, noop. |
| 3   | SetPatchType0NcaPath                        | u64 TitleID + X descriptor [ContentPath](Filesystem%20services#ContentPath.md##ContentPath "wikilink") |                                                                                                |
| 4   | \[2.0.0+\] GetPatchType1NcaPath             | u64 TitleID + C descriptor                                                                             |                                                                                                |
| 5   | \[2.0.0+\] RegisterPatchType1FallbackPath   | u64 TitleID + X descriptor [ContentPath](Filesystem%20services#ContentPath.md##ContentPath "wikilink") | Sets the Type 1 fallback TID and path to the provided arguments.                               |
| 6   | \[2.0.0+\] UnregisterPatchType1FallbackPath | u64 TitleID                                                                                            | If the Type 1 fallback TID is == argument TID, unregisters the fallback path. Otherwise, noop. |
| 7   | \[2.0.0+\] SetPatchType1NcaPath             | u64 TitleID + X descriptor [ContentPath](Filesystem%20services#ContentPath.md##ContentPath "wikilink") |                                                                                                |

### IAddOnContentLocationResolver

This is
"nn::lr::IAddOnContentLocationResolver".

| Cmd | Name                              | Arguments                                                                           | Notes                              |
| --- | --------------------------------- | ----------------------------------------------------------------------------------- | ---------------------------------- |
| 0   | GetAddOnContentNcaPath            | u64 TitleID + C descriptor                                                          |                                    |
| 1   | RegisterAddOnContent              | [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink") + u64 TitleID |                                    |
| 2   | ClearAddOnContentLocationResolver | None                                                                                | Clears all registered titles here. |

### Location List Entry

Total size is 0x320 bytes.

| Offset | Size  | Description                                        |
| ------ | ----- | -------------------------------------------------- |
| 0x0    | 0x8   | Pointer to previous entry                          |
| 0x8    | 0x8   | Pointer to next entry                              |
| 0x10   | 0x8   | TitleID                                            |
| 0x18   | 0x300 | [ContentPath](Filesystem%20services.md "wikilink") |
| 0x318  | 0x4   | Flag                                               |
| 0x31C  | 0x4   | Padding                                            |

# Content Manager services

## ncm

This is
"nn::ncm::IContentManager".

| Cmd | Name                                                   | Notes                                                                                                                                                                                |
| --- | ------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 0   | CreatePlaceholderAndRegisteredDirectoriesForMediaId    | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink").                                                                                                       |
| 1   | CreateSaveDataDirectoryForMediaId                      | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink").                                                                                                       |
| 2   | GetExistsPlaceholderAndRegisteredDirectoriesForMediaId | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink").                                                                                                       |
| 3   | GetExistsSaveDataDirectoryForMediaId                   | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink").                                                                                                       |
| 4   | GetIContentStorage                                     | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink"), \[2.0.0+\] Only returns a storage if one has previously been opened globally via OpenIContentStorage. |
| 5   | GetIContentMetaDatabase                                | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink"), \[2.0.0+\] Only returns a storage if one has previously been opened globally via OpenIContentStorage. |
| 6   | \[1.0.0\] CloseContentStorageForcibly                  | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink"). Calls IContentStorage-\>CloseAndFlushStorage().                                                       |
| 7   | \[1.0.0\] CloseContentMetaDatabaseForcibly             | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink"). Calls IContentMetaDatabase-\>CloseMetaDatabase().                                                     |
| 8   | DeleteSaveDataForMediaId                               | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink"), and deletes the associated savedata.                                                                  |
| 9   | \[2.0.0+\] OpenIContentStorage                         | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink"), and opens an IContentStorage for the StorageID to be gotten with GetIContentStorage.                  |
| 10  | \[2.0.0+\] CloseIContentStorage                        | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink"), and closes the associated IContentStorage.                                                            |
| 11  | \[2.0.0+\] OpenIContentMetaDatabase                    | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink"), and opens an IContentMetaDatabase for the StorageID to be gotten with GetIContentMetaDatabase.        |
| 12  | \[2.0.0+\] CloseIContentMetaDatabase                   | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink"), and closes the associated IContentMetaDatabase.                                                       |

### IContentStorage

This is
"nn::ncm::IContentStorage".

| Cmd | Name                                                                        | Notes                                                                                                                                                                       |
| --- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0   | [\#GeneratePlaceHolderId](#GeneratePlaceHolderId "wikilink")                | Returns a random UUID for the Content Storage.                                                                                                                              |
| 1   | CreatePlaceholderEntryAndRegisteredDirectoryEntry                           | Takes two [\#NcaIDs](#NcaID "wikilink"), and a u64 filesize.                                                                                                                |
| 2   | DeletePlaceholderEntry                                                      | Takes a [\#NcaID](#NcaID "wikilink").                                                                                                                                       |
| 3   | DoesPlaceholderEntryExist                                                   | Takes a [\#NcaID](#NcaID "wikilink").                                                                                                                                       |
| 4   | WritePlaceholderEntry                                                       | Takes a [\#NcaID](#NcaID "wikilink"), a u64-offset, and type 5 buffer. Writes the buffer to the file for the NcaID's placeholder path at the specified offset.              |
| 5   | MovePlaceholderToRegistered                                                 | Takes two [\#NcaIDs](#NcaID "wikilink"), moves the Placeholder NCA content to the registered NCA path.                                                                      |
| 6   | DeleteRegisteredEntry                                                       | Takes a [\#NcaID](#NcaID "wikilink").                                                                                                                                       |
| 7   | DoesRegisteredEntryExist                                                    | Takes a [\#NcaID](#NcaID "wikilink").                                                                                                                                       |
| 8   | GetPath                                                                     | Takes a [\#NcaID](#NcaID "wikilink"). Returns a [Content Path](Filesystem%20services#ContentPath.md##ContentPath "wikilink").                                               |
| 9   | GetPlaceholderPath                                                          | Takes a [\#NcaID](#NcaID "wikilink"). Returns a [Content Path](Filesystem%20services#ContentPath.md##ContentPath "wikilink").                                               |
| 10  | CleanPlaceholderDirectory                                                   | Deletes and re-creates the Placeholder directory.                                                                                                                           |
| 11  | GetNumberOfPlacholderEntries                                                | This is like [\#GetNumberOfRegisteredEntries](#GetNumberOfRegisteredEntries "wikilink"), but for the Placeholder directory.                                                 |
| 12  | [\#GetNumberOfRegisteredEntries](#GetNumberOfRegisteredEntries "wikilink")  |                                                                                                                                                                             |
| 13  | [\#GetRegisteredEntries](#GetRegisteredEntries "wikilink")                  |                                                                                                                                                                             |
| 14  | [\#GetRegisteredEntrySize](#GetRegisteredEntrySize "wikilink")              |                                                                                                                                                                             |
| 15  | CloseAndFlushStorage                                                        | Closes/Flushes all resources for the storage, and causes all future IPC commands to the current session to return error 0xC805.                                             |
| 16  | \[2.0.0+\] CreatePlaceholderEntryRegisteredEntryAndRegisteredDirectoryEntry | Takes three 0x10-sized [\#NcaIDs](#NcaID "wikilink"). Creates the registered directory NCA path, and renames the placeholder path to the registered NCA path.               |
| 17  | \[2.0.0+\] SetPlaceholderEntrySize                                          | Takes a [\#NcaID](#NcaID "wikilink"), and a u64 size                                                                                                                        |
| 18  | \[2.0.0+\] [\#ReadRegisteredEntryRaw](#ReadRegisteredEntryRaw "wikilink")   |                                                                                                                                                                             |
| 19  | \[2.0.0+\] GetPlaceholderEntryRightsID                                      | Gets the Rights ID for the [\#NcaID](#NcaID "wikilink")'s placeholder path.                                                                                                 |
| 20  | \[2.0.0+\] GetRegisteredEntryRightsID                                       | Gets the Rights ID for the [\#NcaID](#NcaID "wikilink")'s registered path                                                                                                   |
| 21  | \[2.0.0+\] WriteRegisteredPathForDebug                                      | Takes a [\#NcaID](#NcaID "wikilink"), a u64 offset, and a type 5 buffer. On debug units, writes the buffer to the NCA's registered path. On retail units, this just aborts. |
| 22  | \[2.0.0+\] GetFreeSpace                                                     | Gets free space for the storage.                                                                                                                                            |
| 23  | \[2.0.0+\] GetTotalSpace                                                    | Gets total space for the storage.                                                                                                                                           |
| 24  | \[3.0.0+\] FlushStorage                                                     | Flushes resources for the storage without closing it.                                                                                                                       |
| 25  | \[4.0.0+\]                                                                  |                                                                                                                                                                             |
| 26  | \[4.0.0+\]                                                                  |                                                                                                                                                                             |

#### GeneratePlaceHolderId

Generates a random [\#NcaID](#NcaID "wikilink") for use as a
placeholder.

Calls nn::util::GenerateUuid(), which internally calls
nn::os::GenerateRandomBytes(16);

#### GetNumberOfRegisteredEntries

Writes the total number of entries which can be read by GetEntries, to
cmdreply <SFCO_offset>+0x10.

#### GetRegisteredEntries

Takes an output buffer, u32 offset and gets all entries starting at that
offset. Returns number of entries read.

Each entry is a [\#NcaID](#NcaID "wikilink").

The total read entries is exactly the same as the number of "<hex>.nca"
directories in the storage FS(or at least under the "registered"
directory?).

#### GetRegisteredEntrySize

Takes a [\#NcaID](#NcaID "wikilink") as input.

Returns the total size readable by ReadEntryRaw. This is the same as the
size-field in the [NAX0](NAX0.md "wikilink") "<NcaID>.nca/00" file.

#### ReadRegisteredEntryRaw

Takes an output buffer, a [\#NcaID](#NcaID "wikilink") as input, and a
u64 file offset.

Reads plaintext NCA file contents from the Registered path for the
NcaID.

### IContentMetaDatabase

This is "nn::ncm::IContentMetaDatabase".

Note the official name for Meta Record is
"ContentMetaKey".

| Cmd | Name                                                   | Notes                                                                                                                                                                                                                                                                                                                                                                                                                |
| --- | ------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0   | InsertEntryContentRecords                              | Takes a [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink"), a type-5 [Content Records](NCA#Content%20records.md##Content_records "wikilink") buffer and a u64 size.                                                                                                                                                                                                                                       |
| 1   | ReadEntryContentRecords                                | Takes a [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink"), a type-6 buffer to write [Content Records](NCA#Content%20records.md##Content_records "wikilink") to and a u64 size. Returns the actual Content Records size read.                                                                                                                                                                             |
| 2   | RemoveEntryContentRecords                              | Takes a [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink"), and removes the associated record.                                                                                                                                                                                                                                                                                                            |
| 3   | GetEntryContentNcaId                                   | Takes a [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink") and a u8 [Title Type](#Title_Types "wikilink"). Returns a [\#NcaID](#NcaID "wikilink").                                                                                                                                                                                                                                                        |
| 4   | ReadEntryContentRecordEntries                          | Takes a type-6 buffer to write [Content Record](NCA#Content%20records.md##Content_records "wikilink") entries to, a [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink"), and a u32 index into the Content Record entries to start copying from. Returns a u32 entries\_read.                                                                                                                               |
| 5   | List                                                   | Takes a type-6 buffer to write [Meta Records](NCA#Meta%20records.md##Meta_records "wikilink") to, a u32 [Title Type](#Title_Types "wikilink"), a u64 TID, a u64 TID\_LOW, and u64 TID\_HIGH. Writes into the buffer all Meta Records with low \<= record-\>title\_id \<= high, and record-\>type == type. Additionally requires record-\>title\_id == TID, if record-\>type is Application, Patch, Add-On, or Delta. |
| 6   | GetMetaRecord                                          | Takes a u64 title id, and returns the [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink") with the highest version field for that title id.                                                                                                                                                                                                                                                                |
| 7   | [\#ListApplication](#ListApplication "wikilink")       |                                                                                                                                                                                                                                                                                                                                                                                                                      |
| 8   | IsEntryPresent                                         | Takes a [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink") and returns whether that record is present in the database.                                                                                                                                                                                                                                                                                    |
| 9   | AreEntriesPresent                                      | Takes a type-5 buffer containing [Meta Records](NCA#Meta%20records.md##Meta_records "wikilink") (code assumes there are size/sizeof(meta\_record) records in the buffer), and returns whether all of those records are present in the database.                                                                                                                                                                      |
| 10  | GetEntryContentRecordsSize                             | Takes a [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink"), and returns the size of the associated [Content Records](NCA#Content%20records.md##Content_records "wikilink").                                                                                                                                                                                                                               |
| 11  | GetEntryUnknownRecordSize                              | Takes a [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink"), and returns u32 from ContentRecords + 16 (only if the Meta record has type Application or Patch).                                                                                                                                                                                                                                             |
| 12  | GetEntryUpdateTitleId                                  | Takes a [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink"), and returns the update title id for that record.                                                                                                                                                                                                                                                                                              |
| 13  | CloseMetaDatabase                                      | Closes the meta database, and causes all future IPC commands to the current session to return error 0xDC05.                                                                                                                                                                                                                                                                                                          |
| 14  | [\#CheckNcaIDsPresent](#CheckNcaIDsPresent "wikilink") | Takes a type-6 byte buffer, and a type-5 buffer of [\#NcaIDs](#NcaID "wikilink").                                                                                                                                                                                                                                                                                                                                    |
| 15  | SaveMetaDatabase                                       | Flushes the in-memory database to savedata.                                                                                                                                                                                                                                                                                                                                                                          |
| 16  | CheckEntryHasNcaId                                     | Takes a [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink") and an [\#NcaID](#NcaID "wikilink"). Returns whether the content records for that meta record contain the NcaID.                                                                                                                                                                                                                               |
| 17  | ReadEntryMetaRecords                                   | Takes a type-6 [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink") output buffer, a u32 eoffset into that buffer, and an input [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink").                                                                                                                                                                                                              |
| 18  | GetEntryUnknown6                                       | Takes a [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink"), and returns u8 from ContentRecords + 6.                                                                                                                                                                                                                                                                                                       |
| 19  | \[2.0.0+\] GetAddOnContentEntryUnknownRecordSize       | Does the same thing as GetEntryUnknownRecordSize, but for AddOnContents.                                                                                                                                                                                                                                                                                                                                             |
| 20  | \[5.0.0+\]                                             |                                                                                                                                                                                                                                                                                                                                                                                                                      |

#### ListApplication

Each 24-byte entry (officially "ApplicationContentMetaKey") is as
follows:

` `[`meta_record`](NCA#Meta%20records.md##Meta_records "wikilink")` meta_record;`  
` u64    base_title_id;`

This function takes in a type 6 buffer to write entries to, and a u8
"filter" [type](#Title_Types "wikilink"). If filter is zero, all update
records will be copied to to the output buffer (space permitting).
Otherwise, only titles with type == filter\_type will be copied to the
output buffer.

This func returns a u32 num\_entries\_written, and a u32
num\_entries\_total.

#### ReadEntryMetaRecords

Takes a type-6 [Meta
Record](NCA#Meta%20records.md##Meta_records "wikilink") output buffer, a
u32 eoffset into that buffer, and an input [Meta
Record](NCA#Meta%20records.md##Meta_records "wikilink") entry. Returns a
u32 for total\_read\_entries.

Reads the meta records stored in the entry's content records into the
output buffer.

This is used, for example, with System Update title 0100000000000816,
which contains Meta Records for all other systitles in its Content
Records.

#### CheckEntryNcaIDsPresent

Takes a type-6 byte buffer, and a type-5 buffer containing
[\#NcaIDs](#NcaID "wikilink").

This function was stubbed to return 0xDC05 in
[2.0.0](2.0.0.md "wikilink").

On 1.0.0: Initialized the output buffer to all 1s. Then, for each
[\#NcaID](#NcaID "wikilink") in the input buffer, it checks if that
NcaID is present anywhere in the database, and if so writes 0 to the
corresponding output byte.

In pseudocode, the function basically does the following:

for i in range(len(out\_buf)):

`   out_buf[i] = 1`

for i, NcaID in NcaIDs:

`   if is_present_in_database(NcaID):`  
`       out_buf[i] = 0`

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

## ncm:v

This service doesn't normally exist on retail.

[Category:Services](Category:Services "wikilink")

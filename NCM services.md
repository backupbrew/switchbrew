NCM contains services for internal file path and content management.

# Location Resolver services

## lr

This is
"nn::lr::ILocationResolverManager".

| Cmd | Name                                        | Arguments                                                             | Notes |
| --- | ------------------------------------------- | --------------------------------------------------------------------- | ----- |
| 0   | OpenLocationResolver                        | [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink") |       |
| 1   | OpenRegisteredLocationResolver              | None                                                                  |       |
| 2   | RefreshLocationResolver                     | [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink") |       |
| 3   | \[2.0.0+\] OpenAddOnContentLocationResolver | None                                                                  |       |

The only sysmodules which use this service are
[FS](Filesystem%20services.md "wikilink"),
[Loader](Loader%20services.md "wikilink"), and
[NS](NS%20Services.md "wikilink"). [boot2](Boot2.md "wikilink") has
access but doesn't use it.

### ILocationResolver

This is
"nn::lr::ILocationResolver".

| Cmd | Name                                                                                             |
| --- | ------------------------------------------------------------------------------------------------ |
| 0   | [\#ResolveProgramPath](#ResolveProgramPath "wikilink")                                           |
| 1   | [\#RedirectProgramPath](#RedirectProgramPath "wikilink")                                         |
| 2   | [\#ResolveApplicationControlPath](#ResolveApplicationControlPath "wikilink")                     |
| 3   | [\#ResolveApplicationHtmlDocumentPath](#ResolveApplicationHtmlDocumentPath "wikilink")           |
| 4   | [\#ResolveDataPath](#ResolveDataPath "wikilink")                                                 |
| 5   | [\#RedirectApplicationControlPath](#RedirectApplicationControlPath "wikilink")                   |
| 6   | [\#RedirectApplicationHtmlDocumentPath](#RedirectApplicationHtmlDocumentPath "wikilink")         |
| 7   | [\#ResolveApplicationLegalInformationPath](#ResolveApplicationLegalInformationPath "wikilink")   |
| 8   | [\#RedirectApplicationLegalInformationPath](#RedirectApplicationLegalInformationPath "wikilink") |
| 9   | [\#Refresh](#Refresh "wikilink")                                                                 |
| 10  | \[5.0.0+\] [\#SetProgramNcaPath2](#SetProgramNcaPath2 "wikilink")                                |
| 11  | \[5.0.0+\] [\#ClearLocationResolver2](#ClearLocationResolver2 "wikilink")                        |
| 12  | \[5.0.0+\] [\#DeleteProgramNcaPath](#DeleteProgramNcaPath "wikilink")                            |
| 13  | \[5.0.0+\] [\#DeleteControlNcaPath](#DeleteControlNcaPath "wikilink")                            |
| 14  | \[5.0.0+\] [\#DeleteDocHtmlNcaPath](#DeleteDocHtmlNcaPath "wikilink")                            |
| 15  | \[5.0.0+\] [\#DeleteInfoHtmlNcaPath](#DeleteInfoHtmlNcaPath "wikilink")                          |

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

#### ResolveProgramPath

Takes an u64 **TitleID** and a C descriptor. Used for
[NCA-type1](NCA%20Content%20FS#NCA-type1.md##NCA-type1 "wikilink").

#### RedirectProgramPath

Takes an u64 **TitleID** and a X descriptor with a
[ContentPath](Filesystem%20services#ContentPath.md##ContentPath "wikilink").
Used for
[NCA-type1](NCA%20Content%20FS#NCA-type1.md##NCA-type1 "wikilink").

Inserts a new [entry](#Location_List_Entry "wikilink") with **flag** set
to 0.

#### ResolveApplicationControlPath

Takes an u64 **TitleID** and a C descriptor. Used for
[NCA-type3](NCA%20Content%20FS#NCA-type3.md##NCA-type3 "wikilink").

#### ResolveApplicationHtmlDocumentPath

Takes an u64 **TitleID** and a C descriptor. Used for
[NCA-type4](NCA%20Content%20FS#NCA-type4.md##NCA-type4 "wikilink").

#### ResolveDataPath

Takes an u64 **TitleID** and a C descriptor. Used for
[NCA-type3](NCA%20Content%20FS#NCA-type3.md##NCA-type3 "wikilink").

#### RedirectApplicationControlPath

Takes an u64 **TitleID** and a X descriptor with a
[ContentPath](Filesystem%20services#ContentPath.md##ContentPath "wikilink").
Used for
[NCA-type3](NCA%20Content%20FS#NCA-type3.md##NCA-type3 "wikilink").

Inserts a new [entry](#Location_List_Entry "wikilink") with **flag** set
to 1.

#### RedirectApplicationHtmlDocumentPath

Takes an u64 **TitleID** and a X descriptor with a
[ContentPath](Filesystem%20services#ContentPath.md##ContentPath "wikilink").
Used for
[NCA-type4](NCA%20Content%20FS#NCA-type4.md##NCA-type4 "wikilink").

Inserts a new [entry](#Location_List_Entry "wikilink") with **flag** set
to 1.

#### ResolveApplicationLegalInformationPath

Takes an u64 **TitleID** and a C descriptor. Used for
[NCA-type5](NCA%20Content%20FS#NCA-type5.md##NCA-type5 "wikilink").

#### RedirectApplicationLegalInformationPath

Takes an u64 **TitleID** and a X descriptor with a
[ContentPath](Filesystem%20services#ContentPath.md##ContentPath "wikilink").
Used for
[NCA-type5](NCA%20Content%20FS#NCA-type5.md##NCA-type5 "wikilink").

Inserts a new [entry](#Location_List_Entry "wikilink") with **flag** set
to 1.

#### Refresh

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

| Cmd | Name                                  | Arguments                                                                                              | Notes                                                                                          |
| --- | ------------------------------------- | ------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------- |
| 0   | ResolveProgramPath                    | u64 TitleID + C descriptor                                                                             | Used for [NCA-type1](NCA%20Content%20FS#NCA-type1.md##NCA-type1 "wikilink").                   |
| 1   | RegisterProgramPath                   | u64 TitleID + X descriptor [ContentPath](Filesystem%20services#ContentPath.md##ContentPath "wikilink") | Sets the Type 0 fallback TID and path to the provided arguments.                               |
| 2   | UnregisterProgramPath                 | u64 TitleID                                                                                            | If the Type 0 fallback TID is == argument TID, unregisters the fallback path. Otherwise, noop. |
| 3   | RedirectProgramPath                   | u64 TitleID + X descriptor [ContentPath](Filesystem%20services#ContentPath.md##ContentPath "wikilink") |                                                                                                |
| 4   | \[2.0.0+\] ResolveHtmlDocumentPath    | u64 TitleID + C descriptor                                                                             |                                                                                                |
| 5   | \[2.0.0+\] RegisterHtmlDocumentPath   | u64 TitleID + X descriptor [ContentPath](Filesystem%20services#ContentPath.md##ContentPath "wikilink") | Sets the Type 1 fallback TID and path to the provided arguments.                               |
| 6   | \[2.0.0+\] UnregisterHtmlDocumentPath | u64 TitleID                                                                                            | If the Type 1 fallback TID is == argument TID, unregisters the fallback path. Otherwise, noop. |
| 7   | \[2.0.0+\] RedirectHtmlDocumentPath   | u64 TitleID + X descriptor [ContentPath](Filesystem%20services#ContentPath.md##ContentPath "wikilink") |                                                                                                |

### IAddOnContentLocationResolver

This is
"nn::lr::IAddOnContentLocationResolver".

| Cmd | Name                          | Arguments                                                                           | Notes                              |
| --- | ----------------------------- | ----------------------------------------------------------------------------------- | ---------------------------------- |
| 0   | ResolveAddOnContentPath       | u64 TitleID + C descriptor                                                          |                                    |
| 1   | RegisterAddOnContentStorage   | [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink") + u64 TitleID |                                    |
| 2   | UnregisterAllAddOnContentPath | None                                                                                | Clears all registered titles here. |

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

| Cmd | Name                                       | Notes                                                                                                                                                                                                     |
| --- | ------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0   | CreateContentStorage                       | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink").                                                                                                                            |
| 1   | CreateContentMetaDatabase                  | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink").                                                                                                                            |
| 2   | VerifyContentStorage                       | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink").                                                                                                                            |
| 3   | VerifyContentMetaDatabase                  | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink").                                                                                                                            |
| 4   | OpenContentStorage                         | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink"), \[2.0.0+\] Only returns a storage if one has previously been opened globally via OpenIContentStorage.                      |
| 5   | OpenContentMetaDatabase                    | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink"), \[2.0.0+\] Only returns a storage if one has previously been opened globally via OpenIContentStorage.                      |
| 6   | \[1.0.0\] CloseContentStorageForcibly      | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink"). Calls IContentStorage-\>CloseAndFlushStorage().                                                                            |
| 7   | \[1.0.0\] CloseContentMetaDatabaseForcibly | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink"). Calls IContentMetaDatabase-\>CloseMetaDatabase().                                                                          |
| 8   | CleanupContentMetaDatabase                 | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink"), and deletes the associated savedata.                                                                                       |
| 9   | \[2.0.0+\] OpenContentStorage2             | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink"), and opens an IContentStorage for the StorageID to be gotten with GetIContentStorage. Note: Name is not official.           |
| 10  | \[2.0.0+\] CloseContentStorage             | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink"), and closes the associated IContentStorage. Note: Name is not official.                                                     |
| 11  | \[2.0.0+\] OpenContentMetaDatabase2        | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink"), and opens an IContentMetaDatabase for the StorageID to be gotten with GetIContentMetaDatabase. Note: Name is not official. |
| 12  | \[2.0.0+\] CloseContentMetaDatabase        | Takes a [StorageID](Filesystem%20services#StorageId.md##StorageId "wikilink"), and closes the associated IContentMetaDatabase. Note: Name is not official.                                                |

### IContentStorage

This is
"nn::ncm::IContentStorage".

| Cmd | Name                                                            | Notes                                                                                                                                                                       |
| --- | --------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0   | [\#GeneratePlaceHolderId](#GeneratePlaceHolderId "wikilink")    | Returns a random UUID for the Content Storage.                                                                                                                              |
| 1   | CreatePlaceHolder                                               | Takes two [\#NcaIDs](#NcaID "wikilink"), and a u64 filesize.                                                                                                                |
| 2   | DeletePlaceHolder                                               | Takes a [\#NcaID](#NcaID "wikilink").                                                                                                                                       |
| 3   | HasPlaceHolder                                                  | Takes a [\#NcaID](#NcaID "wikilink").                                                                                                                                       |
| 4   | WritePlaceHolder                                                | Takes a [\#NcaID](#NcaID "wikilink"), a u64-offset, and type 5 buffer. Writes the buffer to the file for the NcaID's placeholder path at the specified offset.              |
| 5   | Register                                                        | Takes two [\#NcaIDs](#NcaID "wikilink"), moves the Placeholder NCA content to the registered NCA path.                                                                      |
| 6   | Delete                                                          | Takes a [\#NcaID](#NcaID "wikilink").                                                                                                                                       |
| 7   | Has                                                             | Takes a [\#NcaID](#NcaID "wikilink").                                                                                                                                       |
| 8   | GetPath                                                         | Takes a [\#NcaID](#NcaID "wikilink"). Returns a [Content Path](Filesystem%20services#ContentPath.md##ContentPath "wikilink").                                               |
| 9   | GetPlaceHolderPath                                              | Takes a [\#NcaID](#NcaID "wikilink"). Returns a [Content Path](Filesystem%20services#ContentPath.md##ContentPath "wikilink").                                               |
| 10  | CleanupAllPlaceHolder                                           | Deletes and re-creates the Placeholder directory.                                                                                                                           |
| 11  | ListPlaceHolder                                                 | This is like [\#GetNumberOfRegisteredEntries](#GetNumberOfRegisteredEntries "wikilink"), but for the Placeholder directory.                                                 |
| 12  | [\#GetContentCount](#GetContentCount "wikilink")                |                                                                                                                                                                             |
| 13  | [\#ListContentId](#ListContentId "wikilink")                    |                                                                                                                                                                             |
| 14  | [\#GetSize](#GetSize "wikilink")                                |                                                                                                                                                                             |
| 15  | DisableForcibly                                                 | Closes/Flushes all resources for the storage, and causes all future IPC commands to the current session to return error 0xC805.                                             |
| 16  | \[2.0.0+\] RevertToPlaceHolder                                  | Takes three 0x10-sized [\#NcaIDs](#NcaID "wikilink"). Creates the registered directory NCA path, and renames the placeholder path to the registered NCA path.               |
| 17  | \[2.0.0+\] SetPlaceHolderSize                                   | Takes a [\#NcaID](#NcaID "wikilink"), and a u64 size                                                                                                                        |
| 18  | \[2.0.0+\] [\#ReadContentIdFile](#ReadContentIdFile "wikilink") |                                                                                                                                                                             |
| 19  | \[2.0.0+\] GetRightsIdFromPlaceHolderId                         | Gets the Rights ID for the [\#NcaID](#NcaID "wikilink")'s placeholder path.                                                                                                 |
| 20  | \[2.0.0+\] GetRightsIdFromContentId                             | Gets the Rights ID for the [\#NcaID](#NcaID "wikilink")'s registered path                                                                                                   |
| 21  | \[2.0.0+\] WriteContentForDebug                                 | Takes a [\#NcaID](#NcaID "wikilink"), a u64 offset, and a type 5 buffer. On debug units, writes the buffer to the NCA's registered path. On retail units, this just aborts. |
| 22  | \[2.0.0+\] GetFreeSpaceSize                                     | Gets free space for the storage.                                                                                                                                            |
| 23  | \[2.0.0+\] GetTotalSpaceSize                                    | Gets total space for the storage.                                                                                                                                           |
| 24  | \[3.0.0+\] FlushStorage                                         | Flushes resources for the storage without closing it.                                                                                                                       |
| 25  | \[4.0.0+\]                                                      |                                                                                                                                                                             |
| 26  | \[4.0.0+\]                                                      |                                                                                                                                                                             |

#### GeneratePlaceHolderId

Generates a random [\#NcaID](#NcaID "wikilink") for use as a
placeholder.

Calls nn::util::GenerateUuid(), which internally calls
nn::os::GenerateRandomBytes(16);

#### GetContentCount

Writes the total number of entries which can be read by GetEntries, to
cmdreply <SFCO_offset>+0x10.

#### ListContentId

Takes an output buffer, u32 offset and gets all entries starting at that
offset. Returns number of entries read.

Each entry is a [\#NcaID](#NcaID "wikilink").

The total read entries is exactly the same as the number of "<hex>.nca"
directories in the storage FS(or at least under the "registered"
directory?).

#### GetSize

Takes a [\#NcaID](#NcaID "wikilink") as input.

Returns the total size readable by ReadEntryRaw. This is the same as the
size-field in the [NAX0](NAX0.md "wikilink") "<NcaID>.nca/00" file.

#### ReadContentIdFile

Takes an output buffer, a [\#NcaID](#NcaID "wikilink") as input, and a
u64 file offset.

Reads plaintext NCA file contents from the Registered path for the
NcaID.

### IContentMetaDatabase

This is "nn::ncm::IContentMetaDatabase".

Note the official name for Meta Record is
"ContentMetaKey".

| Cmd | Name                                                     | Notes                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| --- | -------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0   | Set                                                      | Takes a [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink"), a type-5 [Content Records](NCA#Content%20records.md##Content_records "wikilink") buffer and a u64 size.                                                                                                                                                                                                                                                                                                                                                                             |
| 1   | Get                                                      | Takes a [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink"), a type-6 buffer to write [Content Records](NCA#Content%20records.md##Content_records "wikilink") to and a u64 size. Returns the actual number of bytes read into the buffer. Content Records start at offset 0x8 of the buffer, at 0x2 is how many there are.                                                                                                                                                                                                                       |
| 2   | Remove                                                   | Takes a [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink"), and removes the associated record.                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| 3   | GetContentIdByType                                       | Takes a [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink") and a u8 [Title Type](#Title_Types "wikilink"). Returns a [\#NcaID](#NcaID "wikilink").                                                                                                                                                                                                                                                                                                                                                                                              |
| 4   | ListContentInfo                                          | Takes a type-6 buffer to write [Content Record](NCA#Content%20records.md##Content_records "wikilink") entries to, a [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink"), and a u32 index into the Content Record entries to start copying from. Returns a u32 entries\_read.                                                                                                                                                                                                                                                                     |
| 5   | List                                                     | Takes a type-6 buffer to write [Meta Records](NCA#Meta%20records.md##Meta_records "wikilink") to, a u32 [Title Type](#Title_Types "wikilink"), a u64 TID, a u64 TID\_LOW, and u64 TID\_HIGH. Writes into the buffer all Meta Records with low \<= record-\>title\_id \<= high, and record-\>type == type. Returns u32 numEntriesTotal, numEntriesWritten. Additionally requires record-\>title\_id == TID, if record-\>type is Application, Patch, Add-On, or Delta, otherwise, you can pass 0 for type to ignore the type and list them all in the range. |
| 6   | GetLatestContentMetaKey                                  | Takes a u64 title id, and returns the [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink") with the highest version field for that title id.                                                                                                                                                                                                                                                                                                                                                                                                      |
| 7   | [\#ListApplication](#ListApplication "wikilink")         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| 8   | Has                                                      | Takes a [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink") and returns whether that record is present in the database.                                                                                                                                                                                                                                                                                                                                                                                                                          |
| 9   | HasAll                                                   | Takes a type-5 buffer containing [Meta Records](NCA#Meta%20records.md##Meta_records "wikilink") (code assumes there are size/sizeof(meta\_record) records in the buffer), and returns whether all of those records are present in the database.                                                                                                                                                                                                                                                                                                            |
| 10  | GetSize                                                  | Takes a [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink"), and returns the size of the associated [Content Records](NCA#Content%20records.md##Content_records "wikilink").                                                                                                                                                                                                                                                                                                                                                                     |
| 11  | GetRequiredSystemVersion                                 | Takes a [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink"), and returns u32 from ContentRecords + 16 (only if the Meta record has type Application or Patch).                                                                                                                                                                                                                                                                                                                                                                                   |
| 12  | GetPatchId                                               | Takes a [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink"), and returns the update title id for that record.                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| 13  | DisableForcibly                                          | Closes the meta database, and causes all future IPC commands to the current session to return error 0xDC05.                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| 14  | [\#LookupOrphanContent](#LookupOrphanContent "wikilink") | Takes a type-6 byte buffer, and a type-5 buffer of [\#NcaIDs](#NcaID "wikilink").                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| 15  | Commit                                                   | Flushes the in-memory database to savedata.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| 16  | HasContent                                               | Takes a [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink") and an [\#NcaID](#NcaID "wikilink"). Returns whether the content records for that meta record contain the NcaID.                                                                                                                                                                                                                                                                                                                                                                     |
| 17  | ListContentMetaInfo                                      | Takes a type-6 [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink") output buffer, a u32 eoffset into that buffer, and an input [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink").                                                                                                                                                                                                                                                                                                                                                    |
| 18  | GetAttributes                                            | Takes a [Meta Record](NCA#Meta%20records.md##Meta_records "wikilink"), and returns u8 from ContentRecords + 6.                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| 19  | \[2.0.0+\] GetRequiredApplicationVersion                 | Does the same thing as GetEntryUnknownRecordSize, but for AddOnContents.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| 20  | \[5.0.0+\]                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |

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

This func returns a u32 num\_entries\_total, and a u32
num\_entries\_written.

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

#### LookupOrphanContent

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
[SD](SD%20Filesystem.md "wikilink")). This is also referred to as
"ContentId" in the official SDK.

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

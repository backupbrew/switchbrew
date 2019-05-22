This is the metadata file that ends in `".cnmt{.nca}"` or `"meta0.ncd"`.
This seems to replace the TMD format.

There's at least 9 different filenames used for ".cnmt":

  - "Application\_{lower-case hex titleID}.cnmt"
  - "Patch\_{lower-case hex titleID}.cnmt"
  - "AddOnContent\_{lower-case hex titleID}.cnmt"
  - "SystemUpdate\_{hex titleID}.cnmt"
  - "SystemData\_{lower-case hex titleID}.cnmt"
  - "SystemProgram\_{lower-case hex titleID}.cnmt"
  - "BootImagePackage\_{lower-case hex titleID}.cnmt"
  - "BootImagePackageSafe\_{lower-case hex titleID}.cnmt"
  - "Delta\_{lower-case hex titleID}.cnmt"

## Header

| Offset | Size | Description                                                          |
| ------ | ---- | -------------------------------------------------------------------- |
| 0x0    | 0x8  | Title ID                                                             |
| 0x8    | 0x4  | [Version](Title%20list.md "wikilink")                                |
| 0xC    | 0x1  | [Meta Type](NCM%20services#Title%20Types.md##Title_Types "wikilink") |
| 0xD    | 0x1  | Unused                                                               |
| 0xE    | 0x2  | Extended Header Size                                                 |
| 0x10   | 0x2  | Content Count                                                        |
| 0x12   | 0x2  | Content Meta Count                                                   |
| 0x14   | 0x1  | Attributes (0=None, 1=IncludesExFatDriver, 2=Rebootless)             |
| 0x15   | 0x3  | Unused                                                               |
| 0x18   | 0x4  | Required Download System Version                                     |
| 0x1C   | 0x4  | Unused                                                               |

## SystemUpdate Extended Header

| Offset | Size | Description          |
| ------ | ---- | -------------------- |
| 0x0    | 0x4  | Extended Header Size |

## Application Extended Header

| Offset | Size | Description             |
| ------ | ---- | ----------------------- |
| 0x0    | 0x8  | Patch ID                |
| 0x8    | 0x4  | Required System Version |

## Patch Extended Header

| Offset | Size | Description             |
| ------ | ---- | ----------------------- |
| 0x0    | 0x8  | Application ID          |
| 0x8    | 0x4  | Required System Version |
| 0xC    | 0x4  | Extended Data Size      |
| 0x10   | 0x8  | Unused                  |

## AddOnContent Extended Header

| Offset | Size | Description                  |
| ------ | ---- | ---------------------------- |
| 0x0    | 0x8  | Application ID               |
| 0x8    | 0x4  | Required Application Version |
| 0xC    | 0x4  | Unused                       |

## Delta Extended Header

| Offset | Size | Description        |
| ------ | ---- | ------------------ |
| 0x0    | 0x8  | Application ID     |
| 0x8    | 0x4  | Extended Data Size |
| 0xC    | 0x4  | Unused             |

## Content records

| Offset | Size | Description                                                                                                                                                                                                  |
| ------ | ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 0x0    | 0x20 | Hash                                                                                                                                                                                                         |
| 0x20   | 0x10 | Content ID                                                                                                                                                                                                   |
| 0x30   | 0x6  | Size                                                                                                                                                                                                         |
| 0x36   | 0x1  | Title Type (0=Meta, 1=Program, 2=Data, 3=Control, 4=[HtmlDocument](Internet%20Browser.md "wikilink"), 5=[LegalInformation](Internet%20Browser.md "wikilink"), 6=[DeltaFragment](NCA%20Format.md "wikilink")) |
| 0x37   | 0x1  | Id Offset                                                                                                                                                                                                    |

## Meta records

| Offset | Size | Description                                                          |
| ------ | ---- | -------------------------------------------------------------------- |
| 0x0    | 0x8  | Title ID                                                             |
| 0x8    | 0x4  | Version                                                              |
| 0xC    | 0x1  | [Meta Type](NCM%20services#Title%20Types.md##Title_Types "wikilink") |
| 0xD    | 0x1  | Attributes (0=None, 1=IncludesExFatDriver, 2=Rebootless)             |
| 0xE    | 0x2  | Unused                                                               |

This is used for SystemUpdate, see here:
[NCM\_services\#ReadEntryMetaRecords](NCM%20services#ReadEntryMetaRecords.md##ReadEntryMetaRecords "wikilink").

## Extended data

Patch-type cnmt files include an extended data section.

| Offset | Size    | Description                                       |
| ------ | ------- | ------------------------------------------------- |
| 0x0    | 4       | Number of previous cnmt entries.                  |
| 0x4    | 4       | Number of previous delta entries.                 |
| 0x8    | 4       | Number of delta info entries.                     |
| 0xC    | 4       | Number of delta application info entries.         |
| 0x10   | 4       | Number of previous content entries.               |
| 0x14   | 4       | Number of delta content entries.                  |
| 0x18   | 4       | Unused?                                           |
| 0x1C   | 0x38\*X | Previous cnmt entries                             |
|        | 0x28\*X | Previous delta entries                            |
|        | 0x28\*X | Delta info entries                                |
|        | 0x34\*X | Delta application info entries                    |
|        | 0x18\*X | Previous content entries                          |
|        | 0x38\*X | Delta content entries. (Standard content records) |
|        | 4       | Unknown                                           |
|        | 4       | Unknown                                           |
|        | 4       | Unknown                                           |
|        |         |                                                   |

## Previous cnmt records

Each entry is 0x38 bytes:

| Offset | Size | Description                                                                       |
| ------ | ---- | --------------------------------------------------------------------------------- |
| 0x0    | 8    | Title ID                                                                          |
| 0x8    | 4    | Title version                                                                     |
| 0xC    | 1    | Type (see [Title Types](NCM%20services#Title%20Types.md##Title_Types "wikilink")) |
| 0xD    | 3    | Unused?                                                                           |
| 0x10   | 32   | Hash                                                                              |
| 0x30   | 2    | Unknown                                                                           |
| 0x32   | 2    | Unused?                                                                           |
| 0x34   | 4    | Unused?                                                                           |
|        |      |                                                                                   |

This contains information on previous metadata files.

## Previous delta records

Each entry is 0x28 bytes:

| Offset | Size | Description       |
| ------ | ---- | ----------------- |
| 0x0    | 8    | Old title ID      |
| 0x8    | 8    | New title ID      |
| 0x10   | 4    | Old title version |
| 0x14   | 4    | New title version |
| 0x18   | 8    | Size              |
| 0x20   | 8    | Unused?           |
|        |      |                   |

This contains information on previous delta patches.

## Delta info records

Each entry is 0x28 bytes:

| Offset | Size | Description         |
| ------ | ---- | ------------------- |
| 0x0    | 8    | Old title ID        |
| 0x8    | 8    | New title ID        |
| 0x10   | 4    | Old title version   |
| 0x14   | 4    | New title version   |
| 0x18   | 8    | Some sort of index? |
| 0x20   | 8    | Some sort of index? |
|        |      |                     |

This contains information on the current delta patch.

## Delta application info records

Each entry is 0x34 bytes:

| Offset | Size | Description                                                                       |
| ------ | ---- | --------------------------------------------------------------------------------- |
| 0x0    | 16   | Old NcaId                                                                         |
| 0x10   | 16   | New NcaId                                                                         |
| 0x20   | 6    | Old size                                                                          |
| 0x26   | 2    | Upper 2 bytes of the new size                                                     |
| 0x28   | 4    | Lower 4 bytes of the new size                                                     |
| 0x2C   | 2    | Unknown                                                                           |
| 0x2E   | 1    | Type (see [Title Types](NCM%20services#Title%20Types.md##Title_Types "wikilink")) |
| 0x2F   | 1    | ? bit0 set = don't install?                                                       |
| 0x30   | 4    | Unused?                                                                           |
|        |      |                                                                                   |

This contains information on how to apply deltas to the previous patch.

## Previous content records

Each entry is 0x18 bytes:

| Offset | Size | Description                                                                       |
| ------ | ---- | --------------------------------------------------------------------------------- |
| 0x0    | 16   | NcaId                                                                             |
| 0x10   | 6    | Size                                                                              |
| 0x16   | 1    | Type (see [Title Types](NCM%20services#Title%20Types.md##Title_Types "wikilink")) |
| 0x17   | 1    |                                                                                   |
|        |      |                                                                                   |

This contains information on previous title content from earlier
patches.

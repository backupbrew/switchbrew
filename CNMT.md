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
| 0x8    | 0x4  | Version                                                              |
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

| Offset | Size | Description        |
| ------ | ---- | ------------------ |
| 0x0    | 0x4  | Extended Data Size |

## Application Extended Header

| Offset | Size | Description             |
| ------ | ---- | ----------------------- |
| 0x0    | 0x8  | Patch ID                |
| 0x8    | 0x4  | Required System Version |
| 0xC    | 0x4  | Unused                  |

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

## Content Records

| Offset | Size | Description                                                                                                                                                                                                    |
| ------ | ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x20 | Hash                                                                                                                                                                                                           |
| 0x20   | 0x10 | Content ID                                                                                                                                                                                                     |
| 0x30   | 0x6  | Size                                                                                                                                                                                                           |
| 0x36   | 0x1  | Content Type (0=Meta, 1=Program, 2=Data, 3=Control, 4=[HtmlDocument](Internet%20Browser.md "wikilink"), 5=[LegalInformation](Internet%20Browser.md "wikilink"), 6=[DeltaFragment](NCA%20Format.md "wikilink")) |
| 0x37   | 0x1  | Id Offset                                                                                                                                                                                                      |

## Content Meta Records

| Offset | Size | Description                                                          |
| ------ | ---- | -------------------------------------------------------------------- |
| 0x0    | 0x8  | Title ID                                                             |
| 0x8    | 0x4  | Version                                                              |
| 0xC    | 0x1  | [Meta Type](NCM%20services#Title%20Types.md##Title_Types "wikilink") |
| 0xD    | 0x1  | Attributes (0=None, 1=IncludesExFatDriver, 2=Rebootless)             |
| 0xE    | 0x2  | Unused                                                               |

This is used for SystemUpdate, see here:
[NCM\_services\#ReadEntryMetaRecords](NCM%20services#ReadEntryMetaRecords.md##ReadEntryMetaRecords "wikilink").

## SystemUpdate Extended Data

| Offset | Size                    | Description        |
| ------ | ----------------------- | ------------------ |
| 0x0    | 0x4                     | Version            |
| 0x4    | 0x4                     | Variation Count    |
| 0x8    | 0x4                     | Firmware Variation |
| 0xC    | 0x1C \* Variation Count | Unused             |

## Patch Extended Data

| Offset | Size                                           | Description                                                                                                               |
| ------ | ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x4                                            | History Count                                                                                                             |
| 0x4    | 0x4                                            | Delta History Count                                                                                                       |
| 0x8    | 0x4                                            | Delta Count                                                                                                               |
| 0xC    | 0x4                                            | Fragment Set Count                                                                                                        |
| 0x10   | 0x4                                            | History Content Count                                                                                                     |
| 0x14   | 0x4                                            | Delta Content Count                                                                                                       |
| 0x18   | 0x4                                            | Unused                                                                                                                    |
| 0x1C   | 0x38 \* History Count                          | [History Headers](CNMT#History%20Header.md##History_Header "wikilink")                                                    |
|        | 0x28 \* Delta History Count                    | [Delta Histories](CNMT#Delta%20History.md##Delta_History "wikilink")                                                      |
|        | 0x28 \* Delta Count                            | [Delta Headers](CNMT#Delta%20Header.md##Delta_Header "wikilink")                                                          |
|        | 0x34 \* Fragment Set Count                     | [Fragment Sets](CNMT#Fragment%20Set.md##Fragment_Set "wikilink")                                                          |
|        | 0x18 \* History Content Count                  | [History Content Records (Content Records without the Hash entry)](CNMT#Content%20Records.md##Content_Records "wikilink") |
|        | 0x38 \* Delta Content Count                    | [Delta Content Records](CNMT#Content%20Records.md##Content_Records "wikilink")                                            |
|        | 0x4 \* Fragment Indicator Count (Fragment Set) | [Fragment Indicators](CNMT#Fragment%20Indicator.md##Fragment_Indicator "wikilink")                                        |

### History Header

| Offset | Size | Description                                                                              |
| ------ | ---- | ---------------------------------------------------------------------------------------- |
| 0x0    | 0x10 | [Content Meta Record](CNMT#Content%20Meta%20Records.md##Content_Meta_Records "wikilink") |
| 0xC    | 0x1  | [Meta Type](NCM%20services#Title%20Types.md##Title_Types "wikilink")                     |
| 0xD    | 0x1  | Attributes (0=None, 1=IncludesExFatDriver, 2=Rebootless)                                 |
| 0xE    | 0x2  | Unused                                                                                   |
| 0x10   | 0x20 | Digest                                                                                   |
| 0x30   | 0x2  | Content Info Count                                                                       |
| 0x32   | 0x6  | Unused                                                                                   |

### Delta History

| Offset | Size | Description          |
| ------ | ---- | -------------------- |
| 0x0    | 0x8  | Source Patch ID      |
| 0x8    | 0x8  | Destination Patch ID |
| 0x10   | 0x4  | Source Version       |
| 0x14   | 0x4  | Destination Version  |
| 0x18   | 0x8  | Download Size        |
| 0x20   | 0x8  | Unused               |

### Delta Header

| Offset | Size | Description          |
| ------ | ---- | -------------------- |
| 0x0    | 0x8  | Source Patch ID      |
| 0x8    | 8    | Destination Patch ID |
| 0x10   | 0x4  | Source Version       |
| 0x14   | 0x4  | Destination Version  |
| 0x18   | 0x2  | Fragment Set Count   |
| 0x1A   | 0x6  | Unused               |
| 0x20   | 0x2  | Content Info Count   |
| 0x22   | 0x6  | Unused               |

### Fragment Set

| Offset | Size | Description                                                                                                                                                                                                    |
| ------ | ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x10 | Source Content ID                                                                                                                                                                                              |
| 0x10   | 0x10 | Destination Content ID                                                                                                                                                                                         |
| 0x20   | 0x6  | Source Size                                                                                                                                                                                                    |
| 0x26   | 0x6  | Destination Size                                                                                                                                                                                               |
| 0x2C   | 0x2  | Fragment Indicator Count                                                                                                                                                                                       |
| 0x2E   | 0x1  | Content Type (0=Meta, 1=Program, 2=Data, 3=Control, 4=[HtmlDocument](Internet%20Browser.md "wikilink"), 5=[LegalInformation](Internet%20Browser.md "wikilink"), 6=[DeltaFragment](NCA%20Format.md "wikilink")) |
| 0x2F   | 0x1  | Update Type (0=ApplyAsDelta, 1=Overwrite, 2=Create)                                                                                                                                                            |
| 0x30   | 0x4  | Unused                                                                                                                                                                                                         |

### Fragment Indicator

| Offset | Size | Description        |
| ------ | ---- | ------------------ |
| 0x0    | 0x2  | Content Info Index |
| 0x2    | 0x2  | Fragment Index     |

## Delta Extended Data

| Offset | Size                                           | Description                                                                        |
| ------ | ---------------------------------------------- | ---------------------------------------------------------------------------------- |
| 0x0    | 0x8                                            | Source Patch ID                                                                    |
| 0x8    | 0x8                                            | Destination Patch ID                                                               |
| 0x10   | 0x4                                            | Source Version                                                                     |
| 0x14   | 0x4                                            | Destination Version                                                                |
| 0x18   | 0x2                                            | Fragment Set Count                                                                 |
| 0x1A   | 0x6                                            | Unused                                                                             |
| 0x20   | 0x34 \* Fragment Set Count                     | [Fragment Sets](CNMT#Fragment%20Set.md##Fragment_Set "wikilink")                   |
|        | 0x4 \* Fragment Indicator Count (Fragment Set) | [Fragment Indicators](CNMT#Fragment%20Indicator.md##Fragment_Indicator "wikilink") |

## Digest

Always found at the end of the file.

| Offset | Size | Description |
| ------ | ---- | ----------- |
| 0x0    | 0x20 | Digest      |

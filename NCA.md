For the content of the NCA FS which can be
[mounted](Filesystem%20services.md "wikilink"), see
[here](NCA%20Content%20FS.md "wikilink").

For the format of the actual NCA, see
[here](NCA%20Format.md "wikilink").

# Metadata file

This is the file that ends in `".cnmt{.nca}"` or `"meta0.ncd"`. This
seems to replace the TMD format.

There's at least 7 different filenames used for ".cnmt":

  - "Application\_{lower-case hex titleID}.cnmt"
  - "Patch\_{lower-case hex titleID}.cnmt"
  - "SystemUpdate\_{hex titleID}.cnmt"
  - "SystemData\_{lower-case hex titleID}.cnmt"
  - "SystemProgram\_{lower-case hex titleID}.cnmt"
  - "BootImagePackage\_{lower-case hex titleID}.cnmt"
  - "BootImagePackageSafe\_{lower-case hex titleID}.cnmt"

It starts with a
header:

| Offset | Size | Description                                                                                     |
| ------ | ---- | ----------------------------------------------------------------------------------------------- |
| 0x0    | 8    | Title ID                                                                                        |
| 0x8    | 4    | u32 [title-version](Title%20list.md "wikilink")                                                 |
| 0xC    | 1    | Type (see [Title Types](Content%20Manager%20services#Title%20Types.md##Title_Types "wikilink")) |
| 0xD    | 1    |                                                                                                 |
| 0xE    | 2    | Offset to table relative to the end of this 0x20-byte header.                                   |
| 0x10   | 2    | Number of content entries                                                                       |
| 0x12   | 2    | Number of meta entries                                                                          |
| 0x14   | 12   |                                                                                                 |

With SystemUpdate, the 4-bytes at offset 0xE are zero, with the
entry-count field located at offset 0x12 instead(header size is the
same).

An optional header can follow, depending on the title type.

At the end of the file following the entries is a 0x20-byte block,
presumably a hash.

With Patch-format, there's additional data after the end of the entries
specified in the header and before the ending hash.

## Application header

| Offset | Size | Description            |
| ------ | ---- | ---------------------- |
| 0x20   | 8    | Application ID         |
| 0x28   | 8    | Minimum system version |

## Patch header

| Offset | Size | Description            |
| ------ | ---- | ---------------------- |
| 0x20   | 8    | Original title ID      |
| 0x28   | 8    | Minimum system version |

## Add-on content header

| Offset | Size | Description                 |
| ------ | ---- | --------------------------- |
| 0x20   | 8    | Application title ID        |
| 0x28   | 8    | Minimum application version |

## Content records

Each entry is 0x38
bytes:

| Offset | Size | Description                                                                                                                                                                                                          |
| ------ | ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 32   | Hash                                                                                                                                                                                                                 |
| 0x20   | 16   | NcaId \[same as first 16-bytes of hash\]                                                                                                                                                                             |
| 0x30   | 6    | Size, same as the output from [Content\_Manager\_services\#GetEntrySize](Content%20Manager%20services#GetEntrySize.md##GetEntrySize "wikilink").                                                                     |
| 0x36   | 1    | Type (0=meta, 1=program, 2=data, 3=control, 4=offline-manual [html](Internet%20Browser.md "wikilink"), 5=legal [html](Internet%20Browser.md "wikilink"), 6=[game-update](NCA%20Format.md "wikilink") RomFS patches?) |
| 0x37   | 1    |                                                                                                                                                                                                                      |

## Meta records

Each entry is 0x10
bytes:

| Offset | Size | Description                                                                                     |
| ------ | ---- | ----------------------------------------------------------------------------------------------- |
| 0x0    | 8    | Title ID                                                                                        |
| 0x8    | 4    | Title version                                                                                   |
| 0xC    | 1    | Type (see [Title Types](Content%20Manager%20services#Title%20Types.md##Title_Types "wikilink")) |
| 0xD    | 1    | ? bit0 set = don't install?                                                                     |
| 0xE    | 2    | Unused?                                                                                         |

This is used for SystemUpdate, see here:
[Content\_Manager\_services\#GetUpdateTitleList](Content%20Manager%20services#GetUpdateTitleList.md##GetUpdateTitleList "wikilink").

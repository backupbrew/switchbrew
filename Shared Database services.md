# pl:u

This is
"nn::pl::detail::ISharedFontManager".

| Cmd | Name                                                                           |
| --- | ------------------------------------------------------------------------------ |
| 0   | [\#RequestLoad](#RequestLoad "wikilink")                                       |
| 1   | [\#GetLoadState](#GetLoadState "wikilink")                                     |
| 2   | [\#GetSize](#GetSize "wikilink")                                               |
| 3   | [\#GetSharedMemoryAddressOffset](#GetSharedMemoryAddressOffset "wikilink")     |
| 4   | [\#GetSharedMemoryNativeHandle](#GetSharedMemoryNativeHandle "wikilink")       |
| 5   | [\#GetSharedFontInOrderOfPriority](#GetSharedFontInOrderOfPriority "wikilink") |

## RequestLoad

Takes a [\#SharedFontType](#SharedFontType "wikilink") (uint32), no
output.

## GetLoadState

Takes a [\#SharedFontType](#SharedFontType "wikilink") (uint32), returns
the [\#LoadState](#LoadState "wikilink") (uint32).

### LoadState

| Value | Description |
| ----- | ----------- |
| 0x00  | Loading     |
| 0x01  | Loaded      |

## GetSize

Takes a [\#SharedFontType](#SharedFontType "wikilink") (uint32), returns
the Font Size (uint32).

## GetSharedMemoryAddressOffset

Takes a [\#SharedFontType](#SharedFontType "wikilink") (uint32), returns
the offset (uint32) to the Font Address.

## GetSharedMemoryNativeHandle

No input, returns an output SharedMemory handle.

User-processes map this SharedMemory with size=0x1100000 and
permissions=R--.

Font data is TTF, located at the offset returned by
[\#GetSharedMemoryAddressOffset](#GetSharedMemoryAddressOffset "wikilink").

## GetSharedFontInOrderOfPriority

Takes an input u64
[LanguageCode](Settings%20services#LanguageCode.md##LanguageCode "wikilink")
and 3 type-0x6 output buffers, returns an output u8 and u32.

## SharedFontType

| Value | Description                     |
| ----- | ------------------------------- |
| 0x00  | Japan, US and Europe (Standard) |
| 0x01  | Chinese Simplified              |
| 0x02  | Extended Chinese Simplified     |
| 0x03  | Chinese Traditional             |
| 0x04  | Korean (Hangul)                 |
| 0x05  | Nintendo Extended               |

# mii:u, mii:e

This is "nn::mii::detail::IStaticService".

| Cmd | Name               |
| --- | ------------------ |
| 0   | GetDatabaseService |

## IDatabaseService

This is "nn::mii::detail::IDatabaseService".

| Cmd | Name                           |
| --- | ------------------------------ |
| 0   | IsUpdated                      |
| 1   | IsFullDatabase                 |
| 2   | GetCount                       |
| 3   | Get                            |
| 4   | Get1                           |
| 5   | UpdateLatest                   |
| 6   | BuildRandom                    |
| 7   | BuildDefault                   |
| 8   | Get2                           |
| 9   | Get3                           |
| 10  | UpdateLatest1                  |
| 11  | FindIndex                      |
| 12  | Move                           |
| 13  | AddOrReplace                   |
| 14  | Delete                         |
| 15  | DestroyFile                    |
| 16  | DeleteFile                     |
| 17  | Format                         |
| 18  | Import                         |
| 19  | Export                         |
| 20  | IsBrokenDatabaseWithClearFlag  |
| 21  | GetIndex                       |
| 22  | \[5.0.0+\] SetInterfaceVersion |
| 23  | \[5.0.0+\] Convert             |

# miiimg

This is "nn::mii::detail::IImageDatabaseService".

| Cmd | Name             |
| --- | ---------------- |
| 0   | Initialize       |
| 10  | Reload           |
| 11  | GetCount         |
| 12  | IsEmpty          |
| 13  | IsFull           |
| 14  | GetAttribute     |
| 15  | LoadImage        |
| 16  | AddOrUpdateImage |
| 17  | DeleteImages     |
| 100 | DeleteFile       |
| 101 | DestroyFile      |
| 102 | ImportFile       |
| 103 | ExportFile       |
| 104 | ForceInitialize  |

[Category:Services](Category:Services "wikilink")

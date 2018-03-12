# pl:u (Shared Font Manager)

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
\#GetSharedMemoryAddressOffset.

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

| Cmd | Name                            |
| --- | ------------------------------- |
| 0   | GetDatabaseServiceSharedPointer |

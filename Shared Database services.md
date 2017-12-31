# pl:u (Shared Font Manager)

| Cmd | Name                                                                       |
| --- | -------------------------------------------------------------------------- |
| 0   | [\#RequestLoad](#RequestLoad "wikilink")                                   |
| 1   | [\#GetLoadState](#GetLoadState "wikilink")                                 |
| 2   | [\#GetSize](#GetSize "wikilink")                                           |
| 3   | [\#GetSharedMemoryAddressOffset](#GetSharedMemoryAddressOffset "wikilink") |
| 4   | GetSharedMemoryNativeHandle                                                |
| 5   | GetSharedFontInOrderOfPriority                                             |

## RequestLoad

Takes a [\#SharedFontType](#SharedFontType "wikilink") (uint32)

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
the Font Size (uint32)

## GetSharedMemoryAddressOffset

Takes a [\#SharedFontType](#SharedFontType "wikilink") (uint32), returns
the offset (uint32) to the Font Address.

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

| Cmd | Name                            |
| --- | ------------------------------- |
| 0   | GetDatabaseServiceSharedPointer |

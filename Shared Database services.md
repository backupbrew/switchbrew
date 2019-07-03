# pl:u

This is "nn::pl::detail::IPlatformServiceManager".

| Cmd | Name                                                                             |
| --- | -------------------------------------------------------------------------------- |
| 0   | [\#RequestSharedFontLoad](#RequestSharedFontLoad "wikilink")                     |
| 1   | [\#GetSharedFontLoadState](#GetSharedFontLoadState "wikilink")                   |
| 2   | [\#GetSharedFontSize](#GetSharedFontSize "wikilink")                             |
| 3   | [\#GetSharedFontAddress](#GetSharedFontAddress "wikilink")                       |
| 4   | [\#GetSharedFontSharedMemoryHandle](#GetSharedFontSharedMemoryHandle "wikilink") |
| 5   | [\#GetSharedFontInOrderOfPriority](#GetSharedFontInOrderOfPriority "wikilink")   |
| 6   | \[4.0.0+\] GetSharedFontInOrderOfPriorityForSystem                               |
| 100 | \[8.0.0+\] RequestApplicationFunctionAuthorization                               |
| 101 | \[8.0.0+\] RequestApplicationFunctionAuthorizationForSystem                      |

## RequestSharedFontLoad

Takes a [\#SharedFontType](#SharedFontType "wikilink") (uint32), no
output.

## GetSharedFontLoadState

Takes a [\#SharedFontType](#SharedFontType "wikilink") (uint32), returns
the [\#LoadState](#LoadState "wikilink") (uint32).

### LoadState

| Value | Description |
| ----- | ----------- |
| 0x00  | Loading     |
| 0x01  | Loaded      |

## GetSharedFontSize

Takes a [\#SharedFontType](#SharedFontType "wikilink") (uint32), returns
the Font Size (uint32).

## GetSharedFontAddress

Takes a [\#SharedFontType](#SharedFontType "wikilink") (uint32), returns
the offset (uint32) to the Font Address.

## GetSharedFontSharedMemoryHandle

No input, returns an output SharedMemory handle.

User-processes map this SharedMemory with size=0x1100000 and
permissions=R--.

Font data is TTF, located at the offset returned by
[\#GetSharedFontAddress](#GetSharedFontAddress "wikilink").

## GetSharedFontInOrderOfPriority

Takes an input u64
[LanguageCode](Settings%20services#LanguageCode.md##LanguageCode "wikilink")
and 3 type-0x6 output buffers, returns an output u8 and u32. The u8 is a
bool to specify if the fonts are loaded or not and the u32 is the font
count. The first buffer contains a list of [Shared font
types](#SharedFontType "wikilink"), the second buffer contains the font
offsets and the final buffer contains the font sizes. The buffers are an
array of u32s which specify information about a specific font.
Buffer1\[n\] is related to Buffer2\[n\] and Buffer3\[n\]. Example: Font
index 0s offset is at Buffer2\[0\], size is at Buffer3\[0\]. The fonts
are relative to the shared memory created by
[\#GetSharedFontSharedMemoryHandle](#GetSharedFontSharedMemoryHandle "wikilink")

## SharedFontType

| Value | Description                     |
| ----- | ------------------------------- |
| 0x00  | Japan, US and Europe (Standard) |
| 0x01  | Chinese Simplified              |
| 0x02  | Extended Chinese Simplified     |
| 0x03  | Chinese Traditional             |
| 0x04  | Korean (Hangul)                 |
| 0x05  | Nintendo Extended               |

  - Nintendo Extended: Contains Nintendo-specific characters, including
    HID buttons, HID controller styles, applet icons, Wii(U) icons, etc.

# mii:u, mii:e

This is "nn::mii::detail::IStaticService".

| Cmd | Name               |
| --- | ------------------ |
| 0   | GetDatabaseService |

## IDatabaseService

This is "nn::mii::detail::IDatabaseService".

| Cmd | Name                                 |
| --- | ------------------------------------ |
| 0   | IsUpdated                            |
| 1   | IsFullDatabase                       |
| 2   | GetCount                             |
| 3   | Get                                  |
| 4   | Get1                                 |
| 5   | UpdateLatest                         |
| 6   | BuildRandom                          |
| 7   | BuildDefault                         |
| 8   | Get2                                 |
| 9   | Get3                                 |
| 10  | UpdateLatest1                        |
| 11  | FindIndex                            |
| 12  | Move                                 |
| 13  | AddOrReplace                         |
| 14  | Delete                               |
| 15  | DestroyFile                          |
| 16  | DeleteFile                           |
| 17  | Format                               |
| 18  | Import                               |
| 19  | Export                               |
| 20  | IsBrokenDatabaseWithClearFlag        |
| 21  | GetIndex                             |
| 22  | \[5.0.0+\] SetInterfaceVersion       |
| 23  | \[5.0.0+\] Convert                   |
| 24  | \[7.0.0+\] ConvertCoreDataToCharInfo |
| 25  | \[7.0.0+\] ConvertCharInfoToCoreData |

# miiimg

This is "nn::mii::detail::IImageDatabaseService".

This was added with \[5.0.0+\].

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

# pdm:ntfy

This is "nn::pdm::detail::INotifyService".

| Cmd | Name                                      |
| --- | ----------------------------------------- |
| 0   | NotifyAppletEvent                         |
| 2   | NotifyOperationModeChangeEvent            |
| 3   | NotifyPowerStateChangeEvent               |
| 4   | NotifyClearAllEvent                       |
| 5   | NotifyEventForDebug                       |
| 6   | \[4.0.0+\] SuspendUserAccountEventService |
| 7   | \[4.0.0+\] ResumeUserAccountEventService  |
| 8   | \[6.0.0+\]                                |
| 9   | \[8.0.0+\]                                |

# pdm:qry

This is "nn::pdm::detail::IQueryService".

| Cmd               | Name                                                                                                                   |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------- |
| 0                 | [\#QueryApplicationEvent](#QueryApplicationEvent "wikilink")                                                           |
| \[1.0.0-6.2.0\] 1 | QueryPlayStatistics                                                                                                    |
| \[1.0.0-6.2.0\] 2 | QueryPlayStatisticsByUserAccountId                                                                                     |
| \[1.0.0-6.2.0\] 3 | QueryPlayStatisticsByNetworkServiceAccountId                                                                           |
| 4                 | [\#QueryPlayStatisticsByApplicationId](#QueryPlayStatisticsByApplicationId "wikilink")                                 |
| 5                 | [\#QueryPlayStatisticsByApplicationIdAndUserAccountId](#QueryPlayStatisticsByApplicationIdAndUserAccountId "wikilink") |
| \[1.0.0-6.2.0\] 6 | QueryPlayStatisticsByApplicationIdAndNetworkServiceAccountId                                                           |
| 7                 | [\#QueryLastPlayTime](#QueryLastPlayTime "wikilink")                                                                   |
| 8                 | [\#QueryPlayEvent](#QueryPlayEvent "wikilink")                                                                         |
| 9                 | [\#GetAvailablePlayEventRange](#GetAvailablePlayEventRange "wikilink")                                                 |
| 10                | [\#QueryAccountEvent](#QueryAccountEvent "wikilink")                                                                   |
| 11                | \[4.0.0+\] [\#QueryAccountPlayEvent](#QueryAccountPlayEvent "wikilink")                                                |
| 12                | \[4.0.0+\] [\#GetAvailableAccountPlayEventRange](#GetAvailableAccountPlayEventRange "wikilink")                        |
| 13                | \[5.0.0+\] [\#QueryApplicationPlayStatisticsForSystem](#QueryApplicationPlayStatisticsForSystem "wikilink")            |
| 14                | \[6.0.0+\]                                                                                                             |
| 15                | \[6.0.0+\]                                                                                                             |
| 16                | \[6.0.0+\]                                                                                                             |

## QueryApplicationEvent

Takes an input u32 entryindex, a type-0x6 output buffer containing an
array of [\#ApplicationEvent](#ApplicationEvent "wikilink"), and returns
an output s32 for actual total output entries.

## QueryPlayStatisticsByApplicationId

Takes an input u64 titleID and returns an output
[\#PlayStatistics](#PlayStatistics "wikilink").

## QueryPlayStatisticsByApplicationIdAndUserAccountId

Takes an input u64 titleID, an input u128 userID, and returns an output
[\#PlayStatistics](#PlayStatistics "wikilink").

## QueryLastPlayTime

Takes a type-0x6 output buffer containing an array of
[\#LastPlayTime](#LastPlayTime "wikilink"), and a type-0x5 input buffer
containing an array of u64 titleIDs. Returns an output s32 for actual
total output entries.

## QueryPlayEvent

Takes an input u32 entryindex, a type-0x6 output buffer containing an
array of [\#PlayEvent](#PlayEvent "wikilink"), and returns an output u32
for actual total output entries.

## GetAvailablePlayEventRange

No input, returns 3 output u32s: total\_entries, start\_entryindex, and
end\_entryindex.

## QueryAccountEvent

Takes an input u32 entryindex, a type-0x6 output buffer containing an
array of [\#AccountEvent](#AccountEvent "wikilink"), and returns an
output s32 for actual total output entries.

## QueryAccountPlayEvent

Takes an input u32 entryoffset, an input u128 userID, a type-0x6 output
buffer containing an array of
[\#AccountPlayEvent](#AccountPlayEvent "wikilink"), and returns an
output u32 for actual total output entries.

## GetAvailableAccountPlayEventRange

Takes an input u128 userID and returns 3 output u32s: total\_entries,
start\_entryindex, and end\_entryindex.

## QueryApplicationPlayStatisticsForSystem

Takes a type-0x6 output buffer containing an array of
[\#ApplicationPlayStatistics](#ApplicationPlayStatistics "wikilink") and
a type-0x5 input buffer containing an array of u64 titleIDs. Returns an
output s32 for actual total output entries.

The number of entries in each array is the same.

## Cmd14

Takes an input u128 userID, a type-0x6 output buffer containing an array
of u64 titleIDs, and returns an output u32 for actual total output
entries.

Returns a list of titles played by the specified user.

## Cmd15

No input, returns an output handle.

## Cmd16

Takes a u128 userID, a type-0x6 output buffer containing an array of
[\#ApplicationPlayStatistics](#ApplicationPlayStatistics "wikilink") and
a type-0x5 input buffer containing an array of u64 titleIDs. Returns an
output s32 for actual total output entries.

Same as
[\#QueryApplicationPlayStatisticsForSystem](#QueryApplicationPlayStatisticsForSystem "wikilink")
except this gets playstats specific to userIDs.

# avm

This is "nn::avm::srv::IAvmService".

This was added with \[6.0.0+\].

| Cmd  | Name                                                                             |
| ---- | -------------------------------------------------------------------------------- |
| 100  |                                                                                  |
| 101  |                                                                                  |
| 102  |                                                                                  |
| 103  | No input, returns an [\#IVersionListImporter](#IVersionListImporter "wikilink"). |
| 200  |                                                                                  |
| 202  |                                                                                  |
| 1000 |                                                                                  |
| 1001 |                                                                                  |
| 1002 |                                                                                  |

## IVersionListImporter

This is "nn::avm::srv::IVersionListImporter".

This was added with \[6.0.0+\].

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |

# ApplicationEvent

| Offset | Size | Description                               |
| ------ | ---- | ----------------------------------------- |
| 0x0    | 0x8  | titleID                                   |
| 0x8    | 0x4  | entryindex                                |
| 0xC    | 0x4  | timestamp0                                |
| 0x10   | 0x4  | timestamp1                                |
| 0x14   | 0x1  | [\#PlayEvent](#PlayEvent "wikilink") +0xF |
| 0x15   | 0x3  | Padding                                   |

This is a 0x18-byte struct.

Timestamp format, converted from PosixTime: total minutes since epoch
UTC 1999/12/31 00:00.

# PlayStatistics

| Offset | Size | Description                                                                                        |
| ------ | ---- | -------------------------------------------------------------------------------------------------- |
| 0x0    | 0x8  | titleID                                                                                            |
| 0x8    | 0x4  | First entryindex                                                                                   |
| 0xC    | 0x4  | First timestamp0. Same as the first [\#ApplicationEvent](#ApplicationEvent "wikilink") timestamp.  |
| 0x10   | 0x4  | First timestamp1. Same as the second [\#ApplicationEvent](#ApplicationEvent "wikilink") timestamp. |
| 0x14   | 0x4  | Last entryindex                                                                                    |
| 0x18   | 0x4  | Last timestamp0. Same as the first [\#ApplicationEvent](#ApplicationEvent "wikilink") timestamp.   |
| 0x1C   | 0x4  | Last timestamp1. Same as the second [\#ApplicationEvent](#ApplicationEvent "wikilink") timestamp.  |
| 0x20   | 0x4  | Total play-time in minutes.                                                                        |
| 0x24   | 0x4  | Total times the application title was launched.                                                    |

This is a 0x28-byte struct.

# LastPlayTime

| Offset | Size | Description                                                                      |
| ------ | ---- | -------------------------------------------------------------------------------- |
| 0x0    | 0x8  | titleID                                                                          |
| 0x8    | 0x4  | Same as the first [\#ApplicationEvent](#ApplicationEvent "wikilink") timestamp.  |
| 0xC    | 0x4  | Same as the second [\#ApplicationEvent](#ApplicationEvent "wikilink") timestamp. |
| 0x10   | 0x4  | ?                                                                                |
| 0x14   | 0x1  | ?                                                                                |
| 0x15   | 0x3  | Padding                                                                          |

This is a 0x18-byte struct. This contains data from the last time the
title was played.

# PlayEvent

| Offset | Size | Description                                   |
| ------ | ---- | --------------------------------------------- |
| 0x0    | 0x8  | titleID, with the u32 low/high words swapped. |
| 0x8    | 0x18 | ?                                             |
| 0x20   | 0x8  | PosixTime timestamp0                          |
| 0x28   | 0x8  | PosixTime timestamp1                          |
| 0x30   | 0x8  | ?                                             |

This is a 0x38-byte struct.

This is the raw entry struct directly read from FS, without any entry
filtering. The other structs are extracted+converted from this one, with
filtering.

# AccountEvent

| Offset | Size | Description     |
| ------ | ---- | --------------- |
| 0x0    | 0x10 | userID          |
| 0x10   | 0x4  | entryindex      |
| 0x14   | 0x4  | Padding         |
| 0x18   | 0x8  | POSIX timestamp |
| 0x20   | 0x8  | POSIX timestamp |
| 0x28   | 0x8  | ?               |
| 0x30   | 0x1  | ?               |
| 0x31   | 0x7  | Padding         |

This is a 0x38-byte struct.

# AccountPlayEvent

| Offset | Size | Description                                   |
| ------ | ---- | --------------------------------------------- |
| 0x0    | 0x4  | ?                                             |
| 0x4    | 0x8  | titleID, with the u32 low/high words swapped. |
| 0xC    | 0xC  | ?                                             |
| 0x18   | 0x8  | POSIX timestamp                               |
| 0x20   | 0x8  | POSIX timestamp                               |

This is a 0x28-byte struct.

This is the raw entry struct directly read from FS, without any entry
filtering. This is separate from [\#PlayEvent](#PlayEvent "wikilink").

# ApplicationPlayStatistics

| Offset | Size | Description                                     |
| ------ | ---- | ----------------------------------------------- |
| 0x0    | 0x8  | titleID                                         |
| 0x8    | 0x8  | Total play-time in nanoseconds.                 |
| 0x10   | 0x8  | Total times the application title was launched. |

This is "nn::pdm::ApplicationPlayStatistics".

This is a 0x18-byte struct.

[Category:Services](Category:Services "wikilink")

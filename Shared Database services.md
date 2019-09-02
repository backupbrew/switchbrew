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

| Cmd | Name                                                                           |
| --- | ------------------------------------------------------------------------------ |
| 0   | [\#NotifyAppletEvent](#NotifyAppletEvent "wikilink")                           |
| 2   | [\#NotifyOperationModeChangeEvent](#NotifyOperationModeChangeEvent "wikilink") |
| 3   | [\#NotifyPowerStateChangeEvent](#NotifyPowerStateChangeEvent "wikilink")       |
| 4   | [\#NotifyClearAllEvent](#NotifyClearAllEvent "wikilink")                       |
| 5   | [\#NotifyEventForDebug](#NotifyEventForDebug "wikilink")                       |
| 6   | \[4.0.0+\] SuspendUserAccountEventService                                      |
| 7   | \[4.0.0+\] ResumeUserAccountEventService                                       |
| 8   | \[6.0.0+\]                                                                     |
| 9   | \[8.0.0+\]                                                                     |

## NotifyAppletEvent

Takes an input u8 [\#AppletEventType](#AppletEventType "wikilink"), an
u8
[AppletId](Applet%20Manager%20services#AppletId.md##AppletId "wikilink"),
an u8
[StorageId](Filesystem%20services#StorageId.md##StorageId "wikilink"),
an u8 [\#PlayLogPolicy](#PlayLogPolicy "wikilink"), an u32
**event\_x8**, and an u64 **titleID**. Returns no output.

When [\#PlayLogPolicy](#PlayLogPolicy "wikilink") is 2 ("None") this
will immediately return 0.

Logs a new [\#PlayEvent](#PlayEvent "wikilink") with the following data:

  - Clears the 0x10-bytes at +0x10.
  - u8 +0xF = [\#AppletEventType](#AppletEventType "wikilink").
  - Sets the 3 timestamps.
  - Converts **titleID** and writes it to +0x0.
  - u32 +0x8 = **event\_x8**.
  - u8 +0xC =
    [AppletId](Applet%20Manager%20services#AppletId.md##AppletId "wikilink"),
    u8 +0xD =
    [StorageId](Filesystem%20services#StorageId.md##StorageId "wikilink"),
    and u8 +0xE = [\#PlayLogPolicy](#PlayLogPolicy "wikilink").

After the initial logging, additional code runs with some of the above
input params.

## NotifyOperationModeChangeEvent

Takes an input u8 **inval**, no output.

Logs a new [\#PlayEvent](#PlayEvent "wikilink") with the following data:
clears the 0x20-bytes at +0x0, u8 +0x1C = 0x3, u8 +0x0 = **inval**, and
sets the 3 timestamps.

## NotifyPowerStateChangeEvent

Takes an input u8 **inval**, no output.

Logs a new [\#PlayEvent](#PlayEvent "wikilink") with the following data:
clears the 0x20-bytes at +0x0, u8 +0x1C = 0x2, u8 +0x0 = **inval**, and
sets the 3 timestamps.

After the initial logging, additional code runs which uses **inval**.

## NotifyClearAllEvent

No input/output.

## NotifyEventForDebug

Takes an input type-0x5 buffer containing an array of
[\#PlayEvent](#PlayEvent "wikilink"), no output.

Gets the [system-setting](System%20Settings.md "wikilink")
`pdm!is_production`, the size must be 1 and the value must be 0,
otherwise an error is returned.

Each [\#PlayEvent](#PlayEvent "wikilink") entry is validated, throwing
an error on failure. After an entry is successfully validated, it is
written to the log.

## Cmd8

Takes an input u8 [\#AppletEventType](#AppletEventType "wikilink"), an
u8
[LibraryAppletMode](Applet%20Manager%20services#LibraryAppletMode.md##LibraryAppletMode "wikilink"),
an u8
[AppletId](Applet%20Manager%20services#AppletId.md##AppletId "wikilink"),
an u8
[StorageId](Filesystem%20services#StorageId.md##StorageId "wikilink"),
an u8 [\#PlayLogPolicy](#PlayLogPolicy "wikilink"), and an u64
**titleID**. Returns no output.

This is similar to [\#NotifyAppletEvent](#NotifyAppletEvent "wikilink").

When [\#PlayLogPolicy](#PlayLogPolicy "wikilink") is 2 ("None") this
will immediately return 0.

Logs a new [\#PlayEvent](#PlayEvent "wikilink") with the following data:

  - Clears the 0x20-bytes at +0x0.
  - u8 +0xF = [\#AppletEventType](#AppletEventType "wikilink").
  - Sets the 3 timestamps.
  - Converts **titleID** and writes it to +0x0.
  - u8 +0x9 =
    [LibraryAppletMode](Applet%20Manager%20services#LibraryAppletMode.md##LibraryAppletMode "wikilink").
  - u8 +0x8 = 1.
  - u8 +0xC =
    [AppletId](Applet%20Manager%20services#AppletId.md##AppletId "wikilink"),
    u8 +0xD =
    [StorageId](Filesystem%20services#StorageId.md##StorageId "wikilink"),
    and u8 +0xE = [\#PlayLogPolicy](#PlayLogPolicy "wikilink").

After the initial logging, additional code runs with some of the above
input params. This is handled the same as
[\#NotifyAppletEvent](#NotifyAppletEvent "wikilink"), except that the
value passed for **event\_x8** is value 0 here.

## Cmd9

Takes an input u8 [\#AppletEventType](#AppletEventType "wikilink"), an
u8
[AppletId](Applet%20Manager%20services#AppletId.md##AppletId "wikilink"),
an u8
[StorageId](Filesystem%20services#StorageId.md##StorageId "wikilink"),
an 0x20-byte struct, an u8 bool flag, an u8
[\#PlayLogPolicy](#PlayLogPolicy "wikilink"), an u32 **event\_x8**, and
an u64 **titleID**. Returns no output.

This is identical to
[\#NotifyAppletEvent](#NotifyAppletEvent "wikilink") except for the
additional struct/flag params.

After the initial logging, additional code runs with some of the above
input params. This is handled the same as
[\#NotifyAppletEvent](#NotifyAppletEvent "wikilink"), except that when
the u8 bool flag is set the input struct is used with this.

# pdm:qry

This is "nn::pdm::detail::IQueryService".

| Cmd               | Name                                                                                                                                      |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| 0                 | [\#QueryApplicationEvent](#QueryApplicationEvent "wikilink")                                                                              |
| \[1.0.0-6.2.0\] 1 | QueryPlayStatistics                                                                                                                       |
| \[1.0.0-6.2.0\] 2 | QueryPlayStatisticsByUserAccountId                                                                                                        |
| \[1.0.0-6.2.0\] 3 | QueryPlayStatisticsByNetworkServiceAccountId                                                                                              |
| 4                 | [\#QueryPlayStatisticsByApplicationId](#QueryPlayStatisticsByApplicationId "wikilink")                                                    |
| 5                 | [\#QueryPlayStatisticsByApplicationIdAndUserAccountId](#QueryPlayStatisticsByApplicationIdAndUserAccountId "wikilink")                    |
| \[1.0.0-6.2.0\] 6 | QueryPlayStatisticsByApplicationIdAndNetworkServiceAccountId                                                                              |
| 7                 | [\#QueryLastPlayTime](#QueryLastPlayTime "wikilink")                                                                                      |
| 8                 | [\#QueryPlayEvent](#QueryPlayEvent "wikilink")                                                                                            |
| 9                 | [\#GetAvailablePlayEventRange](#GetAvailablePlayEventRange "wikilink")                                                                    |
| 10                | [\#QueryAccountEvent](#QueryAccountEvent "wikilink")                                                                                      |
| 11                | \[4.0.0+\] [\#QueryAccountPlayEvent](#QueryAccountPlayEvent "wikilink")                                                                   |
| 12                | \[4.0.0+\] [\#GetAvailableAccountPlayEventRange](#GetAvailableAccountPlayEventRange "wikilink")                                           |
| 13                | \[5.0.0+\] [\#QueryApplicationPlayStatisticsForSystem](#QueryApplicationPlayStatisticsForSystem "wikilink")                               |
| 14                | \[6.0.0+\] [\#QueryRecentlyPlayedApplication](#QueryRecentlyPlayedApplication "wikilink")                                                 |
| 15                | \[6.0.0+\] [\#GetRecentlyPlayedApplicationUpdateEvent](#GetRecentlyPlayedApplicationUpdateEvent "wikilink")                               |
| 16                | \[6.0.0+\] [\#QueryApplicationPlayStatisticsByUserAccountIdForSystem](#QueryApplicationPlayStatisticsByUserAccountIdForSystem "wikilink") |

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

## QueryRecentlyPlayedApplication

Takes an input u128 userID, a type-0x6 output buffer containing an array
of u64 titleIDs, and returns an output u32 for actual total output
entries.

Returns a list of titles played by the specified user.

## GetRecentlyPlayedApplicationUpdateEvent

No input, returns an output Event handle with autoclear=false.

This is signaled when logging a new [\#PlayEvent](#PlayEvent "wikilink")
which would be available via
[\#QueryAccountEvent](#QueryAccountEvent "wikilink"), where
[\#PlayEvent](#PlayEvent "wikilink") +0x18 is 0.

## QueryApplicationPlayStatisticsByUserAccountIdForSystem

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
| 0x10   | 0x4  | Total minutes since the title was last played.                                   |
| 0x14   | 0x1  | Flag indicating whether the above field is set.                                  |
| 0x15   | 0x3  | Padding                                                                          |

This is a 0x18-byte struct. This contains data from the last time the
title was played.

# PlayEventType

| Value | Description                                                                                |
| ----- | ------------------------------------------------------------------------------------------ |
| 0     | Applet                                                                                     |
| 1     | Account                                                                                    |
| 2     | PowerStateChange                                                                           |
| 3     | OperationModeChange                                                                        |
| 4     | Initialize. Used for the very first [\#PlayEvent](#PlayEvent "wikilink") entry in the log. |

This is an enum for [\#PlayEvent](#PlayEvent "wikilink") +0x1C, which
indicates the type of [\#PlayEvent](#PlayEvent "wikilink").

# AppletEventType

| Value | Description      |
| ----- | ---------------- |
| 0     | "launch"         |
| 1     | "exit"           |
| 2     | "in\_focus"      |
| 3     | "out\_of\_focus" |
| 4     | "out\_of\_focus" |
| 5     | "exit"           |
| 6     | "exit"           |

This is an enum for [\#PlayEvent](#PlayEvent "wikilink") +0xF with
[\#PlayEventType](#PlayEventType "wikilink") = Applet, this indicates
the type of the Applet event.

# PlayLogPolicy

| Value | Meaning | Description                                                                                                                                                                                  |
| ----- | ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0     | All     | All pdm:qry cmds which require [\#PlayEventType](#PlayEventType "wikilink") = Applet and AppletId = Application will only return the entry when PlayLogPolicy matches this value.            |
| 1     | LogOnly | The above commands will filter out the entry with this.                                                                                                                                      |
| 2     | None    | pdm:ntfy [\#NotifyAppletEvent](#NotifyAppletEvent "wikilink"), [\#Cmd8](#Cmd8 "wikilink"), and [\#Cmd9](#Cmd9 "wikilink") will immediately return 0 when the input param matches this value. |

This is an enum for [\#PlayEvent](#PlayEvent "wikilink") +0xE with
[\#PlayEventType](#PlayEventType "wikilink") = Applet. This is set via
the above commands, which uses this as an input param.

# PlayEvent

| Offset | Size | Description                                                                            |
| ------ | ---- | -------------------------------------------------------------------------------------- |
| 0x1C   | 0x1  | [\#PlayEventType](#PlayEventType "wikilink")                                           |
| 0x1D   | 0x3  | Padding                                                                                |
| 0x20   | 0x8  | PosixTime timestamp from [StandardUserSystemClock](PCV%20services.md "wikilink").      |
| 0x28   | 0x8  | PosixTime timestamp from [StandardNetworkSystemClock](PCV%20services.md "wikilink").   |
| 0x30   | 0x8  | Timestamp in seconds derived from [StandardSteadyClock](PCV%20services.md "wikilink"). |

This is a 0x38-byte struct.

This is the raw entry struct directly read from FS, without any entry
filtering. The other structs are extracted+converted from this one, with
filtering.

Filtering:

  - [\#QueryApplicationEvent](#QueryApplicationEvent "wikilink"),
    [\#QueryLastPlayTime](#QueryLastPlayTime "wikilink"), and
    [\#QueryApplicationPlayStatisticsForSystem](#QueryApplicationPlayStatisticsForSystem "wikilink"):
    PlayEvent +0x1C must be 0, +0xC must be 1, and +0xE must be 0.
  - [\#QueryPlayStatisticsByApplicationId](#QueryPlayStatisticsByApplicationId "wikilink"):
    PlayEvent +0x1C must be 0, +0xC must be 1, and the titleID must
    match.
  - [\#QueryAccountEvent](#QueryAccountEvent "wikilink"): PlayEvent
    +0x1C must be 1 and PlayEvent +0x18 must be \<=1.
  - [\#QueryApplicationPlayStatisticsForSystem](#QueryApplicationPlayStatisticsForSystem "wikilink"):
    In addition to the above, this also handles
    [\#PlayEventType](#PlayEventType "wikilink") PowerStateChange, where
    PlayEvent +0x0 is value 0 or 1.

The structure of the first 0x1C-bytes are determined by
[\#PlayEventType](#PlayEventType "wikilink"). For titleIDs/userIDs, the
low/high u32 in each u64 is swapped.

Applet:

| Offset | Size | Description                                                                                                                 |
| ------ | ---- | --------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x8  | titleID                                                                                                                     |
| 0x8    | 0x4  | Title version, set by pdm:ntfy [\#NotifyAppletEvent](#NotifyAppletEvent "wikilink") and [\#Cmd9](#Cmd9 "wikilink").         |
| 0x8    | 0x1  | When set to u8 0x1 by pdm:ntfy [\#Cmd8](#Cmd8 "wikilink"), this indicates that +0x9 is set. Only used for non-applications. |
| 0x9    | 0x1  | See above. [LibraryAppletMode](Applet%20Manager%20services#LibraryAppletMode.md##LibraryAppletMode "wikilink")              |
| 0xC    | 0x1  | [AppletId](Applet%20Manager%20services#AppletId.md##AppletId "wikilink")                                                    |
| 0xD    | 0x1  | [StorageId](Filesystem%20services#StorageId.md##StorageId "wikilink")                                                       |
| 0xE    | 0x1  | [\#PlayLogPolicy](#PlayLogPolicy "wikilink")                                                                                |
| 0xF    | 0x1  | [\#AppletEventType](#AppletEventType "wikilink")                                                                            |
| 0x10   | 0xC  | Unused                                                                                                                      |

Account:

| Offset | Size | Description                                                                                                        |
| ------ | ---- | ------------------------------------------------------------------------------------------------------------------ |
| 0x0    | 0x10 | userID                                                                                                             |
| 0x10   | 0x8  | titleID, when u8 +0x18 = 2.                                                                                        |
| 0x18   | 0x1  | Type. 0-1 to be listed by [\#QueryAccountEvent](#QueryAccountEvent "wikilink"), or 2 to include the above titleID. |
| 0x19   | 0x3  | Padding                                                                                                            |

PlayEventType PowerStateChange/OperationModeChange: u8 +0x0 is the input
value from
[\#NotifyOperationModeChangeEvent](#NotifyOperationModeChangeEvent "wikilink")/[\#NotifyPowerStateChangeEvent](#NotifyPowerStateChangeEvent "wikilink"),
the rest is unused.

# AccountEvent

| Offset | Size | Description                                |
| ------ | ---- | ------------------------------------------ |
| 0x0    | 0x10 | userID                                     |
| 0x10   | 0x4  | entryindex                                 |
| 0x14   | 0x4  | Padding                                    |
| 0x18   | 0x8  | [\#PlayEvent](#PlayEvent "wikilink") +0x20 |
| 0x20   | 0x8  | [\#PlayEvent](#PlayEvent "wikilink") +0x28 |
| 0x28   | 0x8  | [\#PlayEvent](#PlayEvent "wikilink") +0x30 |
| 0x30   | 0x1  | [\#PlayEvent](#PlayEvent "wikilink") +0x18 |
| 0x31   | 0x7  | Padding                                    |

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

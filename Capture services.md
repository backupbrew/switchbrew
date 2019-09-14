# caps:a

This is "nn::capsrv::sf::IAlbumAccessorService".

| Cmd   | Name                                                   |
| ----- | ------------------------------------------------------ |
| 0     | GetAlbumFileCount                                      |
| 1     | GetAlbumFileList                                       |
| 2     | LoadAlbumFile                                          |
| 3     | DeleteAlbumFile                                        |
| 4     | StorageCopyAlbumFile                                   |
| 5     | IsAlbumMounted                                         |
| 6     | GetAlbumUsage                                          |
| 7     | GetAlbumFileSize                                       |
| 8     | LoadAlbumFileThumbnail                                 |
| 9     | \[2.0.0+\] LoadAlbumScreenShotImage                    |
| 10    | \[2.0.0+\] LoadAlbumScreenShotThumbnailImage           |
| 11    | \[2.0.0+\] GetAlbumEntryFromApplicationAlbumEntry      |
| 12    | \[3.0.0+\] LoadAlbumScreenShotImageEx                  |
| 13    | \[3.0.0+\] LoadAlbumScreenShotThumbnailImageEx         |
| 14    | \[3.0.0+\] LoadAlbumScreenShotImageEx0                 |
| 15    | \[4.0.0+\] GetAlbumUsage3                              |
| 16    | \[4.0.0+\] GetAlbumMountResult                         |
| 17    | \[4.0.0+\] GetAlbumUsage16                             |
| 18    | \[6.0.0+\]                                             |
| 100   | \[5.0.0+\] GetAlbumFileCountEx0                        |
| 101   | \[5.0.0+\] GetAlbumFileListEx0                         |
| 202   | \[1.0.0-2.3.0\] SaveEditedScreenShot                   |
| 301   | GetLastOverlayScreenShotThumbnail                      |
| 302   | \[4.0.0+\] GetLastOverlayMovieThumbnail                |
| 401   | GetAutoSavingStorage                                   |
| 501   | GetRequiredStorageSpaceSizeToCopyAll                   |
| 1001  | \[3.0.0+\] LoadAlbumScreenShotThumbnailImageEx0        |
| 1002  | \[3.0.0+\] LoadAlbumScreenShotImageEx1                 |
| 1003  | \[4.0.0+\] LoadAlbumScreenShotThumbnailImageEx1        |
| 8001  | ForceAlbumUnmounted                                    |
| 8002  | ResetAlbumMountStatus                                  |
| 8011  | RefreshAlbumCache                                      |
| 8012  | GetAlbumCache                                          |
| 8013  | \[4.0.0+\] GetAlbumCacheEx                             |
| 8021  | \[2.0.0+\] GetAlbumEntryFromApplicationAlbumEntryAruid |
| 10011 | SetInternalErrorConversionEnabled                      |
| 50000 | \[6.0.0+\] LoadMakerNoteInfoForDebug                   |
| 60002 | \[4.0.0+\] OpenAccessorSession                         |

Cmd1002: Takes a total of 0x38-bytes of input, two type-0x5 input
buffers, and returns 0x20-bytes of output. \[4.0.0+\] No longer returns
output, and now takes the following buffers instead: type-0x16,
type-0x46, and type-0x6.

Cmd60002: Takes a total of 8-bytes of input, a PID, and returns an
[\#IAlbumAccessorSession](#IAlbumAccessorSession "wikilink").

## IAlbumAccessorSession

This is "nn::capsrv::sf::IAlbumAccessorSession".

This was added with \[4.0.0+\].

| Cmd  | Name                                      |
| ---- | ----------------------------------------- |
| 2001 | OpenAlbumMovieReadStream                  |
| 2002 | CloseAlbumMovieReadStream                 |
| 2003 | GetAlbumMovieReadStreamMovieDataSize      |
| 2004 | ReadMovieDataFromAlbumMovieReadStream     |
| 2005 | GetAlbumMovieReadStreamBrokenReason       |
| 2006 | GetAlbumMovieReadStreamImageDataSize      |
| 2007 | ReadImageDataFromAlbumMovieReadStream     |
| 2008 | ReadFileAttributeFromAlbumMovieReadStream |

# caps:c

This is "nn::capsrv::sf::IAlbumControlService", previously
"nn::capsrv::sf::ICaptureControllerService" with \[1.0.0\].

| Cmd                  | Name                                         | Notes                                                                                                               |
| -------------------- | -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| \[1.0.0\] 1          | CaptureRawImage                              |                                                                                                                     |
| \[1.0.0\] 2          | CaptureRawImageWithTimeout                   |                                                                                                                     |
| 33                   | \[7.0.0+\]                                   |                                                                                                                     |
| \[1.0.0\] 1001       | RequestTakingScreenShot                      |                                                                                                                     |
| \[1.0.0\] 1002       | RequestTakingScreenShotWithTimeout           |                                                                                                                     |
| \[1.0.0\] 1011       | NotifyTakingScreenShotRefused                |                                                                                                                     |
| 2001                 | NotifyAlbumStorageIsAvailable                |                                                                                                                     |
| 2002                 | NotifyAlbumStorageIsUnavailable              |                                                                                                                     |
| 2011                 | \[2.0.0+\] RegisterAppletResourceUserId      |                                                                                                                     |
| 2012                 | \[2.0.0+\] UnregisterAppletResourceUserId    |                                                                                                                     |
| 2013                 | \[2.0.0+\] GetApplicationIdFromAruid         |                                                                                                                     |
| 2014                 | \[2.0.0+\] CheckApplicationIdRegistered      |                                                                                                                     |
| 2101                 | \[2.0.0+\] GenerateCurrentAlbumFileId        | Takes an input u8 and u64, returns a 0x18-byte struct.                                                              |
| 2102                 | \[2.0.0+\] GenerateApplicationAlbumEnrty     |                                                                                                                     |
| \[2.0.0-3.0.2\] 2201 | SaveAlbumScreenShotFile                      |                                                                                                                     |
| 2202                 | \[4.0.0+\] SaveAlbumScreenShotFileEx         |                                                                                                                     |
| 2301                 | \[2.0.0+\] SetOverlayScreenShotThumbnailData |                                                                                                                     |
| 2302                 | \[4.0.0+\] SetOverlayMovieThumbnailData      |                                                                                                                     |
| 60001                | \[4.0.0+\] OpenControlSession                | Takes a total of 8-bytes of input and a PID, returns an [\#IAlbumControlSession](#IAlbumControlSession "wikilink"). |

### Cmd33

Takes an input u64
[\#ShimLibraryVersion](#ShimLibraryVersion "wikilink"), an u64
[AppletResourceUserId](Applet%20Manager%20services#AppletResourceUserId.md##AppletResourceUserId "wikilink"),
and a PID, no output.

This is used by [caps:su](Applet%20Manager%20services.md "wikilink")
SetShimLibraryVersion.

## IAlbumControlSession

This is "nn::capsrv::sf::IAlbumControlSession".

This was added with \[4.0.0+\].

| Cmd  | Name                                      | Notes |
| ---- | ----------------------------------------- | ----- |
| 2001 | OpenAlbumMovieReadStream                  |       |
| 2002 | CloseAlbumMovieReadStream                 |       |
| 2003 | GetAlbumMovieReadStreamMovieDataSize      |       |
| 2004 | ReadMovieDataFromAlbumMovieReadStream     |       |
| 2005 | GetAlbumMovieReadStreamBrokenReason       |       |
| 2006 | GetAlbumMovieReadStreamImageDataSize      |       |
| 2007 | ReadImageDataFromAlbumMovieReadStream     |       |
| 2008 | ReadFileAttributeFromAlbumMovieReadStream |       |
| 2401 | OpenAlbumMovieWriteStream                 |       |
| 2402 | FinishAlbumMovieWriteStream               |       |
| 2403 | CommitAlbumMovieWriteStream               |       |
| 2404 | DiscardAlbumMovieWriteStream              |       |
| 2405 | DiscardAlbumMovieWriteStreamNoDelete      |       |
| 2406 | \[7.0.0+\]                                |       |
| 2411 | StartAlbumMovieWriteStreamDataSection     |       |
| 2412 | EndAlbumMovieWriteStreamDataSection       |       |
| 2413 | StartAlbumMovieWriteStreamMetaSection     |       |
| 2414 | EndAlbumMovieWriteStreamMetaSection       |       |
| 2421 | ReadDataFromAlbumMovieWriteStream         |       |
| 2422 | WriteDataToAlbumMovieWriteStream          |       |
| 2424 | WriteMetaToAlbumMovieWriteStream          |       |
| 2431 | GetAlbumMovieWriteStreamBrokenReason      |       |
| 2433 | GetAlbumMovieWriteStreamDataSize          |       |
| 2434 | SetAlbumMovieWriteStreamDataSize          |       |

# caps:u

This is "nn::capsrv::sf::IAlbumApplicationService".

This was added with \[5.0.0+\].

Official sw via the `nn::album` wrappers uses start\_DateTime =
YYYY-MM-DD 1970-01-01 with the rest set to all-zero, end\_DateTime is
the same except year = 3000. With
[\#GetAlbumFileList0AafeAruidDeprecated](#GetAlbumFileList0AafeAruidDeprecated "wikilink"),
start\_PosixTime = UTC 1999-12-31 00:00 (0x386BF200), and end\_PosixTime
= UTC 2100-01-01 00:00 (0xF4865700).

| Cmd   | Name                                                                                                        |
| ----- | ----------------------------------------------------------------------------------------------------------- |
| 32    | \[7.0.0+\] [\#SetShimLibraryVersion](#SetShimLibraryVersion "wikilink")                                     |
| 102   | [\#GetAlbumFileList0AafeAruidDeprecated](#GetAlbumFileList0AafeAruidDeprecated "wikilink")                  |
| 103   | [\#DeleteAlbumFileByAruid](#DeleteAlbumFileByAruid "wikilink")                                              |
| 104   | [\#GetAlbumFileSizeByAruid](#GetAlbumFileSizeByAruid "wikilink")                                            |
| 105   | [\#DeleteAlbumFileByAruidForDebug](#DeleteAlbumFileByAruidForDebug "wikilink")                              |
| 110   | [\#LoadAlbumScreenShotImageByAruid](#LoadAlbumScreenShotImageByAruid "wikilink")                            |
| 120   | [\#LoadAlbumScreenShotThumbnailImageByAruid](#LoadAlbumScreenShotThumbnailImageByAruid "wikilink")          |
| 130   | [\#PrecheckToCreateContentsByAruid](#PrecheckToCreateContentsByAruid "wikilink")                            |
| 140   | \[6.0.0+\] [\#GetAlbumFileList1AafeAruidDeprecated](#GetAlbumFileList1AafeAruidDeprecated "wikilink")       |
| 141   | \[6.0.0+\] [\#GetAlbumFileList2AafeUidAruidDeprecated](#GetAlbumFileList2AafeUidAruidDeprecated "wikilink") |
| 142   | \[7.0.0+\] [\#GetAlbumFileList3AaeAruid](#GetAlbumFileList3AaeAruid "wikilink")                             |
| 143   | \[7.0.0+\] [\#GetAlbumFileList4AaeUidAruid](#GetAlbumFileList4AaeUidAruid "wikilink")                       |
| 60002 | [\#OpenAccessorSessionForApplication](#OpenAccessorSessionForApplication "wikilink")                        |

## SetShimLibraryVersion

Takes an input u64
[\#ShimLibraryVersion](#ShimLibraryVersion "wikilink"), an u64
[AppletResourceUserId](Applet%20Manager%20services#AppletResourceUserId.md##AppletResourceUserId "wikilink"),
and a PID, no output.

## GetAlbumFileList0AafeAruidDeprecated

Takes a type-0x6 output buffer containing an array of
[\#ApplicationAlbumFileEntry](#ApplicationAlbumFileEntry "wikilink"), a
PID, an u8 [\#ContentType](#ContentType "wikilink"), two s64s, and an
u64
[AppletResourceUserId](Applet%20Manager%20services#AppletResourceUserId.md##AppletResourceUserId "wikilink").
Returns an output u64 for total output entries.

The two s64s are the start/end PosixTime.

## DeleteAlbumFileByAruid

Takes a PID, an input u8 [\#ContentType](#ContentType "wikilink"), an
[\#ApplicationAlbumFileEntry](#ApplicationAlbumFileEntry "wikilink"), an
[AppletResourceUserId](Applet%20Manager%20services#AppletResourceUserId.md##AppletResourceUserId "wikilink"),
and no output.

The [\#ContentType](#ContentType "wikilink") must match 3.

## GetAlbumFileSizeByAruid

Takes a PID, an input
[\#ApplicationAlbumFileEntry](#ApplicationAlbumFileEntry "wikilink"), an
[AppletResourceUserId](Applet%20Manager%20services#AppletResourceUserId.md##AppletResourceUserId "wikilink"),
and returns an output u64.

This gets the filesize for the entire specified Album file.

## DeleteAlbumFileByAruidForDebug

Takes a PID, an
[\#ApplicationAlbumFileEntry](#ApplicationAlbumFileEntry "wikilink"), an
[AppletResourceUserId](Applet%20Manager%20services#AppletResourceUserId.md##AppletResourceUserId "wikilink"),
and no output.

The cached value loaded from
[Settings\_services\#GetDebugModeFlag](Settings%20services#GetDebugModeFlag.md##GetDebugModeFlag "wikilink")
must be 1, otherwise an error is returned.

## LoadAlbumScreenShotImageByAruid

Takes a PID, a type-0x16 output buffer containing a
[\#LoadAlbumScreenShotImageOutputForApplication](#LoadAlbumScreenShotImageOutputForApplication "wikilink"),
a type-0x46 output buffer, a type-0x6 output buffer, an
[\#ApplicationAlbumFileEntry](#ApplicationAlbumFileEntry "wikilink"), a
[\#ScreenShotDecodeOption](#ScreenShotDecodeOption "wikilink"), and no
output.

The type-0x46 buffer contains the RGBA8 image data. The type-0x6 buffer
is a work buffer used for reading the entire AlbumFile, the buffer size
must be at least the AlbumFile filesize (cleared before the cmd
returns).

## LoadAlbumScreenShotThumbnailImageByAruid

Takes a PID, a type-0x16 output buffer containing a
[\#LoadAlbumScreenShotImageOutputForApplication](#LoadAlbumScreenShotImageOutputForApplication "wikilink"),
a type-0x46 output buffer, a type-0x6 output buffer, an
[\#ApplicationAlbumFileEntry](#ApplicationAlbumFileEntry "wikilink"), a
[\#ScreenShotDecodeOption](#ScreenShotDecodeOption "wikilink"), and no
output.

The type-0x46 buffer contains the RGBA8 image data. The type-0x6 buffer
is a work buffer used for reading the entire AlbumFile, the buffer size
must be at least the AlbumFile filesize (cleared before the cmd
returns).

## PrecheckToCreateContentsByAruid

Takes a PID, an input u8 [\#ContentType](#ContentType "wikilink"), an
u64, an
[AppletResourceUserId](Applet%20Manager%20services#AppletResourceUserId.md##AppletResourceUserId "wikilink"),
and no output.

## GetAlbumFileList1AafeAruidDeprecated

Takes a type-0x6 output buffer containing an array of
[\#ApplicationAlbumFileEntry](#ApplicationAlbumFileEntry "wikilink"), a
PID, an u8 [\#ContentType](#ContentType "wikilink"), two
[\#AlbumFileDateTime](#AlbumFileDateTime "wikilink"), and an u64
[AppletResourceUserId](Applet%20Manager%20services#AppletResourceUserId.md##AppletResourceUserId "wikilink").
Returns an output u64 for total output entries.

The first [\#AlbumFileDateTime](#AlbumFileDateTime "wikilink") is the
start\_DateTime, the second
[\#AlbumFileDateTime](#AlbumFileDateTime "wikilink") is the
end\_DateTime. In the IPC rawdata, these use 2-byte alignment.

## GetAlbumFileList2AafeUidAruidDeprecated

Takes a type-0x6 output buffer containing an array of
[\#ApplicationAlbumFileEntry](#ApplicationAlbumFileEntry "wikilink"), a
PID, an u8 [\#ContentType](#ContentType "wikilink"), two
[\#AlbumFileDateTime](#AlbumFileDateTime "wikilink"), an u128 userID,
and an u64
[AppletResourceUserId](Applet%20Manager%20services#AppletResourceUserId.md##AppletResourceUserId "wikilink").
Returns an output u64 for total output entries.

The first [\#AlbumFileDateTime](#AlbumFileDateTime "wikilink") is the
start\_DateTime, the second
[\#AlbumFileDateTime](#AlbumFileDateTime "wikilink") is the
end\_DateTime. In the IPC rawdata, these use 2-byte alignment.

## GetAlbumFileList3AaeAruid

Takes a type-0x6 output buffer containing an array of
[\#ApplicationAlbumEntry](#ApplicationAlbumEntry "wikilink"), a PID, an
u8 [\#ContentType](#ContentType "wikilink"), two
[\#AlbumFileDateTime](#AlbumFileDateTime "wikilink"), and an u64
[AppletResourceUserId](Applet%20Manager%20services#AppletResourceUserId.md##AppletResourceUserId "wikilink").
Returns an output u64 for total output entries.

The first [\#AlbumFileDateTime](#AlbumFileDateTime "wikilink") is the
start\_DateTime, the second
[\#AlbumFileDateTime](#AlbumFileDateTime "wikilink") is the
end\_DateTime. In the IPC rawdata, these use 2-byte alignment.

## GetAlbumFileList4AaeUidAruid

Takes a type-0x6 output buffer containing an array of
[\#ApplicationAlbumEntry](#ApplicationAlbumEntry "wikilink"), a PID, an
u8 [\#ContentType](#ContentType "wikilink"), two
[\#AlbumFileDateTime](#AlbumFileDateTime "wikilink"), an u128 userID,
and an u64
[AppletResourceUserId](Applet%20Manager%20services#AppletResourceUserId.md##AppletResourceUserId "wikilink").
Returns an output u64 for total output entries.

The first [\#AlbumFileDateTime](#AlbumFileDateTime "wikilink") is the
start\_DateTime, the second
[\#AlbumFileDateTime](#AlbumFileDateTime "wikilink") is the
end\_DateTime. In the IPC rawdata, these use 2-byte alignment.

## OpenAccessorSessionForApplication

Takes a PID, an input
[\#ApplicationAlbumFileEntry](#ApplicationAlbumFileEntry "wikilink"), an
u64
[AppletResourceUserId](Applet%20Manager%20services#AppletResourceUserId.md##AppletResourceUserId "wikilink"),
and returns an output
[\#IAlbumAccessorApplicationSession](#IAlbumAccessorApplicationSession "wikilink").

## IAlbumAccessorApplicationSession

This is "nn::capsrv::sf::IAlbumAccessorApplicationSession".

This was added with \[5.0.0+\].

This is opened prior to using
[\#OpenAlbumMovieReadStream](#OpenAlbumMovieReadStream "wikilink"), when
it previously wasn't opened. Official sw only closes this session when
closing caps:u, not when using
[\#CloseAlbumMovieReadStream](#CloseAlbumMovieReadStream "wikilink").

| Cmd  | Name                                                                                         |
| ---- | -------------------------------------------------------------------------------------------- |
| 2001 | [\#OpenAlbumMovieReadStream](#OpenAlbumMovieReadStream "wikilink")                           |
| 2002 | [\#CloseAlbumMovieReadStream](#CloseAlbumMovieReadStream "wikilink")                         |
| 2003 | [\#GetAlbumMovieReadStreamMovieDataSize](#GetAlbumMovieReadStreamMovieDataSize "wikilink")   |
| 2004 | [\#ReadMovieDataFromAlbumMovieReadStream](#ReadMovieDataFromAlbumMovieReadStream "wikilink") |
| 2005 | [\#GetAlbumMovieReadStreamBrokenReason](#GetAlbumMovieReadStreamBrokenReason "wikilink")     |

### OpenAlbumMovieReadStream

Takes a PID, an input
[\#ApplicationAlbumFileEntry](#ApplicationAlbumFileEntry "wikilink"), an
u64
[AppletResourceUserId](Applet%20Manager%20services#AppletResourceUserId.md##AppletResourceUserId "wikilink"),
and returns an output u64
[\#AlbumMovieReadStreamHandle](#AlbumMovieReadStreamHandle "wikilink").

Up to 4 streams can be open at the same time. Multiple streams can be
open at the same time for the same
[\#ApplicationAlbumFileEntry](#ApplicationAlbumFileEntry "wikilink").

### CloseAlbumMovieReadStream

Takes an input u64
[\#AlbumMovieReadStreamHandle](#AlbumMovieReadStreamHandle "wikilink"),
no output.

### GetAlbumMovieReadStreamMovieDataSize

Takes an input u64
[\#AlbumMovieReadStreamHandle](#AlbumMovieReadStreamHandle "wikilink"),
returns an output u64.

This gets the size of the actual MP4, without the JPEG at the end.

### ReadMovieDataFromAlbumMovieReadStream

Takes a type-0x6 output buffer, an input u64
[\#AlbumMovieReadStreamHandle](#AlbumMovieReadStreamHandle "wikilink"),
an input s64 offset, and returns an output u64 actual\_size.

offset(+size) must not be negative. offset and size must be aligned to
0x40000-bytes. When offset(+size) goes beyond the size from
[\#GetAlbumMovieReadStreamMovieDataSize](#GetAlbumMovieReadStreamMovieDataSize "wikilink"),
the regions of the buffer which goes beyond that are cleared to 0, and
actual\_size is still set to the input size.

### GetAlbumMovieReadStreamBrokenReason

Takes an input u64
[\#AlbumMovieReadStreamHandle](#AlbumMovieReadStreamHandle "wikilink"),
no output.

Unused by official sw.

# ShimLibraryVersion

This is a version field. Official sw uses func
`nn::capsrv::GetShimLibraryVersion()` to load this from a global var,
which is then used with various commands (the input for those cmds must
match value 1).

\[7.0.0-9.0.0\] This is value 1.

Controls which struct version to use for
[\#ApplicationAlbumEntry](#ApplicationAlbumEntry "wikilink") /
[\#AlbumFileEntry](#AlbumFileEntry "wikilink"). However, the struct size
for the newer version is used regardless on \[7.0.0+\] for the actual
cmds.

# Enums

### AlbumImageOrientation

| Value | Description |
| ----- | ----------- |
| 0     | Unknown.    |
| 1     | Unknown.    |
| 2     | Unknown.    |
| 3     | Unknown.    |

This is "nn::album::ImageOrientation".

### AlbumReportOption

| Value | Description                                                     |
| ----- | --------------------------------------------------------------- |
| 0     | Don't display the screenshot-taken Overlay-applet notification. |
| 1     | Display the screenshot-taken Overlay notification.              |

This is "nn::album::AlbumReportOption".

### ContentType

| Value | Description                                                                                                                               |
| ----- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| 0     | Screenshot. Album screenshots.                                                                                                            |
| 1     | Movie. Album videos.                                                                                                                      |
| 3     | ExtraMovie. Videos recorded by the current Application title via [GRC MovieMaker](GRC%20services#IMovieMaker.md##IMovieMaker "wikilink"). |

# AlbumFileDateTime

| Offset | Size | Description                                                              |
| ------ | ---- | ------------------------------------------------------------------------ |
| 0x0    | 0x2  | Year                                                                     |
| 0x2    | 0x1  | Month                                                                    |
| 0x3    | 0x1  | Day                                                                      |
| 0x4    | 0x1  | Hour                                                                     |
| 0x5    | 0x1  | Minute                                                                   |
| 0x6    | 0x1  | Second                                                                   |
| 0x7    | 0x1  | Unique ID for when there's multiple Album files with the same timestamp. |

This is "nn::capsrv::AlbumFileDateTime". This is a 0x8-byte struct.

This corresponds to each field in the Album entry filename, prior to the
"-": `YYYYMMDDHHMMSSII`.

# AlbumEntry

| Offset | Size | Description                                          |
| ------ | ---- | ---------------------------------------------------- |
| 0x0    | 0x8  | Unknown                                              |
| 0x8    | 0x8  | titleID                                              |
| 0x10   | 0x8  | [\#AlbumFileDateTime](#AlbumFileDateTime "wikilink") |
| 0x18   | 0x1  | Unknown                                              |
| 0x19   | 0x1  | Unknown                                              |
| 0x1A   | 0x6  | Padding?                                             |

This is "nn::capsrv::AlbumEntry". This is a 0x20-byte struct.

# AlbumFileEntry

This is "nn::album::AlbumFileEntry". This is identical to
[\#ApplicationAlbumEntry](#ApplicationAlbumEntry "wikilink"). On older
versions where official sw used to use cmds which use
[\#ApplicationAlbumFileEntry](#ApplicationAlbumFileEntry "wikilink"),
this struct matches
[\#ApplicationAlbumFileEntry](#ApplicationAlbumFileEntry "wikilink").

# ApplicationAlbumEntry

| Offset | Size | Description                                          |
| ------ | ---- | ---------------------------------------------------- |
| 0x0    | 0x8  | Unknown.                                             |
| 0x8    | 0x8  | Unknown.                                             |
| 0x10   | 0x8  | [\#AlbumFileDateTime](#AlbumFileDateTime "wikilink") |
| 0x18   | 0x8  | Unknown.                                             |

This is "nn::capsrv::ApplicationAlbumEntry". This is a 0x20-byte struct.
On older versions where
[\#ShimLibraryVersion](#ShimLibraryVersion "wikilink") is 0, this has a
different format.

With the output from
[caps:su](Applet%20Manager%20services#caps:su.md##caps:su "wikilink")
sdk-nso only uses this for the
[Share-applet](Internet%20Browser.md "wikilink") (when the output is
used at all), with everything else it's used as an
[\#AlbumFileEntry](#AlbumFileEntry "wikilink"). In those cases with the
`nn::album` wrapper funcs, it's "converted" by just copying the struct
(arrays are "converted" by just returning a ptr to the input array).

# ApplicationAlbumFileEntry

| Offset | Size | Description                                                  |
| ------ | ---- | ------------------------------------------------------------ |
| 0x0    | 0x20 | [\#ApplicationAlbumEntry](#ApplicationAlbumEntry "wikilink") |
| 0x20   | 0x8  | [\#AlbumFileDateTime](#AlbumFileDateTime "wikilink")         |
| 0x28   | 0x8  | Unknown.                                                     |

This is "nn::capsrv::ApplicationAlbumFileEntry". This is a 0x30-byte
struct.

On newer versions where official sw uses
[\#ApplicationAlbumEntry](#ApplicationAlbumEntry "wikilink"),
[\#ApplicationAlbumEntry](#ApplicationAlbumEntry "wikilink") is
converted to ApplicationAlbumFileEntry when using cmds which need it
with:

  - First 0x20-bytes are the same.
  - u64 ApplicationAlbumFileEntry+0x20 =
    [\#ApplicationAlbumEntry](#ApplicationAlbumEntry "wikilink")+0x10.
  - Last 8-bytes = 0.

# ScreenShotAttribute

| Offset | Size | Description                                                  |
| ------ | ---- | ------------------------------------------------------------ |
| 0x0    | 0x4  | Always set to 0 by official sw.                              |
| 0x4    | 0x4  | [\#AlbumImageOrientation](#AlbumImageOrientation "wikilink") |
| 0x8    | 0x4  | Always set to 0 by official sw.                              |
| 0xC    | 0x4  | Always set to 1 by official sw.                              |
| 0x10   | 0x30 | Always set to 0 by official sw.                              |

This is "nn::capsrv::detail::ScreenShotAttributeEx0" /
"nn::capsrv::ScreenShotAttribute". This is a 0x40-byte struct.

# ApplicationData

| Offset | Size  | Description    |
| ------ | ----- | -------------- |
| 0x0    | 0x400 | UserData       |
| 0x400  | 0x4   | UserData size. |

This is "nn::capsrv::ApplicationData". This is a 0x404-byte struct.

# UserIdList

| Offset | Size | Description    |
| ------ | ---- | -------------- |
| 0x0    | 0x80 | u128 userIDs   |
| 0x80   | 0x1  | Total userIDs. |
| 0x81   | 0x7  | Padding.       |

This is "nn::capsrv::UserIdList". This is a 0x88-byte struct.

# LoadAlbumScreenShotImageOutputForApplication

| Offset | Size  | Description                                                                          |
| ------ | ----- | ------------------------------------------------------------------------------------ |
| 0x0    | 0x8   | s64 Width. Official sw copies this to a s32 output field.                            |
| 0x8    | 0x8   | s64 Height. Official sw copies this to a s32 output field.                           |
| 0x10   | 0x40  | [\#ScreenShotAttributeForApplication](#ScreenShotAttributeForApplication "wikilink") |
| 0x50   | 0x404 | [\#ApplicationData](#ApplicationData "wikilink")                                     |
| 0x454  | 0xAC  | Unused                                                                               |

This is "nn::capsrv::sf::LoadAlbumScreenShotImageOutputForApplication".
This is a 0x500-byte struct.

# ScreenShotDecodeOption

This is "nn::capsrv::ScreenShotDecodeOption". This is a 0x20-byte
struct.

Official sw sets this to all-zero with the input for
[\#LoadAlbumScreenShotImageByAruid](#LoadAlbumScreenShotImageByAruid "wikilink")/[\#LoadAlbumScreenShotThumbnailImageByAruid](#LoadAlbumScreenShotThumbnailImageByAruid "wikilink").

# ScreenShotAttributeForApplication

| Offset | Size | Description  |
| ------ | ---- | ------------ |
| 0x0    | 0x4  | Unknown.     |
| 0x4    | 0x1  | Unknown.     |
| 0x5    | 0x1  | Unknown.     |
| 0x6    | 0x1  | Unknown.     |
| 0x7    | 0x1  | Padding.     |
| 0x8    | 0x4  | Unknown.     |
| 0xC    | 0x4  | Unknown.     |
| 0x10   | 0x4  | Unknown.     |
| 0x14   | 0x4  | Unknown.     |
| 0x18   | 0x4  | Unknown.     |
| 0x1C   | 0x4  | Unknown.     |
| 0x20   | 0x2  | Unknown.     |
| 0x22   | 0x2  | Unknown.     |
| 0x24   | 0x2  | Unknown.     |
| 0x26   | 0x2  | Unknown.     |
| 0x28   | 0x18 | Always zero. |

This is "nn::capsrv::ScreenShotAttributeForApplication". This is a
0x40-byte struct.

Official sw only uses this in `nn::album` funcs which convert this to
[\#AlbumFileAttribute](#AlbumFileAttribute "wikilink"), with the output
from
[\#LoadAlbumScreenShotImageByAruid](#LoadAlbumScreenShotImageByAruid "wikilink")/[\#LoadAlbumScreenShotThumbnailImageByAruid](#LoadAlbumScreenShotThumbnailImageByAruid "wikilink")
(only the first u32 is used).

# AlbumFileAttribute

| Offset | Size | Description                                                                                                                                                                               |
| ------ | ---- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x8  | The `nn::album` funcs referenced by [\#ScreenShotAttributeForApplication](#ScreenShotAttributeForApplication "wikilink") set this to: `ScreenShotAttributeForApplication.first_u32 == 2`. |
| 0x8    | 0x8  | Set to zero by official sw.                                                                                                                                                               |

This is "nn::album::AlbumFileAttribute". This is a 0x10-byte struct. See
also
[\#ScreenShotAttributeForApplication](#ScreenShotAttributeForApplication "wikilink").

# AlbumMovieReadStreamHandle

This is "nn::capsrv::AlbumMovieReadStreamHandle" /
"nn::album::MovieStreamHandle".

This is an u64 stream handle.

# Notes

capsrv is responsible for validating the MACs for screenshots stored on
the SD card, if the setting
capsrv\!enable\_album\_screenshot\_filedata\_verification is non-zero.

Screenshots are validated as follows: The JPEG's MAC is extracted from
the EXIF maker note, and stored. A timestamp string is generated by
calling snprintf(\&str, 20, "%04d:%02d:%02d %02d:%02d:%02d", ...); with
stored timestamp values. If this doesn't match the timestamp string
stored in EXIF, then an error 0xA34CE is returned. Otherwise, the entire
JPEG is loaded into memory, and the stored EXIF maker note is cleared to
zeroes. Then, an HMAC-SHA256 is computed over the entire JPEG using a
hardcoded secret key. if (memcmp(calculated\_hmac, stored\_hmac, 0x10)
== 0), the screenshot is valid, else 0xA3ACE is returned.

In [3.0.0](3.0.0.md "wikilink"), MAC calculation was changed: now,
instead of calculating an HMAC, a plain SHA256 hash is calculated.
capsrv basically does screenshot\_kek =
spl::GenerateAesKek(<hardcoded screenshot_kek_source>);
spl::LoadAesKey(screenshot\_kek, <hardcoded screenshot_key_source>); MAC
= spl::ComputeCmac(hash);

## Videos

[4.0.0](4.0.0.md "wikilink") includes video playback etc support in
Album via mp4. These include a JPEG thumbnail, which is used for video
"validation". The EXIF is also much larger: the MakerNote is
0x498-bytes, with encrypted data starting at offset +0x8. This
encryption uses AES-CTR with hardcoded key/ctr. MAC calculation works
the same way as the [3.0.0](3.0.0.md "wikilink")+ JPEG MAC calculation,
except with a different movie\_kek\_source/movie\_key\_source.

Note: the Album process itself uses libstagefright for video playback.

[Category:Services](Category:Services "wikilink")

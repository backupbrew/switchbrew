GRC (Game Recording) uses libstagefright and the NvMMLite TVMR library
for writing [recorded](4.0.0.md "wikilink") video to MP4s.

Error reporting is done using the new
[/dev/nverpt-ctrl](NV%20services#%20dev%20nverpt-ctrl.md##/dev/nverpt-ctrl "wikilink")
ioctls.

# grc:c

This is "nn::grcsrv::IGrcService".

| Cmd  | Name                   | Notes                                                                                                                   |
| ---- | ---------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| 1    | OpenContinuousRecorder | Takes a total of 0x28-bytes of input and a handle, returns an [\#IContinuousRecorder](#IContinuousRecorder "wikilink"). |
| 2    | OpenGameMovieTrimmer   | Takes an input u64 and a handle, returns an [\#IGameMovieTrimmer](#IGameMovieTrimmer "wikilink").                       |
| 3    | \[5.0.0+\]             | Takes a total of 0x8-bytes of input and a handle, returns an [\#IOffscreenRecorder](#IOffscreenRecorder "wikilink").    |
| 101  | \[5.0.0+\]             | Takes a total of 0x10-bytes of input, returns an [\#IMovieMaker](#IMovieMaker "wikilink").                              |
| 9903 | \[5.0.0+\]             | Takes 8-bytes of input, no output.                                                                                      |

\[5.0.0+\] OpenContinuousRecorder now takes an additional 0x20-bytes of
input.

## IContinuousRecorder

This is "nn::grcsrv::IContinuousRecorder".

| Cmd | Name       |
| --- | ---------- |
| 1   |            |
| 2   |            |
| 10  |            |
| 11  |            |
| 12  |            |
| 13  |            |
| 14  | \[5.0.0+\] |

\[5.0.0+\] Cmd11 now takes a total of 0x40-bytes of input.

\[8.0.0+\] Cmd11/cmd14 no longer take any rawdata input, these now take
a type-0x15 input buffer.

## IGameMovieTrimmer

This is "nn::grcsrv::IGameMovieTrimmer".

| Cmd | Name                                                     |
| --- | -------------------------------------------------------- |
| 1   | [\#BeginTrim](#BeginTrim "wikilink")                     |
| 2   | [\#EndTrim](#EndTrim "wikilink")                         |
| 10  | [\#GetNotTrimmingEvent](#GetNotTrimmingEvent "wikilink") |
| 20  | [\#SetThumbnailRgba](#SetThumbnailRgba "wikilink")       |

Album uses
[CreateGameMovieTrimmer](Applet%20Manager%20services#CreateGameMovieTrimmer.md##CreateGameMovieTrimmer "wikilink"),
and retries using the cmd in a loop on error 0x8D4 with
svcSleepThread(100000000) being used first. Then all 4 of these commands
are used in that same func:
[\#SetThumbnailRgba](#SetThumbnailRgba "wikilink") if the input buffer
is set, [\#GetNotTrimmingEvent](#GetNotTrimmingEvent "wikilink"),
[\#BeginTrim](#BeginTrim "wikilink"), waits on the event, then
[\#EndTrim](#EndTrim "wikilink") and cleanup.

### BeginTrim

Takes an input s32 **start**, a s32 **end**, and a
[\#GameMovieId](#GameMovieId "wikilink"), no output.

The two s32s are the start/end timestamps in 0.5s units.

### EndTrim

No input, returns an output [\#GameMovieId](#GameMovieId "wikilink").

This just loads the [\#GameMovieId](#GameMovieId "wikilink") from state,
when available.

### GetNotTrimmingEvent

No input, returns an output Event handle with autoclear=false.

### SetThumbnailRgba

Takes a type-0x45 input buffer, a s32 **width**, and a s32 **height**,
no output.

**width** must be 1280, **height** must be 720, and the buffer size must
be at least 0x384000. After this validation, this just copies the input
buffer to state with size 0x384000 and returns 0.

# grc:d

This is "nn::grcsrv::IRemoteVideoTransfer".

Added with [6.0.0](6.0.0.md "wikilink").

| Cmd | Name | Notes                                                                                                         |
| --- | ---- | ------------------------------------------------------------------------------------------------------------- |
| 1   |      | No input/output.                                                                                              |
| 2   |      | Takes an input u32 (must be value 0-1) and a type-0x6 output buffer, returns a total of 0x10-bytes of output. |

## Cmd1

Begins video stream. This must not be used more than once, even from a
different service session: otherwise the sysmodule will assert.

## Cmd2

Retrieves stream data, from the video recording being done of the
currently running game title. Takes u32 "stream" (0: video, 1: audio),
returns u32 (num\_frames?), u32 data\_size, u64 (start\_timestamp?).
Video stream writes H.264 NAL units to the output buffer (try `ffplay -f
h264`). Audio stream is PCM16, 2 channels, and sample-rate = 48000Hz.
Official code uses buffer size 0x32000 for video, 0x1000 for audio, and
multiple threads to read out both streams at the same time.

This will block until data is available. This will hang if there is no
game title running which has video capture enabled.

# IOffscreenRecorder

This is "nn::grcsrv::IOffscreenRecorder".

This was added with \[5.0.0+\].

| Cmd | Name | Notes                                                                        |
| --- | ---- | ---------------------------------------------------------------------------- |
| 201 |      | Takes a total of 0x8-bytes of input, returns a total of 0x8-bytes of output. |
| 202 |      | Takes a total of 0x8-bytes of input, no output.                              |

# IMovieMaker

This is "nn::grcsrv::IMovieMaker".

This was added with \[5.0.0+\].

| Cmd | Name                                                                                                   |
| --- | ------------------------------------------------------------------------------------------------------ |
| 2   | [\#CreateVideoProxy](#CreateVideoProxy "wikilink")                                                     |
| 9   | \[7.0.0+\] [\#SetAlbumShimLibraryVersion](#SetAlbumShimLibraryVersion "wikilink")                      |
| 10  | [\#OpenOffscreenLayer](#OpenOffscreenLayer "wikilink")                                                 |
| 11  | [\#CloseOffscreenLayer](#CloseOffscreenLayer "wikilink")                                               |
| 20  | [\#StartOffscreenRecording](#StartOffscreenRecording "wikilink")                                       |
| 21  | [\#AbortOffscreenRecording](#AbortOffscreenRecording "wikilink")                                       |
| 22  | [\#RequestOffscreenRecordingFinishReady](#RequestOffscreenRecordingFinishReady "wikilink")             |
| 23  | [\#CompleteOffscreenRecordingFinish](#CompleteOffscreenRecordingFinish "wikilink")                     |
| 24  | [\#StartOffscreenRecordingEx](#StartOffscreenRecordingEx "wikilink")                                   |
| 25  | [\#CompleteOffscreenRecordingFinishEx0](#CompleteOffscreenRecordingFinishEx0 "wikilink")               |
| 26  | \[7.0.0+\] [\#CompleteOffscreenRecordingFinishEx1](#CompleteOffscreenRecordingFinishEx1 "wikilink")    |
| 30  | [\#GetOffscreenLayerError](#GetOffscreenLayerError "wikilink")                                         |
| 41  | [\#EncodeOffscreenLayerAudioSample](#EncodeOffscreenLayerAudioSample "wikilink")                       |
| 50  | [\#GetOffscreenLayerRecordingFinishReadyEvent](#GetOffscreenLayerRecordingFinishReadyEvent "wikilink") |
| 52  | [\#GetOffscreenLayerAudioEncodeReadyEvent](#GetOffscreenLayerAudioEncodeReadyEvent "wikilink")         |

## CreateVideoProxy

No input, returns an [\#IHOSBinderDriver](#IHOSBinderDriver "wikilink").

## SetAlbumShimLibraryVersion

Takes an input u64
[ShimLibraryVersion](Capture%20services#ShimLibraryVersion.md##ShimLibraryVersion "wikilink"),
no output.

## OpenOffscreenLayer

Takes an input u64 **LayerHandle**, returns an output s32 **ID**.

This gets the **ID** for the
[\#IHOSBinderDriver](#IHOSBinderDriver "wikilink") returned by
[\#CreateVideoProxy](#CreateVideoProxy "wikilink").

## CloseOffscreenLayer

Takes an input u64 **LayerHandle**, no output.

## StartOffscreenRecording

Takes an input u64, no output.

Seems to be unused by official user processes,
[\#StartOffscreenRecordingEx](#StartOffscreenRecordingEx "wikilink") is
used instead.

## AbortOffscreenRecording

Takes an input u64 **LayerHandle**, no output.

## RequestOffscreenRecordingFinishReady

Takes an input u64 **LayerHandle**, no output.

This is the first cmd used by official sw when finishing recording. Then
it waits on the Event originally loaded from
[\#GetOffscreenLayerRecordingFinishReadyEvent](#GetOffscreenLayerRecordingFinishReadyEvent "wikilink").
Then CompleteOffscreenRecordingFinishEx\* is used, depending on the
sdk-nso version. On any errors,
[\#AbortOffscreenRecording](#AbortOffscreenRecording "wikilink") is
used.

## StartOffscreenRecordingEx

Takes an input u64 **LayerHandle** and an
[\#OffscreenRecordingParameter](#OffscreenRecordingParameter "wikilink"),
no output.

## CompleteOffscreenRecordingFinish

Takes an input u64 **LayerHandle** and a type-0x5 input buffer, no
output.

Seems to be unused by official user processes,
[\#CompleteOffscreenRecordingFinishEx0](#CompleteOffscreenRecordingFinishEx0 "wikilink")
is used instead.

The input buffer contains the optional ApplicationData for the JPEG
thumbnail, size must be \<=0x400.

The recorded video will not be accessible via the Album-applet since
it's stored separately from other Album data.

## CompleteOffscreenRecordingFinishEx0

Takes two input s32s **width**/**height**, an input u64 **LayerHandle**
and 2 type-0x5 input buffers, no output.

The input buffers are optional, addr=NULL and size=0 can be used for
these. The first buffer is for
[ApplicationData](#CompleteOffscreenRecordingFinish "wikilink"), the
second buffer buffer contains the RGBA8 image thumbnail.

**width**/**height** must be 1280x720, these fields are unused
afterwards.

Besides **width**/**height**, this is the same as
[\#CompleteOffscreenRecordingFinish](#CompleteOffscreenRecordingFinish "wikilink")
except the second buffer is user-specified instead of addr=NULL/size=0.

## CompleteOffscreenRecordingFinishEx1

Takes two input s32s **width**/**height**, an input u64 **LayerHandle**
and two type-0x5 input buffers, returns an output
[ApplicationAlbumEntry](Capture%20services.md "wikilink").

Same as
[\#CompleteOffscreenRecordingFinishEx0](#CompleteOffscreenRecordingFinishEx0 "wikilink")
except the output struct is returned in the cmdreply. Official sw copies
the output struct into a "nn::album::AlbumFileEntry".

## GetOffscreenLayerError

Takes an input u64 **LayerHandle**, no output.

## EncodeOffscreenLayerAudioSample

Takes an input u64 **LayerHandle** and a type-0x5 input buffer, returns
an output u64 **out\_size**.

Official sw enters a loop for handling the user-specified buffer:

  - Waits on the Event originally loaded from
    [\#GetOffscreenLayerAudioEncodeReadyEvent](#GetOffscreenLayerAudioEncodeReadyEvent "wikilink").
  - Uses the cmd with the current buffer\_addr+pos and the
    remaining\_size.
  - Updates the current pos and remaining\_size with the **out\_size**.
  - Repeats the loop until the remaining\_size is 0.

## GetOffscreenLayerRecordingFinishReadyEvent

Takes an input u64 **LayerHandle**, returns an output event handle with
autoclear disabled.

## GetOffscreenLayerAudioEncodeReadyEvent

Takes an input u64 **LayerHandle**, returns an output event handle with
autoclear disabled.

# OffscreenRecordingParameter

| Offset | Size | Description                                          | Default value                    |
| ------ | ---- | ---------------------------------------------------- | -------------------------------- |
| 0x0    | 0x10 | ?                                                    | 0                                |
| 0x10   | 0x4  | ?                                                    | 0x103                            |
| 0x14   | 0x4  | s32 VideoBitRate                                     | 8000000                          |
| 0x18   | 0x4  | s32 VideoWidth                                       | 1280                             |
| 0x1C   | 0x4  | s32 VideoHeight                                      | 720                              |
| 0x20   | 0x4  | s32 VideoFrameRate                                   | 30                               |
| 0x24   | 0x4  | s32 VideoKeyFrameInterval                            | 30                               |
| 0x28   | 0x4  | s32 AudioBitRate                                     | 128000 (\[5.0.0-5.1.0\] 1536000) |
| 0x2C   | 0x4  | s32 AudioSampleRate                                  | 48000                            |
| 0x30   | 0x4  | s32 AudioChannelCount                                | 2                                |
| 0x34   | 0x4  | "nn::audio::SampleFormat" AudioSampleFormat          | 2                                |
| 0x38   | 0x4  | "nn::album::ImageOrientation" VideoImageOrientation. | 0                                |
| 0x3C   | 0x44 | ?                                                    | 0                                |

This is "nn::grcsrv::OffscreenRecordingParameter". This is a 0x80-byte
struct. "nn::grc::OffscreenRecordingParameter" and
"nn::album::MovieMakerMovieParameter" are identical to this.

The above default values are initialized by the official user-process
via sdk-nso funcs
"nn::album::MovieMakerMovieParameter::GetDefaultValue()" /
"nn::album::MovieMakerMovieParameter::MovieMakerMovieParameter()" (both
funcs are identical).

# GameMovieId

| Offset | Size | Description                                                                    |
| ------ | ---- | ------------------------------------------------------------------------------ |
| 0x0    | 0x18 | Same as the last 0x18-bytes of [AlbumEntry](Capture%20services.md "wikilink"). |
| 0x18   | 0x28 | Unused, always zero.                                                           |

This is "nn::grcsrv::GameMovieId". This is a 0x40-byte struct.

# IHOSBinderDriver

This is the same interface as NV
[IHOSBinderDriver](Nvnflinger%20services#dispdrv.md##dispdrv "wikilink").

[Category:Services](Category:Services "wikilink")

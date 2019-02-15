GRC (Game Recording) uses libstagefright and the NvMMLite TVMR library
for writing [recorded](4.0.0.md "wikilink") video to MP4s.

Error reporting is done using the new
[/dev/nverpt-ctrl](NV%20services#%20dev%20nverpt-ctrl.md##/dev/nverpt-ctrl "wikilink")
ioctls.

# grc:c

This is
"nn::grcsrv::IGrcService".

| Cmd | Name                   | Notes                                                                                                                   |
| --- | ---------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| 1   | OpenContinuousRecorder | Takes a total of 0x48-bytes of input and a handle, returns an [\#IContinuousRecorder](#IContinuousRecorder "wikilink"). |
| 2   | OpenGameMovieTrimmer   | Takes a total of 0x8-bytes of input and a handle, returns an [\#IGameMovieTrimmer](#IGameMovieTrimmer "wikilink").      |
| 3   |                        | Takes a total of 0x8-bytes of input and a handle, returns an [\#IUnknown](#IUnknown "wikilink").                        |
| 101 |                        | Takes a total of 0x10-bytes of input, returns an [\#IMovieMaker](#IMovieMaker "wikilink").                              |

## IContinuousRecorder

This is "nn::grcsrv::IContinuousRecorder".

| Cmd | Name |
| --- | ---- |
| 1   |      |
| 2   |      |
| 10  |      |
| 11  |      |
| 12  |      |
| 13  |      |
| 14  |      |

## IGameMovieTrimmer

This is "nn::grcsrv::IGameMovieTrimmer".

| Cmd | Name                |
| --- | ------------------- |
| 1   | BeginTrim           |
| 2   | EndTrim             |
| 10  | GetNotTrimmingEvent |
| 20  | SetThumbnailRgba    |

# grc:d

This is "nn::grcsrv::IRemoteVideoTransfer".

Added with
[6.0.0](6.0.0.md "wikilink").

| Cmd | Name | Notes                                                                                                         |
| --- | ---- | ------------------------------------------------------------------------------------------------------------- |
| 1   |      | No input/output.                                                                                              |
| 2   |      | Takes an input u32 (must be value 0-1) and a type-0x6 output buffer, returns a total of 0x10-bytes of output. |

# IUnknown

| Cmd | Name | Notes                                                                        |
| --- | ---- | ---------------------------------------------------------------------------- |
| 201 |      | Takes a total of 0x8-bytes of input, returns a total of 0x8-bytes of output. |
| 202 |      | Takes a total of 0x8-bytes of input, no output.                              |

# IMovieMaker

This is
"nn::grcsrv::IMovieMaker".

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

Takes a total of 8-bytes of input, no output.

## OpenOffscreenLayer

Takes an input u64 **LayerHandle**, returns an output u32.

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

## CompleteOffscreenRecordingFinishEx0

Takes two input u32s **width**/**height**, an input u64 **LayerHandle**
and 2 type-0x5 input buffers, no output.

The input buffers are optional, addr=NULL and size=0 can be used for
these.

**width**/**height** must be 1280x720, these fields are unused
afterwards.

Besides **width**/**height**, this is the same as
[\#CompleteOffscreenRecordingFinish](#CompleteOffscreenRecordingFinish "wikilink")
except the second buffer is user-specified instead of addr=NULL/size=0.

## CompleteOffscreenRecordingFinishEx1

Takes two input u32s **width**/**height**, an input u64 **LayerHandle**
and two type-0x5 input buffers, returns a 0x20-byte output struct.

Same as
[\#CompleteOffscreenRecordingFinishEx0](#CompleteOffscreenRecordingFinishEx0 "wikilink")
except the output struct is returned in the cmdreply.

## EncodeOffscreenLayerAudioSample

Takes an input u64 **LayerHandle** and a type-0x5 input buffer, returns
an output u64.

## GetOffscreenLayerError

Takes an input u64 **LayerHandle**, no output.

## GetOffscreenLayerRecordingFinishReadyEvent

Takes an input u64 **LayerHandle**, returns an output event handle with
autoclear disabled.

## GetOffscreenLayerAudioEncodeReadyEvent

Takes an input u64 **LayerHandle**, returns an output event handle with
autoclear disabled.

# OffscreenRecordingParameter

This is a 0x80-byte struct.

# IHOSBinderDriver

This is the same interface as NV
[IHOSBinderDriver](Nvnflinger%20services#dispdrv.md##dispdrv "wikilink").

[Category:Services](Category:Services "wikilink")

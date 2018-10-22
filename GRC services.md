GRC (Game Recording) uses libstagefright and the NvMMLite TVMR library
for writing [recorded](4.0.0.md "wikilink") video to MP4s.

Error reporting is done using the new
[/dev/nverpt-ctrl](NV%20services#%20dev%20nverpt-ctrl.md##/dev/nverpt-ctrl "wikilink")
ioctls.

# grc:c

This is "nn::grcsrv::IGrcService".

| Cmd | Name                   |
| --- | ---------------------- |
| 1   | OpenContinuousRecorder |
| 2   | OpenGameMovieTrimmer   |

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

| Cmd | Name | Notes                                                                                                    |
| --- | ---- | -------------------------------------------------------------------------------------------------------- |
| 1   |      | No input/output.                                                                                         |
| 2   |      | Takes a total of 4-bytes of input and a type-0x6 output buffer, returns a total of 0x10-bytes of output. |

# IMovieMaker

This is
"nn::grcsrv::IMovieMaker".

| Cmd | Name                                                                                                   |
| --- | ------------------------------------------------------------------------------------------------------ |
| 2   | [\#CreateVideoProxy](#CreateVideoProxy "wikilink")                                                     |
| 10  | [\#OpenOffscreenLayer](#OpenOffscreenLayer "wikilink")                                                 |
| 11  | [\#CloseOffscreenLayer](#CloseOffscreenLayer "wikilink")                                               |
| 20  | [\#StartOffscreenRecording](#StartOffscreenRecording "wikilink")                                       |
| 21  | [\#AbortOffscreenRecording](#AbortOffscreenRecording "wikilink")                                       |
| 22  | [\#RequestOffscreenRecordingFinishReady](#RequestOffscreenRecordingFinishReady "wikilink")             |
| 23  | [\#CompleteOffscreenRecordingFinish](#CompleteOffscreenRecordingFinish "wikilink")                     |
| 24  | [\#StartOffscreenRecordingEx](#StartOffscreenRecordingEx "wikilink")                                   |
| 25  | [\#CompleteOffscreenRecordingFinishEx0](#CompleteOffscreenRecordingFinishEx0 "wikilink")               |
| 30  | [\#GetOffscreenLayerError](#GetOffscreenLayerError "wikilink")                                         |
| 41  | [\#EncodeOffscreenLayerAudioSample](#EncodeOffscreenLayerAudioSample "wikilink")                       |
| 50  | [\#GetOffscreenLayerRecordingFinishReadyEvent](#GetOffscreenLayerRecordingFinishReadyEvent "wikilink") |
| 52  | [\#GetOffscreenLayerAudioEncodeReadyEvent](#GetOffscreenLayerAudioEncodeReadyEvent "wikilink")         |

## CreateVideoProxy

No input, returns an
[IHOSBinderDriver](Nvnflinger%20services#dispdrv.md##dispdrv "wikilink").

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

Takes an input u64 and a type-0x5 input buffer, no output.

Seems to be unused by official user processes,
[\#CompleteOffscreenRecordingFinishEx0](#CompleteOffscreenRecordingFinishEx0 "wikilink")
is used instead.

## CompleteOffscreenRecordingFinishEx0

Takes an input u64 **LayerHandle** and 2 type-0x5 input buffers, no
output.

## EncodeOffscreenLayerAudioSample

Takes an input u64 **LayerHandle** and a type-0x5 input buffer, returns
an output u64.

## GetOffscreenLayerError

Takes an input u64 **LayerHandle**, no output.

## GetOffscreenLayerRecordingFinishReadyEvent

Takes an input u64 **LayerHandle**, returns an output event handle.

## GetOffscreenLayerAudioEncodeReadyEvent

Takes an input u64 **LayerHandle**, returns an output event handle.

# OffscreenRecordingParameter

This is a 0x80-byte struct.

[Category:Services](Category:Services "wikilink")

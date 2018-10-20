GRC (Game Recording) uses libstagefright and the NvMMLite TVMR library
for writing [recorded](4.0.0.md "wikilink") video to MP4s.

Error reporting is done using the new
[/dev/nverpt-ctrl](NV%20services#%20dev%20nverpt-ctrl.md##/dev/nverpt-ctrl "wikilink")
ioctls.

# grc:c

This is "nn::grcsrv::IGrcService"

| Cmd | Name                   |
| --- | ---------------------- |
| 1   | OpenContinuousRecorder |
| 2   | OpenGameMovieTrimmer   |

# IContinuousRecorder

This is "nn::grcsrv::IContinuousRecorder".

| Cmd | Name |
| --- | ---- |
| 1   |      |
| 2   |      |
| 10  |      |
| 11  |      |
| 12  |      |
| 13  |      |

# IGameMovieTrimmer

This is "nn::grcsrv::IGameMovieTrimmer".

| Cmd | Name                |
| --- | ------------------- |
| 1   | BeginTrim           |
| 2   | EndTrim             |
| 10  | GetNotTrimmingEvent |
| 20  | SetThumbnailRgba    |

# IMovieMaker

This is
"nn::grcsrv::IMovieMaker".

| Cmd | Name                                                                                       |
| --- | ------------------------------------------------------------------------------------------ |
| 2   | [\#CreateVideoProxy](#CreateVideoProxy "wikilink")                                         |
| 10  | [\#OpenOffscreenLayer](#OpenOffscreenLayer "wikilink")                                     |
| 11  | [\#CloseOffscreenLayer](#CloseOffscreenLayer "wikilink")                                   |
| 20  | [\#StartOffscreenRecording](#StartOffscreenRecording "wikilink")                           |
| 21  | [\#AbortOffscreenRecording](#AbortOffscreenRecording "wikilink")                           |
| 22  | [\#RequestOffscreenRecordingFinishReady](#RequestOffscreenRecordingFinishReady "wikilink") |
| 23  | [\#CompleteOffscreenRecordingFinish](#CompleteOffscreenRecordingFinish "wikilink")         |
| 24  | [\#StartOffscreenRecordingEx](#StartOffscreenRecordingEx "wikilink")                       |
| 25  | [\#CompleteOffscreenRecordingFinishEx0](#CompleteOffscreenRecordingFinishEx0 "wikilink")   |
| 30  | [\#GetOffscreenLayerError](#GetOffscreenLayerError "wikilink")                             |
| 41  | EncodeOffscreenLayerAudioSample                                                            |
| 50  | GetOffscreenLayerRecordingFinishReadyEvent                                                 |
| 52  | GetOffscreenLayerAudioEncodeReadyEvent                                                     |

## CreateVideoProxy

No input, returns an
[IHOSBinderDriver](Nvnflinger%20services#dispdrv.md##dispdrv "wikilink").

## OpenOffscreenLayer

Takes an input u64, returns an output u32.

## CloseOffscreenLayer

Takes an input u64, no output.

## StartOffscreenRecording

Takes an input u64, no output.

## AbortOffscreenRecording

Takes an input u64, no output.

## RequestOffscreenRecordingFinishReady

Takes an input u64, no output.

## StartOffscreenRecordingEx

Takes an input u64 and an
[\#OffscreenRecordingParameter](#OffscreenRecordingParameter "wikilink"),
no output.

## CompleteOffscreenRecordingFinish

Takes an input u64 and a type-0x5 input buffer, no output.

## CompleteOffscreenRecordingFinishEx0

Takes an input u64 and 2 type-0x5 input buffers, no output.

## GetOffscreenLayerError

Takes an input u64, no output.

# OffscreenRecordingParameter

This is a 0x80-byte struct.

[Category:Services](Category:Services "wikilink")

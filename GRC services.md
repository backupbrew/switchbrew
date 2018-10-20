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

This is "nn::grcsrv::IMovieMaker".

| Cmd | Name                                               |
| --- | -------------------------------------------------- |
| 2   | [\#CreateVideoProxy](#CreateVideoProxy "wikilink") |
| 10  | OpenOffscreenLayer                                 |
| 11  | CloseOffscreenLayer                                |
| 20  | StartOffscreenRecording                            |
| 21  | AbortOffscreenRecording                            |
| 22  | RequestOffscreenRecordingFinishReady               |
| 23  | CompleteOffscreenRecordingFinish                   |
| 24  | StartOffscreenRecordingEx                          |
| 25  | CompleteOffscreenRecordingFinishEx0                |
| 30  | GetOffscreenLayerError                             |
| 41  | EncodeOffscreenLayerAudioSample                    |
| 50  | GetOffscreenLayerRecordingFinishReadyEvent         |
| 52  | GetOffscreenLayerAudioEncodeReadyEvent             |

## CreateVideoProxy

No input, returns an
[IHOSBinderDriver](Nvnflinger%20services#dispdrv.md##dispdrv "wikilink").

[Category:Services](Category:Services "wikilink")

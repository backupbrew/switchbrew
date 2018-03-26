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

[Category:Services](Category:Services "wikilink")

GRC (Game Recording) uses libstagefright and the NvMMLite TVMR library
for writing [recorded](4.0.0.md "wikilink") video to MP4s.

Error reporting is done using the new
[/dev/nverpt-ctrl](NV%20services#%20dev%20nverpt-ctrl.md##/dev/nverpt-ctrl "wikilink")
ioctls.

# grc:c

This is "nn::grcsrv::IGrcService"

| Cmd | Name                  |
| --- | --------------------- |
| 1   | GetContinuousRecorder |
| 2   | GetGameMovieTrimmer   |

# nn::grcsrv::IContinuousRecorder

| Cmd | Name |
| --- | ---- |
| 1   |      |
| 2   |      |
| 10  |      |
| 11  |      |
| 12  |      |
| 13  |      |

# nn::grcsrv::IGameMovieTrimmer

| Cmd | Name |
| --- | ---- |
| 1   |      |
| 2   |      |
| 10  |      |
| 20  |      |

[Category:Services](Category:Services "wikilink")

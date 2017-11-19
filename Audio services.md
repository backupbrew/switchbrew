# audout:u

| Cmd | Name                                       |
| --- | ------------------------------------------ |
| 0   | ListAudioOuts                              |
| 1   | [\#OpenAudioOut](#OpenAudioOut "wikilink") |

## OpenAudioOut

Takes two u64s (an interface ID and a PID placeholder?), a PID, a
process handle, and the name of the interface you want to connect to.
Returns an [\#IAudioOut](#IAudioOut "wikilink") object.

## IAudioOut

| Cmd | Name                      |
| --- | ------------------------- |
| 0   | GetAudioOutState          |
| 1   | StartAudioOut             |
| 2   | StopAudioOut              |
| 3   | AppendAudioOutBuffer      |
| 4   | RegisterBufferEvent       |
| 5   | GetReleasedAudioOutBuffer |
| 6   | ContainsAudioOutBuffer    |

[Category:Services](Category:Services "wikilink")

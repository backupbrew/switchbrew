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

| Cmd | Name                                               |
| --- | -------------------------------------------------- |
| 0   | [\#GetAudioOutState](#GetAudioOutState "wikilink") |
| 1   | StartAudioOut                                      |
| 2   | StopAudioOut                                       |
| 3   | AppendAudioOutBuffer                               |
| 4   | RegisterBufferEvent                                |
| 5   | GetReleasedAudioOutBuffer                          |
| 6   | ContainsAudioOutBuffer                             |

### GetAudioOutState

Returns a AudioOutState, 0x00=Started 0x01=Stopped

# audin:u

| Cmd | Name         |
| --- | ------------ |
| 0   | ListAudioIns |
| 1   | OpenAudioIn  |

## IAudioIn

| Cmd | Name                                             |
| --- | ------------------------------------------------ |
| 0   | [\#GetAudioInState](#GetAudioInState "wikilink") |
| 1   | StartAudioIn                                     |
| 2   | StopAudioIn                                      |
| 3   | AppendAudioInBuffer                              |
| 4   | RegisterBufferEvent                              |
| 5   | GetReleasedAudioInBuffer                         |
| 6   | ContainsAudioInBuffer                            |

### GetAudioInState

Returns a AudioInState, 0x00=Started 0x01=Stopped

[Category:Services](Category:Services "wikilink")

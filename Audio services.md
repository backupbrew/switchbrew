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

Returns an AudioOutState, 0x00=Started 0x01=Stopped

# audout:a

| Cmd | Name                    |
| --- | ----------------------- |
| 0   | RequestSuspendAudioOuts |
| 1   | RequestResumeAudioOuts  |

# audout:d

| Cmd | Name                                                                             |
| --- | -------------------------------------------------------------------------------- |
| 0   | [\#RequestSuspendAudioOutsForDebug](#RequestSuspendAudioOutsForDebug "wikilink") |
| 1   | [\#RequestResumeAudioOutsForDebug](#RequestResumeAudioOutsForDebug "wikilink")   |

## RequestSuspendAudioOutsForDebug

Takes an
[AppletResourceUserId](AM%20services#AppletResourceUserId.md##AppletResourceUserId "wikilink").
(u64)

## RequestResumeAudioOutsForDebug

Takes an
[AppletResourceUserId](AM%20services#AppletResourceUserId.md##AppletResourceUserId "wikilink").
(u64)

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

Returns an AudioInState, 0x00=Started 0x01=Stopped

# audin:a

| Cmd | Name                   |
| --- | ---------------------- |
| 0   | RequestSuspendAudioIns |
| 1   | RequestResumeAudioIns  |

# audin:d

| Cmd | Name                                                                           |
| --- | ------------------------------------------------------------------------------ |
| 0   | [\#RequestSuspendAudioInsForDebug](#RequestSuspendAudioInsForDebug "wikilink") |
| 1   | [\#RequestResumeAudioInsForDebug](#RequestResumeAudioInsForDebug "wikilink")   |

## RequestSuspendAudioInsForDebug

Takes an
[AppletResourceUserId](AM%20services#AppletResourceUserId.md##AppletResourceUserId "wikilink").
(u64)

## RequestResumeAudioInsForDebug

Takes an
[AppletResourceUserId](AM%20services#AppletResourceUserId.md##AppletResourceUserId "wikilink").
(u64)

# audrec:u

| Cmd | Name                    |
| --- | ----------------------- |
| 0   | OpenFinalOutputRecorder |

## IFinalOutputRecorder

| Cmd | Name                                 |
| --- | ------------------------------------ |
| 0   | GetFinalOutputRecorderState          |
| 1   | StartFinalOutputRecorder             |
| 2   | StopFinalOutputRecorder              |
| 3   | AppendFinalOutputRecorderBuffer      |
| 4   | RegisterBufferEvent                  |
| 5   | GetReleasedFinalOutputRecorderBuffer |
| 6   | ContainsFinalOutputRecorderBuffer    |

# audren:u

| Cmd | Name                                 |
| --- | ------------------------------------ |
| 0   | OpenAudioRenderer                    |
| 1   | GetAudioRendererWorkBufferSize       |
| 2   | GetAudioRenderersProcessMasterVolume |
| 3   | SetAudioRenderersProcessMasterVolume |

## IAudioRenderer

| Cmd | Name                               |
| --- | ---------------------------------- |
| 0   | GetAudioRendererSampleRate         |
| 1   | GetAudioRendererSampleCount        |
| 2   | GetAudioRendererMixBufferCount     |
| 3   | GetAudioRendererState              |
| 4   | RequestUpdateAudioRenderer         |
| 5   | StartAudioRenderer                 |
| 6   | StopAudioRenderer                  |
| 7   | QuerySystemEvent                   |
| 8   | SetAudioRendererRenderingTimeLimit |
| 9   | GetAudioRendererRenderingTimeLimit |

# codecctl

| Cmd | Name                                           |
| --- | ---------------------------------------------- |
| 0   | InitializeCodecController                      |
| 1   | FinalizeCodecController                        |
| 2   | SleepCodecController                           |
| 3   | WakeCodecController                            |
| 4   | [\#SetCodecVolume](#SetCodecVolume "wikilink") |
| 5   | GetCodecVolumeMax                              |
| 6   | GetCodecVolumeMin                              |
| 7   | SetCodecActiveTarget                           |
| 8   | Unknown                                        |
| 9   | BindCodecHeadphoneMicJackInterrupt             |
| 10  | IsCodecHeadphoneMicJackInserted                |
| 11  | ClearCodecHeadphoneMicJackInterrupt            |
| 12  | IsCodecDeviceRequested                         |

## SetCodecVolume

Takes a Volume (uint32)

[Category:Services](Category:Services "wikilink")

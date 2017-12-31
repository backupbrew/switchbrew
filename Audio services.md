# audout:u

| Cmd | Name                                       |
| --- | ------------------------------------------ |
| 0   | ListAudioOuts                              |
| 1   | [\#OpenAudioOut](#OpenAudioOut "wikilink") |

## OpenAudioOut

Takes two u64s (an interface ID and a PID placeholder?), a PID, a
process handle, and the name of the interface you want to connect to.
Returns an [\#IAudioOut](#IAudioOut "wikilink") object and four u32s:
the sample rate, channel count, [PCM format](#PCM_format "wikilink"),
and an unknown field.

### PCM format

| Value | Name      |
| ----- | --------- |
| 0     | Invalid   |
| 1     | INT8      |
| 2     | INT16     |
| 3     | INT24     |
| 4     | INT32     |
| 5     | PCM Float |
| 6     | ADPCM     |

## IAudioOut

| Cmd | Name                                                                                                         |
| --- | ------------------------------------------------------------------------------------------------------------ |
| 0   | [\#GetAudioOutState](#GetAudioOutState "wikilink")                                                           |
| 1   | StartAudioOut                                                                                                |
| 2   | StopAudioOut                                                                                                 |
| 3   | [\#AppendAudioOutBuffer](#AppendAudioOutBuffer "wikilink") taking a type 0x5 (A descriptor) buffer           |
| 4   | [\#RegisterBufferEvent](#RegisterBufferEvent "wikilink")                                                     |
| 5   | [\#GetReleasedAudioOutBuffer](#GetReleasedAudioOutBuffer "wikilink") taking a type 0x6 (B descriptor) buffer |
| 6   | [\#ContainsAudioOutBuffer](#ContainsAudioOutBuffer "wikilink")                                               |
| 7   | [\#AppendAudioOutBuffer](#AppendAudioOutBuffer "wikilink") taking a type 0x21 buffer                         |
| 8   | [\#GetReleasedAudioOutBuffer](#GetReleasedAudioOutBuffer "wikilink") taking a type 0x22 buffer               |

### GetAudioOutState

Returns an AudioOutState, 0x00=Started 0x01=Stopped (u32)

### AppendAudioOutBuffer

Takes a u64 (not sure what this is, might act as some sort of identifier
for the audio buffer? official applications seem to use the address of
the audio buffer struct for this) and a buffer. The format of said
buffer is as follows:

| Offset | Size | Description                         |
| ------ | ---- | ----------------------------------- |
| 0x00   | 8    | Pointer to the sample data pointer. |
| 0x08   | 8    | Pointer to sample data.             |
| 0x10   | 8    | Capacity of sample buffer           |
| 0x18   | 8    | Size of data in sample buffer       |
| 0x20   | 8    | Unknown. Zero works.                |

### RegisterBufferEvent

Returns an event handle that is signalled when a buffer is released

### GetReleasedAudioOutBuffer

Takes a buffer, which it will fill with the identifiers passed from
[\#AppendAudioOutBuffer](#AppendAudioOutBuffer "wikilink") of audio
buffers that have been released. Will return a u32 (may indicate how
many buffers were released?)

### ContainsAudioOutBuffer

Takes a u64 (pointer to audio buffer?). Returns a bool. (u8)

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

Returns an AudioInState, 0x00=Started 0x01=Stopped (u32)

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

| Cmd | Name                                                                                   |
| --- | -------------------------------------------------------------------------------------- |
| 0   | [\#GetAudioRendererSampleRate](#GetAudioRendererSampleRate "wikilink")                 |
| 1   | [\#GetAudioRendererSampleCount](#GetAudioRendererSampleCount "wikilink")               |
| 2   | [\#GetAudioRendererMixBufferCount](#GetAudioRendererMixBufferCount "wikilink")         |
| 3   | [\#GetAudioRendererState](#GetAudioRendererState "wikilink")                           |
| 4   | RequestUpdateAudioRenderer                                                             |
| 5   | StartAudioRenderer                                                                     |
| 6   | StopAudioRenderer                                                                      |
| 7   | QuerySystemEvent                                                                       |
| 8   | [\#SetAudioRendererRenderingTimeLimit](#SetAudioRendererRenderingTimeLimit "wikilink") |
| 9   | [\#GetAudioRendererRenderingTimeLimit](#GetAudioRendererRenderingTimeLimit "wikilink") |

### GetAudioRendererSampleRate

Returns the Sample Rate. (u32)

### GetAudioRendererSampleCount

Returns the Sample Count. (u32)

### GetAudioRendererMixBufferCount

Returns the number of Mix Buffers. (u32)

### GetAudioRendererState

Returns an AudioRenderState, 0x00=Started 0x01=Stopped (u32)

### SetAudioRendererRenderingTimeLimit

Takes a upper limit of the rendering time in percent. (u32)

### GetAudioRendererRenderingTimeLimit

Returns the upper limit of the rendering time in percent. (u32)

# audout:a, audin:a, audrec:a and audren:a

| Cmd | Name           |
| --- | -------------- |
| 0   | RequestSuspend |
| 1   | RequestResume  |

# audout:d, audin:d, audrec:d and audren:d

| Cmd | Name                                                           |
| --- | -------------------------------------------------------------- |
| 0   | [\#RequestSuspendForDebug](#RequestSuspendForDebug "wikilink") |
| 1   | [\#RequestResumeForDebug](#RequestResumeForDebug "wikilink")   |

## RequestSuspendForDebug

Takes an
[AppletResourceUserId](AM%20services#AppletResourceUserId.md##AppletResourceUserId "wikilink").
(u64)

## RequestResumeForDebug

Takes an
[AppletResourceUserId](AM%20services#AppletResourceUserId.md##AppletResourceUserId "wikilink").
(u64)

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

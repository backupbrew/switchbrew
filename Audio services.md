# audout:u

This is "nn::audio::detail::IAudioOutManager".

| Cmd | Name                                                        |
| --- | ----------------------------------------------------------- |
| 0   | [\#ListAudioOuts](#ListAudioOuts "wikilink")                |
| 1   | [\#OpenAudioOut](#OpenAudioOut "wikilink")                  |
| 2   | \[3.0.0+\] [\#ListAudioOutsEx](#ListAudioOutsEx "wikilink") |
| 3   | \[3.0.0+\] [\#OpenAudioOutEx](#OpenAudioOutEx "wikilink")   |

## ListAudioOuts

Takes a type-6 output buffer. Populates the output buffer with the
available audio output devices' names and returns an u32 with the number
of device names written.

## OpenAudioOut

Takes a type-5 input buffer (**DeviceNameIn**), a type-6 output buffer
(**DeviceNameOut**), two u32s **SampleRate** (must be 48000) and
**ChannelCount** (high u16 can't be 0, official apps pass 0xCAFE0000),
one u64 **ClientPID**, a PID and a copy-handle. Returns an
[\#IAudioOut](#IAudioOut "wikilink") object and four u32s: the sample
rate, channel count, [PCM format](#PCM_format "wikilink"), and the
initial AudioOutState.

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

## ListAudioOutsEx

Same as [\#ListAudioOuts](#ListAudioOuts "wikilink"), but takes a
type-0x22 output buffer instead.

## OpenAudioOutEx

Same as [\#OpenAudioOut](#OpenAudioOut "wikilink"), but takes a
type-0x21 input buffer instead.

## IAudioOut

This is
"nn::audio::detail::IAudioOut".

| Cmd | Name                                                                                |
| --- | ----------------------------------------------------------------------------------- |
| 0   | [\#GetAudioOutState](#GetAudioOutState "wikilink")                                  |
| 1   | [\#StartAudioOut](#StartAudioOut "wikilink")                                        |
| 2   | [\#StopAudioOut](#StopAudioOut "wikilink")                                          |
| 3   | [\#AppendAudioOutBuffer](#AppendAudioOutBuffer "wikilink")                          |
| 4   | [\#RegisterBufferEvent](#RegisterBufferEvent "wikilink")                            |
| 5   | [\#GetReleasedAudioOutBuffer](#GetReleasedAudioOutBuffer "wikilink")                |
| 6   | [\#ContainsAudioOutBuffer](#ContainsAudioOutBuffer "wikilink")                      |
| 7   | \[3.0.0+\] [\#AppendAudioOutBufferEx](#AppendAudioOutBufferEx "wikilink")           |
| 8   | \[3.0.0+\] [\#GetReleasedAudioOutBufferEx](#GetReleasedAudioOutBufferEx "wikilink") |
| 9   | \[4.0.0+\]                                                                          |
| 10  | \[4.0.0+\]                                                                          |
| 11  | \[4.0.0+\]                                                                          |

### GetAudioOutState

Returns an u32 **AudioOutState** (0x00=Started, 0x01=Stopped).

### StartAudioOut

Starts audio playback using data from appended buffers.

### StopAudioOut

Stops audio playback.

### AppendAudioOutBuffer

Takes a type-5 input buffer for sample data and a u64 which acts as a
tag for the supplied buffer (official apps use the buffer's address).

The format of the input buffer is as follows:

| Offset | Size | Description                         |
| ------ | ---- | ----------------------------------- |
| 0x00   | 8    | Pointer to next buffer              |
| 0x08   | 8    | Pointer to sample buffer            |
| 0x10   | 8    | Capacity of sample buffer           |
| 0x18   | 8    | Size of data in the sample buffer   |
| 0x20   | 8    | Offset of data in the sample buffer |

### RegisterBufferEvent

Returns an event handle that is signalled when a buffer is released.

### GetReleasedAudioOutBuffer

Takes a type-6 output buffer which will be filled with the identifiers
from [\#AppendAudioOutBuffer](#AppendAudioOutBuffer "wikilink") of audio
buffers that have been released. Returns an u32
**ReleasedBuffersCount**.

### ContainsAudioOutBuffer

Takes an u64 **tag** for the desired buffer. Returns 1 if the buffer was
appended and not yet released.

### AppendAudioOutBufferEx

Same as [\#AppendAudioOutBuffer](#AppendAudioOutBuffer "wikilink") but
takes a type-0x21 buffer instead.

### GetReleasedAudioOutBufferEx

Same as
[\#GetReleasedAudioOutBuffer](#GetReleasedAudioOutBuffer "wikilink") but
takes a type-0x22 buffer instead.

# audin:u

This is "nn::audio::detail::IAudioInManagerForDebugger".

| Cmd | Name                      |
| --- | ------------------------- |
| 0   | ListAudioIns              |
| 1   | OpenAudioIn               |
| 2   | \[3.0.0+\] ListAudioInsEx |
| 3   | \[3.0.0+\] OpenAudioInEx  |

## IAudioIn

This is "nn::audio::detail::IAudioIn".

| Cmd | Name                                             |
| --- | ------------------------------------------------ |
| 0   | [\#GetAudioInState](#GetAudioInState "wikilink") |
| 1   | StartAudioIn                                     |
| 2   | StopAudioIn                                      |
| 3   | AppendAudioInBuffer                              |
| 4   | RegisterBufferEvent                              |
| 5   | GetReleasedAudioInBuffer                         |
| 6   | ContainsAudioInBuffer                            |
| 7   |                                                  |
| 8   | \[3.0.0+\] AppendAudioInBufferEx                 |
| 9   | \[3.0.0+\] GetReleasedAudioInBufferEx            |
| 10  | \[3.0.0+\]                                       |

### GetAudioInState

Returns an AudioInState, 0x00=Started 0x01=Stopped (u32)

# audrec:u

This is "nn::audio::detail::IFinalOutputRecorderManager".

| Cmd | Name                    |
| --- | ----------------------- |
| 0   | OpenFinalOutputRecorder |

## IFinalOutputRecorder

This is "nn::audio::detail::IFinalOutputRecorder".

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

This is "nn::audio::detail::IAudioRendererManager".

| Cmd | Name                                 |
| --- | ------------------------------------ |
| 0   | OpenAudioRenderer                    |
| 1   | GetAudioRendererWorkBufferSize       |
| 2   | GetAudioRenderersProcessMasterVolume |
| 3   | SetAudioRenderersProcessMasterVolume |

## IAudioRenderer

This is
"nn::audio::detail::IAudioRenderer".

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

# audout:a, audin:a, audrec:a, audren:a

This is "nn::audio::detail::IAudioOutManagerForApplet",
"nn::audio::detail::IAudioInManagerForApplet",
"nn::audio::detail::IFinalOutputRecorderManagerForApplet",
"nn::audio::detail::IAudioRendererManagerForApplet".

| Cmd | Name           |
| --- | -------------- |
| 0   | RequestSuspend |
| 1   | RequestResume  |

# audout:d, audin:d, audrec:d, audren:d

This is "nn::audio::detail::IAudioOutManagerForDebugger",
"nn::audio::detail::IAudioInManagerForDebugger",
"nn::audio::detail::IFinalOutputRecorderManagerForDebugger",
"nn::audio::detail::IAudioRendererManagerForDebugger".

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

This is "nn::audio::detail::ICodecController".

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

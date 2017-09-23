The only image data contained in this sysmodule is basically a saved
display framebuffer, no image data for actively-used
layers/framebuffers.

# mm:u

NVIDIA multimedia (NvMM) platform service.

| Cmd | Name                   |
| --- | ---------------------- |
| 0   | ?                      |
| 1   | ?                      |
| 2   | ?                      |
| 3   | ?                      |
| 4   | module\_init\_clk      |
| 5   | module\_deinit\_clk    |
| 6   | module\_set\_clk\_rate |
| 7   | module\_get\_clk\_rate |

# vi:u

This is
"nn::visrv::sf::IApplicationRootService".

| Cmd | Name              | Notes                                                                                                                  |
| --- | ----------------- | ---------------------------------------------------------------------------------------------------------------------- |
| 0   | GetDisplayService | Returns an [\#IApplicationDisplayService](#IApplicationDisplayService "wikilink"). Takes an input u64(?), can be zero. |
|     |                   |                                                                                                                        |

# vi:m

This is
"nn::visrv::sf::IManagerRootService".

| Cmd | Name                                   | Notes                                                                                                          |
| --- | -------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| 2   | GetDisplayService                      | Returns an [\#IApplicationDisplayService](#IApplicationDisplayService "wikilink").                             |
| 3   | GetDisplayServiceWithProxyNameExchange | Takes an input u64 and u32. Returns an [\#IApplicationDisplayService](#IApplicationDisplayService "wikilink"). |
|     |                                        |                                                                                                                |

# vi:s

This is "nn::visrv::sf::ISystemRootService".

| Cmd | Name                                   |
| --- | -------------------------------------- |
| 1   | GetDisplayService                      |
| 3   | GetDisplayServiceWithProxyNameExchange |
|     |                                        |

# IApplicationDisplayService

| Cmd  | Name                                    | Notes                                                                      |
| ---- | --------------------------------------- | -------------------------------------------------------------------------- |
| 100  | GetRelayService                         | Returns an [\#IHOSBinderDriver](#IHOSBinderDriver "wikilink").             |
| 101  | GetSystemDisplayService                 | Returns an [\#ISystemDisplayService](#ISystemDisplayService "wikilink").   |
| 102  | GetManagerDisplayService                | Returns an [\#IManagerDisplayService](#IManagerDisplayService "wikilink"). |
| 103  | GetIndirectDisplayTransactionService    | Returns an [\#IHOSBinderDriver](#IHOSBinderDriver "wikilink").             |
| 1000 | ListDisplays                            |                                                                            |
| 1010 | OpenDisplay                             |                                                                            |
| 1011 | OpenDefaultDisplay                      |                                                                            |
| 1020 | CloseDisplay                            |                                                                            |
| 1101 | SetDisplayEnabled                       |                                                                            |
| 1102 | GetDisplayResolution                    |                                                                            |
| 2020 | OpenLayer                               |                                                                            |
| 2021 | CloseLayer                              |                                                                            |
| 2030 | CreateStrayLayer                        |                                                                            |
| 2031 | DestroyStrayLayer                       |                                                                            |
| 2101 | SetLayerScalingMode                     |                                                                            |
| 2450 | GetIndirectLayerImageMap                |                                                                            |
| 2451 | GetIndirectLayerImageCropMap            |                                                                            |
| 2460 | GetIndirectLayerImageRequiredMemoryInfo |                                                                            |
| 5202 | GetDisplayVsyncEvent                    |                                                                            |
| 5203 | GetDisplayVsyncEventForDebug            |                                                                            |
|      |                                         |                                                                            |

## ListDisplays

Takes a type-0x6 output buffer containing the array of
[\#DisplayInfo](#DisplayInfo "wikilink") output entries. Returns an
output u64: total number of output entries.

Normally(?) this only returns the "Default" display.

## OpenDisplay

Takes a [\#DisplayName](#DisplayName "wikilink") as input. Returns an
output u64, the DisplayId.

To open the default display, input string "Default" can be used.

## OpenDefaultDisplay

Returns an output u64.

Probably not (?) used by newer official user-processes, since those use
OpenDisplay with the default string instead.

## CloseDisplay

Takes an input u64, DisplayId.

## SetDisplayEnabled

Takes an input u32 boolean, and an u64(DisplayId?).

## GetDisplayResolution

Takes an input u64 DisplayId and returns two output u64s.

## OpenLayer

Takes a PID-descriptor, a type-0x6 buffer for the output
[\#NativeWindow](#NativeWindow "wikilink"), a
[\#DisplayName](#DisplayName "wikilink")(which was previously used with
[\#OpenDisplay](#OpenDisplay "wikilink")), an u64 LayerId, and an u64
[AppletResourceUserId](AM%20services.md "wikilink"). Returns an output
u64 NativeWindow\_Size.

Official user-processes use a LayerId stored in a global state
field("...ExternalLayerId") if non-zero, otherwise:

  - When AppletResourceUserId==0,
    [\#CreateStrayLayer](#CreateStrayLayer "wikilink") is used instead
    of the OpenLayer cmd.
  - When AppletResourceUserId\!=0,
    [AM\_services\#CreateManagedDisplayLayer](AM%20services#CreateManagedDisplayLayer.md##CreateManagedDisplayLayer "wikilink")
    is used and the output from that is used for LayerId with the
    OpenLayer cmd.

## CloseLayer

Takes an input u64: LayerId which was used with
[\#OpenLayer](#OpenLayer "wikilink").

## CreateStrayLayer

Takes a type-0x6 buffer for the output
[\#NativeWindow](#NativeWindow "wikilink"), an u32(LayerFlags bitmask),
and an u64 DisplayId. Returns two output u64s: LayerId and
NativeWindow\_Size.

## DestroyStrayLayer

Takes an input u64: LayerId from
[\#CreateStrayLayer](#CreateStrayLayer "wikilink").

## SetLayerScalingMode

Takes an input u32("ScalingMode") and u64.

## GetIndirectLayerImageMap

Takes a PID-descriptor, an type-0x46 buffer, and four u64s: width(s32),
height(s32), \<output from [AM](AM%20services.md "wikilink")
GetIndirectLayerConsumerHandle\>, and
[AppletResourceUserId](AM%20services.md "wikilink"). Returns two output
u64s.

## GetIndirectLayerImageCropMap

Takes a PID-descriptor, an type-0x46 buffer, four floats, four u64s(last
u64 is [AppletResourceUserId](AM%20services.md "wikilink")). Returns two
output u64s. The floats are stored immediately after each other(32bits).

## GetIndirectLayerImageRequiredMemoryInfo

Takes two input u64s: with and height. Returns two output u64s. First
u64 is the buffer size to use with the ImageMap cmds.

## GetDisplayVsyncEvent

Takes an input u64 DisplayId and returns a handle.

## GetDisplayVsyncEventForDebug

Takes an input u64 DisplayId and returns a handle.

## IHOSBinderDriver

| Cmd | Name               |
| --- | ------------------ |
| 0   | TransactParcel     |
| 1   | AdjustRefcount     |
| 2   | GetNativeHandle    |
| 3   | TransactParcelAuto |

## ISystemDisplayService

| Cmd  | Name                        |
| ---- | --------------------------- |
| 1200 | GetZOrderCountMin           |
| 1202 | GetZOrderCountMax           |
| 1203 | GetDisplayLogicalResolution |
| 1204 | SetDisplayMagnification     |
| 2201 | SetLayerPosition            |
| 2203 | SetLayerSize                |
| 2204 | GetLayerZ                   |
| 2205 | SetLayerZ                   |
| 2207 | SetLayerVisibility          |
| 2209 | SetLayerAlpha               |
| 2312 | CreateStrayLayer            |
| 2400 | OpenIndirectLayer           |
| 2401 | CloseIndirectLayer          |
| 2402 | FlipIndirectLayer           |
| 3000 | ListDisplayModes            |
| 3001 | ListDisplayRgbRanges        |
| 3002 | ListDisplayContentTypes     |
| 3200 | GetDisplayMode              |
| 3201 | SetDisplayMode              |
| 3202 | GetDisplayUnderscan         |
| 3203 | SetDisplayUnderscan         |
| 3204 | GetDisplayContentType       |
| 3205 | SetDisplayContentType       |
| 3206 | GetDisplayRgbRange          |
| 3207 | SetDisplayRgbRange          |
| 3208 | GetDisplayCmuMode           |
| 3209 | SetDisplayCmuMode           |
| 3210 | GetDisplayContrastRatio     |
| 3211 | SetDisplayContrastRatio     |
| 3214 | GetDisplayGamma             |
| 3215 | SetDisplayGamma             |
| 3216 | GetDisplayCmuLuma           |
| 3217 | SetDisplayCmuLuma           |
|      |                             |

## IManagerDisplayService

| Cmd  | Name                               |
| ---- | ---------------------------------- |
| 1102 | GetDisplayResolution               |
| 2010 | CreateManagedLayer                 |
| 2011 | DestroyManagedLayer                |
| 2050 | CreateIndirectLayer                |
| 2051 | DestroyIndirectLayer               |
| 2052 | CreateIndirectProducerEndPoint     |
| 2053 | DestroyIndirectProducerEndPoint    |
| 2054 | CreateIndirectConsumerEndPoint     |
| 2055 | DestroyIndirectConsumerEndPoint    |
| 2300 | AcquireLayerTexturePresentingEvent |
| 2301 | ReleaseLayerTexturePresentingEvent |
| 2302 | GetDisplayHotplugEvent             |
| 2402 | GetDisplayHotplugState             |
| 4201 | SetDisplayAlpha                    |
| 4203 | SetDisplayLayerStack               |
| 4205 | SetDisplayPowerState               |
| 6000 | AddToLayerStack                    |
| 6001 | RemoveFromLayerStack               |
| 6002 | SetLayerVisibility                 |
| 7000 | SetContentVisibility               |
| 8000 | SetConductorLayer                  |
| 8100 | SetIndirectProducerFlipOffset      |

# DisplayInfo

| Offset | Size | Description                              |
| ------ | ---- | ---------------------------------------- |
| 0x0    | 0x40 | [\#DisplayName](#DisplayName "wikilink") |
| 0x40   | 0x8? | Normally 0x1 for the "Default" Display?  |
| 0x48   | 0x8? | Normally 0x1 for the "Default" Display?  |
| 0x50   | 0x8? | Width                                    |
| 0x58   | 0x8? | Height                                   |

This is a 0x60-byte structure.

The width/height for the "Default" Display is the resolution for 1080p
even when in handheld-mode.

# DisplayName

This is a 0x40-byte block: a NUL-terminated string.

# NativeWindow

| Offset | Size | Description                |
| ------ | ---- | -------------------------- |
| 0x0    | 0x8? | ?                          |
| 0x8    | 0x8? | ?                          |
| 0x10   | 0x8? | ?                          |
| 0x18   | 0x8? | ?                          |
| 0x20   | 0x8? | ?                          |
| 0x28   | ?    | "dispdrv" string normally? |

Max size of this buffer is 0x100-bytes(outbuf size used by official
user-processes). Parsed("Deserialize...") by a function called by the
code described under [\#OpenLayer](#OpenLayer "wikilink"), which
executes code with Android symbols.

[Category:Services](Category:Services "wikilink")

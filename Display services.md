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

| Cmd | Name              | Notes                                                                              |
| --- | ----------------- | ---------------------------------------------------------------------------------- |
| 0   | GetDisplayService | Returns an [\#IApplicationDisplayService](#IApplicationDisplayService "wikilink"). |
|     |                   |                                                                                    |

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
output u64.

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

This is a 0x60-byte structure.

# DisplayName

This is a 0x40-byte block: a NUL-terminated string.

[Category:Services](Category:Services "wikilink")

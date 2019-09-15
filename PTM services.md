# fan

This is "nn::fan::detail::IManager".

| Cmd | Name           |
| --- | -------------- |
| 0   | OpenController |

## IController

This is "nn::fan::detail::IController".

| Cmd | Name                                        |
| --- | ------------------------------------------- |
| 0   | SetRotationSpeedLevel                       |
| 1   | SetRotationSpeedLevelByDiff                 |
| 2   | GetRotationSpeedLevel                       |
| 3   | SetRotationRate                             |
| 4   | GetRotationRate                             |
| 5   | \[1.0.0-6.2.0\] EnableFan                   |
| 6   | \[1.0.0-6.2.0\] DisableFan                  |
| 7   | \[1.0.0-6.2.0\] GetActualRotationSpeedLevel |

\[7.0.0+\] SetRotationSpeedLevelByDiff/SetRotationRate no longer takes
any input. GetRotationRate no longer returns output. These were
presumably replaced with new cmds?

# psm

This is "nn::psm::IPsmServer".

| Cmd | Name                                                                                 |
| --- | ------------------------------------------------------------------------------------ |
| 0   | [\#GetBatteryChargePercentage](#GetBatteryChargePercentage "wikilink")               |
| 1   | [\#GetChargerType](#GetChargerType "wikilink")                                       |
| 2   | [\#EnableBatteryCharging](#EnableBatteryCharging "wikilink")                         |
| 3   | [\#DisableBatteryCharging](#DisableBatteryCharging "wikilink")                       |
| 4   | [\#IsBatteryChargingEnabled](#IsBatteryChargingEnabled "wikilink")                   |
| 5   | [\#AcquireControllerPowerSupply](#AcquireControllerPowerSupply "wikilink")           |
| 6   | [\#ReleaseControllerPowerSupply](#ReleaseControllerPowerSupply "wikilink")           |
| 7   | [\#OpenSession](#OpenSession "wikilink")                                             |
| 8   | [\#EnableEnoughPowerChargeEmulation](#EnableEnoughPowerChargeEmulation "wikilink")   |
| 9   | [\#DisableEnoughPowerChargeEmulation](#DisableEnoughPowerChargeEmulation "wikilink") |
| 10  | [\#EnableFastBatteryCharging](#EnableFastBatteryCharging "wikilink")                 |
| 11  | [\#DisableFastBatteryCharging](#DisableFastBatteryCharging "wikilink")               |
| 12  | [\#GetBatteryVoltageState](#GetBatteryVoltageState "wikilink")                       |
| 13  | [\#GetRawBatteryChargePercentage](#GetRawBatteryChargePercentage "wikilink")         |
| 14  | [\#IsEnoughPowerSupplied](#IsEnoughPowerSupplied "wikilink")                         |
| 15  | [\#GetBatteryAgePercentage](#GetBatteryAgePercentage "wikilink")                     |
| 16  | [\#GetBatteryChargeInfoEvent](#GetBatteryChargeInfoEvent "wikilink")                 |
| 17  | [\#GetBatteryChargeInfoFields](#GetBatteryChargeInfoFields "wikilink")               |
| 18  | \[3.0.0+\] GetBatteryChargeCalibratedEvent                                           |

## GetBatteryChargePercentage

No input, returns an output u32.

## GetChargerType

No input, returns an output u32.

## EnableBatteryCharging

No input/output.

## DisableBatteryCharging

No input/output.

## IsBatteryChargingEnabled

No input, returns an output u8.

## AcquireControllerPowerSupply

No input/output.

## ReleaseControllerPowerSupply

No input/output.

## OpenSession

No input, returns an output [\#IPsmSession](#IPsmSession "wikilink").

## EnableEnoughPowerChargeEmulation

No input/output.

## DisableEnoughPowerChargeEmulation

No input/output.

## EnableFastBatteryCharging

No input/output.

## DisableFastBatteryCharging

No input/output.

## GetBatteryVoltageState

No input, returns an output u32.

## GetRawBatteryChargePercentage

No input, returns an output u64.

## IsEnoughPowerSupplied

No input, returns an output u8.

## GetBatteryAgePercentage

No input, returns an output u64.

## GetBatteryChargeInfoEvent

No input, returns an output event.

## GetBatteryChargeInfoFields

No input, returns an output 0x40-byte struct.

## IPsmSession

This is "nn::psm::IPsmSession".

| Cmd | Name                                                                                               |
| --- | -------------------------------------------------------------------------------------------------- |
| 0   | [\#BindStateChangeEvent](#BindStateChangeEvent "wikilink")                                         |
| 1   | [\#UnbindStateChangeEvent](#UnbindStateChangeEvent "wikilink")                                     |
| 2   | [\#SetChargerTypeChangeEventEnabled](#SetChargerTypeChangeEventEnabled "wikilink")                 |
| 3   | [\#SetPowerSupplyChangeEventEnabled](#SetPowerSupplyChangeEventEnabled "wikilink")                 |
| 4   | [\#SetBatteryVoltageStateChangeEventEnabled](#SetBatteryVoltageStateChangeEventEnabled "wikilink") |

### BindStateChangeEvent

No input, returns an output event with autoclear disabled.

### UnbindStateChangeEvent

No input/output.

### SetChargerTypeChangeEventEnabled

Takes an input u8 bool, no output.

### SetPowerSupplyChangeEventEnabled

Takes an input u8 bool, no output.

### SetBatteryVoltageStateChangeEventEnabled

Takes an input u8 bool, no output.

# tc

This is "nn::tc::IManager".

| Cmd | Name                                |
| --- | ----------------------------------- |
| 0   | SetOperatingMode                    |
| 1   | GetThermalEvent                     |
| 2   | IsActionAllowed                     |
| 3   | EnableVirtualTemperature            |
| 4   | DisableVirtualTemperature           |
| 5   | SetVirtualTemperature               |
| 6   | EnableFanControl                    |
| 7   | DisableFanControl                   |
| 8   | IsFanControlEnabled                 |
| 9   | \[5.0.0+\] GetSkinTemperatureMilliC |

# ts

This is "nn::ts::server::IMeasurementServer".

| Cmd | Name                                                                                              |
| --- | ------------------------------------------------------------------------------------------------- |
| 0   | [\#GetTemperatureRange](#GetTemperatureRange "wikilink")                                          |
| 1   | [\#GetTemperature](#GetTemperature "wikilink")                                                    |
| 2   | [\#SetMeasurementMode](#SetMeasurementMode "wikilink")                                            |
| 3   | [\#GetTemperatureMilliC](#GetTemperatureMilliC "wikilink")                                        |
| 4   | \[8.0.0+\] ? (Takes a total of 4-bytes of input, returns an [\#IUnknown0](#IUnknown0 "wikilink")) |

## IUnknown0

Added with \[8.0.0+\].

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |
| 3   |      |

## GetTemperatureRange

Takes an u8 [\#Location](#Location "wikilink") and returns an s32
minimum temperature + s32 maximum temperature.

The returned temperature values are in Celsius.

## GetTemperature

Takes an u8 [\#Location](#Location "wikilink") and returns an output
s32.

The output is the temperature in Celsius.

## SetMeasurementMode

Takes an u8 [\#Location](#Location "wikilink") and an u8
MeasurementMode, no output.

## GetTemperatureMilliC

Takes an u8 [\#Location](#Location "wikilink") and returns an output
s32.

The output is the temperature in MilliC.

## Location

| Value | Name     |
| ----- | -------- |
| 0     | Internal |
| 1     | External |

# pcm

This is "nn::pcm::IManager".

| Cmd | Name             |
| --- | ---------------- |
| 0   | IsSupported      |
| 1   | ReadCurrentPower |

# apm:am

This is "nn::apm::IManager".

This was added with \[8.0.0+\] and replaces the old
[apm](PPC%20services#apm.md##apm "wikilink") service.

| Cmd | Name                                                                    |
| --- | ----------------------------------------------------------------------- |
| 0   | [\#OpenSession](#OpenSession "wikilink")                                |
| 1   | GetPerformanceMode                                                      |
| 6   | \[7.0.0+\] [\#IsCpuOverclockEnabled](#IsCpuOverclockEnabled "wikilink") |

## OpenSession

Returns an [\#ISession](#ISession "wikilink").

## IsCpuOverclockEnabled

No input, returns an output u8 bool.

# apm:sys

This is "nn::apm::ISystemManager".

| Cmd | Name                                                                                              |
| --- | ------------------------------------------------------------------------------------------------- |
| 0   | RequestPerformanceMode                                                                            |
| 1   | GetPerformanceEvent                                                                               |
| 2   | GetThrottlingState                                                                                |
| 3   | GetLastThrottlingState                                                                            |
| 4   | ClearLastThrottlingState                                                                          |
| 5   | \[5.0.0+\] LoadAndApplySettings                                                                   |
| 6   | \[7.0.0+\] [\#SetCpuBoostMode](#SetCpuBoostMode "wikilink")                                       |
| 7   | \[7.0.0+\] [\#GetCurrentPerformanceConfiguration](#GetCurrentPerformanceConfiguration "wikilink") |

## GetPerformanceEvent

Returns an [\#ISession](#ISession "wikilink").

## SetCpuBoostMode

Takes an u32 [\#CpuBoostMode](#CpuBoostMode "wikilink").

### CpuBoostMode

| Mode | Description                                                                                                                     |
| ---- | ------------------------------------------------------------------------------------------------------------------------------- |
| 0    | Disabled.                                                                                                                       |
| 1    | Use [performance configurations](#PerformanceConfiguration "wikilink") 0x92220009 and 0x9222000A, or 0x9222000B and 0x9222000C. |
| 2    | Use [performance configurations](#PerformanceConfiguration "wikilink") 0x9222000B and 0x9222000C.                               |

## GetCurrentPerformanceConfiguration

Returns the currently active
[\#PerformanceConfiguration](#PerformanceConfiguration "wikilink")
(default value is 0x00020003).

# ISession

This is "nn::apm::ISession".

| Cmd | Name                                                                      |
| --- | ------------------------------------------------------------------------- |
| 0   | SetPerformanceConfiguration                                               |
| 1   | GetPerformanceConfiguration                                               |
| 2   | \[8.0.0+\] [\#SetCpuOverclockEnabled](#SetCpuOverclockEnabled "wikilink") |

## SetPerformanceConfiguration

Takes an u32 [\#PerformanceMode](#PerformanceMode "wikilink") and an u32
[\#PerformanceConfiguration](#PerformanceConfiguration "wikilink").

## GetPerformanceConfiguration

Takes an u32 [\#PerformanceMode](#PerformanceMode "wikilink") and
returns an output u32
[\#PerformanceConfiguration](#PerformanceConfiguration "wikilink").

## SetCpuOverclockEnabled

Takes an input u8 bool, no output.

## PerformanceMode

| Value | Name     |
| ----- | -------- |
| 0     | Handheld |
| 1     | Docked   |

## PerformanceConfiguration

| Value                 | CPU clock | GPU clock | Memory clock |
| --------------------- | --------- | --------- | ------------ |
| 0x00010000            | 1020      | 384       | 1600         |
| 0x00010001            | 1020      | 768       | 1600         |
| 0x00010002            | 1224      | 691.2     | 1600         |
| 0x00020000            | 1020      | 230.4     | 1600         |
| 0x00020001            | 1020      | 307.2     | 1600         |
| 0x00020002            | 1224      | 230.4     | 1600         |
| 0x00020003            | 1020      | 307       | 1331.2       |
| 0x00020004            | 1020      | 384       | 1331.2       |
| 0x00020005            | 1020      | 307.2     | 1065.6       |
| 0x00020006            | 1020      | 384       | 1065.6       |
| 0x92220007            | 1020      | 460.8     | 1600         |
| 0x92220008            | 1020      | 460.8     | 1331.2       |
| \[7.0.0+\] 0x92220009 | 1785      | 768       | 1600         |
| \[7.0.0+\] 0x9222000A | 1785      | 768       | 1331.2       |
| \[7.0.0+\] 0x9222000B | 1020      | 768       | 1600         |
| \[7.0.0+\] 0x9222000C | 1020      | 768       | 1331.2       |

Clocks are all in MHz.

Configurations 0x10001 and 0x20000 are only available while docked.
Configurations 0x10002 and 0x20002 are only available for SDEV units.

# fgm, fgm:0, fgm:9

This is "nn::fgm::sf::ISession".

| Cmd | Name       |
| --- | ---------- |
| 0   | Initialize |

## IRequest

This is "nn::fgm::sf::IRequest".

| Cmd | Name       |
| --- | ---------- |
| 0   | Initialize |
| 1   | Set        |
| 2   | Get        |
| 3   | Cancel     |

# fgm:dbg

This is "nn::fgm::sf::IDebugger".

| Cmd | Name       |
| --- | ---------- |
| 0   | Initialize |
| 1   | Read       |
| 2   | Cancel     |

# Settings

| Key                                            | Size   | Notes                                                                                                           |
| ---------------------------------------------- | ------ | --------------------------------------------------------------------------------------------------------------- |
| background\_download\_stress\_testing\_storage | strlen | "sdcard", "builtin", "system".                                                                                  |
| battery\_draining\_enabled                     | 1      | ?                                                                                                               |
| fs\_access\_log\_mode                          | strlen | "log", "sdcard", "log+sdcard", "off".                                                                           |
| fs\_speed\_emulation\_mode                     | strlen | "faster", "slower", "random", "off".                                                                            |
| host\_romfs\_redirection\_target               | strlen | "builtin", "off".                                                                                               |
| idle\_time\_detect\_mode                       | strlen | "on", "off".                                                                                                    |
| initial\_tick\_value                           | strlen | "7days", "14days", "30days", "90days", "hex": ?.                                                                |
| memory\_mode                                   | strlen | "auto", "4GB", "6GB".                                                                                           |
| needs\_update\_vulnerability\_policy           | strlen | "default": ?, "force\_true": ?, "force\_false": ?.                                                              |
| operation\_mode\_policy                        | strlen | "auto": ?, "handheld", "console".                                                                               |
| performance\_mode\_policy                      | strlen | "auto": use boost mode when docked. "normal": never use boost mode. "boost": always use boost mode (SDEV only). |
| screenshot\_target                             | strlen | "screenshot": ?, "physical": ?.                                                                                 |
| sdev\_cpu\_overclock\_enabled                  | 1      | SDEV only. Used to allow access to 1224MHz CPU mode.                                                            |
| sdev\_throttling\_additional\_delay\_us        | 4      | SDEV only.                                                                                                      |
| sdev\_throttling\_additional\_delay\_enabled   | 1      | SDEV only.                                                                                                      |
| sleep\_mode                                    | strlen | "default": ?, "pseudo": ?.                                                                                      |
| throttling\_for\_smpd\_enabled                 | 1      | Not used as of 3.0.                                                                                             |
| throttling\_for\_undock\_enabled               | 1      | Not used as of 3.0.                                                                                             |

[Category:Services](Category:Services "wikilink")

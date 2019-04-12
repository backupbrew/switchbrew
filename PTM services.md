# fan

This is "nn::fan::detail::IManager".

| Cmd | Name           |
| --- | -------------- |
| 0   | OpenController |
|     |                |

## IController

This is "nn::fan::detail::IController".

| Cmd               | Name                        |
| ----------------- | --------------------------- |
| 0                 | SetRotationSpeedLevel       |
| 1                 | SetRotationSpeedLevelByDiff |
| 2                 | GetRotationSpeedLevel       |
| 3                 | SetRotationRate             |
| 4                 | GetRotationRate             |
| \[1.0.0-6.2.0\] 5 | EnableFan                   |
| \[1.0.0-6.2.0\] 6 | DisableFan                  |
| \[1.0.0-6.2.0\] 7 | GetActualRotationSpeedLevel |
|                   |                             |

\[7.0.0+\] SetRotationSpeedLevelByDiff/SetRotationRate no longer takes
any input. GetRotationRate no longer returns output. These were
presumably replaced with new cmds?

# psm

This is
"nn::psm::IPsmServer".

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
|     |                                                                                      |

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

This is
"nn::psm::IPsmSession".

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

| Cmd | Name             |
| --- | ---------------- |
| 0   | SetOperatingMode |
| 1   | GetThermalEvent  |
| 2   |                  |
| 3   |                  |
| 4   |                  |
| 5   |                  |
| 6   |                  |
| 7   |                  |
| 8   |                  |
|     |                  |

# ts

This is "nn::ts::server::IMeasurementServer".

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |
| 3   |      |
|     |      |

# pcm

This is "nn::pcm::IManager".

| Cmd | Name             |
| --- | ---------------- |
| 0   | IsSupported      |
| 1   | ReadCurrentPower |

[Category:Services](Category:Services "wikilink")

# lbl

This is
"nn::lbl::detail::ILblController".

| Cmd | Name                                                                   |
| --- | ---------------------------------------------------------------------- |
| 0   | SaveCurrentSetting                                                     |
| 1   | LoadCurrentSetting                                                     |
| 2   | SetCurrentBrightnessSetting                                            |
| 3   | GetCurrentBrightnessSetting                                            |
| 4   | ApplyCurrentBrightnessSettingToBacklight                               |
| 5   | GetBrightnessSettingAppliedToBacklight                                 |
| 6   | SwitchBacklightOn                                                      |
| 7   | SwitchBacklightOff                                                     |
| 8   | GetBacklightSwitchStatus                                               |
| 9   | EnableDimming                                                          |
| 10  | DisableDimming                                                         |
| 11  | IsDimmingEnabled                                                       |
| 12  | EnableAutoBrightnessControl                                            |
| 13  | DisableAutoBrightnessControl                                           |
| 14  | IsAutoBrightnessControlEnabled                                         |
| 15  | SetAmbientLightSensorValue                                             |
| 16  | [\#GetAmbientLightSensorValue](#GetAmbientLightSensorValue "wikilink") |
| 17  | SetBrightnessReflectionDelayLevel                                      |
| 18  | GetBrightnessReflectionDelayLevel                                      |
| 19  | SetCurrentBrightnessMapping                                            |
| 20  | GetCurrentBrightnessMapping                                            |
| 21  | SetCurrentAmbientLightSensorMapping                                    |
| 22  | GetCurrentAmbientLightSensorMapping                                    |
| 23  | \[3.0.0+\] IsAmbientLightSensorAvailable                               |
| 24  | \[3.0.0+\] SetCurrentBrightnessSettingForVrMode                        |
| 25  | \[3.0.0+\] GetCurrentBrightnessSettingForVrMode                        |
| 26  | \[3.0.0+\] [\#EnableVrMode](#EnableVrMode "wikilink")                  |
| 27  | \[3.0.0+\] [\#DisableVrMode](#DisableVrMode "wikilink")                |
| 28  | \[3.0.0+\] [\#IsVrModeEnabled](#IsVrModeEnabled "wikilink")            |
| 29  | \[7.0.0+\]                                                             |

## Ambient Light Sensor Notes

The BH1730 outputs 2 values. Visible light and IR light. This is then
calculated through an algorithm that checks for Gain, Measurement time,
filter qualities and ouputs lux (max correct measurement of 100K lux).
The default values are Gain 64x and ITIME of 38 (256 - 218). This allows
for a max lux value of 17972 lux when visible light value is maximum and
IR light is 0. When both of them are on their limit, the output is 1192
lux. The sensor is fully configurable.

## GetAmbientLightSensorValue

No input. Before 5.x, outputs lux in float. (5.0.0+) Returns an output
struct:

| Offset | Size | Description                                                              |
| ------ | ---- | ------------------------------------------------------------------------ |
| 0x0    | 0x4  | bOverLimit. (u32) Equals to 1 if visible or IR light data is over 65534. |
| 0x4    | 0x4  | fLux. (float) Value in lux from the ambient light sensor.                |

Note: if bOverLimit=1 and the default ALS configuration is used, the
measurement of fLux should not be considered and the actual max value
depends on the type of light. Ranges from 12.5K - 17.5K.

## GetCurrentBrightnessSetting

No input. Returns an output u32 int of the current backlight level.

## GetBrightnessSettingAppliedToBacklight

No input. Returns an output u32 int of the backlight level computed from
the ambient light sensor.

## IsAutoBrightnessControlEnabled

No input. Returns an output u8 bool indicating whether auto brightness
is enabled.

## EnableVrMode

No input/output. Used by
[AM\_services\#SetVrModeEnabled](AM%20services#SetVrModeEnabled.md##SetVrModeEnabled "wikilink").

Sets a global state field to 0x1.

## DisableVrMode

No input/output. Used by
[AM\_services\#SetVrModeEnabled](AM%20services#SetVrModeEnabled.md##SetVrModeEnabled "wikilink").

Sets the global state field used by
[\#EnableVrMode](#EnableVrMode "wikilink") to 0x0.

## IsVrModeEnabled

No input. Returns an output u8 bool set by the above commands.

[Category:Services](Category:Services "wikilink")

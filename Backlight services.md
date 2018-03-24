# lbl

This is "nn::lbl::detail::ILblController".

| Cmd | Name                                                    |
| --- | ------------------------------------------------------- |
| 0   |                                                         |
| 1   |                                                         |
| 2   |                                                         |
| 3   |                                                         |
| 4   |                                                         |
| 5   |                                                         |
| 6   | TurnOnBacklight                                         |
| 7   | TurnOffBacklight                                        |
| 8   | GetBacklightStatus                                      |
| 9   |                                                         |
| 10  |                                                         |
| 11  |                                                         |
| 12  |                                                         |
| 13  |                                                         |
| 14  |                                                         |
| 15  |                                                         |
| 16  | ReadRawLightSensor                                      |
| 17  |                                                         |
| 18  |                                                         |
| 19  |                                                         |
| 20  |                                                         |
| 21  |                                                         |
| 22  |                                                         |
| 23  | \[3.0.0+\]                                              |
| 24  | \[3.0.0+\]                                              |
| 25  | \[3.0.0+\]                                              |
| 26  | \[3.0.0+\] [\#EnableVrMode](#EnableVrMode "wikilink")   |
| 27  | \[3.0.0+\] [\#DisableVrMode](#DisableVrMode "wikilink") |
| 28  | \[3.0.0+\] [\#GetVrMode](#GetVrMode "wikilink")         |

## EnableVrMode

No input/output. Used by
[AM\_services\#SetVrModeEnabled](AM%20services#SetVrModeEnabled.md##SetVrModeEnabled "wikilink").

Sets a global state field to 0x1.

## DisableVrMode

No input/output. Used by
[AM\_services\#SetVrModeEnabled](AM%20services#SetVrModeEnabled.md##SetVrModeEnabled "wikilink").

Sets the global state field used by
[\#EnableVrMode](#EnableVrMode "wikilink") to 0x0.

## GetVrMode

No input. Returns an output u8 bool set by the above commands.

[Category:Services](Category:Services "wikilink")

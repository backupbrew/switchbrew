# fan

This is "nn::fan::detail::IManager".

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |
| 3   |      |
| 4   |      |
| 5   |      |
| 6   |      |
| 7   |      |
|     |      |

# psm

This is "nn::psm::IPsmServer".

| Cmd | Name                          |
| --- | ----------------------------- |
| 0   |                               |
| 1   |                               |
| 2   |                               |
| 3   |                               |
| 4   |                               |
| 5   |                               |
| 6   |                               |
| 7   | OpenSession                   |
| 8   |                               |
| 9   |                               |
| 10  |                               |
| 11  |                               |
| 12  | GetBatteryVoltageState        |
| 13  | GetRawBatteryChargePercentage |
| 14  |                               |
| 15  |                               |
| 16  |                               |
| 17  |                               |
|     |                               |

## IPsmSession

This is "nn::psm::IPsmSession".

| Cmd | Name                                     |
| --- | ---------------------------------------- |
| 0   | BindStateChangeEvent                     |
| 1   | UnbindStateChangeEvent                   |
| 2   | SetChargerTypeChangeEventEnabled         |
| 3   | SetPowerSupplyChangeEventEnabled         |
| 4   | SetBatteryVoltageStateChangeEventEnabled |

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

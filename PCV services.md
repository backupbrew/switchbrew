# bpc

This is "nn::bpc::IBoardPowerControlManager".

| Cmd | Name                      |
| --- | ------------------------- |
| 0   | ShutdownSystem            |
| 1   | RebootSystem              |
| 2   | GetWakeupReason           |
| 3   | GetShutdownReason         |
| 4   | GetAcOk                   |
| 5   | GetBoardPowerControlEvent |
| 6   | GetSleepButtonState       |
| 7   | GetPowerEvent             |
| 8   |                           |
| 9   |                           |
| 10  |                           |

# bpc:r

This is "nn::bpc::IRtcManager".

| Cmd | Name                      |
| --- | ------------------------- |
| 0   | GetExternalRtcValue       |
| 1   | SetExternalRtcValue       |
| 2   | ReadExternalRtcResetFlag  |
| 3   | ClearExternalRtcResetFlag |

GetExternalRtcValue / SetExternalRtcValue directly accesses the
max77620\_rtc0 device.

# pcv

This is "nn::pcv::detail::IPcvService".

| Cmd | Name                     |
| --- | ------------------------ |
| 0   | SetPowerEnabled          |
| 1   | SetClockEnabled          |
| 2   | SetClockRate             |
| 3   | GetClockRate             |
| 4   | GetState                 |
| 5   | GetPossibleClockRates    |
| 6   | SetMinVClockRate         |
| 7   | SetReset                 |
| 8   | SetVoltageEnabled        |
| 9   | GetVoltageEnabled        |
| 10  | GetVoltageRange          |
| 11  | SetVoltageValue          |
| 12  | GetVoltageValue          |
| 13  | GetTemperatureThresholds |
| 14  | SetTemperature           |
| 15  | Initialize               |
| 16  | IsInitialized            |
| 17  | Finalize                 |
| 18  | PowerOn                  |
| 19  | PowerOff                 |
| 20  | ChangeVoltage            |
| 21  | GetPowerClockInfoEvent   |
| 22  | GetOscillatorClock       |
| 23  | GetDvfsTable             |
| 24  | GetModuleStateTable      |
| 25  | GetPowerDomainStateTable |
| 26  | GetFuseInfo              |
|     |                          |

## User Name to Block Maps

### Power Switch / Clocking / Reset

| Name | Block                | Rail     | Notes                                       |
| ---- | -------------------- | -------- | ------------------------------------------- |
| 0    | CpuBus               | vdd\_cpu |                                             |
| 1    | GPU                  | vdd\_gpu |                                             |
| 2    | I2S1                 | vdd\_soc |                                             |
| 3    | I2S2                 | vdd\_soc |                                             |
| 4    | I2S3                 | vdd\_soc |                                             |
| 5    | PWM                  | vdd\_soc |                                             |
| 6    | I2C1                 | vdd\_soc |                                             |
| 7    | I2C2                 | vdd\_soc |                                             |
| 8    | I2C3                 | vdd\_soc |                                             |
| 9    | I2C4                 | vdd\_soc |                                             |
| 10   | I2C5                 | vdd\_soc |                                             |
| 11   | I2C6                 | vdd\_soc |                                             |
| 12   | SPI1                 | vdd\_soc |                                             |
| 13   | SPI2                 | vdd\_soc |                                             |
| 14   | SPI3                 | vdd\_soc |                                             |
| 15   | SPI4                 | vdd\_soc |                                             |
| 16   | DISP1                | vdd\_soc |                                             |
| 17   | DISP2                | vdd\_soc |                                             |
| 20   | SDMMC1               | vdd\_soc |                                             |
| 21   | SDMMC2               | vdd\_soc |                                             |
| 22   | SDMMC3               | vdd\_soc |                                             |
| 23   | SDMMC4               | vdd\_soc |                                             |
| 24   | \-                   | \-       | Not actual block. Used for debug and stuff. |
| 25   | CSITE                | vdd\_soc |                                             |
| 26   | TSEC                 | vdd\_soc |                                             |
| 27   | MSELECT              | vdd\_soc |                                             |
| 28   | HDA2CODEC\_2X        | vdd\_soc |                                             |
| 29   | ACTMON               | vdd\_soc |                                             |
| 30   | I2C\_SLOW            | vdd\_soc |                                             |
| 31   | SOR1                 | vdd\_soc |                                             |
| 33   | HDA                  | vdd\_soc |                                             |
| 34   | XUSB\_CORE\_HOST     | vdd\_soc |                                             |
| 35   | XUSB\_FALCON         | vdd\_soc |                                             |
| 36   | XUSB\_FS             | vdd\_soc |                                             |
| 37   | XUSB\_CORE\_DEV      | vdd\_soc |                                             |
| 38   | XUSB\_SS\_HOSTDEV    | vdd\_soc |                                             |
| 39   | UARTA                | vdd\_soc |                                             |
| 40   | UARTB                | vdd\_soc |                                             |
| 41   | UARTC                | vdd\_soc |                                             |
| 42   | UARTD                | vdd\_soc |                                             |
| 43   | HOST1X               | vdd\_soc |                                             |
| 44   | ENTROPY              | vdd\_soc |                                             |
| 45   | SOC\_THERM           | vdd\_soc |                                             |
| 46   | VIC                  | vdd\_soc |                                             |
| 47   | NVENC                | vdd\_soc |                                             |
| 48   | NVJPG                | vdd\_soc |                                             |
| 49   | NVDEC                | vdd\_soc |                                             |
| 50   | QSPI                 | vdd\_soc |                                             |
| 52   | TSECB                | vdd\_soc |                                             |
| 53   | APE                  | vdd\_soc |                                             |
| 54   | ACLK                 | vdd\_soc |                                             |
| 55   | UARTAPE              | vdd\_soc |                                             |
| 56   | EMC                  | vdd\_soc |                                             |
| 57   | PLLE0                | vdd\_soc |                                             |
| 58   | PLLE0                | vdd\_soc |                                             |
| 59   | DSI                  | vdd\_soc |                                             |
| 60   | MAUD                 | vdd\_soc |                                             |
| 61   | DPAUX1               | vdd\_soc |                                             |
| 62   | MIPI\_CAL            | vdd\_soc |                                             |
| 63   | UART\_FST\_MIPI\_CAL | vdd\_soc |                                             |
| 64   | OSC                  | vdd\_soc |                                             |
| 65   | SCLK                 | vdd\_soc |                                             |
| 66   | SOR\_SAFE            | vdd\_soc |                                             |
| 67   | XUSB\_SS             | vdd\_soc |                                             |
| 68   | XUSB\_HOST           | vdd\_soc |                                             |
| 69   | XUSB\_DEV            | vdd\_soc |                                             |
| 70   | EXTPERIPH1           | vdd\_soc |                                             |
| 71   | AHUB                 | vdd\_soc |                                             |
| 72   | HDA2HDMICODEC        | vdd\_soc |                                             |
| 73   | PLLP5                | vdd\_soc |                                             |
| 74   | USBD                 | vdd\_soc |                                             |
| 75   | USB2                 | vdd\_soc |                                             |
| 76   | PCIE                 | vdd\_soc |                                             |
| 77   | AFI                  | vdd\_soc |                                             |
| 78   | PCIEXCLK             | vdd\_soc |                                             |
| 79   | PEX\_USB\_UPHY       | vdd\_soc |                                             |
| 80   | XUSB\_PADCTL         | vdd\_soc |                                             |
| 81   | APBDMA               | vdd\_soc |                                             |
| 82   | USB2\_TRK            | vdd\_soc |                                             |
| 83   | PLLE0                | vdd\_soc |                                             |
| 84   | PLLE0                | vdd\_soc |                                             |
| 85   | CEC                  | vdd\_soc |                                             |
|      |                      |          |                                             |

### Voltage

| Name | Block          | Notes |
| ---- | -------------- | ----- |
| 0    | max77620\_sd0  |       |
| 1    | max77620\_sd1  |       |
| 2    | max77620\_sd2  |       |
| 3    | max77620\_sd3  |       |
| 4    | max77620\_ldo0 |       |
| 5    | max77620\_ldo1 |       |
| 6    | max77620\_ldo2 |       |
| 7    | max77620\_ldo3 |       |
| 8    | max77620\_ldo4 |       |
| 9    | max77620\_ldo5 |       |
| 10   | max77620\_ldo6 |       |
| 11   | max77620\_ldo7 |       |
| 12   | max77620\_ldo8 |       |
| 13   | max77621\_cpu  |       |
| 14   | max77621\_gpu  |       |
|      |                |       |

Note: max77620 GPIOs are only used internally by the driver during init,
and not exposed via an API.

# pcv:arb

This is "nn::pcv::IArbitrationManager".

| Cmd | Name           |
| --- | -------------- |
| 0   | ReleaseControl |
|     |                |

# pcv:imm

This is "nn::pcv::IImmediateManager".

| Cmd | Name         |
| --- | ------------ |
| 0   | SetClockRate |
|     |              |

# time:u, time:a, time:s

This is
"nn::timesrv::detail::<service::IStaticService>".

| Cmd | Name                                                 | Notes                                                          |
| --- | ---------------------------------------------------- | -------------------------------------------------------------- |
| 0   | GetStandardUserSystemClock                           | Returns an [\#ISystemClock](#ISystemClock "wikilink").         |
| 1   | GetStandardNetworkSystemClock                        | Returns an [\#ISystemClock](#ISystemClock "wikilink").         |
| 2   | GetStandardSteadyClock                               | Returns an [\#ISteadyClock](#ISteadyClock "wikilink").         |
| 3   | GetTimeZoneService                                   | Returns an [\#ITimeZoneService](#ITimeZoneService "wikilink"). |
| 4   | GetStandardLocalSystemClock                          | Returns an [\#ISystemClock](#ISystemClock "wikilink").         |
| 100 | IsStandardUserSystemClockAutomaticCorrectionEnabled  |                                                                |
| 101 | SetStandardUserSystemClockAutomaticCorrectionEnabled |                                                                |
| 200 | IsStandardNetworkSystemClockAccuracySufficient       |                                                                |
|     |                                                      |                                                                |

## ISteadyClock

| Cmd | Name                | Notes                                                                                   |
| --- | ------------------- | --------------------------------------------------------------------------------------- |
| 0   | GetCurrentTimePoint | No input, returns an output [\#SteadyClockTimePoint](#SteadyClockTimePoint "wikilink"). |
| 2   | GetTestOffset       | No input, returns an output [\#TimeSpanType](#TimeSpanType "wikilink").                 |
| 3   | SetTestOffset       | Takes an input [\#TimeSpanType](#TimeSpanType "wikilink"), no output.                   |
| 100 | GetRtcValue         | No input, returns an output s64.                                                        |
| 101 | IsRtcResetDetected  | No input, returns an output u8 bool.                                                    |
| 102 | GetSetupResultValue | No input, returns an output u32.                                                        |
| 200 | GetInternalOffset   | No input, returns an output [\#TimeSpanType](#TimeSpanType "wikilink").                 |
| 201 | SetInternalOffset   | Takes an input [\#TimeSpanType](#TimeSpanType "wikilink"), no output.                   |
|     |                     |                                                                                         |

### SteadyClockTimePoint

This is a 0x18-byte struct.

### TimeSpanType

This is an
u64.

## ISystemClock

| Cmd | Name                  | Notes                                                                     |
| --- | --------------------- | ------------------------------------------------------------------------- |
| 0   | GetCurrentTime        | Returns an output [\#PosixTime](#PosixTime "wikilink").                   |
| 1   | SetCurrentTime        | Takes an input [\#PosixTime](#PosixTime "wikilink").                      |
| 2   | GetSystemClockContext | Returns an output [\#SystemClockContext](#SystemClockContext "wikilink"). |
| 3   | SetSystemClockContext | Takes an input [\#SystemClockContext](#SystemClockContext "wikilink").    |
|     |                       |                                                                           |

### PosixTime

This is an u64 for UTC POSIX time.

### SystemClockContext

This is an 0x20-byte
struct.

## ITimeZoneService

| Cmd | Name                      | Notes                                                         |
| --- | ------------------------- | ------------------------------------------------------------- |
| 0   | GetDeviceLocationName     | Returns an output [\#LocationName](#LocationName "wikilink"). |
| 1   | SetDeviceLocationName     | Takes an input [\#LocationName](#LocationName "wikilink").    |
| 2   | GetTotalLocationNameCount | No input, returns an output u32.                              |
| 3   | LoadLocationNameList      |                                                               |
| 4   | LoadTimeZoneRule          |                                                               |
| 5   | GetTimeZoneRuleVersion    |                                                               |
| 100 | ToCalendarTime            |                                                               |
| 101 | ToCalendarTimeWithMyRule  |                                                               |
| 200 | ToPosixTime               |                                                               |
| 201 | ToPosixTimeWithMyRule     |                                                               |
|     |                           |                                                               |

### LocationName

| Offset | Size | Description                              |
| ------ | ---- | ---------------------------------------- |
| 0x0    | 0x10 | Location name string, no NUL-terminator. |
| 0x10   | ?    |                                          |
| 0x18   | 0x8? | ?                                        |
| 0x20   | ?    | ?                                        |

This is an 0x24-byte struct.

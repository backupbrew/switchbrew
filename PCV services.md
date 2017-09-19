# bpc

| Cmd | Name                     |
| --- | ------------------------ |
| 0   | ShutdownConsole          |
| 1   | RebootConsole            |
| 2   |                          |
| 3   |                          |
| 4   |                          |
| 5   | Returns an event handle. |
| 6   |                          |
| 7   | Returns an event handle. |
| 8   |                          |
| 9   |                          |
| 10  |                          |

# bpc:r

# pcv

| Cmd | Name            |
| --- | --------------- |
| 0   | SetPowerEnabled |
| 1   | SetClockEnabled |
| 2   |                 |
| 3   |                 |
| 4   |                 |
| 5   |                 |
| 6   |                 |
| 7   | SetReset        |
| 8   |                 |
| 9   |                 |
| 10  |                 |
| 11  |                 |
| 12  |                 |
| 13  |                 |
| 14  |                 |
| 15  |                 |
| 16  |                 |
| 17  |                 |
|     |                 |

# pcv:arb

| Cmd | Name |
| --- | ---- |
| 0   |      |
|     |      |

# pcv:imm

| Cmd | Name |
| --- | ---- |
| 0   |      |
|     |      |

# time:u, time:a, time:s

The following is
"nn::timesrv::detail::<service::IStaticService>"

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

# ISteadyClock

| Cmd | Name                |
| --- | ------------------- |
| 0   | GetCurrentTimePoint |
| 2   | GetTestOffset       |
| 3   | SetTestOffset       |
| 100 | GetRtcValue         |
| 101 | IsRtcResetDetected  |
| 102 | GetSetupResultValue |
| 200 | GetInternalOffset   |
| 201 | SetInternalOffset   |
|     |                     |

# ISystemClock

# ITimeZoneService

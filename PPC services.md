APM is utilized for setting system performance profiles including clocks
for CPU, GPU, and memory.

# apm

This is "nn::apm::IManager".

| Cmd | Name                                     |
| --- | ---------------------------------------- |
| 0   | [\#OpenSession](#OpenSession "wikilink") |
| 1   | GetPerformanceMode                       |
| 6   | IsCpuOverclockEnabled                    |

## OpenSession

Returns an [\#ISession](#ISession "wikilink").

# apm:p

This is "nn::apm::IManagerPrivileged".

| Cmd | Name        |
| --- | ----------- |
| 0   | OpenSession |

## OpenSession

Returns an [\#ISession](#ISession "wikilink").

# apm:sys

This is
"nn::apm::ISystemManager".

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

Takes an u32
[\#CpuBoostMode](#CpuBoostMode "wikilink").

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

| Cmd | Name                        |
| --- | --------------------------- |
| 0   | SetPerformanceConfiguration |
| 1   | GetPerformanceConfiguration |

## SetPerformanceConfiguration

Takes an u32 [\#PerformanceMode](#PerformanceMode "wikilink") and an u32
[\#PerformanceConfiguration](#PerformanceConfiguration "wikilink").

## GetPerformanceConfiguration

Takes an u32 [\#PerformanceMode](#PerformanceMode "wikilink") and
returns an output u32
[\#PerformanceConfiguration](#PerformanceConfiguration "wikilink").

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

Some of these require apm:p.

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

| Key                                          | Size   | Notes                                                                                                           |
| -------------------------------------------- | ------ | --------------------------------------------------------------------------------------------------------------- |
| battery\_draining\_enabled                   | 1      | ?                                                                                                               |
| performance\_mode\_policy                    | strlen | "auto": use boost mode when docked. "normal": never use boost mode. "boost": always use boost mode (SDEV only). |
| sdev\_cpu\_overclock\_enabled                | 1      | SDEV only. Used to allow access to 1224MHz CPU mode.                                                            |
| sdev\_throttling\_additional\_delay\_us      | 4      | SDEV only.                                                                                                      |
| sdev\_throttling\_additional\_delay\_enabled | 1      | SDEV only.                                                                                                      |
| throttling\_for\_smpd\_enabled               | 1      | Not used as of 3.0.                                                                                             |
| throttling\_for\_undock\_enabled             | 1      | Not used as of 3.0.                                                                                             |

[Category:Services](Category:Services "wikilink")

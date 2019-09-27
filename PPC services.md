APM is utilized for setting system performance profiles including clocks
for CPU, GPU, and memory.

\[9.0.0+\] The PPC system module is now stubbed and all its services
were moved into [PTM](PTM%20services.md "wikilink").

# apm

This is "nn::apm::IManager".

This was moved to [AM](Applet%20Manager%20services.md "wikilink") with
\[8.0.0+\] and is now a shim for [apm:am](#apm:am "wikilink").

| Cmd | Name                                                                    |
| --- | ----------------------------------------------------------------------- |
| 0   | [\#OpenSession](#OpenSession "wikilink")                                |
| 1   | GetPerformanceMode                                                      |
| 6   | \[7.0.0+\] [\#IsCpuOverclockEnabled](#IsCpuOverclockEnabled "wikilink") |

## OpenSession

Returns an [\#ISession](#ISession "wikilink").

## IsCpuOverclockEnabled

No input, returns an output u8 bool.

# apm:p

This is "nn::apm::IManagerPrivileged".

This service no longer exists in \[8.0.0+\].

| Cmd | Name        |
| --- | ----------- |
| 0   | OpenSession |

## OpenSession

Returns an [\#ISession](#ISession "wikilink").

# apm:am

This is "nn::apm::IManager".

This was added with \[8.0.0+\] and is the same as the old
[apm](#apm "wikilink") service.

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

| Mode | Description                                                                                                                                                                       |
| ---- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0    | Disabled.                                                                                                                                                                         |
| 1    | Boost CPU. Additionally, throttle GPU to minimum. Use [performance configurations](#PerformanceConfiguration "wikilink") 0x92220009 and 0x9222000A, or 0x9222000B and 0x9222000C. |
| 2    | Conserve power. Only throttle GPU to minimum. Use [performance configurations](#PerformanceConfiguration "wikilink") 0x9222000B and 0x9222000C.                                   |

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
| 0x00010000            | 1020.0    | 384.0     | 1600.0       |
| 0x00010001            | 1020.0    | 768.0     | 1600.0       |
| 0x00010002            | 1224.0    | 691.2     | 1600.0       |
| 0x00020000            | 1020.0    | 230.4     | 1600.0       |
| 0x00020001            | 1020.0    | 307.2     | 1600.0       |
| 0x00020002            | 1224.0    | 230.4     | 1600.0       |
| 0x00020003            | 1020.0    | 307.2     | 1331.2       |
| 0x00020004            | 1020.0    | 384.0     | 1331.2       |
| 0x00020005            | 1020.0    | 307.2     | 1065.6       |
| 0x00020006            | 1020.0    | 384.0     | 1065.6       |
| 0x92220007            | 1020.0    | 460.8     | 1600.0       |
| 0x92220008            | 1020.0    | 460.8     | 1331.2       |
| \[7.0.0+\] 0x92220009 | 1785.0    | 76.8      | 1600.0       |
| \[7.0.0+\] 0x9222000A | 1785.0    | 76.8      | 1331.2       |
| \[7.0.0+\] 0x9222000B | 1020.0    | 76.8      | 1600.0       |
| \[7.0.0+\] 0x9222000C | 1020.0    | 76.8      | 1331.2       |

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

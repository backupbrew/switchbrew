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

# vi:u "ApplicationRootService"

| Cmd | Name                                         |
| --- | -------------------------------------------- |
| 0   | RegisterInterface\_ApplicationDisplayService |
|     |                                              |

# vi:m "ManagerRootService"

| Cmd | Name                                          |
| --- | --------------------------------------------- |
| 2   | RegisterInterface\_ApplicationDisplayService  |
| 3   | RegisterInterface2\_ApplicationDisplayService |
|     |                                               |

# vi:s "SystemRootService"

| Cmd | Name                                          |
| --- | --------------------------------------------- |
| 1   | RegisterInterface\_ApplicationDisplayService  |
| 3   | RegisterInterface2\_ApplicationDisplayService |
|     |                                               |

# IApplicationDisplayService

| Cmd  | Name                                     |
| ---- | ---------------------------------------- |
| 100  | RegisterInterface\_HOSBinderDriver       |
| 101  | RegisterInterface\_SystemDisplayService  |
| 102  | RegisterInterface\_ManagerDisplayService |
| 103  | RegisterInterface2\_HOSBinderDriver      |
| 1000 | GetDisplayProfiles                       |
| 1010 |                                          |
| 1011 |                                          |
| 1020 |                                          |
| 1101 |                                          |
| 1102 | GetDisplaySize                           |
| 2020 |                                          |
| 2021 |                                          |
| 2030 |                                          |
| 2031 |                                          |
| 2101 |                                          |
| 2450 |                                          |
| 2451 |                                          |
| 2460 |                                          |
| 5202 |                                          |
| 5203 |                                          |
|      |                                          |

# IHOSBinderDriver

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |
|     |      |

# ISystemDisplayService

| Cmd  | Name |
| ---- | ---- |
| 1200 |      |
| 1202 |      |
| 1203 |      |
| 2201 |      |
| 2203 |      |
| 2204 |      |
| 2205 |      |
| 2207 |      |
| 2209 |      |
| 2312 |      |
| 2400 |      |
| 2401 |      |
| 2402 |      |
| 3000 |      |
| 3001 |      |
| 3002 |      |
| 3200 |      |
| 3201 |      |
| 3202 |      |
| 3203 |      |
| 3204 |      |
| 3205 |      |
| 3206 |      |
| 3207 |      |
| 3208 |      |
| 3209 |      |
| 3210 |      |
| 3211 |      |
| 3214 |      |
| 3215 |      |
| 3216 |      |
| 3217 |      |
|      |      |

# IManagerDisplayService

| Cmd  | Name |
| ---- | ---- |
| 2010 |      |
| 2011 |      |
| 2050 |      |
| 2051 |      |
| 2052 |      |
| 2053 |      |
| 2054 |      |
| 2055 |      |
| 2300 |      |
| 2301 |      |
| 2302 |      |
| 2402 |      |
| 4201 |      |
| 4203 |      |
| 4205 |      |
| 6000 |      |
| 6001 |      |
| 6002 |      |
| 7000 |      |
| 8000 |      |
| 8100 |      |

[Category:Services](Category:Services "wikilink")

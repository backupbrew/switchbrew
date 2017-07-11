APM is utilized for setting system performance profiles; including
clocks for CPU, GPU, and memory.

## apm

| Cmd | Name                                | Notes |
| --- | ----------------------------------- | ----- |
| 0   | [GetISession](#ISession "wikilink") |       |
| 1   | GetPerformanceMode                  |       |

### ISession

| Cmd | Name                        | Notes                                                   |
| --- | --------------------------- | ------------------------------------------------------- |
| 0   | SetPerformanceConfiguration | Takes u32 PerformanceMode                               |
| 1   | GetPerformanceConfiguration | Takes u32 PerformanceMode, u32 PerformanceConfiguration |

### PerformanceMode

| Value | Name     |
| ----- | -------- |
| 0     | Handheld |
| 1     | Docked   |

### PerformanceConfiguration

| Value      | Name              |
| ---------- | ----------------- |
| 0x10000    | Docked profiles   |
| 0x10001    |                   |
| 0x10002    |                   |
| 0x20000    | Handheld profiles |
| 0x20001    |                   |
| 0x20002    |                   |
| 0x20003    |                   |
| 0x20004    |                   |
| 0x20005    |                   |
| 0x20006    |                   |
| 0x92220007 | Unknown profiles  |
| 0x92220008 |                   |

The lower 16 bits seem to loosely indicate relative profile performance,
with higher values being slower. Unknown profiles can be applied in
handheld mode (these may be ultra-low-power modes).

## apm:p

## apm:sys

[Category:Services](Category:Services "wikilink")

# pm:bm

| Cmd | Name                  |
| --- | --------------------- |
| 0   | GetMaintenanceMode?   |
| 1   | EnableMaintenanceMode |

# pm:info

| Cmd | Name              |
| --- | ----------------- |
| 0   | GetProcessTitleID |

# pm:shell

| Cmd | Name                                                |
| --- | --------------------------------------------------- |
| 0   | LaunchProcess                                       |
| 1   | TerminatePid                                        |
| 2   |                                                     |
| 3   | GetProcessEventWaiter                               |
| 4   | GetProcessEventType (0=CONTINUE, 1=CRASHING, 2,3,5) |
| 5   | FinalizeEventType2                                  |
| 6   | FinalizeCrashingProcess                             |
| 7   |                                                     |
| 8   | GetCrashingProcessPid                               |

[Category:Services](Category:Services "wikilink")

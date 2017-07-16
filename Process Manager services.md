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
| 1   | TerminateProcessByPid                               |
| 2   | TerminateProcessByTitleID                           |
| 3   | GetProcessEventWaiter                               |
| 4   | GetProcessEventType (0=CONTINUE, 1=CRASHING, 2,3,5) |
| 5   | FinalizeEventType2                                  |
| 6   | FinalizeCrashingProcess                             |
| 7   | NotifyBootFinished                                  |
| 8   | GetCrashingProcessPid                               |

[Category:Services](Category:Services "wikilink")

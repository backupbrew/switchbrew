# pm:bm

| Cmd | Name                  |
| --- | --------------------- |
| 0   | GetMaintenanceMode    |
| 1   | EnableMaintenanceMode |

# pm:info

| Cmd | Name              |
| --- | ----------------- |
| 0   | GetProcessTitleID |

# pm:shell

| Cmd | Name                                                             |
| --- | ---------------------------------------------------------------- |
| 0   | LaunchProcess                                                    |
| 1   | TerminateProcessByPid                                            |
| 2   | TerminateProcessByTitleID                                        |
| 3   | GetProcessEventWaiter                                            |
| 4   | GetProcessEventType (0=CONTINUE, 1=CRASHING, 2,3,5)              |
| 5   | [\#FinalizeDeadProcess](#FinalizeDeadProcess "wikilink")         |
| 6   | [\#ClearProcessCrashedFlag](#ClearProcessCrashedFlag "wikilink") |
| 7   | [\#NotifyBootFinished](#NotifyBootFinished "wikilink")           |
| 8   | [\#GetCrashingProcessPid](#GetCrashingProcessPid "wikilink")     |

## FinalizeDeadProcess

Takes a pid as input. If the process with pid has the state "dead", it
unregisters the pid in fsp:pr, sm:m, and ldr:pm.

Then it removes the process from PMs internal linked-list of active
processes.

## ClearProcessCrashedFlag

Takes a pid as input. Clears 0x10 from process flags.

## NotifyBootFinished

Launches a process with hardcoded [boot2](Boot2.md "wikilink") title-id.

## GetCrashingProcessPid

Loops through the internal linked-list of processes, looks for mask 0x40
set in process flags. Returns pid of first such entry.

[Category:Services](Category:Services "wikilink")

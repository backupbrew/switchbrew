PM has a separate thread that is waiting for synchronization on process
handles.

When the kernel signals a process handle, it uses svcResetSignal on the
process handle and then it uses svcGetProcessInfo to read out the
ProcessState.

If the process moved state non-3 -\> 3 it clears bit4 in process flags.

If process flags has mask 8 set:

  - If new state is 2, it clears 0x20 and sets 0x10 in process flags,
    and signals the ProcessEventWaiter handle.
  - If new state is 4, it clears 0x20 and sets 0x10 in process flags,
    and signals the ProcessEventWaiter handle.
  - If new state is 7, it sets 0x30 in process flags, and signals the
    ProcessEventWaiter handle.

If process flags has mask 1 set:

  - If new state is 6, it signals the ProcessEventWaiter handle.

If mask 1 is not set, it immediately does what is otherwise done by the
[\#FinalizeDeadProcess](#FinalizeDeadProcess "wikilink") command.

# pm:bm

| Cmd | Name                  |
| --- | --------------------- |
| 0   | GetMaintenanceMode    |
| 1   | EnableMaintenanceMode |

# pm:dmnt

| Cmd | Name                                                         |
| --- | ------------------------------------------------------------ |
| 0   | [\#GetZero](#GetZero "wikilink")                             |
| 1   | [\#GetProcessesWithFlag4](#GetProcessesWithFlag4 "wikilink") |
| 2   | [\#StartProcess](#StartProcess "wikilink")                   |
| 3   | GetProcessTitleIdByPid                                       |
| 4   | .. Returns a handle.                                         |
| 5   | GetCrashingProcessPid                                        |
| 6   | .. Returns a handle.                                         |

## GetZero

Always returns u32 0.

## GetProcessesWithFlag4

Returns an array of pids of all processes that have mask 4 set in
process flags.

## StartProcess

Takes a pid. Process state must be 0 or 1. Then it uses
svcStartProcess(process\_handle, u8, u8, u32) with args coming from
ldr:pm GetProgramInfo.

After that, it sets process state to 2.

# pm:info

| Cmd | Name                   |
| --- | ---------------------- |
| 0   | GetProcessTitleIdByPid |

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

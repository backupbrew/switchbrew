# Process Tracker thread

PM has a separate thread that is waiting for synchronization on process
handles.

## State changes

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

## Process launch

This thread can also be triggered by the pm:shell
[\#LaunchProcess](#LaunchProcess "wikilink") cmd.

It uses [ldr:pm](Loader%20services.md "wikilink") GetProgramInfo with
the supplied title-id.

If ((\*(u8\*) (info\_output+2)) & 3) is == 1, it goes through the
process list and errors if any has bit 0x40 set. Thus only one process
can have bit 0x40 set at a time.

It calls [ldr:pm](Loader%20services.md "wikilink") RegisterTitle, then
[ldr:pm](Loader%20services.md "wikilink") CreateProcess, then
[fsp-pr](Filesystem%20services.md "wikilink") RegisterTitle, then
[sm:m](Services%20API.md "wikilink") RegisterTitle.

The second input argument for [ldr:pm](Loader%20services.md "wikilink")
CreateProcess is (launch\_flags \>\> 2) & 3.

If launch\_flags has mask 1 set, it sets mask 1 in process flags.

If launch\_flags flags has mask 0x10 set, it sets mask 8 in process
flags.

If ((\*(u8\*) (info\_output+2)) & 3) is == 1, it sets 0x40 in the
process flags, and signals the event returned by
[\#EnableDebug](#EnableDebug "wikilink").

Finally it does svcStartProcess on the process handle that was returned
by [ldr:pm](Loader%20services.md "wikilink") CreateProcess.

Thus at the point of launch, the pid is already registered in ldr, fs,
sm, and pm.

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
| 4   | [\#EnableDebugForTitleId](#EnableDebugForTitleId "wikilink") |
| 5   | GetCrashingProcessPid                                        |
| 6   | [\#EnableDebug](#EnableDebug "wikilink")                     |

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

## EnableDebugForTitleId

Takes a title-id of the program to debug. Sets this to a global field.
Next time it gets launched it will be handled differently.

Returns an event handle that is signaled when the requested title is
launched.

## EnableDebug

Does \*not\* take a specific title-id as input.

Returns an event handle that is triggered for debug titles.

# pm:info

| Cmd | Name                   |
| --- | ---------------------- |
| 0   | GetProcessTitleIdByPid |

# pm:shell

| Cmd | Name                                                             |
| --- | ---------------------------------------------------------------- |
| 0   | [\#LaunchProcess](#LaunchProcess "wikilink")                     |
| 1   | TerminateProcessByPid                                            |
| 2   | TerminateProcessByTitleID                                        |
| 3   | GetProcessEventWaiter                                            |
| 4   | GetProcessEventType (0=CONTINUE, 1=CRASHING, 2,3,5)              |
| 5   | [\#FinalizeDeadProcess](#FinalizeDeadProcess "wikilink")         |
| 6   | [\#ClearProcessCrashedFlag](#ClearProcessCrashedFlag "wikilink") |
| 7   | [\#NotifyBootFinished](#NotifyBootFinished "wikilink")           |
| 8   | [\#GetCrashingProcessPid](#GetCrashingProcessPid "wikilink")     |

## LaunchProcess

Takes a title-id and launch\_flags. See [\#Process
launch](#Process_launch "wikilink").

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

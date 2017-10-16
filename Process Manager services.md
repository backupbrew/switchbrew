# Process Tracker thread

PM has a separate thread that is waiting for synchronization on process
handles.

## State changes

When the kernel signals a process handle, it uses svcResetSignal on the
process handle and then it uses svcGetProcessInfo to read out the
ProcessState.

If the process moved state non-3 -\> 3 it clears 4 in process flags.

If process flags has mask 8 set:

  - If new state is 2, it clears 0x20 and sets 0x10 in process flags,
    and signals the ProcessEventWaiter handle.
  - If new state is 4, it clears 0x20 and sets 0x10 in process flags,
    and signals the ProcessEventWaiter handle.
  - If new state is 7, it sets 0x30 in process flags, and signals the
    ProcessEventWaiter handle.

\[2.0.0+\] If new state is 2, and process flags has 0x80 set, it sets
mask 0x100 and signals the ProcessEventWaiter handle.

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

Resource limits for the process is selected by ApplicationType which is
((\*(u8\*) (info\_output+2)) & 3) being 0, 1, or 2. Value 3 is not used.
1 = application, 2 = applet.

It calls [ldr:pm](Loader%20services.md "wikilink") RegisterTitle, then
[ldr:pm](Loader%20services.md "wikilink") CreateProcess, then
[fsp-pr](Filesystem%20services.md "wikilink") RegisterTitle, then
[sm:m](Services%20API.md "wikilink") RegisterTitle.

\[1.0.0\] The second input argument for
[ldr:pm](Loader%20services.md "wikilink") CreateProcess is
(launch\_flags \>\> 2) & 3.

\[2.0.0+\] The second input argument for
[ldr:pm](Loader%20services.md "wikilink") CreateProcess is
((launch\_flags \>\> 2) & 2) | ((launch\_flags \>\> 1) \!= 1).

If launch\_flags has mask 1 set, it sets mask 1 in process flags.

If launch\_flags has mask 0x10 set, it sets mask 8 in process flags.

\[2.0.0+\] If launch\_flags has mask 0x20 set, it sets mask 0x80 in
process flags.

\[2.0.0+\] The launch\_flags mask 0x10 and 0x20 will be ignored unless
((\*(u8\*) (info\_output+2)) & 4) is set.

If ((\*(u8\*) (info\_output+2)) & 3) is == 1, it sets 0x40 in the
process flags, and signals the event returned by
[\#EnableDebug](#EnableDebug "wikilink"). svcStartProcess is not called
in this case, it has to be done manually by the
[\#StartProcess](#StartProcess "wikilink") command.

If the title-id matches the title-id given in
[\#EnableDebugForTitleId](#EnableDebugForTitleId "wikilink"), then
svcStartProcess is not called. Instead process remains in suspended
state, and has to be done manually by the
[\#StartProcess](#StartProcess "wikilink") command.

If launch\_flags has mask 2 set, svcStartProcess is skipped.

Finally it does svcStartProcess on the process handle that was returned
by [ldr:pm](Loader%20services.md "wikilink") CreateProcess, and sets
process state to 2.

The arguments for svcStartProcess are process\_handle,
\*(u8\*)info\_output, \*(u8\*)(info\_output+1),
\*(u32\*)(info\_output+4).

Thus at the point of launch, the pid is already registered in ldr, fs,
sm, and pm.

# pm:bm

| Cmd | Name               |
| --- | ------------------ |
| 0   | GetBootMode        |
| 1   | SetMaintenanceBoot |

# pm:dmnt

| Cmd | Name                                                                     |
| --- | ------------------------------------------------------------------------ |
| 0   | [\#GetDebugMode](#GetDebugMode "wikilink")                               |
| 1   | [\#GetDebugProcesses](#GetDebugProcesses "wikilink")                     |
| 2   | [\#StartDebugProcess](#StartDebugProcess "wikilink")                     |
| 3   | [\#GetDebugProcessTitleIdByPid](#GetDebugProcessTitleIdByPid "wikilink") |
| 4   | [\#EnableDebugForTitleId](#EnableDebugForTitleId "wikilink")             |
| 5   | [\#GetCrashingDebugProcessPid](#GetCrashingDebugProcessPid "wikilink")   |
| 6   | [\#EnableDebug](#EnableDebug "wikilink")                                 |

## GetDebugMode

Always returns u32 0 on retail.

\[2.0.0+\] Additional check on input that can return 0xC0F. The meaning
is probably useless because function is somewhat nopped on non-dev
builds anyway.

## GetDebugProcesses

Returns an array of pids of all processes that have mask 4 set in
process flags.

\[2.0.0+\] Additional check on input that can return 0xC0F. The meaning
is probably useless because function is somewhat nopped on non-dev
builds anyway.

## StartDebugProcess

Takes a pid. Process state must be 0 or 1. Then it uses
svcStartProcess(process\_handle, u8, u8, u32) with args coming from
ldr:pm GetProgramInfo.

After that, it sets process state to 2.

## GetDebugProcessTitleIdByPid

Same as
[GetProcessTitleIdByPid](Process%20Manager%20services#GetProcessTitleIdByPid.md##GetProcessTitleIdByPid "wikilink")
but for debug processes.

## EnableDebugForTitleId

Takes a title-id of the program to debug. Sets this to a global field.
Next time it gets launched it will be handled differently.

Returns an event handle that is signaled when the requested title is
launched.

## GetCrashingDebugProcessPid

Same as
[GetCrashingProcessPid](Process%20Manager%20services#GetCrashingProcessPid.md##GetCrashingProcessPid "wikilink")
but for debug processes.

## EnableDebug

Does \*not\* take a specific title-id as input.

Returns an event handle that is triggered for debug titles.

# pm:info

| Cmd | Name                                                           |
| --- | -------------------------------------------------------------- |
| 0   | [\#GetProcessTitleIdByPid](#GetProcessTitleIdByPid "wikilink") |

## GetProcessTitleIdByPid

Takes a pid and returns the title-id associated with the
process.

# pm:shell

| Cmd | Name                                                                       |
| --- | -------------------------------------------------------------------------- |
| 0   | [\#LaunchProcess](#LaunchProcess "wikilink")                               |
| 1   | TerminateProcessByPid                                                      |
| 2   | TerminateProcessByTitleId                                                  |
| 3   | GetProcessEventWaiter                                                      |
| 4   | [\#GetProcessEventType](#GetProcessEventType "wikilink")                   |
| 5   | [\#FinalizeDeadProcess](#FinalizeDeadProcess "wikilink")                   |
| 6   | [\#ClearProcessNotificationFlag](#ClearProcessNotificationFlag "wikilink") |
| 7   | [\#NotifyBootFinished](#NotifyBootFinished "wikilink")                     |
| 8   | [\#GetCrashingProcessPid](#GetCrashingProcessPid "wikilink")               |

## LaunchProcess

Takes launch\_flags, title-id, and storageID. See [\#Process
launch](#Process_launch "wikilink").

Returns the u64 title PID.

## GetProcessEventType

Returns 1 if flags has mask 2 set.

Returns 2 if flags has mask 1 set and state is 6.

Returns 3 if flags has mask 0x10 set and not bit5.

Returns 4 if flags has mask 0x30 set.

\[2.0.0+\] returns 5 if state \>= 2 and flags has mask 0x100 set.

Returns 0 if process is not found.

## FinalizeDeadProcess

Takes a pid as input. If the process with pid has the state "dead", it
unregisters the pid in fsp:pr, sm:m, and ldr:pm.

Then it removes the process from PMs internal linked-list of active
processes.

## ClearProcessNotificationFlag

Takes a pid as input. Clears 0x10 from process flags.

## NotifyBootFinished

Launches a process with hardcoded [boot2](Boot2.md "wikilink") title-id.

## GetCrashingProcessPid

Loops through the internal linked-list of processes, looks for mask 0x40
set in process flags. Returns pid of first such entry.

[Category:Services](Category:Services "wikilink")

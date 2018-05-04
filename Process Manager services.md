# LaunchFlags

| Bit | Mask | Name                                       |
| --- | ---- | ------------------------------------------ |
| 0   | 1    | LaunchFlags\_NotifyWhenExited              |
| 1   | 2    | LaunchFlags\_StartSuspended                |
| 2   | 4    |                                            |
| 3   | 8    |                                            |
| 4   | 0x10 | LaunchFlags\_NotifyDebugEvents             |
| 5   | 0x20 | \[2.0.0+\] LaunchFlags\_NotifyDebugSpecial |

# Process Tracker thread

PM has a separate thread that is waiting for synchronization on process
handles.

## State changes

When the kernel signals a process handle, it uses svcResetSignal on the
process handle and then it uses svcGetProcessInfo to read out the
ProcessEvent.

If the process moved from non-crashed -\> ProcessEvent\_Crashed it
clears 4 in process flags.

If process flags has mask 8 set:

  - If event is ProcessEvent\_Running or ProcessEvent\_DebugDetached, it
    clears 0x20 and sets 0x10 in process flags, and signals the
    ProcessEventWaiter handle.
  - If event is ProcessEvent\_DebugSuspended, it sets 0x20 and 0x10 in
    process flags, and signals the ProcessEventWaiter handle.

\[2.0.0+\] If new state is ProcessEvent\_DebugDetached, and process
flags has 0x80 set, it sets mask 0x100 and signals the
ProcessEventWaiter handle.

If process flags has mask 1 set:

  - If new state is ProcessEvent\_Exited, it signals the
    ProcessEventWaiter handle.

If mask 1 is not set, it immediately does what is otherwise done by the
[\#FinalizeDeadProcess](#FinalizeDeadProcess "wikilink") command.

## Process launch

This thread can also be triggered by the pm:shell
[\#LaunchProcess](#LaunchProcess "wikilink") cmd.

It uses [ldr:pm](Loader%20services.md "wikilink") GetProgramInfo with
the supplied title-id.

If ApplicationType == Application, it goes through the process list and
errors if any has mask 0x40 set. Thus you can only run one Application
at a time.

Resource limits for the process is selected by ApplicationType.

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

If ApplicationType == Application, it sets 0x40 in the process flags,
and signals the event returned by
[\#EnableDebugForApplication](#EnableDebugForApplication "wikilink").
svcStartProcess is not called in this case, it has to be done manually
by the [\#StartProcess](#StartProcess "wikilink") command.

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

This is "nn::pm::detail::IBootModeInterface".

| Cmd | Name               |
| --- | ------------------ |
| 0   | GetBootMode        |
| 1   | SetMaintenanceBoot |

# pm:dmnt

This is
"nn::pm::detail::IDebugMonitorInterface".

| Cmd | Name                                                                 |
| --- | -------------------------------------------------------------------- |
| 0   | [\#IsDebugMode](#IsDebugMode "wikilink")                             |
| 1   | [\#GetDebugProcesses](#GetDebugProcesses "wikilink")                 |
| 2   | [\#StartDebugProcess](#StartDebugProcess "wikilink")                 |
| 3   | [\#GetTitlePid](#GetTitlePid "wikilink")                             |
| 4   | [\#EnableDebugForTitleId](#EnableDebugForTitleId "wikilink")         |
| 5   | [\#GetApplicationPid](#GetApplicationPid "wikilink")                 |
| 6   | [\#EnableDebugForApplication](#EnableDebugForApplication "wikilink") |

## IsDebugMode

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

Takes a pid. Last process event must be ProcessEvent\_Created or
ProcessEvent\_DebugAttached.

Then it uses svcStartProcess(process\_handle, u8, u8, u32) with args
coming from ldr:pm GetProgramInfo.

After that, it sets last process state to ProcessEvent\_DebugDetached.

## GetTitlePid

Takes a title-id and returns the pid.

## EnableDebugForTitleId

Takes a title-id of the program to debug. Sets this to a global field.

Next time it gets launched it will be handled differently.

Returns an event handle that is signaled when the requested title is
about to be launched.

## GetApplicationPid

Returns the pid of the application process.

## EnableDebugForApplication

Does \*not\* take a specific title-id as input.

Returns an event handle that is triggered for application titles.

# pm:info

This is "nn::pm::detail::IInformationInterface".

| Cmd | Name                                   |
| --- | -------------------------------------- |
| 0   | [\#GetTitleId](#GetTitleId "wikilink") |

## GetTitleId

Takes a pid and returns the title-id associated with the process.

# pm:shell

This is
"nn::pm::detail::IShellInterface".

| Cmd                   | Name                                                                                      |
| --------------------- | ----------------------------------------------------------------------------------------- |
| 0                     | [\#LaunchProcess](#LaunchProcess "wikilink")                                              |
| 1                     | TerminateProcessByPid                                                                     |
| 2                     | TerminateProcessByTitleId                                                                 |
| 3                     | GetProcessEventWaiter                                                                     |
| 4                     | [\#GetProcessEventType](#GetProcessEventType "wikilink")                                  |
| (\[1.0.0-4.1.0\] 5)   | [\#FinalizeDeadProcess](#FinalizeDeadProcess "wikilink")                                  |
| (\[1.0.0-4.1.0\] 6)   | [\#ClearProcessNotificationFlag](#ClearProcessNotificationFlag "wikilink")                |
| 5 (\[1.0.0-4.1.0\] 7) | [\#NotifyBootFinished](#NotifyBootFinished "wikilink")                                    |
| 6 (\[1.0.0-4.1.0\] 8) | [\#GetApplicationPid](#GetApplicationPid "wikilink")                                      |
| 7 (\[1.0.0-4.1.0\] 9) | \[4.0.0+\] [\#BoostSystemMemoryResourceLimit](#BoostSystemMemoryResourceLimit "wikilink") |

## LaunchProcess

Takes launch\_flags, title-id, and storageID. See [\#Process
launch](#Process_launch "wikilink").

Returns the u64 title PID.

## GetProcessEventType

Returns 1 if flags has mask 2 set.

Returns 2 if flags has mask 1 set and state is 6.

Returns 3 if flags has mask 0x10 set and not 0x20.

Returns 4 if flags has mask 0x30 set.

\[2.0.0+\] returns 5 if state \>= 2 and flags has mask 0x100 set.

Returns 0 if process is not found.

## FinalizeDeadProcess

Takes a pid as input. If the process with pid has the state "dead", it
unregisters the pid in fsp:pr, sm:m, and ldr:pm.

Then it removes the process from PMs internal linked-list of active
processes.

\[5.0.0+\] This command was removed.

## ClearProcessNotificationFlag

Takes a pid as input. Clears 0x10 from process flags.

\[5.0.0+\] This command was removed.

## NotifyBootFinished

This launches the [boot2](Boot2.md "wikilink") title.

\[4.0.0+\] When booting from SafeMode Firmware, instead of
[boot2](Boot2.md "wikilink"), this launches the following titles in
order:

  - 0100000000000009 (settings)
  - 0100000000000006 (usb)
  - 010000000000001D (pcie)
  - 0100000000000007 (tma)
  - 010000000000001F (ns)
  - 0100000000000015 (lm)
  - 0100000000000010 (ptm)
  - 0100000000000016 (wlan)
  - 0100000000000012 (bsdsockets)
  - 010000000000000F (nifm)
  - 0100000000000024 (ssl)
  - 0100000000000025 (nim)
  - 0100000000000031 (glue)
  - 010000000000003D (safemode)

## GetApplicationPid

Loops through the internal linked-list of processes, looks for mask 0x40
set in process flags. Returns pid of first such entry.

## BoostSystemMemoryResourceLimit

Takes an u64 **mem\_size** as input. If the desired memory size doesn't
exceed an internal limit (imposed by PM by looking at the
[MemoryArrange](SPL%20services#MemoryArrange.md##MemoryArrange "wikilink")
ConfigItem), PM calls svcSetResourceLimitLimitValue to set the new
[LimitableResource\_Memory](SVC#LimitableResource.md##LimitableResource "wikilink")
value.

This is used directly by [ns:am2
BoostSystemMemoryResourceLimit](NS%20Services#IApplicationManagerInterface.md##IApplicationManagerInterface "wikilink").

[Category:Services](Category:Services "wikilink")

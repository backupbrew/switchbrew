dmnt (Debug Monitor) is a sysmodule used to debug Horizon OS processes.
This system module is not present in retail units.

# dmnt:-

This is "nn::dmnt::IInterface".

| Cmd | Name                           |
| --- | ------------------------------ |
| 0   | BreakDebugProcess              |
| 1   | TerminateDebugProcess          |
| 2   | CloseHandle                    |
| 3   | LoadImage                      |
| 4   | GetProcessId                   |
| 5   | GetProcessHandle               |
| 6   | WaitSynchronization            |
| 7   | GetDebugEvent                  |
| 8   | GetProcessModuleInfo           |
| 9   | GetProcessList                 |
| 10  | GetThreadList                  |
| 11  | GetDebugThreadContext          |
| 12  | ContinueDebugEvent             |
| 13  | ReadDebugProcessMemory         |
| 14  | WriteDebugProcessMemory        |
| 15  | SetDebugThreadContext          |
| 16  | GetDebugThreadParam            |
| 17  | InitializeThreadInfo           |
| 18  | SetHardwareBreakPoint          |
| 19  | QueryDebugProcessMemory        |
| 20  | GetProcessMemoryDetails        |
| 21  | AttachByProgramId              |
| 22  | AttachOnLaunch                 |
| 23  | GetDebugMonitorProcessId       |
| 25  | GetJitDebugProcessList         |
| 26  | CreateCoreDump                 |
| 27  | GetAllDebugThreadInfo          |
| 29  | TargetIO\_FileOpen             |
| 30  | TargetIO\_FileClose            |
| 31  | TargetIO\_FileRead             |
| 32  | TargetIO\_FileWrite            |
| 33  | TargetIO\_FileSetAttributes    |
| 34  | TargetIO\_FileGetInformation   |
| 35  | TargetIO\_FileSetTime          |
| 36  | TargetIO\_FileSetSize          |
| 37  | TargetIO\_FileDelete           |
| 38  | TargetIO\_FileMove             |
| 39  | TargetIO\_DirectoryCreate      |
| 40  | TargetIO\_DirectoryDelete      |
| 41  | TargetIO\_DirectoryRename      |
| 42  | TargetIO\_DirectoryGetCount    |
| 43  | TargetIO\_DirectoryOpen        |
| 44  | TargetIO\_DirectoryGetNext     |
| 45  | TargetIO\_DirectoryClose       |
| 46  | TargetIO\_GetFreeSpace         |
| 47  | TargetIO\_GetVolumeInformation |
| 48  | InitiateCoreDump               |
| 49  | ContinueCoreDump               |
| 50  | AddTTYToCoreDump               |
| 51  | AddImageToCoreDump             |
| 52  | CloseCoreDump                  |
|     |                                |

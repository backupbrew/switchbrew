AM (Applet Manager) provides services for interacting with system
applets while abstracting several aspects of power and operation
management.

Contains multiple raw images, with at least the following:
"NN\_OMM\_CHARGING\_BIN\_{begin|end}"(charging icon), low-battery icon,
and the Nintendo Switch logo displayed during system boot.

# appletAE

This is
"nn::am::<service::IAllSystemAppletProxiesService>".

| Cmd | Name                                                                      | Notes                                                                    |
| --- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| 100 | OpenSystemAppletProxy                                                     | Returns an [\#ISystemAppletProxy](#ISystemAppletProxy "wikilink").       |
| 200 | OpenLibraryAppletProxy ( \[3.0.0+\] OpenLibraryAppletProxyOld)            | Returns an [\#ILibraryAppletProxy](#ILibraryAppletProxy "wikilink").     |
| 201 | \[3.0.0+\] [\#OpenLibraryAppletProxy](#OpenLibraryAppletProxy "wikilink") | Returns an [\#ILibraryAppletProxy](#ILibraryAppletProxy "wikilink").     |
| 300 | OpenOverlayAppletProxy                                                    | Returns an [\#IOverlayAppletProxy](#IOverlayAppletProxy "wikilink").     |
| 350 | OpenSystemApplicationProxy                                                | Returns an [\#IApplicationProxy](#IApplicationProxy "wikilink").         |
| 400 | CreateSelfLibraryAppletCreatorForDevelop                                  | Returns an [\#ILibraryAppletCreator](#ILibraryAppletCreator "wikilink"). |
|     |                                                                           |                                                                          |

All of these commands except
[\#OpenLibraryAppletProxy](#OpenLibraryAppletProxy "wikilink") take the
same input as
[\#OpenApplicationProxy](#OpenApplicationProxy "wikilink"), with the
same user-process retry-loop as
[\#OpenApplicationProxy](#OpenApplicationProxy "wikilink").

This service seems to be used by all system non-regular-applications.

The 01000000000010XX system [titles](Title%20list.md "wikilink") use the
following applet types(above Open{type}Proxy commands):

  - "qlaunch": SystemApplet
  - "overlay": OverlayApplet
  - "starter": SystemApplication
  - "maintenance": SystemApplet
  - All others: LibraryApplet

## OpenLibraryAppletProxy

Returns an [\#IApplicationProxy](#IApplicationProxy "wikilink").

Takes a [reserved](IPC%20Marshalling.md "wikilink") input u64(official
user-processes use hard-coded value 0), a PID,a process
copy-handle(cur-proc handle alias), and an 0x80-byte type-0x15 input
buffer **AppletAttribute**.

Official user-processes use the same retry loop with this as the other
Open\*Proxy
commands.

## ISystemAppletProxy

| Cmd  | Name                        | Notes                                                                            |
| ---- | --------------------------- | -------------------------------------------------------------------------------- |
| 0    | GetCommonStateGetter        | Returns an [\#ICommonStateGetter](#ICommonStateGetter "wikilink").               |
| 1    | GetSelfController           | Returns an [\#ISelfController](#ISelfController "wikilink").                     |
| 2    | GetWindowController         | Returns an [\#IWindowController](#IWindowController "wikilink").                 |
| 3    | GetAudioController          | Returns an [\#IAudioController](#IAudioController "wikilink").                   |
| 4    | GetDisplayController        | Returns an [\#IDisplayController](#IDisplayController "wikilink").               |
| 10   | GetProcessWindingController | Returns an [\#IProcessWindingController](#IProcessWindingController "wikilink"). |
| 11   | GetLibraryAppletCreator     | Returns an [\#ILibraryAppletCreator](#ILibraryAppletCreator "wikilink").         |
| 20   | GetHomeMenuFunctions        | Returns an [\#IHomeMenuFunctions](#IHomeMenuFunctions "wikilink").               |
| 21   | GetGlobalStateController    | Returns an [\#IGlobalStateController](#IGlobalStateController "wikilink").       |
| 22   | GetApplicationCreator       | Returns an [\#IApplicationCreator](#IApplicationCreator "wikilink").             |
| 1000 | GetDebugFunctions           | Returns an [\#IDebugFunctions](#IDebugFunctions "wikilink").                     |
|      |                             |                                                                                  |

### IHomeMenuFunctions

| Cmd | Name                               | Notes                                                                          |
| --- | ---------------------------------- | ------------------------------------------------------------------------------ |
| 10  | RequestToGetForeground             |                                                                                |
| 11  | LockForeground                     |                                                                                |
| 12  | UnlockForeground                   |                                                                                |
| 20  | PopFromGeneralChannel              | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |
| 21  | GetPopFromGeneralChannelEvent      |                                                                                |
| 30  | GetHomeButtonWriterLockAccessor    | Returns an [\#ILockAccessor](#ILockAccessor "wikilink").                       |
| 31  | \[2.0.0+\] GetWriterLockAccessorEx | Returns an [\#ILockAccessor](#ILockAccessor "wikilink").                       |
|     |                                    |                                                                                |

#### ILockAccessor

| Cmd | Name     |
| --- | -------- |
| 1   | TryLock  |
| 2   | Unlock   |
| 3   | GetEvent |

### IGlobalStateController

| Cmd | Name                                         |
| --- | -------------------------------------------- |
| 0   | RequestToEnterSleep                          |
| 1   | EnterSleep                                   |
| 2   | StartSleepSequence                           |
| 3   | StartShutdownSequence                        |
| 4   | StartRebootSequence                          |
| 10  | LoadAndApplyIdlePolicySettings               |
| 11  | \[2.0.0+\] NotifyCecSettingsChanged          |
| 12  | \[2.0.0+\] SetDefaultHomeButtonLongPressTime |
| 13  | \[2.0.0+\] UpdateDefaultDisplayResolution    |
| 14  | \[2.0.0+\] ShouldSleepOnBoot                 |
|     |                                              |

### IApplicationCreator

| Cmd | Name                                 | Notes                                                                  |
| --- | ------------------------------------ | ---------------------------------------------------------------------- |
| 0   | CreateApplication                    | Returns an [\#IApplicationAccessor](#IApplicationAccessor "wikilink"). |
| 1   | PopLaunchRequestedApplication        | Returns an [\#IApplicationAccessor](#IApplicationAccessor "wikilink"). |
| 10  | CreateSystemApplication              | Returns an [\#IApplicationAccessor](#IApplicationAccessor "wikilink"). |
| 100 | PopFloatingApplicationForDevelopment | Returns an [\#IApplicationAccessor](#IApplicationAccessor "wikilink"). |

#### IApplicationAccessor

| Cmd | Name                                    | Notes                                                                          |
| --- | --------------------------------------- | ------------------------------------------------------------------------------ |
| 0   | GetAppletStateChangedEvent              |                                                                                |
| 1   | IsCompleted                             |                                                                                |
| 10  | Start                                   |                                                                                |
| 20  | RequestExit                             |                                                                                |
| 25  | Terminate                               |                                                                                |
| 30  | GetResult                               |                                                                                |
| 101 | RequestForApplicationToGetForeground    |                                                                                |
| 110 | TerminateAllLibraryApplets              |                                                                                |
| 111 | AreAnyLibraryAppletsLeft                |                                                                                |
| 112 | GetCurrentLibraryApplet                 | Returns an [\#IAppletAccessor](#IAppletAccessor "wikilink").                   |
| 120 | GetApplicationId                        |                                                                                |
| 121 | PushLaunchParameter                     | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |
| 122 | GetApplicationControlProperty           |                                                                                |
| 123 | \[2.0.0+\] GetApplicationLaunchProperty |                                                                                |

##### IAppletAccessor

| Cmd | Name                       |
| --- | -------------------------- |
| 0   | GetAppletStateChangedEvent |
| 1   | IsCompleted                |
| 10  | Start                      |
| 20  | RequestExit                |
| 25  | Terminate                  |
| 30  | GetResult                  |

## ILibraryAppletProxy

| Cmd  | Name                         | Notes                                                                              |
| ---- | ---------------------------- | ---------------------------------------------------------------------------------- |
| 0    | GetCommonStateGetter         | Returns an [\#ICommonStateGetter](#ICommonStateGetter "wikilink").                 |
| 1    | GetSelfController            | Returns an [\#ISelfController](#ISelfController "wikilink").                       |
| 2    | GetWindowController          | Returns an [\#IWindowController](#IWindowController "wikilink").                   |
| 3    | GetAudioController           | Returns an [\#IAudioController](#IAudioController "wikilink").                     |
| 4    | GetDisplayController         | Returns an [\#IDisplayController](#IDisplayController "wikilink").                 |
| 10   | GetProcessWindingController  | Returns an [\#IProcessWindingController](#IProcessWindingController "wikilink").   |
| 11   | GetLibraryAppletCreator      | Returns an [\#ILibraryAppletCreator](#ILibraryAppletCreator "wikilink").           |
| 20   | GetLibraryAppletSelfAccessor | Returns an [\#ILibraryAppletSelfAccessor](#ILibraryAppletSelfAccessor "wikilink"). |
| 1000 | GetDebugFunctions            | Returns an [\#IDebugFunctions](#IDebugFunctions "wikilink").                       |
|      |                              |                                                                                    |

### ILibraryAppletSelfAccessor

| Cmd | Name                                                       | Notes                                                                          |
| --- | ---------------------------------------------------------- | ------------------------------------------------------------------------------ |
| 0   | PopInData                                                  | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |
| 1   | PushOutData                                                | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |
| 2   | PopInteractiveInData                                       | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |
| 3   | PushInteractiveOutData                                     | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |
| 5   | GetPopInDataEvent                                          |                                                                                |
| 6   | GetPopInteractiveInDataEvent                               |                                                                                |
| 10  | ExitProcessAndReturn                                       |                                                                                |
| 11  | [\#GetLibraryAppletInfo](#GetLibraryAppletInfo "wikilink") |                                                                                |
| 12  | GetMainAppletIdentityInfo                                  |                                                                                |
| 13  | CanUseApplicationCore                                      |                                                                                |
| 14  | GetCallerAppletIdentityInfo                                |                                                                                |
| 15  | \[2.0.0+\] GetMainAppletApplicationControlProperty         |                                                                                |
| 16  | \[2.0.0+\] GetMainAppletStorageId                          |                                                                                |
| 17  | \[2.0.0+\] GetCallerAppletIdentityInfoStack                |                                                                                |
| 20  | PopExtraStorage                                            | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |
| 25  | GetPopExtraStorageEvent                                    |                                                                                |
| 30  | UnpopInData                                                | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |
| 31  | UnpopExtraStorage                                          | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |
| 40  | \[2.0.0+\] GetIndirectLayerProducerHandle                  |                                                                                |
| 50  | \[2.0.0+\] ReportVisibleError                              |                                                                                |

#### GetLibraryAppletInfo

No input. Returns an u64
LibraryAppletInfo.

## IOverlayAppletProxy

| Cmd  | Name                        | Notes                                                                            |
| ---- | --------------------------- | -------------------------------------------------------------------------------- |
| 0    | GetCommonStateGetter        | Returns an [\#ICommonStateGetter](#ICommonStateGetter "wikilink").               |
| 1    | GetSelfController           | Returns an [\#ISelfController](#ISelfController "wikilink").                     |
| 2    | GetWindowController         | Returns an [\#IWindowController](#IWindowController "wikilink").                 |
| 3    | GetAudioController          | Returns an [\#IAudioController](#IAudioController "wikilink").                   |
| 4    | GetDisplayController        | Returns an [\#IDisplayController](#IDisplayController "wikilink").               |
| 10   | GetProcessWindingController | Returns an [\#IProcessWindingController](#IProcessWindingController "wikilink"). |
| 11   | GetLibraryAppletCreator     | Returns an [\#ILibraryAppletCreator](#ILibraryAppletCreator "wikilink").         |
| 20   | GetOverlayFunctions         | Returns an [\#IOverlayFunctions](#IOverlayFunctions "wikilink").                 |
| 1000 | GetDebugFunctions           | Returns an [\#IDebugFunctions](#IDebugFunctions "wikilink").                     |
|      |                             |                                                                                  |

### IOverlayFunctions

| Cmd | Name                                             |
| --- | ------------------------------------------------ |
| 0   | BeginToWatchShortHomeButtonMessage               |
| 1   | EndToWatchShortHomeButtonMessage                 |
| 2   | GetApplicationIdForLogo                          |
| 3   | SetGpuTimeSliceBoost                             |
| 4   | \[2.0.0+\] SetAutoSleepTimeAndDimmingTimeEnabled |
| 5   | \[2.0.0+\] TerminateApplicationAndSetReason      |
| 6   | \[2.0.0+\] SetScreenShotPermissionGlobally       |

## IApplicationProxy

| Cmd  | Name                        | Notes                                                                            |
| ---- | --------------------------- | -------------------------------------------------------------------------------- |
| 0    | GetCommonStateGetter        | Returns an [\#ICommonStateGetter](#ICommonStateGetter "wikilink").               |
| 1    | GetSelfController           | Returns an [\#ISelfController](#ISelfController "wikilink").                     |
| 2    | GetWindowController         | Returns an [\#IWindowController](#IWindowController "wikilink").                 |
| 3    | GetAudioController          | Returns an [\#IAudioController](#IAudioController "wikilink").                   |
| 4    | GetDisplayController        | Returns an [\#IDisplayController](#IDisplayController "wikilink").               |
| 10   | GetProcessWindingController | Returns an [\#IProcessWindingController](#IProcessWindingController "wikilink"). |
| 11   | GetLibraryAppletCreator     | Returns an [\#ILibraryAppletCreator](#ILibraryAppletCreator "wikilink").         |
| 20   | GetApplicationFunctions     | Returns an [\#IApplicationFunctions](#IApplicationFunctions "wikilink").         |
| 1000 | GetDebugFunctions           | Returns an [\#IDebugFunctions](#IDebugFunctions "wikilink").                     |
|      |                             |                                                                                  |

### IApplicationFunctions

| Cmd | Name                                                                                | Notes                                                                          |
| --- | ----------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| 1   | PopLaunchParameter                                                                  | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |
| 10  | CreateApplicationAndPushAndRequestToStart                                           | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |
| 11  | \[2.0.0+\] CreateApplicationAndPushAndRequestToStartForQuest                        | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |
| 20  | EnsureSaveData                                                                      |                                                                                |
| 21  | GetDesiredLanguage                                                                  |                                                                                |
| 22  | [\#SetTerminateResult](#SetTerminateResult "wikilink")                              |                                                                                |
| 23  | GetDisplayVersion                                                                   |                                                                                |
| 24  | \[2.0.0+\] GetLaunchStorageInfoForDebug                                             |                                                                                |
| 25  | \[2.0.0+\] ExtendSaveData                                                           |                                                                                |
| 26  | \[2.0.0+\] GetSaveDataSize                                                          |                                                                                |
| 30  | BeginBlockingHomeButtonShortAndLongPressed                                          |                                                                                |
| 31  | EndBlockingHomeButtonShortAndLongPressed                                            |                                                                                |
| 32  | BeginBlockingHomeButton                                                             |                                                                                |
| 33  | EndBlockingHomeButton                                                               |                                                                                |
| 40  | [\#NotifyRunning](#NotifyRunning "wikilink")                                        |                                                                                |
| 50  | \[2.0.0+\] GetPseudoDeviceId                                                        |                                                                                |
| 60  | \[2.0.0+\] SetMediaPlaybackStateForApplication                                      |                                                                                |
| 65  | \[3.0.0+\] IsGamePlayRecordingSupported                                             |                                                                                |
| 66  | \[3.0.0+\] [\#InitializeGamePlayRecording](#InitializeGamePlayRecording "wikilink") |                                                                                |
| 67  | \[3.0.0+\] [\#SetGamePlayRecordingState](#SetGamePlayRecordingState "wikilink")     |                                                                                |
| 70  | \[3.0.0+\] RequestToShutdown                                                        |                                                                                |
| 71  | \[3.0.0+\] RequestToReboot                                                          |                                                                                |

The BOTW game uses this GamePlayRecording functionality from the
main-nso "nninitStartup" function, with size 0x6000000(96MiB). The
official GamePlayRecording-enable code does the following(this will
panic on any failure):

  - [Creates](SVC.md "wikilink") TransferMemory using the input buffer
    and size, with permissions=0.
  - Uses
    [\#InitializeGamePlayRecording](#InitializeGamePlayRecording "wikilink")
    with the TransferMemory.
  - Closes the TransferMemory handle, + TransferMemory cleanup.
  - Uses
    [\#SetGamePlayRecordingState](#SetGamePlayRecordingState "wikilink")
    with value 0x1.

This GamePlayRecording functionality presumably enables the
video-recording usable starting with [4.0.0](4.0.0.md "wikilink").

#### SetTerminateResult

Takes an input u32 **Result**, no output.

For example, in some cases official apps use this with
[error](Error%20codes.md "wikilink") 0x2A2 then uses svcBreak.

#### NotifyRunning

Takes no input. Returns an output u8, which is ignored by official
user-processes.

#### InitializeGamePlayRecording

Takes a TransferMemory handle and an u64 for the size of the
TransferMemory.

#### SetGamePlayRecordingState

Takes an input
u32.

## ILibraryAppletCreator

| Cmd | Name                           | Notes                                                                          |
| --- | ------------------------------ | ------------------------------------------------------------------------------ |
| 0   | CreateLibraryApplet            | Returns an [\#ILibraryAppletAccessor](#ILibraryAppletAccessor "wikilink").     |
| 1   | TerminateAllLibraryApplets     |                                                                                |
| 2   | AreAnyLibraryAppletsLeft       |                                                                                |
| 10  | CreateStorage                  | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |
| 11  | CreateTransferMemoryStorage    | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |
| 12  | \[2.0.0+\] CreateHandleStorage | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |
|     |                                |                                                                                |

### ILibraryAppletAccessor

| Cmd | Name                                      | Notes                                                                          |
| --- | ----------------------------------------- | ------------------------------------------------------------------------------ |
| 0   | GetAppletStateChangedEvent                |                                                                                |
| 1   | IsCompleted                               |                                                                                |
| 10  | Start                                     |                                                                                |
| 20  | RequestExit                               |                                                                                |
| 25  | Terminate                                 |                                                                                |
| 30  | GetResult                                 |                                                                                |
| 50  | SetOutOfFocusApplicationSuspendingEnabled |                                                                                |
| 100 | PushInData                                | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |
| 101 | PopOutData                                | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |
| 102 | PushExtraStorage                          | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |
| 103 | PushInteractiveInData                     | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |
| 104 | PopInteractiveOutData                     | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |
| 105 | GetPopOutDataEvent                        |                                                                                |
| 106 | GetPopInteractiveOutDataEvent             |                                                                                |
| 110 | NeedsToExitProcess                        |                                                                                |
| 120 | GetLibraryAppletInfo                      |                                                                                |
| 150 | RequestForAppletToGetForeground           |                                                                                |
| 160 | \[2.0.0+\] GetIndirectLayerConsumerHandle |                                                                                |

## ICommonStateGetter

| Cmd | Name                                                          | Notes                                                                          |
| --- | ------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| 0   | [\#GetEventHandle](#GetEventHandle "wikilink")                |                                                                                |
| 1   | [\#ReceiveMessage](#ReceiveMessage "wikilink")                |                                                                                |
| 2   | GetThisAppletKind                                             |                                                                                |
| 3   | AllowToEnterSleep                                             |                                                                                |
| 4   | DisallowToEnterSleep                                          |                                                                                |
| 5   | GetOperationMode                                              |                                                                                |
| 6   | GetPerformanceMode                                            |                                                                                |
| 7   | GetCradleStatus                                               |                                                                                |
| 8   | GetBootMode                                                   |                                                                                |
| 9   | [\#GetCurrentFocusState](#GetCurrentFocusState "wikilink")    |                                                                                |
| 10  | RequestToAcquireSleepLock                                     |                                                                                |
| 11  | ReleaseSleepLock                                              |                                                                                |
| 12  | ReleaseSleepLockTransiently                                   |                                                                                |
| 13  | GetAcquiredSleepLockEvent                                     |                                                                                |
| 20  | PushToGeneralChannel                                          | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |
| 30  | GetHomeButtonReaderLockAccessor                               | Returns an [\#ILockAccessor](#ILockAccessor "wikilink").                       |
| 31  | \[2.0.0+\] GetReaderLockAccessorEx                            | Returns an [\#ILockAccessor](#ILockAccessor "wikilink").                       |
| 40  | \[2.0.0+\] GetCradleFwVersion                                 |                                                                                |
| 50  | \[3.0.0+\] IsVrModeEnabled                                    |                                                                                |
| 51  | \[3.0.0+\] [\#SetVrModeEnabled](#SetVrModeEnabled "wikilink") |                                                                                |
| 55  | \[3.0.0+\] IsInControllerFirmwareUpdateSection                |                                                                                |
| 60  | \[3.0.0+\] GetDefaultDisplayResolution                        |                                                                                |
| 61  | \[3.0.0+\] GetDefaultDisplayResolutionChangeEvent             |                                                                                |

Officially notification messages are handled by the application itself,
not sdk-nso in ExeFS. Official apps call code in sdk-nso which basically
uses svcWaitSynchronization with the event from
[\#GetEventHandle](#GetEventHandle "wikilink") to check whether a
message is available, then if so it uses
[\#ReceiveMessage](#ReceiveMessage "wikilink"). The actual handling for
message IDs is done in the app itself(see
[\#NotificationMessage](#NotificationMessage "wikilink")).

### GetEventHandle

No input. Returns an output event handle. This is signalled when a
message is available with
[\#ReceiveMessage](#ReceiveMessage "wikilink").

### ReceiveMessage

No input. Returns an output u32. Error 0x680 indicates no message is
available.

### GetCurrentFocusState

No input. Returns an output u8.

### SetVrModeEnabled

Takes an input u8 bool flag. No output.

Updates internal AM state fields. If the new state doesn't match the
previous state, this uses the
[Backlight\_services](Backlight%20services.md "wikilink")
{Disable/Enable}VrMode command depending on whether
flag={disable/enable}.

## ISelfController

| Cmd | Name                                                                                      |
| --- | ----------------------------------------------------------------------------------------- |
| 0   | Exit                                                                                      |
| 1   | LockExit                                                                                  |
| 2   | UnlockExit                                                                                |
| 3   | \[2.0.0+\] EnterFatalSection                                                              |
| 4   | \[2.0.0+\] LeaveFatalSection                                                              |
| 9   | GetLibraryAppletLaunchableEvent                                                           |
| 10  | SetScreenShotPermission                                                                   |
| 11  | SetOperationModeChangedNotification                                                       |
| 12  | SetPerformanceModeChangedNotification                                                     |
| 13  | [\#SetFocusHandlingMode](#SetFocusHandlingMode "wikilink")                                |
| 14  | SetRestartMessageEnabled                                                                  |
| 15  | \[2.0.0+\] SetScreenShotAppletIdentityInfo                                                |
| 16  | \[2.0.0+\] [\#SetOutOfFocusSuspendingEnabled](#SetOutOfFocusSuspendingEnabled "wikilink") |
| 17  | \[2.0.0+\] SetControllerFirmwareUpdateSection                                             |
| 18  | \[2.0.0+\] SetRequiresCaptureButtonShortPressedMessage                                    |
| 19  | \[2.0.0+\] SetScreenShotImageOrientation                                                  |
| 40  | [\#CreateManagedDisplayLayer](#CreateManagedDisplayLayer "wikilink")                      |
| 50  | SetHandlesRequestToDisplay                                                                |
| 51  | ApproveToDisplay                                                                          |
| 60  | OverrideAutoSleepTimeAndDimmingTime                                                       |
| 61  | SetMediaPlaybackState                                                                     |
| 62  | SetIdleTimeDetectionExtension                                                             |
| 63  | GetIdleTimeDetectionExtension                                                             |
| 64  | SetInputDetectionSourceSet                                                                |
| 65  | \[2.0.0+\] ReportUserIsActive                                                             |
| 66  | \[2.0.0+\] GetCurrentIlluminance                                                          |
| 67  | \[2.0.0+\] IsIlluminanceAvailable                                                         |

### SetFocusHandlingMode

Takes 3 input u8s with each field located immediately after the previous
u8, these are bool flags. No output.

### SetOutOfFocusSuspendingEnabled

Takes an input u8(bool flag). No output.

### CreateManagedDisplayLayer

Returns an output u64 LayerId which is then used by the user-process
with
[Display\_services\#OpenLayer](Display%20services#OpenLayer.md##OpenLayer "wikilink").

## IWindowController

| Cmd | Name                                                             | Notes                      |
| --- | ---------------------------------------------------------------- | -------------------------- |
| 0   | CreateWindow                                                     | Returns an IWindow object. |
| 1   | [\#GetAppletResourceUserId](#GetAppletResourceUserId "wikilink") |                            |
| 10  | [\#AcquireForegroundRights](#AcquireForegroundRights "wikilink") |                            |
| 11  | ReleaseForegroundRights                                          |                            |
| 12  | RejectToChangeIntoBackground                                     |                            |

### GetAppletResourceUserId

Returns an output u64:
[\#AppletResourceUserId](#AppletResourceUserId "wikilink").

### AcquireForegroundRights

No input/output.

## IAudioController

| Cmd | Name                                 |
| --- | ------------------------------------ |
| 0   | SetExpectedMasterVolume              |
| 1   | GetMainAppletExpectedMasterVolume    |
| 2   | GetLibraryAppletExpectedMasterVolume |
| 3   | ChangeMainAppletMasterVolume         |
| 4   | SetTransparentVolumeRate             |

## IDisplayController

| Cmd | Name                                   |
| --- | -------------------------------------- |
| 0   | GetLastForegroundCaptureImage          |
| 1   | UpdateLastForegroundCaptureImage       |
| 2   | GetLastApplicationCaptureImage         |
| 3   | GetCallerAppletCaptureImage            |
| 4   | UpdateCallerAppletCaptureImage         |
| 5   | GetLastForegroundCaptureImageEx        |
| 6   | GetLastApplicationCaptureImageEx       |
| 7   | GetCallerAppletCaptureImageEx          |
| 8   | \[2.0.0+\] TakeScreenShotOfOwnLayer    |
| 10  | AcquireLastApplicationCaptureBuffer    |
| 11  | ReleaseLastApplicationCaptureBuffer    |
| 12  | AcquireLastForegroundCaptureBuffer     |
| 13  | ReleaseLastForegroundCaptureBuffer     |
| 14  | AcquireCallerAppletCaptureBuffer       |
| 15  | ReleaseCallerAppletCaptureBuffer       |
| 16  | AcquireLastApplicationCaptureBufferEx  |
| 17  | AcquireLastForegroundCaptureBufferEx   |
| 18  | AcquireCallerAppletCaptureBufferEx     |
| 20  | \[2.0.0+\] ClearCaptureBuffer          |
| 21  | \[2.0.0+\] ClearAppletTransitionBuffer |

## ILibraryAppletCreator

| Cmd | Name                           | Notes                                                                          |
| --- | ------------------------------ | ------------------------------------------------------------------------------ |
| 0   | CreateLibraryApplet            | Returns a [\#ILibraryAppletAccessor](#ILibraryAppletAccessor "wikilink").      |
| 1   | TerminateAllLibraryApplets     |                                                                                |
| 2   | AreAnyLibraryAppletsLeft       |                                                                                |
| 10  | CreateStorage                  | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |
| 11  | CreateTransferMemoryStorage    | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |
| 12  | \[2.0.0+\] CreateHandleStorage | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |

## IProcessWindingController

| Cmd | Name                                             | Notes                                                                          |
| --- | ------------------------------------------------ | ------------------------------------------------------------------------------ |
| 0   | [\#GetLaunchReason](#GetLaunchReason "wikilink") |                                                                                |
| 11  | OpenCallingLibraryApplet                         | Returns an [\#ILibraryAppletAccessor](#ILibraryAppletAccessor "wikilink").     |
| 21  | PushContext                                      | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |
| 22  | PopContext                                       | Returns an [IStorage](Filesystem%20services#IStorage.md##IStorage "wikilink"). |
| 23  | CancelWindingReservation                         |                                                                                |
| 30  | WindAndDoReserved                                |                                                                                |
| 40  | ReserveToStartAndWaitAndUnwindThis               | Returns an [\#ILibraryAppletAccessor](#ILibraryAppletAccessor "wikilink").     |

### GetLaunchReason

No input. Returns an u32 AppletProcessLaunchReason.

Used by
LibraryApplets.

## IDebugFunctions

| Cmd | Name                            | Notes                                                                  |
| --- | ------------------------------- | ---------------------------------------------------------------------- |
| 0   | NotifyMessageToHomeMenuForDebug |                                                                        |
| 1   | OpenMainApplication             | Returns an [\#IApplicationAccessor](#IApplicationAccessor "wikilink"). |
| 10  | EmulateButtonEvent              |                                                                        |
| 20  | InvalidateTransitionLayer       |                                                                        |

# appletOE

This is
"nn::am::<service::IApplicationProxyService>".

| Cmd | Name                                                       | Notes |
| --- | ---------------------------------------------------------- | ----- |
| 0   | [\#OpenApplicationProxy](#OpenApplicationProxy "wikilink") |       |
|     |                                                            |       |

This seems to be used by all(?) regular-applications, even
[flog](Flog.md "wikilink").

## OpenApplicationProxy

Returns an [\#IApplicationProxy](#IApplicationProxy "wikilink"). See
[\#appletAE](#appletAE "wikilink").

Takes a [reserved](IPC%20Marshalling.md "wikilink") input u64(official
user-processes use hard-coded value 0), a PID, and a process
copy-handle(cur-proc handle alias).

On failure, official user-processes will retry using this command in a
loop while the retval is 0x19280, with svcSleepThread(10000000) being
called first.

# idle:sys

# omm

Operation Mode Manager (OMM) is a service responsible for arbitrating
the operation changes between docked and handheld modes. Besides
[PTM\_services](PTM%20services.md "wikilink"), this is the only service
that interacts with the [Dock](Dock.md "wikilink") through
[usb:pd\*](USB%20services.md "wikilink").

| Cmd | Name                        |
| --- | --------------------------- |
| 0   | GetOperationMode            |
| 1   | GetOperationModeChangeEvent |
| 2   | EnableAudioVisual           |
| 3   | DisableAudioVisual          |
| 4   | EnterSleepAndWait           |
| 5   | GetCradleStatus             |
| 6   | FadeInDisplay               |
| 7   | FadeOutDisplay              |
| 8   | \[2.0.0+\]                  |
| 9   | \[2.0.0+\]                  |

# spsm

This is "IPowerStateInterface".

| Cmd | Name                    |
| --- | ----------------------- |
| 0   | GetState                |
| 1   | SleepSystemAndWaitAwake |
| 2   |                         |
| 3   |                         |
| 4   |                         |
| 5   |                         |
| 6   |                         |
| 7   |                         |
| 8   |                         |
| 9   |                         |

# Enums

### AppletId

| ID   | Title-id         | Description                                                                                                      |
| ---- | ---------------- | ---------------------------------------------------------------------------------------------------------------- |
| 0x02 | 010000000000100C | "overlayDisp"                                                                                                    |
| 0x03 | 0100000000001000 | "qlaunch"                                                                                                        |
| 0x04 | 0100000000001012 | "starter"                                                                                                        |
| 0x0A | 0100000000001001 | "auth"                                                                                                           |
| 0x0B | 0100000000001002 | "cabinet"                                                                                                        |
| 0x0C | 0100000000001003 | "controller"                                                                                                     |
| 0x0D | 0100000000001004 | "dataErase"                                                                                                      |
| 0x0E | 0100000000001005 | "error"                                                                                                          |
| 0x0F | 0100000000001006 | "netConnect"                                                                                                     |
| 0x10 | 0100000000001007 | "playerSelect"                                                                                                   |
| 0x11 | 0100000000001008 | "swkbd"                                                                                                          |
| 0x12 | 0100000000001009 | "miiEdit"                                                                                                        |
| 0x13 | 010000000000100A | "LibAppletWeb" [WebApplet](Internet%20Browser#010000000000100A.md##010000000000100A "wikilink") applet           |
| 0x14 | 010000000000100B | "LibAppletShop" [ShopN](Internet%20Browser#ShopN.md##ShopN "wikilink") applet                                    |
| 0x15 | 010000000000100D | "photoViewer"                                                                                                    |
| 0x16 | 010000000000100E |                                                                                                                  |
| 0x17 | 010000000000100F | "LibAppletOff" [Offline](Internet%20Browser#Offline%20Applet.md##Offline_Applet "wikilink") applet               |
| 0x18 | 0100000000001010 | "LibAppletLns" [Whitelisted](Internet%20Browser#Whitelisted%20Applets.md##Whitelisted_Applets "wikilink") applet |
| 0x19 | 0100000000001011 | "LibAppletAuth" [WifiWebAuth](Internet%20Browser#WifiWebAuthApplet.md##WifiWebAuthApplet "wikilink") applet      |
| 0x1A | 0100000000001013 | "myPage"                                                                                                         |
|      |                  |                                                                                                                  |

### ShimKind

This is from strings and code in the [
web-applets](Internet%20Browser.md "wikilink").

This indicates the type of web-applet.

| shimKind value | Description       |
| -------------- | ----------------- |
| 2              | LoginApplet       |
| 4              | ShareApplet       |
| 5              | WebApplet         |
| 6              | WifiWebAuthApplet |
| 7              | LobbyApplet       |

### NotificationMessage

| ID   | Description             |
| ---- | ----------------------- |
| 0x10 | ?                       |
| 0x1E | OperationMode changed   |
| 0x1F | PerformanceMode changed |

# AppletResourceUserId

This u64 is officially called "nn::applet::AppletResourceUserId". Used
by a number of non-AM services.

[Category:Services](Category:Services "wikilink")

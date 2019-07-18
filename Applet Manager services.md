AM (Applet Manager) provides services for interacting with system
applets while abstracting several aspects of power and operation
management.

Contains multiple raw images, with at least the following:
"NN\_OMM\_CHARGING\_BIN\_{begin|end}"(charging icon), low-battery icon,
and the Nintendo Switch logo displayed during system boot.

# appletAE

This is "nn::am::<service::IAllSystemAppletProxiesService>".

| Cmd  | Name                                                                                               | Notes                                                                |
| ---- | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| 100  | OpenSystemAppletProxy                                                                              | Returns an [\#ISystemAppletProxy](#ISystemAppletProxy "wikilink").   |
| 200  | OpenLibraryAppletProxyOld (\[1.0.0-2.3.0\] OpenLibraryAppletProxy)                                 | Returns an [\#ILibraryAppletProxy](#ILibraryAppletProxy "wikilink"). |
| 201  | \[3.0.0+\] [\#OpenLibraryAppletProxy](#OpenLibraryAppletProxy "wikilink")                          | Returns an [\#ILibraryAppletProxy](#ILibraryAppletProxy "wikilink"). |
| 300  | OpenOverlayAppletProxy                                                                             | Returns an [\#IOverlayAppletProxy](#IOverlayAppletProxy "wikilink"). |
| 350  | OpenSystemApplicationProxy                                                                         | Returns an [\#IApplicationProxy](#IApplicationProxy "wikilink").     |
| 400  | [\#CreateSelfLibraryAppletCreatorForDevelop](#CreateSelfLibraryAppletCreatorForDevelop "wikilink") |                                                                      |
| 410  | \[6.0.0+\] [\#GetSystemAppletControllerForDebug](#GetSystemAppletControllerForDebug "wikilink")    |                                                                      |
| 1000 | \[6.0.0+\] [\#GetDebugFunctions](#GetDebugFunctions "wikilink")                                    |                                                                      |

All of these Open\*Proxy commands except
[\#OpenLibraryAppletProxy](#OpenLibraryAppletProxy "wikilink") take the
same input as
[\#OpenApplicationProxy](#OpenApplicationProxy "wikilink"), with the
same user-process retry-loop as
[\#OpenApplicationProxy](#OpenApplicationProxy "wikilink"). These
Open\*Proxy commands (including appletOE) doesn't seem to usable from
processes which aren't actual applets (such as sysmodules), at least for
applet-types which aren't already in use.

This service is used by all system non-regular-applications.

The 01000000000010XX system [titles](Title%20list.md "wikilink") use the
following applet types(above Open{type}Proxy commands):

  - "qlaunch": SystemApplet
  - "overlay": OverlayApplet
  - "starter": SystemApplication
  - "maintenance": SystemApplet
  - All others: LibraryApplet

## OpenLibraryAppletProxy

Returns an [\#ILibraryAppletProxy](#ILibraryAppletProxy "wikilink").

Takes a [reserved](IPC%20Marshalling.md "wikilink") input u64(official
user-processes use hard-coded value 0), a PID,a process
copy-handle(cur-proc handle alias), and an 0x80-byte type-0x15 input
buffer **AppletAttribute**.

Official user-processes use the same retry loop with this as the other
Open\*Proxy commands.

## CreateSelfLibraryAppletCreatorForDevelop

Takes a PID and an input u64 pid\_placeholder, returns an
[\#ILibraryAppletCreator](#ILibraryAppletCreator "wikilink").

The cached value loaded from
[Settings\_services\#GetDebugModeFlag](Settings%20services#GetDebugModeFlag.md##GetDebugModeFlag "wikilink")
must be 1, otherwise an error is returned.

The cached value loaded from
[system-setting](System%20Settings.md "wikilink")
`am.debug!dev_function` must be set to 0x1 with size 0x1, otherwise an
error is returned.

## GetSystemAppletControllerForDebug

No input, returns an
[\#ISystemAppletControllerForDebug](#ISystemAppletControllerForDebug "wikilink").

The cached value loaded from
[system-setting](System%20Settings.md "wikilink")
`am.debug!dev_function` must be set to 0x1 with size 0x1, and various
state checks must pass, otherwise 0 is returned with no output
interface.

## GetDebugFunctions

No input, returns an [\#IDebugFunctions](#IDebugFunctions "wikilink").

The cached value loaded from
[system-setting](System%20Settings.md "wikilink")
`am.debug!dev_function` must be set to 0x1 with size 0x1, otherwise 0 is
returned with no output interface.

## ISystemAppletProxy

| Cmd  | Name                                | Notes                                                                            |
| ---- | ----------------------------------- | -------------------------------------------------------------------------------- |
| 0    | GetCommonStateGetter                | Returns an [\#ICommonStateGetter](#ICommonStateGetter "wikilink").               |
| 1    | GetSelfController                   | Returns an [\#ISelfController](#ISelfController "wikilink").                     |
| 2    | GetWindowController                 | Returns an [\#IWindowController](#IWindowController "wikilink").                 |
| 3    | GetAudioController                  | Returns an [\#IAudioController](#IAudioController "wikilink").                   |
| 4    | GetDisplayController                | Returns an [\#IDisplayController](#IDisplayController "wikilink").               |
| 10   | GetProcessWindingController         | Returns an [\#IProcessWindingController](#IProcessWindingController "wikilink"). |
| 11   | GetLibraryAppletCreator             | Returns an [\#ILibraryAppletCreator](#ILibraryAppletCreator "wikilink").         |
| 20   | GetHomeMenuFunctions                | Returns an [\#IHomeMenuFunctions](#IHomeMenuFunctions "wikilink").               |
| 21   | GetGlobalStateController            | Returns an [\#IGlobalStateController](#IGlobalStateController "wikilink").       |
| 22   | GetApplicationCreator               | Returns an [\#IApplicationCreator](#IApplicationCreator "wikilink").             |
| 23   | \[7.0.0+\] GetAppletCommonFunctions | Returns an [\#IAppletCommonFunctions](#IAppletCommonFunctions "wikilink").       |
| 1000 | GetDebugFunctions                   | Returns an [\#IDebugFunctions](#IDebugFunctions "wikilink").                     |

### IHomeMenuFunctions

| Cmd | Name                                                                             | Notes |
| --- | -------------------------------------------------------------------------------- | ----- |
| 10  | RequestToGetForeground                                                           |       |
| 11  | LockForeground                                                                   |       |
| 12  | UnlockForeground                                                                 |       |
| 20  | [\#PopFromGeneralChannel](#PopFromGeneralChannel "wikilink")                     |       |
| 21  | [\#GetPopFromGeneralChannelEvent](#GetPopFromGeneralChannelEvent "wikilink")     |       |
| 30  | [\#GetHomeButtonWriterLockAccessor](#GetHomeButtonWriterLockAccessor "wikilink") |       |
| 31  | \[2.0.0+\] [\#GetWriterLockAccessorEx](#GetWriterLockAccessorEx "wikilink")      |       |
| 100 | \[6.0.0+\] PopRequestLaunchApplicationForDebug                                   |       |
| 200 | \[8.0.0+\] [\#LaunchDevMenu](#LaunchDevMenu "wikilink")                          |       |

#### PopFromGeneralChannel

No input, returns an output [\#IStorage](#IStorage "wikilink").

#### GetPopFromGeneralChannelEvent

No input, returns an output handle.

#### GetHomeButtonWriterLockAccessor

No input, returns an output
[\#ILockAccessor](#ILockAccessor "wikilink").

#### GetWriterLockAccessorEx

Takes an input u32, returns an output
[\#ILockAccessor](#ILockAccessor "wikilink").

#### LaunchDevMenu

No input/output.

Uses
[NS\_Services\#IApplicationManagerInterface](NS%20Services#IApplicationManagerInterface.md##IApplicationManagerInterface "wikilink")
cmd99.

#### ILockAccessor

| Cmd | Name                               |
| --- | ---------------------------------- |
| 1   | TryLock                            |
| 2   | Unlock                             |
| 3   | [\#GetEvent](#GetEvent "wikilink") |

##### GetEvent

No input, returns an output handle.

### IGlobalStateController

| Cmd | Name                                                                          | Notes |
| --- | ----------------------------------------------------------------------------- | ----- |
| 0   | RequestToEnterSleep                                                           |       |
| 1   | EnterSleep                                                                    |       |
| 2   | StartSleepSequence                                                            |       |
| 3   | StartShutdownSequence                                                         |       |
| 4   | StartRebootSequence                                                           |       |
| 9   | \[7.0.0+\] [\#IsAutoPowerDownRequested](#IsAutoPowerDownRequested "wikilink") |       |
| 10  | LoadAndApplyIdlePolicySettings                                                |       |
| 11  | \[2.0.0+\] NotifyCecSettingsChanged                                           |       |
| 12  | \[3.0.0+\] SetDefaultHomeButtonLongPressTime                                  |       |
| 13  | \[3.0.0+\] UpdateDefaultDisplayResolution                                     |       |
| 14  | \[3.0.0+\] [\#ShouldSleepOnBoot](#ShouldSleepOnBoot "wikilink")               |       |
| 15  | \[4.0.0+\] GetHdcpAuthenticationFailedEvent                                   |       |

#### IsAutoPowerDownRequested

No input, returns an output u8 bool.

#### ShouldSleepOnBoot

No input, returns an output u8 bool.

### IApplicationCreator

| Cmd | Name                                                                                       | Notes |
| --- | ------------------------------------------------------------------------------------------ | ----- |
| 0   | [\#CreateApplication](#CreateApplication "wikilink")                                       |       |
| 1   | [\#PopLaunchRequestedApplication](#PopLaunchRequestedApplication "wikilink")               |       |
| 10  | [\#CreateSystemApplication](#CreateSystemApplication "wikilink")                           |       |
| 100 | [\#PopFloatingApplicationForDevelopment](#PopFloatingApplicationForDevelopment "wikilink") |       |

#### CreateApplication

Takes an input u64 `nn::ncm::ApplicationId`(titleID), returns an
[\#IApplicationAccessor](#IApplicationAccessor "wikilink").

#### PopLaunchRequestedApplication

No input, returns an
[\#IApplicationAccessor](#IApplicationAccessor "wikilink").

#### CreateSystemApplication

Takes an input u64 `nn::ncm::SystemApplicationId`, returns an
[\#IApplicationAccessor](#IApplicationAccessor "wikilink").

#### PopFloatingApplicationForDevelopment

No input, returns an
[\#IApplicationAccessor](#IApplicationAccessor "wikilink").

#### IApplicationAccessor

| Cmd | Name                                                                         | Notes |
| --- | ---------------------------------------------------------------------------- | ----- |
| 0   | [\#GetAppletStateChangedEvent](#GetAppletStateChangedEvent "wikilink")       |       |
| 1   | [\#IsCompleted](#IsCompleted "wikilink")                                     |       |
| 10  | Start                                                                        |       |
| 20  | RequestExit                                                                  |       |
| 25  | Terminate                                                                    |       |
| 30  | GetResult                                                                    |       |
| 101 | RequestForApplicationToGetForeground                                         |       |
| 110 | TerminateAllLibraryApplets                                                   |       |
| 111 | AreAnyLibraryAppletsLeft                                                     |       |
| 112 | [\#GetCurrentLibraryApplet](#GetCurrentLibraryApplet "wikilink")             |       |
| 120 | GetApplicationId                                                             |       |
| 121 | [\#PushLaunchParameter](#PushLaunchParameter "wikilink")                     |       |
| 122 | [\#GetApplicationControlProperty](#GetApplicationControlProperty "wikilink") |       |
| 123 | \[2.0.0+\] GetApplicationLaunchProperty                                      |       |
| 124 | \[6.0.0+\] GetApplicationLaunchRequestInfo                                   |       |
| 130 | \[6.0.0+\] SetUsers                                                          |       |
| 131 | \[6.0.0+\] CheckRightsEnvironmentAvailable                                   |       |
| 132 | \[6.0.0+\] GetNsRightsEnvironmentHandle                                      |       |
| 140 | \[6.0.0+\] GetDesirableUids                                                  |       |
| 150 | \[6.0.0+\] ReportApplicationExitTimeout                                      |       |
| 160 | \[8.0.0+\] [\#SetApplicationAttribute](#SetApplicationAttribute "wikilink")  |       |
| 170 | \[8.0.0+\] HasSaveDataAccessPermission                                       |       |

Commands \<=30 are inherited from
[\#IAppletAccessor](#IAppletAccessor "wikilink").

##### GetCurrentLibraryApplet

No input, returns an output
[\#IAppletAccessor](#IAppletAccessor "wikilink").

##### PushLaunchParameter

Takes an input u32
[\#LaunchParameterKind](#LaunchParameterKind "wikilink") and an input
[\#IStorage](#IStorage "wikilink"), no output.

##### GetApplicationControlProperty

No input, takes a type-0x6 output buffer.

This gets the application [control.nacp](NACP%20Format.md "wikilink").

##### SetApplicationAttribute

Takes a type-0x15 input buffer containing an
[\#ApplicationAttribute](#ApplicationAttribute "wikilink"), no output.

##### IAppletAccessor

| Cmd | Name                                                                   |
| --- | ---------------------------------------------------------------------- |
| 0   | [\#GetAppletStateChangedEvent](#GetAppletStateChangedEvent "wikilink") |
| 1   | [\#IsCompleted](#IsCompleted "wikilink")                               |
| 10  | [\#Start](#Start "wikilink")                                           |
| 20  | [\#RequestExit](#RequestExit "wikilink")                               |
| 25  | [\#Terminate](#Terminate "wikilink")                                   |
| 30  | [\#GetResult](#GetResult "wikilink")                                   |

#### GetAppletStateChangedEvent

No input, returns an output event handle with autoclear=false.

#### IsCompleted

No input, returns an output u8 bool.

#### Start

No input/output.

#### RequestExit

No input/output.

#### Terminate

No input/output.

#### GetResult

No input/output.

## IAppletCommonFunctions

Added with [7.0.0](7.0.0.md "wikilink").

| Cmd | Name                                       | Notes                                                                                                          |
| --- | ------------------------------------------ | -------------------------------------------------------------------------------------------------------------- |
| 10  | ReadThemeStorage                           | Takes an input u64 **offset** and a type-0x22 output buffer, returns an output u64 **actual\_transfer\_size**. |
| 11  | WriteThemeStorage                          | Takes an input u64 **offset** and a type-0x21 input buffer, no output.                                         |
| 40  | \[8.0.0+\] GetDisplayLogicalResolution     |                                                                                                                |
| 42  | \[8.0.0+\] SetDisplayMagnification         |                                                                                                                |
| 50  | \[8.0.0+\] SetHomeButtonDoubleClickEnabled |                                                                                                                |
| 51  | \[8.0.0+\] GetHomeButtonDoubleClickEnabled |                                                                                                                |

ReadThemeStorage/WriteThemeStorage: these commands copy data from/to a
state buffer and the user specified buffer. The size of the state buffer
is 0x400-bytes.

## ILibraryAppletProxy

| Cmd  | Name                                | Notes                                                                                |
| ---- | ----------------------------------- | ------------------------------------------------------------------------------------ |
| 0    | GetCommonStateGetter                | Returns an [\#ICommonStateGetter](#ICommonStateGetter "wikilink").                   |
| 1    | GetSelfController                   | Returns an [\#ISelfController](#ISelfController "wikilink").                         |
| 2    | GetWindowController                 | Returns an [\#IWindowController](#IWindowController "wikilink").                     |
| 3    | GetAudioController                  | Returns an [\#IAudioController](#IAudioController "wikilink").                       |
| 4    | GetDisplayController                | Returns an [\#IDisplayController](#IDisplayController "wikilink").                   |
| 10   | GetProcessWindingController         | Returns an [\#IProcessWindingController](#IProcessWindingController "wikilink").     |
| 11   | GetLibraryAppletCreator             | Returns an [\#ILibraryAppletCreator](#ILibraryAppletCreator "wikilink").             |
| 20   | OpenLibraryAppletSelfAccessor       | Returns an [\#ILibraryAppletSelfAccessor](#ILibraryAppletSelfAccessor "wikilink").   |
| 21   | \[7.0.0+\] GetAppletCommonFunctions | No input, returns an [\#IAppletCommonFunctions](#IAppletCommonFunctions "wikilink"). |
| 1000 | GetDebugFunctions                   | Returns an [\#IDebugFunctions](#IDebugFunctions "wikilink").                         |

### ILibraryAppletSelfAccessor

| Cmd | Name                                                                                                        | Notes |
| --- | ----------------------------------------------------------------------------------------------------------- | ----- |
| 0   | [\#PopInData](#PopInData "wikilink")                                                                        |       |
| 1   | [\#PushOutData](#PushOutData "wikilink")                                                                    |       |
| 2   | [\#PopInteractiveInData](#PopInteractiveInData "wikilink")                                                  |       |
| 3   | [\#PushInteractiveOutData](#PushInteractiveOutData "wikilink")                                              |       |
| 5   | [\#GetPopInDataEvent](#GetPopInDataEvent "wikilink")                                                        |       |
| 6   | [\#GetPopInteractiveInDataEvent](#GetPopInteractiveInDataEvent "wikilink")                                  |       |
| 10  | [\#ExitProcessAndReturn](#ExitProcessAndReturn "wikilink")                                                  |       |
| 11  | [\#GetLibraryAppletInfo](#GetLibraryAppletInfo "wikilink")                                                  |       |
| 12  | GetMainAppletIdentityInfo                                                                                   |       |
| 13  | [\#CanUseApplicationCore](#CanUseApplicationCore "wikilink")                                                |       |
| 14  | GetCallerAppletIdentityInfo                                                                                 |       |
| 15  | \[2.0.0+\] [\#GetMainAppletApplicationControlProperty](#GetMainAppletApplicationControlProperty "wikilink") |       |
| 16  | \[2.0.0+\] [\#GetMainAppletStorageId](#GetMainAppletStorageId "wikilink")                                   |       |
| 17  | \[3.0.0+\] GetCallerAppletIdentityInfoStack                                                                 |       |
| 18  | \[4.0.0+\] GetNextReturnDestinationAppletIdentityInfo                                                       |       |
| 19  | \[4.0.0+\] GetDesirableKeyboardLayout                                                                       |       |
| 20  | [\#PopExtraStorage](#PopExtraStorage "wikilink")                                                            |       |
| 25  | [\#GetPopExtraStorageEvent](#GetPopExtraStorageEvent "wikilink")                                            |       |
| 30  | [\#UnpopInData](#UnpopInData "wikilink")                                                                    |       |
| 31  | [\#UnpopExtraStorage](#UnpopExtraStorage "wikilink")                                                        |       |
| 40  | \[2.0.0+\] GetIndirectLayerProducerHandle                                                                   |       |
| 50  | \[3.0.0+\] ReportVisibleError                                                                               |       |
| 51  | \[4.0.0+\] ReportVisibleErrorWithErrorContext                                                               |       |
| 60  | \[4.0.0+\] [\#GetMainAppletApplicationDesiredLanguage](#GetMainAppletApplicationDesiredLanguage "wikilink") |       |
| 70  | \[8.0.0+\] GetCurrentApplicationId                                                                          |       |
| 80  | \[6.0.0+\] RequestExitToSelf                                                                                |       |
| 90  | \[5.0.0+\] CreateApplicationAndPushAndRequestToLaunch                                                       |       |
| 100 | \[4.0.0+\] [\#CreateGameMovieTrimmer](#CreateGameMovieTrimmer "wikilink")                                   |       |
| 101 | \[5.0.0+\] ReserveResourceForMovieOperation                                                                 |       |
| 102 | \[5.0.0+\] UnreserveResourceForMovieOperation                                                               |       |
| 110 | \[6.0.0+\] GetMainAppletAvailableUsers                                                                      |       |

#### PopInData

No input, returns an output [\#IStorage](#IStorage "wikilink").

#### PushOutData

Takes an input [\#IStorage](#IStorage "wikilink"), no output.

#### PopInteractiveInData

No input, returns an output [\#IStorage](#IStorage "wikilink").

#### PushInteractiveOutData

Takes an input [\#IStorage](#IStorage "wikilink"), no output.

#### GetPopInDataEvent

No input, returns an output handle.

#### GetPopInteractiveInDataEvent

No input, returns an output handle.

#### GetMainAppletApplicationControlProperty

No input, takes a type-0x16 output buffer.

This gets the [control.nacp](NACP%20Format.md "wikilink").

#### GetMainAppletStorageId

No input, returns an output u8 storageId.

#### ExitProcessAndReturn

No input/output.

Exits the LibraryApplet and returns to running the title which launched
this LibraryApplet ([qlaunch](Qlaunch.md "wikilink") for example).

#### GetLibraryAppletInfo

No input. Returns an output
[\#LibraryAppletInfo](#LibraryAppletInfo "wikilink").

#### CanUseApplicationCore

No input, returns an output u8 bool.

#### PopExtraStorage

No input, returns an output [\#IStorage](#IStorage "wikilink").

#### GetPopExtraStorageEvent

No input, returns an output handle.

#### UnpopInData

Takes an input [\#IStorage](#IStorage "wikilink"), no output.

#### UnpopExtraStorage

Takes an input [\#IStorage](#IStorage "wikilink"), no output.

#### GetMainAppletApplicationDesiredLanguage

No input, returns an output
[LanguageCode](Settings%20services#LanguageCode.md##LanguageCode "wikilink").

#### CreateGameMovieTrimmer

Takes an input u64 and handle, returns a GRC
[IGameMovieTrimmer](GRC%20services#IGameMovieTrimmer.md##IGameMovieTrimmer "wikilink").

## IOverlayAppletProxy

| Cmd  | Name                                | Notes                                                                                |
| ---- | ----------------------------------- | ------------------------------------------------------------------------------------ |
| 0    | GetCommonStateGetter                | Returns an [\#ICommonStateGetter](#ICommonStateGetter "wikilink").                   |
| 1    | GetSelfController                   | Returns an [\#ISelfController](#ISelfController "wikilink").                         |
| 2    | GetWindowController                 | Returns an [\#IWindowController](#IWindowController "wikilink").                     |
| 3    | GetAudioController                  | Returns an [\#IAudioController](#IAudioController "wikilink").                       |
| 4    | GetDisplayController                | Returns an [\#IDisplayController](#IDisplayController "wikilink").                   |
| 10   | GetProcessWindingController         | Returns an [\#IProcessWindingController](#IProcessWindingController "wikilink").     |
| 11   | GetLibraryAppletCreator             | Returns an [\#ILibraryAppletCreator](#ILibraryAppletCreator "wikilink").             |
| 20   | GetOverlayFunctions                 | Returns an [\#IOverlayFunctions](#IOverlayFunctions "wikilink").                     |
| 21   | \[7.0.0+\] GetAppletCommonFunctions | No input, returns an [\#IAppletCommonFunctions](#IAppletCommonFunctions "wikilink"). |
| 1000 | GetDebugFunctions                   | Returns an [\#IDebugFunctions](#IDebugFunctions "wikilink").                         |

### IOverlayFunctions

| Cmd | Name                                                |
| --- | --------------------------------------------------- |
| 0   | BeginToWatchShortHomeButtonMessage                  |
| 1   | EndToWatchShortHomeButtonMessage                    |
| 2   | GetApplicationIdForLogo                             |
| 3   | SetGpuTimeSliceBoost                                |
| 4   | \[2.0.0+\] SetAutoSleepTimeAndDimmingTimeEnabled    |
| 5   | \[2.0.0+\] TerminateApplicationAndSetReason         |
| 6   | \[3.0.0+\] SetScreenShotPermissionGlobally          |
| 10  | \[6.0.0+\] StartShutdownSequenceForOverlay          |
| 11  | \[6.0.0+\] StartRebootSequenceForOverlay            |
| 20  | \[8.0.0+\] SetHandlingHomeButtonShortPressedEnabled |
| 90  | \[7.0.0+\] SetRequiresGpuResourceUse                |
| 101 | \[5.0.0+\] BeginToObserveHidInputForDevelop         |

#### SetRequiresGpuResourceUse

Takes an input u8, no output.

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

### IApplicationFunctions

| Cmd  | Name                                                                                                                                                      | Notes |
| ---- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | ----- |
| 1    | [\#PopLaunchParameter](#PopLaunchParameter "wikilink")                                                                                                    |       |
| 10   | [\#CreateApplicationAndPushAndRequestToStart](#CreateApplicationAndPushAndRequestToStart "wikilink")                                                      |       |
| 11   | \[3.0.0+\] [\#CreateApplicationAndPushAndRequestToStartForQuest](#CreateApplicationAndPushAndRequestToStartForQuest "wikilink")                           |       |
| 12   | \[4.0.0+\] [\#CreateApplicationAndRequestToStart](#CreateApplicationAndRequestToStart "wikilink")                                                         |       |
| 13   | \[4.0.0+\] [\#CreateApplicationAndRequestToStartForQuest](#CreateApplicationAndRequestToStartForQuest "wikilink")                                         |       |
| 14   | \[7.0.0+\] [\#CreateApplicationWithAttributeAndPushAndRequestToStartForQuest](#CreateApplicationWithAttributeAndPushAndRequestToStartForQuest "wikilink") |       |
| 15   | \[7.0.0+\] [\#CreateApplicationWithAttributeAndRequestToStartForQuest](#CreateApplicationWithAttributeAndRequestToStartForQuest "wikilink")               |       |
| 20   | EnsureSaveData                                                                                                                                            |       |
| 21   | [\#GetDesiredLanguage](#GetDesiredLanguage "wikilink")                                                                                                    |       |
| 22   | [\#SetTerminateResult](#SetTerminateResult "wikilink")                                                                                                    |       |
| 23   | [\#GetDisplayVersion](#GetDisplayVersion "wikilink")                                                                                                      |       |
| 24   | \[2.0.0+\] GetLaunchStorageInfoForDebug                                                                                                                   |       |
| 25   | \[3.0.0+\] ExtendSaveData                                                                                                                                 |       |
| 26   | \[3.0.0+\] GetSaveDataSize                                                                                                                                |       |
| 27   | \[5.0.0+\] CreateCacheStorage                                                                                                                             |       |
| 30   | [\#BeginBlockingHomeButtonShortAndLongPressed](#BeginBlockingHomeButtonShortAndLongPressed "wikilink")                                                    |       |
| 31   | [\#EndBlockingHomeButtonShortAndLongPressed](#EndBlockingHomeButtonShortAndLongPressed "wikilink")                                                        |       |
| 32   | [\#BeginBlockingHomeButton](#BeginBlockingHomeButton "wikilink")                                                                                          |       |
| 33   | [\#EndBlockingHomeButton](#EndBlockingHomeButton "wikilink")                                                                                              |       |
| 40   | [\#NotifyRunning](#NotifyRunning "wikilink")                                                                                                              |       |
| 50   | \[2.0.0+\] [\#GetPseudoDeviceId](#GetPseudoDeviceId "wikilink")                                                                                           |       |
| 60   | \[2.0.0+\] [\#SetMediaPlaybackStateForApplication](#SetMediaPlaybackStateForApplication "wikilink")                                                       |       |
| 65   | \[3.0.0+\] [\#IsGamePlayRecordingSupported](#IsGamePlayRecordingSupported "wikilink")                                                                     |       |
| 66   | \[3.0.0+\] [\#InitializeGamePlayRecording](#InitializeGamePlayRecording "wikilink")                                                                       |       |
| 67   | \[3.0.0+\] [\#SetGamePlayRecordingState](#SetGamePlayRecordingState "wikilink")                                                                           |       |
| 68   | \[4.0.0+\] [\#RequestFlushGamePlayingMovieForDebug](#RequestFlushGamePlayingMovieForDebug "wikilink")                                                     |       |
| 70   | \[3.0.0+\] [\#RequestToShutdown](#RequestToShutdown "wikilink")                                                                                           |       |
| 71   | \[3.0.0+\] [\#RequestToReboot](#RequestToReboot "wikilink")                                                                                               |       |
| 80   | \[4.0.0+\] [\#ExitAndRequestToShowThanksMessage](#ExitAndRequestToShowThanksMessage "wikilink")                                                           |       |
| 90   | \[4.0.0+\] [\#EnableApplicationCrashReport](#EnableApplicationCrashReport "wikilink")                                                                     |       |
| 100  | \[5.0.0+\] [\#InitializeApplicationCopyrightFrameBuffer](#InitializeApplicationCopyrightFrameBuffer "wikilink")                                           |       |
| 101  | \[5.0.0+\] [\#SetApplicationCopyrightImage](#SetApplicationCopyrightImage "wikilink")                                                                     |       |
| 102  | \[5.0.0+\] [\#SetApplicationCopyrightVisibility](#SetApplicationCopyrightVisibility "wikilink")                                                           |       |
| 110  | \[5.0.0+\] [\#QueryApplicationPlayStatistics](#QueryApplicationPlayStatistics "wikilink")                                                                 |       |
| 111  | \[6.0.0+\] [\#QueryApplicationPlayStatisticsByUid](#QueryApplicationPlayStatisticsByUid "wikilink")                                                       |       |
| 120  | \[5.0.0+\] [\#ExecuteProgram](#ExecuteProgram "wikilink")                                                                                                 |       |
| 121  | \[5.0.0+\] [\#ClearUserChannel](#ClearUserChannel "wikilink")                                                                                             |       |
| 122  | \[5.0.0+\] [\#UnpopToUserChannel](#UnpopToUserChannel "wikilink")                                                                                         |       |
| 123  | \[5.0.0+\] [\#GetPreviousProgramIndex](#GetPreviousProgramIndex "wikilink")                                                                               |       |
| 124  | \[6.0.0+\] [\#EnableApplicationAllThreadDumpOnCrash](#EnableApplicationAllThreadDumpOnCrash "wikilink")                                                   |       |
| 130  | \[8.0.0+\] [\#GetGpuErrorDetectedSystemEvent](#GetGpuErrorDetectedSystemEvent "wikilink")                                                                 |       |
| 500  | \[5.0.0+\] StartContinuousRecordingFlushForDebug                                                                                                          |       |
| 1000 | \[5.0.0+\] [\#CreateMovieMaker](#CreateMovieMaker "wikilink")                                                                                             |       |
| 1001 | \[5.0.0+\] [\#PrepareForJit](#PrepareForJit "wikilink")                                                                                                   |       |

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

#### PopLaunchParameter

Takes an input u32
[\#LaunchParameterKind](#LaunchParameterKind "wikilink"), returns an
output [\#IStorage](#IStorage "wikilink").

Pops a LaunchParameter [\#IStorage](#IStorage "wikilink"), the storage
will be removed from sysmodule state during this.

#### CreateApplicationAndPushAndRequestToStart

Takes an input u64 titleID and an input
[\#IStorage](#IStorage "wikilink"), no output. titleID=0 can be used to
relaunch the current application.

#### CreateApplicationAndPushAndRequestToStartForQuest

Takes 2 input u32s (loaded from struct
[\#ApplicationAttributeForQuest](#ApplicationAttributeForQuest "wikilink")),
an input u64 titleID, and an input [\#IStorage](#IStorage "wikilink"),
no output.

#### CreateApplicationAndRequestToStart

Takes an input u64 titleID, no output.

Same as
[\#CreateApplicationAndPushAndRequestToStart](#CreateApplicationAndPushAndRequestToStart "wikilink")
except without the input storage, official sw uses this when no input
storage is specified.

#### CreateApplicationAndRequestToStartForQuest

Takes 2 input u32s (loaded from struct
[\#ApplicationAttributeForQuest](#ApplicationAttributeForQuest "wikilink"))
and an input u64 titleID, no output.

Same as
[\#CreateApplicationAndPushAndRequestToStartForQuest](#CreateApplicationAndPushAndRequestToStartForQuest "wikilink")
except without the input storage, official sw uses this when no input
storage is specified.

#### CreateApplicationWithAttributeAndPushAndRequestToStartForQuest

Takes an input u64 titleID, a type-0x15 input buffer containing an
[\#ApplicationAttribute](#ApplicationAttribute "wikilink"), an input
[\#IStorage](#IStorage "wikilink"), no output.

Same as
[\#CreateApplicationAndPushAndRequestToStartForQuest](#CreateApplicationAndPushAndRequestToStartForQuest "wikilink")
except the entire attributes structure is directly specified via the
input buffer. This command replaces
[\#CreateApplicationAndPushAndRequestToStartForQuest](#CreateApplicationAndPushAndRequestToStartForQuest "wikilink"),
official user-processes no longer use
[\#CreateApplicationAndPushAndRequestToStartForQuest](#CreateApplicationAndPushAndRequestToStartForQuest "wikilink").

#### CreateApplicationWithAttributeAndRequestToStartForQuest

Takes an input u64 titleID and a type-0x15 input buffer containing an
[\#ApplicationAttribute](#ApplicationAttribute "wikilink"), no output.

Same as
[\#CreateApplicationAndRequestToStartForQuest](#CreateApplicationAndRequestToStartForQuest "wikilink")
except the entire attributes structure is directly specified via the
input buffer. This command replaces
[\#CreateApplicationAndRequestToStartForQuest](#CreateApplicationAndRequestToStartForQuest "wikilink"),
official user-processes no longer use
[\#CreateApplicationAndPushAndRequestToStartForQuest](#CreateApplicationAndPushAndRequestToStartForQuest "wikilink").

#### GetDesiredLanguage

No input, returns an output
[LanguageCode](Settings%20services#LanguageCode.md##LanguageCode "wikilink").

#### SetTerminateResult

Takes an input u32 **Result**, no output.

For example, in some cases official apps use this with
[error](Error%20codes.md "wikilink") 0x2A2 then uses svcBreak.

#### GetDisplayVersion

No input, returns an output 0x10-byte struct.

The output struct is "nn::oe::DisplayVersion". This the DisplayVersion
string copied from the application
[control.nacp](NACP%20Format.md "wikilink"), this is always
NUL-terminated.

#### BeginBlockingHomeButtonShortAndLongPressed

Takes an input s64, no output.

Official user-processes use hard-coded value 0 for the s64.

Starts blocking the Home button.

#### EndBlockingHomeButtonShortAndLongPressed

No input/output.

Ends the blocking started by
[\#BeginBlockingHomeButtonShortAndLongPressed](#BeginBlockingHomeButtonShortAndLongPressed "wikilink").

#### BeginBlockingHomeButton

Takes an input s64 nanoseconds, no output. The input nanoseconds can be
zero.

#### EndBlockingHomeButton

No input/output.

#### NotifyRunning

Takes no input. Returns an output u8 bool, which is ignored by official
user-processes.

#### GetPseudoDeviceId

No input, returns an output 0x10-byte "nn::util::Uuid" struct.

The 0x20-byte output data from
[GetSystemSeedForPseudoDeviceId](NS%20Services.md "wikilink") followed
by the 8-byte [SeedForPseudoDeviceId](NACP%20Format.md "wikilink") from
the current control.nacp, is hashed with SHA1. Then
"nn::util::GenerateUuidVersion5" is called with the final hash, the
output from this is then returned for the Uuid.

#### SetMediaPlaybackStateForApplication

Takes an input u8 bool, no output.

#### IsGamePlayRecordingSupported

No input, returns an output u8 bool.

#### InitializeGamePlayRecording

Takes a TransferMemory handle and an u64 for the size of the
TransferMemory. The size must match 0x6000000 otherwise an error is
returned.

#### SetGamePlayRecordingState

Takes an input u32. 0 = disable/pause, 1 = enable/restart.

#### RequestFlushGamePlayingMovieForDebug

No input/output.

#### RequestToShutdown

No input/output.

#### RequestToReboot

No input/output.

#### ExitAndRequestToShowThanksMessage

No input/output.

Used to exit the application and return to the kiosk menu. Official sw
uses [\#UnlockExit](#UnlockExit "wikilink") immediately before this.

This throws an error when the cached
[Settings\_services\#GetQuestFlag](Settings%20services#GetQuestFlag.md##GetQuestFlag "wikilink")
value is 0.

#### EnableApplicationCrashReport

Takes an input u8 bool, no output.

#### InitializeApplicationCopyrightFrameBuffer

Takes an input TransferMemory handle, an s32 **width**, an s32
**height**, an u64 tmem\_size, and no output.

tmem\_size must be 0x40000-byte aligned. **width** must be 1-1280, and
**height** must be 1-720.

User-processes create the tmem with an user-specified buffer with
permissions=0. **width** = 1280 and **height** = 720.

This is used as an overlay for screenshots.

#### SetApplicationCopyrightImage

Takes a type-0x45 input buffer, an s32 **x**, an s32 **y**, an s32
**width**, an s32 **height**, an s32 **WindowOriginMode**, and no
output.

The last s32 is "nn::oe::WindowOriginMode". This should be at least 1.

**x** and **y** must not have the negative bit set. **width** and
**height** must not be \<1.

Sets the RGBA8 image for use with
[\#InitializeApplicationCopyrightFrameBuffer](#InitializeApplicationCopyrightFrameBuffer "wikilink").
Overrides the current image, if this was already used previously.

#### SetApplicationCopyrightVisibility

Takes an input u8 bool, no output.

Sets the visibility for the image set by
[\#SetApplicationCopyrightImage](#SetApplicationCopyrightImage "wikilink"),
in screenshots. By default it's visible.

#### QueryApplicationPlayStatistics

Takes a type-0x6 output buffer containing an array of
[ApplicationPlayStatistics](Shared%20Database%20services.md "wikilink")
and a type-0x5 input buffer containing an array of u64 titleIDs. Returns
an output s32 for actual total output entries.

The number of entries in each array is the same.

See also
[PlayLogQueryCapability](NACP%20Format#PlayLogQueryCapability.md##PlayLogQueryCapability "wikilink").

This uses [pdm:qry](Shared%20Database%20services.md "wikilink")
QueryApplicationPlayStatisticsForSystem.

#### QueryApplicationPlayStatisticsByUid

Takes a u128 userID, a type-0x6 output buffer containing an array of
[ApplicationPlayStatistics](Shared%20Database%20services.md "wikilink")
and a type-0x5 input buffer containing an array of u64 titleIDs. Returns
an output s32 for actual total output entries.

Same as
[\#QueryApplicationPlayStatistics](#QueryApplicationPlayStatistics "wikilink")
except this uses [pdm:qry](Shared%20Database%20services.md "wikilink")
cmd16, to get playstats specific to userIDs.

#### ExecuteProgram

Takes an input u32
[\#ProgramSpecifyKind](#ProgramSpecifyKind "wikilink") and an input u64,
no output.

#### ClearUserChannel

No input/output.

Clears the UserChannel used by
[\#UnpopToUserChannel](#UnpopToUserChannel "wikilink").

#### UnpopToUserChannel

Takes an input [\#IStorage](#IStorage "wikilink"), no output.

The input storage is pushed to the UserChannel. This is the same channel
used by [\#LaunchParameterKind](#LaunchParameterKind "wikilink") value
1.

User-processes create a storage using data specified by the user
(written to offset=0 size=inputsize), with max size 0x1000. This storage
is then used with this cmd.

#### GetPreviousProgramIndex

No input, returns an output s32.

#### EnableApplicationAllThreadDumpOnCrash

Takes an input u8 bool, no output.

#### GetGpuErrorDetectedSystemEvent

No input, returns an output Event handle with autoclear=false.

This is used by sdknso during applet-application initialization. A
seperate thread is setup where event-waiting is handled. When the Event
is signaled, official sw will assert.

#### CreateMovieMaker

Takes an input u64 and handle, returns an
[\#IMovieMaker](#IMovieMaker "wikilink").

#### PrepareForJit

Takes no input. Launches title 010000000000003B (currently not present
on retail systems) if some context variable is set.

### IMovieMaker

| Cmd | Name                                               |
| --- | -------------------------------------------------- |
| 0   | [\#GetGrcMovieMaker](#GetGrcMovieMaker "wikilink") |
| 1   | [\#GetLayerHandle](#GetLayerHandle "wikilink")     |

#### GetGrcMovieMaker

No input, returns a GRC [IMovieMaker](GRC%20services.md "wikilink").

#### GetLayerHandle

No input, returns an output u64.

## ILibraryAppletCreator

| Cmd | Name                                                                     | Notes |
| --- | ------------------------------------------------------------------------ | ----- |
| 0   | [\#CreateLibraryApplet](#CreateLibraryApplet "wikilink")                 |       |
| 1   | [\#TerminateAllLibraryApplets](#TerminateAllLibraryApplets "wikilink")   |       |
| 2   | [\#AreAnyLibraryAppletsLeft](#AreAnyLibraryAppletsLeft "wikilink")       |       |
| 10  | [\#CreateStorage](#CreateStorage "wikilink")                             |       |
| 11  | [\#CreateTransferMemoryStorage](#CreateTransferMemoryStorage "wikilink") |       |
| 12  | \[2.0.0+\] [\#CreateHandleStorage](#CreateHandleStorage "wikilink")      |       |

### CreateLibraryApplet

Takes 2 input u32s [\#AppletId](#AppletId "wikilink") and
[\#LibraryAppletMode](#LibraryAppletMode "wikilink"), returns an
[\#ILibraryAppletAccessor](#ILibraryAppletAccessor "wikilink").

### TerminateAllLibraryApplets

No input/output.

### AreAnyLibraryAppletsLeft

No input, returns an output u8 bool.

### CreateStorage

Takes an input s64 for the storage size, returns an
[\#IStorage](#IStorage "wikilink").

This allocates a buffer with the specified size which can then be
accessed via [\#IStorageAccessor](#IStorageAccessor "wikilink").

### CreateTransferMemoryStorage

Takes an input TransferMemory copy-handle, an input u8 bool, and an s64
size, returns an [\#IStorage](#IStorage "wikilink").

The user-process creates the TransferMemory with permissions=0.

The TransferMemory is mapped, which can then be accessed via
[\#IStorageAccessor](#IStorageAccessor "wikilink"). The input bool
controls whether writing to the storage is allowed:
[\#Write](#Write "wikilink") will throw an error if this flag is not
set.

### CreateHandleStorage

Takes an input copy-handle and an input s64, returns an
[\#IStorage](#IStorage "wikilink"). In some cases the s64 must not have
the negative bit set.

The input can be arbitrary, however official sw is only (?) known to use
this for TransferMemory (with s64=size).

### ILibraryAppletAccessor

| Cmd | Name                                                                                                 | Notes |
| --- | ---------------------------------------------------------------------------------------------------- | ----- |
| 0   | [\#GetAppletStateChangedEvent](#GetAppletStateChangedEvent "wikilink")                               |       |
| 1   | [\#IsCompleted](#IsCompleted "wikilink")                                                             |       |
| 10  | [\#Start](#Start "wikilink")                                                                         |       |
| 20  | [\#RequestExit](#RequestExit "wikilink")                                                             |       |
| 25  | [\#Terminate](#Terminate "wikilink")                                                                 |       |
| 30  | [\#GetResult](#GetResult "wikilink")                                                                 |       |
| 50  | [\#SetOutOfFocusApplicationSuspendingEnabled](#SetOutOfFocusApplicationSuspendingEnabled "wikilink") |       |
| 100 | [\#PushInData](#PushInData "wikilink")                                                               |       |
| 101 | [\#PopOutData](#PopOutData "wikilink")                                                               |       |
| 102 | [\#PushExtraStorage](#PushExtraStorage "wikilink")                                                   |       |
| 103 | [\#PushInteractiveInData](#PushInteractiveInData "wikilink")                                         |       |
| 104 | [\#PopInteractiveOutData](#PopInteractiveOutData "wikilink")                                         |       |
| 105 | [\#GetPopOutDataEvent](#GetPopOutDataEvent "wikilink")                                               |       |
| 106 | [\#GetPopInteractiveOutDataEvent](#GetPopInteractiveOutDataEvent "wikilink")                         |       |
| 110 | [\#NeedsToExitProcess](#NeedsToExitProcess "wikilink")                                               |       |
| 120 | [\#GetLibraryAppletInfo](#GetLibraryAppletInfo "wikilink")                                           |       |
| 150 | [\#RequestForAppletToGetForeground](#RequestForAppletToGetForeground "wikilink")                     |       |
| 160 | \[2.0.0+\] [\#GetIndirectLayerConsumerHandle](#GetIndirectLayerConsumerHandle "wikilink")            |       |

Commands \<=30 are inherited from
[\#IAppletAccessor](#IAppletAccessor "wikilink"). GetLibraryAppletInfo
is identical to the
[\#ILibraryAppletSelfAccessor](#ILibraryAppletSelfAccessor "wikilink")
cmd.

#### SetOutOfFocusApplicationSuspendingEnabled

Takes an input u8 bool, no output.

#### PushInData

Takes an input [\#IStorage](#IStorage "wikilink"), no output.

#### PopOutData

No input, returns an output [\#IStorage](#IStorage "wikilink").

#### PushExtraStorage

Takes an input [\#IStorage](#IStorage "wikilink"), no output.

#### PushInteractiveInData

Takes an input [\#IStorage](#IStorage "wikilink"), no output.

#### PopInteractiveOutData

No input, returns an output [\#IStorage](#IStorage "wikilink").

#### GetPopOutDataEvent

No input, returns an output handle.

#### GetPopInteractiveOutDataEvent

No input, returns an output event handle with autoclear=false.

#### NeedsToExitProcess

No input, returns an output u8 bool.

#### RequestForAppletToGetForeground

No input/output.

#### GetIndirectLayerConsumerHandle

Takes an input PID and an input u64 AppletResourceUserId, returns an
output u64 IndirectLayerConsumerHandle.

Official sw uses this during LibraryApplet creation when
[\#LibraryAppletMode](#LibraryAppletMode "wikilink") is 0x3.

## ICommonStateGetter

| Cmd | Name                                                                                                      | Notes |
| --- | --------------------------------------------------------------------------------------------------------- | ----- |
| 0   | [\#GetEventHandle](#GetEventHandle "wikilink")                                                            |       |
| 1   | [\#ReceiveMessage](#ReceiveMessage "wikilink")                                                            |       |
| 2   | [\#GetThisAppletKind](#GetThisAppletKind "wikilink")                                                      |       |
| 3   | AllowToEnterSleep                                                                                         |       |
| 4   | DisallowToEnterSleep                                                                                      |       |
| 5   | [\#GetOperationMode](#GetOperationMode "wikilink")                                                        |       |
| 6   | [\#GetPerformanceMode](#GetPerformanceMode "wikilink")                                                    |       |
| 7   | [\#GetCradleStatus](#GetCradleStatus "wikilink")                                                          |       |
| 8   | [\#GetBootMode](#GetBootMode "wikilink")                                                                  |       |
| 9   | [\#GetCurrentFocusState](#GetCurrentFocusState "wikilink")                                                |       |
| 10  | RequestToAcquireSleepLock                                                                                 |       |
| 11  | ReleaseSleepLock                                                                                          |       |
| 12  | ReleaseSleepLockTransiently                                                                               |       |
| 13  | [\#GetAcquiredSleepLockEvent](#GetAcquiredSleepLockEvent "wikilink")                                      |       |
| 20  | [\#PushToGeneralChannel](#PushToGeneralChannel "wikilink")                                                |       |
| 30  | [\#GetHomeButtonReaderLockAccessor](#GetHomeButtonReaderLockAccessor "wikilink")                          |       |
| 31  | \[2.0.0+\] [\#GetReaderLockAccessorEx](#GetReaderLockAccessorEx "wikilink")                               |       |
| 32  | \[7.0.0+\] [\#GetWriterLockAccessorEx](#GetWriterLockAccessorEx "wikilink")                               |       |
| 40  | \[2.0.0+\] GetCradleFwVersion                                                                             |       |
| 50  | \[3.0.0+\] [\#IsVrModeEnabled](#IsVrModeEnabled "wikilink")                                               |       |
| 51  | \[3.0.0+\] [\#SetVrModeEnabled](#SetVrModeEnabled "wikilink")                                             |       |
| 52  | \[4.0.0+\] SetLcdBacklighOffEnabled                                                                       |       |
| 53  | \[7.0.0+\] [\#BeginVrModeEx](#BeginVrModeEx "wikilink")                                                   |       |
| 54  | \[7.0.0+\] [\#EndVrModeEx](#EndVrModeEx "wikilink")                                                       |       |
| 55  | \[3.0.0+\] [\#IsInControllerFirmwareUpdateSection](#IsInControllerFirmwareUpdateSection "wikilink")       |       |
| 60  | \[3.0.0+\] GetDefaultDisplayResolution                                                                    |       |
| 61  | \[3.0.0+\] [\#GetDefaultDisplayResolutionChangeEvent](#GetDefaultDisplayResolutionChangeEvent "wikilink") |       |
| 62  | \[4.0.0+\] GetHdcpAuthenticationState                                                                     |       |
| 63  | \[4.0.0+\] GetHdcpAuthenticationStateChangeEvent                                                          |       |
| 64  | \[5.0.0+\] SetTvPowerStateMatchingMode                                                                    |       |
| 65  | \[5.1.0+\] GetApplicationIdByContentActionName                                                            |       |
| 66  | \[6.0.0+\] [\#SetCpuBoostMode](#SetCpuBoostMode "wikilink")                                               |       |
| 80  | \[6.0.0+\] PerformSystemButtonPressingIfInFocus                                                           |       |
| 90  | \[7.0.0+\] SetPerformanceConfigurationChangedNotification                                                 |       |
| 91  | \[7.0.0+\] GetCurrentPerformanceConfiguration                                                             |       |
| 200 | \[7.0.0+\] GetOperationModeSystemInfo                                                                     |       |

Officially notification messages are handled by the application itself,
not sdk-nso in ExeFS. Official apps call code in sdk-nso which basically
uses svcWaitSynchronization with the event from
[\#GetEventHandle](#GetEventHandle "wikilink") to check whether a
message is available, then if so it uses
[\#ReceiveMessage](#ReceiveMessage "wikilink"). The actual handling for
message IDs is done in the app itself(see
[\#NotificationMessage](#NotificationMessage "wikilink")).

\[7.0.0+\] User-processes now use BeginVrModeEx/EndVrModeEx instead of
[\#SetVrModeEnabled](#SetVrModeEnabled "wikilink"). Prior to using using
BeginVrModeEx, [pctl](Parental%20Control%20services.md "wikilink")
IsStereoVisionPermitted is used and error 0xD08E is thrown if not
allowed by pctl.

### GetEventHandle

No input. Returns an output event handle. This is signalled when a
message is available with
[\#ReceiveMessage](#ReceiveMessage "wikilink").

### ReceiveMessage

No input. Returns an output u32. Error 0x680 indicates no message is
available.

### GetThisAppletKind

No input, returns an output [\#AppletKind](#AppletKind "wikilink").

### GetOperationMode

No input. Returns an output u8 for the current
[\#OperationMode](#OperationMode "wikilink").

### GetPerformanceMode

No input. Returns an output u32 for the current PerformanceMode.

### GetCradleStatus

No input, returns an output u8.

### GetBootMode

No input, returns an output u8.

Returns the value from
[pm:bm](Process%20Manager%20services.md "wikilink") GetBootMode.

### GetCurrentFocusState

No input. Returns an output u8:

  - 1: In focus.
  - 2/3: Out of focus(running in "background").

### GetAcquiredSleepLockEvent

No input, returns an output handle.

### PushToGeneralChannel

Takes an input [\#IStorage](#IStorage "wikilink"), no output.

This is not usable under an Application, however it is usable under a
LibraryApplet.

Used for sending requests to [qlaunch](Qlaunch.md "wikilink"). sdk-nso
creates a 0x10-byte storage which is sent to this. The following are the
functions which use this, with the data written to the storage:

  - `RequestHomeMenu` `5341 4d53 0100 0000 0200 0000 0100 0000` Returns
    to the main Home Menu, equivalent to pressing the HOME button.
  - `RequestJumpToSystemUpdate`
    `5341 4d53 0100 0000 0b00 0000 0100 0000` Equivalent to entering
    "System Update" under System Settings. When leaving this, it returns
    to the main Home Menu.

### GetHomeButtonReaderLockAccessor

No input, returns an output
[\#ILockAccessor](#ILockAccessor "wikilink").

### GetReaderLockAccessorEx

Takes an input u32, returns an output
[\#ILockAccessor](#ILockAccessor "wikilink").

### GetWriterLockAccessorEx

Takes an input u32, returns an output
[\#ILockAccessor](#ILockAccessor "wikilink").

### IsVrModeEnabled

No input, returns an output u8 bool.

### SetVrModeEnabled

Takes an input u8 bool flag. No output.

Updates internal AM state fields. If the new state doesn't match the
previous state, this uses the
[Backlight\_services](Backlight%20services.md "wikilink")
{Disable/Enable}VrMode command depending on whether
flag={disable/enable}.

When the VrMode is set to true, the console shows a screen rendered like
vr asking the user to move his face away and hit the 'close' button.
When this button is pressed, the console resets the vrMode to false.

### BeginVrModeEx

No input/output.

Identical to [\#SetVrModeEnabled](#SetVrModeEnabled "wikilink") except
with hard-coded flag=1.

### EndVrModeEx

No input/output.

Identical to [\#SetVrModeEnabled](#SetVrModeEnabled "wikilink") except
with hard-coded flag=0.

### IsInControllerFirmwareUpdateSection

No input, returns an output u8 bool.

### GetDefaultDisplayResolutionChangeEvent

No input, returns an output handle.

### SetCpuBoostMode

Takes an input u32 **CpuBoostMode** (only modes 0 and 1 are valid) and
passes it to
[SetCpuBoostMode](PPC%20services#apm:sys.md##apm:sys "wikilink").

### SetPerformanceConfigurationChangedNotification

Takes an input u8 bool, no output.

### GetCurrentPerformanceConfiguration

No input, returns the result of calling
[GetCurrentPerformanceConfiguration](PPC%20services#apm:sys.md##apm:sys "wikilink").

### GetOperationModeSystemInfo

No input, returns a total of 4-bytes of output.

## ISelfController

| Cmd  | Name                                                                                                                |
| ---- | ------------------------------------------------------------------------------------------------------------------- |
| 0    | [\#Exit](#Exit "wikilink")                                                                                          |
| 1    | [\#LockExit](#LockExit "wikilink")                                                                                  |
| 2    | [\#UnlockExit](#UnlockExit "wikilink")                                                                              |
| 3    | \[2.0.0+\] [\#EnterFatalSection](#EnterFatalSection "wikilink")                                                     |
| 4    | \[2.0.0+\] [\#LeaveFatalSection](#LeaveFatalSection "wikilink")                                                     |
| 9    | [\#GetLibraryAppletLaunchableEvent](#GetLibraryAppletLaunchableEvent "wikilink")                                    |
| 10   | [\#SetScreenShotPermission](#SetScreenShotPermission "wikilink")                                                    |
| 11   | [\#SetOperationModeChangedNotification](#SetOperationModeChangedNotification "wikilink")                            |
| 12   | [\#SetPerformanceModeChangedNotification](#SetPerformanceModeChangedNotification "wikilink")                        |
| 13   | [\#SetFocusHandlingMode](#SetFocusHandlingMode "wikilink")                                                          |
| 14   | [\#SetRestartMessageEnabled](#SetRestartMessageEnabled "wikilink")                                                  |
| 15   | \[2.0.0+\] [\#SetScreenShotAppletIdentityInfo](#SetScreenShotAppletIdentityInfo "wikilink")                         |
| 16   | \[2.0.0+\] [\#SetOutOfFocusSuspendingEnabled](#SetOutOfFocusSuspendingEnabled "wikilink")                           |
| 17   | \[3.0.0+\] [\#SetControllerFirmwareUpdateSection](#SetControllerFirmwareUpdateSection "wikilink")                   |
| 18   | \[3.0.0+\] [\#SetRequiresCaptureButtonShortPressedMessage](#SetRequiresCaptureButtonShortPressedMessage "wikilink") |
| 19   | \[3.0.0+\] [\#SetAlbumImageOrientation](#SetAlbumImageOrientation "wikilink")                                       |
| 20   | \[4.0.0+\] SetDesirableKeyboardLayout                                                                               |
| 40   | [\#CreateManagedDisplayLayer](#CreateManagedDisplayLayer "wikilink")                                                |
| 41   | \[4.0.0+\] IsSystemBufferSharingEnabled                                                                             |
| 42   | \[4.0.0+\] GetSystemSharedLayerHandle                                                                               |
| 43   | \[5.0.0+\] GetSystemSharedBufferHandle                                                                              |
| 50   | [\#SetHandlesRequestToDisplay](#SetHandlesRequestToDisplay "wikilink")                                              |
| 51   | [\#ApproveToDisplay](#ApproveToDisplay "wikilink")                                                                  |
| 60   | OverrideAutoSleepTimeAndDimmingTime                                                                                 |
| 61   | [\#SetMediaPlaybackState](#SetMediaPlaybackState "wikilink")                                                        |
| 62   | SetIdleTimeDetectionExtension                                                                                       |
| 63   | GetIdleTimeDetectionExtension                                                                                       |
| 64   | SetInputDetectionSourceSet                                                                                          |
| 65   | \[2.0.0+\] [\#ReportUserIsActive](#ReportUserIsActive "wikilink")                                                   |
| 66   | \[3.0.0+\] [\#GetCurrentIlluminance](#GetCurrentIlluminance "wikilink")                                             |
| 67   | \[3.0.0+\] [\#IsIlluminanceAvailable](#IsIlluminanceAvailable "wikilink")                                           |
| 68   | \[5.0.0+\] [\#SetAutoSleepDisabled](#SetAutoSleepDisabled "wikilink")                                               |
| 69   | \[5.0.0+\] [\#IsAutoSleepDisabled](#IsAutoSleepDisabled "wikilink")                                                 |
| 70   | \[4.0.0+\] [\#ReportMultimediaError](#ReportMultimediaError "wikilink")                                             |
| 71   | \[5.0.0+\] [\#GetCurrentIlluminanceEx](#GetCurrentIlluminanceEx "wikilink")                                         |
| 80   | \[4.0.0+\] [\#SetWirelessPriorityMode](#SetWirelessPriorityMode "wikilink")                                         |
| 90   | \[6.0.0+\] GetAccumulatedSuspendedTickValue                                                                         |
| 91   | \[6.0.0+\] GetAccumulatedSuspendedTickChangedEvent                                                                  |
| 100  | \[7.0.0+\] [\#SetAlbumImageTakenNotificationEnabled](#SetAlbumImageTakenNotificationEnabled "wikilink")             |
| 110  | \[8.0.0+\] [\#SetApplicationAlbumUserData](#SetApplicationAlbumUserData "wikilink")                                 |
| 1000 | \[7.0.0+\] [\#GetDebugStorageChannel](#GetDebugStorageChannel "wikilink")                                           |

### Exit

No input/output.

### LockExit

No input/output.

Locks exit process of pressing X to close in HOME Menu for an
application or HOME button for an applet. When locked, it will show the
"waiting for software to be closed dialog" until UnlockExit is called or
a 15 seconds timeout (when the latter occurs, the process is
force-terminated).

### UnlockExit

No input/output.

Unlocks exit process, if LockExit was previously used.

### EnterFatalSection

No input/output.

### LeaveFatalSection

No input/output.

[\#EnterFatalSection](#EnterFatalSection "wikilink") must be executed at
least once before executing this command, otherwise error code 0x40080
will be returned. EnterFatalSection and LeaveFatalSection work in pairs,
that is, N calls to EnterFatalSection must be performed first in order
to perform N executions of LeaveFatalSection. Essentially, these two
functions operate like how one would lock and unlock a recursive mutex.

### GetLibraryAppletLaunchableEvent

No input, returns an output event handle with autoclear=false.

### SetScreenShotPermission

Takes an input s32. No output.

Controls whether screenshot-capture is allowed.

| Value | Description                |
| ----- | -------------------------- |
| 0     | Inherit from parent applet |
| 1     | Enable                     |
| 2     | Disable                    |
|       |                            |

### SetOperationModeChangedNotification

Takes an input u8 bool flag. No output.

### SetPerformanceModeChangedNotification

Takes an input u8 bool flag. No output.

### SetFocusHandlingMode

Takes 3 input u8s with each field located immediately after the previous
u8, these are bool flags. No output.

### SetRestartMessageEnabled

Takes an input u8 bool flag, no output.

See [\#NotificationMessage](#NotificationMessage "wikilink").

### SetScreenShotAppletIdentityInfo

Takes an input 0x10-byte struct AppletIdentityInfo. No output.

### SetOutOfFocusSuspendingEnabled

Takes an input u8 bool flag. No output.

### SetControllerFirmwareUpdateSection

Takes an input u8 bool flag, no output.

### SetRequiresCaptureButtonShortPressedMessage

Takes an input u8 bool flag, no output.

See [\#NotificationMessage](#NotificationMessage "wikilink").

When enabled with a non-Overlay applet, Overlay applet will not be
notified of capture button short-presses for screenshots.

### SetAlbumImageOrientation

Takes an input s32 "nn::album::ImageOrientation". No output.

### CreateManagedDisplayLayer

Returns an output u64 LayerId which is then used by the user-process
with
[Display\_services\#OpenLayer](Display%20services#OpenLayer.md##OpenLayer "wikilink").

### SetHandlesRequestToDisplay

Takes an input u8 bool, no output.

Sets an internal state flag. When the input flag is 0, this will in
additional run the same code as
[\#ApproveToDisplay](#ApproveToDisplay "wikilink").

### ApproveToDisplay

No input/output.

### SetMediaPlaybackState

Takes an input u8 bool, no output.

### ReportUserIsActive

No input/output.

Uses idle:sys ReportUserIsActive.

### GetCurrentIlluminance

No input, returns an output float.

Uses [lbl](Backlight%20services.md "wikilink") command
GetAmbientLightSensorValue, where only the output float is used.

### IsIlluminanceAvailable

No input, returns an output u8 bool.

Uses [lbl](Backlight%20services.md "wikilink") command
IsAmbientLightSensorAvailable.

User-processes can use this to determine whether to continue with using
GetCurrentIlluminance(Ex).

### SetAutoSleepDisabled

Takes an input u8 bool, no output.

### IsAutoSleepDisabled

No input, returns an output u8 bool.

### ReportMultimediaError

Takes an input Result and a type-0x5 input buffer, no output.

The buffer contains a 0x138-byte "movie::MultimediaTelemetryReport"
struct.

### GetCurrentIlluminanceEx

No input, returns an output u8 bool and float.

Uses [lbl](Backlight%20services.md "wikilink") command
GetAmbientLightSensorValue.

### SetWirelessPriorityMode

Takes an input s32 enum **WirelessPriorityMode**, no output.

The input value must be 1 or 2.

### SetAlbumImageTakenNotificationEnabled

Takes an input u8 bool, no output.

See [\#NotificationMessage](#NotificationMessage "wikilink").

### SetApplicationAlbumUserData

Takes a type-0x21 input buffer, no output.

The buffer contains arbitrary UserData.

The size must be \<=0x400. The input buffer is copied to a buffer loaded
from a state ptr (throwing an error when the state ptr is not set), with
the u32 size being written to statebuf+0x400 afterwards.

### GetDebugStorageChannel

Returns an output [\#IStorageChannel](#IStorageChannel "wikilink").

## IStorageChannel

Added with [7.0.0](7.0.0.md "wikilink").

| Cmd | Name              | Notes                                                           |
| --- | ----------------- | --------------------------------------------------------------- |
| 0   | Push              | No input, returns an output [\#IStorage](#IStorage "wikilink"). |
| 1   | Unpop             | No input, returns an output [\#IStorage](#IStorage "wikilink"). |
| 2   | Pop               | No input, returns an output [\#IStorage](#IStorage "wikilink"). |
| 3   | GetPopEventHandle | No input, returns an output handle.                             |
| 4   | Clear             | No input/output.                                                |

## IWindowController

| Cmd | Name                                                             | Notes                                         |
| --- | ---------------------------------------------------------------- | --------------------------------------------- |
| 0   | [\#CreateWindow](#CreateWindow "wikilink")                       |                                               |
| 1   | [\#GetAppletResourceUserId](#GetAppletResourceUserId "wikilink") |                                               |
| 2   | \[6.0.0+\] GetAppletResourceUserIdOfCallerApplet                 |                                               |
| 10  | [\#AcquireForegroundRights](#AcquireForegroundRights "wikilink") |                                               |
| 11  | ReleaseForegroundRights                                          |                                               |
| 12  | RejectToChangeIntoBackground                                     |                                               |
| 20  | \[7.0.0+\] SetAppletWindowVisibility                             | Takes an input u8, no output.                 |
| 21  | \[7.0.0+\] SetAppletGpuTimeSlice                                 | Takes a total of 8-bytes of input, no output. |

### CreateWindow

Takes an input u32, returns an output [\#IWindow](#IWindow "wikilink").

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

GetMainAppletExpectedMasterVolume/SetExpectedMasterVolume are used for
saving/restoring state for LibraryApplet launching, with
SetExpectedMasterVolume being used with new state prior to launching a
LibraryApplet. With official sw these applet funcs are used directly in
the main-codebin.

## IDisplayController

| Cmd | Name                                                                                     |
| --- | ---------------------------------------------------------------------------------------- |
| 0   | GetLastForegroundCaptureImage                                                            |
| 1   | UpdateLastForegroundCaptureImage                                                         |
| 2   | GetLastApplicationCaptureImage                                                           |
| 3   | GetCallerAppletCaptureImage                                                              |
| 4   | UpdateCallerAppletCaptureImage                                                           |
| 5   | GetLastForegroundCaptureImageEx                                                          |
| 6   | GetLastApplicationCaptureImageEx                                                         |
| 7   | GetCallerAppletCaptureImageEx                                                            |
| 8   | \[2.0.0+\] TakeScreenShotOfOwnLayer                                                      |
| 9   | \[5.0.0+\] CopyBetweenCaptureBuffers                                                     |
| 10  | [\#AcquireLastApplicationCaptureBuffer](#AcquireLastApplicationCaptureBuffer "wikilink") |
| 11  | ReleaseLastApplicationCaptureBuffer                                                      |
| 12  | [\#AcquireLastForegroundCaptureBuffer](#AcquireLastForegroundCaptureBuffer "wikilink")   |
| 13  | ReleaseLastForegroundCaptureBuffer                                                       |
| 14  | [\#AcquireCallerAppletCaptureBuffer](#AcquireCallerAppletCaptureBuffer "wikilink")       |
| 15  | ReleaseCallerAppletCaptureBuffer                                                         |
| 16  | AcquireLastApplicationCaptureBufferEx                                                    |
| 17  | AcquireLastForegroundCaptureBufferEx                                                     |
| 18  | AcquireCallerAppletCaptureBufferEx                                                       |
| 20  | \[3.0.0+\] ClearCaptureBuffer                                                            |
| 21  | \[3.0.0+\] ClearAppletTransitionBuffer                                                   |
| 22  | \[4.0.0+\] AcquireLastApplicationCaptureSharedBuffer                                     |
| 23  | \[4.0.0+\] ReleaseLastApplicationCaptureSharedBuffer                                     |
| 24  | \[4.0.0+\] AcquireLastForegroundCaptureSharedBuffer                                      |
| 25  | \[4.0.0+\] ReleaseLastForegroundCaptureSharedBuffer                                      |
| 26  | \[4.0.0+\] AcquireCallerAppletCaptureSharedBuffer                                        |
| 27  | \[4.0.0+\] ReleaseCallerAppletCaptureSharedBuffer                                        |
| 28  | \[6.0.0+\] TakeScreenShotOfOwnLayerEx                                                    |

### AcquireLastApplicationCaptureBuffer

No input, returns an output handle.

### AcquireLastForegroundCaptureBuffer

No input, returns an output handle.

### AcquireCallerAppletCaptureBuffer

No input, returns an output handle.

## ISystemAppletControllerForDebug

| Cmd | Name                              | Notes                                                                             |
| --- | --------------------------------- | --------------------------------------------------------------------------------- |
| 1   | RequestLaunchApplicationForDebug  |                                                                                   |
| 2   | \[7.0.0+\] GetDebugStorageChannel | No input, returns an output [\#IStorageChannel](#IStorageChannel "wikilink").     |
| 3   | \[7.0.0+\] CreateStorageForDebug  | Takes a total of 8-bytes of input, returns an [\#IStorage](#IStorage "wikilink"). |

## IProcessWindingController

| Cmd | Name                                                                                   | Notes |
| --- | -------------------------------------------------------------------------------------- | ----- |
| 0   | [\#GetLaunchReason](#GetLaunchReason "wikilink")                                       |       |
| 11  | [\#OpenCallingLibraryApplet](#OpenCallingLibraryApplet "wikilink")                     |       |
| 21  | [\#PushContext](#PushContext "wikilink")                                               |       |
| 22  | [\#PopContext](#PopContext "wikilink")                                                 |       |
| 23  | CancelWindingReservation                                                               |       |
| 30  | WindAndDoReserved                                                                      |       |
| 40  | [\#ReserveToStartAndWaitAndUnwindThis](#ReserveToStartAndWaitAndUnwindThis "wikilink") |       |
| 41  | \[4.0.0+\] ReserveToStartAndWait                                                       |       |

### GetLaunchReason

No input. Returns an u32 AppletProcessLaunchReason.

Used by LibraryApplets.

### OpenCallingLibraryApplet

No input, returns an output
[\#ILibraryAppletAccessor](#ILibraryAppletAccessor "wikilink").

### PushContext

Takes an input [\#IStorage](#IStorage "wikilink"), no output.

### PopContext

No input, returns an output [\#IStorage](#IStorage "wikilink").

### ReserveToStartAndWaitAndUnwindThis

Takes an input
[\#ILibraryAppletAccessor](#ILibraryAppletAccessor "wikilink"), no
output.

## IDebugFunctions

| Cmd | Name                                                                          | Notes |
| --- | ----------------------------------------------------------------------------- | ----- |
| 0   | NotifyMessageToHomeMenuForDebug                                               |       |
| 1   | [\#OpenMainApplication](#OpenMainApplication "wikilink")                      |       |
| 10  | EmulateButtonEvent                                                            |       |
| 20  | InvalidateTransitionLayer                                                     |       |
| 30  | \[6.0.0+\] RequestLaunchApplicationWithUserAndArgumentForDebug                |       |
| 40  | \[6.0.0+\] GetAppletResourceUsageInfo                                         |       |
| 100 | \[7.0.0+\] [\#SetCpuBoostModeForApplet](#SetCpuBoostModeForApplet "wikilink") |       |

### OpenMainApplication

No input, returns an output
[\#IApplicationAccessor](#IApplicationAccessor "wikilink").

### SetCpuBoostModeForApplet

Takes an input u32 **CpuBoostMode** (only modes 0 and 1 are valid) and
passes it to
[SetCpuBoostMode](PPC%20services#apm:sys.md##apm:sys "wikilink").

## IStorage

| Cmd | Name                           | Notes                                                                                    |
| --- | ------------------------------ | ---------------------------------------------------------------------------------------- |
| 0   | Open                           | No input. Returns an [\#IStorageAccessor](#IStorageAccessor "wikilink").                 |
| 1   | \[2.0.0+\] OpenTransferStorage | No input. Returns an [\#ITransferStorageAccessor](#ITransferStorageAccessor "wikilink"). |

Open can only be used when the IStorage was created by
[\#CreateStorage](#CreateStorage "wikilink") or
[\#CreateTransferMemoryStorage](#CreateTransferMemoryStorage "wikilink").
OpenTransferStorage can only be used when the IStorage was created by
[\#CreateHandleStorage](#CreateHandleStorage "wikilink").

Only 1 \*Accessor session can be open for each IStorage at a time.

## IStorageAccessor

| Cmd | Name    | Notes                                             |
| --- | ------- | ------------------------------------------------- |
| 0   | GetSize | No input. Returns an s64.                         |
| 10  | Write   | Takes an input s64 and a type-0x21 input buffer.  |
| 11  | Read    | Takes an input s64 and a type-0x22 output buffer. |

## ITransferStorageAccessor

| Cmd | Name      | Notes                                       |
| --- | --------- | ------------------------------------------- |
| 0   | GetSize   | No input. Returns an output s64.            |
| 1   | GetHandle | No input. Returns an output s64 and handle. |

These commands return the data originally from
[\#CreateHandleStorage](#CreateHandleStorage "wikilink") input, both
return the same s64.

# appletOE

This is "nn::am::<service::IApplicationProxyService>".

| Cmd | Name                                                       | Notes |
| --- | ---------------------------------------------------------- | ----- |
| 0   | [\#OpenApplicationProxy](#OpenApplicationProxy "wikilink") |       |

This is used by all regular-applications, including
[flog](Flog.md "wikilink") and "Retail Interactive Display Menu". Only
one session can be open for this service at a time.

## OpenApplicationProxy

Returns an [\#IApplicationProxy](#IApplicationProxy "wikilink"). See
[\#appletAE](#appletAE "wikilink").

Takes a [reserved](IPC%20Marshalling.md "wikilink") input u64 (official
user-processes use hard-coded value 0), a PID, and a process copy-handle
(cur-proc handle alias).

On failure, official user-processes will retry using this command in a
loop while the retval is 0x19280, with svcSleepThread(10000000) being
called first.

# idle:sys

This is "nn::idle::detail::IPolicyManagerSystem"

| Cmd        | Name                  |
| ---------- | --------------------- |
| 0          | GetAutoPowerDownEvent |
| 1          | \[1.0.0-3.0.2\]       |
| \[7.0.0+\] |                       |
| 2          | \[1.0.0-3.0.2\]       |
| 3          | SetHandlingContext    |
| 4          | LoadAndApplySettings  |
| 5          | ReportUserIsActive    |

\[3.0.0+\] SetHandlingContext now takes an additional 0x10-bytes of
input.

# omm

This is "nn::omm::detail::IOperationModeManager"

Operation Mode Manager (OMM) is a service responsible for arbitrating
the operation changes between docked and handheld modes. Besides
[PTM\_services](PTM%20services.md "wikilink"), this is the only service
that interacts with the [Dock](Dock.md "wikilink") through
[usb:pd\*](USB%20services.md "wikilink").

| Cmd | Name                                                   | Notes                                           |
| --- | ------------------------------------------------------ | ----------------------------------------------- |
| 0   | GetOperationMode                                       |                                                 |
| 1   | GetOperationModeChangeEvent                            |                                                 |
| 2   | EnableAudioVisual                                      |                                                 |
| 3   | DisableAudioVisual                                     |                                                 |
| 4   | EnterSleepAndWait                                      |                                                 |
| 5   | GetCradleStatus                                        |                                                 |
| 6   | FadeInDisplay                                          |                                                 |
| 7   | FadeOutDisplay                                         |                                                 |
| 8   | \[2.0.0+\] GetCradleFwVersion                          |                                                 |
| 9   | \[2.0.0+\] NotifyCecSettingsChanged                    |                                                 |
| 10  | \[3.0.0+\] SetOperationModePolicy                      |                                                 |
| 11  | \[3.0.0+\] GetDefaultDisplayResolution                 |                                                 |
| 12  | \[3.0.0+\] GetDefaultDisplayResolutionChangeEvent      |                                                 |
| 13  | \[3.0.0+\] UpdateDefaultDisplayResolution              |                                                 |
| 14  | \[3.0.0+\] ShouldSleepOnBoot                           |                                                 |
| 15  | \[4.0.0+\] NotifyHdcpApplicationExecutionStarted       |                                                 |
| 16  | \[4.0.0+\] NotifyHdcpApplicationExecutionFinished      |                                                 |
| 17  | \[4.0.0+\] NotifyHdcpApplicationDrawingStarted         |                                                 |
| 18  | \[4.0.0+\] NotifyHdcpApplicationDrawingFinished        |                                                 |
| 19  | \[4.0.0+\] GetHdcpAuthenticationFailedEvent            |                                                 |
| 20  | \[4.0.0+\] GetHdcpAuthenticationFailedEmulationEnabled |                                                 |
| 21  | \[4.0.0+\] SetHdcpAuthenticationFailedEmulation        |                                                 |
| 22  | \[4.0.0+\] GetHdcpStateChangeEvent                     |                                                 |
| 23  | \[4.0.0+\] GetHdcpState                                |                                                 |
| 24  | \[5.0.0+\] ShowCardUpdateProcessing                    |                                                 |
| 25  | \[5.0.0+\] SetApplicationCecSettingsAndNotifyChanged   |                                                 |
| 26  | \[7.0.0+\]                                             | No input, returns a total of 4-bytes of output. |

# spsm

This is "nn::spsm::detail::IPowerStateInterface".

| Cmd | Name                                          |
| --- | --------------------------------------------- |
| 0   | GetState                                      |
| 1   | SleepSystemAndWaitAwake                       |
| 2   |                                               |
| 3   |                                               |
| 4   | GetNotificationMessageEventHandle             |
| 5   |                                               |
| 6   |                                               |
| 7   |                                               |
| 8   | AnalyzePerformanceLogForLastSleepWakeSequence |
| 9   | ChangeHomeButtonLongPressingTime              |
| 10  |                                               |
| 11  | \[1.0.0-3.0.2\]                               |

\[3.0.0+\] Cmd11 now takes a total of 8-bytes of input.

# tcap

This is "nn::tcap::server::IManager".

| Cmd | Name                                  |
| --- | ------------------------------------- |
| 0   | GetContinuousHighSkinTemperatureEvent |
| 1   | SetOperationMode                      |
| 2   | LoadAndApplySettings                  |

# caps:su

This is "nn::capsrv::sf::IScreenShotApplicationService".

This was added with [6.0.0](6.0.0.md "wikilink").

This can be used by applications to save screenshots.

| Cmd | Name                             | Notes                                                                                                                                  |
| --- | -------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| 32  | \[7.0.0+\] SetShimLibraryVersion | Takes a total of 0x10-bytes of input and a PID, no output.                                                                             |
| 201 | SaveScreenShot                   |                                                                                                                                        |
| 203 | SaveScreenShotEx0                |                                                                                                                                        |
| 205 | \[8.0.0+\] SaveScreenShotEx1     |                                                                                                                                        |
| 210 | SaveScreenShotEx2                | Takes a total of 0x50-bytes of input, a type-0x15 input buffer, and a type-0x45 input buffer. Returns a total of 0x20-bytes of output. |

**SetShimLibraryVersion** is a wrapper for
[caps:c](Capture%20services.md "wikilink") cmd33. Commands
**SaveScreenShot**, **SaveScreenShotEx0**, **SaveScreenShotEx1** and
**SaveScreenShotEx2** are wrappers for
[caps:sc](Display%20services.md "wikilink") cmd210.

## SaveScreenShot

Takes two input u32s, an u64 AppletResourceUserId, a PID, and a
type-0x45 input buffer. Returns a 0x20-byte struct
**ApplicationAlbumEntry**.

Official user-processes doesn't use this, instead
[\#SaveScreenShotEx0](#SaveScreenShotEx0 "wikilink") is used:
ScreenShotAttributeEx0 is all-zero except +0 is set to an input u32.

## SaveScreenShotEx0

Takes an input 0x40-byte struct **ScreenShotAttributeEx0**, an input
u32, an input u64 AppletResourceUserId, a PID, and a type-0x45 input
buffer. Returns a 0x20-byte struct **ApplicationAlbumEntry**.

# Library Applets

This section documents library applet launching.

Before starting the applet, [\#IStorages](#IStorage "wikilink") are
[created](#ILibraryAppletCreator "wikilink") and written, then passed to
[\#ILibraryAppletAccessor](#ILibraryAppletAccessor "wikilink")
PushInData. The [\#IStorage](#IStorage "wikilink") session is closed
afterwards. The first [\#IStorage](#IStorage "wikilink") is
[\#CommonArguments](#CommonArguments "wikilink"), followed by any
applet-specific [\#IStorages](#IStorage "wikilink").

Once the applet finishes running successfully,
[\#ILibraryAppletAccessor](#ILibraryAppletAccessor "wikilink")
PopOutData can be used to get the applet-specific
[\#IStorage](#IStorage "wikilink") containing the applet output data.

## CommonArguments

The first [IStorage](#CreateStorage "wikilink") passed to applets should
contain the common library applet arguments. This is populated by
`nn::la::CommonArgumentsWriter` and has the following format.

This struct is 0x20-bytes.

Official sw handles the first 8-bytes separately, which is a header.
With CommonArguments version 0x0, the header is 4-bytes, while starting
with version 0x1 it's 8-bytes.

| Offset | Size | Typical Value | Notes                                                                                      |
| ------ | ---- | ------------- | ------------------------------------------------------------------------------------------ |
| 0x0    | 4    | 1             | Common Arguments version                                                                   |
| 0x4    | 4    | 0x20          | Common Arguments size                                                                      |
| 0x8    | 4    |               | Library applet version (API version)                                                       |
| 0xC    | 4    | 0             | Theme color                                                                                |
| 0x10   | 1    | 0             | Play startup sound                                                                         |
| 0x18   | 8    | N/A           | System tick (see [svcGetSystemTick](SVC#svcGetSystemTick.md##svcGetSystemTick "wikilink")) |
|        |      |               |                                                                                            |

# Enums

### AppletId

See also [:Category:Library
Applets](:Category:Library%20Applets.md "wikilink").

| ID   | Title-id         | Description                                                                                                      |
| ---- | ---------------- | ---------------------------------------------------------------------------------------------------------------- |
| 0x01 |                  | Application. Not valid for use with LibraryApplets.                                                              |
| 0x02 | 010000000000100C | "overlayDisp"                                                                                                    |
| 0x03 | 0100000000001000 | "qlaunch"                                                                                                        |
| 0x04 | 0100000000001012 | "starter"                                                                                                        |
| 0x0A | 0100000000001001 | ["auth"](Auth%20Applet.md "wikilink")                                                                            |
| 0x0B | 0100000000001002 | "cabinet"                                                                                                        |
| 0x0C | 0100000000001003 | "controller"                                                                                                     |
| 0x0D | 0100000000001004 | "dataErase"                                                                                                      |
| 0x0E | 0100000000001005 | ["error"](Error%20Applet.md "wikilink")                                                                          |
| 0x0F | 0100000000001006 | "netConnect"                                                                                                     |
| 0x10 | 0100000000001007 | ["playerSelect"](Profile%20Selector.md "wikilink")                                                               |
| 0x11 | 0100000000001008 | ["swkbd"](Software%20Keyboard.md "wikilink")                                                                     |
| 0x12 | 0100000000001009 | "miiEdit"                                                                                                        |
| 0x13 | 010000000000100A | "LibAppletWeb" [WebApplet](Internet%20Browser#010000000000100A.md##010000000000100A "wikilink") applet           |
| 0x14 | 010000000000100B | "LibAppletShop" [ShopN](Internet%20Browser#ShopN.md##ShopN "wikilink") applet                                    |
| 0x15 | 010000000000100D | "photoViewer"                                                                                                    |
| 0x16 | 010000000000100E | "set"                                                                                                            |
| 0x17 | 010000000000100F | "LibAppletOff" [Offline](Internet%20Browser#Offline%20Applet.md##Offline_Applet "wikilink") applet               |
| 0x18 | 0100000000001010 | "LibAppletLns" [Whitelisted](Internet%20Browser#Whitelisted%20Applets.md##Whitelisted_Applets "wikilink") applet |
| 0x19 | 0100000000001011 | "LibAppletAuth" [WifiWebAuth](Internet%20Browser#WifiWebAuthApplet.md##WifiWebAuthApplet "wikilink") applet      |
| 0x1A | 0100000000001013 | "myPage"                                                                                                         |

### LibraryAppletMode

| ID  | Description                                                                                                                                                   |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0 | AllForeground                                                                                                                                                 |
| 0x1 | Background                                                                                                                                                    |
| 0x2 | No UI                                                                                                                                                         |
| 0x3 | Background with indirect display, see also [\#GetIndirectLayerConsumerHandle](#GetIndirectLayerConsumerHandle "wikilink"). Only used by swkbd InlineKeyboard. |
| 0x4 | AllForegroundInitiallyHidden. Can be used by \[7.0.0+\] [WebSession](Internet%20Browser.md "wikilink").                                                       |
|     |                                                                                                                                                               |

### NotificationMessage

| ID   | Description                                                                                  |
| ---- | -------------------------------------------------------------------------------------------- |
| 0x4  | Exit requested                                                                               |
| 0xF  | [FocusState](#GetCurrentFocusState "wikilink") changed                                       |
| 0x10 | Current applet execution was [resumed](#SetRestartMessageEnabled "wikilink").                |
| 0x1E | OperationMode changed                                                                        |
| 0x1F | PerformanceMode changed                                                                      |
| 0x5A | Capture button was [short-pressed](#SetRequiresCaptureButtonShortPressedMessage "wikilink"). |
| 0x5C | Screenshot was [taken](#SetAlbumImageTakenNotificationEnabled "wikilink").                   |

### OperationMode

| Value | Description |
| ----- | ----------- |
| 0     | Handheld    |
| 1     | Docked      |

### LaunchParameterKind

| Value | Description                          |
| ----- | ------------------------------------ |
| 1     | Application-specific LaunchParameter |
| 2     | account PreselectedUser              |
| 3     | Unknown if used by anything?         |

### LibraryAppletExitReason

| Value | Description |
| ----- | ----------- |
| 0     | Normal      |
| 1     | Canceled    |
| 2     | Abnormal    |
| 10    | Unexpected  |

### ProgramSpecifyKind

| Value | Description                                                                                                                                                           |
| ----- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0     | u8 ProgramIndex. "ExecuteProgram". User-process enters an infinite svcSleepThread loop afterwards.                                                                    |
| 1     | u64 titleID. "JumpToSubApplicationProgramForDevelopment". Only available when [DebugMode](Settings%20services#GetDebugModeFlag.md##GetDebugModeFlag "wikilink") is 1. |
| 2     | u64 = value 0. "RestartProgram"                                                                                                                                       |
|       |                                                                                                                                                                       |

This is "nn::am::<service::ProgramSpecifyKind>". This controls the type
of the u64 passed to [\#ExecuteProgram](#ExecuteProgram "wikilink").

# AppletResourceUserId

This u64 is officially called "nn::applet::AppletResourceUserId". Used
by a number of non-AM services.

# LibraryAppletInfo

This struct is 8-bytes: +0 u32 is [\#AppletId](#AppletId "wikilink"), +4
u32 is [\#LibraryAppletMode](#LibraryAppletMode "wikilink").

# AppletKind

This is 8-bytes.

# ApplicationAttributeForQuest

| Offset | Size | Description                                                                |
| ------ | ---- | -------------------------------------------------------------------------- |
| 0x0    | 0x4  | See [\#ApplicationAttribute](#ApplicationAttribute "wikilink").            |
| 0x4    | 0x4  | See [\#ApplicationAttribute](#ApplicationAttribute "wikilink").            |
| 0x8    | 0x4  | \[7.0.0+\] See [\#ApplicationAttribute](#ApplicationAttribute "wikilink"). |

This struct is "nn::applet::ApplicationAttributeForQuest".

User-processes copy the first 0x8-bytes (0xC-bytes with
[\#CreateApplicationWithAttributeAndPushAndRequestToStartForQuest](#CreateApplicationWithAttributeAndPushAndRequestToStartForQuest "wikilink")/[\#CreateApplicationWithAttributeAndRequestToStartForQuest](#CreateApplicationWithAttributeAndRequestToStartForQuest "wikilink"))
to a [\#ApplicationAttribute](#ApplicationAttribute "wikilink") with the
rest of the struct being cleared, which is then passed to the actual cmd
(CreateApplication\*ToStartForQuest).

# ApplicationAttribute

| Offset | Size | Description                                                                    |
| ------ | ---- | ------------------------------------------------------------------------------ |
| 0x0    | 0x4  | Default is 0 for non-Quest. Only used when non-zero: unknown value in seconds. |
| 0x4    | 0x4  | Default is 0 for non-Quest. Only used when non-zero: unknown value in seconds. |
| 0x8    | 0x4  | float audio volume. Must be in the range of 0.0f-1.0f. The default is 1.0f.    |
| 0xC    | 0x14 | Unused. Default is 0.                                                          |

This struct is "nn::am::ApplicationAttribute". This struct is
0x20-bytes.

Internally AM only uses the first 0xC-bytes from ApplicationAttribute,
regardless of the cmd.

# Notes

AM-sysmodule will only initialize
[pdm:ntfy](Shared%20Database%20services.md "wikilink") / use pdm:ntfy
service commands when the value from
[pm:bm](Process%20Manager%20services.md "wikilink") GetBootMode is not
0x1.

[Category:Services](Category:Services "wikilink")

See [here](HID%20Shared%20Memory.md "wikilink") for the HID
shared-memory.

# hid

This is
"nn::hid::IHidServer".

| Cmd  | Name                                                                                             |
| ---- | ------------------------------------------------------------------------------------------------ |
| 0    | [\#CreateAppletResource](#CreateAppletResource "wikilink")                                       |
| 1    | ActivateDebugPad                                                                                 |
| 11   | ActivateTouchScreen                                                                              |
| 21   | ActivateMouse                                                                                    |
| 31   | ActivateKeyboard                                                                                 |
| 40   | AcquireXpadIdEventHandle                                                                         |
| 41   | ReleaseXpadIdEventHandle                                                                         |
| 51   | ActivateXpad                                                                                     |
| 55   | GetXpadIds                                                                                       |
| 56   | ActivateJoyXpad                                                                                  |
| 58   | GetJoyXpadLifoHandle                                                                             |
| 59   | GetJoyXpadIds                                                                                    |
| 60   | ActivateSixAxisSensor                                                                            |
| 61   | DeactivateSixAxisSensor                                                                          |
| 62   | GetSixAxisSensorLifoHandle                                                                       |
| 63   | ActivateJoySixAxisSensor                                                                         |
| 64   | DeactivateJoySixAxisSensor                                                                       |
| 65   | GetJoySixAxisSensorLifoHandle                                                                    |
| 66   | StartSixAxisSensor                                                                               |
| 67   | StopSixAxisSensor                                                                                |
| 68   | IsSixAxisSensorFusionEnabled                                                                     |
| 69   | EnableSixAxisSensorFusion                                                                        |
| 70   | SetSixAxisSensorFusionParameters                                                                 |
| 71   | GetSixAxisSensorFusionParameters                                                                 |
| 72   | ResetSixAxisSensorFusionParameters                                                               |
| 73   | SetAccelerometerParameters                                                                       |
| 74   | GetAccelerometerParameters                                                                       |
| 75   | ResetAccelerometerParameters                                                                     |
| 76   | SetAccelerometerPlayMode                                                                         |
| 77   | GetAccelerometerPlayMode                                                                         |
| 78   | ResetAccelerometerPlayMode                                                                       |
| 79   | SetGyroscopeZeroDriftMode                                                                        |
| 80   | GetGyroscopeZeroDriftMode                                                                        |
| 81   | ResetGyroscopeZeroDriftMode                                                                      |
| 82   | IsSixAxisSensorAtRest                                                                            |
| 91   | ActivateGesture                                                                                  |
| 100  | SetSupportedNpadStyleSet                                                                         |
| 101  | GetSupportedNpadStyleSet                                                                         |
| 102  | SetSupportedNpadIdType                                                                           |
| 103  | ActivateNpad                                                                                     |
| 104  | DeactivateNpad                                                                                   |
| 106  | AcquireNpadStyleSetUpdateEventHandle                                                             |
| 107  | DisconnectNpad                                                                                   |
| 108  | GetPlayerLedPattern                                                                              |
| 120  | SetNpadJoyHoldType                                                                               |
| 121  | GetNpadJoyHoldType                                                                               |
| 122  | [\#SetNpadJoyAssignmentModeSingleByDefault](#SetNpadJoyAssignmentModeSingleByDefault "wikilink") |
| 123  | [\#SetNpadJoyAssignmentModeSingle](#SetNpadJoyAssignmentModeSingle "wikilink")                   |
| 124  | [\#SetNpadJoyAssignmentModeDual](#SetNpadJoyAssignmentModeDual "wikilink")                       |
| 125  | [\#MergeSingleJoyAsDualJoy](#MergeSingleJoyAsDualJoy "wikilink")                                 |
| 126  | StartLrAssignmentMode                                                                            |
| 127  | StopLrAssignmentMode                                                                             |
| 128  | SetNpadHandheldActivationMode                                                                    |
| 129  | [\#GetNpadHandheldActivationMode](#GetNpadHandheldActivationMode "wikilink")                     |
| 130  | SwapNpadAssignment                                                                               |
| 131  | IsUnintendedHomeButtonInputProtectionEnabled                                                     |
| 132  | EnableUnintendedHomeButtonInputProtection                                                        |
| 200  | [\#GetVibrationDeviceInfo](#GetVibrationDeviceInfo "wikilink")                                   |
| 201  | [\#SendVibrationValue](#SendVibrationValue "wikilink")                                           |
| 202  | [\#GetActualVibrationValue](#GetActualVibrationValue "wikilink")                                 |
| 203  | [\#CreateActiveVibrationDeviceList](#CreateActiveVibrationDeviceList "wikilink")                 |
| 204  | [\#PermitVibration](#PermitVibration "wikilink")                                                 |
| 205  | [\#IsVibrationPermitted](#IsVibrationPermitted "wikilink")                                       |
| 206  | [\#SendVibrationValues](#SendVibrationValues "wikilink")                                         |
| 300  | ActivateConsoleSixAxisSensor                                                                     |
| 301  | StartConsoleSixAxisSensor                                                                        |
| 302  | StopConsoleSixAxisSensor                                                                         |
| 400  | IsUsbFullKeyControllerEnabled                                                                    |
| 401  | EnableUsbFullKeyController                                                                       |
| 402  | IsUsbFullKeyControllerConnected                                                                  |
| 1000 | SetNpadCommunicationMode                                                                         |
| 1001 | GetNpadCommunicationMode                                                                         |

## CreateAppletResource

Takes a PID and an u64
[AppletResourceUserId](AM%20services.md "wikilink"). Returns an
[\#IAppletResource](#IAppletResource "wikilink").

## SetNpadJoyAssignmentModeSingleByDefault

Takes a PID-descriptor, an u32, and an
[AppletResourceUserId](AM%20services.md "wikilink"). No output.

## SetNpadJoyAssignmentModeSingle

Takes a PID-descriptor, an u32,
[AppletResourceUserId](AM%20services.md "wikilink"), and s64
**NpadJoyDeviceType**. No output.

## SetNpadJoyAssignmentModeDual

Takes a PID-descriptor, an u32, and an
[AppletResourceUserId](AM%20services.md "wikilink"). No output.

## MergeSingleJoyAsDualJoy

Takes a PID-descriptor, two u32s, and an
[AppletResourceUserId](AM%20services.md "wikilink"). No output.

## GetNpadHandheldActivationMode

Takes a PID and an u64
[AppletResourceUserId](AM%20services.md "wikilink"). Returns an output
u64. Official user-processes panic if the output u64 is not 0-2.

## GetVibrationDeviceInfo

Takes a [\#VibrationDeviceHandle](#VibrationDeviceHandle "wikilink").
Returns an output
[\#VibrationDeviceInfo](#VibrationDeviceInfo "wikilink").

## SendVibrationValue

Takes a PID-descriptor, a
[\#VibrationDeviceHandle](#VibrationDeviceHandle "wikilink"), a
[\#VibrationValue](#VibrationValue "wikilink") immediately after that,
and an u64 [AppletResourceUserId](AM%20services.md "wikilink"). No
output.

## GetActualVibrationValue

Takes a PID-descriptor, a
[\#VibrationDeviceHandle](#VibrationDeviceHandle "wikilink"), and an u64
[AppletResourceUserId](AM%20services.md "wikilink"). Returns an output
[\#VibrationValue](#VibrationValue "wikilink").

## CreateActiveVibrationDeviceList

No input. Returns an
[\#IActiveVibrationDeviceList](#IActiveVibrationDeviceList "wikilink").

## PermitVibration

Takes an input u8 bool. No output.

This affects the config displayed by System Settings.

## IsVibrationPermitted

No input. Returns an output u8 bool.

## SendVibrationValues

Takes an u64 [AppletResourceUserId](AM%20services.md "wikilink"), and
two type-0x9 input buffers containing an array of:
[\#VibrationDeviceHandle](#VibrationDeviceHandle "wikilink") for first
buffer, and [\#VibrationValue](#VibrationValue "wikilink") for the
second buffer.

Official sw uses the same entry-count for each array.

## VibrationDeviceHandle

This is an u32.

## VibrationDeviceInfo

This is a 0x8-byte struct.

## VibrationValue

This is a 0x10-byte struct.

## IAppletResource

| Cmd | Name                                                         |
| --- | ------------------------------------------------------------ |
| 0   | [\#GetSharedMemoryHandle](#GetSharedMemoryHandle "wikilink") |

### GetSharedMemoryHandle

No input. Returned a [sharedmem](HID%20Shared%20Memory.md "wikilink")
handle.

## IActiveVibrationDeviceList

This is
"nn::hid::IActiveVibrationDeviceList".

| Cmd | Name                                                             |
| --- | ---------------------------------------------------------------- |
| 0   | [\#ActivateVibrationDevice](#ActivateVibrationDevice "wikilink") |

### ActivateVibrationDevice

Takes an input
[\#VibrationDeviceHandle](#VibrationDeviceHandle "wikilink"). No output.

# hid:dbg

This is "nn::hid::IHidDebugServer".

| Cmd | Name                                  |
| --- | ------------------------------------- |
| 0   | DeactivateDebugPad                    |
| 1   | SetDebugPadAutoPilotState             |
| 2   | UnsetDebugPadAutoPilotState           |
| 10  | DeactivateTouchScreen                 |
| 11  | SetTouchScreenAutoPilotState          |
| 12  | UnsetTouchScreenAutoPilotState        |
| 20  | DeactivateMouse                       |
| 21  | SetMouseAutoPilotState                |
| 22  | UnsetMouseAutoPilotState              |
| 30  | DeactivateKeyboard                    |
| 31  | SetKeyboardAutoPilotState             |
| 32  | UnsetKeyboardAutoPilotState           |
| 50  | DeactivateXpad                        |
| 51  | SetXpadAutoPilotState                 |
| 52  | UnsetXpadAutoPilotState               |
| 60  | DeactivateJoyXpad                     |
| 91  | DeactivateGesture                     |
| 110 | DeactivateHomeButton                  |
| 111 | SetHomeButtonAutoPilotState           |
| 112 | UnsetHomeButtonAutoPilotState         |
| 120 | DeactivateSleepButton                 |
| 121 | SetSleepButtonAutoPilotState          |
| 122 | UnsetSleepButtonAutoPilotState        |
| 123 | DeactivateInputDetector               |
| 130 | DeactivateCaptureButton               |
| 131 | SetCaptureButtonAutoPilotState        |
| 132 | UnsetCaptureButtonAutoPilotState      |
| 133 | SetShiftAccelerometerCalibrationValue |
| 134 | GetShiftAccelerometerCalibrationValue |
| 135 | SetShiftGyroscopeCalibrationValue     |
| 136 | GetShiftGyroscopeCalibrationValue     |
| 140 | DeactivateConsoleSixAxisSensor        |
| 201 | ActivateFirmwareUpdate                |
| 202 | DeactivateFirmwareUpdate              |
| 203 | StartFirmwareUpdate                   |
| 204 | GetFirmwareUpdateStage                |
| 205 | GetFirmwareVersion                    |
| 206 | GetDestinationFirmwareVersion         |
| 207 | DiscardFirmwareInfoCacheForRevert     |
| 208 | StartFirmwareUpdateForRevert          |
| 209 | GetAvailableFirmwareVersionForRevert  |
| 211 | UpdateControllerColor                 |

# hid:sys

This is
"nn::hid::IHidSystemServer".

| Cmd  | Name                                                               |
| ---- | ------------------------------------------------------------------ |
| 31   | SendKeyboardLockKeyEvent                                           |
| 101  | AcquireHomeButtonEventHandle                                       |
| 111  | ActivateHomeButton                                                 |
| 121  | AcquireSleepButtonEventHandle                                      |
| 131  | ActivateSleepButton                                                |
| 141  | AcquireCaptureButtonEventHandle                                    |
| 151  | ActivateCaptureButton                                              |
| 210  | AcquireNfcDeviceUpdateEventHandle                                  |
| 211  | GetNpadsWithNfc                                                    |
| 212  | AcquireNfcActivateEventHandle                                      |
| 213  | ActivateNfc                                                        |
| 230  | AcquireIrSensorEventHandle                                         |
| 231  | ActivateIrSensor                                                   |
| 301  | ActivateNpadSystem                                                 |
| 303  | ApplyNpadSystemCommonPolicy                                        |
| 304  | EnableAssigningSingleOnSlSrPress                                   |
| 305  | DisableAssigningSingleOnSlSrPress                                  |
| 306  | GetLastActiveNpad                                                  |
| 307  | GetNpadSystemExtStyle                                              |
| 311  | SetNpadPlayerLedBlinkingDevice                                     |
| 321  | GetUniquePadsFromNpad                                              |
| 322  | GetIrSensorState                                                   |
| 323  | GetXcdHandleForNpadWithIrSensor                                    |
| 500  | SetAppletResourceUserId                                            |
| 501  | RegisterAppletResourceUserId                                       |
| 502  | UnregisterAppletResourceUserId                                     |
| 503  | EnableAppletToGetInput                                             |
| 504  | SetAruidValidForVibration                                          |
| 505  | EnableAppletToGetSixAxisSensor                                     |
| 510  | [\#SetVibrationMasterVolume](#SetVibrationMasterVolume "wikilink") |
| 511  | GetVibrationMasterVolume                                           |
| 512  | BeginPermitVibrationSession                                        |
| 513  | EndPermitVibrationSession                                          |
| 520  | EnableHandheldHids                                                 |
| 521  | DisableHandheldHids                                                |
| 540  | AcquirePlayReportControllerUsageUpdateEvent                        |
| 541  | GetPlayReportControllerUsages                                      |
| 542  | AcquirePlayReportRegisteredDeviceUpdateEvent                       |
| 543  | GetRegisteredDevices                                               |
| 544  | AcquireConnectionTriggerTimeoutEvent                               |
| 545  | SendConnectionTrigger                                              |
| 546  | AcquireDeviceRegisteredEventForControllerSupport                   |
| 547  | GetAllowedBluetoothLinksCount                                      |
| 700  | ActivateUniquePad                                                  |
| 702  | AcquireUniquePadConnectionEventHandle                              |
| 703  | GetUniquePadIds                                                    |
| 751  | AcquireJoyDetachOnBluetoothOffEventHandle                          |
| 800  | ListSixAxisSensorHandles                                           |
| 801  | IsSixAxisSensorUserCalibrationSupported                            |
| 802  | ResetSixAxisSensorCalibrationValues                                |
| 803  | StartSixAxisSensorUserCalibration                                  |
| 804  | CancelSixAxisSensorUserCalibration                                 |
| 805  | GetUniquePadBluetoothAddress                                       |
| 806  | DisconnectUniquePad                                                |
| 821  | StartAnalogStickManualCalibration                                  |
| 822  | RetryCurrentAnalogStickManualCalibrationStage                      |
| 823  | CancelAnalogStickManualCalibration                                 |
| 824  | ResetAnalogStickManualCalibration                                  |
| 850  | IsUsbFullKeyControllerEnabled                                      |
| 851  | EnableUsbFullKeyController                                         |
| 852  | IsUsbConnected                                                     |
| 900  | ActivateInputDetector                                              |
| 901  | NotifyInputDetector                                                |
| 1000 | InitializeFirmwareUpdate                                           |
| 1001 | GetFirmwareVersion                                                 |
| 1002 | GetAvailableFirmwareVersion                                        |
| 1003 | IsFirmwareUpdateAvailable                                          |
| 1004 | CheckFirmwareUpdateRequired                                        |
| 1005 | StartFirmwareUpdate                                                |
| 1006 | AbortFirmwareUpdate                                                |
| 1007 | GetFirmwareUpdateState                                             |

## SetVibrationMasterVolume

Takes an input 32bit float.

# irs

This is
"nn::irsensor::IIrSensorServer".

| Cmd | Name                                                                           |
| --- | ------------------------------------------------------------------------------ |
| 302 | [\#ActivateIrsensor](#ActivateIrsensor "wikilink")                             |
| 303 | [\#DeactivateIrsensor](#DeactivateIrsensor "wikilink")                         |
| 304 | [\#GetIrsensorSharedMemoryHandle](#GetIrsensorSharedMemoryHandle "wikilink")   |
| 305 | [\#StopImageProcessor](#StopImageProcessor "wikilink")                         |
| 306 | [\#RunMomentProcessor](#RunMomentProcessor "wikilink")                         |
| 307 | [\#RunClusteringProcessor](#RunClusteringProcessor "wikilink")                 |
| 308 | [\#RunImageTransferProcessor](#RunImageTransferProcessor "wikilink")           |
| 309 | [\#GetImageTransferProcessorState](#GetImageTransferProcessorState "wikilink") |
| 310 | [\#RunTeraPluginProcessor](#RunTeraPluginProcessor "wikilink")                 |
| 311 | [\#GetNpadIrCameraHandle](#GetNpadIrCameraHandle "wikilink")                   |
| 312 | [\#RunDpdProcessor](#RunDpdProcessor "wikilink")                               |
| 313 | [\#SuspendImageProcessor](#SuspendImageProcessor "wikilink")                   |
| 314 | \[3.0.0+\] [\#CheckFirmwareVersion](#CheckFirmwareVersion "wikilink")          |

## ActivateIrsensor

Takes a PID-descriptor and an
[AppletResourceUserId](AM%20services.md "wikilink"). No output.

## DeactivateIrsensor

Takes a PID-descriptor and an
[AppletResourceUserId](AM%20services.md "wikilink"). No output.

## GetIrsensorSharedMemoryHandle

Takes a PID-descriptor and an
[AppletResourceUserId](AM%20services.md "wikilink"). Returns a
SharedMemory handle.

The SharedMemory is mapped with permissions=read-only and size=0x8000.

## StopImageProcessor

Takes a PID-descriptor, an
[\#IrCameraHandle](#IrCameraHandle "wikilink"), and an
[AppletResourceUserId](AM%20services.md "wikilink"). No output.

## RunMomentProcessor

Takes a PID-descriptor, an
[\#IrCameraHandle](#IrCameraHandle "wikilink"), an
[AppletResourceUserId](AM%20services.md "wikilink"), and a
[\#PackedMomentProcessorConfig](#PackedMomentProcessorConfig "wikilink").
No output.

## RunClusteringProcessor

Takes a PID-descriptor, an
[\#IrCameraHandle](#IrCameraHandle "wikilink"), an
[AppletResourceUserId](AM%20services.md "wikilink"), and a
[\#PackedClusteringProcessorConfig](#PackedClusteringProcessorConfig "wikilink").
No output.

## RunImageTransferProcessor

Takes a PID-descriptor, an
[\#IrCameraHandle](#IrCameraHandle "wikilink"), an
[AppletResourceUserId](AM%20services.md "wikilink"), a
[\#PackedImageTransferProcessorConfig](#PackedImageTransferProcessorConfig "wikilink"),
an u64 for the TransferMemory\_size, and a TransferMemory handle. No
output.

Official sw creates the TransferMemory with an user-specified buffer and
permissions=0.

## GetImageTransferProcessorState

Takes a PID-descriptor, a type-0x6 output buffer, an
[\#IrCameraHandle](#IrCameraHandle "wikilink"), and an
[AppletResourceUserId](AM%20services.md "wikilink"). Returns an
[\#ImageTransferProcessorState](#ImageTransferProcessorState "wikilink").
No output.

## RunTeraPluginProcessor

Takes a PID-descriptor, an
[\#IrCameraHandle](#IrCameraHandle "wikilink"), a
[\#PackedTeraPluginProcessorConfig](#PackedTeraPluginProcessorConfig "wikilink")
(immediately after the previous word), and an
[AppletResourceUserId](AM%20services.md "wikilink"). No output.

## GetNpadIrCameraHandle

Takes an input u32. Returns an output
[\#IrCameraHandle](#IrCameraHandle "wikilink").

## RunDpdProcessor

Takes a PID-descriptor, an
[\#IrCameraHandle](#IrCameraHandle "wikilink"), a
[\#PackedDpdProcessorConfig](#PackedDpdProcessorConfig "wikilink")
(immediately after the previous word), and an
[AppletResourceUserId](AM%20services.md "wikilink"). No output.

## SuspendImageProcessor

Takes a PID-descriptor, an
[\#IrCameraHandle](#IrCameraHandle "wikilink"), and an
[AppletResourceUserId](AM%20services.md "wikilink"). No output.

## CheckFirmwareVersion

Takes a PID-descriptor, an
[\#IrCameraHandle](#IrCameraHandle "wikilink"), a
[\#PackedMcuVersion](#PackedMcuVersion "wikilink"), and an
[AppletResourceUserId](AM%20services.md "wikilink"). No output.

## IrCameraHandle

This is an u32.

## PackedMomentProcessorConfig

This is a 0x20-byte struct. This is converted from another structure by
the official
user-process.

| Offset | Size | Description            | DefaultConfig                  |
| ------ | ---- | ---------------------- | ------------------------------ |
| 0x0    | 0x8  | ?                      | 0x493E0                        |
| 0x8    | 0x1  | ?                      | 0x0                            |
| 0x9    | 0x1  | ?                      | 0x8                            |
| 0xA    | 0x1  | ?                      | 0x0                            |
| 0xB    | 0x5  | Padding                |                                |
| 0x10   | 0x8  | u16, u32, u16          | {Not written}, 0x1400000, 0xF0 |
| 0x18   | 0x4  | Hard-coded to 0xA0003. |                                |
| 0x1C   | 0x1  | ?                      | 0x1                            |
| 0x1D   | 0x1  | ?                      | 0x50                           |
| 0x1E   | 0x2  | Padding                |                                |

## PackedClusteringProcessorConfig

This is a 0x28-byte struct.

## PackedImageTransferProcessorConfig

This is a 0x18-byte struct. This is converted from another structure by
the official user-process. The conversion is the same as
PackedMomentProcessorConfig, except the code using out +0x1C/+0x1D was
removed, and the constant is now located at out+0x10. The code which
wrote to out u64 +0x10 from in+0x24 was replaced with code which writes
an u8 to out+0x14.

## ImageTransferProcessorState

This is a 0x10-byte struct.

## PackedTeraPluginProcessorConfig

This is an u64.

## PackedDpdProcessorConfig

This is a 0x10-byte struct.

## PackedMcuVersion

This is an u32.

# RomFS

The hid-sysmodule RomFS contains:

` ftmFwUpdate`  
`   ├── NTD_4CD_1801.fts256`  
`   └── NTD_4CD_2602.fts256`

These are firmware files for the touchscreen controller.

# Firmware update

Starting with [3.0.0](3.0.0.md "wikilink") HID-sysmodule now contains
strings for data stored in title
[0100000000000822](Title%20list.md "wikilink").

[Category:Services](Category:Services "wikilink")

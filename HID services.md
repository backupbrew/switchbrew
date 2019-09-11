See [here](HID%20Shared%20Memory.md "wikilink") for the HID
shared-memory.

# hid

This is "nn::hid::IHidServer".

| Cmd  | Name                                                                                                |
| ---- | --------------------------------------------------------------------------------------------------- |
| 0    | [\#CreateAppletResource](#CreateAppletResource "wikilink")                                          |
| 1    | ActivateDebugPad                                                                                    |
| 11   | ActivateTouchScreen                                                                                 |
| 21   | ActivateMouse                                                                                       |
| 31   | ActivateKeyboard                                                                                    |
| 32   | \[6.0.0+\] SendKeyboardLockKeyEvent                                                                 |
| 40   | AcquireXpadIdEventHandle                                                                            |
| 41   | ReleaseXpadIdEventHandle                                                                            |
| 51   | ActivateXpad                                                                                        |
| 55   | GetXpadIds                                                                                          |
| 56   | ActivateJoyXpad                                                                                     |
| 58   | GetJoyXpadLifoHandle                                                                                |
| 59   | GetJoyXpadIds                                                                                       |
| 60   | ActivateSixAxisSensor                                                                               |
| 61   | DeactivateSixAxisSensor                                                                             |
| 62   | GetSixAxisSensorLifoHandle                                                                          |
| 63   | ActivateJoySixAxisSensor                                                                            |
| 64   | DeactivateJoySixAxisSensor                                                                          |
| 65   | GetJoySixAxisSensorLifoHandle                                                                       |
| 66   | StartSixAxisSensor                                                                                  |
| 67   | StopSixAxisSensor                                                                                   |
| 68   | IsSixAxisSensorFusionEnabled                                                                        |
| 69   | EnableSixAxisSensorFusion                                                                           |
| 70   | SetSixAxisSensorFusionParameters                                                                    |
| 71   | GetSixAxisSensorFusionParameters                                                                    |
| 72   | ResetSixAxisSensorFusionParameters                                                                  |
| 73   | SetAccelerometerParameters                                                                          |
| 74   | GetAccelerometerParameters                                                                          |
| 75   | ResetAccelerometerParameters                                                                        |
| 76   | SetAccelerometerPlayMode                                                                            |
| 77   | GetAccelerometerPlayMode                                                                            |
| 78   | ResetAccelerometerPlayMode                                                                          |
| 79   | SetGyroscopeZeroDriftMode                                                                           |
| 80   | GetGyroscopeZeroDriftMode                                                                           |
| 81   | ResetGyroscopeZeroDriftMode                                                                         |
| 82   | IsSixAxisSensorAtRest                                                                               |
| 83   | \[6.0.0+\] IsFirmwareUpdateAvailableForSixAxisSensor                                                |
| 91   | ActivateGesture                                                                                     |
| 100  | [\#SetSupportedNpadStyleSet](#SetSupportedNpadStyleSet "wikilink")                                  |
| 101  | [\#GetSupportedNpadStyleSet](#GetSupportedNpadStyleSet "wikilink")                                  |
| 102  | [\#SetSupportedNpadIdType](#SetSupportedNpadIdType "wikilink")                                      |
| 103  | ActivateNpad                                                                                        |
| 104  | DeactivateNpad                                                                                      |
| 106  | [\#AcquireNpadStyleSetUpdateEventHandle](#AcquireNpadStyleSetUpdateEventHandle "wikilink")          |
| 107  | DisconnectNpad                                                                                      |
| 108  | GetPlayerLedPattern                                                                                 |
| 109  | \[5.0.0+\] ActivateNpadWithRevision                                                                 |
| 120  | SetNpadJoyHoldType                                                                                  |
| 121  | GetNpadJoyHoldType                                                                                  |
| 122  | [\#SetNpadJoyAssignmentModeSingleByDefault](#SetNpadJoyAssignmentModeSingleByDefault "wikilink")    |
| 123  | [\#SetNpadJoyAssignmentModeSingle](#SetNpadJoyAssignmentModeSingle "wikilink")                      |
| 124  | [\#SetNpadJoyAssignmentModeDual](#SetNpadJoyAssignmentModeDual "wikilink")                          |
| 125  | [\#MergeSingleJoyAsDualJoy](#MergeSingleJoyAsDualJoy "wikilink")                                    |
| 126  | StartLrAssignmentMode                                                                               |
| 127  | StopLrAssignmentMode                                                                                |
| 128  | SetNpadHandheldActivationMode                                                                       |
| 129  | [\#GetNpadHandheldActivationMode](#GetNpadHandheldActivationMode "wikilink")                        |
| 130  | SwapNpadAssignment                                                                                  |
| 131  | IsUnintendedHomeButtonInputProtectionEnabled                                                        |
| 132  | EnableUnintendedHomeButtonInputProtection                                                           |
| 133  | \[5.0.0+\] SetNpadJoyAssignmentModeSingleWithDestination                                            |
| 134  | \[6.1.0+\] SetNpadAnalogStickUseCenterClamp                                                         |
| 135  | \[8.0.0+\] SetNpadCaptureButtonAssignment                                                           |
| 136  | \[8.0.0+\] ClearNpadCaptureButtonAssignment                                                         |
| 200  | [\#GetVibrationDeviceInfo](#GetVibrationDeviceInfo "wikilink")                                      |
| 201  | [\#SendVibrationValue](#SendVibrationValue "wikilink")                                              |
| 202  | [\#GetActualVibrationValue](#GetActualVibrationValue "wikilink")                                    |
| 203  | [\#CreateActiveVibrationDeviceList](#CreateActiveVibrationDeviceList "wikilink")                    |
| 204  | [\#PermitVibration](#PermitVibration "wikilink")                                                    |
| 205  | [\#IsVibrationPermitted](#IsVibrationPermitted "wikilink")                                          |
| 206  | [\#SendVibrationValues](#SendVibrationValues "wikilink")                                            |
| 207  | \[4.0.0+\] SendVibrationGcErmCommand                                                                |
| 208  | \[4.0.0+\] GetActualVibrationGcErmCommand                                                           |
| 209  | \[4.0.0+\] BeginPermitVibrationSession                                                              |
| 210  | \[4.0.0+\] EndPermitVibrationSession                                                                |
| 211  | \[7.0.0+\] [\#IsVibrationDeviceMounted](#IsVibrationDeviceMounted "wikilink")                       |
| 300  | \[3.0.0+\] ActivateConsoleSixAxisSensor                                                             |
| 301  | \[3.0.0+\] StartConsoleSixAxisSensor                                                                |
| 302  | \[3.0.0+\] StopConsoleSixAxisSensor                                                                 |
| 303  | \[5.0.0+\] [\#ActivateSevenSixAxisSensor](#ActivateSevenSixAxisSensor "wikilink")                   |
| 304  | \[5.0.0+\] [\#StartSevenSixAxisSensor](#StartSevenSixAxisSensor "wikilink")                         |
| 305  | \[5.0.0+\] [\#StopSevenSixAxisSensor](#StopSevenSixAxisSensor "wikilink")                           |
| 306  | \[5.0.0+\] [\#InitializeSevenSixAxisSensor](#InitializeSevenSixAxisSensor "wikilink")               |
| 307  | \[5.0.0+\] [\#FinalizeSevenSixAxisSensor](#FinalizeSevenSixAxisSensor "wikilink")                   |
| 308  | \[5.0.0+\] [\#SetSevenSixAxisSensorFusionStrength](#SetSevenSixAxisSensorFusionStrength "wikilink") |
| 309  | \[5.0.0+\] [\#GetSevenSixAxisSensorFusionStrength](#GetSevenSixAxisSensorFusionStrength "wikilink") |
| 310  | \[6.0.0+\] [\#ResetSevenSixAxisSensorTimestamp](#ResetSevenSixAxisSensorTimestamp "wikilink")       |
| 400  | \[3.0.0+\] IsUsbFullKeyControllerEnabled                                                            |
| 401  | \[3.0.0+\] EnableUsbFullKeyController                                                               |
| 402  | \[3.0.0+\] IsUsbFullKeyControllerConnected                                                          |
| 403  | \[4.0.0+\] HasBattery                                                                               |
| 404  | \[4.0.0+\] HasLeftRightBattery                                                                      |
| 405  | \[4.0.0+\] GetNpadInterfaceType                                                                     |
| 406  | \[4.0.0+\] GetNpadLeftRightInterfaceType                                                            |
| 407  | \[9.0.0+\]                                                                                          |
| 408  | \[9.0.0+\]                                                                                          |
| 500  | \[5.0.0+\] GetPalmaConnectionHandle                                                                 |
| 501  | \[5.0.0+\] InitializePalma                                                                          |
| 502  | \[5.0.0+\] AcquirePalmaOperationCompleteEvent                                                       |
| 503  | \[5.0.0+\] GetPalmaOperationInfo                                                                    |
| 504  | \[5.0.0+\] PlayPalmaActivity                                                                        |
| 505  | \[5.0.0+\] SetPalmaFrModeType                                                                       |
| 506  | \[5.0.0+\] ReadPalmaStep                                                                            |
| 507  | \[5.0.0+\] EnablePalmaStep                                                                          |
| 508  | \[5.0.0+\] ResetPalmaStep                                                                           |
| 509  | \[5.0.0+\] ReadPalmaApplicationSection                                                              |
| 510  | \[5.0.0+\] WritePalmaApplicationSection                                                             |
| 511  | \[5.0.0+\] ReadPalmaUniqueCode                                                                      |
| 512  | \[5.0.0+\] SetPalmaUniqueCodeInvalid                                                                |
| 513  | \[5.0.0+\] WritePalmaActivityEntry                                                                  |
| 514  | \[5.0.0+\] WritePalmaRgbLedPatternEntry                                                             |
| 515  | \[5.0.0+\] WritePalmaWaveEntry                                                                      |
| 516  | \[5.0.0+\] SetPalmaDataBaseIdentificationVersion                                                    |
| 517  | \[5.0.0+\] GetPalmaDataBaseIdentificationVersion                                                    |
| 518  | \[5.0.0+\] SuspendPalmaFeature                                                                      |
| 519  | \[5.1.0+\] GetPalmaOperationResult                                                                  |
| 520  | \[5.1.0+\] ReadPalmaPlayLog                                                                         |
| 521  | \[5.1.0+\] ResetPalmaPlayLog                                                                        |
| 522  | \[5.1.0+\] SetIsPalmaAllConnectable                                                                 |
| 523  | \[5.1.0+\] SetIsPalmaPairedConnectable                                                              |
| 524  | \[5.1.0+\] PairPalma                                                                                |
| 525  | \[5.1.0+\] SetPalmaBoostMode                                                                        |
| 526  | \[7.0.0+\] CancelWritePalmaWaveEntry                                                                |
| 527  | \[8.0.0+\] EnablePalmaBoostMode                                                                     |
| 528  | \[8.0.0+\] GetPalmaBluetoothAddress                                                                 |
| 529  | \[8.0.0+\] SetDisallowedPalmaConnection                                                             |
| 1000 | SetNpadCommunicationMode                                                                            |
| 1001 | GetNpadCommunicationMode                                                                            |
| 1002 | \[9.0.0+\] SetTouchScreenConfiguration                                                              |
| 1003 | \[9.0.0+\] IsFirmwareUpdateNeededForNotification                                                    |

## CreateAppletResource

Takes a PID and an u64
[AppletResourceUserId](AM%20services.md "wikilink"). Returns an
[\#IAppletResource](#IAppletResource "wikilink").

## SetSupportedNpadStyleSet

Takes a PID-descriptor, an u32
[\#NpadStyleTag](#NpadStyleTag "wikilink"), and an u64
[AppletResourceUserId](AM%20services.md "wikilink"), no output.

## GetSupportedNpadStyleSet

Takes a PID-descriptor and an u64
[AppletResourceUserId](AM%20services.md "wikilink"), returns an u32
[\#NpadStyleTag](#NpadStyleTag "wikilink").

## SetSupportedNpadIdType

Takes a PID-descriptor, a type-0x9 input buffer, and an
[AppletResourceUserId](AM%20services.md "wikilink"). No output.

The input buffer contains an array of u32
[\#NpadIdType](#NpadIdType "wikilink").

## AcquireNpadStyleSetUpdateEventHandle

Takes an input u32, an u64
[AppletResourceUserId](AM%20services.md "wikilink"), and an u64. Returns
an output event handle, autoclear for this is user-specified.

The value for the last u64 doesn't seem to matter (?): official sw sets
this to the address of the structure used for storing the event which is
initialized after using this cmd.

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

## IsVibrationDeviceMounted

Takes a total of 0x10-bytes of input and a PID, returns an output u8
bool.

## ActivateSevenSixAxisSensor

Takes a PID and an u64
[AppletResourceUserId](AM%20services.md "wikilink"), no output.

## StartSevenSixAxisSensor

Takes a PID and an u64
[AppletResourceUserId](AM%20services.md "wikilink"), no output.

## StopSevenSixAxisSensor

Takes a PID and an u64
[AppletResourceUserId](AM%20services.md "wikilink"), no output.

## InitializeSevenSixAxisSensor

Takes a PID, an u64 [AppletResourceUserId](AM%20services.md "wikilink"),
two u64s for the size of each TransferMemory, and two TransferMemory
handles. No output.

The size of the first TransferMemory is 0x1000 with
MemoryPermission=read-only, while the second one has size 0x7F000 with
MemoryPermission=none.

## FinalizeSevenSixAxisSensor

Takes a PID and an u64
[AppletResourceUserId](AM%20services.md "wikilink"), no output.

## SetSevenSixAxisSensorFusionStrength

Takes a PID, a float, and an u64
[AppletResourceUserId](AM%20services.md "wikilink"), no output.

## GetSevenSixAxisSensorFusionStrength

Takes a PID and an u64
[AppletResourceUserId](AM%20services.md "wikilink"), returns an output
float.

## ResetSevenSixAxisSensorTimestamp

Takes a PID and an u64
[AppletResourceUserId](AM%20services.md "wikilink"), no output.

## VibrationDeviceHandle

This is an u32.

## VibrationDeviceInfo

This is a 0x8-byte struct.

## VibrationValue

This is a 0x10-byte struct, which contains 4 float values.

## IAppletResource

| Cmd | Name                                                         |
| --- | ------------------------------------------------------------ |
| 0   | [\#GetSharedMemoryHandle](#GetSharedMemoryHandle "wikilink") |

### GetSharedMemoryHandle

No input. Returned a [sharedmem](HID%20Shared%20Memory.md "wikilink")
handle.

## IActiveVibrationDeviceList

This is "nn::hid::IActiveVibrationDeviceList".

| Cmd | Name                                                             |
| --- | ---------------------------------------------------------------- |
| 0   | [\#ActivateVibrationDevice](#ActivateVibrationDevice "wikilink") |

### ActivateVibrationDevice

Takes an input
[\#VibrationDeviceHandle](#VibrationDeviceHandle "wikilink"). No output.

## NpadStyleTag

This is a bitfield describing which controller styles are supported.

| Bits  | Description      | Notes                                    |
| ----- | ---------------- | ---------------------------------------- |
| 0     | NpadFullKey      | Pro Controller.                          |
| 1     | NpadHandheld     | Joy-Con controller in handheld mode.     |
| 2     | NpadJoyDual      | Joy-Con controller in dual mode.         |
| 3     | NpadJoyLeft      | Joy-Con left controller in single mode.  |
| 4     | NpadJoyRight     | Joy-Con right controller in single mode. |
| 5     | NpadGc           | GameCube controller.                     |
| 6     | NpadPalma        | Poké Ball Plus controller.               |
| 7     | NpadLark         | NES/Famicom controller.                  |
| 8     | NpadHandheldLark | NES/Famicom controller in handheld mode. |
| 9     | NpadLucia        | Unknown.                                 |
| 10-28 | Reserved         |                                          |
| 29    | NpadSystemExt    | Generic external controller.             |
| 30    | NpadSystem       | Generic controller.                      |
| 31    | Reserved         |                                          |

## NpadIdType

This is an u32. This is the controller index used in
[sharedmem](HID%20Shared%20Memory#Controllers.md##Controllers "wikilink").
0x20 is handheld.

# hid:dbg

This is "nn::hid::IHidDebugServer".

| Cmd                     | Name                                                                                          |
| ----------------------- | --------------------------------------------------------------------------------------------- |
| 0                       | DeactivateDebugPad                                                                            |
| 1                       | SetDebugPadAutoPilotState                                                                     |
| 2                       | UnsetDebugPadAutoPilotState                                                                   |
| 10                      | DeactivateTouchScreen                                                                         |
| 11                      | SetTouchScreenAutoPilotState                                                                  |
| 12                      | UnsetTouchScreenAutoPilotState                                                                |
| 13                      | \[9.0.0+\] GetTouchScreenConfiguration                                                        |
| 20                      | DeactivateMouse                                                                               |
| 21                      | SetMouseAutoPilotState                                                                        |
| 22                      | UnsetMouseAutoPilotState                                                                      |
| 30                      | DeactivateKeyboard                                                                            |
| 31                      | SetKeyboardAutoPilotState                                                                     |
| 32                      | UnsetKeyboardAutoPilotState                                                                   |
| 50                      | DeactivateXpad                                                                                |
| 51                      | SetXpadAutoPilotState                                                                         |
| 52                      | UnsetXpadAutoPilotState                                                                       |
| 53 (\[1.0.0-8.1.0\] 60) | [\#DeactivateJoyXpad](#DeactivateJoyXpad "wikilink")                                          |
| 60                      | \[9.0.0+\] ClearNpadSystemCommonPolicy                                                        |
| 91                      | DeactivateGesture                                                                             |
| 110                     | DeactivateHomeButton                                                                          |
| 111                     | SetHomeButtonAutoPilotState                                                                   |
| 112                     | UnsetHomeButtonAutoPilotState                                                                 |
| 120                     | DeactivateSleepButton                                                                         |
| 121                     | SetSleepButtonAutoPilotState                                                                  |
| 122                     | UnsetSleepButtonAutoPilotState                                                                |
| 123                     | DeactivateInputDetector                                                                       |
| 130                     | DeactivateCaptureButton                                                                       |
| 131                     | SetCaptureButtonAutoPilotState                                                                |
| 132                     | UnsetCaptureButtonAutoPilotState                                                              |
| 133                     | \[3.0.0+\] SetShiftAccelerometerCalibrationValue                                              |
| 134                     | \[3.0.0+\] GetShiftAccelerometerCalibrationValue                                              |
| 135                     | \[3.0.0+\] SetShiftGyroscopeCalibrationValue                                                  |
| 136                     | \[3.0.0+\] GetShiftGyroscopeCalibrationValue                                                  |
| 140                     | \[3.0.0+\] DeactivateConsoleSixAxisSensor                                                     |
| 141                     | \[5.0.0+\] GetConsoleSixAxisSensorSamplingFrequency                                           |
| 142                     | \[5.0.0+\] DeactivateSevenSixAxisSensor                                                       |
| 143                     | \[5.0.0+\] GetConsoleSixAxisSensorCountStates                                                 |
| 144                     | \[8.0.0+\] GetAccelerometerFsr                                                                |
| 145                     | \[8.0.0+\] SetAccelerometerFsr                                                                |
| 146                     | \[8.0.0+\] GetAccelerometerOdr                                                                |
| 147                     | \[8.0.0+\] SetAccelerometerOdr                                                                |
| 148                     | \[8.0.0+\] GetGyroscopeFsr                                                                    |
| 149                     | \[8.0.0+\] SetGyroscopeFsr                                                                    |
| 150                     | \[8.0.0+\] GetGyroscopeOdr                                                                    |
| 151                     | \[8.0.0+\] SetGyroscopeOdr                                                                    |
| 201                     | ActivateFirmwareUpdate                                                                        |
| 202                     | DeactivateFirmwareUpdate                                                                      |
| 203                     | [\#StartFirmwareUpdate](#StartFirmwareUpdate "wikilink")                                      |
| 204                     | GetFirmwareUpdateStage                                                                        |
| 205                     | [\#GetFirmwareVersion](#GetFirmwareVersion "wikilink")                                        |
| 206                     | [\#GetDestinationFirmwareVersion](#GetDestinationFirmwareVersion "wikilink")                  |
| 207                     | [\#DiscardFirmwareInfoCacheForRevert](#DiscardFirmwareInfoCacheForRevert "wikilink")          |
| 208                     | \[3.0.0+\] StartFirmwareUpdateForRevert                                                       |
| 209                     | \[3.0.0+\] GetAvailableFirmwareVersionForRevert                                               |
| 210                     | \[4.0.0+\] IsFirmwareUpdatingDevice                                                           |
| 211                     | \[6.0.0+\] StartFirmwareUpdateIndividual                                                      |
| 215                     | \[6.0.0+\] SetUsbFirmwareForceUpdateEnabled                                                   |
| 216                     | \[6.0.0+\] SetAllKuinaDevicesToFirmwareUpdateMode                                             |
| 221                     | \[3.0.0+\] [\#UpdateControllerColor](#UpdateControllerColor "wikilink")                       |
| 222                     | \[4.0.0+\] ConnectUsbPadsAsync                                                                |
| 223                     | \[4.0.0+\] DisconnectUsbPadsAsync                                                             |
| 224                     | \[5.0.0+\] [\#UpdateDesignInfo](#UpdateDesignInfo "wikilink")                                 |
| 225                     | \[5.0.0+\] [\#GetUniquePadDriverState](#GetUniquePadDriverState "wikilink")                   |
| 226                     | \[5.0.0+\] GetSixAxisSensorDriverStates                                                       |
| 227                     | \[5.0.0+\] GetRxPacketHistory                                                                 |
| 228                     | \[6.0.0+\] AcquireOperationEventHandle                                                        |
| 229                     | \[6.0.0+\] [\#ReadSerialFlash](#ReadSerialFlash "wikilink")                                   |
| 230                     | \[6.0.0+\] WriteSerialFlash                                                                   |
| 231                     | \[6.0.0+\] GetOperationResult                                                                 |
| 232                     | \[6.0.0+\] EnableShipmentMode                                                                 |
| 233                     | \[6.0.0+\] ClearPairingInfo                                                                   |
| 234                     | \[6.0.0+\] GetUniquePadDeviceTypeSetInternal                                                  |
| 235                     | \[7.0.0+\] EnableAnalogStickPower                                                             |
| 236                     | \[9.0.0+\] RequestKuinaUartClockCal                                                           |
| 237                     | \[9.0.0+\] GetKuinaUartClockCal                                                               |
| 238                     | \[9.0.0+\] SetKuinaUartClockTrim                                                              |
| 239                     | \[9.0.0+\] KuinaLoopbackTest                                                                  |
| 240                     | \[9.0.0+\] RequestBatteryVoltage                                                              |
| 241                     | \[9.0.0+\] GetBatteryVoltage                                                                  |
| 242                     | \[9.0.0+\] GetUniquePadPowerInfo                                                              |
| 243                     | \[9.0.0+\] RebootUniquePad                                                                    |
| 244                     | \[9.0.0+\] RequestKuinaFirmwareVersion                                                        |
| 245                     | \[9.0.0+\] GetKuinaFirmwareVersion                                                            |
| 246                     | \[9.0.0+\] GetVidPid                                                                          |
| 301                     | \[5.0.0-8.1.0\] [\#GetAbstractedPadHandles](#GetAbstractedPadHandles "wikilink")              |
| 302                     | \[5.0.0-8.1.0\] [\#GetAbstractedPadState](#GetAbstractedPadState "wikilink")                  |
| 303                     | \[5.0.0-8.1.0\] [\#GetAbstractedPadsState](#GetAbstractedPadsState "wikilink")                |
| 321                     | \[5.0.0-8.1.0\] [\#SetAutoPilotVirtualPadState](#SetAutoPilotVirtualPadState "wikilink")      |
| 322                     | \[5.0.0-8.1.0\] [\#UnsetAutoPilotVirtualPadState](#UnsetAutoPilotVirtualPadState "wikilink")  |
| 323                     | \[5.0.0+\] [\#UnsetAllAutoPilotVirtualPadState](#UnsetAllAutoPilotVirtualPadState "wikilink") |
| 324                     | \[7.0.0+\] [\#AttachHdlsWorkBuffer](#AttachHdlsWorkBuffer "wikilink")                         |
| 325                     | \[7.0.0+\] [\#ReleaseHdlsWorkBuffer](#ReleaseHdlsWorkBuffer "wikilink")                       |
| 326                     | \[7.0.0+\] [\#DumpHdlsNpadAssignmentState](#DumpHdlsNpadAssignmentState "wikilink")           |
| 327                     | \[7.0.0+\] [\#DumpHdlsStates](#DumpHdlsStates "wikilink")                                     |
| 328                     | \[7.0.0+\] [\#ApplyHdlsNpadAssignmentState](#ApplyHdlsNpadAssignmentState "wikilink")         |
| 329                     | \[7.0.0+\] [\#ApplyHdlsStateList](#ApplyHdlsStateList "wikilink")                             |
| 330                     | \[7.0.0+\] [\#AttachHdlsVirtualDevice](#AttachHdlsVirtualDevice "wikilink")                   |
| 331                     | \[7.0.0+\] [\#DetachHdlsVirtualDevice](#DetachHdlsVirtualDevice "wikilink")                   |
| 332                     | \[7.0.0+\] [\#SetHdlsState](#SetHdlsState "wikilink")                                         |
| 350                     | \[5.0.0+\] AddRegisteredDevice                                                                |
| 400                     | \[6.0.0+\] DisableExternalMcuOnNxDevice                                                       |
| 401                     | \[6.0.0+\] DisableRailDeviceFiltering                                                         |
| 500                     | \[8.0.0+\] SetFactoryInt                                                                      |
| 501                     | \[8.0.0+\] IsFactoryBootEnabled                                                               |
| 550                     | \[9.0.0+\] SetAnalogStickModelDataTemporarily                                                 |
| 551                     | \[9.0.0+\] GetAnalogStickModelData                                                            |
| 552                     | \[9.0.0+\] ResetAnalogStickModelData                                                          |

## StartFirmwareUpdate

Takes a total of 0x20-bytes of input, 2 handles, and returns an output
handle.

\[3.0.0+\] Now takes a total of 8-bytes of input, and no longer uses any
input/output handles.

## GetFirmwareVersion

Takes a total of 8-bytes of input, and returns a total of 4-bytes of
output.

\[3.0.0+\] Now returns an additional 0xC-bytes of output.

## GetDestinationFirmwareVersion

Takes a total of 8-bytes of input, and returns a total of 4-bytes of
output.

\[3.0.0+\] Now returns an additional 0xC-bytes of output.

## DiscardFirmwareInfoCacheForRevert

Takes a total of 8-bytes of input, and returns a total of 5-bytes of
output.

\[3.0.0+\] No input/output.

## UpdateControllerColor

Takes two input u32s for the colors, an input u64 **UniquePadId**, and
no output.

A state flag must be clear, otherwise an error is thrown. Afterwards,
this flag is set.

Sends the spi-write subcommand to the specified controller, for writing
the [color data](Joy-Con#Colors.md##Colors "wikilink"). This writes to
offset 0x6050 size 0x6, where the first 3-bytes are from the first u32
and the remaining 3-bytes are from the second u32.

## UpdateDesignInfo

Takes 4 input u32s for the colors, an input u8, an input u64
**UniquePadId**, and no output.

A state flag must be clear (same as
[\#UpdateControllerColor](#UpdateControllerColor "wikilink")), otherwise
an error is thrown. Afterwards, this flag is set.

Sends the spi-write subcommand to the specified controller, for writing
to offset 0x6050 size 0xD. The first 3-bytes from each u32 is used for
the spi-write-data, with the u8 being copied immediately afterwards the
color data.

## GetUniquePadDriverState

Takes a total of 8-bytes of input, returns a total of 0x20-bytes of
output.

\[9.0.0+\] Now takes a total of 8-bytes of input, returns a total of
0x18-bytes of output.

## ReadSerialFlash

Takes an input TransferMemory handle, an input u32 offset, an input u64
size, and an u64 **UniquePadId**, no output.

Reads from the specified controller's spi-flash. The input size is the
original size without page-alignment. The TransferMemory permissions is
RW-.

This doesn't seem to be usable?

## GetAbstractedPadHandles

Takes a type-0xA output buffer containing an array of u64
**AbstractedPadHandle** and returns an output s32 for total entries.

Returns a handle for each controller detected by the system.

## GetAbstractedPadState

Takes an input u64 **AbstractedPadHandle**, returns an output
[\#AbstractedPadState](#AbstractedPadState "wikilink").

## GetAbstractedPadsState

Takes a type-0xA output buffer containing an array of u64
**AbstractedPadHandle**, a type-0x22 output buffer containing an array
of [\#AbstractedPadState](#AbstractedPadState "wikilink"), and returns
an output s32 for total entries.

## SetAutoPilotVirtualPadState

Takes an input s8 **AbstractedVirtualPadId** and an input
[\#AbstractedPadState](#AbstractedPadState "wikilink"), no output.

## UnsetAutoPilotVirtualPadState

Takes an input s8 **AbstractedVirtualPadId**, no output.

Clears AutoPilot state for the specified pad.

## UnsetAllAutoPilotVirtualPadState

No input/output.

Same as
[\#UnsetAutoPilotVirtualPadState](#UnsetAutoPilotVirtualPadState "wikilink")
except this clears state for every pad.

## AttachHdlsWorkBuffer

Takes an input TransferMemory handle and an u64 for the TransferMemory
size, no output.

Official user-processes use TransferMemory size=0x1000 and
permissions=RW.

This TransferMemory is used as input/output by the other Hdls commands.

Hdls is for virtual HID controllers.

## ReleaseHdlsWorkBuffer

No input/output.

## DumpHdlsNpadAssignmentState

No input/output.

After using this cmd, the output
[\#HdlsNpadAssignment](#HdlsNpadAssignment "wikilink") is located at
tmem+0.

## DumpHdlsStates

No input/output.

After using this cmd, the output
[\#HdlsStateList](#HdlsStateList "wikilink") struct is located at
tmem+0.

## ApplyHdlsNpadAssignmentState

Takes an input u8 bool, no output.

Prior to using this cmd, the input
[\#HdlsNpadAssignment](#HdlsNpadAssignment "wikilink") is written to
tmem+0 by the user-process.

## ApplyHdlsStateList

No input/output.

Prior to using this cmd, the input
[\#HdlsStateList](#HdlsStateList "wikilink") is written to tmem+0 by the
user-process.

The [\#HdlsState](#HdlsState "wikilink") will be applied for each
HdlsHandle. If a HdlsHandle is not found, code similar to
[\#AttachHdlsVirtualDevice](#AttachHdlsVirtualDevice "wikilink") will
run with the [\#HdlsDeviceInfo](#HdlsDeviceInfo "wikilink"), then it
will continue with applying state with the new device.

## AttachHdlsVirtualDevice

Takes an [\#HdlsDeviceInfo](#HdlsDeviceInfo "wikilink"), returns a
8-byte **HdlsHandle**.

## DetachHdlsVirtualDevice

Takes an input 8-byte **HdlsHandle**, no output.

## SetHdlsState

Takes an input [\#HdlsState](#HdlsState "wikilink") and an input 8-byte
**HdlsHandle**, no output.

## AbstractedPadState

| Offset | Size | Description                                                                                                                                                                                                                                                                        |
| ------ | ---- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x4  | Type, only 1 bit can be set. Converted to [\#HdlsDeviceInfo](#HdlsDeviceInfo "wikilink")::type internally by [\#SetAutoPilotVirtualPadState](#SetAutoPilotVirtualPadState "wikilink").                                                                                             |
| 0x4    | 0x1  | Flags. [\#SetAutoPilotVirtualPadState](#SetAutoPilotVirtualPadState "wikilink") only uses bit0: when clear it will skip using the rest of the input and run [\#UnsetAutoPilotVirtualPadState](#UnsetAutoPilotVirtualPadState "wikilink") internally.                               |
| 0x5    | 0x3  | Padding                                                                                                                                                                                                                                                                            |
| 0x8    | 0x4  | RGBA Single Body Color                                                                                                                                                                                                                                                             |
| 0xC    | 0x4  | RGBA Single Buttons Color                                                                                                                                                                                                                                                          |
| 0x10   | 0x1  | Type2. See [\#HiddbgHdlsDeviceInfo](#HiddbgHdlsDeviceInfo "wikilink")::type2.                                                                                                                                                                                                      |
| 0x11   | 0x3  | Padding                                                                                                                                                                                                                                                                            |
| 0x14   | 0x24 | [\#HdlsState](#HdlsState "wikilink"). Unknown if the last 4-bytes are included in this struct, [\#SetAutoPilotVirtualPadState](#SetAutoPilotVirtualPadState "wikilink")/[\#hiddbgGetAbstractedPadsState](#hiddbgGetAbstractedPadsState "wikilink") only uses the first 0x20-bytes. |
| 0x38   | 0x60 | Unused with [\#SetAutoPilotVirtualPadState](#SetAutoPilotVirtualPadState "wikilink")/[\#GetAbstractedPadsState](#GetAbstractedPadsState "wikilink").                                                                                                                               |

Normally the input state is merged with an existing controller selected
by Type. However in some cases (BIT(2-5) with type2\!=0x2 and BIT(31))
it's detected as a dedicated controller.

Type:

| Bits | [\#HdlsDeviceInfo](#HdlsDeviceInfo "wikilink")::type bits | Description | Notes                                             |
| ---- | --------------------------------------------------------- | ----------- | ------------------------------------------------- |
| 0    | 0                                                         |             |                                                   |
| 1    | 15                                                        |             | [\#DeviceType](#DeviceType "wikilink") |= BIT(1)  |
| 2    | 1                                                         |             |                                                   |
| 3    | 2                                                         |             |                                                   |
| 4    | 1                                                         |             |                                                   |
| 5    | 2                                                         |             |                                                   |
| 6    | 3                                                         |             |                                                   |
| 7    | 11                                                        |             | [\#DeviceType](#DeviceType "wikilink") |= BIT(11) |
| 8    | 12                                                        |             | [\#DeviceType](#DeviceType "wikilink") |= BIT(12) |
| 9    | 13                                                        |             | [\#DeviceType](#DeviceType "wikilink") |= BIT(13) |
| 10   | 14                                                        |             | [\#DeviceType](#DeviceType "wikilink") |= BIT(14) |
| 11   | 15                                                        |             | [\#DeviceType](#DeviceType "wikilink") |= BIT(11) |
| 12   | 12                                                        |             | [\#DeviceType](#DeviceType "wikilink") |= BIT(12) |
| 13   | 13                                                        |             | [\#DeviceType](#DeviceType "wikilink") |= BIT(13) |
| 14   | 14                                                        |             | [\#DeviceType](#DeviceType "wikilink") |= BIT(14) |
| 15   | 17                                                        |             |                                                   |
| 31   | 21                                                        |             | [\#DeviceType](#DeviceType "wikilink") = BIT(31)  |
|      |                                                           |             |                                                   |

The above "[\#DeviceType](#DeviceType "wikilink") |=" notes only apply
when type2 is 0x2.

## HdlsNpadAssignment

| Offset | Size              | Description                                                                |
| ------ | ----------------- | -------------------------------------------------------------------------- |
| 0x0    | 0x4               | s32 Total entries                                                          |
| 0x4    | 0x4               | Padding                                                                    |
| 0x8    | 0x200(0x20\*0x10) | Array of [\#HdlsNpadAssignmentEntry](#HdlsNpadAssignmentEntry "wikilink"). |

This is a 0x208-byte struct.

### HdlsNpadAssignmentEntry

| Offset | Size | Description |
| ------ | ---- | ----------- |
| 0x0    | 0x8  | HdlsHandle  |
| 0x8    | 0x4  | ?           |
| 0xC    | 0x4  | ?           |
| 0x10   | 0x8  | ?           |
| 0x18   | 0x1  | ?           |
| 0x19   | 0x7  | Padding     |

This is a 0x20-byte struct.

## HdlsStateList

| Offset | Size              | Description                                                      |
| ------ | ----------------- | ---------------------------------------------------------------- |
| 0x0    | 0x4               | s32 Total entries                                                |
| 0x4    | 0x4               | Padding                                                          |
| 0x8    | 0x400(0x40\*0x10) | Array of [\#HdlsStateListEntry](#HdlsStateListEntry "wikilink"). |

This is a 0x408-byte struct.

This contains a list of all controllers, including non-virtual
controllers.

### HdlsStateListEntry

| Offset | Size | Description                                                                                                                                              |
| ------ | ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x8  | HdlsHandle                                                                                                                                               |
| 0x8    | 0x10 | [\#HdlsDeviceInfo](#HdlsDeviceInfo "wikilink"). With [\#ApplyHdlsStateList](#ApplyHdlsStateList "wikilink") this is only used when creating new devices. |
| 0x18   | 0x24 | [\#HdlsState](#HdlsState "wikilink")                                                                                                                     |
| 0x3C   | 0x4  | Padding                                                                                                                                                  |

This is a 0x40-byte struct.

## HdlsDeviceInfo

| Offset | Size | Description                                                                                                                                                                                                                                                                                                                                                                                        |
| ------ | ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x4  | Only one bit can be set, see below.                                                                                                                                                                                                                                                                                                                                                                |
| 0x4    | 0x4  | RGBA Single Body Color                                                                                                                                                                                                                                                                                                                                                                             |
| 0x8    | 0x4  | RGBA Single Buttons Color                                                                                                                                                                                                                                                                                                                                                                          |
| 0xC    | 0x1  | Additional type field used with the above type field, if the value doesn't match one of the following a default is used. Type Pro-Controller: value 0x3 indicates that the controller is connected via USB. Type bit21: value 0x3 = unknown. When value is 0x2, state is merged with an existing controller (when the type value is compatible with this). Otherwise, it's a dedicated controller. |
| 0xD    | 0x3  | Padding                                                                                                                                                                                                                                                                                                                                                                                            |

This is a 0x10-byte struct.

Bits for the above type field:

| Bits  | Description | Notes                                                                                                                         |
| ----- | ----------- | ----------------------------------------------------------------------------------------------------------------------------- |
| 0-7   |             | BIT(N\*4+0) = Pro Controller, BIT(N\*4+1) = Joy-Con Left, BIT(N\*4+2) = Joy-Con Right, BIT(N\*4+3) = invalid. Where N is 0-1. |
| 8-10  |             | Pro Controller                                                                                                                |
| 11    |             | Famicom left controller                                                                                                       |
| 12    |             | Famicom right controller (with microphone)                                                                                    |
| 13    |             | NES left controller                                                                                                           |
| 14    |             | NES right controller                                                                                                          |
| 15-16 |             | Invalid                                                                                                                       |
| 17    |             | Generic external controller                                                                                                   |
| 18-20 |             | Invalid                                                                                                                       |
| 21-23 |             | Generic controller                                                                                                            |

## HdlsState

| Offset | Size          | Description                                                                                                                                |
| ------ | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| 0x0    | 0x1           | powerConnected for the main [PowerInfo](HID%20Shared%20Memory#Controllers.md##Controllers "wikilink").                                     |
| 0x1    | 0x1           | ORRed with powerConnected to set the value of the first byte for the controller [flags](HID%20Shared%20Memory#Flags.md##Flags "wikilink"). |
| 0x2    | 0x6           | Unknown                                                                                                                                    |
| 0x8    | 0x4           | batteryCharge for the main [PowerInfo](HID%20Shared%20Memory#Controllers.md##Controllers "wikilink").                                      |
| 0xC    | 0x4           | [Buttons](HID%20Shared%20Memory#Button%20State.md##Button_State "wikilink"). Bit18 = HOME and bit19 = Capture.                             |
| 0x10   | 0x10(4\*2\*2) | Joystick data, see [HID\_Shared\_Memory\#Controller\_State](HID%20Shared%20Memory#Controller%20State.md##Controller_State "wikilink").     |
| 0x20   | 0x1           | Unused for input. Set with output from [\#DumpHdlsStates](#DumpHdlsStates "wikilink") (zero in some cases).                                |
| 0x21   | 0x3           | Padding                                                                                                                                    |

This is a 0x24-byte struct.

# hid:sys

This is "nn::hid::IHidSystemServer".

| Cmd  | Name                                                                                      |
| ---- | ----------------------------------------------------------------------------------------- |
| 31   | SendKeyboardLockKeyEvent                                                                  |
| 101  | AcquireHomeButtonEventHandle                                                              |
| 111  | ActivateHomeButton                                                                        |
| 121  | AcquireSleepButtonEventHandle                                                             |
| 131  | ActivateSleepButton                                                                       |
| 141  | AcquireCaptureButtonEventHandle                                                           |
| 151  | ActivateCaptureButton                                                                     |
| 161  | \[7.0.0+\] GetPlatformConfig                                                              |
| 210  | AcquireNfcDeviceUpdateEventHandle                                                         |
| 211  | GetNpadsWithNfc                                                                           |
| 212  | AcquireNfcActivateEventHandle                                                             |
| 213  | ActivateNfc                                                                               |
| 214  | \[4.0.0+\] GetXcdHandleForNpadWithNfc                                                     |
| 215  | \[4.0.0+\] IsNfcActivated                                                                 |
| 230  | AcquireIrSensorEventHandle                                                                |
| 231  | ActivateIrSensor                                                                          |
| 301  | ActivateNpadSystem                                                                        |
| 303  | ApplyNpadSystemCommonPolicy                                                               |
| 304  | EnableAssigningSingleOnSlSrPress                                                          |
| 305  | DisableAssigningSingleOnSlSrPress                                                         |
| 306  | GetLastActiveNpad                                                                         |
| 307  | GetNpadSystemExtStyle                                                                     |
| 308  | \[5.0.0+\] ApplyNpadSystemCommonPolicyFull                                                |
| 309  | \[5.0.0+\] GetNpadFullKeyGripColor                                                        |
| 310  | \[6.0.0+\] [\#GetMaskedSupportedNpadStyleSet](#GetMaskedSupportedNpadStyleSet "wikilink") |
| 311  | SetNpadPlayerLedBlinkingDevice                                                            |
| 312  | \[6.0.0+\] SetSupportedNpadStyleSetAll                                                    |
| 313  | \[9.0.0+\] GetNpadCaptureButtonAssignment                                                 |
| 314  | \[9.0.0+\] GetAppletFooterUiType                                                          |
| 315  | \[9.0.0+\] GetAppletDetailedUiType                                                        |
| 321  | \[3.0.0+\] [\#GetUniquePadsFromNpad](#GetUniquePadsFromNpad "wikilink")                   |
| 322  | GetIrSensorState                                                                          |
| 323  | GetXcdHandleForNpadWithIrSensor                                                           |
| 500  | SetAppletResourceUserId                                                                   |
| 501  | RegisterAppletResourceUserId                                                              |
| 502  | UnregisterAppletResourceUserId                                                            |
| 503  | EnableAppletToGetInput                                                                    |
| 504  | SetAruidValidForVibration                                                                 |
| 505  | EnableAppletToGetSixAxisSensor                                                            |
| 510  | [\#SetVibrationMasterVolume](#SetVibrationMasterVolume "wikilink")                        |
| 511  | GetVibrationMasterVolume                                                                  |
| 512  | \[3.0.0+\] BeginPermitVibrationSession                                                    |
| 513  | \[3.0.0+\] EndPermitVibrationSession                                                      |
| 520  | EnableHandheldHids                                                                        |
| 521  | DisableHandheldHids                                                                       |
| 522  | \[9.0.0+\] SetJoyConRailEnabled                                                           |
| 523  | \[9.0.0+\] IsJoyConRailEnabled                                                            |
| 540  | AcquirePlayReportControllerUsageUpdateEvent                                               |
| 541  | GetPlayReportControllerUsages                                                             |
| 542  | AcquirePlayReportRegisteredDeviceUpdateEvent                                              |
| 543  | GetRegisteredDevicesOld (\[1.0.0-4.1.0\] GetRegisteredDevices)                            |
| 544  | \[3.0.0+\] AcquireConnectionTriggerTimeoutEvent                                           |
| 545  | \[3.0.0+\] SendConnectionTrigger                                                          |
| 546  | \[3.0.0+\] AcquireDeviceRegisteredEventForControllerSupport                               |
| 547  | \[3.0.0+\] GetAllowedBluetoothLinksCount                                                  |
| 548  | \[5.0.0+\] GetRegisteredDevices                                                           |
| 549  | \[6.0.0+\] GetConnectableRegisteredDevices                                                |
| 700  | ActivateUniquePad                                                                         |
| 702  | AcquireUniquePadConnectionEventHandle                                                     |
| 703  | [\#GetUniquePadIds](#GetUniquePadIds "wikilink")                                          |
| 751  | AcquireJoyDetachOnBluetoothOffEventHandle                                                 |
| 800  | ListSixAxisSensorHandles                                                                  |
| 801  | IsSixAxisSensorUserCalibrationSupported                                                   |
| 802  | ResetSixAxisSensorCalibrationValues                                                       |
| 803  | StartSixAxisSensorUserCalibration                                                         |
| 804  | CancelSixAxisSensorUserCalibration                                                        |
| 805  | \[3.0.0+\] GetUniquePadBluetoothAddress                                                   |
| 806  | \[3.0.0+\] DisconnectUniquePad                                                            |
| 807  | \[5.0.0+\] GetUniquePadType                                                               |
| 808  | \[5.0.0+\] GetUniquePadInterface                                                          |
| 809  | \[5.0.0+\] GetUniquePadSerialNumber                                                       |
| 810  | \[5.0.0+\] GetUniquePadControllerNumber                                                   |
| 811  | \[5.0.0+\] GetSixAxisSensorUserCalibrationStage                                           |
| 812  | \[8.0.0+\] GetConsoleUniqueSixAxisSensorHandle                                            |
| 821  | StartAnalogStickManualCalibration                                                         |
| 822  | RetryCurrentAnalogStickManualCalibrationStage                                             |
| 823  | CancelAnalogStickManualCalibration                                                        |
| 824  | ResetAnalogStickManualCalibration                                                         |
| 825  | \[5.0.0+\] GetAnalogStickState                                                            |
| 826  | \[5.0.0+\] GetAnalogStickManualCalibrationStage                                           |
| 827  | \[5.0.0+\] IsAnalogStickButtonPressed                                                     |
| 828  | \[5.0.0+\] IsAnalogStickInReleasePosition                                                 |
| 829  | \[5.0.0+\] IsAnalogStickInCircumference                                                   |
| 830  | \[7.0.0+\] [\#SetNotificationLedPattern](#SetNotificationLedPattern "wikilink")           |
| 831  | \[9.0.0+\] SetNotificationLedPatternWithTimeout                                           |
| 832  | \[9.0.0+\] PrepareHidsForNotificationWake                                                 |
| 850  | \[3.0.0+\] IsUsbFullKeyControllerEnabled                                                  |
| 851  | \[3.0.0+\] EnableUsbFullKeyController                                                     |
| 852  | \[3.0.0+\] IsUsbConnected                                                                 |
| 870  | \[5.1.0+\] IsHandheldButtonPressedOnConsoleMode                                           |
| 900  | ActivateInputDetector                                                                     |
| 901  | [\#NotifyInputDetector](#NotifyInputDetector "wikilink")                                  |
| 1000 | \[3.0.0+\] InitializeFirmwareUpdate                                                       |
| 1001 | \[3.0.0+\] GetFirmwareVersion                                                             |
| 1002 | \[3.0.0+\] GetAvailableFirmwareVersion                                                    |
| 1003 | \[3.0.0+\] IsFirmwareUpdateAvailable                                                      |
| 1004 | \[3.0.0+\] CheckFirmwareUpdateRequired                                                    |
| 1005 | \[3.0.0+\] StartFirmwareUpdate                                                            |
| 1006 | \[3.0.0+\] AbortFirmwareUpdate                                                            |
| 1007 | \[3.0.0+\] GetFirmwareUpdateState                                                         |
| 1008 | \[4.0.0+\] ActivateAudioControl                                                           |
| 1009 | \[4.0.0+\] AcquireAudioControlEventHandle                                                 |
| 1010 | \[4.0.0+\] GetAudioControlStates                                                          |
| 1011 | \[4.0.0+\] DeactivateAudioControl                                                         |
| 1050 | \[5.0.0+\] IsSixAxisSensorAccurateUserCalibrationSupported                                |
| 1051 | \[5.0.0+\] StartSixAxisSensorAccurateUserCalibration                                      |
| 1052 | \[5.0.0+\] CancelSixAxisSensorAccurateUserCalibration                                     |
| 1053 | \[5.0.0+\] GetSixAxisSensorAccurateUserCalibrationState                                   |
| 1100 | \[5.0.0+\] [\#GetHidbusSystemServiceObject](#GetHidbusSystemServiceObject "wikilink")     |
| 1120 | \[6.0.0+\] SetFirmwareHotfixUpdateSkipEnabled                                             |
| 1130 | \[6.0.0+\] InitializeUsbFirmwareUpdate                                                    |
| 1131 | \[6.0.0+\] FinalizeUsbFirmwareUpdate                                                      |
| 1132 | \[6.0.0+\] CheckUsbFirmwareUpdateRequired                                                 |
| 1133 | \[6.0.0+\] StartUsbFirmwareUpdate                                                         |
| 1134 | \[6.0.0+\] GetUsbFirmwareUpdateState                                                      |
| 1150 | \[8.0.0+\] SetTouchScreenMagnification                                                    |
| 1151 | \[9.0.0+\] GetTouchScreenFirmwareVersion                                                  |
| 1152 | \[9.0.0+\] SetTouchScreenDefaultConfiguration                                             |
| 1153 | \[9.0.0+\] GetTouchScreenDefaultConfiguration                                             |
| 1154 | \[9.0.0+\] IsFirmwareAvailableForNotification                                             |
| 1155 | \[9.0.0+\] SetForceHandheldStyleVibration                                                 |
| 1156 | \[9.0.0+\]                                                                                |

## GetMaskedSupportedNpadStyleSet

Takes an input u64 AppletResourceUserId, returns an output u32
[\#NpadStyleTag](#NpadStyleTag "wikilink").

Official sw uses the output from
[GetAppletResourceUserIdOfCallerApplet](Applet%20Manager%20services.md "wikilink")
with this.

## GetUniquePadsFromNpad

Takes an input u32 [\#NpadIdType](#NpadIdType "wikilink"), a type-0xA
output buffer, and returns an output u64 for total output entries.

The output buffer contains an array of u64 **UniquePadId**.

## SetVibrationMasterVolume

Takes an input 32bit float.

## GetUniquePadIds

Takes a type-0xA output buffer, and returns an output u64 for total
output entries.

The output buffer contains an array of u64 **UniquePadId**.

## NotifyInputDetector

Takes an input u32 bitmask InputSourceId, no output.

This is the only hid:sys command used by USB-sysmodule (with value
0x40).

## SetNotificationLedPattern

Takes an input
[\#NotificationLedPattern](#NotificationLedPattern "wikilink") and an
u64 **UniquePadId**, no output.

The specified controller must have a HOME button.

This sends subcommand 0x38 to the specified controller, for setting the
pattern for the HOME button notification LED. The input structure is
converted to the format used by this
[subcommand](https://github.com/dekuNukem/Nintendo_Switch_Reverse_Engineering/blob/master/bluetooth_hid_subcommands_notes.md#subcommand-0x38-set-home-light).

## GetHidbusSystemServiceObject

No input, returns an
[\#IHidbusSystemServer](#IHidbusSystemServer "wikilink").

## NotificationLedPattern

| Offset | Size | Subcommand argdata bytepos | Subcommand argdata nibble | Description                                                                                                                                                                                                                                      |
| ------ | ---- | -------------------------- | ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 0x0    | 0x1  | 0x0                        | Low                       | Mini Cycle Base Duration. Value 0x1-0xF: 12.5ms - 187.5ms. Value 0x0 = 0ms/OFF.                                                                                                                                                                  |
| 0x1    | 0x1  | 0x0                        | High                      | Number of Mini Cycles + 1. Value 0x0-0xF: 1 - 16 mini cycles.                                                                                                                                                                                    |
| 0x2    | 0x1  | 0x1                        | Low                       | Number of Full Cycles. Value 0x1-0xF: 1 - 15 full cycles. Value 0x0 is repeat forever, but if Mini Cycle Base Duration is set to 0x0, it does the 1st Mini Cycle with a 12.5ms base duration and then the LED stays on with LED Start Intensity. |
| 0x3    | 0x1  | 0x1                        | High                      | LED Start Intensity. Value 0x0-0xF: 0% - 100%. (In HW, 1 - 241 duty)                                                                                                                                                                             |
| 0x4    | 0x1  | 0x2                        | High                      | Mini Cycle 1 LED Intensity. Value 0x0-0xF: 0% - 100%. (In HW, 1 - 241 duty)                                                                                                                                                                      |
| 0x5    | 0x1  | 0x3                        | High                      | Fading Transition Steps to Mini Cycle 1 (Uses PWM). Value 0x0: Instant. Each step duration is based on Mini Cycle Step Duration Multiplier.                                                                                                      |
| 0x6    | 0x1  | 0x3                        | Low                       | Final Step Duration Multiplier of Mini Cycle 1. Value is a Multiplier of Mini Cycle Base Duration. Value 0x0: 12.5ms, 0x1 - xF: 1x - 15x.                                                                                                        |
| 0x7    | 0x1  |                            |                           | Unused                                                                                                                                                                                                                                           |
| 0x8    | 0x1  | 0x2                        | Low                       | Mini Cycle 2 LED Intensity.                                                                                                                                                                                                                      |
| 0x9    | 0x1  | 0x4                        | High                      | Fading Transition Steps to Mini Cycle 2 (see above).                                                                                                                                                                                             |
| 0xA    | 0x1  | 0x4                        | Low                       | Final Step Duration Multiplier of Mini Cycle 2 (see above).                                                                                                                                                                                      |
| 0xB    | 0x1  |                            |                           | Unused                                                                                                                                                                                                                                           |
| 0xC    | 0x1  | 0x5                        | High                      | Mini Cycle 3 LED Intensity.                                                                                                                                                                                                                      |
| 0xD    | 0x1  | 0x6                        | High                      | Fading Transition Steps to Mini Cycle 3 (see above).                                                                                                                                                                                             |
| 0xE    | 0x1  | 0x6                        | Low                       | Final Step Duration Multiplier of Mini Cycle 3 (see above).                                                                                                                                                                                      |
| 0xF    | 0x1  |                            |                           | Unused                                                                                                                                                                                                                                           |
| 0x10   | 0x1  | 0x5                        | Low                       | Mini Cycle 4 LED Intensity.                                                                                                                                                                                                                      |
| 0x11   | 0x1  | 0x7                        | High                      | Fading Transition Duration to Mini Cycle 4 (see above).                                                                                                                                                                                          |
| 0x12   | 0x1  | 0x7                        | Low                       | Final Step Duration Multiplier of Mini Cycle 4 (see above).                                                                                                                                                                                      |
| 0x13   | 0x1  |                            |                           | Unused                                                                                                                                                                                                                                           |
| 0x14   | 0x1  | 0x8                        | High                      | Mini Cycle 5 LED Intensity.                                                                                                                                                                                                                      |
| 0x15   | 0x1  | 0x9                        | High                      | Fading Transition Steps to Mini Cycle 5 (see above).                                                                                                                                                                                             |
| 0x16   | 0x1  | 0x9                        | Low                       | Final Step Duration Multiplier of Mini Cycle 5 (see above).                                                                                                                                                                                      |
| 0x17   | 0x1  |                            |                           | Unused                                                                                                                                                                                                                                           |
| 0x18   | 0x1  | 0x8                        | Low                       | Mini Cycle 6 LED Intensity.                                                                                                                                                                                                                      |
| 0x19   | 0x1  | 0xA                        | High                      | Fading Transition Steps to Mini Cycle 6 (see above).                                                                                                                                                                                             |
| 0x1A   | 0x1  | 0xA                        | Low                       | Final Step Duration Multiplier of Mini Cycle 6 (see above).                                                                                                                                                                                      |
| 0x1B   | 0x1  |                            |                           | Unused                                                                                                                                                                                                                                           |
| 0x1C   | 0x1  | 0xB                        | High                      | Mini Cycle 7 LED Intensity.                                                                                                                                                                                                                      |
| 0x1D   | 0x1  | 0xC                        | High                      | Fading Transition Steps to Mini Cycle 7 (see above).                                                                                                                                                                                             |
| 0x1E   | 0x1  | 0xC                        | Low                       | Final Step Duration Multiplier of Mini Cycle 7 (see above).                                                                                                                                                                                      |
| 0x1F   | 0x1  |                            |                           | Unused                                                                                                                                                                                                                                           |
| 0x20   | 0x1  | 0xB                        | Low                       | Mini Cycle 8 LED Intensity.                                                                                                                                                                                                                      |
| 0x21   | 0x1  | 0xD                        | Low                       | Fading Transition Steps to Mini Cycle 8 (see above).                                                                                                                                                                                             |
| 0x22   | 0x1  | 0xD                        | High                      | Final Step Duration Multiplier of Mini Cycle 8 (see above).                                                                                                                                                                                      |
| 0x23   | 0x1  |                            |                           | Unused                                                                                                                                                                                                                                           |
| 0x24   | 0x1  | 0xE                        | High                      | Mini Cycle 9 LED Intensity.                                                                                                                                                                                                                      |
| 0x25   | 0x1  | 0xF                        | High                      | Fading Transition Steps to Mini Cycle 9 (see above).                                                                                                                                                                                             |
| 0x26   | 0x1  | 0xF                        | Low                       | Final Step Duration Multiplier of Mini Cycle 9 (see above).                                                                                                                                                                                      |
| 0x27   | 0x1  |                            |                           | Unused                                                                                                                                                                                                                                           |
| 0x28   | 0x1  | 0xE                        | Low                       | Mini Cycle 10 LED Intensity.                                                                                                                                                                                                                     |
| 0x29   | 0x1  | 0x10                       | High                      | Fading Transition Steps to Mini Cycle 10 (see above).                                                                                                                                                                                            |
| 0x2A   | 0x1  | 0x10                       | Low                       | Final Step Duration Multiplier of Mini Cycle 10 (see above).                                                                                                                                                                                     |
| 0x2B   | 0x1  |                            |                           | Unused                                                                                                                                                                                                                                           |
| 0x2C   | 0x1  | 0x11                       | High                      | Mini Cycle 11 LED Intensity.                                                                                                                                                                                                                     |
| 0x2D   | 0x1  | 0x12                       | High                      | Fading Transition Steps to Mini Cycle 11 (see above).                                                                                                                                                                                            |
| 0x2E   | 0x1  | 0x12                       | Low                       | Final Step Duration Multiplier of Mini Cycle 11 (see above).                                                                                                                                                                                     |
| 0x2F   | 0x1  |                            |                           | Unused                                                                                                                                                                                                                                           |
| 0x30   | 0x1  | 0x11                       | Low                       | Mini Cycle 12 LED Intensity.                                                                                                                                                                                                                     |
| 0x31   | 0x1  | 0x13                       | High                      | Fading Transition Steps to Mini Cycle 12 (see above).                                                                                                                                                                                            |
| 0x32   | 0x1  | 0x13                       | Low                       | Final Step Duration Multiplier of Mini Cycle 12 (see above).                                                                                                                                                                                     |
| 0x33   | 0x1  |                            |                           | Unused                                                                                                                                                                                                                                           |
| 0x34   | 0x1  | 0x14                       | High                      | Mini Cycle 13 LED Intensity.                                                                                                                                                                                                                     |
| 0x35   | 0x1  | 0x15                       | High                      | Fading Transition Steps to Mini Cycle 13 (see above).                                                                                                                                                                                            |
| 0x36   | 0x1  | 0x15                       | Low                       | Final Step Duration Multiplier of Mini Cycle 13 (see above).                                                                                                                                                                                     |
| 0x37   | 0x1  |                            |                           | Unused                                                                                                                                                                                                                                           |
| 0x38   | 0x1  | 0x14                       | Low                       | Mini Cycle 14 LED Intensity.                                                                                                                                                                                                                     |
| 0x39   | 0x1  | 0x16                       | High                      | Fading Transition Steps to Mini Cycle 14 (see above).                                                                                                                                                                                            |
| 0x3A   | 0x1  | 0x16                       | Low                       | Final Step Duration Multiplier of Mini Cycle 14 (see above).                                                                                                                                                                                     |
| 0x3B   | 0x1  |                            |                           | Unused                                                                                                                                                                                                                                           |
| 0x3C   | 0x1  | 0x17                       | High                      | Mini Cycle 15 LED Intensity.                                                                                                                                                                                                                     |
| 0x3D   | 0x1  | 0x18                       | High                      | Fading Transition Steps to Mini Cycle 15 (see above).                                                                                                                                                                                            |
| 0x3E   | 0x1  | 0x18                       | Low                       | Final Step Duration Multiplier of Mini Cycle 15 (see above).                                                                                                                                                                                     |
| 0x3F   | 0x1  |                            |                           | Unused                                                                                                                                                                                                                                           |
| 0x40   | 0x1  | 0x17                       | Low                       | Mini Cycle 16 LED Intensity.                                                                                                                                                                                                                     |
| 0x41   | 0x1  | 0x19                       | High                      | Fading Transition Steps to Mini Cycle 16 (see above). (Unused in older Joy-Con / Pro-Con FW. Unknown for new.)                                                                                                                                   |
| 0x42   | 0x1  | 0x19                       | Low                       | Final Step Duration Multiplier of Mini Cycle 16 (see above). (Unused in older Joy-Con / Pro-Con FW. Unknown for new.)                                                                                                                            |
| 0x43   | 0x1  |                            |                           | Unused                                                                                                                                                                                                                                           |
| 0x44   | 0x1  | 0x1A                       | High                      | Unknown (Unused in older Joy-Con / Pro-Con FW. Unknown for new.)                                                                                                                                                                                 |
| 0x45   | 0x1  | 0x1A                       | Low                       | Unknown (Unused in older Joy-Con / Pro-Con FW. Unknown for new.)                                                                                                                                                                                 |
| 0x46   | 0x1  |                            |                           | Padding                                                                                                                                                                                                                                          |
| 0x47   | 0x1  |                            |                           | Padding                                                                                                                                                                                                                                          |
|        |      |                            |                           |                                                                                                                                                                                                                                                  |

This is "nn::hid::system::NotificationLedPattern".

This is a 0x48-byte struct.

The above descriptions in the table are based on the info from
[here](https://github.com/dekuNukem/Nintendo_Switch_Reverse_Engineering/blob/master/bluetooth_hid_subcommands_notes.md).

argdata in the subcommand is initialized as follows:
`((u8*)cmd_argdata)[pos] = u8_in[pos2] | u8_in[pos3]<<4;` Hence, 4bits
from pairs of 2-bytes of the input struct are combined to write to the
subcommand. Only the low 4bits of each used byte in the struct is used.
This is written to stack initially, then copied to the actual
cmd\_argdata (the data immediately following the subcommandID byte).
There's a total of 0x1B-bytes of cmd\_argdata initialized from this.

The layout of cmd\_argdata is as follows:

| Offset | Size | Description                                   |
| ------ | ---- | --------------------------------------------- |
| 0x0    | 0x1B | See above.                                    |
| 0x1B   | 0xB  | Cleared to zero.                              |
| 0x26   | 0x5  | Unused                                        |
| 0x2B   | 0x8  | Set to an input value, which is hard-coded 0. |
| 0x33   | 0x2  | Set to value 0.                               |
| 0x35   | 0x1  | Set to value 1.                               |

## DeviceType

This is a bitmask describing the controller device type.

| Bits  | Description     | Notes                                                  |
| ----- | --------------- | ------------------------------------------------------ |
| 0     | FullKey         | Pro Controller and Gc controller.                      |
| 1     |                 | Unknown                                                |
| 2     | HandheldLeft    | Joy-Con/Famicom/NES left controller in handheld mode.  |
| 3     | HandheldRight   | Joy-Con/Famicom/NES right controller in handheld mode. |
| 4     | JoyLeft         | Joy-Con left controller.                               |
| 5     | JoyRight        | Joy-Con right controller.                              |
| 6     | Palma           | Poké Ball Plus controller.                             |
| 7     | LarkLeft (HVC)  | Famicom left controller.                               |
| 8     | LarkRight (HVC) | Famicom right controller (with microphone).            |
| 9     | LarkLeft (NES)  | NES left controller.                                   |
| 10    | LarkRight (NES) | NES right controller.                                  |
| 11-14 |                 | Reserved                                               |
| 15    | SystemExt       | Generic external controller.                           |
| 16-30 |                 | Reserved                                               |
| 31    | System          | Generic controller.                                    |

## IHidbusSystemServer

This is "nn::hidbus::IHidbusSystemServer".

This was added with \[5.0.0+\].

| Cmd | Name |
| --- | ---- |
| 500 |      |
| 501 |      |
| 502 |      |

# hid:tmp

This is "nn::hid::IHidTemporaryServer".

This service was added with \[3.0.0+\], then removed with \[8.0.0+\].

| Cmd | Name                                     |
| --- | ---------------------------------------- |
| 0   | GetConsoleSixAxisSensorCalibrationValues |

# irs

This is "nn::irsensor::IIrSensorServer".

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
| 312 | [\#RunPointingProcessor](#RunPointingProcessor "wikilink")                     |
| 313 | [\#SuspendImageProcessor](#SuspendImageProcessor "wikilink")                   |
| 314 | \[3.0.0+\] [\#CheckFirmwareVersion](#CheckFirmwareVersion "wikilink")          |
| 315 | \[4.0.0+\] SetFunctionLevel                                                    |
| 316 | \[4.0.0+\] RunImageTransferExProcessor                                         |
| 317 | \[4.0.0+\] RunIrLedProcessor                                                   |
| 318 | \[4.0.0+\] StopImageProcessorAsync                                             |
| 319 | \[4.0.0+\] ActivateIrsensorWithFunctionLevel                                   |

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

Takes an input u32 NpadTypeId. Returns an output
[\#IrCameraHandle](#IrCameraHandle "wikilink").

## RunPointingProcessor

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
the official user-process.

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

# irs:sys

This is "nn::irsensor::IIrSensorSystemServer".

| Cmd | Name                           |
| --- | ------------------------------ |
| 500 | SetAppletResourceUserId        |
| 501 | RegisterAppletResourceUserId   |
| 502 | UnregisterAppletResourceUserId |
| 503 | EnableAppletToGetInput         |

# ahid:cd

This is "nn::ahid::IServerSession".

Used for USB HID devices.

This service no longer exists in \[9.0.0+\].

| Cmd               | Name            | Notes                                                                        |
| ----------------- | --------------- | ---------------------------------------------------------------------------- |
| 0                 | AcquireDevice   | Takes an input s32, no output.                                               |
| 1                 | ReleaseDevice   | Takes an input s32, no output.                                               |
| 2                 | GetCtrlSession  | Takes an input u32, returns an [\#ICtrlSession](#ICtrlSession "wikilink").   |
| 3                 | GetReadSession  | Takes an input u32, returns an [\#IReadSession](#IReadSession "wikilink").   |
| \[1.0.0-2.3.0\] 4 | GetWriteSession | Takes an input u32, returns an [\#IWriteSession](#IWriteSession "wikilink"). |

## ICtrlSession

This is "nn::ahid::ICtrlSession".

This no longer exists in \[9.0.0+\].

| Cmd | Name                   | Notes |
| --- | ---------------------- | ----- |
| 0   | GetString              |       |
| 1   | GetCodeBook            |       |
| 2   | GetReport              |       |
| 3   | SetReport              |       |
| 4   | GetIdle                |       |
| 5   | SetIdle                |       |
| 6   | GetProtocol            |       |
| 7   | SetProtocol            |       |
| 8   | GetDescriptor          |       |
| 9   | SetDescriptor          |       |
| 10  | GetStateChangeEvent    |       |
| 11  | SignalStateChangeEvent |       |
| 12  | \[3.0.0+\] Write       |       |

All of these use USB [CtrlXfer](USB%20services.md "wikilink"), except
for cmd10-11 which are event(?) related, and cmd1 which copies
0x4000-bytes from state to output.

## IReadSession

This is "nn::ahid::IReadSession".

This no longer exists in \[9.0.0+\].

| Cmd | Name | Notes |
| --- | ---- | ----- |
| 0   | Read |       |

Cmd0 uses [PostBufferAsync](USB%20services.md "wikilink") etc with the
INPUT endpoint. The size must be \<=0x1000. The actual transfer size is
returned in an output u64. The data is copied from the tmpbuf to the
output buffer using the actual-transfer-size.

\[3.0.0+\] Cmd0 now takes a total of 8-bytes of input.

## IWriteSession

This is "nn::ahid::IWriteSession".

This was removed with \[3.0.0+\].

| Cmd | Name  | Notes                                                                                                                  |
| --- | ----- | ---------------------------------------------------------------------------------------------------------------------- |
| 0   | Write | This is the inverse of [\#IReadSession](#IReadSession "wikilink") cmd0. Uses the OUTPUT endpoint with an input buffer. |

# ahid:hdr

This is "nn::ahid::hdr::ISession".

Used internally for USB HID devices.

This service no longer exists in \[9.0.0+\].

| Cmd | Name                       |
| --- | -------------------------- |
| 0   | GetDeviceEntries           |
| 1   | GetDeviceList              |
| 2   | GetDeviceParameters        |
| 3   | AttachDevice               |
| 4   | DetachDevice               |
| 5   | \[6.0.0+\] SetDeviceFilter |

# xcd:sys

This is "nn::xcd::detail::ISystemServer".

| Cmd | Name                              |
| --- | --------------------------------- |
| 0   | GetDataFormat                     |
| 1   | SetDataFormat                     |
| 2   | GetMcuState                       |
| 3   | SetMcuState                       |
| 4   | GetMcuVersionForNfc               |
| 5   | CheckNfcDevicePower               |
| 6   | \[5.0.0+\]                        |
| 10  | SetNfcEvent                       |
| 11  | GetNfcInfo                        |
| 12  | StartNfcDiscovery                 |
| 13  | StopNfcDiscovery                  |
| 14  | StartNtagRead                     |
| 15  | StartNtagWrite                    |
| 16  | SendNfcRawData                    |
| 17  | RegisterMifareKey                 |
| 18  | ClearMifareKey                    |
| 19  | StartMifareRead                   |
| 20  | StartMifareWrite                  |
| 101 | GetAwakeTriggerReasonForLeftRail  |
| 102 | GetAwakeTriggerReasonForRightRail |

\[5.0.0+\] SetDataFormat, SetMcuState, and ClearMifareKey: now takes a
total of 0xC-bytes of input instead of 0x10.

\[6.0.0+\]: The buffer type used by GetNfcInfo is now 0x32 instead of
0x1A.

# hidbus

This is "nn::hidbus::IHidbusServer".

This was added with \[5.0.0+\].

| Cmd                | Name                             |
| ------------------ | -------------------------------- |
| 1                  | GetBusHandle                     |
| 2                  | IsExternalDeviceConnected        |
| 3                  | Initialize                       |
| 4                  | Finalize                         |
| 5                  | EnableExternalDevice             |
| 6                  | GetExternalDeviceId              |
| 7                  | SendCommandAsync                 |
| 8                  | GetSendCommandAsynceResult       |
| 9                  | SetEventForSendCommandAsycResult |
| 10                 | GetSharedMemoryHandle            |
| 11                 | EnableJoyPollingReceiveMode      |
| 12                 | DisableJoyPollingReceiveMode     |
| \[5.0.0-6.2.0\] 13 | GetPollingData                   |
| 14                 | \[6.0.0+\] SetStatusManagerType  |

# RomFS

The hid-sysmodule RomFS contains:

` ftmFwUpdate`  
`   ├── NTD_4CD_1801.fts256`  
`   ├── NTD_4CD_2602.fts256`  
`   ├── NTD_4CD_3801.fts256`  
`   └── NTD_4CD_xxxx.fts256 [7.0.0+]`

These are firmware files for the touchscreen controller.

\[9.0.0+\] The hid-sysmodule RomFS now contains:

` ftmFwUpdate`  
`   ├── FTS_00120100.fts256`  
`   ├── FTS_32000001.fts256`  
`   ├── FTS_32000102.fts256`  
`   ├── FTS_32000302.fts256`  
`   └── FTS_32000402.fts256`

# Firmware update

HID-sysmodule mounts the contents of title
[0100000000000822](Title%20list.md "wikilink") as "systemData" or the
contents of title [010000000000B22B](Title%20list.md "wikilink") as
"systemDataD". Both titles contain the same files, but
[0100000000000822](Title%20list.md "wikilink") is used on retail units
while [010000000000B22B](Title%20list.md "wikilink") is used for
development.

These titles contain the following files:

  - **ExpectVersionInfo.csv** - List in the format
    "\[device\],\[type\],\[version\]" where "device" can be "JoyLeft",
    "JoyRight", "FullKey", "Palma" or "Handheld", "type" can be "BT",
    "MCU", "USB" or "SioH" and "version" is the hexadecimal
    representation of the firmware file's version.
  - **FirmwareInfo.csv** - List in the format
    "\[device\],\[type\],\[version\],\[file\]" where "device", "type"
    and "version" should match the values from "ExpectVersionInfo" and
    "file" is the name of the firmware file.
  - **ukyosakyo\_ep2\_ota.bin** - Left/Right Joy-Con BT firmware.
  - **raizo\_ep2\_ota.bin** - Pro Controller BT firmware.
  - **tera\_ota.bin** - Right Joy-Con MCU firmware.
  - **tera\_ota\_iap.bin** - Right Joy-Con MCU (IAP profile) firmware.
  - **tera\_fullkey\_ota.bin** - Pro Controller MCU firmware.
  - **tera\_fullkey\_ota\_iap.bin** - Pro Controller MCU (IAP profile)
    firmware.
  - \[6.0.0+\] **ProController.dfu** - Pro Controller USB firmware.
  - \[6.1.0+\] **PalmaFw.bin** - Poké Ball Plus BT firmware.
  - \[9.0.0+\] **ExpectVersionInfo-platform.hoag.csv** - Same as
    "ExpectVersionInfo.csv" but for the Switch Lite platform.
  - \[9.0.0+\] **FirmwareInfo-platform.hoag.csv** - Same as
    "FirmwareInfo.csv" but for the Switch Lite platform.
  - \[9.0.0+\] **sioh.bin** - Switch Lite Joy-Con firmware.
  - \[9.0.0+\] **sioh\_iap.bin** - Switch Lite Joy-Con (IAP profile)
    firmware.

[Category:Services](Category:Services "wikilink")

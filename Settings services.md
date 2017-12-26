# set

This is "nn::settings::ISettingsServer".

| Cmd | Name                                      |
| --- | ----------------------------------------- |
| 0   | GetLanguageCode                           |
| 1   | GetAvailableLanguageCodes                 |
| 2   | \[4.0.0+\] MakeLanguageCode               |
| 3   | GetAvailableLanguageCodeCount             |
| 4   | GetRegionCode                             |
| 5   | \[4.0.0+\] GetAvailableLanguageCodes2     |
| 6   | \[4.0.0+\] GetAvailableLanguageCodeCount2 |
| 7   | \[4.0.0+\] GetKeyCodeMap                  |

# set:fd

This is
"nn::settings::IFirmwareDebugSettingsServer".

| Cmd | Name                           | Notes                                                                          |
| --- | ------------------------------ | ------------------------------------------------------------------------------ |
| 2   | SetSettingsItemValue           |                                                                                |
| 3   | ResetSettingsItemValue         |                                                                                |
| 4   | CreateSettingsItemKeyIterator  | Returns an [\#ISettingsItemKeyIterator](#ISettingsItemKeyIterator "wikilink"). |
| 10  | \[4.0.0+\] ReadSettings        |                                                                                |
| 11  | \[4.0.0+\] ResetSettings       |                                                                                |
| 20  | \[4.0.0+\] SetWebInspectorFlag |                                                                                |
| 21  | \[4.0.0+\] SetAllowedSslHosts  |                                                                                |
| 22  | \[4.0.0+\] SetHostFsMountPoint |                                                                                |

## ISettingsItemKeyIterator

| Cmd | Name       |
| --- | ---------- |
| 0   | GoNext     |
| 1   | GetKeySize |
| 2   | GetKey     |

# set:cal

This is
"nn::settings::IFactorySettingsServer".

| Cmd | Name                                                                     |
| --- | ------------------------------------------------------------------------ |
| 0   | GetBluetoothBdAddress                                                    |
| 1   | GetConfigurationId1                                                      |
| 2   | GetAccelerometerOffset                                                   |
| 3   | GetAccelerometerScale                                                    |
| 4   | GetGyroscopeOffset                                                       |
| 5   | GetGyroscopeScale                                                        |
| 6   | GetWirelessLanMacAddress                                                 |
| 7   | GetWirelessLanCountryCodeCount                                           |
| 8   | GetWirelessLanCountryCodes                                               |
| 9   | GetSerialNumber                                                          |
| 10  | SetInitialSystemAppletProgramId                                          |
| 11  | SetOverlayDispProgramId                                                  |
| 12  | GetBatteryLot                                                            |
| 14  | [\#GetEciDeviceCertificate](#GetEciDeviceCertificate "wikilink")         |
| 15  | [\#GetEticketDeviceCertificate](#GetEticketDeviceCertificate "wikilink") |
| 16  | [\#GetSslKey](#GetSslKey "wikilink")                                     |
| 17  | [\#GetSslCertificate](#GetSslCertificate "wikilink")                     |
| 18  | [\#GetGameCardKey](#GetGameCardKey "wikilink")                           |
| 19  | [\#GetGameCardCertificate](#GetGameCardCertificate "wikilink")           |
| 20  | [\#GetEciDeviceKey](#GetEciDeviceKey "wikilink")                         |
| 21  | [\#GetEticketDeviceKey](#GetEticketDeviceKey "wikilink")                 |
| 22  | GetSpeakerParameter                                                      |
| 23  | \[4.0.0+\] GetLcdVendorId                                                |
|     |                                                                          |

Used for accessing data calibrated at the factory.

## GetEciDeviceCertificate

Takes a type-0x16 output buffer with fixed size 0x180.

Returns the device certificate (ECC signed). This is identical to 3DS
DeviceCert/CTCert besides the strings. NIM loads the DeviceId from this.

## GetEticketDeviceCertificate

Takes a type-0x16 output buffer with fixed size 0x240.

Returns the ETicket certificate (RSA signed).

## GetSslKey

Takes a type-0x16 output buffer with fixed size 0x134.

Returns the extended SSL key (0x130 bytes) from
[CAL0](Calibration#CAL0.md##CAL0 "wikilink"). If the extended key is not
programmed then it falls back to the normal SSL key (0x110 bytes).

Used by SSL-sysmodule, see [here](SSL%20services.md "wikilink").

## GetSslCertificate

Takes a type-0x16 output buffer with fixed size 0x804.

Returns a
[container](Settings%20services#setcal%20Container%20Structure.md##setcal_Container_Structure "wikilink")
with the plaintext SSL certificate.

Used by SSL-sysmodule, see [here](SSL%20services.md "wikilink").

## GetGameCardKey

Takes a type-0x16 output buffer with fixed size 0x134.

Returns the extended GameCard key (0x130 bytes) from
[CAL0](Calibration#CAL0.md##CAL0 "wikilink"). If the extended key is not
programmed then it falls back to the normal GameCard key (0x110 bytes).

## GetGameCardCertificate

Takes a type-0x16 output buffer with fixed size 0x404.

Returns a
[container](Settings%20services#setcal%20Container%20Structure.md##setcal_Container_Structure "wikilink")
with the GameCard certificate.

## GetEciDeviceKey

Returns the extended device ECC-B233 key (0x50 bytes) from
[CAL0](Calibration#CAL0.md##CAL0 "wikilink"). If the extended key is not
programmed then it falls back to the normal device ECC-B233 key (0x30
bytes).

## GetEticketDeviceKey

Takes a type-0x16 output buffer with fixed size 0x244.

Returns the extended ETicket RSA-2048 key (0x240 bytes) from
[CAL0](Calibration#CAL0.md##CAL0 "wikilink"). If the extended key is not
programmed then it falls back to the normal ETicket RSA-2048 key (0x220
bytes).

## setcal Container Structure

| Offset | Size         | Name                                           |
| ------ | ------------ | ---------------------------------------------- |
| 0x0    | 0x4          | Size (same size used for decryption if needed) |
| 0x4    | {above size} | Actual data starts here.                       |

This container is used for returning data with variable sizes.

# set:sys

This is
"nn::settings::ISystemSettingsServer".

| Cmd | Name                                                                                              |
| --- | ------------------------------------------------------------------------------------------------- |
| 0   | SetLanguageCode                                                                                   |
| 1   | SetNetworkSettings                                                                                |
| 2   | GetNetworkSettings                                                                                |
| 3   | [\#GetFirmwareVersion](#GetFirmwareVersion "wikilink")                                            |
| 4   | \[3.0.0+\] GetFirmwareVersion2                                                                    |
| 7   | GetLockScreenFlag                                                                                 |
| 8   | SetLockScreenFlag                                                                                 |
| 9   | GetBacklightSettings                                                                              |
| 10  | SetBacklightSettings                                                                              |
| 11  | SetBluetoothDevicesSettings                                                                       |
| 12  | GetBluetoothDevicesSettings                                                                       |
| 13  | GetExternalSteadyClockSourceId                                                                    |
| 14  | SetExternalSteadyClockSourceId                                                                    |
| 15  | GetUserSystemClockContext                                                                         |
| 16  | SetUserSystemClockContext                                                                         |
| 17  | GetAccountSettings                                                                                |
| 18  | SetAccountSettings                                                                                |
| 19  | GetAudioVolume                                                                                    |
| 20  | SetAudioVolume                                                                                    |
| 21  | GetEulaVersions                                                                                   |
| 22  | SetEulaVersions                                                                                   |
| 23  | GetColorSetId                                                                                     |
| 24  | SetColorSetId                                                                                     |
| 25  | GetConsoleInformationUploadFlag                                                                   |
| 26  | SetConsoleInformationUploadFlag                                                                   |
| 27  | GetAutomaticApplicationDownloadFlag                                                               |
| 28  | SetAutomaticApplicationDownloadFlag                                                               |
| 29  | GetNotificationSettings                                                                           |
| 30  | SetNotificationSettings                                                                           |
| 31  | GetAccountNotificationSettings                                                                    |
| 32  | SetAccountNotificationSettings                                                                    |
| 35  | GetVibrationMasterVolume                                                                          |
| 36  | SetVibrationMasterVolume                                                                          |
| 37  | GetSettingsItemValueSize                                                                          |
| 38  | [\#GetSettingsItemValue](#GetSettingsItemValue "wikilink")                                        |
| 39  | GetTvSettings                                                                                     |
| 40  | SetTvSettings                                                                                     |
| 41  | GetEdid                                                                                           |
| 42  | SetEdid                                                                                           |
| 43  | GetAudioOutputMode                                                                                |
| 44  | SetAudioOutputMode                                                                                |
| 45  | IsForceMuteOnHeadphoneRemoved                                                                     |
| 46  | SetForceMuteOnHeadphoneRemoved                                                                    |
| 47  | GetQuestFlag                                                                                      |
| 48  | SetQuestFlag                                                                                      |
| 49  | GetDataDeletionSettings                                                                           |
| 50  | SetDataDeletionSettings                                                                           |
| 51  | GetInitialSystemAppletProgramId                                                                   |
| 52  | GetOverlayDispProgramId                                                                           |
| 53  | GetDeviceTimeZoneLocationName                                                                     |
| 54  | SetDeviceTimeZoneLocationName                                                                     |
| 55  | GetWirelessCertificationFileSize                                                                  |
| 56  | [GetWirelessCertificationFile](Flash%20Filesystem#PRODINFOF.md##PRODINFOF "wikilink")             |
| 57  | SetRegionCode                                                                                     |
| 58  | GetNetworkSystemClockContext                                                                      |
| 59  | SetNetworkSystemClockContext                                                                      |
| 60  | IsUserSystemClockAutomaticCorrectionEnabled                                                       |
| 61  | SetUserSystemClockAutomaticCorrectionEnabled                                                      |
| 62  | [\#GetDebugModeFlag](#GetDebugModeFlag "wikilink")                                                |
| 63  | GetPrimaryAlbumStorage                                                                            |
| 64  | SetPrimaryAlbumStorage                                                                            |
| 65  | GetUsb30EnableFlag                                                                                |
| 66  | SetUsb30EnableFlag                                                                                |
| 67  | GetBatteryLot                                                                                     |
| 68  | [\#GetSerialNumber](#GetSerialNumber "wikilink")                                                  |
| 69  | GetNfcEnableFlag                                                                                  |
| 70  | SetNfcEnableFlag                                                                                  |
| 71  | GetSleepSettings                                                                                  |
| 72  | SetSleepSettings                                                                                  |
| 73  | GetWirelessLanEnableFlag                                                                          |
| 74  | SetWirelessLanEnableFlag                                                                          |
| 75  | GetInitialLaunchSettings                                                                          |
| 76  | SetInitialLaunchSettings                                                                          |
| 77  | GetDeviceNickName                                                                                 |
| 78  | SetDeviceNickName                                                                                 |
| 79  | GetProductModel                                                                                   |
| 80  | GetLdnChannel                                                                                     |
| 81  | SetLdnChannel                                                                                     |
| 82  | AcquireTelemetryDirtyFlagEventHandle                                                              |
| 83  | GetTelemetryDirtyFlags                                                                            |
| 84  | GetPtmBatteryLot                                                                                  |
| 85  | SetPtmBatteryLot                                                                                  |
| 86  | GetPtmFuelGaugeParameter                                                                          |
| 87  | SetPtmFuelGaugeParameter                                                                          |
| 88  | GetBluetoothEnableFlag                                                                            |
| 89  | SetBluetoothEnableFlag                                                                            |
| 90  | GetMiiAuthorId                                                                                    |
| 91  | SetShutdownRtcValue                                                                               |
| 92  | GetShutdownRtcValue                                                                               |
| 93  | AcquireFatalDirtyFlagEventHandle                                                                  |
| 94  | GetFatalDirtyFlags                                                                                |
| 95  | \[2.0.0+\] GetAutoUpdateEnableFlag                                                                |
| 96  | \[2.0.0+\] SetAutoUpdateEnableFlag                                                                |
| 97  | \[2.0.0+\] GetNxControllerSettings                                                                |
| 98  | \[2.0.0+\] SetNxControllerSettings                                                                |
| 99  | \[2.0.0+\] GetBatteryPercentageFlag                                                               |
| 100 | \[2.0.0+\] SetBatteryPercentageFlag                                                               |
| 101 | \[2.0.0+\] GetExternalRtcResetFlag                                                                |
| 102 | \[2.0.0+\] SetExternalRtcResetFlag                                                                |
| 103 | \[3.0.0+\] GetUsbFullKeyEnableFlag                                                                |
| 104 | \[3.0.0+\] SetUsbFullKeyEnableFlag                                                                |
| 105 | \[3.0.0+\] SetExternalSteadyClockInternalOffset                                                   |
| 106 | \[3.0.0+\] GetExternalSteadyClockInternalOffset                                                   |
| 107 | \[3.0.0+\] GetBacklightSettingsEx                                                                 |
| 108 | \[3.0.0+\] SetBacklightSettingsEx                                                                 |
| 109 | \[3.0.0+\] GetHeadphoneVolumeWarningCount                                                         |
| 110 | \[3.0.0+\] SetHeadphoneVolumeWarningCount                                                         |
| 111 | \[3.0.0+\] GetBluetoothAfhEnableFlag                                                              |
| 112 | \[3.0.0+\] SetBluetoothAfhEnableFlag                                                              |
| 113 | \[3.0.0+\] GetBluetoothBoostEnableFlag                                                            |
| 114 | \[3.0.0+\] SetBluetoothBoostEnableFlag                                                            |
| 115 | \[3.0.0+\] GetInRepairProcessEnableFlag                                                           |
| 116 | \[3.0.0+\] SetInRepairProcessEnableFlag                                                           |
| 117 | \[3.0.0+\] GetHeadphoneVolumeUpdateFlag                                                           |
| 118 | \[3.0.0+\] SetHeadphoneVolumeUpdateFlag                                                           |
| 119 | \[3.0.0+\] NeedsToUpdateHeadphoneVolume                                                           |
| 120 | \[3.0.0+\] GetPushNotificationActivityModeOnSleep                                                 |
| 121 | \[3.0.0+\] SetPushNotificationActivityModeOnSleep                                                 |
| 122 | \[4.0.0+\] [\#GetServiceDiscoveryControlSettings](#GetServiceDiscoveryControlSettings "wikilink") |
| 123 | \[4.0.0+\] SetServiceDiscoveryControlSettings                                                     |
| 124 | \[4.0.0+\] GetErrorReportSharePermission                                                          |
| 125 | \[4.0.0+\] SetErrorReportSharePermission                                                          |
| 126 | \[4.0.0+\] GetAppletLaunchFlags                                                                   |
| 127 | \[4.0.0+\] SetAppletLaunchFlags                                                                   |
| 128 | \[4.0.0+\] GetConsoleSixAxisSensorAccelerationBias                                                |
| 129 | \[4.0.0+\] SetConsoleSixAxisSensorAccelerationBias                                                |
| 130 | \[4.0.0+\] GetConsoleSixAxisSensorAngularVelocityBias                                             |
| 131 | \[4.0.0+\] SetConsoleSixAxisSensorAngularVelocityBias                                             |
| 132 | \[4.0.0+\] GetConsoleSixAxisSensorAccelerationGain                                                |
| 133 | \[4.0.0+\] SetConsoleSixAxisSensorAccelerationGain                                                |
| 134 | \[4.0.0+\] GetConsoleSixAxisSensorAngularVelocityGain                                             |
| 135 | \[4.0.0+\] SetConsoleSixAxisSensorAngularVelocityGain                                             |
| 136 | \[4.0.0+\] GetKeyboardLayout                                                                      |
| 137 | \[4.0.0+\] SetKeyboardLayout                                                                      |
| 138 | \[4.0.0+\] GetWebInspectorFlag                                                                    |
| 139 | \[4.0.0+\] GetAllowedSslHosts                                                                     |
| 140 | \[4.0.0+\] GetHostFsMountPoint                                                                    |

Official user-processes get a new service session handle each time a
set:sys cmd is used, with the session being closed aftewards.

## GetFirmwareVersion

Takes a type-0x1A output buffer. User-processes use hard-coded size
0x100.

If needed, reads the content of the
[System\_Version\_Title](System%20Version%20Title.md "wikilink") "/file"
into state. This is only done once.

Then the above 0x100-byte data is copied to the output buffer.

## GetSettingsItemValue

Takes two type-0x19 input buffers and a type-0x6 output buffer. Returns
an output u64 for the actual size written to the outbuf.

The outbuf\_size is compared with the config\_size. When config\_size is
larger than outbuf\_size, outbuf\_size is used for the memcpy, otherwise
config\_size is used. Afterwards the size used for the memcpy is written
to output(see above).

If loading from main config fails, it will also attempt to load config
from various state if the input strings match hard-coded strings.

## GetDebugModeFlag

Returns an output u8.

Loads the 1-byte config for \<"settings\_debug",
"is\_debug\_mode\_enabled"\>. If that fails, value 0x1 is written to
output. This uses the same func as ReadSetting internally.

Returned retval is always 0.

## GetSerialNumber

Returns the 0x18-byte SerialNumber string.

## GetServiceDiscoveryControlSettings

Returns 0x01 if [safemode](Safemode.md "wikilink") needs to be launched.

[Category:Services](Category:Services "wikilink")

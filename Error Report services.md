# erpt:c

This is "nn::erpt::sf::IContext".

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |
| 3   |      |
| 4   |      |
| 5   |      |

# erpt:r

This is "nn::erpt::sf::ISession".

| Cmd | Name        |
| --- | ----------- |
| 0   | OpenManager |
| 1   | OpenReport  |

## IManager

This is "nn::erpt::sf::IManager".

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |

## IReport

This is "nn::erpt::sf::IReport".

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |
| 3   |      |
| 4   |      |
| 5   |      |

# Reports

## Fields

| Name                                 | Format  | Description                                                           |
| ------------------------------------ | ------- | --------------------------------------------------------------------- |
| TestU64                              |         |                                                                       |
| TestU32                              |         |                                                                       |
| TestI64                              |         |                                                                       |
| TestI32                              |         |                                                                       |
| TestString                           |         |                                                                       |
| TestU8Array                          |         |                                                                       |
| TestU32Array                         |         |                                                                       |
| TestU64Array                         |         |                                                                       |
| TestI32Array                         |         |                                                                       |
| TestI64Array                         |         |                                                                       |
| ErrorCode                            |         |                                                                       |
| ErrorDescription                     |         |                                                                       |
| OccurrenceTimestamp                  | Integer | UTC unix timestamp from [user-time](PCV%20services.md "wikilink").    |
| ReportIdentifier                     |         |                                                                       |
| ConnectionStatus                     |         |                                                                       |
| AccessPointSSID                      |         |                                                                       |
| AccessPointSecurityType              |         |                                                                       |
| RadioStrength                        |         |                                                                       |
| NXMacAddress                         |         |                                                                       |
| IPAddressAcquisitionMethod           |         |                                                                       |
| CurrentIPAddress                     |         |                                                                       |
| SubnetMask                           |         |                                                                       |
| GatewayIPAddress                     |         |                                                                       |
| DNSType                              |         |                                                                       |
| PriorityDNSIPAddress                 |         |                                                                       |
| AlternateDNSIPAddress                |         |                                                                       |
| UseProxyFlag                         |         |                                                                       |
| ProxyIPAddress                       |         |                                                                       |
| ProxyPort                            |         |                                                                       |
| ProxyAutoAuthenticateFlag            |         |                                                                       |
| MTU                                  |         |                                                                       |
| ConnectAutomaticallyFlag             |         |                                                                       |
| UseStealthNetworkFlag                |         |                                                                       |
| LimitHighCapacityFlag                |         |                                                                       |
| NATType                              |         |                                                                       |
| WirelessAPMacAddress                 |         |                                                                       |
| GlobalIPAddress                      |         |                                                                       |
| EnableWirelessInterfaceFlag          |         |                                                                       |
| EnableWifiFlag                       |         |                                                                       |
| EnableBluetoothFlag                  |         |                                                                       |
| EnableNFCFlag                        |         |                                                                       |
| NintendoZoneSSIDListVersion          |         |                                                                       |
| LANAdapterMacAddress                 |         |                                                                       |
| ApplicationID                        |         |                                                                       |
| ApplicationTitle                     |         |                                                                       |
| ApplicationVersion                   |         |                                                                       |
| ApplicationStorageLocation           |         |                                                                       |
| DownloadContentType                  |         |                                                                       |
| InstallContentType                   |         |                                                                       |
| ConsoleStartingUpFlag                |         |                                                                       |
| SystemStartingUpFlag                 |         |                                                                       |
| ConsoleFirstInitFlag                 |         |                                                                       |
| HomeMenuScreenDisplayedFlag          |         |                                                                       |
| DataManagementScreenDisplayedFlag    |         |                                                                       |
| ConnectionTestingFlag                |         |                                                                       |
| ApplicationRunningFlag               |         |                                                                       |
| DataCorruptionDetectedFlag           |         |                                                                       |
| ProductModel                         |         |                                                                       |
| CurrentLanguage                      |         |                                                                       |
| UseNetworkTimeProtocolFlag           |         |                                                                       |
| TimeZone                             |         |                                                                       |
| ControllerFirmware                   |         |                                                                       |
| VideoOutputSetting                   |         |                                                                       |
| NANDFreeSpace                        |         |                                                                       |
| SDCardFreeSpace                      |         |                                                                       |
| SerialNumber                         |         |                                                                       |
| OsVersion                            |         |                                                                       |
| ScreenBrightnessAutoAdjustFlag       |         |                                                                       |
| HdmiAudioOutputMode                  |         |                                                                       |
| SpeakerAudioOutputMode               |         |                                                                       |
| HeadphoneAudioOutputMode             |         |                                                                       |
| MuteOnHeadsetUnpluggedFlag           |         |                                                                       |
| NumUserRegistered                    |         |                                                                       |
| StorageAutoOrganizeFlag              |         |                                                                       |
| ControllerVibrationVolume            |         |                                                                       |
| LockScreenFlag                       |         |                                                                       |
| InternalBatteryLotNumber             |         |                                                                       |
| LeftControllerSerialNumber           |         |                                                                       |
| RightControllerSerialNumber          |         |                                                                       |
| NotifyInGameDownloadCompletionFlag   |         |                                                                       |
| NotificationSoundFlag                |         |                                                                       |
| TVResolutionSetting                  |         |                                                                       |
| RGBRangeSetting                      |         |                                                                       |
| ReduceScreenBurnFlag                 |         |                                                                       |
| TVAllowsCecFlag                      |         |                                                                       |
| HandheldModeTimeToScreenSleep        |         |                                                                       |
| ConsoleModeTimeToScreenSleep         |         |                                                                       |
| StopAutoSleepDuringContentPlayFlag   |         |                                                                       |
| LastConnectionTestDownloadSpeed      |         |                                                                       |
| LastConnectionTestUploadSpeed        |         |                                                                       |
| ServerFQDN                           |         |                                                                       |
| HTTPRequestContents                  |         |                                                                       |
| HTTPRequestResponseContents          |         |                                                                       |
| EdgeServerIPAddress                  |         |                                                                       |
| CDNContentPath                       |         |                                                                       |
| FileAccessPath                       |         |                                                                       |
| GameCardCID                          |         |                                                                       |
| NANDCID                              |         |                                                                       |
| MicroSDCID                           |         |                                                                       |
| NANDSpeedMode                        |         |                                                                       |
| MicroSDSpeedMode                     |         |                                                                       |
| GameCardSpeedMode                    |         |                                                                       |
| UserAccountInternalID                |         |                                                                       |
| NetworkServiceAccountInternalID      |         |                                                                       |
| NintendoAccountInternalID            |         |                                                                       |
| USB3AvailableFlag                    |         |                                                                       |
| CallStack                            |         |                                                                       |
| SystemStartupLog                     |         |                                                                       |
| RegionSetting                        |         |                                                                       |
| NintendoZoneConnectedFlag            |         |                                                                       |
| ForcedSleepHighTemperatureReading    |         |                                                                       |
| ForcedSleepFanSpeedReading           |         |                                                                       |
| ForcedSleepHWInfo                    |         |                                                                       |
| AbnormalPowerStateInfo               |         |                                                                       |
| ScreenBrightnessLevel                |         |                                                                       |
| ProgramId                            |         |                                                                       |
| AbortFlag                            |         |                                                                       |
| ReportVisibilityFlag                 |         |                                                                       |
| FatalFlag                            |         |                                                                       |
| OccurrenceTimestampNet               | Integer | UTC unix timestamp from [network-time](PCV%20services.md "wikilink"). |
| ResultBacktrace                      |         |                                                                       |
| GeneralRegisterAarch32               |         |                                                                       |
| StackBacktrace32                     |         |                                                                       |
| ExceptionInfoAarch32                 |         |                                                                       |
| GeneralRegisterAarch64               |         |                                                                       |
| ExceptionInfoAarch64                 |         |                                                                       |
| StackBacktrace64                     |         |                                                                       |
| RegisterSetFlag32                    |         |                                                                       |
| RegisterSetFlag64                    |         |                                                                       |
| ProgramMappedAddr32                  |         |                                                                       |
| ProgramMappedAddr64                  |         |                                                                       |
| AbortType                            |         |                                                                       |
| PrivateOsVersion                     |         |                                                                       |
| CurrentSystemPowerState              |         |                                                                       |
| PreviousSystemPowerState             |         |                                                                       |
| DestinationSystemPowerState          |         |                                                                       |
| PscTransitionCurrentState            |         |                                                                       |
| PscTransitionPreviousState           |         |                                                                       |
| PscInitializedList                   |         |                                                                       |
| PscCurrentPmStateList                |         |                                                                       |
| PscNextPmStateList                   |         |                                                                       |
| PerformanceMode                      |         |                                                                       |
| PerformanceConfiguration             |         |                                                                       |
| Throttled                            |         |                                                                       |
| ThrottlingDuration                   |         |                                                                       |
| ThrottlingTimestamp                  | Integer | UTC unix timestamp                                                    |
| GameCardCrcErrorCount                |         |                                                                       |
| GameCardAsicCrcErrorCount            |         |                                                                       |
| GameCardRefreshCount                 |         |                                                                       |
| GameCardReadRetryCount               |         |                                                                       |
| EdidBlock                            |         |                                                                       |
| EdidExtensionBlock                   |         |                                                                       |
| CreateProcessFailureFlag             |         |                                                                       |
| TemperaturePcb                       |         |                                                                       |
| TemperatureSoc                       |         |                                                                       |
| CurrentFanDuty                       |         |                                                                       |
| LastDvfsThresholdTripped             |         |                                                                       |
| CradlePdcHFwVersion                  |         |                                                                       |
| CradlePdcAFwVersion                  |         |                                                                       |
| CradleMcuFwVersion                   |         |                                                                       |
| CradleDp2HdmiFwVersion               |         |                                                                       |
| RunningApplicationId                 |         |                                                                       |
| RunningApplicationTitle              |         |                                                                       |
| RunningApplicationVersion            |         |                                                                       |
| RunningApplicationStorageLocation    |         |                                                                       |
| RunningAppletList                    |         |                                                                       |
| FocusedAppletHistory                 |         |                                                                       |
| CompositorState                      |         |                                                                       |
| CompositorLayerState                 |         |                                                                       |
| CompositorDisplayState               |         |                                                                       |
| CompositorHWCState                   |         |                                                                       |
| InputCurrentLimit                    |         |                                                                       |
| BoostModeCurrentLimit                |         |                                                                       |
| FastChargeCurrentLimit               |         |                                                                       |
| ChargeVoltageLimit                   |         |                                                                       |
| ChargeConfiguration                  |         |                                                                       |
| HizMode                              |         |                                                                       |
| ChargeEnabled                        |         |                                                                       |
| PowerSupplyPath                      |         |                                                                       |
| BatteryTemperature                   |         |                                                                       |
| BatteryChargePercent                 |         |                                                                       |
| BatteryChargeVoltage                 |         |                                                                       |
| BatteryAge                           |         |                                                                       |
| PowerRole                            |         |                                                                       |
| PowerSupplyType                      |         |                                                                       |
| PowerSupplyVoltage                   |         |                                                                       |
| PowerSupplyCurrent                   |         |                                                                       |
| FastBatteryChargingEnabled           |         |                                                                       |
| ControllerPowerSupplyAcquired        |         |                                                                       |
| OtgRequested                         |         |                                                                       |
| NANDPreEolInfo                       |         |                                                                       |
| NANDDeviceLifeTimeEstTypA            |         |                                                                       |
| NANDDeviceLifeTimeEstTypB            |         |                                                                       |
| NANDPatrolCount                      |         |                                                                       |
| NANDNumActivationFailures            |         |                                                                       |
| NANDNumActivationErrorCorrections    |         |                                                                       |
| NANDNumReadWriteFailures             |         |                                                                       |
| NANDNumReadWriteErrorCorrections     |         |                                                                       |
| NANDErrorLog                         |         |                                                                       |
| SdCardUserAreaSize                   |         |                                                                       |
| SdCardProtectedAreaSize              |         |                                                                       |
| SdCardNumActivationFailures          |         |                                                                       |
| SdCardNumActivationErrorCorrections  |         |                                                                       |
| SdCardNumReadWriteFailures           |         |                                                                       |
| SdCardNumReadWriteErrorCorrections   |         |                                                                       |
| SdCardErrorLog                       |         |                                                                       |
| EncryptionKey                        |         |                                                                       |
| EncryptedExceptionInfo               |         |                                                                       |
| GameCardTimeoutRetryErrorCount       |         |                                                                       |
| FsRemountForDataCorruptCount         |         |                                                                       |
| FsRemountForDataCorruptRetryOutCount |         |                                                                       |

[Category:Services](Category:Services "wikilink")

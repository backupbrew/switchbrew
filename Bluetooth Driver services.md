# btdrv

This is "nn::bluetooth::IBluetoothDriver".

The bluetooth driver implements the bluetooth protocol over h4/uart.

It interfaces with the [uart](Bus%20services#uart.md##uart "wikilink")
service to actually talk with the bluetooth hardware.

The code seems to be derived from a broadcom stack. A good starting
point for similar source code can be found in the MICO project:
<https://github.com/yinhongxing/mico/tree/ea67ff3659f12d730d4dc3b8d547b093bd2ee2ee/MICO/bluetooth_bte>
Note that the library files contain many (symbolized) functions which
match
btdrv.

| Cmd                     | Name                                                         |
| ----------------------- | ------------------------------------------------------------ |
| 0                       | InitializeBluetoothDriver                                    |
| 1                       | InitializeBluetooth                                          |
| 2                       | EnableBluetooth                                              |
| 3                       | DisableBluetooth                                             |
| 4                       | CleanupBluetooth                                             |
| 5                       | GetAdapterProperties                                         |
| 6                       | GetAdapterProperty                                           |
| 7                       | SetAdapterProperty                                           |
| 8                       | StartDiscovery                                               |
| 9                       | CancelDiscovery                                              |
| 10                      | CreateBond                                                   |
| 11                      | RemoveBond                                                   |
| 12                      | CancelBond                                                   |
| 13                      | PinReply                                                     |
| 14                      | SspReply                                                     |
| 15                      | GetEventInfo                                                 |
| 16                      | InitializeHid                                                |
| 17                      | HidConnect                                                   |
| 18                      | HidDisconnect                                                |
| 19                      | HidSendData                                                  |
| 20                      | HidSendData2                                                 |
| 21                      | HidSetReport                                                 |
| 22                      | HidGetReport                                                 |
| 23                      | HidWakeController                                            |
| 24                      | HidAddPairedDevice                                           |
| 25                      | HidGetPairedDevice                                           |
| 26                      | CleanupHid                                                   |
| 27                      | HidGetEventInfo                                              |
| 28                      | ExtSetTsi                                                    |
| 29                      | ExtSetBurstMode                                              |
| 30                      | ExtSetZeroRetran                                             |
| 31                      | ExtSetMcMode                                                 |
| 32                      | ExtStartLlrMode                                              |
| 33                      | ExtExitLlrMode                                               |
| 34                      | ExtSetRadio                                                  |
| 35                      | ExtSetVisibility                                             |
| 36                      | ExtSetTbfcScan                                               |
| 37                      | RegisterHidReportEvent                                       |
| 38                      | [\#HidGetReportEventInfo](#HidGetReportEventInfo "wikilink") |
| 39                      | GetLatestPlr                                                 |
| 40                      | ExtGetPendingConnections                                     |
| 41                      | GetChannelMap                                                |
| 42                      | EnableBluetoothBoostSetting                                  |
| 43                      | IsBluetoothBoostSettingEnabled                               |
| 44                      | EnableBluetoothAfhSetting                                    |
| 45                      | IsBluetoothAfhSettingEnabled                                 |
| 46                      | \[5.0.0+\] InitializeBluetoothLe                             |
| 47                      | \[5.0.0+\] EnableBluetoothLe                                 |
| 48                      | \[5.0.0+\] DisableBluetoothLe                                |
| 49                      | \[5.0.0+\] CleanupBluetoothLe                                |
| 50                      | \[5.0.0+\] SetLeVisibility                                   |
| 51                      | \[5.0.0+\] SetLeConnectionParameter                          |
| 52                      | \[5.0.0+\] SetLeDefaultConnectionParameter                   |
| 53                      | \[5.0.0+\] SetLeAdvertiseData                                |
| 54                      | \[5.0.0+\] SetLeAdvertiseParameter                           |
| 55                      | \[5.0.0+\] StartLeScan                                       |
| 56                      | \[5.0.0+\] StopLeScan                                        |
| 57                      | \[5.0.0+\] AddLeScanFilterCondition                          |
| 58                      | \[5.0.0+\] DeleteLeScanFilterCondition                       |
| 59                      | \[5.0.0+\] DeleteLeScanFilter                                |
| 60                      | \[5.0.0+\] ClearLeScanFilters                                |
| 61                      | \[5.0.0+\] EnableLeScanFilter                                |
| 62                      | \[5.0.0+\] RegisterLeClient                                  |
| 63                      | \[5.0.0+\] UnregisterLeClient                                |
| 64                      | \[5.0.0+\] UnregisterLeClientAll                             |
| 65                      | \[5.0.0+\] LeClientConnect                                   |
| 66                      | \[5.1.0+\] ?                                                 |
| 67 (\[5.0.0-5.0.2\] 66) | LeClientCancelConnection                                     |
| 68 (\[5.0.0-5.0.2\] 67) | \[5.0.0+\] LeClientDisconnect                                |
| 69 (\[5.0.0-5.0.2\] 68) | \[5.0.0+\] LeClientGetAttributes                             |
| 70 (\[5.0.0-5.0.2\] 69) | \[5.0.0+\] LeClientDiscoverService                           |
| 71 (\[5.0.0-5.0.2\] 70) | \[5.0.0+\] LeClientConfigureMtu                              |
| 72 (\[5.0.0-5.0.2\] 71) | \[5.0.0+\] RegisterLeServer                                  |
| 73 (\[5.0.0-5.0.2\] 72) | \[5.0.0+\] UnregisterLeServer                                |
| 74 (\[5.0.0-5.0.2\] 73) | \[5.0.0+\] LeServerConnect                                   |
| 75                      | \[5.0.0+\] CreateLeService                                   |
| 76 (\[5.0.0-5.0.2\] 74) | \[5.0.0+\] LeServerDisconnect                                |
| 77                      | \[5.0.0+\] AddLeCharacteristic                               |
| 78 (\[5.0.0-5.0.2\] 76) | \[5.0.0+\] StartLeService                                    |
| 79 (\[5.0.0-5.0.2\] 78) | \[5.0.0+\] AddLeDescriptor                                   |
| 80 (\[5.0.0-5.0.2\] 79) | \[5.0.0+\] GetLeCoreEventInfo                                |
| 81 (\[5.0.0-5.0.2\] 80) | \[5.0.0+\] LeGetFirstCharacteristic                          |
| 82 (\[5.0.0-5.0.2\] 81) | \[5.0.0+\] LeGetNextCharacteristic                           |
| 83 (\[5.0.0-5.0.2\] 82) | \[5.0.0+\] LeGetFirstDescriptor                              |
| 84                      | \[5.0.0+\] RegisterLeCoreDataPath                            |
| 85                      | \[5.0.0+\] UnregisterLeCoreDataPath                          |
| 86                      | \[5.0.0+\] RegisterLeHidDataPath                             |
| 87                      | \[5.0.0+\] UnregisterLeHidDataPath                           |
| 88                      | \[5.0.0+\] RegisterLeDataPath                                |
| 89 (\[5.0.0-5.0.2\] 83) | \[5.0.0+\] LeGetNextDescriptor                               |
| 90 (\[5.0.0-5.0.2\] 89) | \[5.0.0+\] UnregisterLeDataPath                              |
| 91 (\[5.0.0-5.0.2\] 90) | \[5.0.0+\] LeClientReadCharacteristic                        |
| 92 (\[5.0.0-5.0.2\] 91) | \[5.0.0+\] LeClientReadDescriptor                            |
| 93 (\[5.0.0-5.0.2\] 92) | \[5.0.0+\] LeClientWriteCharacteristic                       |
| 94                      | \[5.0.0+\] LeClientRegisterNotification                      |
| 95 (\[5.0.0-5.0.2\] 93) | \[5.0.0+\] LeClientWriteDescriptor                           |
| 96 (\[5.0.0-5.0.2\] 95) | \[5.0.0+\] LeClientDeregisterNotification                    |
| 97 (\[5.0.0-5.0.2\] 96) | \[5.0.0+\] GetLeHidEventInfo                                 |
| 97                      | \[5.0.0-5.0.2\] RegisterBleHidEvent                          |
| 98                      | \[5.1.0+\] SetLeScanParameter                                |
| 256                     | \[5.0.0+\] GetIsManufacturingMode                            |
| 257                     | \[7.0.0+\] EmulateBluetoothCrash                             |

## HidGetReportEventInfo

No input, takes a type-0xA output buffer and returns 4-bytes of output.

\[7.0.0+\] No longer takes a buffer or returns output, now returns an
output handle.

# bt

This is "nn::bluetooth::IBluetoothUser".

| Cmd | Name                           |
| --- | ------------------------------ |
| 0   | LeClientReadCharacteristic     |
| 1   | LeClientReadDescriptor         |
| 2   | LeClientWriteCharacteristic    |
| 3   | LeClientWriteDescriptor        |
| 4   | LeClientRegisterNotification   |
| 5   | LeClientDeregisterNotification |
| 6   | SetLeResponse                  |
| 7   | LeSendIndication               |
| 8   | GetLeEventInfo                 |
| 9   | RegisterBleEvent               |

[Category:Services](Category:Services "wikilink")

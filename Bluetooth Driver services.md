# btdrv

This is "nn::bluetooth::IBluetoothDriver".

The bluetooth driver implements the bluetooth protocol over h4/uart.

It interfaces with the [uart](Bus%20services#uart.md##uart "wikilink")
service to actually talk with the bluetooth hardware.

The code seems to be derived from a broadcom stack. A good starting
point for similar source code can be found in the MICO project:
<https://github.com/yinhongxing/mico/tree/ea67ff3659f12d730d4dc3b8d547b093bd2ee2ee/MICO/bluetooth_bte>
Note that the library files contain many (symbolized) functions which
match btdrv.

| Cmd | Name                                 |
| --- | ------------------------------------ |
| 0   |                                      |
| 1   | Init                                 |
| 2   | Enable                               |
| 3   | Disable                              |
| 4   | CleanupAndShutdown                   |
| 5   | GetAdapterProperties                 |
| 6   | GetAdapterProperty                   |
| 7   | SetAdapterProperty                   |
| 8   | StartDiscovery                       |
| 9   | CancelDiscovery                      |
| 10  | CreateBond                           |
| 11  | RemoveBond                           |
| 12  | CancelBond                           |
| 13  | PinReply                             |
| 14  | SspReply                             |
| 15  |                                      |
| 16  | InitInterfaces                       |
| 17  | HidHostInterface\_Connect            |
| 18  | HidHostInterface\_Disconnect         |
| 19  | HidHostInterface\_SendData           |
| 20  | HidHostInterface\_SendData2          |
| 21  | HidHostInterface\_SetReport          |
| 22  | HidHostInterface\_GetReport          |
| 23  | HidHostInterface\_WakeController     |
| 24  | HidHostInterface\_AddPairedDevice    |
| 25  | HidHostInterface\_GetPairedDevice    |
| 26  | HidHostInterface\_CleanupAndShutdown |
| 27  |                                      |
| 28  | ExtInterface\_SetTSI                 |
| 29  | ExtInterface\_SetBurstMode           |
| 30  | ExtInterface\_SetZeroRetran          |
| 31  | ExtInterface\_SetMcMode              |
| 32  | ExtInterface\_StartLlrMode           |
| 33  | ExtInterface\_ExitLlrMode            |
| 34  | ExtInterface\_SetRadio               |
| 35  | ExtInterface\_SetVisibility          |
| 36  |                                      |
| 37  |                                      |
| 38  | HidHostInterface\_GetLatestPlr       |
| 39  | ExtInterface\_GetPendingConnections  |
| 40  | HidHostInterface\_GetChannelMap      |
| 41  | SetIsBluetoothBoostEnabled           |
| 42  | GetIsBluetoothBoostEnabled           |
| 43  | SetIsBluetoothAfhEnabled             |
| 44  | GetIsBluetoothAfhEnabled             |

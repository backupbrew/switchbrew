# wlan:inf

This is "nn::wlan::detail::IInfraManager".

| Cmd | Name            |
| --- | --------------- |
| 0   |                 |
| 1   |                 |
| 2   | GetMacAddress   |
| 3   | StartScan       |
| 4   | StopScan        |
| 5   | Connect         |
| 6   | CancelConnect   |
| 7   | Disconnect      |
| 8   |                 |
| 9   |                 |
| 10  | GetState        |
| 11  | GetScanResult   |
| 12  | GetRssi         |
| 13  | ChangeRxAntenna |
| 14  |                 |
| 15  |                 |
| 16  | RequestWakeUp   |
| 17  | RequestIfUpDown |
| 18  | \[3.0.0+\]      |
| 19  | \[3.0.0+\]      |
| 20  | \[3.0.0+\]      |
| 21  | \[3.0.0+\]      |
| 22  | \[3.0.0+\]      |
| 23  | \[3.0.0+\]      |
| 24  | \[3.0.0+\]      |
| 25  | \[3.0.0+\]      |
| 26  | \[4.0.0+\]      |
| 27  | \[4.0.0+\]      |
| 28  | \[5.0.0+\]      |
| 29  | \[7.0.0+\]      |
| 30  | \[8.0.0+\]      |

\[4.0.0+\] Connect now takes an additional 4-bytes of input.

\[5.0.0+\] Cmd24 now returns a total of 0x58-bytes of output instead of
0x5C.

\[7.0.0+\] Input/output for cmds 27/28 were swapped, perhaps these cmds
were swapped?

# wlan:lcl

This is "nn::wlan::detail::ILocalManager".

| Cmd | Name                          |
| --- | ----------------------------- |
| 0   |                               |
| 1   |                               |
| 2   |                               |
| 3   |                               |
| 4   |                               |
| 5   |                               |
| 6   | GetMacAddress                 |
| 7   | CreateBss                     |
| 8   | DestroyBss                    |
| 9   | StartScan                     |
| 10  | StopScan                      |
| 11  | Connect                       |
| 12  | CancelConnect                 |
| 13  | Join                          |
| 14  | CancelJoin                    |
| 15  | Disconnect                    |
| 16  | SetBeaconLostCount            |
| 17  |                               |
| 18  |                               |
| 19  |                               |
| 20  | GetBssIndicationEvent         |
| 21  | GetBssIndicationInfo          |
| 22  | GetState                      |
| 23  | GetAllowedChannels            |
| 24  | AddIe                         |
| 25  | DeleteIe                      |
| 26  |                               |
| 27  |                               |
| 28  | CreateRxEntry                 |
| 29  | DeleteRxEntry                 |
| 30  |                               |
| 31  |                               |
| 32  | AddMatchingDataToRxEntry      |
| 33  | RemoveMatchingDataFromRxEntry |
| 34  | GetScanResult                 |
| 35  |                               |
| 36  | SetActionFrameWithBeacon      |
| 37  | CancelActionFrameWithBeacon   |
| 38  | CreateRxEntryForActionFrame   |
| 39  | DeleteRxEntryForActionFrame   |
| 40  |                               |
| 41  |                               |
| 42  | CancelGetActionFrame          |
| 43  | GetRssi                       |
| 44  |                               |
| 45  | \[4.0.0+\]                    |
| 46  | \[4.0.0+\]                    |
| 47  | \[4.0.0+\]                    |
| 48  | \[4.0.0-8.1.0\]               |
| 49  | \[6.0.0-8.1.0\]               |
| 50  | \[6.0.0-8.1.0\]               |
| 51  | \[8.0.0-8.1.0\]               |
| 52  | \[8.0.0-8.1.0\]               |

\[4.0.0+\] CreateBss, Connect, and Join now takes an additional 4-bytes
of input.

\[5.0.0+\] GetAllowedChannels now returns a total of 4-bytes of output
instead of 0x50, and now takes a type-0xA output buffer.

# wlan:lg

This is "nn::wlan::detail::ILocalGetFrame".

| Cmd | Name |
| --- | ---- |
| 0   |      |

# wlan:lga

This is "nn::wlan::detail::ILocalGetActionFrame".

| Cmd | Name |
| --- | ---- |
| 0   |      |

\[5.0.0+\] Cmd0 now takes an additional 4-bytes of input, and returns an
additional 4-bytes of output.

# wlan:sg

This is "nn::wlan::detail::ISocketGetFrame".

| Cmd | Name |
| --- | ---- |
| 0   |      |

# wlan:soc

This is "nn::wlan::detail::ISocketManager".

| Cmd | Name                   |
| --- | ---------------------- |
| 0   |                        |
| 1   |                        |
| 2   |                        |
| 3   |                        |
| 4   |                        |
| 5   |                        |
| 6   | GetMacAddress          |
| 7   | SwitchTsfTimerFunction |
| 8   |                        |
| 9   |                        |
| 10  |                        |
| 11  |                        |
| 12  | \[6.0.0+\]             |

# wlan:dtc

This was added with \[6.0.0+\].

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |
| 3   |      |
| 4   |      |
| 5   |      |
| 6   |      |
| 7   |      |
| 8   |      |
| 9   |      |
| 10  |      |
| 11  |      |
| 12  |      |
| 13  |      |
| 14  |      |
| 15  |      |
| 16  |      |
| 17  |      |
| 18  |      |
| 19  |      |
| 20  |      |
| 21  |      |
| 22  |      |
| 23  |      |
| 24  |      |
| 25  |      |
| 26  |      |
| 27  |      |

\[7.0.0+\] Cmd14 now takes an input u8.

[Category:Services](Category:Services "wikilink")

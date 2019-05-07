# npns:u

This is "nn::npns::INpnsUser".

| Cmd | Name                                                                              |
| --- | --------------------------------------------------------------------------------- |
| 1   | ListenAll                                                                         |
| 2   | ListenTo                                                                          |
| 3   | Receive                                                                           |
| 4   | ReceiveRaw                                                                        |
| 5   | GetReceiveEvent                                                                   |
| 7   | GetStateChangeEvent                                                               |
| 21  | CreateToken                                                                       |
| 23  | DestroyToken                                                                      |
| 25  | QueryIsTokenValid                                                                 |
| 26  | \[6.0.0+\] ListenToMyApplicationId                                                |
| 101 | Suspend                                                                           |
| 102 | Resume                                                                            |
| 103 | GetState                                                                          |
| 104 | \[3.0.0+\] GetStatistics                                                          |
| 111 | GetJid                                                                            |
| 120 | \[7.0.0+\] [\#CreateNotificationReceiver](#CreateNotificationReceiver "wikilink") |
| 151 | \[8.0.0+\] GetStateWithHandover                                                   |
| 152 | \[8.0.0+\] GetStateChangeEventWithHandover                                        |
| 153 | \[8.0.0+\] GetDropEventWithHandover                                               |

## CreateNotificationReceiver

Returns an [\#INotificationReceiver](#INotificationReceiver "wikilink").

## INotificationReceiver

This is "nn::npns::INotificationReceiver".

This was added with \[7.0.0+\].

| Cmd | Name                    | Notes                                                           |
| --- | ----------------------- | --------------------------------------------------------------- |
| 1   | ListenTo                | Takes a total of 8-bytes of input, no output.                   |
| 2   | ListenToMyApplicationId | Takes a total of 8-bytes of input and a PID, no output.         |
| 3   | Receive                 | Takes a total of 2-bytes of input and a type-0x6 output buffer. |
| 4   | GetReceiveEvent         | No input, returns an output handle.                             |

# npns:s

This is "nn::npns::INpnsSystem".

| Cmd | Name                                                                              |
| --- | --------------------------------------------------------------------------------- |
| 1   | ListenAll                                                                         |
| 2   | ListenTo                                                                          |
| 3   | Receive                                                                           |
| 4   | ReceiveRaw                                                                        |
| 5   | GetReceiveEvent                                                                   |
| 6   | ListenUndelivered                                                                 |
| 7   | GetStateChangeEvent                                                               |
| 11  | SubscribeTopic                                                                    |
| 12  | UnsubscribeTopic                                                                  |
| 13  | QueryIsTopicExist                                                                 |
| 21  | CreateToken                                                                       |
| 22  | CreateTokenWithApplicationId                                                      |
| 23  | DestroyToken                                                                      |
| 24  | DestroyTokenWithApplicationId                                                     |
| 25  | QueryIsTokenValid                                                                 |
| 31  | UploadTokenToBaaS                                                                 |
| 32  | DestroyTokenForBaaS                                                               |
| 33  | \[7.0.0+\] CreateTokenForBaas                                                     |
| 34  | \[7.0.0+\] SetBaasDeviceAccountIdList                                             |
| 101 | Suspend                                                                           |
| 102 | Resume                                                                            |
| 103 | GetState                                                                          |
| 104 | \[3.0.0+\] GetStatistics                                                          |
| 105 | \[3.0.0+\] GetPlayReportRequestEvent                                              |
| 111 | GetJid                                                                            |
| 112 | CreateJid                                                                         |
| 113 | DestroyJid                                                                        |
| 114 | AttachJid                                                                         |
| 115 | DetachJid                                                                         |
| 120 | \[7.0.0+\] [\#CreateNotificationReceiver](#CreateNotificationReceiver "wikilink") |
| 151 | \[8.0.0+\] GetStateWithHandover                                                   |
| 152 | \[8.0.0+\] GetStateChangeEventWithHandover                                        |
| 153 | \[8.0.0+\] GetDropEventWithHandover                                               |
| 201 | \[3.0.0+\] RequestChangeStateForceTimed                                           |
| 202 | \[3.0.0+\] RequestChangeStateForceAsync                                           |

[Category:Services](Category:Services "wikilink")

# nfc:am

This is "nn::nfc::am::detail::IAmManager".

| Cmd | Name              |
| --- | ----------------- |
| 0   | CreateAmInterface |

## IAm

This is "nn::nfc::am::detail::IAm".

| Cmd | Name                   |
| --- | ---------------------- |
| 0   | Initialize             |
| 1   | Finalize               |
| 2   | NotifyForegroundApplet |

# nfc:mf:u

This is "nn::nfc::mifare::detail::IUserManager".

| Cmd | Name                |
| --- | ------------------- |
| 0   | CreateUserInterface |

## IUser

This is "nn::nfc::mifare::detail::IUser".

| Cmd | Name                             |
| --- | -------------------------------- |
| 0   | Initialize                       |
| 1   | Finalize                         |
| 2   | ListDevices                      |
| 3   | StartDetection                   |
| 4   | StopDetection                    |
| 5   | Read                             |
| 6   | Write                            |
| 7   | GetTagInfo                       |
| 8   | GetActivateEventHandle           |
| 9   | GetDeactivateEventHandle         |
| 10  | GetState                         |
| 11  | GetDeviceState                   |
| 12  | GetNpadId                        |
| 13  | GetAvailabilityChangeEventHandle |

# nfc:user

This is "nn::nfc::detail::IUserManager".

| Cmd | Name                |
| --- | ------------------- |
| 0   | CreateUserInterface |

## IUser

This is "nn::nfc::detail::IUser".

| Cmd  | Name                                     |
| ---- | ---------------------------------------- |
| 0    | Initialize                               |
| 1    | Finalize                                 |
| 2    | GetState                                 |
| 3    | IsNfcEnabled                             |
| 400  | \[4.0.0+\] Initialize                    |
| 401  | \[4.0.0+\] Finalize                      |
| 402  | \[4.0.0+\] GetState                      |
| 403  | \[4.0.0+\] IsNfcEnabled                  |
| 404  | \[4.0.0+\] ListDevices                   |
| 405  | \[4.0.0+\] GetDeviceState                |
| 406  | \[4.0.0+\] GetNpadId                     |
| 407  | \[4.0.0+\] AttachAvailabilityChangeEvent |
| 408  | \[4.0.0+\] StartDetection                |
| 409  | \[4.0.0+\] StopDetection                 |
| 410  | \[4.0.0+\] GetTagInfo                    |
| 411  | \[4.0.0+\] AttachActivateEvent           |
| 412  | \[4.0.0+\] AttachDeactivateEvent         |
| 1000 | \[4.0.0+\] ReadMifare                    |
| 1001 | \[4.0.0+\] WriteMifare                   |
| 1300 | \[4.0.0+\] SendCommandByPassThrough      |
| 1301 | \[4.0.0+\] KeepPassThroughSession        |
| 1302 | \[4.0.0+\] ReleasePassThroughSession     |

# nfc:sys

This is "nn::nfc::detail::ISystemManager".

| Cmd | Name                  |
| --- | --------------------- |
| 0   | CreateSystemInterface |

## ISystem

This is "nn::nfc::detail::ISystem".

| Cmd  | Name                                     |
| ---- | ---------------------------------------- |
| 0    | Initialize                               |
| 1    | Finalize                                 |
| 2    | GetState                                 |
| 3    | IsNfcEnabled                             |
| 100  | SetNfcEnabled                            |
| 400  | \[4.0.0+\] InitializeSystem              |
| 401  | \[4.0.0+\] FinalizeSystem                |
| 402  | \[4.0.0+\] GetState                      |
| 403  | \[4.0.0+\] IsNfcEnabled                  |
| 404  | \[4.0.0+\] ListDevices                   |
| 405  | \[4.0.0+\] GetDeviceState                |
| 406  | \[4.0.0+\] GetNpadId                     |
| 407  | \[4.0.0+\] AttachAvailabilityChangeEvent |
| 408  | \[4.0.0+\] StartDetection                |
| 409  | \[4.0.0+\] StopDetection                 |
| 410  | \[4.0.0+\] GetTagInfo                    |
| 411  | \[4.0.0+\] AttachActivateEvent           |
| 412  | \[4.0.0+\] AttachDeactivateEvent         |
| 500  | \[4.0.0+\] SetNfcEnabled                 |
| 1000 | \[4.0.0+\] ReadMifare                    |
| 1001 | \[4.0.0+\] WriteMifare                   |
| 1300 | \[4.0.0+\] SendCommandByPassThrough      |
| 1301 | \[4.0.0+\] KeepPassThroughSession        |
| 1302 | \[4.0.0+\] ReleasePassThroughSession     |

# nfp:user

This is "nn::nfp::detail::IUserManager".

| Cmd | Name                |
| --- | ------------------- |
| 0   | CreateUserInterface |

## IUser

This is "nn::nfp::detail::IUser".

| Cmd | Name                          |
| --- | ----------------------------- |
| 0   | Initialize                    |
| 1   | Finalize                      |
| 2   | ListDevices                   |
| 3   | StartDetection                |
| 4   | StopDetection                 |
| 5   | Mount                         |
| 6   | Unmount                       |
| 7   | OpenApplicationArea           |
| 8   | GetApplicationArea            |
| 9   | SetApplicationArea            |
| 10  | Flush                         |
| 11  | Restore                       |
| 12  | CreateApplicationArea         |
| 13  | GetTagInfo                    |
| 14  | GetRegisterInfo               |
| 15  | GetCommonInfo                 |
| 16  | GetModelInfo                  |
| 17  | AttachActivateEvent           |
| 18  | AttachDeactivateEvent         |
| 19  | GetState                      |
| 20  | GetDeviceState                |
| 21  | GetNpadId                     |
| 22  | GetApplicationArea2           |
| 23  | AttachAvailabilityChangeEvent |
| 24  | RecreateApplicationArea       |

# nfp:dbg

This is "nn::nfp::detail::IDebugManager".

| Cmd | Name                 |
| --- | -------------------- |
| 0   | CreateDebugInterface |

## IDebug

This is "nn::nfp::detail::IDebug".

| Cmd | Name                          |
| --- | ----------------------------- |
| 0   | InitializeDebug               |
| 1   | FinalizeDebug                 |
| 2   | ListDevices                   |
| 3   | StartDetection                |
| 4   | StopDetection                 |
| 5   | Mount                         |
| 6   | Unmount                       |
| 7   | OpenApplicationArea           |
| 8   | GetApplicationArea            |
| 9   | SetApplicationArea            |
| 10  | Flush                         |
| 11  | Restore                       |
| 12  | CreateApplicationArea         |
| 13  | GetTagInfo                    |
| 14  | GetRegisterInfo               |
| 15  | GetCommonInfo                 |
| 16  | GetModelInfo                  |
| 17  | AttachActivateEvent           |
| 18  | AttachDeactivateEvent         |
| 19  | GetState                      |
| 20  | GetDeviceState                |
| 21  | GetNpadId                     |
| 22  | GetApplicationArea2           |
| 23  | AttachAvailabilityChangeEvent |
| 24  | RecreateApplicationArea       |
| 100 | Format                        |
| 101 | GetAdminInfo                  |
| 102 | GetRegisterInfo               |
| 103 | SetRegisterInfo               |
| 104 | DeleteRegisterInfo            |
| 105 | DeleteApplicationArea         |
| 106 | ExistsApplicationArea         |
| 200 | GetAll                        |
| 201 | SetAll                        |
| 202 | FlushDebug                    |
| 203 | BreakTag                      |
| 204 | ReadBackupData                |
| 205 | WriteBackupData               |
| 206 | WriteNtf                      |
| 300 | \[1.0.0-3.0.2\]               |
| 301 | \[1.0.0-3.0.2\]               |
| 302 | \[1.0.0-3.0.2\]               |
| 303 | \[1.0.0-3.0.2\]               |
| 304 | \[1.0.0-3.0.2\]               |
| 305 | \[1.0.0-3.0.2\]               |
| 306 | \[1.0.0-3.0.2\]               |
| 307 | \[1.0.0-3.0.2\]               |
| 308 | \[1.0.0-3.0.2\]               |
| 309 | \[1.0.0-3.0.2\]               |
| 310 | \[1.0.0-3.0.2\]               |
| 311 | \[1.0.0-3.0.2\]               |
| 312 | \[1.0.0-3.0.2\]               |
| 313 | \[1.0.0-3.0.2\]               |
| 314 | \[1.0.0-3.0.2\]               |

# nfp:sys

This is "nn::nfp::detail::ISystemManager".

| Cmd | Name                  |
| --- | --------------------- |
| 0   | CreateSystemInterface |

## ISystem

This is "nn::nfp::detail::ISystem".

| Cmd | Name                          |
| --- | ----------------------------- |
| 0   | InitializeSystem              |
| 1   | FinalizeSystem                |
| 2   | ListDevices                   |
| 3   | StartDetection                |
| 4   | StopDetection                 |
| 5   | Mount                         |
| 6   | Unmount                       |
| 10  | Flush                         |
| 11  | Restore                       |
| 13  | GetTagInfo                    |
| 14  | GetRegisterInfo               |
| 15  | GetCommonInfo                 |
| 16  | GetModelInfo                  |
| 17  | AttachActivateEvent           |
| 18  | AttachDeactivateEvent         |
| 19  | GetState                      |
| 20  | GetDeviceState                |
| 21  | GetNpadId                     |
| 23  | AttachAvailabilityChangeEvent |
| 100 | Format                        |
| 101 | GetAdminInfo                  |
| 102 | GetRegisterInfo               |
| 103 | SetRegisterInfo               |
| 104 | DeleteRegisterInfo            |
| 105 | DeleteApplicationArea         |
| 106 | ExistsApplicationArea         |

[Category:Services](Category:Services "wikilink")

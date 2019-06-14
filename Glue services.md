# arp:r

This is "nn::arp::detail::IReader".

| Cmd | Name                                           | Notes                                                                                                                            |
| --- | ---------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| 0   | GetApplicationLaunchProperty                   | Takes an input u64 ProcessId, returns an [\#ApplicationLaunchProperty](#ApplicationLaunchProperty "wikilink")                    |
| 1   | GetApplicationLaunchPropertyWithApplicationId  | Takes an input u64 TitleId, returns an [\#ApplicationLaunchProperty](#ApplicationLaunchProperty "wikilink")                      |
| 2   | GetApplicationControlProperty                  | Takes an input u64 ProcessId, returns a type-0x16 buffer filled with the contents of [control.nacp](NACP%20Format.md "wikilink") |
| 3   | GetApplicationControlPropertyWithApplicationId | Takes an input u64 TitleId, returns a type-0x16 buffer filled with the contents of [control.nacp](NACP%20Format.md "wikilink")   |

# arp:w

This is "nn::arp::detail::IWriter".

| Cmd | Name             | Notes                                             |
| --- | ---------------- | ------------------------------------------------- |
| 0   | AcquireRegistrar | Returns an [\#IRegistrar](#IRegistrar "wikilink") |
| 1   | DeleteProperties | Takes an input u64 unknown                        |

## IRegistrar

This is "nn::arp::detail::IRegistrar".

| Cmd | Name                          | Notes                                                                                                   |
| --- | ----------------------------- | ------------------------------------------------------------------------------------------------------- |
| 0   | Issue                         | Takes an input u64 unknown                                                                              |
| 1   | SetApplicationLaunchProperty  | Takes an input [\#ApplicationLaunchProperty](#ApplicationLaunchProperty "wikilink")                     |
| 2   | SetApplicationControlProperty | Takes an input type-0x15 buffer filled with the contents of [control.nacp](NACP%20Format.md "wikilink") |

# bgtc:t

This is "nn::bgtc::ITaskService".

| Cmd | Name                                              |
| --- | ------------------------------------------------- |
| 1   | NotifyTaskStarting                                |
| 2   | NotifyTaskFinished                                |
| 3   | GetTriggerEvent                                   |
| 4   | IsInHalfAwake                                     |
| 5   | NotifyClientName                                  |
| 6   | \[3.0.0+\] IsInFullAwake                          |
| 11  | ScheduleTask                                      |
| 12  | GetScheduledTaskInterval                          |
| 13  | UnscheduleTask                                    |
| 14  | GetScheduleEvent                                  |
| 15  | SchedulePeriodicTask                              |
| 101 | \[3.0.0+\] GetOperationMode                       |
| 102 | \[3.0.0+\] WillDisconnectNetworkWhenEnteringSleep |
| 103 | \[3.0.0+\] WillStayHalfAwakeInsteadSleep          |
|     |                                                   |

# bgtc:sc

This is "nn::bgtc::IStateControlService".

| Cmd | Name                                         |
| --- | -------------------------------------------- |
| 1   | GetState                                     |
| 2   | GetStateChangedEvent                         |
| 3   | NotifyEnteringHalfAwake                      |
| 4   | NotifyLeavingHalfAwake                       |
| 5   | \[3.0.0+\] SetIsUsingSleepUnsupportedDevices |
|     |                                              |

# ApplicationLaunchProperty

Total size is 0x10-bytes.

| Offset | Size | Description                                                                      |
| ------ | ---- | -------------------------------------------------------------------------------- |
| 0x00   | 0x08 | Title ID                                                                         |
| 0x08   | 0x04 | Version                                                                          |
| 0x0C   | 0x01 | Base Game [Storage Id](Filesystem%20services#StorageId.md##StorageId "wikilink") |
| 0x0D   | 0x01 | Update [Storage Id](Filesystem%20services#StorageId.md##StorageId "wikilink")    |
| 0x0E   | 0x02 | Padding                                                                          |

[Category:Services](Category:Services "wikilink")

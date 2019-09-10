# arp:r

This is "nn::arp::detail::IReader".

| Cmd  | Name                                           | Notes                                                                                                                            |
| ---- | ---------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| 0    | GetApplicationLaunchProperty                   | Takes an input u64 ProcessId, returns an [\#ApplicationLaunchProperty](#ApplicationLaunchProperty "wikilink")                    |
| 1    | GetApplicationLaunchPropertyWithApplicationId  | Takes an input u64 TitleId, returns an [\#ApplicationLaunchProperty](#ApplicationLaunchProperty "wikilink")                      |
| 2    | GetApplicationControlProperty                  | Takes an input u64 ProcessId, returns a type-0x16 buffer filled with the contents of [control.nacp](NACP%20Format.md "wikilink") |
| 3    | GetApplicationControlPropertyWithApplicationId | Takes an input u64 TitleId, returns a type-0x16 buffer filled with the contents of [control.nacp](NACP%20Format.md "wikilink")   |
| 9998 |                                                |                                                                                                                                  |
| 9999 |                                                |                                                                                                                                  |

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
| 16  | \[9.0.0+\]                                        |
| 101 | \[3.0.0+\] GetOperationMode                       |
| 102 | \[3.0.0+\] WillDisconnectNetworkWhenEnteringSleep |
| 103 | \[3.0.0+\] WillStayHalfAwakeInsteadSleep          |

# bgtc:sc

This is "nn::bgtc::IStateControlService".

| Cmd | Name                                         |
| --- | -------------------------------------------- |
| 1   | GetState                                     |
| 2   | GetStateChangedEvent                         |
| 3   | NotifyEnteringHalfAwake                      |
| 4   | NotifyLeavingHalfAwake                       |
| 5   | \[3.0.0+\] SetIsUsingSleepUnsupportedDevices |

# time:a, time:r, time:u

These are "nn::timesrv::detail::<service::IStaticService>".

These were added with \[9.0.0+\].

| Cmd | Name                                                                 | Notes                                                          |
| --- | -------------------------------------------------------------------- | -------------------------------------------------------------- |
| 0   | GetStandardUserSystemClock                                           | Returns an [\#ISystemClock](#ISystemClock "wikilink").         |
| 1   | GetStandardNetworkSystemClock                                        | Returns an [\#ISystemClock](#ISystemClock "wikilink").         |
| 2   | GetStandardSteadyClock                                               | Returns an [\#ISteadyClock](#ISteadyClock "wikilink").         |
| 3   | GetTimeZoneService                                                   | Returns an [\#ITimeZoneService](#ITimeZoneService "wikilink"). |
| 4   | GetStandardLocalSystemClock                                          | Returns an [\#ISystemClock](#ISystemClock "wikilink").         |
| 5   | \[4.0.0+\] GetEphemeralNetworkSystemClock                            | Returns an [\#ISystemClock](#ISystemClock "wikilink").         |
| 20  | \[6.0.0+\] GetSharedMemoryNativeHandle                               |                                                                |
| 30  | \[6.0.0-8.1.0\] GetStandardNetworkClockOperationEventReadableHandle  |                                                                |
| 31  | \[6.0.0-8.1.0\] GetEphemeralNetworkClockOperationEventReadableHandle |                                                                |
| 50  | \[4.0.0+\] SetStandardSteadyClockInternalOffset                      |                                                                |
| 51  | \[9.0.0+\] GetStandardSteadyClockRtcValue                            |                                                                |
| 100 | IsStandardUserSystemClockAutomaticCorrectionEnabled                  |                                                                |
| 101 | SetStandardUserSystemClockAutomaticCorrectionEnabled                 |                                                                |
| 102 | \[5.0.0+\] GetStandardUserSystemClockInitialYear                     |                                                                |
| 200 | \[3.0.0+\] IsStandardNetworkSystemClockAccuracySufficient            |                                                                |
| 201 | \[6.0.0+\] GetStandardUserSystemClockAutomaticCorrectionUpdatedTime  |                                                                |
| 300 | \[4.0.0+\] CalculateMonotonicSystemClockBaseTimePoint                |                                                                |
| 400 | \[4.0.0+\] GetClockSnapshot                                          |                                                                |
| 401 | \[4.0.0+\] GetClockSnapshotFromSystemClockContext                    |                                                                |
| 500 | \[4.0.0+\] CalculateStandardUserSystemClockDifferenceByUser          |                                                                |
| 501 | \[4.0.0+\] CalculateSpanBetween                                      |                                                                |

## ISteadyClock

This is "nn::timesrv::detail::<service::ISteadyClock>".

| Cmd | Name                              | Notes                                                                                   |
| --- | --------------------------------- | --------------------------------------------------------------------------------------- |
| 0   | GetCurrentTimePoint               | No input, returns an output [\#SteadyClockTimePoint](#SteadyClockTimePoint "wikilink"). |
| 2   | GetTestOffset                     | No input, returns an output [\#TimeSpanType](#TimeSpanType "wikilink").                 |
| 3   | SetTestOffset                     | Takes an input [\#TimeSpanType](#TimeSpanType "wikilink"), no output.                   |
| 100 | \[2.0.0+\] GetRtcValue            | No input, returns an output s64.                                                        |
| 101 | \[2.0.0+\] IsRtcResetDetected     | No input, returns an output u8 bool.                                                    |
| 102 | \[2.0.0+\] GetSetupResultValue    | No input, returns an output u32.                                                        |
| 200 | \[3.0.0+\] GetInternalOffset      | No input, returns an output [\#TimeSpanType](#TimeSpanType "wikilink").                 |
| 201 | \[3.0.0-3.0.2\] SetInternalOffset | Takes an input [\#TimeSpanType](#TimeSpanType "wikilink"), no output.                   |

### SteadyClockTimePoint

| Offset | Size | Description                          |
| ------ | ---- | ------------------------------------ |
| 0x0    | 0x8  | A u64 representing a point in time.  |
| 0x8    | 0x10 | An ID representing the clock source. |

This is a 0x18-byte struct.

### TimeSpanType

This is an u64.

## ISystemClock

This is "nn::timesrv::detail::<service::ISystemClock>".

| Cmd | Name                                       | Notes                                                                     |
| --- | ------------------------------------------ | ------------------------------------------------------------------------- |
| 0   | GetCurrentTime                             | Returns an output [\#PosixTime](#PosixTime "wikilink").                   |
| 1   | SetCurrentTime                             | Takes an input [\#PosixTime](#PosixTime "wikilink").                      |
| 2   | GetSystemClockContext                      | Returns an output [\#SystemClockContext](#SystemClockContext "wikilink"). |
| 3   | SetSystemClockContext                      | Takes an input [\#SystemClockContext](#SystemClockContext "wikilink").    |
| 4   | \[9.0.0+\] GetOperationEventReadableHandle |                                                                           |

### PosixTime

This is an s64 for UTC POSIX time.

### SystemClockContext

This is an 0x20-byte struct.

| Offset | Size | Description                                                                 |
| ------ | ---- | --------------------------------------------------------------------------- |
| 0x0    | 0x8  | a [\#PosixTime](#PosixTime "wikilink") representing the system clock epoch. |
| 0x8    | 0x18 | a [\#SteadyClockTimePoint](#SteadyClockTimePoint "wikilink")                |

## ITimeZoneService

This is "nn::timesrv::detail::<service::ITimeZoneService>".

| Cmd | Name                                                         | Notes                                                                                                                                                                                                                                                             |
| --- | ------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0   | GetDeviceLocationName                                        | No input, returns an output [\#LocationName](#LocationName "wikilink").                                                                                                                                                                                           |
| 1   | SetDeviceLocationName                                        | Takes an input [\#LocationName](#LocationName "wikilink"), no output.                                                                                                                                                                                             |
| 2   | GetTotalLocationNameCount                                    | No input, returns an output s32.                                                                                                                                                                                                                                  |
| 3   | LoadLocationNameList                                         |                                                                                                                                                                                                                                                                   |
| 4   | LoadTimeZoneRule                                             | Takes an input [\#LocationName](#LocationName "wikilink") and a type-0x16 output buffer for [\#TimeZoneRule](#TimeZoneRule "wikilink"), no output.                                                                                                                |
| 5   | \[2.0.0+\] GetTimeZoneRuleVersion                            | No input, returns an output [\#TimeZoneRuleVersion](#TimeZoneRuleVersion "wikilink").                                                                                                                                                                             |
| 6   | \[5.0.0+\] GetDeviceLocationNameAndUpdatedTime               |                                                                                                                                                                                                                                                                   |
| 7   | \[9.0.0+\] SetDeviceLocationNameWithTimeZoneRule             |                                                                                                                                                                                                                                                                   |
| 8   | \[9.0.0+\] ParseTimeZoneBinary                               |                                                                                                                                                                                                                                                                   |
| 20  | \[9.0.0+\] GetDeviceLocationNameOperationEventReadableHandle |                                                                                                                                                                                                                                                                   |
| 100 | ToCalendarTime                                               | Takes an input [\#PosixTime](#PosixTime "wikilink") and a type-0x15 input buffer for [\#TimeZoneRule](#TimeZoneRule "wikilink"), returns an output [\#CalendarTime](#CalendarTime "wikilink") and [\#CalendarAdditionalInfo](#CalendarAdditionalInfo "wikilink"). |
| 101 | ToCalendarTimeWithMyRule                                     | Takes an input [\#PosixTime](#PosixTime "wikilink"), returns an output [\#CalendarTime](#CalendarTime "wikilink") and [\#CalendarAdditionalInfo](#CalendarAdditionalInfo "wikilink").                                                                             |
| 201 | ToPosixTime                                                  | Takes an input [\#CalendarTime](#CalendarTime "wikilink"), a type-0x15 input buffer for [\#TimeZoneRule](#TimeZoneRule "wikilink"), an type-0xA output buffer for [\#PosixTime](#PosixTime "wikilink") array, and returns an output s32.                          |
| 202 | ToPosixTimeWithMyRule                                        | Takes an input [\#CalendarTime](#CalendarTime "wikilink"), an type-0xA output buffer for [\#PosixTime](#PosixTime "wikilink") array, and returns an output s32.                                                                                                   |

### LoadLocationNameList

Takes an input s32 LocationName\_index and a type-0x6 output buffer for
[\#LocationName](#LocationName "wikilink"), returns an output s32 for
total output entries.

### LocationName

This contains a TimeZone location string with a max size of 0x24 bytes.

### TimeZoneRule

This is an 0x4000-byte struct. Official sw uses fixed-size 0x4000 for
the buffer size with the above commands.

This is loaded from the [TimeZoneBinary](Title%20list.md "wikilink")
title with the specified LocationName under the zoneinfo/ directory, the
content is then converted into this TimeZoneRule structure.

The files contained under zoneinfo/ directory are Tzif2 files without
Tzif1 header and data at the begining of them (see
[RFC8536](https://tools.ietf.org/html/rfc8536) for more information).

The conversion of a Tzif2 file to a TimeZoneRule structure is based on
[tz database code](https://github.com/eggert/tz/blob/master/localtime.c)
with some custom modifications (Leap seconds aren't handled, no usage of
"posixrules" and Tzif1 support stripped out).

| Offset | Size        | Description                                         |
| ------ | ----------- | --------------------------------------------------- |
| 0x0    | 0x4         | timecnt                                             |
| 0x4    | 0x4         | typecnt                                             |
| 0x8    | 0x4         | charcnt                                             |
| 0xC    | 0x1         | goback                                              |
| 0xD    | 0x1         | goahead                                             |
| 0xE    | 0x2         | Padding                                             |
| 0x10   | 0x8 \* 1000 | ats                                                 |
| 0x1f50 | 0x1 \* 1000 | types                                               |
| 0x2338 | 0x10 \* 128 | ttis (time type information), struct ttinfo\[1000\] |
| 0x2b38 | 0x1 \* 512  | chars                                               |
| 0x2d38 | 0x4         | defaulttype                                         |
| 0x2d3c | 0x12c4      | Reserved / Unused                                   |

### ttinfo

This is an 0x10-byte struct. Represent a Time Type Information used in
[\#TimeZoneRule](#TimeZoneRule "wikilink").

| Offset | Size | Description |
| ------ | ---- | ----------- |
| 0x0    | 0x4  | tt\_gmtoff  |
| 0x4    | 0x1  | tt\_isdst   |
| 0x5    | 0x3  | Padding     |
| 0x8    | 0x4  | tt\_abbrind |
| 0xC    | 0x1  | tt\_ttisstd |
| 0xD    | 0x1  | tt\_ttisgmt |
| 0xE    | 0x2  | Padding     |

### TimeZoneRuleVersion

This is an u128.

### CalendarTime

| Offset | Size | Description        |
| ------ | ---- | ------------------ |
| 0x0    | 0x2  | Year               |
| 0x2    | 0x1  | Month              |
| 0x3    | 0x1  | Day                |
| 0x4    | 0x1  | Hour               |
| 0x5    | 0x1  | Minute             |
| 0x6    | 0x1  | Second             |
| 0x7    | 0x1  | Padding / unknown? |

This is an 0x8-byte struct.

### CalendarAdditionalInfo

| Offset | Size | Description                                    |
| ------ | ---- | ---------------------------------------------- |
| 0x0    | 0x4  | 0-based day-of-week.                           |
| 0x4    | 0x4  | 0-based day-of-year.                           |
| 0x8    | 0x8  | Timezone name string.                          |
| 0x10   | 0x4  | 0 = no DST, 1 = DST.                           |
| 0x14   | 0x4  | s32 seconds relative to UTC for this timezone. |

This is an 0x18-byte struct. This stores timezone info.

# notif:a

This is "nn::notification::server::INotificationServicesForApplication".

This was added with \[9.0.0+\].

| Cmd  | Name                     |
| ---- | ------------------------ |
| 500  | RegisterAlarmSetting     |
| 510  | UpdateAlarmSetting       |
| 520  | ListAlarmSettings        |
| 530  | LoadApplicationParameter |
| 540  | DeleteAlarmSetting       |
| 1000 | Initialize               |

# notif:s

This is "nn::notification::server::INotificationServicesForSystem".

This was added with \[9.0.0+\].

| Cmd  | Name                     |
| ---- | ------------------------ |
| 500  | RegisterAlarmSetting     |
| 510  | UpdateAlarmSetting       |
| 520  | ListAlarmSettings        |
| 530  | LoadApplicationParameter |
| 540  | DeleteAlarmSetting       |
| 1000 | Initialize               |
| 1010 |                          |
| 1020 |                          |
| 1030 |                          |
| 1040 |                          |
| 1500 |                          |
| 1510 |                          |
| 2000 |                          |
| 2001 |                          |
| 2010 |                          |
| 2020 |                          |
| 8000 |                          |
| 8010 |                          |
| 9000 |                          |

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

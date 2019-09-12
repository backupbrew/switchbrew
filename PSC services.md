PSC (Power State Control) provides services related to power state
changes in the system.

# Concept

psc:m allows a process to register a module that depends on power
management in some way. A client calls GetPmModule to receive an
IPmModule (Power Managed Module), and then calls
IPmModule-\>Initialize(module\_id, module\_dependency\_list) where
module\_id is the ModuleId enum member for the client, and the
dependency list is an array of module IDs for the modules that this
depends on. Initialize() returns an event handle that the client can
wait on to be notified of a power state change.

psc:c allows a module to the power state controller for the system (in
practice, AM is the only client to the controller).
IPmControl-\>DispatchRequest() is used notify all IPmModules of a state
change.

For example, FS registers itself as an IPmModule with dependencies on
pinmux, gpio, pcv, tma, and initializes the SD card once those
dependencies have registered..

It then does (basically) the following pseudocode (actual code located
at .text + 0xB2DB0 in 6.0.0 FS):

`   while (true) {`  
`       Fs_IPmModule->WaitSignaled();`  
`       `  
`       Fs_IPmModule->GetRequest(&state);`  
`       switch (state) {`  
`           case WakingUp:`  
`               /* hardware devices are woken up here */`  
`           case GoingToSleep:`  
`               /* hardware devices are put to sleep here */`  
`           case ShuttingDown:`  
`               /* hardware devices are turned off here */`  
`       }`  
`       `  
`       Fs_IPmModule->Acknowledge(state);`  
`   }`

# psc:c

This is "nn::psc::sf::IPmControl".

| Cmd | Name                                   |
| --- | -------------------------------------- |
| 0   | Initialize                             |
| 1   | DispatchRequest                        |
| 2   | GetResult                              |
| 3   | GetState                               |
| 4   | Cancel                                 |
| 5   | \[1.0.0-6.2.0\] PrintModuleInformation |
| 6   | GetModuleInformation                   |
| 10  | \[9.0.0+\]                             |
| 11  | \[9.0.0+\]                             |

# psc:m

This is "nn::psc::sf::IPmService".

| Cmd | Name        | Notes                                            |
| --- | ----------- | ------------------------------------------------ |
| 0   | GetPmModule | Returns an [\#IPmModule](#IPmModule "wikilink"). |

## IPmModule

This is "nn::psc::sf::IPmModule".

| Cmd | Name                     |
| --- | ------------------------ |
| 0   | Initialize               |
| 1   | GetRequest               |
| 2   | Acknowledge              |
| 3   | Finalize                 |
| 4   | \[5.1.0+\] AcknowledgeEx |

# psc:l

This was added with \[9.0.0+\].

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |
| 3   |      |
| 4   |      |

# srepo:u, srepo:a

These are "nn::srepo::detail::ipc::ISrepoService".

These were added with \[5.0.0+\].

| Cmd   | Name       |
| ----- | ---------- |
| 10100 |            |
| 10101 | \[6.0.0+\] |
| 10200 | \[6.0.0+\] |
| 10201 | \[6.0.0+\] |
| 11000 | \[6.0.0+\] |
| 11001 | \[6.0.0+\] |
| 11002 | \[6.0.0+\] |
| 11003 | \[6.0.0+\] |
| 11004 | \[6.0.0+\] |
| 11100 | \[6.0.0+\] |
| 11200 | \[6.0.0+\] |
| 11300 | \[6.0.0+\] |
| 11400 | \[6.0.0+\] |
| 11500 | \[6.0.0+\] |
| 11600 | \[6.0.0+\] |
| 11601 | \[6.0.0+\] |
| 11602 | \[6.0.0+\] |
| 11700 | \[6.0.0+\] |
| 11800 | \[6.0.0+\] |
| 11801 | \[6.0.0+\] |
| 11810 | \[8.0.0+\] |
| 11811 | \[8.0.0+\] |
| 12000 | \[8.0.0+\] |
| 12001 | \[8.0.0+\] |
| 13000 | \[8.0.0+\] |
| 13001 | \[8.0.0+\] |
| 20100 |            |
| 20200 |            |
| 20300 | \[6.0.0+\] |
| 20400 | \[6.0.0+\] |
| 20401 | \[6.0.0+\] |
| 20402 | \[7.0.0+\] |
| 20500 | \[8.0.0+\] |

## Cmd13000

Takes a type-0x5 input buffer, no output.

\[9.0.0+\] No input, returns a total of 0xC-bytes of output, an
[\#IUnknown0](#IUnknown0 "wikilink"), and a handle.

## IUnknown0

Added with \[9.0.0+\].

| Cmd | Name |
| --- | ---- |
| 0   |      |

Cmd0: no input, returns a total of 8-bytes of output.

# ovln:rcv

This is "nn::ovln::IReceiverService".

| Cmd | Name         |
| --- | ------------ |
| 0   | OpenReceiver |

## IReceiver

This is "nn::ovln::IReceiver".

| Cmd | Name                  |
| --- | --------------------- |
| 0   | AddSource             |
| 1   | RemoveSource          |
| 2   | GetReceiveEventHandle |
| 3   | Receive               |
| 4   | ReceiveWithTick       |

# ovln:snd

This is "nn::ovln::ISenderService".

| Cmd | Name       |
| --- | ---------- |
| 0   | OpenSender |

## ISender

This is "nn::ovln::ISender".

| Cmd | Name                      |
| --- | ------------------------- |
| 0   | Send                      |
| 1   | GetUnreceivedMessageCount |

# time:su

This is "nn::timesrv::detail::<service::ITimeServiceManager>".

This was added with \[9.0.0+\].

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 5   |      |
| 6   |      |
| 9   |      |
| 10  |      |
| 11  |      |
| 12  |      |
| 13  |      |
| 14  |      |
| 15  |      |
| 50  |      |
| 51  |      |
| 52  |      |
| 60  |      |
| 100 |      |
| 200 |      |
| 201 |      |
| 202 |      |

# time:al

This is "nn::timesrv::detail::<service::IAlarmService>".

This was added with \[9.0.0+\].

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |

Cmd0/cmd1: no input, returns an
[\#ISteadyClockAlarm](#ISteadyClockAlarm "wikilink").

## ISteadyClockAlarm

This is "nn::timesrv::detail::<service::ISteadyClockAlarm>".

This was added with \[9.0.0+\].

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |
| 3   |      |
| 10  |      |
| 11  |      |

### Cmd10

Opens a session for [psc:l](#psc:l "wikilink") and returns it's
interface.

# time:m

This is "nn::timesrv::detail::<service::IPowerStateRequestHandler>".

This was added with \[9.0.0+\].

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |

# time:s, time:p

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

# ins:r

This is "nn::ins::IReceiverManager".

This was added with \[9.0.0+\].

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |

## Cmd0

Takes an input u32 **InsID**. Returns an u64.

## Cmd1

Takes an input u32 **InsID** and an input u64 (unused, official software
passes struct pointer). Returns an output Event handle with autoclear
disabled.

# ins:s

This is "nn::ins::ISenderManager".

This was added with \[9.0.0+\].

| Cmd | Name |
| --- | ---- |
| 0   |      |

## Cmd0

Takes an input u32 **InsID** and an input u64 (unused, official software
passes struct pointer). Returns an output Event handle with autoclear
disabled.

# PSC Module IDs

| ID   | Module                                                   |
| ---- | -------------------------------------------------------- |
| 0x03 |                                                          |
| 0x04 | [USB](USB%20services.md "wikilink")                      |
| 0x05 |                                                          |
| 0x07 | [Pcv](PCV%20services.md "wikilink")                      |
| 0x08 | [Pcv:Imm](PCV%20services.md "wikilink")                  |
| 0x09 | [Gpio](Bus%20services.md "wikilink")                     |
| 0x0A | [Pinmux](Bus%20services.md "wikilink")                   |
| 0x0B | [Uart](Bus%20services.md "wikilink")                     |
| 0x0C | [I2c](Bus%20services.md "wikilink")                      |
| 0x0D | [I2c:Pcv](Bus%20services.md "wikilink")                  |
| 0x0E | [Sasbus](Bus%20services.md "wikilink")                   |
| 0x0F | [Pwm](Bus%20services.md "wikilink")                      |
| 0x10 |                                                          |
| 0x13 | [PCIe](PCIe%20services.md "wikilink")                    |
| 0x14 | [Backlight](Backlight%20services.md "wikilink")          |
| 0x15 | [Nvnflinger](Nvnflinger%20services.md "wikilink")        |
| 0x18 | [nn::psc::PmModuleId\_Hid](HID%20services.md "wikilink") |
| 0x1B |                                                          |
| 0x1C | [Audio](Audio%20services.md "wikilink")                  |
| 0x1E |                                                          |
| 0x1F | [Bluetooth](Bluetooth%20Driver%20services.md "wikilink") |
| 0x20 | [Bpc](PCV%20services.md "wikilink")                      |
| 0x21 | [Ptm](PTM%20services.md "wikilink")                      |
| 0x23 | [nn::psc::PmModuleId\_Nfc](NFC%20services.md "wikilink") |
| 0x24 | [Ppc](PPC%20services.md "wikilink")                      |
| 0x25 |                                                          |
| 0x26 | [Nifm](Network%20Interface%20services.md "wikilink")     |
| 0x28 | [Npns](NPNS%20services.md "wikilink")                    |
| 0x29 | [nn::psc::PmModuleId\_Lm](Log%20services.md "wikilink")  |
| 0x2A | [Bcat](BCAT%20services.md "wikilink")                    |
| 0x2B | [Time](PCV%20services.md "wikilink")                     |
| 0x2C | [Pctl](Parental%20Control%20services.md "wikilink")      |
| 0x2D | [Erpt](Error%20Report%20services.md "wikilink")          |
| 0x2E | [Eupld](Error%20Upload%20services.md "wikilink")         |
| 0x2F | [Friend](Friend%20services.md "wikilink")                |
| 0x30 | [Glue](Glue%20services.md "wikilink")                    |
| 0x31 | [Account](Account%20services.md "wikilink")              |
| 0x32 | [SasBus](Bus%20services.md "wikilink")                   |
| 0x65 | [NV](NV%20services.md "wikilink")                        |

# Power Management States

| ID                  | Name | Description                             |
| ------------------- | ---- | --------------------------------------- |
| Awake               | 0    | Everything is awake.                    |
| ReadyAwaken         | 1    | Preparing to transition to awake.       |
| ReadySleep          | 2    | Preparing to transition to sleep.       |
| ReadySleepCritical  | 3    | Critical services are ready to sleep.   |
| ReadyAwakenCritical | 4    | Critical services are ready to wake up. |
| ReadyShutdown       | 5    | Preparing to transition to shutdown.    |

[Category:Services](Category:Services "wikilink")

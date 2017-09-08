# set

| Cmd | Name            |
| --- | --------------- |
| 0   | GetLanguageCode |
| 1   | SetLanguageCode |
| 3   |                 |
| 4   |                 |

# set:fd

# set:cal

| Cmd | Name                                             |
| --- | ------------------------------------------------ |
| 0   | GetBdAddress                                     |
| 1   | GetConfigurationId1                              |
| 2   | GetAccelerometerOffset                           |
| 3   | GetAccelerometerScale                            |
| 4   | GetGyroscopeOffset                               |
| 5   | GetGyroscopeScale                                |
| 6   | GetWlanMacAddress                                |
| 7   | GetWlanCountryCodesNum                           |
| 8   | GetWlanCountryCodes                              |
| 9   | GetSerialNumber                                  |
| 10  |                                                  |
| 11  |                                                  |
| 12  | GetBatteryLot                                    |
| 14  | [\#GetDeviceCert](#GetDeviceCert "wikilink")     |
| 15  | [\#GetETicketCert](#GetETicketCert "wikilink")   |
| 16  | [\#GetSslKey](#GetSslKey "wikilink")             |
| 17  | [\#GetSslCert](#GetSslCert "wikilink")           |
| 18  | [\#GetGameCardKey](#GetGameCardKey "wikilink")   |
| 19  | [\#GetGameCardCert](#GetGameCardCert "wikilink") |
| 20  | [\#GetDeviceKey](#GetDeviceKey "wikilink")       |
| 21  | [\#GetETicketKey](#GetETicketKey "wikilink")     |
| 22  | GetSpeakerCalibrationValues                      |
|     |                                                  |

Used for accessing data calibrated at the factory.

## GetDeviceCert

Takes a type-0x16 output buffer with fixed size 0x180.

Returns the device certificate (ECC signed). This is identical to 3DS
DeviceCert/CTCert besides the strings. NIM loads the DeviceId from this.

## GetETicketCert

Takes a type-0x16 output buffer with fixed size 0x240.

Returns the ETicket certificate (RSA signed).

## GetSslKey

Takes a type-0x16 output buffer with fixed size 0x134.

Returns the extended SSL key (0x130 bytes) from
[CAL0](Calibration#CAL0.md##CAL0 "wikilink"). If the extended key is not
programmed then it falls back to the normal SSL key (0x110 bytes).

Used by SSL-sysmodule, see [here](SSL%20services.md "wikilink").

## GetSslCert

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

## GetGameCardCert

Takes a type-0x16 output buffer with fixed size 0x404.

Returns a
[container](Settings%20services#setcal%20Container%20Structure.md##setcal_Container_Structure "wikilink")
with the GameCard certificate.

## GetDeviceKey

Returns the extended device ECC-B233 key (0x50 bytes) from
[CAL0](Calibration#CAL0.md##CAL0 "wikilink"). If the extended key is not
programmed then it falls back to the normal device ECC-B233 key (0x30
bytes).

## GetETicketKey

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

This container is used for returning data with variable
sizes.

# set:sys

| Cmd | Name                                                                              |
| --- | --------------------------------------------------------------------------------- |
| 3   | [\#GetSystemVersion](#GetSystemVersion "wikilink")                                |
| 37  | QuerySetting                                                                      |
| 38  | [\#ReadSetting](#ReadSetting "wikilink")                                          |
| 56  | [GetWirelessCertification](Flash%20Filesystem#PRODINFOF.md##PRODINFOF "wikilink") |
| 62  | [\#GetDebugMode](#GetDebugMode "wikilink")                                        |
| 68  | [\#GetSerialNumber](#GetSerialNumber "wikilink")                                  |

Official user-processes get a new service session handle each time a
set:sys cmd is used, with the session being closed aftewards.

## ReadSetting

Takes two type-0x19 input buffers and a type-0x6 output buffer. Returns
an output u64 for the actual size written to the outbuf.

The outbuf\_size is compared with the config\_size. When config\_size is
larger than outbuf\_size, outbuf\_size is used for the memcpy, otherwise
config\_size is used. Afterwards the size used for the memcpy is written
to output(see above).

If loading from main config fails, it will also attempt to load config
from various state if the input strings match hard-coded strings.

## GetSystemVersion

Takes a type-0x1A output buffer. User-processes use hard-coded size
0x100.

If needed, reads the content of the
[System\_Version\_Title](System%20Version%20Title.md "wikilink") "/file"
into state. This is only done once.

Then the above 0x100-byte data is copied to the output buffer.

## GetDebugMode

Returns an output u8.

Loads the 1-byte config for \<"settings\_debug",
"is\_debug\_mode\_enabled"\>. If that fails, value 0x1 is written to
output. This uses the same func as ReadSetting internally.

Returned retval is always 0.

## GetSerialNumber

Returns the 0x18-byte SerialNumber string.

[Category:Services](Category:Services "wikilink")

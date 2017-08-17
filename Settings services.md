# set

| Cmd | Name            |
| --- | --------------- |
| 0   | GetLanguageCode |
| 1   | SetLanguageCode |
| 3   |                 |
| 4   |                 |

# set:fd

# set:cal

| Cmd | Name              |
| --- | ----------------- |
| 14  | GetDeviceCert     |
| 15  | GetDeviceCert2    |
| 16  | GetTLSClientPrivk |
| 17  | GetTLSClientCert  |

Used for accessing data calibrated at the factory. Probably only for
console-unique data?(Everything read so far has been console-unique)

## GetDeviceCert

Takes a type-0x16 output buffer with fixed size 0x180.

Returns the DeviceCert. This is identical to 3DS DeviceCert/CTCert
besides the strings. NIM loads the DeviceId from this.

## GetDeviceCert2

Takes a type-0x16 output buffer with fixed size 0x240.

Same as GetDeviceCert, except this returns more data and the data starts
differing at offset 0x108 compared to GetDeviceCert.

## GetTLSClientPrivk

Takes a type-0x16 output buffer with fixed size 0x134.

Returns a container-structure for the encrypted TLS client-privk.
Decrypting this fails unless an unknown size \>0x134 is passed to this
setcal cmd?

Used by SSL-sysmodule, see [here](SSL%20services.md "wikilink").

## GetTLSClientCert

Takes a type-0x16 output buffer with fixed size 0x804.

Returns a container-structure for the plaintext TLS client-cert.

Used by SSL-sysmodule, see
[here](SSL%20services.md "wikilink").

### setcal Container Structure

| Offset | Size         | Name                                           |
| ------ | ------------ | ---------------------------------------------- |
| 0x0    | 0x4          | Size (same size used for decryption if needed) |
| 0x4    | {above size} | Actual data starts here.                       |

# set:sys

| Cmd | Name                                                                              |
| --- | --------------------------------------------------------------------------------- |
| 3   | GetSystemVersion                                                                  |
| 37  | QuerySetting                                                                      |
| 38  | ReadSetting                                                                       |
| 56  | [GetWirelessCertification](Flash%20Filesystem#PRODINFOF.md##PRODINFOF "wikilink") |
| 68  | GetSerialNumber                                                                   |

## GetSystemVersion

Takes a type-0x1A output buffer. User-processes use hard-coded size
0x100.

Returns the content of the
[System\_Version\_Title](System%20Version%20Title.md "wikilink")
"/file".

## GetSerialNumber

Returns the 0x18-byte SerialNumber string.

[Category:Services](Category:Services "wikilink")

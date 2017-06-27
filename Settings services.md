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

Used for accessing data calibrated at the factory.

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

Returns the encrypted TLS client-privk. Buf+0 is u32 size of the
encrypted/plaintext data, +4 is the actual start of the encrypted data.

Used by SSL-sysmodule, see [here](SSL%20services.md "wikilink").

## GetTLSClientCert

Takes a type-0x16 output buffer with fixed size 0x804.

Returns the plaintext TLS client-cert Buf+0 is the u32 size of the
actual cert, +4 is the actual start of the cert.

# set:sys

| Cmd | Name                                                        |
| --- | ----------------------------------------------------------- |
| ?   | GetSystemVersion                                            |
| ?   | GetSerialNumber (Returns the 0x18-byte SerialNumber string) |

## GetSystemVersion

Returns the content of the
[System\_Version\_Title](System%20Version%20Title.md "wikilink")
"/file".

[Category:Services](Category:Services "wikilink")

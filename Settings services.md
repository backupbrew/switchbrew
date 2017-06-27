# set

| Cmd | Name            |
| --- | --------------- |
| 0   | GetLanguageCode |
| 1   | SetLanguageCode |
| 3   |                 |
| 4   |                 |

# set:fd

# set:cal

| Cmd                            | Name                                              |
| ------------------------------ | ------------------------------------------------- |
| ?                              | GetDeviceId (Returns the 64bit DeviceId)          |
| GetDeviceId\_cmd+1 presumably? | GetDeviceCert (Returns the 0x240-byte DeviceCert) |
| 16                             | GetTLSClientPrivk                                 |
| 17                             | GetTLSClientCert                                  |

Used for accessing data calibrated at the factory.

## GetTLSClientPrivk

Takes a type-0x16 output buffer with fixed size 0x134.

Returns the encrypted TLS client-privk. Buf+0 is u32 size of the
encrypted/plaintext data, +4 is the actual start of the encrypted data.

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

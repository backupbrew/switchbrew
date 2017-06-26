# set

| Cmd | Name            |
| --- | --------------- |
| 0   | GetLanguageCode |
| 1   | SetLanguageCode |
| 3   |                 |
| 4   |                 |

# set:fd

# set:cal

| Cmd                                  | Name                                              |
| ------------------------------------ | ------------------------------------------------- |
| ?                                    | GetDeviceId (Returns the 64bit DeviceId)          |
| GetDeviceId\_cmd+1 presumably?       | GetDeviceCert (Returns the 0x240-byte DeviceCert) |
| ?                                    | GetTLSClientPrivk                                 |
| GetTLSClientPrivk\_cmd+1 presumably? | GetTLSClientCert                                  |

Used for accessing data calibrated at the factory.

## GetTLSClientPrivk

.Returns the encrypted TLS client-privk, outbuf\_size = 0x134. Buf+0 is
u32 size of the encrypted/plaintext data, +4 is the actual start of the
encrypted data.

## GetTLSClientCert

Returns the plaintext TLS client-cert, outbuf\_size = 0x804. Buf+0 is
the u32 size of the actual cert, +4 is the actual start of the cert.

# set:sys

[Category:Services](Category:Services "wikilink")

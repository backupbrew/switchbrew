# set

| Cmd | Name            |
| --- | --------------- |
| 0   | GetLanguageCode |
| 1   | SetLanguageCode |
| 3   |                 |
| 4   |                 |

# set:fd

# set:cal

| Cmd                                  | Name                                                                             |
| ------------------------------------ | -------------------------------------------------------------------------------- |
| ?                                    | GetDeviceId (Returns the 64bit DeviceId)                                         |
| GetDeviceId\_cmd+1 presumably?       | GetDeviceCert (Returns the 0x240-byte DeviceCert)                                |
| ?                                    | GetTLSClientPrivk (Returns the encrypted TLS client-privk, outbuf\_size = 0x134) |
| GetTLSClientPrivk\_cmd+1 presumably? | GetTLSClientCert (Returns the plaintext TLS client-cert, outbuf\_size = 0x804)   |

Used for accessing data calibrated at the factory.

# set:sys

[Category:Services](Category:Services "wikilink")

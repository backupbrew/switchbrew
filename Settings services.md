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
| 62  | GetDebugMode                                                                      |
| 68  | GetSerialNumber                                                                   |

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

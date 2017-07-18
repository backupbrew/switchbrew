# Header

The header is 0x200-bytes, at
Gamecard+0.

| Offset | Size  | Description                                                                   |
| ------ | ----- | ----------------------------------------------------------------------------- |
| 0x0    | 0x100 | RSA-2048 signature, presumably.                                               |
| 0x100  | 0x4   | Magicnum "HEAD"                                                               |
| 0x104  | 0x4   | Offset of Secure partition (Size of non-secure data?), in Media Units         |
| 0x108  | 0x4   | 0xFFFFFFFF                                                                    |
| 0x10C  | 0x4   | ?                                                                             |
| 0x110  | 0x8   | ?                                                                             |
| 0x118  | 0x8   | Size of the Gamecart, in Media Units                                          |
| 0x120  | 0x10  | ?                                                                             |
| 0x130  | 0x8   | Offset of HFS0 FS partition                                                   |
| 0x138  | 8     | HFS0 Header size                                                              |
| 0x140  | 0x20  | SHA256 hash of the HFS0 Header                                                |
| 0x160  | 0x20  | SHA256 hash of ?                                                              |
| 0x180  | 0x4   | 1?                                                                            |
| 0x184  | 0x4   | 2?                                                                            |
| 0x188  | 0x4   | 0?                                                                            |
| 0x18C  | 0x4   | Offset of Secure partition (Size of non-secure data?), in Media Units, again. |
| 0x190  | 0x70  | Encrypted data/hashes of some kind                                            |

# Cert

This is for the CERT, located at Gamecard + 0x7000 (always?). This
matches exactly the output from fsp-srv IDeviceOperator cmd 206
"GetGameCardDeviceCertificate".

| Offset | Size  | Description                       |
| ------ | ----- | --------------------------------- |
| 0x0    | 0x100 | RSA-2048 signature, presumably.   |
| 0x100  | 0x4   | Magicnum "CERT"                   |
| 0x110  | 0x10  | ?                                 |
| 0x12A  | 0xD6  | Encrypted data. Some kind of key? |

The data between the CERT and the start of the HFS0 is all 0xFF.

# HFS0

This is the FS which has magicnum "HFS0" at header+0.

| Offset       | Size | Description              |
| ------------ | ---- | ------------------------ |
| 0x0          | 0x4  | HFS0 Magic               |
| 0x4          | 0x4  | Number of files          |
| 0x8          | 0x4  | Size of the string table |
| 0xC          | 0x4  | Zero/Reserved            |
| 0x10         | X    | File Entry Table         |
| 0x10 + X     | Y    | String Table             |
| 0x10 + X + Y | Z    | Raw File Data            |

Where File Entry Table consists of Number of Files
FileEntries:

| Offset | Size | Description                                                                                                              |
| ------ | ---- | ------------------------------------------------------------------------------------------------------------------------ |
| 0x0    | 0x8  | Offset of file in Data                                                                                                   |
| 0x8    | 0x8  | Size of file in Data                                                                                                     |
| 0x10   | 0x4  | Offset of filename in String Table                                                                                       |
| 0x14   | 0x4  | Size of Hashed region of file (for HFS0s, this is the size of the pre-filedata portion, for NCAs this is usually 0x200). |
| 0x18   | 8    | Zero/Reserved                                                                                                            |
| 0x20   | 0x20 | SHA256 hash of the first (size of hashed region) bytes of filedata.                                                      |

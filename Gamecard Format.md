# Header

The header is 0x200-bytes at offset 0 in the
Gamecard.

| Offset | Size  | Description                                                                              |
| ------ | ----- | ---------------------------------------------------------------------------------------- |
| 0x0    | 0x100 | RSA-2048 PKCS \#1 signature over the XCI header (data from 0x100 to 0x200)               |
| 0x100  | 0x4   | Magicnum "HEAD"                                                                          |
| 0x104  | 0x4   | Write Size (size of non-secure data in Media Units which are 0x200 bytes)                |
| 0x108  | 0x4   | 0xFFFFFFFF                                                                               |
| 0x10C  | 0x1   | ?                                                                                        |
| 0x10D  | 0x1   | Gamecard Type (0xFA = 1GB, 0xF8 = 2GB, 0xF0 = 4GB, 0xE0 = 8GB, 0xE1 = 16GB, 0xE2 = 32GB) |
| 0x10E  | 0x1   | ?                                                                                        |
| 0x10F  | 0x1   | Gamecard Options (bit0 = AutoBoot, bit1 = HistoryErase)                                  |
| 0x110  | 0x8   | ?                                                                                        |
| 0x118  | 0x8   | Gamecard Size (in Media Units which are 0x200 bytes)                                     |
| 0x120  | 0x10  | Gamecard Initial Data IV (reversed)                                                      |
| 0x130  | 0x8   | HFS0 partition offset                                                                    |
| 0x138  | 0x8   | HFS0 header size                                                                         |
| 0x140  | 0x20  | SHA256 hash of the HFS0 Header                                                           |
| 0x160  | 0x20  | SHA256 hash of the crypto header                                                         |
| 0x180  | 0x4   | 1?                                                                                       |
| 0x184  | 0x4   | 2?                                                                                       |
| 0x188  | 0x4   | 0?                                                                                       |
| 0x18C  | 0x4   | Duplicate Write Size (size of non-secure data in Media Units which are 0x200 bytes)      |
| 0x190  | 0x70  | Gamecard Initial Data (AES-128-CBC encrypted)                                            |

# Cert

This is for the CERT, located at Gamecard + 0x7000 (always?). This
matches exactly the output from fsp-srv IDeviceOperator cmd 206
"GetGameCardDeviceCertificate".

| Offset | Size  | Description                                                   |
| ------ | ----- | ------------------------------------------------------------- |
| 0x0    | 0x100 | RSA-2048 PKCS \#1 signature over the data from 0x100 - 0x200. |
| 0x100  | 0x4   | Magicnum "CERT"                                               |
| 0x110  | 0x10  | ?                                                             |
| 0x12A  | 0xD6  | Encrypted data. Some kind of key?                             |

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

The string table is 00-padded to align the start of raw filedata with a
sector/media unit boundary (usually?).

# Typical Cartridge Layout

Observed gamecards contain three partitions: "update", "normal", and
"secure".

The update partition (Gamecard partition 0 for fsp-srv cmd 31) contains
.cnmt.nca + .nca files for the entire system update required to play the
game. Launch day carts contain a full copy of 1.0 ncas, newer carts
contain newer sysupdate NCAs etc.

The normal partition contains the .cnmt.nca and the game icondata nca.
This is presumably for future compatibility so that if a future update
changes the cryptographic protocol for the secure partition, Game icon
data can still be shown in the home menu on old firmwares.

The secure partition contains an identical copy of the .cnmt.nca and
game icondata nca, as well as all other ncas required for the game.

The entire rest of the gamecard after the secure partition ends is all
FF padding.

\[4.0.0+\] The "normal" partition is now empty and a new partition
"logo" was added.

Known internally as "XCI" (NX Card Image), this is the format used for
storing the contents of a Nintendo Switch Gamecard.

# Gamecard Header

This header is 0x200 bytes and is located at offset 0 in the
Gamecard.

| Offset | Size  | Description                                                                              |
| ------ | ----- | ---------------------------------------------------------------------------------------- |
| 0x0    | 0x100 | RSA-2048 PKCS \#1 signature over the header (data from 0x100 to 0x200)                   |
| 0x100  | 0x4   | Magicnum "HEAD"                                                                          |
| 0x104  | 0x4   | Secure Area Start Address (in Media Units which are 0x200 bytes)                         |
| 0x108  | 0x4   | Backup Area Start Address (always 0xFFFFFFFF)                                            |
| 0x10C  | 0x1   | Title KEK Index (high nibble) and KEK Index (low nibble)                                 |
| 0x10D  | 0x1   | Gamecard Size (0xFA = 1GB, 0xF8 = 2GB, 0xF0 = 4GB, 0xE0 = 8GB, 0xE1 = 16GB, 0xE2 = 32GB) |
| 0x10E  | 0x1   | Gamecard Header Version                                                                  |
| 0x10F  | 0x1   | Gamecard Flags (bit0 = AutoBoot, bit1 = HistoryErase)                                    |
| 0x110  | 0x8   | Package Id (used for challenge–response authentication)                                  |
| 0x118  | 0x8   | Valid Data End Address (in Media Units which are 0x200 bytes)                            |
| 0x120  | 0x10  | Gamecard Info IV (reversed)                                                              |
| 0x130  | 0x8   | HFS0 partition offset                                                                    |
| 0x138  | 0x8   | HFS0 header size                                                                         |
| 0x140  | 0x20  | SHA-256 hash of the [HFS0 Header](#HFS0_Header "wikilink")                               |
| 0x160  | 0x20  | SHA-256 hash of the [Initial Data](#Initial_Data "wikilink")                             |
| 0x180  | 0x4   | Secure Mode Flag (always 1, which means Secure Mode is available)                        |
| 0x184  | 0x4   | Title Key Flag (always 2)                                                                |
| 0x188  | 0x4   | Key Flag (always 0)                                                                      |
| 0x18C  | 0x4   | Normal Area End Address (in Media Units which are 0x200 bytes)                           |
| 0x190  | 0x70  | [Gamecard Info](#Gamecard_Info "wikilink") (AES-128-CBC encrypted)                       |

## Gamecard Info

When decrypted, this 0x70 byte region is as
follows:

| Offset | Size | Description                                                                                 |
| ------ | ---- | ------------------------------------------------------------------------------------------- |
| 0x0    | 0x8  | Firmware Version (0x01 for old Gamecards, 0x02 for new Gamecards with the "logo" partition) |
| 0x8    | 0x4  | Access Control Flags (0x00A10010 for 25MHz access or 0x00A10011 for 50MHz access)           |
| 0xC    | 0x4  | Read Wait Time (always 0x1388)                                                              |
| 0x10   | 0x4  | Read Wait Time2 (always 0)                                                                  |
| 0x14   | 0x4  | Write Wait Time (always 0)                                                                  |
| 0x18   | 0x4  | Write Wait Time2 (always 0)                                                                 |
| 0x1C   | 0x4  | Firmware Mode                                                                               |
| 0x20   | 0x4  | CUP Version                                                                                 |
| 0x24   | 0x4  | Empty                                                                                       |
| 0x28   | 0x8  | Update Partition Hash                                                                       |
| 0x30   | 0x8  | CUP Id (always 0x0100000000000816, which is the title-listing data archive's title ID)      |
| 0x38   | 0x38 | Empty                                                                                       |

# Gamecard Certificate

This is the Gamecard's unique certificate and is located at offset
0x7000.

[FS](Filesystem%20services.md "wikilink") IDeviceOperator cmd 206
"GetGameCardDeviceCertificate" retrieves this
data.

| Offset | Size  | Description                                                   |
| ------ | ----- | ------------------------------------------------------------- |
| 0x0    | 0x100 | RSA-2048 PKCS \#1 signature over the data from 0x100 to 0x200 |
| 0x100  | 0x4   | Magicnum "CERT"                                               |
| 0x110  | 0x10  | ?                                                             |
| 0x120  | 0xA   | ?                                                             |
| 0x12A  | 0xD6  | Encrypted data. Some kind of key?                             |

The data between the Gamecard Certificate and the start of the HFS0
region is all 0xFF.

# Initial Data

This data is used for challenge–response authentication when changing to
the Gamecard's secure mode.

[FS](Filesystem%20services.md "wikilink") calculates a SHA-256 hash over
the whole 0x200 bytes and compares it with the hash stored at offset
0x160 in the [Gamecard
Header](#Gamecard_Header "wikilink").

| Offset | Size  | Description                                                                    |
| ------ | ----- | ------------------------------------------------------------------------------ |
| 0x0    | 0x8   | Package Id from [Gamecard Header](#Gamecard_Header "wikilink") at offset 0x110 |
| 0x8    | 0x8   | Empty                                                                          |
| 0x10   | 0x10  | Challenge–response authentication data                                         |
| 0x20   | 0x10  | Challenge–response authentication MAC                                          |
| 0x30   | 0xC   | Challenge–response authentication Nonce                                        |
| 0x3C   | 0x1C4 | Reserved (must be empty)                                                       |

# HFS0

This is the Gamecard file system which starts with magicnum "HFS0".

## Header

The "SHA-256 File System" or "HFS0" starts at offset 0xF000 in the
Gamecard. The first 0x200 bytes act as a global header and represent the
root partition which points to the other partitions ("normal", "logo",
"update" and "secure).

A hash for this header is stored at offset 0x140 in the [Gamecard
Header](#Gamecard_Header "wikilink").

## File System

The actual file system is as follows (also valid for the root
partition):

| Offset       | Size | Description              |
| ------------ | ---- | ------------------------ |
| 0x0          | 0x4  | Magicnum "HFS0"          |
| 0x4          | 0x4  | Number of files          |
| 0x8          | 0x4  | Size of the string table |
| 0xC          | 0x4  | Zero/Reserved            |
| 0x10         | X    | File Entry Table         |
| 0x10 + X     | Y    | String Table             |
| 0x10 + X + Y | Z    | Raw File Data            |

Where File Entry Table consists of Number of Files
FileEntries:

| Offset | Size | Description                                                                                                             |
| ------ | ---- | ----------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x8  | Offset of file in Data                                                                                                  |
| 0x8    | 0x8  | Size of file in Data                                                                                                    |
| 0x10   | 0x4  | Offset of filename in String Table                                                                                      |
| 0x14   | 0x4  | Size of Hashed region of file (for HFS0s, this is the size of the pre-filedata portion, for NCAs this is usually 0x200) |
| 0x18   | 8    | Zero/Reserved                                                                                                           |
| 0x20   | 0x20 | SHA-256 hash of the first (size of hashed region) bytes of filedata                                                     |

The string table is 00-padded to align the start of raw filedata with a
sector/media unit boundary (usually?).

# Cartridge Layout

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

The entire rest of the Gamecard after the secure partition ends is all
FF padding.

\[4.0.0+\] The "normal" partition is now empty and a new partition
"logo" was added.

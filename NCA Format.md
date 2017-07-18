The entire raw NCAs are encrypted.

The only known area which is not encrypted in the raw NCA is the logo
section, when the NCA includes that section. Everything else documented
on this page is for the plaintext version of that data.

# Encryption

The first {at least 0xC00 bytes} are encrypted with AES-XTS with sector
size 0x200, at least 6 sectors in total. Everything in this region uses
same
keydata.

# Header

| Offset | Size            | Description                                                                                                                                               |
| ------ | --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x100           | RSA-2048 signature over the 0x200-bytes starting at offset 0x200 using fixed key.                                                                         |
| 0x100  | 0x100           | RSA-2048 signature over the 0x200-bytes starting at offset 0x200 using key from [NPDM](NPDM.md "wikilink"), or zeroes if not a program.                   |
| 0x200  | 0x4             | Magicnum "NCA3"                                                                                                                                           |
| 0x204  | 0x1             | Distribution Type (0=Download, 1=GameCard)                                                                                                                |
| 0x205  | 0x1             | Content Type (0=Program, 1=Meta, 2=Control, 3=Manual, 4=Data)                                                                                             |
| 0x206  | 0x1             | Crypto Type (0=Auto, 1=None, 2=Unknown added with [3.0.0](3.0.0.md "wikilink"), used with ncatype1(not used for ncatype0, unknown for others), 3=AES-CTR) |
| 0x207  | 0x1             | Key index                                                                                                                                                 |
| 0x208  | 0x8             | Size of the entire NCA.                                                                                                                                   |
| 0x210  | 0x8             | titleID                                                                                                                                                   |
| 0x21C  | 0x4             | Version value? Compared with a required minimum-value.                                                                                                    |
| 0x230  | 0x10            | Rights ID ([Ticket](Ticket.md "wikilink"))                                                                                                                |
| 0x240  | 0x10\*0x4(0x40) | Table for each section, see below.                                                                                                                        |
| 0x280  | 0x20\*0x4(0x80) | Table of SHA256 hashes, over each 0x200-byte Section Header Block.                                                                                        |
| 0x300  | 0x10\*0x4(0x40) | Key area                                                                                                                                                  |

The header is 0x400-bytes, at NCA+0.

## Section Table Entry

| Offset | Size | Description      |
| ------ | ---- | ---------------- |
| 0x0    | 0x4  | Media offset     |
| 0x4    | 0x4  | Media end-offset |
| 0x8    | 0x4  | Unknown          |
| 0xC    | 0x4  | Unknown          |

Entry size is 0x10-bytes.

Media offset is absoluteoffset/{mediasize}, where mediasize is
hard-coded to
0x200.

# Section Header Block

| Offset | Size | Description                                                                                                              |
| ------ | ---- | ------------------------------------------------------------------------------------------------------------------------ |
| 0x0    | 0x1  | ?                                                                                                                        |
|        |      |                                                                                                                          |
| 0x1    | 0x1  | ?                                                                                                                        |
| 0x2    | 0x1  | ?                                                                                                                        |
| 0x3    | 0x1  | Filesystem type. 0x2 = PFS0, 0x3 = RomFS, everything else is invalid.                                                    |
| 0x4    | 0x1  | Crypto type. 0 and \>4 are invalid. 1 = none(plaintext from raw NCA). 2 = other crypto. 3 = regular crypto. 4 = unknown. |
| 0x5    | 0x1  | Padding?                                                                                                                 |
| 0x8    |      | FS-specific superblock.                                                                                                  |

The Section Header Block for each section is at
absoluteoffset+0x400+(sectionid\*0x200), where sectionid corresponds to
the index used with the entry/hash tables.

The total size is
0x200-bytes.

## PFS0 superblock

| Offset | Size | Description                                                                        |
| ------ | ---- | ---------------------------------------------------------------------------------- |
| 0x8    | 0x20 | SHA256 hash over the hash-table at section-start+0 with the below hash-table size. |
| 0x28   | 0x4  | Block size in bytes.                                                               |
| 0x2C   | 0x4  | Must be 0x2.                                                                       |
| 0x30   | 0x8  | Offset of hash-table. Normally zero?                                               |
| 0x38   | 0x8  | Size of hash-table.                                                                |
| 0x40   | 0x8  | Offset relative to section-start where the PFS0 header is located.                 |
| 0x48   | 0x8  | Actual byte-size of the PFS0 filesystem relative to the PFS0 header.               |
| 0x50   | 0xF4 | Normally zeros.                                                                    |
| 0x144  | ?    | 0x1?                                                                               |
| 0x148  | 0xB8 | Normally zeros.                                                                    |

This documents the structure of Section Header Block +0 for
PFS0.

## RomFS superblock

| Offset | Size | Description                                                                                                                              |
| ------ | ---- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| 0x8    | 0xE0 | IVFC header. Basically the same as [Savegames](Savegames.md "wikilink") IVFC except with 2 more levels and +0x0C is non-zero, see below. |

This documents the structure of Section Header Block +0 for
RomFS.

### IVFC

| Start | Length | Description                                                           |
| ----- | ------ | --------------------------------------------------------------------- |
| 0x00  | 4      | Magic ("IVFC")                                                        |
| 0x04  | 4      | Magic Number (0x20000)                                                |
| 0x08  | 4      | Master hash size?                                                     |
| 0x0C  | 4      | Usually 7? Unknown, could be related to total number of levels maybe? |
| 0x10  | 8      | Level 1 offset                                                        |
| 0x18  | 8      | Level 1 size                                                          |
| 0x20  | 4      | Level 1 block size, in log2                                           |
| 0x24  | 4      | Reserved                                                              |
| 0x28  | 8      | Level 2 offset                                                        |
| 0x30  | 8      | Level 2 size                                                          |
| 0x38  | 4      | Level 2 block size, in log2.                                          |
| 0x3C  | 4      | Reserved                                                              |
| 0x40  | 8      | Level 3 offset                                                        |
| 0x48  | 8      | Level 3 size                                                          |
| 0x50  | 4      | Level 3 block size, in log2.                                          |
| 0x54  | 4      | Reserved                                                              |
| 0x58  | 8      | Level 4 offset                                                        |
| 0x60  | 8      | Level 4 size                                                          |
| 0x68  | 4      | Level 4 block size, in log2.                                          |
| 0x6C  | 4      | Reserved                                                              |
| 0x70  | 8      | Level 5 offset                                                        |
| 0x78  | 8      | Level 5 size                                                          |
| 0x80  | 4      | Level 5 block size, in log2.                                          |
| 0x84  | 4      | Reserved                                                              |
| 0x88  | 8      | Level 6 offset                                                        |
| 0x90  | 8      | Level 6 size                                                          |
| 0x98  | 4      | Level 6 block size, in log2.                                          |
| 0x9C  | 4      | Reserved                                                              |
| 0xA0  | 32     | Unknown, reserved?                                                    |
| 0xC0  | 32     | Hash                                                                  |

# Logo section

This is a PFS0. See [here](NCA%20Content%20FS.md "wikilink") for the
mounted-FS logo contents.

# ExeFS section

This is a PFS0.

See [here](ExeFS.md "wikilink") for mounted-FS ExeFS
contents.

# PFS0

| Offset                                       | Size                              | Description                              |
| -------------------------------------------- | --------------------------------- | ---------------------------------------- |
| {Hash-table offset from superblock}          | {Hash-table size from superblock} | Table of SHA256 hashes.                  |
| {Hash-table \<offset+size\> from superblock} |                                   | Zeros for alignment to {alignment size}. |
| {PFS0 offset from superblock}                | {PFS0 size from superblock}       | The actual PFS0.                         |

This is the FS which has magicnum "PFS0" at header+0. This is very
similar to [HFS0](Gamecard%20Format.md "wikilink").

The hash table is hashes for every {Block size from superblock} starting
at the PFS0 header. The size used for the last hash is {PFS0 filesystem
size from superblock} - offset\_relativeto\_header.

See also the PFS0 superblock above.

| Offset       | Size | Description              |
| ------------ | ---- | ------------------------ |
| 0x0          | 0x4  | "PFS0" Magic             |
| 0x4          | 0x4  | Number of files          |
| 0x8          | 0x4  | Size of the string table |
| 0xC          | 0x4  | Zero/Reserved            |
| 0x10         | X    | File Entry Table         |
| 0x10 + X     | Y    | String Table             |
| 0x10 + X + Y | Z    | Raw File Data            |

Where File Entry Table consists of Number of Files FileEntries:

| Offset | Size | Description                        |
| ------ | ---- | ---------------------------------- |
| 0x0    | 0x8  | Offset of file in Data             |
| 0x8    | 0x8  | Size of file in Data               |
| 0x10   | 0x4  | Offset of filename in String Table |
| 0x14   | 0x4  | Normally zero?                     |

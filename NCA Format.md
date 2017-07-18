The entire raw NCAs are encrypted.

The only known area which is not encrypted in the raw NCA is the logo
section, when the NCA includes that section. Everything else documented
on this page is for the plaintext version of that
data.

# Header

| Offset | Size            | Description                                                                                                                             |
| ------ | --------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x100           | RSA-2048 signature over the 0x200-bytes starting at offset 0x200 using fixed key.                                                       |
| 0x100  | 0x100           | RSA-2048 signature over the 0x200-bytes starting at offset 0x200 using key from [NPDM](NPDM.md "wikilink"), or zeroes if not a program. |
| 0x200  | 0x4             | Magicnum "NCA3"                                                                                                                         |
| 0x204  | 0x3             | ?                                                                                                                                       |
| 0x207  | 0x1             | Key index                                                                                                                               |
| 0x208  | 0x8             | Size of the entire NCA.                                                                                                                 |
| 0x210  | 0x8             | titleID                                                                                                                                 |
| 0x230  | 0x10            | Rights ID ([Ticket](Ticket.md "wikilink"))                                                                                              |
| 0x240  | 0x10\*0x4(0x40) | Table for each section, see below.                                                                                                      |
| 0x280  | 0x20\*0x4(0x80) | Table of SHA256 hashes, over each 0x200-byte Section Header Block.                                                                      |
| 0x300  | 0x10\*0x4(0x40) | Key area                                                                                                                                |

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
| 0x3    | 0x1  | ?                                                                                                                        |
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
| 0x2C   | 0x4  | ?                                                                                  |
| 0x38   | 0x8? | Size of hash-table.                                                                |
| 0x40   | 0x8? | Offset relative to section-start where the PFS0 header is located.                 |
| 0x48   | 0x8  | Actual byte-size of the PFS0 filesystem relative to the PFS0 header.               |
| 0x50   | 0xF4 | Normally zeros.                                                                    |
| 0x144  | ?    | 0x1?                                                                               |
| 0x148  | 0xB8 | Normally zeros.                                                                    |

This documents the structure of Section Header Block +0 for PFS0.

## RomFS superblock

| Offset | Size | Description |
| ------ | ---- | ----------- |
| 0x8    |      | IVFC header |

This documents the structure of Section Header Block +0 for RomFS.

# Logo section

This is a PFS0. See [here](NCA%20Content%20FS.md "wikilink") for the
mounted-FS logo contents.

# ExeFS section

This is a PFS0.

See [here](ExeFS.md "wikilink") for mounted-FS ExeFS contents.

# PFS0

| Offset | Size | Description                              |
| ------ | ---- | ---------------------------------------- |
| 0x0    | X    | Table of SHA256 hashes.                  |
| X      | Y    | Zeros for alignment to {alignment size}. |
| X+Y    |      | Start of the PFS0 header.                |

This is the FS which has magicnum "PFS0" at header+0.

The hash table is hashes for every {Block size from superblock} starting
at the PFS0 header. The size used for the last hash is {PFS0 filesystem
size from superblock} - offset\_relativeto\_header.

See also the PFS0 superblock above.

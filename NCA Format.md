The entire raw NCAs are encrypted.

The only known area which is not encrypted in the raw NCA is the logo
section, when the NCA includes that section. Everything else documented
on this page is for the plaintext version of that data.

# Encryption

The first 0xC00 bytes are encrypted with AES-XTS with sector size 0x200
with a non-standard "tweak" (endianness is reversed, see
[here](https://gist.github.com/SciresM/fe8a631d13c069bd66e9c656ab5b3f7f)),
this encrypted data is an 0x400 NCA header + an 0x200 header for each
section in the section table.

For pre-1.0.0 "NCA2" NCAs, the first 0x400 byte are encrypted the same
way as in NCA3. However, each section header is individually encrypted
as though it were sector 0, instead of the appropriate sector as in
NCA3.

# Header

| Offset | Size            | Description                                                                                                                                                                                                                                                                                                                             |
| ------ | --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x100           | RSA-2048 signature over the header (data from 0x200 to 0x400) using a fixed key                                                                                                                                                                                                                                                         |
| 0x100  | 0x100           | RSA-2048 signature over the header (data from 0x200 to 0x400) using a key from [NPDM](NPDM.md "wikilink") (or zeroes if not a program)                                                                                                                                                                                                  |
| 0x200  | 0x4             | Magicnum "NCA3" ("NCA2", "NCA1" or "NCA0" for pre-1.0.0 NCAs)                                                                                                                                                                                                                                                                           |
| 0x204  | 0x1             | Distribution Type (0x00 = System NCA, 0x01 = Gamecard NCA)                                                                                                                                                                                                                                                                              |
| 0x205  | 0x1             | Content Type (0x00 = Program, 0x01 = Meta, 0x02 = Control, 0x03 = Manual, 0x04 = Data, 0x05 = PublicData)                                                                                                                                                                                                                               |
| 0x206  | 0x1             | Old Key Generation (0x00 = [1.0.0](1.0.0.md "wikilink"), 0x01 = Unused, 0x02 = [3.0.0](3.0.0.md "wikilink"))                                                                                                                                                                                                                            |
| 0x207  | 0x1             | Key Area Encryption Key Index (0x00 = Application, 0x01 = Ocean, 0x02 = System)                                                                                                                                                                                                                                                         |
| 0x208  | 0x8             | Size of the entire NCA                                                                                                                                                                                                                                                                                                                  |
| 0x210  | 0x8             | Title ID                                                                                                                                                                                                                                                                                                                                |
| 0x218  | 0x4             | Content Index                                                                                                                                                                                                                                                                                                                           |
| 0x21C  | 0x4             | SDK AddOn Version (used in "FS\_ACCESS: { sdk\_version: {byte3}.{byte2}.{byte1}, ..." with byte0 set to 0 and compared with a required minimum value: 0x000B0000)                                                                                                                                                                       |
| 0x220  | 0x1             | Key Generation (0x03 = [3.0.1](3.0.1.md "wikilink"), 0x04 = [4.0.0](4.0.0.md "wikilink"), 0x05 = [5.0.0](5.0.0.md "wikilink"), 0x06 = [6.0.0](6.0.0.md "wikilink"), 0x07 = [6.2.0](6.2.0.md "wikilink"), 0x08 = [7.0.0](7.0.0.md "wikilink"), 0x09 = [8.1.0](8.1.0.md "wikilink"), 0x0A = [9.0.0](9.0.0.md "wikilink"), 0xFF = Invalid) |
| 0x230  | 0x10            | Rights ID ([Ticket](Ticket.md "wikilink"))                                                                                                                                                                                                                                                                                              |
| 0x240  | 0x10\*0x4(0x40) | Table for each section (see below)                                                                                                                                                                                                                                                                                                      |
| 0x280  | 0x20\*0x4(0x80) | Table of SHA256 hashes (over each 0x200-byte [Section Header Block](#Section_Header_Block "wikilink"))                                                                                                                                                                                                                                  |
| 0x300  | 0x10\*0x4(0x40) | Key area                                                                                                                                                                                                                                                                                                                                |

The header is 0x400-bytes, at NCA+0.

When the above **Old Key Generation** field is 0x2 on \>= v3.0,
different {crypto/keydata} is used for the sections' data. With system
content, this is used with every ncatype except ncatype0. The only other
exception is {data-content} for the firm titles: this is required in
order for older-system-versions to install it.

**Key Generation** 0x3 (with **Old Key Generation** set to 0x2) is used
for all [3.0.1](3.0.1.md "wikilink") sysmodules and the
[System\_Version\_Title](System%20Version%20Title.md "wikilink"). With
[3.0.2](3.0.2.md "wikilink"), all updated titles use the crypto from
[3.0.1](3.0.1.md "wikilink") for non-ncatype0, except for firm
{data-content}. In some cases various game content uses the above newer
crypto as well.

**Key Generation** is always **Master Key Version** + 1, except for
generations 0 and 1 which are both version 0.

The keyindex passed to <key-generation-related code> is determined as
follows:

  - Pre-[3.0.0](3.0.0.md "wikilink"): The **Key Area Encryption Key
    Index** field (0x207) is passed directly.
  - [3.0.0](3.0.0.md "wikilink")+: It's determined using the **Key Area
    Encryption Key Index** field (0x207) and the **Old Key Generation**
    field (0x206). The latter field must be 0, 1 or 2. In each
    ncahdr\_keyindex block, it executes "if(ncahdr\_x206\>=3)<panic>",
    but that won't trigger due to the earlier check. The end result is
    basically the same as pre-[3.0.0](3.0.0.md "wikilink"), except when
    ncahdr\_x206 == 0x2, final\_index is
    new\_base\_index+ncahdr\_keyindex. Actual implementation loads index
    from u32\_array\[ncahdr\_crypto\_type\], where the address of
    u32\_array is different for each ncahdr\_keyindex.
  - [3.0.1](3.0.1.md "wikilink")+: The dedicated range check for the
    **Old Key Generation** field (0x206) was removed, since the updated
    code no longer needs it. The output from a function masked with 0xFF
    is now used instead of ncahdr\_x206. The range check for that field
    was changed from {ncahdr\_x206 check with panic described above}, to
    "if(index\>=4)final\_index=10;"(skips accessing the array and uses
    10 directly). The arrays were updated with an additional entry:
    final\_index=v301\_base\_index+ncahdr\_keyindex.
      - The keydata for the above index10 is not(?) known to be
        initialized.
      - The new function called by the code described above does:
      - `if(ncahdr_x206 < ncahdr_x220){ret = ncahdr_x220; } else { ret =
        ncahdr_x206; } return ret;`

## Section Table Entry

| Offset | Size | Description        |
| ------ | ---- | ------------------ |
| 0x0    | 0x4  | Media Start Offset |
| 0x4    | 0x4  | Media End Offset   |
| 0x8    | 0x4  | Unknown            |
| 0xC    | 0x4  | Unknown            |

Entry size is 0x10-bytes.

Media offset is absoluteoffset/{mediasize}, where mediasize is 0x200
bytes.

# Section Header Block

| Offset | Size | Description                                                                                            |
| ------ | ---- | ------------------------------------------------------------------------------------------------------ |
| 0x0    | 0x2  | Version (always 2)                                                                                     |
| 0x2    | 0x1  | Filesystem Type (0 = RomFS, 1 = PFS0)                                                                  |
| 0x3    | 0x1  | Hash Type (2 = PFS0, 3 = RomFS)                                                                        |
| 0x4    | 0x1  | Encryption Type (1 = None, 2 = AesCtrOld, 3 = AesCtr, 4 = AesCtrEx)                                    |
| 0x5    | 0x1  | Padding                                                                                                |
| 0x8    | 0xF8 | FS-specific superblock                                                                                 |
| 0x100  | ?    | Optional BKTR header (can be used with any section, but only known to be used with game-updates RomFS) |

The Section Header Block for each section is at
absoluteoffset+0x400+(sectionid\*0x200), where sectionid corresponds to
the index used with the entry/hash tables.

The total size is 0x200-bytes.

## PFS0 superblock

| Offset | Size | Description                                                                       |
| ------ | ---- | --------------------------------------------------------------------------------- |
| 0x0    | 0x20 | SHA256 hash over the hash-table at section-start+0 with the below hash-table size |
| 0x20   | 0x4  | Block size in bytes                                                               |
| 0x24   | 0x4  | Must be 0x2                                                                       |
| 0x28   | 0x8  | Offset of hash-table (normally zero)                                              |
| 0x30   | 0x8  | Size of hash-table                                                                |
| 0x38   | 0x8  | Offset relative to section-start where the PFS0 header is located                 |
| 0x40   | 0x8  | Actual byte-size of the PFS0 filesystem relative to the PFS0 header               |
| 0x48   | 0xB0 | Empty                                                                             |

## RomFS superblock

| Offset | Size | Description                                                                                                                              |
| ------ | ---- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| 0x8    | 0xE0 | IVFC header (basically the same as [Savegames](Savegames.md "wikilink") IVFC except with 2 more levels and +0x0C is non-zero, see below) |

This documents the structure of Section Header Block +0 for RomFS.

### IVFC

| Start | Length | Description                                                           |
| ----- | ------ | --------------------------------------------------------------------- |
| 0x00  | 4      | Magicnum "IVFC"                                                       |
| 0x04  | 4      | Magic Number (0x20000)                                                |
| 0x08  | 4      | Master hash size?                                                     |
| 0x0C  | 4      | Usually 7? Unknown, could be related to total number of levels maybe? |
| 0x10  | 8      | Level 1 offset                                                        |
| 0x18  | 8      | Level 1 size                                                          |
| 0x20  | 4      | Level 1 block size (in log2)                                          |
| 0x24  | 4      | Reserved                                                              |
| 0x28  | 8      | Level 2 offset                                                        |
| 0x30  | 8      | Level 2 size                                                          |
| 0x38  | 4      | Level 2 block size (in log2)                                          |
| 0x3C  | 4      | Reserved                                                              |
| 0x40  | 8      | Level 3 offset                                                        |
| 0x48  | 8      | Level 3 size                                                          |
| 0x50  | 4      | Level 3 block size (in log2)                                          |
| 0x54  | 4      | Reserved                                                              |
| 0x58  | 8      | Level 4 offset                                                        |
| 0x60  | 8      | Level 4 size                                                          |
| 0x68  | 4      | Level 4 block size (in log2)                                          |
| 0x6C  | 4      | Reserved                                                              |
| 0x70  | 8      | Level 5 offset                                                        |
| 0x78  | 8      | Level 5 size                                                          |
| 0x80  | 4      | Level 5 block size (in log2)                                          |
| 0x84  | 4      | Reserved                                                              |
| 0x88  | 8      | Level 6 offset                                                        |
| 0x90  | 8      | Level 6 size                                                          |
| 0x98  | 4      | Level 6 block size (in log2)                                          |
| 0x9C  | 4      | Reserved                                                              |
| 0xA0  | 32     | Unknown, reserved?                                                    |
| 0xC0  | 32     | Hash                                                                  |

## BKTR

| Start | Length | Description                                              |
| ----- | ------ | -------------------------------------------------------- |
| 0x0   | 0x8    | Offset                                                   |
| 0x8   | 0x8    | Size                                                     |
| 0x10  | 0x4    | Magicnum "BKTR"                                          |
| 0x14  | 0x4    | u32, must be \<=1.                                       |
| 0x18  | 0x4    | s32, must be \>=1.                                       |
| 0x1C  | 0x4    | ?                                                        |
| 0x20  | 0x20   | Same as the above 0x20-bytes except with different data. |
| 0x40  | 0x4?   | ?                                                        |
| 0x44  | 0x4?   | ?                                                        |

Using this header is enabled when offset 0x8 in this header is non-zero.

The above byte-offsets are relative to the start of the section-data.

The two sections specified by the two BKTR entries are usually(?) at the
very end of the section data(section\_endoffset-{size of BKTR
sections}).

### RomFS Patching

The BKTR section enables combining data from an update NCA with the
RomFS from a base NCA to create a single patched RomFS image.

The first BKTR entry describes how to map regions of the two RomFS
images to create the patched RomFS. It has the following format:

| Start  | Length    | Description                                                          |
| ------ | --------- | -------------------------------------------------------------------- |
| 0x0    | 0x4       | Padding/Unused?                                                      |
| 0x4    | 0x4       | Number of Buckets                                                    |
| 0x8    | 0x8       | Total Size of the Virtual RomFS Image                                |
| 0x10   | 0x3FF0    | Base Virtual Offset for each Bucket (u64s, padded with 0s until end) |
| 0x4000 | 0x4000\*X | Relocation Buckets                                                   |

Where relocation buckets are as follows:

| Start | Length | Description                |
| ----- | ------ | -------------------------- |
| 0x0   | 0x4    | Padding/Unused?            |
| 0x4   | 0x4    | Number of Entries          |
| 0x8   | 0x8    | End offset for this Bucket |
| 0x10  | 0x3FF0 | Relocation Entries         |

Where relocation entries are as follows:

| Start | Length | Description                                 |
| ----- | ------ | ------------------------------------------- |
| 0x0   | 0x8    | Address in Patched RomFS                    |
| 0x8   | 0x8    | Address in Source RomFS                     |
| 0x10  | 0x4    | 1=Is from Patch RomFS, 0=Is from Base RomFS |

The second BKTR entry describes the subsections within the Patch RomFS.
It has the following format:

| Start  | Length    | Description                                                           |
| ------ | --------- | --------------------------------------------------------------------- |
| 0x0    | 0x4       | Padding/Unused?                                                       |
| 0x4    | 0x4       | Number of Buckets                                                     |
| 0x8    | 0x8       | Total Size of the Physical Patch Image                                |
| 0x10   | 0x3FF0    | Base Physical Offset for each Bucket (u64s, padded with 0s until end) |
| 0x4000 | 0x4000\*X | Subsection Buckets                                                    |

Where subsection buckets are as follows:

| Start | Length | Description                |
| ----- | ------ | -------------------------- |
| 0x0   | 0x4    | Padding/Unused?            |
| 0x4   | 0x4    | Number of Entries          |
| 0x8   | 0x8    | End offset for this Bucket |
| 0x10  | 0x3FF0 | Subsection Entries         |

Where subsection entries are as follows:

| Start | Length | Description                  |
| ----- | ------ | ---------------------------- |
| 0x0   | 0x8    | Address in Patch RomFS       |
| 0x8   | 0x4    | Padding/Unused?              |
| 0xC   | 0x4    | Value for subsection AES-CTR |

Official code assumes the relocation entries are sorted, and performs a
binary search when determining where to read from. Each subsection in
the Patch RomFS has its CTR calculated separately from the others based
on the value in its entry (the BKTR entries use normal crypto). Thus
decrypting a Patch RomFS requires decrypting and parsing the BKTR
entries before anything else.

# Logo section

This is a PFS0.

See [here](NCA%20Content%20FS.md "wikilink") for the mounted-FS logo
contents.

# ExeFS section

This is a PFS0.

See [here](ExeFS.md "wikilink") for mounted-FS ExeFS contents.

# Game-updates

The section-data for ncatype1 RomFS section(section1) uses
section-crypto-type 0x4.

Game-updates also contain multiple ncatype6 content, which contain
"section0\_pfs0/fragment". Some of these are just NCAs, unknown for the
rest(presumably NCAs with additional crypto?). The first ncatype6
content fragment file has a NDV0 header, with the NCA starting at offset
0x44.

# PFS0

| Offset                                       | Size                              | Description                              |
| -------------------------------------------- | --------------------------------- | ---------------------------------------- |
| {Hash-table offset from superblock}          | {Hash-table size from superblock} | Table of SHA256 hashes.                  |
| {Hash-table \<offset+size\> from superblock} |                                   | Zeros for alignment to {alignment size}. |
| {PFS0 offset from superblock}                | {PFS0 size from superblock}       | The actual PFS0.                         |

This is the FS which has magicnum "PFS0" at header+0. This is very
similar to [HFS0](Gamecard%20Format.md "wikilink"). A tool for
extracting this FS is available
[here](https://gist.github.com/yellows8/1a96c2b846f4ebc4bb45d7f7fa1eb7db).

The hash table is hashes for every {Block size from superblock} starting
at the PFS0 header. The size used for the last hash is {PFS0 filesystem
size from superblock} - offset\_relativeto\_header.

See also the PFS0 superblock above.

| Offset       | Size | Description              |
| ------------ | ---- | ------------------------ |
| 0x0          | 0x4  | Magicnum "PFS0"          |
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

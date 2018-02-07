Present in the firmware package titles (0100000000000819,
010000000000081A, 010000000000081B and 010000000000081C) and installed
into eMMC storage's [BCPKG2
partitions](Flash%20Filesystem#User%20Partitions.md##User_Partitions "wikilink"),
"package2" contains the Switch kernel and the built-in system modules.

# Format

Package2 is distributed in an already encrypted format. Therefore, it's
not additionally encrypted when installed into the flash
filesystem.

| Offset | Size     | Description                                                                                |
| ------ | -------- | ------------------------------------------------------------------------------------------ |
| 0x0    | 0x100    | [RSA-2048](#Public_Keys "wikilink") signature (PKCS\#1 v2.1 RSASSA-PSS-VERIFY with SHA256) |
| 0x100  | 0x100    | Encrypted header                                                                           |
| 0x200  | Variable | Encrypted body                                                                             |

## Encryption

Package2's contents are AES-CTR encrypted with a key known only by
TrustZone.

The encrypted header's CTR is stored as it's first 0x10 bytes (offset
0x100). The encrypted body is divided in up to 4 sections, each one with
a CTR stored inside the decrypted header.

## Header

When decrypted, package2's header is as
follows.

| Offset | Size | Description                                                                                                                                                  |
| ------ | ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 0x0    | 0x10 | Header's CTR, official code copies the pre-decryption CTR over the decrypted result. Also used as metadata.                                                  |
| 0x10   | 0x10 | Section 0 CTR                                                                                                                                                |
| 0x20   | 0x10 | Section 1 CTR                                                                                                                                                |
| 0x30   | 0x10 | Section 2 CTR                                                                                                                                                |
| 0x40   | 0x10 | Section 3 CTR                                                                                                                                                |
| 0x50   | 0x4  | Magic "PK21"                                                                                                                                                 |
| 0x54   | 0x4  | Base offset                                                                                                                                                  |
| 0x58   | 0x4  | Always 0                                                                                                                                                     |
| 0x5C   | 0x2  | Version. HighByte must be \<{maxver} and LowByte must be \>{minver}, where {maxver} and {minver} are constants used by TZ updated with each package1 update. |
| 0x5E   | 0x2  | Padding                                                                                                                                                      |
| 0x60   | 0x4  | Section 0 size                                                                                                                                               |
| 0x64   | 0x4  | Section 1 size                                                                                                                                               |
| 0x68   | 0x4  | Section 2 size                                                                                                                                               |
| 0x6C   | 0x4  | Section 3 size                                                                                                                                               |
| 0x70   | 0x4  | Section 0 offset                                                                                                                                             |
| 0x74   | 0x4  | Section 1 offset                                                                                                                                             |
| 0x78   | 0x4  | Section 2 offset                                                                                                                                             |
| 0x7C   | 0x4  | Section 3 offset                                                                                                                                             |
| 0x80   | 0x20 | SHA-256 hash over encrypted section 0                                                                                                                        |
| 0xA0   | 0x20 | SHA-256 hash over encrypted section 1                                                                                                                        |
| 0xC0   | 0x20 | SHA-256 hash over encrypted section 2                                                                                                                        |
| 0xE0   | 0x20 | SHA-256 hash over encrypted section 3                                                                                                                        |

Each section follows each other immediately and is encrypted with the
same key used for encrypting the header. The section offsets are
relative to a base, which is typically 0x80000000 pointing to the base
of DRAM.

Before being decrypted, the encrypted header's CTR additionally encodes
metadata used to validate package2's contents as follows:

  - Size of the entire package2 with the raw header = ctr\_word2 ^
    ctr\_word3 ^ ctr\_word0
  - Metadata version field = ((ctr\_word1 ^ (ctr\_word1 \>\> 16)) &
    0xFF) ^ (ctr\_word1 \>\> 24)

In \[4.0.0\], the metadata version field must be less or equal to 4.

## Section 0

When decrypted, this section contains the plaintext Switch kernel
binary.

## Section 1

When decrypted, this section contains the built-in system modules
encapsulated in a custom format.

### INI1

| Offset | Type | Description     |
| ------ | ---- | --------------- |
| 0x0    | u32  | Magic "INI1"    |
| 0x4    | u32  | Size            |
| 0x8    | u32  | NumberProcesses |
| 0xC    | u32  | Padding (zero)  |

#### KIP1

Kernel internal
process?

| Offset | Type                                              | Description                                                                                                                                                          |
| ------ | ------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | u32                                               | Magic "KIP1"                                                                                                                                                         |
| 0x4    | char\[12\]                                        | Name                                                                                                                                                                 |
| 0x10   | u64                                               | TitleId                                                                                                                                                              |
| 0x18   | u32                                               | Process category (0: regular title, 1: kernel built-in). Should be 1 here.                                                                                           |
| 0x1C   | u8                                                | Main thread priority                                                                                                                                                 |
| 0x1D   | u8                                                | Default CPU core                                                                                                                                                     |
| 0x1E   | u8                                                | Reserved (unused)                                                                                                                                                    |
| 0x1F   | u8                                                | Flags: bit0-2: compression-enable for each section, when set. Bit3: Is64Bit. Bit4: IsAddrSpace36Bit. Bit5: \[2.0.0+\] PoolPartitionId. Bit6, Bit7: reserved (unused) |
| 0x20   | [\#SectionHeader](#SectionHeader "wikilink")\[6\] | Sections: .text, .rodata, .data, .bss and two reserved (ignored) sections.                                                                                           |
| 0x80   | u32\[0x20\]                                       | KernelCaps                                                                                                                                                           |

##### SectionHeader

| Offset | Type | Description                                                                              |
| ------ | ---- | ---------------------------------------------------------------------------------------- |
| 0x0    | u32  | OutOffset                                                                                |
| 0x4    | u32  | DecompressedSize                                                                         |
| 0x8    | u32  | CompressedSize                                                                           |
| 0xC    | u32  | Attribute: the size in pages of the main thread's stack for .rodata, reserved otherwise. |

Compressed size can be 0 or lower than exepected, this is the case for
BSS for example.

##### Compression

The compression used here is BLZ, with a modified footer since 3ds. The
footer is now 0xC bytes instead of 0x8, and has the form u32
compressed\_data\_len; u32 initial\_index; u32
additional\_len\_when\_uncompressed;

## Section 2

This section has a valid CTR and SHA-256 hash (over NULL) stored in the
package2's header, but it's size is always 0. Likely reserved for future
expansion.

## Section 3

This section is not present (CTR and SHA-256 hash in package2's header
are NULL). Likely reserved for future
expansion.

# Versions

| System version               | Package1 maxver constant | Package1 minver constant | Package2 version field |
| ---------------------------- | ------------------------ | ------------------------ | ---------------------- |
| [1.0.0](1.0.0.md "wikilink") | 0x2                      | 0x3                      | 0x0104                 |
| [2.0.0](2.0.0.md "wikilink") | 0x3                      | 0x4                      | 0x0205                 |
| [3.0.0](3.0.0.md "wikilink") | 0x4                      | 0x5                      | 0x0306                 |
| [3.0.2](3.0.2.md "wikilink") | 0x5                      | 0x6                      | 0x0407                 |
| [4.0.0](4.0.0.md "wikilink") | 0x6                      | 0x7                      | 0x0508                 |

# Public Keys

### Exponent

`0x10001`

### Retail Modulus

    00000000: 8D13A777 6AE5DCC0 3B25D058 E4206959  ..§wjåÜÀ;%ÐXä iY
    00000010: 554BAB70 40082807 A8A7FD0F 312E11FE  UK«p@.(.¨§ý.1..þ
    00000020: 47A0F99D DF80DB86 5A2789CD 976C85C5  G ù.ß€Û†Z'‰Í—l…Å
    00000030: 6C397F41 F2FF2420 C395A6F7 9D4A4574  l9.Aòÿ$ Ã•¦÷.JEt
    00000040: 8B5D288A C6993568 85A56432 809FD348  ‹](ŠÆ™5h…¥d2€ŸÓH
    00000050: 39A21D24 6769DF75 AC12B5BD C32990BE  9¢.$gißu¬.µ½Ã).¾
    00000060: 37E4A080 9ABE36BF 1F2CAB2B ADF59732  7ä €š¾6¿.,«+.õ—2
    00000070: 9A429D09 8B08F063 47A3E91B 36D82D8A  šB..‹.ðcG£é.6Ø-Š
    00000080: D7E15411 95E44588 698A2B35 CED0A50B  ×áT.•äEˆiŠ+5ÎÐ¥.
    00000090: D55DACDB AF114DCA B81EE701 9EF446A3  Õ]¬Û¯.MÊ¸.ç.žôF£
    000000A0: 8A946D76 BD8AC83B D231580C 79A826E9  Š”mv½ŠÈ;Ò1X.y¨&é
    000000B0: D1799CCB D42B6A4F C6CCCF90 A7B99847  ÑyœËÔ+jOÆÌÏ.§¹˜G
    000000C0: FDFA4C6C 6F81873B CAB850F6 3E395D4D  ýúLlo.‡;Ê¸Pö>9]M
    000000D0: 973F0F35 3953FBFA CDABA87A 629A3FF2  —?.59SûúÍ«¨zbš?ò
    000000E0: 0927963F 079A91F7 16BFC63A 825A4BCF  .'–?.š‘÷.¿Æ:‚ZKÏ
    000000F0: 4950958C 55807E39 B148051E 21C7244F  IP•ŒU€~9±H..!Ç$O

### Debug Modulus

`B3 65 54 FB 0A B0 1E 85 A7 F6 CF 91 8E BA 96 99`  
`0D 8B 91 69 2A EE 01 20 4F 34 5C 2C 4F 4E 37 C7`  
`F1 0B D4 CD A1 7F 93 F1 33 59 CE B1 E9 DD 26 E6`  
`F3 BB 77 87 46 7A D6 4E 47 4A D1 41 B7 79 4A 38`  
`06 6E CF 61 8F CD C1 40 0B FA 26 DC C0 34 51 83`  
`D9 3B 11 54 3B 96 27 32 9A 95 BE 1E 68 11 50 A0`  
`6B 10 A8 83 8B F5 FC BC 90 84 7A 5A 5C 43 52 E6`  
`C8 26 E9 FE 06 A0 8B 53 0F AF 1E C4 1C 0B CF 50`  
`1A A4 F3 5C FB F0 97 E4 DE 32 0A 9F E3 5A AA B7`  
`44 7F 5C 33 60 B9 0F 22 2D 33 2A E9 69 79 31 42`  
`8F E4 3A 13 8B E7 26 BD 08 87 6C A6 F2 73 F6 8E`  
`A7 F2 FE FB 6C 28 66 0D BD D7 EB 42 A8 78 E6 B8`  
`6B AE C7 A9 E2 40 6E 89 20 82 25 8E 3C 6A 60 D7`  
`F3 56 8E EC 8D 51 8A 63 3C 04 78 23 0E 90 0C B4`  
`E7 86 3B 4F 8E 13 09 47 32 0E 04 B8 4D 5B B0 46`  
`71 B0 5C F4 AD 63 4F C5 E2 AC 1E C4 33 96 09 7B`

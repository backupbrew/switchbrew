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

`8D 13 A7 77 6A E5 DC C0 3B 25 D0 58 E4 20 69 59`  
`55 4B AB 70 40 08 28 07 A8 A7 FD 0F 31 2E 11 FE`  
`47 A0 F9 9D DF 80 DB 86 5A 27 89 CD 97 6C 85 C5`  
`6C 39 7F 41 F2 FF 24 20 C3 95 A6 F7 9D 4A 45 74`  
`8B 5D 28 8A C6 99 35 68 85 A5 64 32 80 9F D3 48`  
`39 A2 1D 24 67 69 DF 75 AC 12 B5 BD C3 29 90 BE`  
`37 E4 A0 80 9A BE 36 BF 1F 2C AB 2B AD F5 97 32`  
`9A 42 9D 09 8B 08 F0 63 47 A3 E9 1B 36 D8 2D 8A`  
`D7 E1 54 11 95 E4 45 88 69 8A 2B 35 CE D0 A5 0B`  
`D5 5D AC DB AF 11 4D CA B8 1E E7 01 9E F4 46 A3`  
`8A 94 6D 76 BD 8A C8 3B D2 31 58 0C 79 A8 26 E9`  
`D1 79 9C CB D4 2B 6A 4F C6 CC CF 90 A7 B9 98 47`  
`FD FA 4C 6C 6F 81 87 3B CA B8 50 F6 3E 39 5D 4D`  
`97 3F 0F 35 39 53 FB FA CD AB A8 7A 62 9A 3F F2`  
`09 27 96 3F 07 9A 91 F7 16 BF C6 3A 82 5A 4B CF`  
`49 50 95 8C 55 80 7E 39 B1 48 05 1E 21 C7 24 4F`

### Debug Modulus

    00000000: B36554FB 0AB01E85 A7F6CF91 8EBA9699  ³eTû.°.…§öÏ‘Žº–™
    00000010: 0D8B9169 2AEE0120 4F345C2C 4F4E37C7  .‹‘i*î. O4\,ON7Ç
    00000020: F10BD4CD A17F93F1 3359CEB1 E9DD26E6  ñ.ÔÍ¡.“ñ3YÎ±éÝ&æ
    00000030: F3BB7787 467AD64E 474AD141 B7794A38  ó»w‡FzÖNGJÑA·yJ8
    00000040: 066ECF61 8FCDC140 0BFA26DC C0345183  .nÏa.ÍÁ@.ú&ÜÀ4Qƒ
    00000050: D93B1154 3B962732 9A95BE1E 681150A0  Ù;.T;–'2š•¾.h.P 
    00000060: 6B10A883 8BF5FCBC 90847A5A 5C4352E6  k.¨ƒ‹õü¼.„zZ\CRæ
    00000070: C826E9FE 06A08B53 0FAF1EC4 1C0BCF50  È&éþ. ‹S.¯.Ä..ÏP
    00000080: 1AA4F35C FBF097E4 DE320A9F E35AAAB7  .¤ó\ûð—äÞ2.ŸãZª·
    00000090: 447F5C33 60B90F22 2D332AE9 69793142  D.\3`¹."-3*éiy1B
    000000A0: 8FE43A13 8BE726BD 08876CA6 F273F68E  .ä:.‹ç&½.‡l¦òsöŽ
    000000B0: A7F2FEFB 6C28660D BDD7EB42 A878E6B8  §òþûl(f.½×ëB¨xæ¸
    000000C0: 6BAEC7A9 E2406E89 2082258E 3C6A60D7  k®Ç©â@n‰ ‚%Ž<j`×
    000000D0: F3568EEC 8D518A63 3C047823 0E900CB4  óVŽì.QŠc<.x#...´
    000000E0: E7863B4F 8E130947 320E04B8 4D5BB046  ç†;OŽ..G2..¸M[°F
    000000F0: 71B05CF4 AD634FC5 E2AC1EC4 3396097B  q°\ô.cOÅâ¬.Ä3–.{

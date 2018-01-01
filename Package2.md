Present in the firmware package titles (0100000000000819,
010000000000081A, 010000000000081B and 010000000000081C) and installed
into eMMC storage's [BCPKG2
partitions](Flash%20Filesystem#User%20Partitions.md##User_Partitions "wikilink"),
"package2" contains the Switch kernel and the built-in system modules.

# Format

Package2 is distributed in an already encrypted format. Therefore, it's
not additionally encrypted when installed into the flash
filesystem.

| Offset | Size     | Description                                                     |
| ------ | -------- | --------------------------------------------------------------- |
| 0x0    | 0x100    | RSA-2048 signature (PKCS\#1 v2.1 RSASSA-PSS-VERIFY with SHA256) |
| 0x100  | 0x100    | Encrypted header                                                |
| 0x200  | Variable | Encrypted body                                                  |

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
| 0x0    | 0x10 | Decrypted header's CTR                                                                                                                                       |
| 0x10   | 0x10 | Section 0 CTR                                                                                                                                                |
| 0x20   | 0x10 | Section 1 CTR                                                                                                                                                |
| 0x30   | 0x10 | Section 2 CTR                                                                                                                                                |
| 0x40   | 0x10 | Section 3 CTR                                                                                                                                                |
| 0x50   | 0x4  | Magic "PK21"                                                                                                                                                 |
| 0x54   | 0x4  | Unknown                                                                                                                                                      |
| 0x58   | 0x4  | Unknown                                                                                                                                                      |
| 0x5C   | 0x2  | Version. HighByte must be \<{maxver} and LowByte must be \>{minver}, where {maxver} and {minver} are constants used by TZ updated with each package1 update. |
| 0x5E   | 0x2  | ?                                                                                                                                                            |
| 0x60   | 0x4  | Section 0 size                                                                                                                                               |
| 0x64   | 0x4  | Section 1 size                                                                                                                                               |
| 0x68   | 0x4  | Section 2 size                                                                                                                                               |
| 0x6C   | 0x4  | Section 3 size                                                                                                                                               |
| 0x70   | 0x4  | Unknown                                                                                                                                                      |
| 0x74   | 0x4  | Unknown                                                                                                                                                      |
| 0x78   | 0x4  | Unknown                                                                                                                                                      |
| 0x7C   | 0x4  | Unknown                                                                                                                                                      |
| 0x80   | 0x20 | SHA-256 hash over encrypted section 0                                                                                                                        |
| 0xA0   | 0x20 | SHA-256 hash over encrypted section 1                                                                                                                        |
| 0xC0   | 0x20 | SHA-256 hash over encrypted section 2                                                                                                                        |
| 0xE0   | 0x20 | SHA-256 hash over encrypted section 3                                                                                                                        |

Each section follows each other immediately and is encrypted with the
same key used for encrypting the header.

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
| 0xC    | u32  | Zero            |

#### KIP1

Kernel internal
process?

| Offset | Type                                              | Description                                                               |
| ------ | ------------------------------------------------- | ------------------------------------------------------------------------- |
| 0x0    | u32                                               | Magic "KIP1"                                                              |
| 0x4    | char\[12\]                                        | Name                                                                      |
| 0x10   | u64                                               | TitleId                                                                   |
| 0x18   | u32                                               |                                                                           |
| 0x1C   | u32                                               | Flags / etc. Byte3 bit0-2: compression-enable for each section, when set. |
| 0x20   | [\#SectionHeader](#SectionHeader "wikilink")\[3\] | Sections                                                                  |
| 0x50   | char\[0x20\]                                      | Padding                                                                   |
| 0x70   | u64\[0x20\]                                       | KernelCaps                                                                |

##### SectionHeader

| Offset | Type | Description      |
| ------ | ---- | ---------------- |
| 0x0    | u32  | OutOffset        |
| 0x4    | u32  | DecompressedSize |
| 0x8    | u32  | CompressedSize   |
| 0xC    | u32  |                  |

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
| [2.0.0](2.0.0.md "wikilink") | 0x3                      | 0x4                      |                        |
| [4.1.0](4.1.0.md "wikilink") | 0x6                      | 0x7                      |                        |

This is the Switch equivalent of 3DS exheader. This is the file with
extension ".npdm" in {Switch ExeFS}. The size of this file
varies.

| Offset     | Size       | Description                                                                                    |
| ---------- | ---------- | ---------------------------------------------------------------------------------------------- |
| 0x0        | 0x80       | META                                                                                           |
| 0x80       | 0x200      | RSA-2048 signature, followed a RSA-2048 modulus for [NCA](NCA.md "wikilink") header (like 3DS) |
| 0x280      | <Varies>   | ACID                                                                                           |
| <See META> | <See META> | ACI0                                                                                           |

# META

| Offset | Size | Description                                                             |
| ------ | ---- | ----------------------------------------------------------------------- |
| 0x0    | 0x4  | Magicnum "META".                                                        |
| 0x20   | ?    | Name string                                                             |
| 0x70   | 0x4  | Absolute offset for ACI0.                                               |
| 0x74   | 0x4  | Size of ACI0.                                                           |
| 0x78   | 0x4  | Absolute offset of the RSA signature.                                   |
| 0x7C   | 0x4  | Size used with the above offset. Offset+size is normally ACI0\_start-8. |

Switch version of 3DS "System Control Info"?

# ACID

| Offset | Size        | Description                         |
| ------ | ----------- | ----------------------------------- |
| 0x0    | 0x4         | Magicnum "ACID".                    |
| 0x4    | 0x28        | ?                                   |
| 0x2C   | 0x4         | Size of the Service Access Control. |
| 0x30   | 0x14        | ?                                   |
| 0x44   | ?           | FS Permissions                      |
| 0xF0   | <See above> | Service Access Control              |

Switch version of AccessDesc?

# ACI0

| Offset | Size        | Description                         |
| ------ | ----------- | ----------------------------------- |
| 0x0    | 0x4         | Magicnum "ACI0".                    |
| 0x4    | 0x28        | ?                                   |
| 0x2C   | 0x4         | Size of the Service Access Control. |
| 0x30   | 0x14        | ?                                   |
| 0x44   | ?           | FS Permissions                      |
| 0x60   | <See above> | Service Access Control              |

Switch version of 3DS ACI(Access Control Info)?

# Service Access Control

This is a list of [service](Services%20API.md "wikilink")-name strings
which the title has access to, with the following structure:

` +0: control_byte`  
` +1: {service-name without nul-terminator}`

Bitmask 0x0F in control\_byte is the {length of the service-name without
nul-terminator} - 1.

Bitmask 0x80 in control\_byte means service is allowed to be registered.

The service string can contain a wildcard `*` character.

# Access Descriptors

Like the 3DS, the switch has a number of kernel capability descriptors.
Unlike 3ds, where descriptors were identified by pattern 11..10 in high
bits, on switch descriptors are identified by pattern 01..11 in low
bits.

| Pattern of bits 20-31 | Type                    | Fields                                                    |
| --------------------- | ----------------------- | --------------------------------------------------------- |
| `0bxxxxxxxx0111?`     | Interrupt info?         | ?                                                         |
| `0bxxxxxxx01111`      | System call mask        | Bits 29-31: System call mask table index; Bits 5-28: mask |
| `0bxxxxx0111111?`     | Kernel release version? | ?                                                         |
| `0bxxxx01111111?`     | Handle table size?      | ?                                                         |
| `0bxxx011111111?`     | Kernel flags?           | ?                                                         |
| `0bx0111111111?`      | Map address range?      | ?                                                         |
| `0b011111111111?`     | Map memory page?        | ?                                                         |

# FS Permissions

| Bit | Description                                            |
| --- | ------------------------------------------------------ |
| 0   | MountContent\* is accessible when set.                 |
| 3   | This is only bit set for ShopN in the permissions-u32. |

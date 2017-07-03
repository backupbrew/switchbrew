This is the Switch equivalent of 3DS exheader. This is the file with
extension ".npdm" in {Switch ExeFS}. The size of this file varies.

| Offset     | Size       | Description |
| ---------- | ---------- | ----------- |
| 0x0        | 0x80       | META        |
| 0x80       | <Varies>   | ACID        |
| <See META> | <See META> | ACI0        |

# META

| Offset | Size | Description                       |
| ------ | ---- | --------------------------------- |
| 0x0    | 0x4  | Magic "META".                     |
| 0x20   | ?    | Title name                        |
| 0x70   | 0x4  | [\#ACI0](#ACI0 "wikilink") offset |
| 0x74   | 0x4  | [\#ACI0](#ACI0 "wikilink") size   |
| 0x78   | 0x4  | [\#ACID](#ACID "wikilink") offset |
| 0x7C   | 0x4  | [\#ACID](#ACID "wikilink") size   |

# ACID

| Offset | Size  | Description                                                           |
| ------ | ----- | --------------------------------------------------------------------- |
| 0      | 0x100 | RSA-2048 signature                                                    |
| 0x100  | 0x100 | RSA-2048 public key                                                   |
| 0x200  | 0x4   | Magic "ACID".                                                         |
| 0x204  | 0x8   | Zeroes                                                                |
| 0x20C  | 0x4   | Format version? (1)                                                   |
| 0x210  | 0x8   | Title id                                                              |
| 0x218  | 0x8   | Title id again                                                        |
| 0x220  | 0x4   | [\#FS Access Control](#FS_Access_Control "wikilink") offset           |
| 0x224  | 0x4   | [\#FS Access Control](#FS_Access_Control "wikilink") size             |
| 0x228  | 0x4   | [\#Service Access Control](#Service_Access_Control "wikilink") offset |
| 0x22C  | 0x4   | [\#Service Access Control](#Service_Access_Control "wikilink") size   |
| 0x230  | 4     | [\#Kernel Access Control](#Kernel_Access_Control "wikilink") offset   |
| 0x234  | 4     | [\#Kernel Access Control](#Kernel_Access_Control "wikilink") size     |
| 0x238  | 0x8   | Padding                                                               |

# ACI0

Looks like an old crappy version of ACID. It has the guessed version
field 0 instead of
1.

# FS Access Control

| Word | Bit | Description                                                                  |
| ---- | --- | ---------------------------------------------------------------------------- |
| 0    |     | Version? Always 1.                                                           |
| 1    | 0   | MountContent\* is accessible when set.                                       |
|      |     |                                                                              |
| 0    | 3   | This is only bit set for ShopN in the permissions-u32.                       |
| 1    | 2   | Enables access to [Bis](Filesystem%20services.md "wikilink") partitionID 27? |
| 1    | 3   | Enables access to [Bis](Filesystem%20services.md "wikilink") partitionID 28? |

# Service Access Control

This is a list of [service](Services%20API.md "wikilink")-name strings
which the title has access to, with the following structure:

` +0: control_byte`  
` +1: {service-name without nul-terminator}`

Bitmask 0x0F in control\_byte is the {length of the service-name without
nul-terminator} - 1.

Bitmask 0x80 in control\_byte means service is allowed to be registered.

The service string can contain a wildcard `*` character.

# Kernel Access Control

On Switch, descriptors are identified by pattern 01..11 in low
bits.

| Pattern of bits 15-0 | Type           | Fields                                                 |
| -------------------- | -------------- | ------------------------------------------------------ |
| `0bxxxxxxxxxxxx0111` | Kernel flags   | 5-0: Main thread priority?                             |
| `0bxxxxxxxxxxx01111` | Syscall mask   | Bits 29-31: Syscall mask table index; Bits 5-28: mask  |
| `0bxxxxxxxxx0111111` | Map IO page    | Bits 7-31: page                                        |
| `0bxxxxxxxx01111111` | Map IO range   | Bits 7-31: page then size alternating                  |
| `0bxxxx011111111111` | Interrupt pair | Bits 12-21: irq0, bits 20-31: irq1, 0x3FF means empty. |

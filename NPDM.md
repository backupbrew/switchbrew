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
| 0xE    | 1    |                                   |
| 0xF    | 1    |                                   |
| 0x1C   | 4    |                                   |
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
| 0x20C  | 0x4   | Retail flag. Must be 1 on retail, on devunit 0 is also allowed.       |
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

| Word | Bit | Description                                                                         |
| ---- | --- | ----------------------------------------------------------------------------------- |
| 0    |     | Version? Always 1.                                                                  |
| 1    | 0   | MountContent\* is accessible when set.                                              |
| 1    | 2   | Enables access to [Bis](Filesystem%20services.md "wikilink") partitionID 27 and 28? |

Web-applets access control:

  - "LibAppletWeb" and "LibAppletOff" have same access control: word0
    bit0 set, word1 bit0 and bit3 set, and word2 bit30 set.
  - Rest of the web-applets: Same as above except word1 bit0 isn't set.

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

| Pattern of lower bits | Type             | Fields                                                                                                                                     |
| --------------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `0bxxxxxxxxxxxx0111`  | Kernel flags     | Bit31-24: ?, bit23-16: ?, bit15-10: ?, bit9-4: ?                                                                                           |
| `0bxxxxxxxxxxx01111`  | Syscall mask     | Bits 29-31: Syscall mask table index; Bits 5-28: mask                                                                                      |
| `0bxxxxxxxxx0111111`  | Map IO page (RW) | Bits 7-31: page                                                                                                                            |
| `0bxxxxxxxx01111111`  | Map IO range     | Bits 7-30: alternating start page and number of pages, bit31: alternating read-only flag then MemoryAttribute 0x2001/0x42002 selector flag |
| `0bxxxx011111111111`  | Interrupt pair   | Bits 12-21: irq0, bits 20-31: irq1, 0x3FF means empty.                                                                                     |
| `0xxxx0111111111111`  |                  |                                                                                                                                            |
| `0xxx01111111111111`  |                  |                                                                                                                                            |
| `0xx011111111111111`  |                  |                                                                                                                                            |
| `0x0111111111111111`  |                  |                                                                                                                                            |
| All ones              | Ignored          |                                                                                                                                            |

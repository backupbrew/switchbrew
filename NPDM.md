This is the Switch equivalent of 3DS
[exheader](https://www.3dbrew.org/wiki/NCCH/Extended_Header). This is
the file with extension ".npdm" in {Switch ExeFS}. The size of this file
varies.

| Offset     | Size       | Description |
| ---------- | ---------- | ----------- |
| 0x0        | 0x80       | META        |
| 0x80       | <Varies>   | ACID        |
| <See META> | <See META> | ACI0        |

# META

| Offset | Size | Description                                                                                              |
| ------ | ---- | -------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x4  | Magic "META".                                                                                            |
| 0x4    |      |                                                                                                          |
| 0x8    |      |                                                                                                          |
| 0xC    | 1    | Flags, bit0: 64-bit instructions, bits1-3: address space width (1=64-bit, 2=32-bit). Needs to be \<= 0xF |
| 0xE    | 1    | MainThreadPrio                                                                                           |
| 0xF    | 1    | DefaultCpuId                                                                                             |
| 0x10   |      |                                                                                                          |
| 0x18   | 4    | ProcessCategory (0: regular title, 1: kernel built-in). Should be 0 here.                                |
| 0x1C   | 4    | MainStackSize                                                                                            |
| 0x20   | ?    | Title name                                                                                               |
| 0x70   | 0x4  | [\#ACI0](#ACI0 "wikilink") offset                                                                        |
| 0x74   | 0x4  | [\#ACI0](#ACI0 "wikilink") size                                                                          |
| 0x78   | 0x4  | [\#ACID](#ACID "wikilink") offset                                                                        |
| 0x7C   | 0x4  | [\#ACID](#ACID "wikilink") size                                                                          |

# ACID

| Offset | Size  | Description                                                                                       |
| ------ | ----- | ------------------------------------------------------------------------------------------------- |
| 0      | 0x100 | RSA-2048 signature, seems to verify the data starting at 0x100 with the size field from 0x204.    |
| 0x100  | 0x100 | RSA-2048 public key, seems to be used for the second [NCA](NCA%20Format.md "wikilink") signature. |
| 0x200  | 0x4   | Magic "ACID".                                                                                     |
| 0x204  | 0x4   | s32 Size field used with the above signature(?).                                                  |
| 0x208  | 0x4   | Zeroes                                                                                            |
| 0x20C  | 0x4   | Retail flag. Must be 1 on retail, on devunit 0 is also allowed.                                   |
| 0x210  | 0x8   | TitleIdRange\_Min                                                                                 |
| 0x218  | 0x8   | TitleIdRange\_Max                                                                                 |
| 0x220  | 0x4   | [\#FS Access Control](#FS_Access_Control "wikilink") offset                                       |
| 0x224  | 0x4   | [\#FS Access Control](#FS_Access_Control "wikilink") size                                         |
| 0x228  | 0x4   | [\#Service Access Control](#Service_Access_Control "wikilink") offset                             |
| 0x22C  | 0x4   | [\#Service Access Control](#Service_Access_Control "wikilink") size                               |
| 0x230  | 4     | [\#Kernel Access Control](#Kernel_Access_Control "wikilink") offset                               |
| 0x234  | 4     | [\#Kernel Access Control](#Kernel_Access_Control "wikilink") size                                 |
| 0x238  | 0x8   | Padding                                                                                           |

# ACI0

| Offset | Size | Description                                                           |
| ------ | ---- | --------------------------------------------------------------------- |
| 0x0    | 0x4  | Magic "ACI0".                                                         |
| 0x4    | 0xC  | Zeroes                                                                |
| 0x10   | 0x8  | Title id                                                              |
| 0x18   | 0x8  | Padding                                                               |
| 0x20   | 0x4  | [\#FS Access Header](#FS_Access_Header "wikilink") offset             |
| 0x24   | 0x4  | [\#FS Access Header](#FS_Access_Header "wikilink") size               |
| 0x28   | 0x4  | [\#Service Access Control](#Service_Access_Control "wikilink") offset |
| 0x2C   | 0x4  | [\#Service Access Control](#Service_Access_Control "wikilink") size   |
| 0x30   | 4    | [\#Kernel Access Control](#Kernel_Access_Control "wikilink") offset   |
| 0x34   | 4    | [\#Kernel Access Control](#Kernel_Access_Control "wikilink") size     |
| 0x38   | 0x8  | Padding                                                               |

# FS Access Header

| Offset | Size | Description                          |
| ------ | ---- | ------------------------------------ |
| 0x0    | 0x1  | Version? Always 1. Must be non-zero. |
| 0x1    | 0x3  | Padding                              |
| 0x4    | 0x8  | Permissions bitmask                  |
| 0xC    | 0x4  | Usually 0x1C                         |
| 0x10   | 0x4  | Usually 0x0                          |
| 0x14   | 0x4  | Usually 0x1C                         |
| 0x18   | 0x4  | Usually 0x0                          |
|        |      |                                      |

# FS Access Control

| Offset | Size | Description                          |
| ------ | ---- | ------------------------------------ |
| 0x0    | 0x1  | Version? Always 1. Must be non-zero. |
| 0x1    | 0x3  | Padding                              |
| 0x4    | 0x8  | Permissions bitmask                  |
| 0xC    | 0x20 | Usually all zeroes for applications  |

[Permissions](Filesystem%20services#Permissions.md##Permissions "wikilink")
bitmask:

| Bit | Description                                                                                                                                                 |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0   | MountContent\* is accessible when set.                                                                                                                      |
| 34  | Enables access to [Bis](Filesystem%20services.md "wikilink") partitionID 27 and 28?                                                                         |
| 63  | Enables access to everything: all [permission-types](Filesystem%20services#Permissions.md##Permissions "wikilink") which check a bitmask have this bit set. |

For bit62 in permissions, see
[here](SPL%20services#GetConfig.md##GetConfig "wikilink").

Web-applets permissions:

  - "LibAppletWeb" and "LibAppletOff" have same access control: bit0 and
    bit3 set, and bit62 set.
  - Rest of the web-applets: Same as above except bit0 isn't set.

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

| Pattern of lower bits | Lowest clear bitmask/bit | Type                 | Fields                                                                                                                                                                                                                                              |
| --------------------- | ------------------------ | -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `0bxxxxxxxxxxxx0111`  | Bit3                     | KernelFlags          | Bit31-24: Highest allowed cpu id, bit23-16: Lowest allowed cpu id, bit15-10: Highest allowed thread prio, bit9-4: Lowest allowed thread prio                                                                                                        |
| `0bxxxxxxxxxxx01111`  | Bit4                     | SyscallMask          | Bits 29-31: Syscall mask table index; Bits 5-28: Mask                                                                                                                                                                                               |
| `0bxxxxxxxxx0111111`  | Bit6                     | MapIoOrNormalRange   | Bits 7-30: Alternating start page and number of pages, bit31: Alternating read-only flag then MemoryAttribute 0x2001/0x42002 selector flag                                                                                                          |
| `0bxxxxxxxx01111111`  | Bit7                     | MapNormalPage (RW)   | Bits 8-31: Page                                                                                                                                                                                                                                     |
| `0bxxxx011111111111`  | Bit11                    | InterruptPair        | Bits 12-21: Irq0, bits 20-31: Irq1, 0x3FF means empty.                                                                                                                                                                                              |
| `0bxx01111111111111`  | Bit13                    | ApplicationType      | Bit16-14: ApplicationType (0=sysmodule, 1=application, 2=applet), bit16 ignored. Parsed by [Process Manager services](Process%20Manager%20services.md "wikilink"). Defaults to 0 if descriptor doesn't exist. Can only run 1 application at a time. |
| `0bx011111111111111`  | Bit14                    | KernelReleaseVersion | Bits 15-X: Version. The raw descriptor is compared with 0x80000, when less than an error is returned. This is equivalent to comparing the bits starting at bit15 with 0x10. This enforces a minimum required version, not a maximum.                |
| `0b0111111111111111`  | Bit15                    | HandleTableSize      | Bit25-16: Number of handles the table shall fit.                                                                                                                                                                                                    |
| `0b1111111111111111`  | Bit16                    | DebugFlags           | Bit17: can be debugged, bit18: can debug others                                                                                                                                                                                                     |
| All ones              |                          | Ignored              |                                                                                                                                                                                                                                                     |

## Mapping restrictions

The physaddr range 0x80060000-0x2000000000 is not allowed to be mapped
as IO. The physaddr range 0x80000000-0x2000000000 is not allowed to be
mapped as Normal.

\[2.0.0+\] The range for IO was changed into 0x80060000-0x81D3FFFF.

\[2.0.0+\] A blacklist was added for IO and Normal mappings:

  - 0x50040000-0x50060000 (ARM, Interrupt Controller)
  - 0x6000F000 (Exception Vectors)
  - 0x6001DC00-0x6001E000 (IPATCH)
  - 0x7000E000 (RTC/PMC)
  - 0x70019000 (MC)
  - 0x7001C000 (MC0)
  - 0x7001D000 (MC1)

## Kernel versions

| Firmware | Kernel Version | Minimum Allowed |
| -------- | -------------- | --------------- |
| 1.0.0    | 5.0.0          | 3.0.0           |
| 2.0.0    | 6.1.0          | 3.0.0           |
| 3.0.0    | 7.4.0          | 3.0.0           |
| 3.0.2    | 7.4.0          | 3.0.0           |

Bit31-19: Major version Bit18-15: Minor version Bit14-0: Zeroes

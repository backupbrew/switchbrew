# Joy-Con Firmware File

The length of the firmware must be 524288
bytes.

| Offset | Endianness | Size   | Description                                                                                          |
| ------ | ---------- | ------ | ---------------------------------------------------------------------------------------------------- |
| 0x00   | B          | 0x14   | Magic number??                                                                                       |
| 0x15   | L          | 0x06   | Unique MAC Address of controller                                                                     |
| 0x3B3  | L          | 0x04   | Offset to Factory Firmware                                                                           |
| 0x1FF4 | B          | 0x08   | OTA Magic, if the controller is Over-The-Air updated.                                                |
| 0x1FFC | L          | 0x04   | Offset to OTA Firmware, if OTA Magic is valid.                                                       |
| 0x6000 | Mixed      | 0x1000 | Factory configuration (see [Factory Configuration Sector](#Factory_Configuration_Sector "wikilink")) |
| 0x8000 | Mixed      | 0x1000 | User calibration (see [User Calibration Sector](#User_Calibration_Sector "wikilink"))                |

## Factory Configuration Sector

| Offset | Endianness | Size  | Description                                                                                        |
| ------ | ---------- | ----- | -------------------------------------------------------------------------------------------------- |
| 0x00   | B          | 0x10  | Serial number                                                                                      |
| 0x10   | ?          | 0x02  | Unknown                                                                                            |
| 0x12   | B          | 0x01  | Type descriptor (see [Type Descriptor](#Type_Descriptor "wikilink"))                               |
| 0x13   | ?          | 0x3D  | Unknown                                                                                            |
| 0x50   | B          | 0x03  | Body color of Controller in RGB Hex (see [Joy-Con Colors](Joy-Con#Colors.md##Colors "wikilink"))   |
| 0x53   | B          | 0x03  | Button color of Controller in RGB Hex (see [Joy-Con Colors](Joy-Con#Colors.md##Colors "wikilink")) |
| 0x56   | ?          | 0xFAA | Unknown                                                                                            |

### Type Descriptor

| Value | Type Name      |
| ----- | -------------- |
| 0x01  | Joy-Con Left   |
| 0x02  | Joy-Con Right  |
| 0x03  | Pro Controller |

## User Calibration Sector

| Offset | Endianness | Size  | Description                             |
| ------ | ---------- | ----- | --------------------------------------- |
| 0x00   | ?          | 0x11  | Unknown                                 |
| 0x10   | B          | 0x0B  | Left Stick Calibration (Factory 0xFF?)  |
| 0x1B   | B          | 0x0B  | Right Stick Calibration (Factory 0xFF?) |
| 0x26   | B          | 0x1A  | Sensor Calibration (Factory 0xFF?)      |
| 0x40   | ?          | 0xFBF | Unknown                                 |

# Firmware Chunks

The firmware itself is stored in PatchRAM chunks, located at the Factory
Offset or the OTA Offset. Each chunk has a Record Type, Size and
Data.

| Offset | Endianness | Size   | Description                                                |
| ------ | ---------- | ------ | ---------------------------------------------------------- |
| 0x00   | L          | 0x01   | Record type (see [Record Types](#Record_Types "wikilink")) |
| 0x01   | L          | 0x02   | Size of data (size)                                        |
| 0x03   | Mixed      | (size) | Data                                                       |

## Record Types

| Value | Record name | Description                                                                                                                      |
| ----- | ----------- | -------------------------------------------------------------------------------------------------------------------------------- |
| 0x08  | REC8        | ROM1 Patches (See [Record 0x08](#Record_0x08 "wikilink") and [Memory Regions](#Memory_Regions "wikilink"))                       |
| 0x0A  | RECA        | RAM (Ram Low and Ram High) Patches (See [Record 0x0A](#Record_0x0A "wikilink") and [Memory Regions](#Memory_Regions "wikilink")) |
| 0x0B  | RECB        | Unknown                                                                                                                          |
| 0xFE  | END         | End of chunk stream                                                                                                              |

### Record 0x08

| Offset | Endianness | Size | Description  |
| ------ | ---------- | ---- | ------------ |
| 0x00   | L          | 0x01 | Index        |
| 0x01   | L          | 0x04 | Address      |
| 0x05   | B          | 0x04 | Data         |
| 0x09   | L          | 0x02 | Unk1?        |
| 0x0B   | L          | 0x02 | Unk2?        |
| 0x0D   | L          | 0x02 | Body size??? |

### Record 0x0A

| Offset | Endianness | Size   | Description | Note                                                                                             |
| ------ | ---------- | ------ | ----------- | ------------------------------------------------------------------------------------------------ |
| 0x00   | L          | 0x04   | Address     | \-                                                                                               |
| 0x04   | B          | (Note) | Data        | To calculate the size do: chunk\_datasize (See [Firmware Chunks](#Firmware_Chunks "wikilink"))-4 |

### Record 0x0B

| Offset | Endianness | Size | Description |
| ------ | ---------- | ---- | ----------- |
| 0x00   | L          | 0x04 | Address     |

## Memory Regions

| Offsets            | Description |
| ------------------ | ----------- |
| 0x00-0xC8000       | ROM 1       |
| 0x260000-0x26C000  | ROM 2       |
| 0xD0000-0x0x0DFFFF | RAM Low     |
| 0x200000-0x247FFF  | RAM High    |

### NAND structure

## Boot Partitions

**Boot Partition 0 (0 of 1)**

| Offset   | Size | Description                                |
| -------- | ---- | ------------------------------------------ |
| 0x000000 |      | title 0100000000000819 BCT                 |
| 0x004000 |      | title 010000000000081A BCT                 |
| 0x008000 |      | title 0100000000000819 BCT                 |
| 0x00C000 |      | title 010000000000081A BCT                 |
| 0x100000 |      | title 0100000000000819 "package1"          |
| 0x140000 |      | title 0100000000000819 "package1" (Backup) |
| 0x180000 |      | Keyblob area                               |
| 0x184000 |      | Unknown, 0x20-bytes hash + one u32?        |

**Boot Partition 1 (1 of 1)**

| Offset   | Size | Description                                |
| -------- | ---- | ------------------------------------------ |
| 0x000000 |      | title 010000000000081A "package1"          |
| 0x040000 |      | title 010000000000081A "package1" (Backup) |

## User Partitions

| Partition name         | Offset     | Size        | [Bis](Filesystem%20services.md "wikilink") Partition ID | Description                                                                                                                                                                                 |
| ---------------------- | ---------- | ----------- | ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| N/A                    | 0x0        | ?           | 20                                                      | GPT header, partition ID also provides raw access to all partitions                                                                                                                         |
| PRODINFO               | 0x00004400 | 0x003FBC00  | 27                                                      | "CAL0" raw partition containing set:cal data                                                                                                                                                |
| PRODINFOF              | 0x00400000 | 0x00400000  | 28                                                      | FAT12 filesystem, additional calibration?                                                                                                                                                   |
| BCPKG2-1-Normal-Main   | 0x00800000 | 0x00800000  | 21                                                      | For all these packages, data starts at offset 0x4000. This is installed from "package2": on retail it's from FIRM-A 0100000000000819, for unknown cases it's from FIRM-C, 010000000000081B. |
| BCPKG2-2-Normal-Sub    | 0x01000000 | 0x00800000  | 22                                                      | Identical to BCPKG2-1-Normal-Main, probably used as a backup partition.                                                                                                                     |
| BCPKG2-3-SafeMode-Main | 0x01800000 | 0x00800000  | 23                                                      | This is installed from "package2" in firmware package B, 010000000000081A.                                                                                                                  |
| BCPKG2-4-SafeMode-Sub  | 0x02000000 | 0x00800000  | 24                                                      | Identical to BCPKG2-3-SafeMode-Main.                                                                                                                                                        |
| BCPKG2-5-Repair-Main   | 0x02800000 | 0x00800000  | 25                                                      | Unknown what title this originates from.                                                                                                                                                    |
| BCPKG2-6-Repair-Sub    | 0x03000000 | 0x00800000  | 26                                                      | Identical to BCPKG2-5-Repair-Main.                                                                                                                                                          |
| SAFE                   | 0x03800000 | 0x04000000  | 29                                                      | FAT32 filesystem                                                                                                                                                                            |
| SYSTEM                 | 0x07800000 | 0xA0000000  | 31                                                      | FAT32 filesystem                                                                                                                                                                            |
| USER                   | 0xA7800000 | 0x680000000 | 30                                                      | FAT32 filesystem                                                                                                                                                                            |

# PRODINFOF

`PRODINFOF`  
`├── Certifications`  
`│   └── WirelessCertification.png`  
`└── ptd`  
`    ├── DeviceIdWithEmsBit.dat`  
`    ├── Ecid.dat`  
`    ├── prodCode.dat`  
`    └── log`  
`        ├── Process_asm1.log`  
`        ├── Process_board1.log`  
`        ├── TestFlagLine.log`  
`        ├── TestFlagQc.log`  
`        ├── AGING`  
`        │   └── Sequence.log`  
`        ├── BOARD_TEST`  
`        │   └── Sequence.log`  
`        ├── BOARD_WIRELESS`  
`        │   └── Sequence.log`  
`        ├── FINAL_CHECK`  
`        │   └── Sequence.log`  
`        ├── LCD_AND_KEY`  
`        │   └── Sequence.log`  
`        └── USB_AND_HP`  
`            └── Sequence.log`

# SYSTEM

`SYSTEM`  
`├── PRF2SAFE.RCV`  
`├── Contents`  
`│   ├── placehld`  
`│   │   └── ... `[`NCA`](NCA.md "wikilink")  
`│   └── registered`  
`│       └── ... `[`NCA`](NCA.md "wikilink")  
`├── save`  
`│   └── ...`  
`└── saveMeta`  
`    └── ...`

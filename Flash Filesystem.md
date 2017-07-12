# NAND structure

## Boot Partitions

**Boot Partition 0 (0 of
1)**

| Offset   | Size   | Description                                                                                                                |
| -------- | ------ | -------------------------------------------------------------------------------------------------------------------------- |
| 0x000000 |        | Title 0100000000000819 BCT                                                                                                 |
| 0x004000 |        | Title 010000000000081A BCT                                                                                                 |
| 0x008000 |        | Title 0100000000000819 BCT                                                                                                 |
| 0x00C000 |        | Title 010000000000081A BCT                                                                                                 |
| 0x100000 |        | Title 0100000000000819 "package1"                                                                                          |
| 0x140000 |        | Title 0100000000000819 "package1" (Backup)                                                                                 |
| 0x180000 | 0x4000 | Keyblob area                                                                                                               |
| 0x184000 |        | Unknown, 0x20-bytes hash (updated when bcpkg-2-1 updates) + one u64? (may be incremented on bcpkg update) All zero on 1.0. |

**Boot Partition 1 (1 of 1)**

| Offset   | Size | Description                                |
| -------- | ---- | ------------------------------------------ |
| 0x000000 |      | Title 010000000000081A "package1"          |
| 0x040000 |      | Title 010000000000081A "package1" (Backup) |

### Keyblob

| Offset | Size  | Description                                                                                                                                    |
| ------ | ----- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x10  | Keyblob AES-CMAC over the remaining 0xA0-bytes (Checked with a safe memcmp which won't abort early, calls the general panic() func on failure) |
| 0x10   | 0x10  | Keyblob AES CTR                                                                                                                                |
| 0x20   | 0x90  | Keyblob encrypted payload                                                                                                                      |
| 0xB0   | 0x150 | Unused, all-zero.                                                                                                                              |

The data at 0x180000 is an array of 0x200-byte entries, with a total of
32 entries. Therefore, there's 32 different keyblobs are stored here.
The raw data for each one is unique compared to the others.

The 0xB0-byte keyblob is installed to the console-unique "customer data"
section in BCTs(BCT+0x450), which is what gets used during system boot.

Which keyblob is loaded from here during install is presumably somewhere
in BCT? \<v3.0 use index0, v3.0 uses index1. Hence, the installed
keyblob was changed with v3.0.

BCT Offset 0x2330 is probably the field controlling this?(0x245C is a
copy of this field?) There's at least 3 versions of package1: v1.0,
v2.0, and v3.0, BCT was updated for all of these. With v1.0 and v2.0
these two fields are the same(0x1), however with v3.0 it's 0x2.

#### panic

The ARM7 panic() function does the following:

  - Clears memory.
  - ...
  - Writes 0x1 to FUSE\_DIS\_PGM. From nvdia source: "check that fuse
    options write access hasn't been disabled".
  - ...
  - Executes: while(1)\*((u32\*)0x60007004) =
0x5\<\<28;

## User Partitions

| Partition name         | Offset      | Size        | [Bis](Filesystem%20services.md "wikilink") Partition ID | Description                                                                                                                                                                                                                                                                                                                                                                                        |
| ---------------------- | ----------- | ----------- | ------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| N/A                    | 0x0         |             | 20                                                      | GPT header, Bis-storage also allows raw access to the entire NAND eMMC sectors starting at sector0.                                                                                                                                                                                                                                                                                                |
| PRODINFO               | 0x00004400  | 0x003FBC00  | 27                                                      | "CAL0" raw partition containing set:cal data.                                                                                                                                                                                                                                                                                                                                                      |
| PRODINFOF              | 0x00400000  | 0x00400000  | 28                                                      | FAT12 filesystem, additional calibration.                                                                                                                                                                                                                                                                                                                                                          |
| BCPKG2-1-Normal-Main   | 0x00800000  | 0x00800000  | 21                                                      | For all these packages, data starts at offset 0x4000 and is not console-unique. This is installed from "package2" in firmware package A (0100000000000819) by default. With the exFAT update installed, this is switched to firmware package C (010000000000081B). The data stored here matches the raw /package2 file stored in the 81\[9AB\] data archives -- there is no additional encryption. |
| BCPKG2-2-Normal-Sub    | 0x01000000  | 0x00800000  | 22                                                      | Identical to BCPKG2-1-Normal-Main, probably used as a backup partition.                                                                                                                                                                                                                                                                                                                            |
| BCPKG2-3-SafeMode-Main | 0x01800000  | 0x00800000  | 23                                                      | This is installed from "package2" in firmware package B (010000000000081A).                                                                                                                                                                                                                                                                                                                        |
| BCPKG2-4-SafeMode-Sub  | 0x02000000  | 0x00800000  | 24                                                      | Identical to BCPKG2-3-SafeMode-Main.                                                                                                                                                                                                                                                                                                                                                               |
| BCPKG2-5-Repair-Main   | 0x02800000  | 0x00800000  | 25                                                      | Installed at the factory.                                                                                                                                                                                                                                                                                                                                                                          |
| BCPKG2-6-Repair-Sub    | 0x03000000  | 0x00800000  | 26                                                      | Identical to BCPKG2-5-Repair-Main.                                                                                                                                                                                                                                                                                                                                                                 |
| SAFE                   | 0x03800000  | 0x04000000  | 29                                                      | FAT32 filesystem.                                                                                                                                                                                                                                                                                                                                                                                  |
| SYSTEM                 | 0x07800000  | 0xA0000000  | 31 (and 32?)                                            | FAT32 filesystem.                                                                                                                                                                                                                                                                                                                                                                                  |
| USER                   | 0xA7800000  | 0x680000000 | 30                                                      | FAT32 filesystem.                                                                                                                                                                                                                                                                                                                                                                                  |
|                        | 0x747BFFE00 | 0x200       |                                                         | This is the backup GPT header specified by the main GPT header. This is also the last sector readable with Bis-storage paritionID 20.                                                                                                                                                                                                                                                              |

If the client process lacks the relevant permission for any of the above
partition IDs, error 0x2EE202 is returned.

[NCAs](NCA.md "wikilink") stored in NAND are raw, identical to the data
readable with
[Content\_Manager\_services\#ReadEntryRaw](Content%20Manager%20services#ReadEntryRaw.md##ReadEntryRaw "wikilink").

The filenames for saveimages is just "<lower-case hex u64 saveID>".
SYSTEM-partition saveIDs are specified by
[FS](Filesystem%20services.md "wikilink") commands, while USER-partition
saveIDs are determined by FS-module internally. The high u32 of the
saveID is normally either 0x00000000 or 0x80000000.

### PRODINFOF

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

#### DeviceIdWithEmsBit.dat

Contains a 0x10-byte uppercase hex string, identical to the DeviceId in
the [DeviceCert](Settings%20services.md "wikilink").

### SYSTEM

`SYSTEM`  
`├── PRF2SAFE.RCV`  
`├── Contents`  
`│   ├── registered`  
`│   │   └── ... `[`NCA`](NCA.md "wikilink")  
`│   └── placehld`  
`│       └── ... `[`NCA`](NCA.md "wikilink")  
`├── `[`save`](Savegames.md "wikilink")  
`│   └── ...`  
`└── saveMeta`  
`    └── ... (empty?)`

The saves stored under this partition are only for system-titles / etc.

### USER

`USER`  
`├── PRF2SAFE.RCV`  
`├── Album (Same layout as `[`SD`](SD%20Filesystem.md "wikilink")`)`  
`├── Contents`  
`│   ├── registered`  
`│   │   └── ... `[`NCA`](NCA.md "wikilink")  
`│   └── placehld`  
`│       └── ... `[`NCA`](NCA.md "wikilink")  
`├── `[`save`](Savegames.md "wikilink")  
`│   └── ...`  
`├── saveMeta`  
`│   └── ... `  
`└── temp `

The saves for all non-system applications, regardless of where the
application is located(storageID), is stored here. Each user account
which has savedata has a separate saveimage. Save-common for an
application is presumably a separate saveimage too. Every saveimage here
is *only* for applications.

### SAFE

`SAFE`  
`├── PRF2SAFE.RCV`  
`├── Contents`  
`│   ├── registered`  
`│   │   └── ... `[`NCA`](NCA.md "wikilink")` (nothing installed?)`  
`│   └── placehld`  
`│       └── ... `[`NCA`](NCA.md "wikilink")  
`└── `[`save`](Savegames.md "wikilink")  
`    ├── 8000000000000000`  
`    └── 8000000000000120`

On a v2.1 system with MountBis, the only thing under here is
"PRF2SAFE.RCV".

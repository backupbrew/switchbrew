# NAND structure

The Switch's eMMC storage features a large user area, two smaller boot
partitions, and a replay-protected memory block which is unused (no
authentication key is programmed).

## Boot Partitions

**Boot Partition 0 (0 of
1)**

| Offset   | Size    | Description                                                                                                       |
| -------- | ------- | ----------------------------------------------------------------------------------------------------------------- |
| 0x000000 | 0x4000  | Title 0100000000000819 BCT                                                                                        |
| 0x004000 | 0x4000  | Title 010000000000081A BCT                                                                                        |
| 0x008000 | 0x4000  | Title 0100000000000819 BCT                                                                                        |
| 0x00C000 | 0x4000  | Title 010000000000081A BCT                                                                                        |
| 0x100000 | 0x40000 | Title 0100000000000819 "package1"                                                                                 |
| 0x140000 | 0x40000 | Title 0100000000000819 "package1" (Backup)                                                                        |
| 0x180000 | 0x4000  | Keyblob area                                                                                                      |
| 0x184000 | 0x20    | Unknown pseudorandom data, often changes on reboot. All zero on 1.0.                                              |
| 0x184020 | 0x8?    | Increments on every boot until hitting a certain number? Bottom 10 bits (0x3FF) are always zero. All zero on 1.0. |

**Boot Partition 1 (1 of 1)**

| Offset   | Size    | Description                                |
| -------- | ------- | ------------------------------------------ |
| 0x000000 | 0x40000 | Title 010000000000081A "package1"          |
| 0x040000 | 0x40000 | Title 010000000000081A "package1" (Backup) |
| 0x080000 | 0x40000 |                                            |
| 0x0C0000 | 0x40000 |                                            |

### Keyblob

| Offset | Size  | Description                                                                                                                                                       |
| ------ | ----- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x10  | Keyblob AES-CMAC over the remaining 0xA0-bytes (Checked with a mem-diff function which is safe against timing attacks, calls the general panic() func on failure) |
| 0x10   | 0x10  | Keyblob AES CTR                                                                                                                                                   |
| 0x20   | 0x90  | Keyblob encrypted payload                                                                                                                                         |
| 0xB0   | 0x150 | Unused, all-zero.                                                                                                                                                 |

Decrypted Keydata format:

| Offset | Size | Description                                |
| ------ | ---- | ------------------------------------------ |
| 0x0    | 0x80 | Array of master static key encryption keys |
| 0x80   | 0x10 | [Stage 2](Package1.md "wikilink") key      |

Starting at 0x180000 is an array of 0x200-byte entries, for a total of
32 keyblobs. Each one is unique compared to the others. They are all
console unique.

The 0xB0-byte keyblob is installed to the "customer data" section in
BCTs (BCT+0x450).

BCT offset 0x2330 is the field controlling which keyblob gets used. NS
uses this to inject the appropriate keyblob on system update.
[Boot](Boot.md "wikilink") also uses this index for repairing corrupt
sectors.

With \[ [3.0.0](3.0.0.md "wikilink") \] index 2 is used instead of index
1. With \[ [3.0.1](3.0.1.md "wikilink") + \] index 3 is used instead of
index 2.

The Tegra 210 BCT format can be found in nvidia's cbootimage
[1](https://github.com/thierryreding/tegra-avp/blob/35f467996e532357db54894c975acab93293d219/include/avp/tegra210/bct.h#L521)

## User Partitions

| Partition name         | Offset      | Size        | [Bis](Filesystem%20services.md "wikilink") Partition ID | Description                                                                                                                                                                                                                                                                                                                                                                                           |
| ---------------------- | ----------- | ----------- | ------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| N/A                    | 0x0         |             | 20                                                      | GPT header, Bis-storage also allows raw access to the entire NAND eMMC sectors starting at sector0.                                                                                                                                                                                                                                                                                                   |
| PRODINFO               | 0x00004400  | 0x003FBC00  | 27                                                      | "CAL0" raw partition containing set:cal data.                                                                                                                                                                                                                                                                                                                                                         |
| PRODINFOF              | 0x00400000  | 0x00400000  | 28                                                      | FAT12 filesystem, additional calibration.                                                                                                                                                                                                                                                                                                                                                             |
| BCPKG2-1-Normal-Main   | 0x00800000  | 0x00800000  | 21                                                      | For all these packages, data starts at offset 0x4000 and is not console-unique. This is installed from "package2" in firmware package A (0100000000000819) by default. With the exFAT update installed, this is switched to firmware package C (010000000000081B). The data stored here matches the raw /nx/package2 file stored in the 81\[9AB\] data archives -- there is no additional encryption. |
| BCPKG2-2-Normal-Sub    | 0x01000000  | 0x00800000  | 22                                                      | Identical to BCPKG2-1-Normal-Main, probably used as a backup partition.                                                                                                                                                                                                                                                                                                                               |
| BCPKG2-3-SafeMode-Main | 0x01800000  | 0x00800000  | 23                                                      | This is installed from "package2" in firmware package B (010000000000081A).                                                                                                                                                                                                                                                                                                                           |
| BCPKG2-4-SafeMode-Sub  | 0x02000000  | 0x00800000  | 24                                                      | Identical to BCPKG2-3-SafeMode-Main.                                                                                                                                                                                                                                                                                                                                                                  |
| BCPKG2-5-Repair-Main   | 0x02800000  | 0x00800000  | 25                                                      | Installed at the factory.                                                                                                                                                                                                                                                                                                                                                                             |
| BCPKG2-6-Repair-Sub    | 0x03000000  | 0x00800000  | 26                                                      | Identical to BCPKG2-5-Repair-Main.                                                                                                                                                                                                                                                                                                                                                                    |
| SAFE                   | 0x03800000  | 0x04000000  | 29                                                      | FAT32 filesystem.                                                                                                                                                                                                                                                                                                                                                                                     |
| SYSTEM                 | 0x07800000  | 0xA0000000  | 31 (and 32?)                                            | FAT32 filesystem.                                                                                                                                                                                                                                                                                                                                                                                     |
| USER                   | 0xA7800000  | 0x680000000 | 30                                                      | FAT32 filesystem.                                                                                                                                                                                                                                                                                                                                                                                     |
|                        | 0x747BFFE00 | 0x200       |                                                         | This is the backup GPT header specified by the main GPT header. This is also the last sector readable with Bis-storage paritionID 20.                                                                                                                                                                                                                                                                 |

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

# System Savegames

This is a listing of known System Savedata and what titles they
correspond
to.

| SaveID             | Owner      | Mount             | Notes                                                                                                                                                     |
| ------------------ | ---------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x8000000000000010 | account    | account:/         | Account database.                                                                                                                                         |
| 0x8000000000000011 | account    | idgen:/           |                                                                                                                                                           |
| 0x8000000000000020 | nfc        | data:/            | NFC data and backups.                                                                                                                                     |
| 0x8000000000000030 | ns         | mii:/             | Mii database.                                                                                                                                             |
| 0x8000000000000031 | ns         | mii:/             | Mii test mode database.                                                                                                                                   |
| 0x8000000000000040 | ns         | apprecdb:/        |                                                                                                                                                           |
| 0x8000000000000041 | ns         | nsaccache:/       | Home menu icondata/lru list for recently played games.                                                                                                    |
| 0x8000000000000043 | ns         | ns\_appman:/      |                                                                                                                                                           |
| 0x8000000000000044 | ns         | ns\_sysup:/       | Content update context.                                                                                                                                   |
| 0x8000000000000045 | ns         | vmdb:/            | Version List/Required Version List storage.                                                                                                               |
| 0x8000000000000046 | ns         | dtlman:/          |                                                                                                                                                           |
| 0x8000000000000047 | ns         | ns\_exfat:/       |                                                                                                                                                           |
| 0x8000000000000048 | ns         | ns\_systemseed:/  |                                                                                                                                                           |
| 0x8000000000000050 | settings   | SystemSettings:/  |                                                                                                                                                           |
| 0x8000000000000051 | settings   | FwdbgSettingsS:/  |                                                                                                                                                           |
| 0x8000000000000052 | settings   | PrivateSettings:/ |                                                                                                                                                           |
| 0x8000000000000053 | settings   | DeviceSettings:/  |                                                                                                                                                           |
| 0x8000000000000054 | settings   | ApplnSettings:/   |                                                                                                                                                           |
| 0x8000000000000060 | ssl        | SslSave:/         |                                                                                                                                                           |
| 0x8000000000000070 | nim        | nim\_sys:/        |                                                                                                                                                           |
| 0x8000000000000071 | nim        | nim\_net:/        |                                                                                                                                                           |
| 0x8000000000000072 | nim        | nim\_tmp:/        |                                                                                                                                                           |
| 0x8000000000000073 | nim        | nim\_dac:/        |                                                                                                                                                           |
| 0x8000000000000074 | nim        | nim\_delta:/      |                                                                                                                                                           |
| 0x8000000000000075 | nim        | nim\_vac:/        |                                                                                                                                                           |
| 0x8000000000000080 | friends    | friends:/         |                                                                                                                                                           |
| 0x8000000000000081 | friends    | friends-sys:/     |                                                                                                                                                           |
| 0x8000000000000082 | friends    | friends-image:/   |                                                                                                                                                           |
| 0x8000000000000090 | bcat       | news:/            | Actual news msgpack archives.                                                                                                                             |
| 0x8000000000000091 | bcat       | news-sys:/        | News metadata, tasklist, history, database, required system version, etc.                                                                                 |
| 0x8000000000000092 | bcat       | news-dl:/         | Storage for newly(?) downloaded news list/data.                                                                                                           |
| 0x80000000000000A0 | bcat       | prepo-sys:/       | Play Report system information.                                                                                                                           |
| 0x80000000000000A1 | bcat       | prepo:/           | Play Report msgpack archives.                                                                                                                             |
| 0x80000000000000B0 | bsdsockets | nsdsave:/         | Socket configuration saved data.                                                                                                                          |
| 0x80000000000000C1 | bcat       | bcat-sys:/        |                                                                                                                                                           |
| 0x80000000000000C2 | bcat       | bcat-dl:/         |                                                                                                                                                           |
| 0x80000000000000D1 | erpt       | save:/            | Contains "/journal" report listing + actual crash reports ("/%08x-%04x-%04x-%02x%02x-%04x%08x"), which are serialized via [MsgPack](http://msgpack.org/). |
| 0x80000000000000E0 | es         | escertificate:/   |                                                                                                                                                           |
| 0x80000000000000E1 | es         | escommon:/        |                                                                                                                                                           |
| 0x80000000000000E2 | es         | espersonalized:/  |                                                                                                                                                           |
| 0x80000000000000F0 | ns         | pdm:/             | Play Data log.                                                                                                                                            |
| 0x8000000000000100 | pctl       | pctlss:/          | Parental Control settings.                                                                                                                                |
| 0x8000000000000110 | npns       | npns\_save:/      | Push notifications persistent storage.                                                                                                                    |
|                    |            |                   |                                                                                                                                                           |

# Structure

These have been redesigned from the 3DS so that they fit within a
Aarch64 MOV instruction immediate most of the time (without requiring
the additional MOVK).

| Bits | Field       |
| ---- | ----------- |
| 8-0  | Module      |
| 21-9 | Description |

When a fatal-error is received the error code is outputted using the
following formatter:

` %04d-%04d`

.. where the first code is `2000 + Module`, and the other being
`Description`. Bits \>=22 from the error-code are unused when displaying
fatal-errors, since the Description ends with bit21.

# Modules

| Value | Name                                         |
| ----- | -------------------------------------------- |
| 1     | Kernel                                       |
| 2     | FS                                           |
| 3     | OS (Memory, Thread, Mutex, NVIDIA)           |
| 4     | HTCS                                         |
| 5     | NCM                                          |
| 6     | DD                                           |
| 7     | Debug Monitor                                |
| 8     | LR                                           |
| 9     | Loader                                       |
| 10    | CMIF (IPC command interface)                 |
| 11    | HIPC (IPC)                                   |
| 15    | PM                                           |
| 16    | NS                                           |
| 17    | Sockets                                      |
| 18    | HTC                                          |
| 20    | NCM Content                                  |
| 21    | SM                                           |
| 22    | RO userland                                  |
| 24    | SDMMC                                        |
| 25    | OVLN                                         |
| 26    | SPL                                          |
| 100   | ETHC                                         |
| 101   | I2C                                          |
| 102   | GPIO                                         |
| 103   | UART                                         |
| 105   | Settings                                     |
| 107   | WLAN                                         |
| 108   | XCD                                          |
| 110   | NIFM                                         |
| 111   | Hwopus                                       |
| 113   | Bluetooth                                    |
| 114   | VI                                           |
| 115   | NFP                                          |
| 116   | Time                                         |
| 117   | FGM                                          |
| 118   | OE                                           |
| 120   | PCIe                                         |
| 121   | Friends                                      |
| 122   | BCAT                                         |
| 123   | SSL                                          |
| 124   | Account                                      |
| 125   | News                                         |
| 126   | Mii                                          |
| 127   | NFC                                          |
| 128   | AM                                           |
| 129   | Play Report                                  |
| 130   | AHID                                         |
| 132   | Home Menu (Qlaunch)                          |
| 133   | PCV                                          |
| 134   | OMM                                          |
| 135   | BPC                                          |
| 136   | PSM                                          |
| 137   | NIM                                          |
| 138   | PSC                                          |
| 139   | TC                                           |
| 140   | USB                                          |
| 141   | NSD                                          |
| 142   | PCTL                                         |
| 143   | BTM                                          |
| 144   | EC (Shop)                                    |
| 145   | ETicket                                      |
| 146   | NGC (Bad Words)                              |
| 147   | Error Report                                 |
| 148   | APM                                          |
| 150   | Profiler                                     |
| 151   | Error Upload                                 |
| 153   | Audio                                        |
| 154   | NPNS                                         |
| 155   | NPNS HTTP Stream                             |
| 157   | ARP                                          |
| 158   | Boot                                         |
| 159   | SWKBD                                        |
| 161   | NFC Mifare                                   |
| 162   | Userland assert                              |
| 163   | Fatal                                        |
| 164   | NIM Shop                                     |
| 165   | SPSM                                         |
| 167   | BGTC                                         |
| 168   | Userland crash                               |
| 179   | OLSC                                         |
| 180   | SREPO                                        |
| 181   | Dauth                                        |
| 202   | HID                                          |
| 203   | LDN                                          |
| 205   | Irsensor                                     |
| 206   | Capture                                      |
| 208   | Manu                                         |
| 209   | ATK                                          |
| 210   | Web                                          |
| 211   |                                              |
| 212   | GRC                                          |
| 216   | Migration                                    |
| 217   | Migration Idc Server                         |
| 345   | libnx                                        |
| 346   | [Homebrew ABI](Homebrew%20ABI.md "wikilink") |
| 347   | Homebrew Loader                              |
| 348   | libnx Nvidia errors                          |
|       |                                              |

# Error codes

| Value             | Module | Description | Notes                                                                                                                                                                                |
| ----------------- | ------ | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 0x0E01            | 1      | 7           | Session count exceeded                                                                                                                                                               |
| 0x1C01            | 1      | 14          | Invalid kernel capability descriptor                                                                                                                                                 |
| 0x4201            | 1      | 33          | Not Implemented                                                                                                                                                                      |
| 0x7601            | 1      | 59          | Thread terminated/termination requested                                                                                                                                              |
| 0x8C01            | 1      | 70          | No more debug events                                                                                                                                                                 |
| 0xCA01            | 1      | 101         | Invalid size                                                                                                                                                                         |
| 0xCC01            | 1      | 102         | Invalid address                                                                                                                                                                      |
| 0xCE01            | 1      | 103         | Resource exhaustion                                                                                                                                                                  |
| 0xD001            | 1      | 104         | Memory exhaustion                                                                                                                                                                    |
| 0xD201            | 1      | 105         | Handle-table exhaustion                                                                                                                                                              |
| 0xD401            | 1      | 106         | Invalid memory state / invalid memory permissions.                                                                                                                                   |
| 0xD801            | 1      | 108         | Invalid memory permissions.                                                                                                                                                          |
| 0xDC01            | 1      | 110         | Invalid memory range                                                                                                                                                                 |
| 0xE001            | 1      | 112         | Invalid thread priority.                                                                                                                                                             |
| 0xE201            | 1      | 113         | Invalid processor id.                                                                                                                                                                |
| 0xE401            | 1      | 114         | Invalid handle.                                                                                                                                                                      |
| 0xE601            | 1      | 115         | Invalid pointer/Syscall copy from user failed.                                                                                                                                       |
| 0xE801            | 1      | 116         | Invalid combination                                                                                                                                                                  |
| 0xEA01            | 1      | 117         | Time out. Also when you give 0 handles to svcWaitSynchronizationN.                                                                                                                   |
| 0xEC01            | 1      | 118         | Canceled/interrupted \[?\]                                                                                                                                                           |
| 0xEE01            | 1      | 119         | Out of range                                                                                                                                                                         |
| 0xF001            | 1      | 120         | Invalid enum                                                                                                                                                                         |
| 0xF201            | 1      | 121         | No such entry                                                                                                                                                                        |
| 0xF401            | 1      | 122         | Irq/DeviceAddressSpace/{...} already registered                                                                                                                                      |
| 0xF601            | 1      | 123         | Port remote dead                                                                                                                                                                     |
| 0xF801            | 1      | 124         | \[Usermode\] Unhandled interrupt/exception                                                                                                                                           |
| 0xFA01            | 1      | 125         | Process already started/Wrong memory permission?                                                                                                                                     |
| 0xFC01            | 1      | 126         | Reserved value                                                                                                                                                                       |
| 0xFE01            | 1      | 127         | Invalid hardware breakpoint                                                                                                                                                          |
| 0x10001           | 1      | 128         | \[Usermode\] Fatal exception                                                                                                                                                         |
| 0x10201           | 1      | 129         | Last thread didn't belong to your process                                                                                                                                            |
| 0x10601           | 1      | 131         | Port closed                                                                                                                                                                          |
| 0x10801           | 1      | 132         | Resource limit exceeded                                                                                                                                                              |
| 0x20801           | 1      | 260         | Command buffer too small                                                                                                                                                             |
| 0x40a01           | 1      | 517         | No such process                                                                                                                                                                      |
| 0x41001           | 1      | 520         | Process not being debugged                                                                                                                                                           |
| 0x202             | 2      | 1           | Path does not exist.                                                                                                                                                                 |
| 0x402             | 2      | 2           | Path already exists.                                                                                                                                                                 |
| 0xE02             | 2      | 7           | Savedata [already](Filesystem%20services.md "wikilink") mounted                                                                                                                      |
| 0x4602            | 2      | 35          | Not enough free space for BIS Calibration partition.                                                                                                                                 |
| 0x4802            | 2      | 36          | Not enough free space for BIS Safe partition.                                                                                                                                        |
| 0x4A02            | 2      | 37          | Not enough free space for BIS User partition.                                                                                                                                        |
| 0x4C02            | 2      | 38          | Not enough free space for BIS System partition.                                                                                                                                      |
| 0x4E02            | 2      | 39          | Not enough free space on SD card.                                                                                                                                                    |
| 0x7802            | 2      | 60          | The specified [NCA](NCA.md "wikilink")-type doesn't exist for this title.                                                                                                            |
| 0x7D202           | 2      | 1001        | Process does not have RomFs                                                                                                                                                          |
| 0x7D402           | 2      | 1002        | Title-id not found / savedata not found.                                                                                                                                             |
| 0xFA202           | 2      | 2001        | SD card not inserted                                                                                                                                                                 |
| 0x13B002          | 2      | 2520        | Gamecard not inserted                                                                                                                                                                |
| 0x13DA02          | 2      | 2541        | Version check failed when mounting gamecard sysupdate partition?                                                                                                                     |
| 0x171402          | 2      | 2954        | Invalid gamecard handle.                                                                                                                                                             |
| 0x177202          | 2      | 3001        | Unimplemented behavior                                                                                                                                                               |
| 0x177602          | 2      | 3003        | File/Directory already exists.                                                                                                                                                       |
| 0x190202          | 2      | 3201        | Memory allocation failure related to FAT filesystem code                                                                                                                             |
| 0x190602          | 2      | 3203        | Memory allocation failure related to FAT filesystem code                                                                                                                             |
| 0x190802          | 2      | 3204        | Memory allocation failure related to FAT filesystem code                                                                                                                             |
| 0x190A02          | 2      | 3205        | Memory allocation failure related to FAT filesystem code                                                                                                                             |
| 0x190C02          | 2      | 3206        | Memory allocation failure related to FAT filesystem code                                                                                                                             |
| 0x191002          | 2      | 3208        | Memory allocation failure related to FAT filesystem code                                                                                                                             |
| 0x195802          | 2      | 3244        | Allocation failure related to SD cards                                                                                                                                               |
| 0x196002          | 2      | 3248        | Out of memory                                                                                                                                                                        |
| 0x196202          | 2      | 3249        | Out of memory                                                                                                                                                                        |
| 0x1A3E02          | 2      | 3359        | Out of memory                                                                                                                                                                        |
| 0x1A4002          | 2      | 3360        | Out of memory                                                                                                                                                                        |
| 0x1A4A02          | 2      | 3365        | Out of memory                                                                                                                                                                        |
| 0x21BC02          | 2      | 4318        | Invalid save data filesystem magic (valid magic is SAVE in ASCII)                                                                                                                    |
| 0x234202          | 2      | 4513        | Error reading ACID section in NPDM                                                                                                                                                   |
| 0x234402          | 2      | 4514        | Invalid NPDM ACID section size                                                                                                                                                       |
| 0x234602          | 2      | 4515        | Last byte of the ACID modulus is zero                                                                                                                                                |
| 0x234802          | 2      | 4516        | Invalid ACID fixed key signature                                                                                                                                                     |
| 0x234A02          | 2      | 4517        | Invalid NCA magic                                                                                                                                                                    |
| 0x234C02          | 2      | 4518        | Invalid NCA header fixed key signature                                                                                                                                               |
| 0x234E02          | 2      | 4519        | Invalid NCA header ACID signature                                                                                                                                                    |
| 0x235002          | 2      | 4520        | Invalid NCA header section hash                                                                                                                                                      |
| 0x235202          | 2      | 4521        | Invalid NCA Key index                                                                                                                                                                |
| 0x235602          | 2      | 4523        | Invalid encryption type                                                                                                                                                              |
| 0x235802          | 2      | 4524        | Redirection BKTR table size is negative                                                                                                                                              |
| 0x235A02          | 2      | 4525        | Encryption BKTR table size is negative                                                                                                                                               |
| 0x235C02          | 2      | 4526        | Redirection BKTR table end offset is past the Encryption BKTR table start offset                                                                                                     |
| 0x235E02          | 2      | 4527        | NCA-path used with the wrong titleID.                                                                                                                                                |
| 0x236002          | 2      | 4528        | NCA header value is out of range                                                                                                                                                     |
| 0x236202          | 2      | 4529        | NCA FS header value is out of range                                                                                                                                                  |
| 0x236802          | 2      | 4532        | PartitionFS hash block size is not a power of 2                                                                                                                                      |
| 0x236A02          | 2      | 4533        | PartitionFS hash "always\_2" field is not 2                                                                                                                                          |
| 0x236C02          | 2      | 4534        | PartitionFS hash table is too small for main data                                                                                                                                    |
| 0x236E02          | 2      | 4535        | Invalid PartitionFS block hash                                                                                                                                                       |
| 0x249802          | 2      | 4684        | Invalid FAT file number.                                                                                                                                                             |
| 0x249C02          | 2      | 4686        | Invalid FAT format for BIS User partition.                                                                                                                                           |
| 0x249E02          | 2      | 4687        | Invalid FAT format for BIS System partition.                                                                                                                                         |
| 0x24A002          | 2      | 4688        | Invalid FAT format for BIS Safe partition.                                                                                                                                           |
| 0x24A202          | 2      | 4689        | Invalid FAT format for BIS Calibration partition.                                                                                                                                    |
| 0x250E02          | 2      | 4743        | [Corrupted](NAX0.md "wikilink") NAX0 header.                                                                                                                                         |
| 0x251002          | 2      | 4744        | Invalid [NAX0](NAX0.md "wikilink") magicnum.                                                                                                                                         |
| 0x280202          | 2      | 5121        | Invalid FAT size                                                                                                                                                                     |
| 0x280402          | 2      | 5122        | Invalid FAT BPB (BIOS Parameter Block)                                                                                                                                               |
| 0x280602          | 2      | 5123        | Invalid FAT parameter                                                                                                                                                                |
| 0x280802          | 2      | 5124        | Invalid FAT sector                                                                                                                                                                   |
| 0x280A02          | 2      | 5125        | Invalid FAT sector                                                                                                                                                                   |
| 0x280C02          | 2      | 5126        | Invalid FAT sector                                                                                                                                                                   |
| 0x280E02          | 2      | 5127        | Invalid FAT sector                                                                                                                                                                   |
| 0x296A02          | 2      | 5301        | Mountpoint not found                                                                                                                                                                 |
| 0x2EE202          | 2      | 6001        | Invalid input                                                                                                                                                                        |
| 0x2EE602          | 2      | 6003        | Path too long                                                                                                                                                                        |
| 0x2EE802          | 2      | 6004        | Invalid character.                                                                                                                                                                   |
| 0x2EEA02          | 2      | 6005        | Invalid directory path.                                                                                                                                                              |
| 0x2EEC02          | 2      | 6006        | Unable to retrieve directory from path                                                                                                                                               |
| 0x2F5A02          | 2      | 6061        | Offset outside storage                                                                                                                                                               |
| 0x313802          | 2      | 6300        | Operation not supported                                                                                                                                                              |
| 0x320002          | 2      | 6400        | Permission denied                                                                                                                                                                    |
| 0x326602          | 2      | 6451        | Missing titlekey(?) required to mount content                                                                                                                                        |
| 0x326E02          | 2      | 6455        | File not closed                                                                                                                                                                      |
| 0x327002          | 2      | 6456        | Directory not closed                                                                                                                                                                 |
| 0x327402          | 2      | 6458        | FS allocators already registered                                                                                                                                                     |
| 0x327602          | 2      | 6459        | FS allocators already used                                                                                                                                                           |
| 0x327A02          | 2      | 6461        | FS allocator alignment violation                                                                                                                                                     |
| 0x339402          | 2      | 6602        | File not found.                                                                                                                                                                      |
| 0x339602          | 2      | 6603        | Directory not found.                                                                                                                                                                 |
| 0x803             | 3      | 4           | OS busy                                                                                                                                                                              |
| 0xE03             | 3      | 7           | Invalid parameter                                                                                                                                                                    |
| 0x1003            | 3      | 8           | Out of memory                                                                                                                                                                        |
| 0x1203            | 3      | 9           | Out of resources                                                                                                                                                                     |
| 0x3EA03           | 3      | 501         | Invalid handle                                                                                                                                                                       |
| 0x3EE03           | 3      | 503         | Invalid memory mirror                                                                                                                                                                |
| 0x7FE03           | 3      | 1023        | TLS slot is not allocated                                                                                                                                                            |
| 0xA05             | 5      | 5           | [NcaID](Content%20Manager%20services.md "wikilink") not found. Returned when attempting to mount titles which exist that aren't \*8XX titles, the same way \*8XX titles are mounted. |
| 0xE05             | 5      | 7           | TitleId not found                                                                                                                                                                    |
| 0x1805            | 5      | 12          | Invalid StorageId                                                                                                                                                                    |
| 0xDC05            | 5      | 110         | Gamecard not inserted                                                                                                                                                                |
| 0x17C05           | 5      | 190         | Gamecard not initialized                                                                                                                                                             |
| 0x1F405           | 5      | 250         | Sdcard not inserted                                                                                                                                                                  |
| 0x20805           | 5      | 260         | Storage not mounted                                                                                                                                                                  |
| 0x806             | 6      | 4           | Converted from error 0xD401                                                                                                                                                          |
| 0x1006            | 6      | 8           | Converted from error 0xE401                                                                                                                                                          |
| 0x408             | 8      | 2           | Program location entry not found                                                                                                                                                     |
| 0x608             | 8      | 3           | Invalid context for control location                                                                                                                                                 |
| 0x808             | 8      | 4           | Storage not found                                                                                                                                                                    |
| 0xA08             | 8      | 5           | Access denied                                                                                                                                                                        |
| 0xC08             | 8      | 6           | Offline manual HTML location entry not found                                                                                                                                         |
| 0xE08             | 8      | 7           | Title is not registered                                                                                                                                                              |
| 0x1008            | 8      | 8           | Control location entry for host not found                                                                                                                                            |
| 0x1208            | 8      | 9           | Legal info HTML location entry not found                                                                                                                                             |
| 0x209             | 9      | 1           | Args too long.                                                                                                                                                                       |
| 0x409             | 9      | 2           | Maximum processes loaded.                                                                                                                                                            |
| 0x609             | 9      | 3           | NPDM too big.                                                                                                                                                                        |
| 0x19009           | 9      | 200         | Invalid access control sizes in NPDM.                                                                                                                                                |
| 0x809             | 9      | 4           | Invalid NPDM.                                                                                                                                                                        |
| 0xA09             | 9      | 5           | Invalid files.                                                                                                                                                                       |
| 0xE09             | 9      | 7           | Already registered.                                                                                                                                                                  |
| 0x1009            | 9      | 8           | Title not found.                                                                                                                                                                     |
| 0x1209            | 9      | 9           | Title-id in ACI0 doesn't match range in ACID.                                                                                                                                        |
| 0x6609            | 9      | 51          | Invalid memory state/permission                                                                                                                                                      |
| 0x6A09            | 9      | 53          | Invalid NRR                                                                                                                                                                          |
| 0xA209            | 9      | 81          | Unaligned NRR address                                                                                                                                                                |
| 0xA409            | 9      | 82          | Bad NRR size                                                                                                                                                                         |
| 0xAA09            | 9      | 85          | Bad NRR address                                                                                                                                                                      |
| 0xAE09            | 9      | 87          | Bad initialization                                                                                                                                                                   |
| 0xC809            | 9      | 100         | Unknown ACI0 descriptor                                                                                                                                                              |
| 0xCE09            | 9      | 103         | ACID/ACI0 don't match for descriptor "KernelFlags"                                                                                                                                   |
| 0xD009            | 9      | 104         | ACID/ACI0 don't match for descriptor "SyscallMask"                                                                                                                                   |
| 0xD409            | 9      | 106         | ACID/ACI0 don't match for descriptor "MapIoOrNormalRange"                                                                                                                            |
| 0xD609            | 9      | 107         | ACID/ACI0 don't match for descriptor "MapNormalPage"                                                                                                                                 |
| 0xDE09            | 9      | 111         | ACID/ACI0 don't match for descriptor "InterruptPair"                                                                                                                                 |
| 0xE209            | 9      | 113         | ACID/ACI0 don't match for descriptor "ApplicationType"                                                                                                                               |
| 0xE409            | 9      | 114         | ACID/ACI0 don't match for descriptor "KernelReleaseVersion"                                                                                                                          |
| 0xE609            | 9      | 115         | ACID/ACI0 don't match for descriptor "HandleTableSize"                                                                                                                               |
| 0xE809            | 9      | 116         | ACID/ACI0 don't match for descriptor "DebugFlags"                                                                                                                                    |
| 0x1940A           | 10     | 202         | Invalid CMIF header size.                                                                                                                                                            |
| 0x1A60A           | 10     | 211         | Invalid CMIF input header.                                                                                                                                                           |
| 0x1A80A           | 10     | 212         | Invalid CMIF output header.                                                                                                                                                          |
| 0x1BA0A           | 10     | 221         | Invalid method dispatch ID.                                                                                                                                                          |
| 0x1D60A           | 10     | 235         | Invalid in object count.                                                                                                                                                             |
| 0x1D80A           | 10     | 236         | Invalid out object count.                                                                                                                                                            |
| 0x25A0A           | 10     | 301         | Out of domain entries.                                                                                                                                                               |
| 0x20B             | 11     | 1           | Unsupported operation                                                                                                                                                                |
| 0xCC0B            | 11     | 102         | Out of server session memory                                                                                                                                                         |
| 0x11A0B           | 11     | 141         | Went past maximum during marshalling.                                                                                                                                                |
| 0x1900B           | 11     | 200         | Session doesn't support domains.                                                                                                                                                     |
| 0x25A0B           | 11     | 301         | Remote process is dead.                                                                                                                                                              |
| 0x3260B           | 11     | 403         | Unknown request type                                                                                                                                                                 |
| 0x3D60B           | 11     | 491         | IPC Query 1 failed.                                                                                                                                                                  |
| 0x20F             | 15     | 1           | Pid not found                                                                                                                                                                        |
| 0x60F             | 15     | 3           | Process has no pending events                                                                                                                                                        |
| 0xA0F             | 15     | 5           | Application already running                                                                                                                                                          |
| 0x410             | 16     | 2           | Title-id not found                                                                                                                                                                   |
| 0xF010            | 16     | 120         | Gamecard sysupdate not required                                                                                                                                                      |
| 0x1F610           | 16     | 251         | Unexpected StorageId                                                                                                                                                                 |
| 0x215             | 21     | 1           | Out of processes                                                                                                                                                                     |
| 0x415             | 21     | 2           | Not initialized.                                                                                                                                                                     |
| 0x615             | 21     | 3           | Max sessions                                                                                                                                                                         |
| 0x815             | 21     | 4           | Service already registered                                                                                                                                                           |
| 0xA15             | 21     | 5           | Out of services                                                                                                                                                                      |
| 0xC15             | 21     | 6           | Invalid name (all zeroes)                                                                                                                                                            |
| 0xE15             | 21     | 7           | Service not registered                                                                                                                                                               |
| 0x1015            | 21     | 8           | Permission denied                                                                                                                                                                    |
| 0x1215            | 21     | 9           | Service Access Control too big.                                                                                                                                                      |
| 0x416             | 22     | 2           | Address space is full                                                                                                                                                                |
| 0x616             | 22     | 3           | NRO already loaded                                                                                                                                                                   |
| 0x816             | 22     | 4           | Invalid NRO header values                                                                                                                                                            |
| 0xC16             | 22     | 6           | Bad NRR magic                                                                                                                                                                        |
| 0x1016            | 22     | 8           | Reached max NRR count                                                                                                                                                                |
| 0x1216            | 22     | 9           | Unable to verify NRO hash or NRR signature                                                                                                                                           |
| 0x80216           | 22     | 1025        | Address not page-aligned                                                                                                                                                             |
| 0x80416           | 22     | 1026        | Incorrect NRO size                                                                                                                                                                   |
| 0x80816           | 22     | 1028        | NRO not loaded                                                                                                                                                                       |
| 0x80A16           | 22     | 1029        | NRR not loaded                                                                                                                                                                       |
| 0x80C16           | 22     | 1030        | Already initialized                                                                                                                                                                  |
| 0x80E16           | 22     | 1031        | Not initialized                                                                                                                                                                      |
| 0x41A             | 26     | 2           | Argument is invalid                                                                                                                                                                  |
| 0xC81A            | 26     | 100         | Incorrect buffer size                                                                                                                                                                |
| 0xCA1A            | 26     | 101         | Unknown TZ error                                                                                                                                                                     |
| 0xD01A            | 26     | 104         | All AES engines busy                                                                                                                                                                 |
| 0xD21A            | 26     | 105         | Invalid AES engine-id                                                                                                                                                                |
| 0x19269           | 105    | 201         | Null settings name                                                                                                                                                                   |
| 0x19469           | 105    | 202         | Null settings key                                                                                                                                                                    |
| 0x19669           | 105    | 203         | Null settings value                                                                                                                                                                  |
| 0x19A69           | 105    | 205         | Null settings value buffer                                                                                                                                                           |
| 0x1A069           | 105    | 208         | Null setting value size buffer                                                                                                                                                       |
| 0x1A269           | 105    | 209         | Null debug mode flag buffer                                                                                                                                                          |
| 0x1BA69           | 105    | 221         | Setting group name has zero length                                                                                                                                                   |
| 0x1BC69           | 105    | 222         | Empty settings item key                                                                                                                                                              |
| 0x1E269           | 105    | 241         | Setting group name is too long (64 character limit?)                                                                                                                                 |
| 0x1E469           | 105    | 242         | Setting name is too long (64 character limit?)                                                                                                                                       |
| 0x20A69           | 105    | 261         | Setting group name ends with '.' or contains invalid characters (allowed: \[a-z0-9\_\\-.\])                                                                                          |
| 0x20C69           | 105    | 262         | Setting name ends with '.' or contains invalid characters (allowed: \[a-z0-9\_\\-.\])                                                                                                |
| 0x4DA69           | 105    | 621         | Null language code buffer                                                                                                                                                            |
| 0x4EE69           | 105    | 631         | Null network settings buffer                                                                                                                                                         |
| 0x4F069           | 105    | 632         | Null network settings output count buffer                                                                                                                                            |
| 0x50269           | 105    | 641         | Null backlight settings buffer                                                                                                                                                       |
| 0x51669           | 105    | 651         | Null Bluetooth device setting buffer                                                                                                                                                 |
| 0x51869           | 105    | 652         | Null Bluetooth device setting output count buffer                                                                                                                                    |
| 0x51A69           | 105    | 653         | Null Bluetooth enable flag buffer                                                                                                                                                    |
| 0x51C69           | 105    | 654         | Null Bluetooth AFH enable flag buffer                                                                                                                                                |
| 0x51E69           | 105    | 655         | Null Bluetooth boost enable flag buffer                                                                                                                                              |
| 0x52069           | 105    | 656         | Null BLE pairing settings buffer                                                                                                                                                     |
| 0x52269           | 105    | 657         | Null BLE pairing settings entry count buffer                                                                                                                                         |
| 0x52A69           | 105    | 661         | Null external steady clock source ID buffer                                                                                                                                          |
| 0x52C69           | 105    | 662         | Null user system clock context buffer                                                                                                                                                |
| 0x52E69           | 105    | 663         | Null network system clock context buffer                                                                                                                                             |
| 0x53069           | 105    | 664         | Null user system clock automatic correction enabled flag buffer                                                                                                                      |
| 0x53269           | 105    | 665         | Null shutdown RTC value buffer                                                                                                                                                       |
| 0x53469           | 105    | 666         | Null external steady clock internal offset buffer                                                                                                                                    |
| 0x53E69           | 105    | 671         | Null account settings buffer                                                                                                                                                         |
| 0x55269           | 105    | 681         | Null audio volume buffer                                                                                                                                                             |
| 0x55669           | 105    | 683         | Null ForceMuteOnHeadphoneRemoved buffer                                                                                                                                              |
| 0x55869           | 105    | 684         | Null headphone volume warning count buffer                                                                                                                                           |
| 0x55E69           | 105    | 687         | Invalid audio output mode                                                                                                                                                            |
| 0x56069           | 105    | 688         | Null headphone volume update flag buffer                                                                                                                                             |
| 0x56669           | 105    | 691         | Null console information upload flag buffer                                                                                                                                          |
| 0x57A69           | 105    | 701         | Null automatic application download flag buffer                                                                                                                                      |
| 0x57C69           | 105    | 702         | Null notification settings buffer                                                                                                                                                    |
| 0x57E69           | 105    | 703         | Null account notification settings entry count buffer                                                                                                                                |
| 0x58069           | 105    | 704         | Null account notification settings buffer                                                                                                                                            |
| 0x58E69           | 105    | 711         | Null vibration master volume buffer                                                                                                                                                  |
| 0x59069           | 105    | 712         | Null NX controller settings buffer                                                                                                                                                   |
| 0x59269           | 105    | 713         | Null NX controller settings entry count buffer                                                                                                                                       |
| 0x59469           | 105    | 714         | Null USB full key enable flag buffer                                                                                                                                                 |
| 0x5A269           | 105    | 721         | Null TV settings buffer                                                                                                                                                              |
| 0x5A469           | 105    | 722         | Null EDID buffer                                                                                                                                                                     |
| 0x5B669           | 105    | 731         | Null data deletion settings buffer                                                                                                                                                   |
| 0x5CA69           | 105    | 741         | Null initial system applet program ID buffer                                                                                                                                         |
| 0x5CC69           | 105    | 742         | Null overlay disp program ID buffer                                                                                                                                                  |
| 0x5CE69           | 105    | 743         | Null IsInRepairProcess buffer                                                                                                                                                        |
| 0x5D069           | 105    | 744         | Null RequiresRunRepairTimeReviser buffer                                                                                                                                             |
| 0x5DE69           | 105    | 751         | Null device timezone location name buffer                                                                                                                                            |
| 0x5F269           | 105    | 761         | Null primary album storage buffer                                                                                                                                                    |
| 0x60669           | 105    | 771         | Null USB 3.0 enable flag buffer                                                                                                                                                      |
| 0x60869           | 105    | 772         | Null USB Type-C power source circuit version buffer                                                                                                                                  |
| 0x61A69           | 105    | 781         | Null battery lot buffer                                                                                                                                                              |
| 0x62E69           | 105    | 791         | Null serial number buffer                                                                                                                                                            |
| 0x64269           | 105    | 801         | Null lock screen flag buffer                                                                                                                                                         |
| 0x64669           | 105    | 803         | Null color set ID buffer                                                                                                                                                             |
| 0x64869           | 105    | 804         | Null quest flag buffer                                                                                                                                                               |
| 0x64A69           | 105    | 805         | Null wireless certification file size buffer                                                                                                                                         |
| 0x64C69           | 105    | 806         | Null wireless certification file buffer                                                                                                                                              |
| 0x64E69           | 105    | 807         | Null initial launch settings buffer                                                                                                                                                  |
| 0x65069           | 105    | 808         | Null device nickname buffer                                                                                                                                                          |
| 0x65269           | 105    | 809         | Null battery percentage flag buffer                                                                                                                                                  |
| 0x65469           | 105    | 810         | Null applet launch flags buffer                                                                                                                                                      |
| 0x7E869           | 105    | 1012        | Null wireless LAN enable flag buffer                                                                                                                                                 |
| 0x7FA69           | 105    | 1021        | Null product model buffer                                                                                                                                                            |
| 0x80E69           | 105    | 1031        | Null NFC enable flag buffer                                                                                                                                                          |
| 0x82269           | 105    | 1041        | Null ECI device certificate buffer                                                                                                                                                   |
| 0x82469           | 105    | 1042        | Null E-Ticket device certificate buffer                                                                                                                                              |
| 0x83669           | 105    | 1051        | Null sleep settings buffer                                                                                                                                                           |
| 0x84A69           | 105    | 1061        | Null EULA version buffer                                                                                                                                                             |
| 0x84C69           | 105    | 1062        | Null EULA version entry count buffer                                                                                                                                                 |
| 0x85E69           | 105    | 1071        | Null LDN channel buffer                                                                                                                                                              |
| 0x87269           | 105    | 1081        | Null SSL key buffer                                                                                                                                                                  |
| 0x87469           | 105    | 1082        | Null SSL certificate buffer                                                                                                                                                          |
| 0x88669           | 105    | 1091        | Null telemetry flags buffer                                                                                                                                                          |
| 0x89A69           | 105    | 1101        | Null Gamecard key buffer                                                                                                                                                             |
| 0x89C69           | 105    | 1102        | Null Gamecard certificate buffer                                                                                                                                                     |
| 0x8AE69           | 105    | 1111        | Null PTM battery lot buffer                                                                                                                                                          |
| 0x8B069           | 105    | 1112        | Null PTM fuel gauge parameter buffer                                                                                                                                                 |
| 0x8C269           | 105    | 1121        | Null ECI device key buffer                                                                                                                                                           |
| 0x8C469           | 105    | 1122        | Null E-Ticket device key buffer                                                                                                                                                      |
| 0x8D669           | 105    | 1131        | Null speaker parameter buffer                                                                                                                                                        |
| 0x8EA69           | 105    | 1141        | Null firmware version buffer                                                                                                                                                         |
| 0x8EC69           | 105    | 1142        | Null firmware version digest buffer                                                                                                                                                  |
| 0x8EE69           | 105    | 1143        | Null rebootless system update version buffer                                                                                                                                         |
| 0x8FE69           | 105    | 1151        | Null Mii author ID buffer                                                                                                                                                            |
| 0x91269           | 105    | 1161        | Null fatal flags buffer                                                                                                                                                              |
| 0x92669           | 105    | 1171        | Null auto update enable flag buffer                                                                                                                                                  |
| 0x93A69           | 105    | 1181        | Null external RTC reset flag buffer                                                                                                                                                  |
| 0x94E69           | 105    | 1191        | Null push notification activity mode buffer                                                                                                                                          |
| 0x96269           | 105    | 1201        | Null service discovery control setting buffer                                                                                                                                        |
| 0x97669           | 105    | 1211        | Null error report share permission buffer                                                                                                                                            |
| 0x98A69           | 105    | 1221        | Null LCD vendor ID buffer                                                                                                                                                            |
| 0x99E69           | 105    | 1231        | Null console SixAxis sensor acceleration bias buffer                                                                                                                                 |
| 0x9A069           | 105    | 1232        | Null console SixAxis sensor angular velocity bias buffer                                                                                                                             |
| 0x9A269           | 105    | 1233        | Null console SixAxis sensor acceleration gain buffer                                                                                                                                 |
| 0x9A469           | 105    | 1234        | Null console SixAxis sensor angular velocity gain buffer                                                                                                                             |
| 0x9A669           | 105    | 1235        | Null console SixAxis sensor angular velocity time bias buffer                                                                                                                        |
| 0x9A869           | 105    | 1236        | Null console SixAxis sensor angular acceleration buffer                                                                                                                              |
| 0x9B269           | 105    | 1241        | Null keyboard layout buffer                                                                                                                                                          |
| 0x9BA69           | 105    | 1245        | Invalid keyboard layout                                                                                                                                                              |
| 0x9C669           | 105    | 1251        | Null web inspector flag buffer                                                                                                                                                       |
| 0x9C869           | 105    | 1252        | Null allowed SSL hosts buffer                                                                                                                                                        |
| 0x9CA69           | 105    | 1253        | Null allowed SSL hosts entry count buffer                                                                                                                                            |
| 0x9CC69           | 105    | 1254        | Null host FS mount point buffer                                                                                                                                                      |
| 0x9EE69           | 105    | 1271        | Null Amiibo key buffer                                                                                                                                                               |
| 0x9F069           | 105    | 1272        | Null Amiibo ECQV certificate buffer                                                                                                                                                  |
| 0x9F269           | 105    | 1273        | Null Amiibo ECDSA certificate buffer                                                                                                                                                 |
| 0x9F469           | 105    | 1274        | Null Amiibo ECQV BLS key buffer                                                                                                                                                      |
| 0x9F669           | 105    | 1275        | Null Amiibo ECQV BLS certificate buffer                                                                                                                                              |
| 0x9F869           | 105    | 1276        | Null Amiibo ECQV BLS root certificate buffer                                                                                                                                         |
| 0x272             | 114    | 1           | Generic error                                                                                                                                                                        |
| 0xCC74            | 116    | 102         | Time not set                                                                                                                                                                         |
| 0x287C            | 124    | 20          | Argument is NULL                                                                                                                                                                     |
| 0x2C7C            | 124    | 22          | Argument is invalid                                                                                                                                                                  |
| 0x3C7C            | 124    | 30          | Bad input buffer size                                                                                                                                                                |
| 0x407C            | 124    | 32          | Invalid input buffer                                                                                                                                                                 |
| 0x27E             | 126    | 1           | Invalid argument                                                                                                                                                                     |
| 0x87E             | 126    | 4           | Entry not found                                                                                                                                                                      |
| 0xCE7E            | 126    | 67          | Invalid database signature value (should be "NFDB")                                                                                                                                  |
| 0xD27E            | 126    | 69          | Invalid database entry count                                                                                                                                                         |
| 0x1987E           | 126    | 204         | Development/debug-only behavior                                                                                                                                                      |
| 0x4680            | 128    | 35          | Error while launching applet.                                                                                                                                                        |
| 0x4A80            | 128    | 37          | Title-ID not found. Caused by code 0x410 when applet launch fails                                                                                                                    |
| 0x3E880           | 128    | 500         | Invalid IStorage size (negative?)                                                                                                                                                    |
| 0x3EC80           | 128    | 502         | IStorage has already been opened by another accessor                                                                                                                                 |
| 0x3EE80           | 128    | 503         | IStorage Read/Write out-of-bounds                                                                                                                                                    |
| 0x3FE80           | 128    | 511         | IStorage opened as wrong type (data opened as transfermem, transfermem opened as data)                                                                                               |
| 0x4B080           | 128    | 600         | Failed to allocate memory for IStorage                                                                                                                                               |
| 0x59080           | 128    | 712         | Thread stack pool exhausted (out of memory)                                                                                                                                          |
| 0x7A880           | 128    | 980         | `am.debug!dev_function` setting needs to be set                                                                                                                                      |
| 0xA83             | 131    | 5           | Unrecognized applet ID                                                                                                                                                               |
| 0x3CF089          | 137    | 7800        | Unknown/invalid libcurl error.                                                                                                                                                       |
| 0x3E8289-0x3F4089 | 137    | 8001-8096   | libcurl error 1-96. Some of the libcurl errors in the error-table map to the above unknown-libcurl-error however.                                                                    |
| 0x68A             | 138    | 3           | Not initialized.                                                                                                                                                                     |
| 0x668C            | 140    | 51          | USB data-transfer in progress                                                                                                                                                        |
| 0xD48C            | 140    | 106         | Invalid descriptor                                                                                                                                                                   |
| 0x1928C           | 140    | 201         | USB device not bound / interface already enabled                                                                                                                                     |
| 0x299             | 153    | 1           | Invalid audio device                                                                                                                                                                 |
| 0x499             | 153    | 2           | Operation couldn't complete successfully                                                                                                                                             |
| 0x699             | 153    | 3           | Invalid sample rate                                                                                                                                                                  |
| 0x899             | 153    | 4           | Buffer size too small                                                                                                                                                                |
| 0x1099            | 153    | 8           | Too many buffers are still unreleased                                                                                                                                                |
| 0x1499            | 153    | 10          | Invalid channel count                                                                                                                                                                |
| 0x40299           | 153    | 513         | Invalid/Unsupported operation                                                                                                                                                        |
| 0xC0099           | 153    | 1536        | Invalid handle                                                                                                                                                                       |
| 0xC0899           | 153    | 1540        | Audio output was already started                                                                                                                                                     |
| 0x3C9D            | 157    | 30          | Address is NULL                                                                                                                                                                      |
| 0x3E9D            | 157    | 31          | PID is NULL                                                                                                                                                                          |
| 0x549D            | 157    | 42          | Already bound                                                                                                                                                                        |
| 0xCC9D            | 157    | 102         | Invalid PID                                                                                                                                                                          |
| 0xAA3             | 163    | 5           | System is booting up repair process without VOL+ held down.                                                                                                                          |
| 0xCA3             | 163    | 6           | System is booting up repair process that requires RepairTimeReviser but does not have special cartridge inserted.                                                                    |
| 0xF0CD            | 205    | 120         | IR image data not available/ready.                                                                                                                                                   |
| 0x35B             | 347    | 1           | Failed to init SM.                                                                                                                                                                   |
| 0x55B             | 347    | 2           | Failed to init FS.                                                                                                                                                                   |
| 0x75B             | 347    | 3           | Failed to to open NRO file. May also happen when SD card isn't inserted / SD mounting failed earlier.                                                                                |
| 0x95B             | 347    | 4           | Failed to read NRO header.                                                                                                                                                           |
| 0xB5B             | 347    | 5           | Invalid NRO magic.                                                                                                                                                                   |
| 0xD5B             | 347    | 6           | Invalid NRO segments.                                                                                                                                                                |
| 0xF5B             | 347    | 7           | Failed to read NRO.                                                                                                                                                                  |
| 0x135B            | 347    | 9           | Failed to allocate heap.                                                                                                                                                             |
| 0x255B            | 347    | 18          | Failed to map code-binary memory.                                                                                                                                                    |
| 0x275B            | 347    | 19          | Failed to map code memory (.text).                                                                                                                                                   |
| 0x295B            | 347    | 20          | Failed to map code memory (.rodata).                                                                                                                                                 |
| 0x2B5B            | 347    | 21          | Failed to map code memory (.data+.bss).                                                                                                                                              |
| 0x315B            | 347    | 24          | Failed to unmap code memory (.text).                                                                                                                                                 |
| 0x335B            | 347    | 25          | Failed to unmap code memory (.rodata).                                                                                                                                               |
| 0x355B            | 347    | 26          | Failed to unmap code memory (.data+.bss).                                                                                                                                            |

## FS Error Codes

The following are the error codes recognized by
nn::fs::detail::LogErrorMessage found in some
[factory](Factory%20Setup.md "wikilink")
titles:

| Value               | Description                                               | Message                                                                                      |
| ------------------- | --------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| 0x7802              | 60                                                        | Error: Specified mount name already exists.                                                  |
| 0xD401              | 106                                                       | Error: Passed buffer is not usable for fs library.                                           |
| 0x7D202             | 1001                                                      | Error: Specified partition is not found.                                                     |
| 0x7D402             | 1002                                                      | Error: Specified target is not found.                                                        |
| 0xFA002 - 0x138602  | 2000 - 2499                                               | Error: Failed to access SD card.                                                             |
| 0x136802 - 0x176E02 | 2500 - 2999                                               | Error: Failed to access game card.                                                           |
| 0x177202            | 3001                                                      | Error: Specified operation is not implemented.                                               |
| 0x177A02            | 3005                                                      | Error: Specified value is out of range.                                                      |
| 0x1B5802 - 0x1F3E02 | 3500 - 3999                                               | Error: Failed to access MMC.                                                                 |
| 0x1F4202 - 0x219602 | 4001 - 4299                                               | Error: ROM is corrupted.                                                                     |
| 0x219A02 - 0x232602 | 4301 - 4499                                               | Error: Save data is corrupted.                                                               |
| 0x232A02 - 0x23EE02 | 4501 - 4599                                               | Error: NCA is corrupted.                                                                     |
| 0x23F202 - 0x243E02 | 4601 - 4639                                               | Error: Integrity verification failed.                                                        |
| 0x244202 - 0x246602 | 4641 - 4659                                               | Error: Partition FS is corrupted.                                                            |
| 0x246A02 - 0x248E02 | 4661 - 4679                                               | Error: Built-in-storage is corrupted.                                                        |
| 0x249202 - 0x24B602 | 4681 - 4699                                               | Error: FAT FS is corrupted.                                                                  |
| 0x24BA02 - 0x24DE02 | 4701 - 4719                                               | Error: HOST FS is corrupted.                                                                 |
| 0x1F4002 - 0x270E02 | 4000, 4300, 4500, 4600, 4640, 4660, 4680, 4700, 4720-4999 | Error: Data is corrupted.                                                                    |
| 0x271002 - 0x2EDE02 | 5000-5999                                                 | Error: Unexpected failure occurred.                                                          |
| 0x2EE402 - 0x2F1A02 | 6002-6029                                                 | Error: Invalid path was specified.                                                           |
| 0x2F5A02            | 6061                                                      | Error: Invalid offset was specified.                                                         |
| 0x2F5C02            | 6062                                                      | Error: Invalid size was specified.                                                           |
| 0x2F5E02            | 6063                                                      | Error: Null pointer argument was specified.                                                  |
| 0x2EE002            | 6000                                                      | Error: Precondition violation.                                                               |
| 0x2EE202 - 0x306E02 | 6001-6199                                                 | Error: Invalid argument was specified.                                                       |
| 0x307202            | 6201                                                      | Error: OpenMode\_AllowAppend is required for implicit extension of file size by WriteFile(). |
| 0x307002 - 0x313602 | 6200, 6202 - 6299                                         | Error: Invalid operation for the open mode.                                                  |
| 0x313802 - 0x31FE02 | 6300-6399                                                 | Error: Unsupported operation.                                                                |
| 0x320002 - 0x32C602 | 6400-6499                                                 | Error: Permission denied.                                                                    |
| 0x346402            | 6706                                                      | Error: Enough journal space is not left.                                                     |
| 0x346A02            | 6709                                                      | Error: The open count of files and directories reached the limitation.                       |

# Fatal Errors

| Error     | Description                                                                                                                                                                                        |
| --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2162-0002 | Can be triggered by running [svcBreak](SVC.md "wikilink"). The svcBreak params have no affect on the value of the thrown error-code.                                                               |
| 2168-0000 | Userland ARM undefined instruction exception                                                                                                                                                       |
| 2168-0001 | Userland ARM prefetch-abort due to PC set to non-executable region                                                                                                                                 |
| 2168-0002 | Userland ARM data abort. Also caused by abnormal process termination via [svcExitProcess](SVC.md "wikilink"). Note: directly jumping to nnMain()-retaddr from non-main-thread has the same result. |
| 2168-0003 | Userland PC address not aligned to 4 bytes                                                                                                                                                         |
| 2168-0008 | Can occur when attempting to call an svc outside the whitelist                                                                                                                                     |

# Support Errors

This section is for Support Errors displayed by the error-applet,
separate from the normal Result errors.

## Support Modules

| Value | Name                                                   |
| ----- | ------------------------------------------------------ |
| 800   | [General web-applet](Internet%20Browser.md "wikilink") |
| 809   | [WifiWebAuthApplet](Internet%20Browser.md "wikilink")  |
| 810   | [Whitelisted-applet](Internet%20Browser.md "wikilink") |
| 811   | [ShopN](Internet%20Browser.md "wikilink")              |

8XX is for/includes system
applets.

## Errors

| Error | Module                     | Description | Notes               |
| ----- | -------------------------- | ----------- | ------------------- |
|       | {web-applets listed above} | 2750        | MP4 parsing failed. |

Normal error-codes displayed by the system also use the same format as
fatal-errors.

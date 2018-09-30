This page describes the format of savegames contained in NAND. NAND
savegames do not use an container with the entire file encrypted.
Various areas of the saveimage is uninitialized data, resulting in
encrypted data in those areas (like 3DS did).

## Main header

The header is 0x4000 bytes long.

There are 2 headers stored at 0x0 and 0x4000, presumably for commit and
rollback purposes.

| Image offset | Length | Description                   |
| ------------ | ------ | ----------------------------- |
| 0x000        | 0x100  | AES-CMAC header               |
| 0x100        | 0x200  | DISF header                   |
| 0x300        | 0x44   | Duplex header                 |
| 0x344        | 0xC4   | Integrity verification header |
| 0x408        | 0x200  | Journal header                |
| 0x608        | 0x48   | Save header                   |
| 0x650        | 0x40   | Main data remap header        |
| 0x690        | 0x40   | Meta data remap header        |
| 0x6D0        | 0x8    | Unknown                       |
| 0x6D8        | 0x200  | Extra data A                  |
| 0x8D8        | 0x200  | Extra data B                  |
| 0xAD8        | 0x3528 | Additional storage            |

The additional storage at the end of the header is used to store any
extra header data. This data's structure is determined by offsets stored
in the main part of the header.

### AES CMAC header

| Image offset | Length | Description                            |
| ------------ | ------ | -------------------------------------- |
| 0x00         | 0x10   | AES-CMAC over DISF header (size 0x200) |
| 0x10         | 0xF0   | Zero padding                           |

The final CMAC key used for this is generated using GenerateAesKek with
a kek source and the device key, along with and LoadAesKey and a set key
seed.

### DISF

This section contains information about the structure of the save
file.

| Start | Length | Description                                                  |
| ----- | ------ | ------------------------------------------------------------ |
| 0x000 | 4      | Magic ("DISF")                                               |
| 0x004 | 4      | Magic Number (0x40000)                                       |
| 0x008 | 32     | Hash of start of DPFS to end of 0x4000 block (0x300-0x3FFF)  |
| 0x028 | 8      | Main data remap mapping table offset                         |
| 0x030 | 8      | Main data remap mapping table size                           |
| 0x038 | 8      | Meta data remap mapping table offset                         |
| 0x040 | 8      | Meta data remap mapping table size                           |
| 0x048 | 8      | Main data remap offset                                       |
| 0x050 | 8      | Main data remap size                                         |
| 0x058 | 8      | Duplex level 1 virtual offset A                              |
| 0x060 | 8      | Duplex level 1 virtual offset B                              |
| 0x068 | 8      | Duplex level 1 size                                          |
| 0x070 | 8      | Duplex level 2 virtual offset A                              |
| 0x078 | 8      | Duplex level 2 virtual offset B                              |
| 0x080 | 8      | Duplex level 2 size                                          |
| 0x088 | 8      | Journal storage virtual offset                               |
| 0x090 | 8      | Journal storage data size A                                  |
| 0x098 | 8      | Journal storage data size B                                  |
| 0x0A0 | 8      | Journal storage journal size                                 |
| 0x0A8 | 8      | Duplex master bitmap offset A                                |
| 0x0B0 | 8      | Duplex master bitmap offset B                                |
| 0x0B8 | 8      | Duplex master bitmap size                                    |
| 0x0C0 | 8      | IVFC master hash offset A                                    |
| 0x0C8 | 8      | IVFC master hash offset B                                    |
| 0x0D0 | 8      | IVFC master hash size                                        |
| 0x0D8 | 8      | Journal block table virtual offset                           |
| 0x0E0 | 8      | Journal block table size                                     |
| 0x0E8 | 8      | Virtual offset of bitmap of modified physical journal blocks |
| 0x0F0 | 8      | Size of bitmap of modified physical journal blocks           |
| 0x0F8 | 8      | Virtual offset of bitmap of modified virtual journal blocks  |
| 0x100 | 8      | Size of bitmap of modified virtual journal blocks            |
| 0x108 | 8      | Virtual offset of bitmap of free journal blocks              |
| 0x110 | 8      | Size of bitmap of free journal blocks                        |
| 0x118 | 8      | IVFC level 1 virtual offset                                  |
| 0x120 | 8      | IVFC level 1 size                                            |
| 0x128 | 8      | IVFC level 2 virtual offset                                  |
| 0x130 | 8      | IVFC level 2 size                                            |
| 0x138 | 8      | IVFC level 3 virtual offset                                  |
| 0x140 | 8      | IVFC level 3 size                                            |
| 0x148 | 8      | File allocation table virtual offset                         |
| 0x150 | 8      | File allocation table size                                   |
| 0x158 | 1      | Index of the active duplex master bitmap                     |
| 0x200 |        | End                                                          |

### Duplex header

  - Block sizes are stored as powers of 2

| Start | Length | Description                    |
| ----- | ------ | ------------------------------ |
| 0x00  | 4      | Magic ("DPFS")                 |
| 0x04  | 4      | Magic Number (0x10000)         |
| 0x08  | 8      | Master bitmap offset           |
| 0x10  | 8      | Master bitmap size             |
| 0x18  | 4      | Master bitmap block size power |
| 0x1C  | 8      | Level 1 offset                 |
| 0x24  | 8      | Level 1 size                   |
| 0x2C  | 4      | Level 1 block size power       |
| 0x30  | 8      | Level 2 offset                 |
| 0x38  | 8      | Level 2 size                   |
| 0x40  | 4      | Level 2 block size power       |
|       |        |                                |

### Integrity verification header

  - Offsets for levels 1-3 come from the metadata remap storage
  - Offsets for level 4 comes from the main data remap storage
  - This is the same header used in NCA files

| Start | Length  | Description                             |
| ----- | ------- | --------------------------------------- |
| 0x00  | 4       | Magic ("IVFC")                          |
| 0x04  | 4       | Magic Number (0x20000)                  |
| 0x08  | 4       | Master hash size                        |
| 0xC   | 4       | Number of levels (Unused in save files) |
| 0x10  | 0x18\*6 | Level information for up to 6 levels    |
| 0xA0  | 32      | Salt seed                               |
|       |         |                                         |

#### Level information

  - 0x18 bytes long
  - Block sizes are stored as powers of 2

| Start | Length | Description      |
| ----- | ------ | ---------------- |
| 0x00  | 8      | Offset           |
| 0x08  | 8      | Size             |
| 0x10  | 4      | Block size power |
| 0x14  | 4      | Reserved         |
|       |        |                  |

### Journal header

| Start | Length | Description                    |
| ----- | ------ | ------------------------------ |
| 0x00  | 4      | Magic ("JNGL")                 |
| 0x04  | 4      | Magic Number (0x10000 or less) |
| 0x08  | 8      | Total size (Incl. journal)     |
| 0x10  | 8      | Journal size                   |
| 0x18  | 8      | Block size                     |
| 0x20  | 4      | Unknown (Must be 0 or 1)       |
| 0x24  | 4      | Main data block count          |
| 0x28  | 8      | Journal block count            |
| 0x200 |        | End                            |
|       |        |                                |

### Save FS header

  - Structure is different than
3DS.

| Start | Length | Description                                                |
| ----- | ------ | ---------------------------------------------------------- |
| 0x00  | 4      | Magic ("SAVE")                                             |
| 0x04  | 4      | Magic Number (0x60000)                                     |
| 0x08  | 8      | Number of blocks. Does not change if save file is resized. |
| 0x10  | 8      | Block Size                                                 |
|       |        | The below fields are read separately from the above fields |
| 0x18  | 8      | Block size                                                 |
| 0x20  | 8      | FAT offset                                                 |
| 0x28  | 4      | FAT entry count                                            |
| 0x2C  | 4      | Padding                                                    |
| 0x30  | 8      | Data offset                                                |
| 0x38  | 4      | Data block count                                           |
| 0x3C  | 4      | Padding                                                    |
| 0x40  | 8      | Directory table block index                                |
| 0x48  | 8      | File table block index                                     |
|       |        |                                                            |

### RMAP

  - There are generally two RMAP blocks in sequence.

| Start | Length | Description            |
| ----- | ------ | ---------------------- |
| 0x00  | 4      | Magic ("RMAP")         |
| 0x04  | 4      | Magic Number (0x10000) |
|       |        |                        |

## Files

### File Offset Table

  - Indexes 0 and 1 are reserved to point towards the folder and file
    tables.

#### File Offset Table Entry

| Start | Length | Description            |
| ----- | ------ | ---------------------- |
| 0x00  | 3      | Data offset, in blocks |
| 0x03  | 1      | Unknown, 80            |
| 0x04  | 4      | Unknown, 0             |

### File/Folder Table Entry

  - The root file/folder index is generally 2

| Start | Length | Description                                       |
| ----- | ------ | ------------------------------------------------- |
| 0x00  | 4      | Parent Folder Index                               |
| 0x04  | 64     | Filename                                          |
| 0x44  | 4      | File/Folder Index?                                |
| 0x48  | 4      | File offset index in offset table, 0 for folders  |
| 0x4c  | 8      | File size, or number of files for folders         |
| 0x54  | 8      | Unknown                                           |
| 0x5c  | 4      | Next File Index, same as folder index for folders |
|       |        |                                                   |

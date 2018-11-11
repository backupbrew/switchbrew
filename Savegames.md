This page describes the format of save files contained in NAND. These
files are stored as completely unencrypted, plaintext data. Save files
are not cleared upon creation, resulting in possible garbage data in
unused portions of the container.

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
| 0x004 | 4      | Version? (Upper 2 bytes must be 0x0004)                      |
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
| 0x160 | 8      | \[5.0.0+\] File allocation table IVFC master hash offset A   |
| 0x168 | 8      | \[5.0.0+\] File allocation table IVFC master hash offset B   |
| 0x170 | 8      | \[5.0.0+\] File allocation table IVFC level 1 virtual offset |
| 0x178 | 8      | \[5.0.0+\] File allocation table IVFC level 1 size           |
| 0x180 | 8      | \[5.0.0+\] File allocation table IVFC level 2 virtual offset |
| 0x188 | 8      | \[5.0.0+\] File allocation table IVFC level 2 size           |
| 0x200 |        | End                                                          |

### Duplex header

  - Block sizes are stored as powers of 2

| Start | Length | Description                             |
| ----- | ------ | --------------------------------------- |
| 0x00  | 4      | Magic ("DPFS")                          |
| 0x04  | 4      | Version? (Upper 2 bytes must be 0x0001) |
| 0x08  | 8      | Master bitmap offset                    |
| 0x10  | 8      | Master bitmap size                      |
| 0x18  | 4      | Master bitmap block size power          |
| 0x1C  | 8      | Level 1 offset                          |
| 0x24  | 8      | Level 1 size                            |
| 0x2C  | 4      | Level 1 block size power                |
| 0x30  | 8      | Level 2 offset                          |
| 0x38  | 8      | Level 2 size                            |
| 0x40  | 4      | Level 2 block size power                |
|       |        |                                         |

### Integrity verification header

  - Offsets for levels 1-3 come from the metadata remap storage
  - Offsets for level 4 comes from the main data remap storage
  - This is the same header used in NCA files

| Start | Length  | Description                             |
| ----- | ------- | --------------------------------------- |
| 0x00  | 4       | Magic ("IVFC")                          |
| 0x04  | 4       | Version? (Upper 2 bytes must be 0x0002) |
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

| Start | Length | Description                                          |
| ----- | ------ | ---------------------------------------------------- |
| 0x00  | 4      | Magic ("JNGL")                                       |
| 0x04  | 4      | Version? (Must be 0x10000 or less)                   |
| 0x08  | 8      | Total size (Incl. journal)                           |
| 0x10  | 8      | Journal size                                         |
| 0x18  | 8      | Block size                                           |
|       |        | The below fields are treated as a separate subheader |
| 0x20  | 4      | Version? (Must be 0 or 1)                            |
| 0x24  | 4      | Main data block count                                |
| 0x28  | 8      | Journal block count                                  |
| 0x200 |        | End                                                  |
|       |        |                                                      |

### Save FS header

  - Structure is different than
3DS.

| Start | Length | Description                                                |
| ----- | ------ | ---------------------------------------------------------- |
| 0x00  | 4      | Magic ("SAVE")                                             |
| 0x04  | 4      | Version? (Upper 2 bytes must be 0x0006)                    |
| 0x08  | 8      | Number of blocks. Does not change if save file is resized. |
| 0x10  | 8      | Block Size                                                 |
|       |        | The below fields are treated as a separate subheader       |
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

### Remap storage header

| Start | Length | Description                                                      |
| ----- | ------ | ---------------------------------------------------------------- |
| 0x00  | 4      | Magic ("RMAP")                                                   |
| 0x04  | 4      | Version? (Must be 0x10000 or less)                               |
| 0x08  | 4      | Number of remapping entries                                      |
| 0x0C  | 4      | Number of remapping segments                                     |
| 0x10  | 4      | Number of bits reserved for the segment index in virtual offsets |
| 0x40  |        | End                                                              |

### Extra data

| Start | Length | Description                                                                   |
| ----- | ------ | ----------------------------------------------------------------------------- |
| 0x00  | 0x40   | [Save Struct](Filesystem%20services#Save%20Struct.md##Save_Struct "wikilink") |
| 0x40  | 8      | Save owner ID                                                                 |
| 0x48  | 8      | Timestamp                                                                     |
| 0x50  | 4      | Flags?                                                                        |
| 0x54  | 4      | Unused?                                                                       |
| 0x58  | 8      | Size of usable save data                                                      |
| 0x60  | 8      | Journal size                                                                  |
| 0x68  | 8      | Commit ID                                                                     |
| 0x200 |        | End                                                                           |

## Remap Storage

Remap Storage is used to remap segments of data from virtual offsets to
physical offsets. This allows extending the save file without having to
relocate existing data.

Each Remap Storage has three components: [a
header](#Remap_storage_header "wikilink"), a remapping table, and the
main data storage.

A remap storage can contain a varying number of segments, each
representing a chunk of contiguous virtual storage. A segment can be
composed of one or more entries. Each of these entries are mapped from
their virtual locations to their physical locations by entries in the
remapping table. A physical offset corresponds to that offset in the
main data storage.

When a segment is extended a new remapping entry is appended to the
physical storage, allowing expansion without relocating the existing
entries.

Each virtual offset has two parts, a segment index and an offset. The
size of these sections is controlled by the remap header.

Example: 0x3000000000000100  
If 4 bits were reserved for the segment index, the offset would be split
like this, representing offset 0x100 of segment 3.  
Segment index: 0x3 Offset: 0x000000000000100

### Remapping Entry

| Start | Length | Description     |
| ----- | ------ | --------------- |
| 0x00  | 8      | Virtual offset  |
| 0x08  | 8      | Physical offset |
| 0x10  | 8      | Size            |
| 0x18  | 4      | Alignment       |
| 0x1c  | 4      | Padding?        |
|       |        |                 |

## Duplex Storage

A Duplex Storage contains four separate elements: [a
header](#Duplex_header "wikilink"), a bitmap, and two identically-sized
chunks of data.

As hinted by the name, a Duplex Storage contains two main chunks of
data. To store X bytes, two chunks of data each with size X are
required.

### Bitmap

This main data storage is split into blocks of the size indicated in the
duplex header. The bitmap contains as many bits as the main data has
blocks. If the main data is 0x40000 bytes long with a block size of
0x4000 bytes, the bitmap would contain 0x10 bits.

The bitmap controls which data chunk is active for each block. e.g. If
bit 3 of the bitmap is a 0 then block 3 of data chunk 0 is active and
block 3 of data chunk 1 is inactive. This means that when data from
block 3 is read, the data from chunk 0 will be returned and the data
from chunk 1 will be completely ignored.

### Hierarchical Duplex Storage

Multiple Duplex Storages can be chained together to gain various
benefits. With a Hierarchical Duplex Storage, the bitmap for the main
data is stored inside another Duplex Storage.

The bitmap for this second Duplex Storage is stored in a special Duplex
Storage. The data of this top level contains a master bitmap that is
typically 0x40 bytes long. A bit in the save file header controls which
master bitmap is active.

This allows for atomic operations on the Hierarchical Duplex Storage.
When writing to the storage, data will be written to the inactive blocks
and inactive bitmaps. When the data is committed the bit in the save
file header is flipped, changing which master bitmap is active.

## Files

### Directory Table Entry

  - Index 0 is the start of a linked list that contains all
    invalid/inactive directories.
  - Index 1 is the start of a linked list that contains all valid/active
    directories.
  - Index 2 is the root
directory.

| Start | Length | Description                                                                                                                                                                            |
| ----- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x00  | 4      | Parent directory node index                                                                                                                                                            |
| 0x04  | 64     | Filename                                                                                                                                                                               |
| 0x44  | 4      | Next sibling directory node index                                                                                                                                                      |
| 0x48  | 4      | First child directory node index                                                                                                                                                       |
| 0x4c  | 8      | First child file node index                                                                                                                                                            |
| 0x54  | 8      | Unused?                                                                                                                                                                                |
| 0x5c  | 4      | Next directory node index in the chain of invalid or valid directories. If this is the first block in a list of length 0, this value will contain the total number of directory nodes. |
|       |        |                                                                                                                                                                                        |

### File Table Entry

  - Index 0 is the start of a linked list that contains all
    invalid/inactive files.
  - Index 1 is the start of a linked list that contains all valid/active
    files.

| Start | Length | Description                                                                                                                                                            |
| ----- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x00  | 4      | Parent directory node index                                                                                                                                            |
| 0x04  | 64     | Filename                                                                                                                                                               |
| 0x44  | 4      | Next sibling file node index                                                                                                                                           |
| 0x48  | 4      | Index of the block that the file starts at                                                                                                                             |
| 0x4c  | 8      | File size in bytes                                                                                                                                                     |
| 0x54  | 8      | Unused?                                                                                                                                                                |
| 0x5c  | 4      | Next file node index in the chain of invalid or valid files. If this is the first block in a list of length 0, this value will contain the total number of file nodes. |
|       |        |                                                                                                                                                                        |

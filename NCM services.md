# ncm

| Cmd | Name                           | Notes                |
| --- | ------------------------------ | -------------------- |
| 0   |                                | Takes a u8 as input. |
| 1   |                                | Takes a u8 as input. |
| 2   |                                | Takes a u8 as input. |
| 3   |                                | Takes a u8 as input. |
| 4   | GetContentStorage              |                      |
| 5   | GetContentMetaDatabase         |                      |
| 8   |                                | Takes a u8 as input. |
| 9   | InitializeStorageForMediaId    |                      |
| 10  | UninitializeStorageForMediaId  |                      |
| 11  | InitializeDatabaseForMediaId   |                      |
| 12  | UninitializeDatabaseForMediaId |                      |

## IContentStorage

| Cmd | Name                                                   | Notes                                                            |
| --- | ------------------------------------------------------ | ---------------------------------------------------------------- |
| 0   | [\#GetRootEntry](#GetRootEntry "wikilink")             |                                                                  |
| 1   |                                                        | Takes two 0x10-sized entries, and a u64.                         |
| 2   |                                                        | Takes a 0x10-sized entry.                                        |
| 3   |                                                        | Takes a 0x10-sized entry, returns a bool/u8.                     |
| 4   |                                                        | Takes a 0x10-sized entry, a u64, and type-5 array.               |
| 5   |                                                        | Takes two 0x10-sized entries.                                    |
| 6   | DeleteContent?                                         | Takes a 0x10-sized entry.                                        |
| 7   |                                                        | Takes a 0x10-sized entry, returns a bool/u8.                     |
| 8   |                                                        | Takes a type-0x1A string and a 0x10-sized entry.                 |
| 9   |                                                        | Takes a type-0x1A string and a 0x10-sized entry.                 |
| 10  |                                                        | Void.                                                            |
| 11  |                                                        | Takes a type-6 buffer, each entry 0x10 bytes, and returns a u32. |
| 12  | [\#GetNumberOfEntries](#GetNumberOfEntries "wikilink") |                                                                  |
| 13  | [\#GetEntries](#GetEntries "wikilink")                 |                                                                  |
| 14  | GetEntrySize                                           |                                                                  |
| 15  |                                                        | Void.                                                            |
| 16  |                                                        | Takes three 0x10-sized entries.                                  |
| 17  |                                                        | Takes a 0x10-sized entry and a u64.                              |
| 18  | [\#ReadEntryRaw](#ReadEntryRaw "wikilink")             |                                                                  |
| 19  |                                                        | Takes a 0x10-sized entry and returns another 0x10-sized entry.   |
| 20  |                                                        | Takes a 0x10-sized entry and returns another 0x10-sized entry.   |
| 21  |                                                        | Takes a 0x10-sized entry, a u64, and a type5 buffer.             |
| 22  | GetFreeSpace                                           |                                                                  |
| 23  | GetTotalSpace                                          |                                                                  |

## GetRootEntry

Returns an entry of 16 completely random-looking bytes. Changes on
reboot?

## GetEntries

Takes a u32 offset and gets all entries starting at that offset. Returns
number of entries read.

Each entry is 16 completely random-looking bytes.

## ReadEntryRaw

Takes an output buffer, a 16-byte entry as input, and a u64 file offset.

Returns encrypted looking
data.

## IContentMetaDatabase

| Cmd | Name                | Notes                                                                                           |
| --- | ------------------- | ----------------------------------------------------------------------------------------------- |
| 0   | InsertContentEntry? | Takes a 0x10-sized entry, a type-5 buffer and a u64.                                            |
| 1   |                     | Takes a 0x10-sized entry, a type-6 buffer and a u64. Returns a u64.                             |
| 2   |                     | Takes a 0x10-sized entry.                                                                       |
| 3   |                     | Takes a 0x10-sized entry and a bool/u8. Returns an 0x10-sized entry.                            |
| 4   |                     | Takes a type-6 buffer, each entry being 24 bytes, 0x10-sized entry and a u32. Returns a u32.    |
| 5   | Iterate             | Takes a type-6 buffer, each entry being 16 bytes, a 0x10-sized entry, and a u32. Returns a u32. |
| 6   |                     | Takes a u64. Returns a 0x10-sized entry.                                                        |
| 7   |                     |                                                                                                 |
| 8   |                     |                                                                                                 |
| 9   |                     |                                                                                                 |
| 10  |                     |                                                                                                 |
| 11  |                     |                                                                                                 |
| 12  |                     |                                                                                                 |
| 13  |                     |                                                                                                 |
| 14  |                     |                                                                                                 |
| 15  | EndIteration        |                                                                                                 |
| 16  |                     |                                                                                                 |
| 17  |                     |                                                                                                 |
| 18  |                     |                                                                                                 |
| 19  |                     |                                                                                                 |

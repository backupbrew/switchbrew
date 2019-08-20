The Switch uses the NRR file format to verify [NRO](NRO.md "wikilink")
at load time. These files contain hashes of each NRO that is allowed to
be loaded by the program. An NRO's SHA-256 hash must match any of the
hashes in the hash table. NRRs are signed with RSASSA-PSS-2048/SHA-256.

| Offset | Size               | Description                                                               |
| ------ | ------------------ | ------------------------------------------------------------------------- |
| 0x0    | 0x4                | Magic "NRR0"                                                              |
| 0x4    | 0xC                | Reserved                                                                  |
| 0x10   | 0x8                | Title ID Mask                                                             |
| 0x18   | 0x8                | Title ID Pattern                                                          |
| 0x20   | 0x10               | Reserved                                                                  |
| 0x30   | 0x100              | Modulus for verifying the second signature                                |
| 0x130  | 0x100              | First signature signed by a Nintendo key, over the above contents         |
| 0x230  | 0x100              | Second signature verifiable with the above key, over the rest of the file |
| 0x330  | 0x8                | Title ID                                                                  |
| 0x338  | 0x4                | File Size                                                                 |
| 0x33C  | 0x4                | Module Type                                                               |
| 0x340  | 0x4                | Hash Offset (Always 0x350)                                                |
| 0x344  | 0x4                | Hash Count                                                                |
| 0x348  | 0x8                | Reserved                                                                  |
| 0x350  | 0x20 \* Hash Count | NRO hashes (SHA-256)                                                      |

[Category:File formats](Category:File_formats "wikilink")

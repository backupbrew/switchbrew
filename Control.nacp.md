Roughly equivalent to non-gfx areas of 3DS SMDH. All strings for
language-entries are UTF-8, unlike SMDH which uses UTF-16.

Total size is
0x4000-bytes.

# Structure

| Offset | Size            | Description                                                                                            |
| ------ | --------------- | ------------------------------------------------------------------------------------------------------ |
| 0x0    | 0x2400          | Language entries                                                                                       |
| 0x2400 | 0xC00           | Normally all-zero? Maybe more language entries?                                                        |
| 0x3000 | 0x24            | Zeros?                                                                                                 |
| 0x3024 | 0x4             | ?                                                                                                      |
| 0x3028 | 0x4             | ?                                                                                                      |
| 0x302C | 0x4             | ?                                                                                                      |
| 0x3030 | 0x4             | ?                                                                                                      |
| 0x3034 | 0x4             | ?                                                                                                      |
| 0x3038 | 0x8             | Application titleID                                                                                    |
| 0x3040 | 0x20            | ?                                                                                                      |
| 0x3060 | 0x10            | Application version string, encoding unknown.                                                          |
| 0x3070 | 0x8             | Base titleID for DLC, set even when DLC is not used. Usually app\_titleID+0x1000?                      |
| 0x3078 | 0x8             | Application titleID                                                                                    |
| 0x3080 | 0x4             | ?                                                                                                      |
| 0x3084 | 0x4             | ?                                                                                                      |
| 0x3088 | 0x4             | ?                                                                                                      |
| 0x308C | 0x24            | Zeros?                                                                                                 |
| 0x30B0 | 0x8             | Application titleID                                                                                    |
| 0x30B8 | 0x38 (0x8\*0x7) | Array of application titleIDs, normally the same as the above app-titleIDs. Only set for game-updates? |
| 0x30F0 | 0x4             | ?                                                                                                      |
| 0x30F4 | 0x4             | ?                                                                                                      |
| 0x30F8 | 0x8             | Application titleID. Only set for game-updates?                                                        |
| 0x3100 | 0x40            | [BCAT](BCAT%20Content%20Container.md "wikilink") passphrase, all-zero when unused.                     |
| 0x3140 | 0xEC0           | Normally all-zero?                                                                                     |

## Language Entry

Total size is 0x300-bytes.

| Offset | Size  | Description                  |
| ------ | ----- | ---------------------------- |
| 0x0    | 0x200 | Application name string      |
| 0x200  | 0x100 | Application developer string |

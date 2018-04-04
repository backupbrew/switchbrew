Roughly equivalent to non-gfx areas of 3DS SMDH. All strings for
language-entries are UTF-8, unlike SMDH which uses UTF-16.

Total size is
0x4000-bytes.

# Structure

| Offset | Size               | Description                                                                                            |
| ------ | ------------------ | ------------------------------------------------------------------------------------------------------ |
| 0x0    | 0x2D00 (0x300\*15) | Language entries                                                                                       |
| 0x2D00 | 0x300              | Normally all-zero?                                                                                     |
| 0x3000 | 0x24               | Zeros?                                                                                                 |
| 0x3024 | 0x4                | ?                                                                                                      |
| 0x3028 | 0x4                | ?                                                                                                      |
| 0x302C | 0x4                | ?                                                                                                      |
| 0x3030 | 0x4                | ?                                                                                                      |
| 0x3034 | 0x4                | ?                                                                                                      |
| 0x3038 | 0x8                | Application titleID                                                                                    |
| 0x3040 | 0x20               | ?                                                                                                      |
| 0x3060 | 0x10               | Application version string, encoding unknown.                                                          |
| 0x3070 | 0x8                | Base titleID for DLC, set even when DLC is not used. Usually app\_titleID+0x1000?                      |
| 0x3078 | 0x8                | Application titleID                                                                                    |
| 0x3080 | 0x4                | ?                                                                                                      |
| 0x3084 | 0x4                | ?                                                                                                      |
| 0x3088 | 0x4                | ?                                                                                                      |
| 0x308C | 0x1C               | Zeros?                                                                                                 |
| 0x30A8 | 0x8                | Product Code (this field is sometimes zeroes, unknown why)                                             |
| 0x30B0 | 0x8                | Application titleID                                                                                    |
| 0x30B8 | 0x38 (0x8\*0x7)    | Array of application titleIDs, normally the same as the above app-titleIDs. Only set for game-updates? |
| 0x30F0 | 0x4                | ?                                                                                                      |
| 0x30F4 | 0x4                | ?                                                                                                      |
| 0x30F8 | 0x8                | Application titleID. Only set for game-updates?                                                        |
| 0x3100 | 0x40               | [BCAT](BCAT%20Content%20Container.md "wikilink") passphrase, all-zero when unused.                     |
| 0x3140 | 0xEC0              | Normally all-zero?                                                                                     |

## Language Entry

Total size is 0x300-bytes.

| Offset | Size  | Description                  |
| ------ | ----- | ---------------------------- |
| 0x0    | 0x200 | Application name string      |
| 0x200  | 0x100 | Application developer string |

Entry index for each
[language](Settings%20services#LanguageCode.md##LanguageCode "wikilink"):

| Entry-index | Icon [language](NCA%20Content%20FS#FS-type3.md##FS-type3 "wikilink") filename |
| ----------- | ----------------------------------------------------------------------------- |
| 0           | "AmericanEnglish"                                                             |
| 1           | "BritishEnglish"                                                              |
| 2           | "Japanese"                                                                    |
| 3           | "French"                                                                      |
| 4           | "German"                                                                      |
| 5           | "LatinAmericanSpanish"                                                        |
| 6           | "Spanish"                                                                     |
| 7           | "Italian"                                                                     |
| 8           | "Dutch"                                                                       |
| 9           | "CanadianFrench"                                                              |
| 10          | "Portuguese"                                                                  |
| 11          | "Russian"                                                                     |
| 12          | "Korean"                                                                      |
| 13          | "Taiwanese"                                                                   |
| 14          | "Chinese"                                                                     |

Official apps tend to have the language entries' strings set to only
English. Some apps don't have certain language entries set at all. In
addition, official apps usually (?) don't have the following language
entries set: Korean, Taiwanese, and Chinese.

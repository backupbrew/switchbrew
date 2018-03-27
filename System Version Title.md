The FS for the system-version title(TID 0100000000000809) contains
"/file" (and, after [5.0.0](5.0.0.md "wikilink"),
"/digest"):

| Offset | Size | Description                                                                                                                                                                                     |
| ------ | ---- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x1  | Major                                                                                                                                                                                           |
| 0x1    | 0x1  | Minor                                                                                                                                                                                           |
| 0x2    | 0x1  | Micro                                                                                                                                                                                           |
| 0x3    | 0x1  | Unknown/Build?                                                                                                                                                                                  |
| 0x4    | 0x1  | Revision Number                                                                                                                                                                                 |
| 0x5    | 0x3  | Normally all-zero. Padding?                                                                                                                                                                     |
| 0x8    | 0x20 | Platform string ("NX" with zeros afterwards)                                                                                                                                                    |
| 0x28   | 0x40 | Hex ASCII string. 0x28-bytes(not including NUL-terminator) normally with zeros afterwards. The value of this string differs from [2.0.0](2.0.0.md "wikilink") and [2.1.0](2.1.0.md "wikilink"). |
| 0x68   | 0x18 | System-version in string form with zeros afterwards. For example: "2.1.0". This is what is displayed in System settings.                                                                        |
| 0x80   | 0x80 | ASCII string with zeros / padding afterwards. For example: "NintendoSDK Firmware for NX 2.0.0-15"                                                                                               |

## Known Versions

### Retail Firmware Updates

| Firmware | Version String                         | Hex ASCII String                         | "/digest" contents                                             |
| -------- | -------------------------------------- | ---------------------------------------- | -------------------------------------------------------------- |
| 1.0.0    | NintendoSDK Firmware for NX 1.0.0-15   | 84b8da475a02261c456e6472b403b31416480165 | N/A                                                            |
| 2.0.0    | NintendoSDK Firmware for NX 2.0.0-15   | 25233e518f580062b41f45fae7ce56bff261094a | N/A                                                            |
| 2.1.0    | NintendoSDK Firmware for NX 2.1.0-0    | e548f82b0aaff5fd18cfd80e7b9bd9808eeb7c99 | N/A                                                            |
| 2.2.0    | NintendoSDK Firmware for NX 2.2.0-1    | c83b637205048e61e73c870f21271cc3c6364396 | N/A                                                            |
| 2.3.0    | NintendoSDK Firmware for NX 2.3.0-0    | 3ed3bbc8885b6362f4f244dcecd2b430fa27310e | N/A                                                            |
| 3.0.0    | NintendoSDK Firmware for NX 3.0.0-10.0 | 7fbde2b0bba4d14107bf836e4643043d9f6c8e47 | N/A                                                            |
| 3.0.1    | NintendoSDK Firmware for NX 3.0.1-0.0  | a3363e086791370ed89dca69c697b4a8bc443d66 | N/A                                                            |
| 3.0.2    | NintendoSDK Firmware for NX 3.0.2-0.0  | 56bc7f71d0e13179ccb6543bbb33d7f537859e49 | N/A                                                            |
| 4.0.0    | NintendoSDK Firmware for NX 4.0.0-4.0  | 875be0f6edc29b23938b7aea50764421b9f217e5 | N/A                                                            |
| 4.0.1    | NintendoSDK Firmware for NX 4.0.1-0.0  | 826588c45cecab1672c46f5de87d83ea6008d583 | N/A                                                            |
| 4.1.0    | NintendoSDK Firmware for NX 4.1.0-0.0  | 314f9468b704e84e1ffed449dfa6108ba4be221d | N/A                                                            |
| 5.0.0    | NintendoSDK Firmware for NX 5.0.1-0.0  | 66790aa646927601523df36a6750205cd944b3de | gW93A\#00050000\#QRnTiv2kqQV-KO9DAn1Wzz4S2-SDH4Zd10y8Jx5KalI=  |
| 5.0.1    | NintendoSDK Firmware for NX 5.0.0-3.0  | 4b51b56242cc388ef487e148048e2c80e25994ad | gW93A\#00050001\#wBt05i54vmIPr7cs44Vvod3M9s5M2Yl2ZVd\_pd036MY= |

### Other

| Firmware | Version String                         | Hex ASCII String                         | Note                                                           |
| -------- | -------------------------------------- | ---------------------------------------- | -------------------------------------------------------------- |
| 2.0.0-2  | NintendoSDK Firmware for NX 2.0.0-2    | 665fafc03935d12eebba8060a135516b021ccbaa | Revision of [factory firmware](Factory%20Setup.md "wikilink"). |
| 2.0.0-13 | NintendoSDK Firmware for NX 2.0.0-13   | 60b5fa391b0055f50fec362d29ac18395f387412 | Revision of [factory firmware](Factory%20Setup.md "wikilink"). |
| 3.0.0    | NintendoSDK Firmware for NX 3.0.0-10.0 | 83480e96a810a6c7cd3a8fb58dfb5b53961ac781 | Revision of [factory firmware](Factory%20Setup.md "wikilink"). |
|          |                                        |                                          |                                                                |

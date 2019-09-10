The FS for the system-version title(TID 0100000000000809) contains
"/file" (and, with \[5.0.0+\], "/digest"):

| Offset | Size | Description                                                                                                                        |
| ------ | ---- | ---------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x1  | Major                                                                                                                              |
| 0x1    | 0x1  | Minor                                                                                                                              |
| 0x2    | 0x1  | Micro                                                                                                                              |
| 0x3    | 0x1  | Padding                                                                                                                            |
| 0x4    | 0x1  | Revision Major                                                                                                                     |
| 0x5    | 0x1  | Revision Minor                                                                                                                     |
| 0x6    | 0x2  | Padding                                                                                                                            |
| 0x8    | 0x20 | Platform string ("NX" with zeros afterwards)                                                                                       |
| 0x28   | 0x40 | Version hash (Hex ASCII string). 0x28-bytes(not including NUL-terminator) normally with zeros afterwards.                          |
| 0x68   | 0x18 | Display version (System-version in string form with zeros afterwards, e.g. "2.1.0"). This is what is displayed in System settings. |
| 0x80   | 0x80 | Display title (System version in longform, e.g. "NintendoSDK Firmware for NX 2.0.0-15"). This is what is displayed in DevMenu.     |

## Known Versions

### Retail Firmware Updates

| Firmware | Version String                         | Hex ASCII String                         | "/digest" contents                                              |
| -------- | -------------------------------------- | ---------------------------------------- | --------------------------------------------------------------- |
| 1.0.0    | NintendoSDK Firmware for NX 1.0.0-15   | 84b8da475a02261c456e6472b403b31416480165 | N/A                                                             |
| 2.0.0    | NintendoSDK Firmware for NX 2.0.0-15   | 25233e518f580062b41f45fae7ce56bff261094a | N/A                                                             |
| 2.1.0    | NintendoSDK Firmware for NX 2.1.0-0    | e548f82b0aaff5fd18cfd80e7b9bd9808eeb7c99 | N/A                                                             |
| 2.2.0    | NintendoSDK Firmware for NX 2.2.0-1    | c83b637205048e61e73c870f21271cc3c6364396 | N/A                                                             |
| 2.3.0    | NintendoSDK Firmware for NX 2.3.0-0    | 3ed3bbc8885b6362f4f244dcecd2b430fa27310e | N/A                                                             |
| 3.0.0    | NintendoSDK Firmware for NX 3.0.0-10.0 | 7fbde2b0bba4d14107bf836e4643043d9f6c8e47 | N/A                                                             |
| 3.0.1    | NintendoSDK Firmware for NX 3.0.1-0.0  | a3363e086791370ed89dca69c697b4a8bc443d66 | N/A                                                             |
| 3.0.2    | NintendoSDK Firmware for NX 3.0.2-0.0  | 56bc7f71d0e13179ccb6543bbb33d7f537859e49 | N/A                                                             |
| 4.0.0    | NintendoSDK Firmware for NX 4.0.0-4.0  | 875be0f6edc29b23938b7aea50764421b9f217e5 | N/A                                                             |
| 4.0.1    | NintendoSDK Firmware for NX 4.0.1-0.0  | 826588c45cecab1672c46f5de87d83ea6008d583 | N/A                                                             |
| 4.1.0    | NintendoSDK Firmware for NX 4.1.0-0.0  | 314f9468b704e84e1ffed449dfa6108ba4be221d | N/A                                                             |
| 5.0.0    | NintendoSDK Firmware for NX 5.0.0-3.0  | 66790aa646927601523df36a6750205cd944b3de | gW93A\#00050000\#QRnTiv2kqQV-KO9DAn1Wzz4S2-SDH4Zd10y8Jx5KalI=   |
| 5.0.1    | NintendoSDK Firmware for NX 5.0.1-0.0  | 4b51b56242cc388ef487e148048e2c80e25994ad | gW93A\#00050001\#wBt05i54vmIPr7cs44Vvod3M9s5M2Yl2ZVd\_pd036MY=  |
| 5.1.0    | NintendoSDK Firmware for NX 5.1.0-3.0  | 23f9df53e25709d756e0c76effcb2473bd3447dd | gW93A\#00050100\#29uVhARHOdeTZmfdPnP785egrfRbPUW5n3IAACuHoPw=   |
| 6.0.0    | NintendoSDK Firmware for NX 6.0.0-5.0  | ef435c4fcf83831d535424f6fc28e6c91f7669d1 | gW93A\#00060000\#9k9lgdev3glK0ltQTdWmdK7jU1BL9oWNJRAFkQpHUYI=   |
| 6.0.1    | NintendoSDK Firmware for NX 6.0.1-1.0  | 880a0ba230a9b9225a87abe1de6c8ab8d832551e | gW93A\#00060001\#a4EXpeev\_mWNw7Dk0vkOsCMIxlosx2JuXPiOa5hEMd0=  |
| 6.1.0    | NintendoSDK Firmware for NX 6.1.0-4.0  | 3e478da6353b192c36490f4aa34df0d10d575146 | gW93A\#00060100\#FziXCoELZt0C7o-t\_rro9xWTcKkgPrsksov-OVrL00c=  |
| 6.2.0    | NintendoSDK Firmware for NX 6.2.0-1.0  | 921f86701e69af7ac02712e24abf18a666c2b5fb | CusHY\#00060200\#-uAUBEUSc-Se5mvfhJsj3Krr9ayN7IyTX60\_XcLsZkQ=  |
| 7.0.0    | NintendoSDK Firmware for NX 7.0.0-5.0  | e4b38b15e880d251c182323894077508803abaaf | CusHY\#00070000\#5PRVTLegTfFlaOw3kznosYec9d8BxGj8pN3wqGa80so=   |
| 7.0.1    | NintendoSDK Firmware for NX 7.0.1-1.0  | b9d2547128fa22760492cf09bffd0a3e43f2132c | CusHY\#00070001\#rBuhja\_901l8V8bKFqeiNBCY-fflYlZVa\_iqvkpEGJI= |
| 8.0.0    | NintendoSDK Firmware for NX 8.0.0-4.99 | e19a1c3067a96ec3028d53564704e4fb76ef7c59 | CusHY\#00080000\#s7CpDsmxJh1kenRjC5cfTDfbrMFNHxBbzr6XvNTA5RI=   |
| 8.0.1    | NintendoSDK Firmware for NX 8.0.1-1.0  | c7b483d6d953f515b9b449489dcfd828cb50fd69 | CusHY\#00080001\#fgCfbpEweqCg1S49PsWL\_b9R-C1Vj\_hJ6aTmSRxycSQ= |
| 8.1.0    | NintendoSDK Firmware for NX 8.1.0-1.0  | 250fc5984a776bf488cdbde04acfac2cd853978f | CusHY\#00080100\#OvqIXdglAGfnEd\_VQr28t7rUtxNE6LHjMQicnQ9o7zk=  |
| 9.0.0    | NintendoSDK Firmware for NX 9.0.0-4.0  | 4de65c071fd0869695b7629f75eb97b2551dbf2f | CusHY\#00090000\#-80vwBkUjWLb5Kpb\_cnuTjBZ0rHwZHhN7R1-vg0Ti5c=  |

### Other

| Firmware  | Version String                         | Hex ASCII String                         | Note                                                           |
| --------- | -------------------------------------- | ---------------------------------------- | -------------------------------------------------------------- |
| 2.0.0-2   | NintendoSDK Firmware for NX 2.0.0-2    | 665fafc03935d12eebba8060a135516b021ccbaa | Revision of [factory firmware](Factory%20Setup.md "wikilink"). |
| 2.0.0-13  | NintendoSDK Firmware for NX 2.0.0-13   | 60b5fa391b0055f50fec362d29ac18395f387412 | Revision of [factory firmware](Factory%20Setup.md "wikilink"). |
| 3.0.0     | NintendoSDK Firmware for NX 3.0.0-10.0 | 83480e96a810a6c7cd3a8fb58dfb5b53961ac781 | Revision of [factory firmware](Factory%20Setup.md "wikilink"). |
| 6.0.0-4.0 | NintendoSDK Firmware for NX 6.0.0-4.0  | 5dc1909aea612d7a444884faca584fa8ae895b5c | Pre-release version of firmware 6.0.0.                         |

### Development Firmwares

| Firmware | Version String                      | Hex ASCII String                         | Note                  |
| -------- | ----------------------------------- | ---------------------------------------- | --------------------- |
| 0.8.5-0  | NintendoSDK Firmware for NX 0.8.5-0 | 3dd94e3e75a61a7a828756919dba98c42ed7069a | Pre-release firmware. |

\_\_NOTOC\_\_ Data sourced from 0100000000000818 archive.

# account

| Name                                       | Versions | Default Values | Description |
| ------------------------------------------ | -------- | -------------- | ----------- |
| na\_license\_verification\_enabled         | 5.0.0+   | true           |             |
| na\_required\_for\_network\_service        | 1.0.0+   | true           |             |
| user\_qualification\_verification\_enabled | 6.0.0+   | false          |             |

# account.daemon

| Name                                   | Versions         | Default Values     | Description |
| -------------------------------------- | ---------------- | ------------------ | ----------- |
| background\_awaking\_periodicity       | 2.0.0+           | 10800 (0x2a30)     |             |
| initial\_schedule\_delay               | 7.0.0+           | 60 (0x3c)          |             |
| long\_sleep\_detection\_threshold      | 7.0.0+           | 1468800 (0x166980) |             |
| na\_info\_refresh\_interval            | 2.0.0-5.0.0      | 46800 (0xb6d0)     |             |
| 5.0.1-5.1.0                            | 72000 (0x11940)  |                    |             |
| 6.0.0-7.0.1                            | 46800 (0xb6d0)   |                    |             |
| 8.0.0+                                 | 457200 (0x6f9f0) |                    |             |
| na\_verification\_url\_retry\_interval | 9.0.0+           | 18000 (0x4650)     |             |
| profile\_sync\_interval                | 2.0.0-5.0.0      | 18000 (0x4650)     |             |
| 5.0.1-5.1.0                            | 172800 (0x2a300) |                    |             |
| 6.0.0+                                 | 18000 (0x4650)   |                    |             |
| schedule\_periodicity                  | 2.0.0+           | 3600 (0xe10)       |             |

# am.debug

This class does not exist on retail firmware.

| Name                          | Versions | Default Values | Description                                                                                                                                    |
| ----------------------------- | -------- | -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| dev\_function                 |          |                | Not set on retail firmware. Enables a few IPC commands and allows OpenSystem/OverlayAppletProxy when there is already a system/overlay applet. |
| cpu\_boost\_always\_no\_boost | ?        |                | Only used when [Settings\_services\#GetDebugModeFlag](Settings%20services#GetDebugModeFlag.md##GetDebugModeFlag "wikilink") returns 1.         |

# am.display

| Name                                              | Versions    | Default Values | Description |
| ------------------------------------------------- | ----------- | -------------- | ----------- |
| force\_immediate\_update\_caller\_applet\_capture | 5.0.0+      | false          |             |
| frame\_buffer\_sharing\_level                     | 4.0.0-4.1.0 | 0 (0x0)        |             |
| 5.0.0+                                            | 2 (0x2)     |                |             |
| transition\_layer\_enabled                        | 1.0.0+      | true           |             |

# am.gpu

| Name                                 | Versions         | Default Values | Description |
| ------------------------------------ | ---------------- | -------------- | ----------- |
| gpu\_scheduling\_bg\_app\_us         | 1.0.0            | 4834 (0x12e2)  |             |
| 2.0.0+                               | 104500 (0x19834) |                |             |
| gpu\_scheduling\_bg\_la\_us          | 1.0.0+           | 0 (0x0)        |             |
| gpu\_scheduling\_bg\_sa\_us          | 1.0.0+           | 0 (0x0)        |             |
| gpu\_scheduling\_enabled             | 1.0.0+           | true           |             |
| gpu\_scheduling\_fg\_app\_us         | 1.0.0            | 16500 (0x4074) |             |
| 2.0.0+                               | 116166 (0x1c5c6) |                |             |
| gpu\_scheduling\_fg\_la\_us          | 1.0.0+           | 11666 (0x2d92) |             |
| gpu\_scheduling\_fg\_sa\_us          | 1.0.0+           | 11666 (0x2d92) |             |
| gpu\_scheduling\_frame\_time\_us     | 1.0.0            | 17000 (0x4268) |             |
| 2.0.0+                               | 116666 (0x1c7ba) |                |             |
| gpu\_scheduling\_hidden\_bg\_la\_us  | 7.0.0+           | 0 (0x0)        |             |
| gpu\_scheduling\_hidden\_fg\_la\_us  | 7.0.0+           | 5000 (0x1388)  |             |
| gpu\_scheduling\_oa\_us              | 1.0.0+           | 500 (0x1f4)    |             |
| gpu\_scheduling\_partial\_fg\_la\_us | 1.0.0+           | 2000 (0x7d0)   |             |

# apm

| Name                                    | Versions    | Default Values | Description |
| --------------------------------------- | ----------- | -------------- | ----------- |
| battery\_draining\_enabled              | 1.0.0-7.0.1 | false          |             |
| performance\_mode\_policy               | 1.0.0+      | "auto"         |             |
| sdev\_cpu\_overclock\_enabled           | 3.0.0+      | false          |             |
| sdev\_throttling\_additional\_delay\_us | 1.0.0+      | 16000 (0x3e80) |             |
| sdev\_throttling\_enabled               | 1.0.0+      | true           |             |

# audio

| Name                                               | Versions    | Default Values | Description |
| -------------------------------------------------- | ----------- | -------------- | ----------- |
| adsp\_log\_enabled                                 | 1.0.0+      | false          |             |
| audin\_log\_enabled                                | 1.0.0-5.1.0 | false          |             |
| audout\_log\_enabled                               | 1.0.0-5.1.0 | false          |             |
| audren\_log\_enabled                               | 1.0.0-5.1.0 | false          |             |
| dev\_feature\_for\_volume\_mapping\_table\_enabled | 7.0.0+      | false          |             |
| hwopus\_log\_enabled                               | 1.0.0-5.1.0 | false          |             |
| suppress\_additional\_mic\_check                   | 6.0.0+      | false          |             |
| suspend\_for\_debugger\_enabled                    | 1.0.0-3.0.2 | false          |             |
| 4.0.0+                                             | true        |                |             |
| uac\_enabled                                       | 6.0.0+      | true           |             |
| uac\_speaker\_enabled                              | 3.0.0-3.0.2 | false          |             |

# bcat

| Name                                           | Versions | Default Values | Description |
| ---------------------------------------------- | -------- | -------------- | ----------- |
| production\_mode                               | 1.0.0+   | true           |             |
| system\_save\_data\_creation\_for\_development | 8.0.0+   | false          |             |

# bgtc

| Name                       | Versions     | Default Values  | Description |
| -------------------------- | ------------ | --------------- | ----------- |
| battery\_threshold\_save   | 2.0.0-2.3.0  | 30 (0x1e)       |             |
| 3.0.0+                     | 20 (0x14)    |                 |             |
| battery\_threshold\_stop   | 2.0.0-2.3.0  | 15 (0xf)        |             |
| 3.0.0+                     | 20 (0x14)    |                 |             |
| enable\_battery\_saver     | 2.0.0+       | 1 (0x1)         |             |
| enable\_halfawake          | 3.0.0+       | 1 (0x1)         |             |
| leaving\_halfawake\_margin | 2.0.0+       | 3 (0x3)         |             |
| minimum\_interval\_normal  | 2.0.0-6.2.0  | 1800 (0x708)    |             |
| 7.0.0+                     | 1200 (0x4b0) |                 |             |
| minimum\_interval\_save    | 2.0.0+       | 86400 (0x15180) |             |

# bluetooth\_debug

| Name       | Versions | Default Values | Description |
| ---------- | -------- | -------------- | ----------- |
| skip\_boot | 1.0.0+   | false          |             |

# boot

| Name                        | Versions | Default Values | Description |
| --------------------------- | -------- | -------------- | ----------- |
| boot\_devmenuapp\_installer | 4.0.0+   | false          |             |
| force\_maintenance          | 1.0.0+   | false          |             |

# bpc

| Name               | Versions | Default Values | Description |
| ------------------ | -------- | -------------- | ----------- |
| enable\_quasi\_off | 2.0.0+   | true           |             |

# bsp0

| Name          | Versions | Default Values | Description |
| ------------- | -------- | -------------- | ----------- |
| tm\_transport | 1.0.0+   | "USB"          |             |
| usb           | 1.0.0+   | "UDS"          |             |

# btm

This class does not exist before 9.0.0.

| Name                         | Versions | Default Values       | Description |
| ---------------------------- | -------- | -------------------- | ----------- |
| auto\_pairing\_device\_name0 | 9.0.0+   | "NintendoGamepad"    |             |
| auto\_pairing\_device\_name1 | 9.0.0+   | "Joy-Con"            |             |
| auto\_pairing\_device\_name2 | 9.0.0+   | "Pro Controller"     |             |
| auto\_pairing\_device\_name3 | 9.0.0+   | "Lic Pro Controller" |             |
| auto\_pairing\_device\_name4 | 9.0.0+   | "NES Controller"     |             |
| auto\_pairing\_device\_name5 | 9.0.0+   | "HVC Controller"     |             |
| auto\_pairing\_device\_name6 | 9.0.0+   | "SNES Controller"    |             |
| auto\_pairing\_device\_name7 | 9.0.0+   | ""                   |             |
| auto\_pairing\_device\_name8 | 9.0.0+   | ""                   |             |
| auto\_pairing\_device\_name9 | 9.0.0+   | ""                   |             |

# capsrv

| Name                                              | Versions | Default Values | Description |
| ------------------------------------------------- | -------- | -------------- | ----------- |
| album\_directory\_path                            | 5.0.0+   | "d:/Album"     |             |
| enable\_album\_directory\_change                  | 5.0.0+   | false          |             |
| enable\_album\_movie\_file\_support               | 4.0.0+   | true           |             |
| enable\_album\_movie\_filehash\_verification      | 4.0.0+   | true           |             |
| enable\_album\_movie\_filesign\_verification      | 4.0.0+   | true           |             |
| enable\_album\_screenshot\_file\_support          | 4.0.0+   | true           |             |
| enable\_album\_screenshot\_filedata\_verification | 1.0.0+   | true           |             |
| screenshot\_layerstack                            | 1.0.0+   | "screenshot"   |             |

# contents\_delivery

| Name                                                 | Versions     | Default Values | Description |
| ---------------------------------------------------- | ------------ | -------------- | ----------- |
| acceptable\_application\_delivery\_protocol\_version | 5.0.0+       | 0 (0x0)        |             |
| application\_delivery\_protocol\_version             | 4.0.0+       | 1 (0x1)        |             |
| enable\_debug\_api                                   | 3.0.0+       | false          |             |
| required\_system\_version\_to\_deliver\_application  | 4.0.0+       | 0 (0x0)        |             |
| system\_delivery\_protocol\_version                  | 4.0.0+       | 1 (0x1)        |             |
| updatable\_firmware\_group\_string                   | 8.0.0-8.1.0  | "1,3,4"        |             |
| 9.0.0+                                               | "1,3,4,8,23" |                |             |

# creport

This class does not exist before 9.0.0.

| Name                | Versions | Default Values | Description |
| ------------------- | -------- | -------------- | ----------- |
| crash\_screen\_shot | 9.0.0+   | false          |             |

# dauth

| Name    | Versions | Default Values | Description |
| ------- | -------- | -------------- | ----------- |
| \_dummy | 5.0.0+   | false          |             |

# devmenu

| Name                                               | Versions    | Default Values   | Description |
| -------------------------------------------------- | ----------- | ---------------- | ----------- |
| application\_update\_requried                      | 6.0.0+      | true             |             |
| development\_mode                                  | 6.0.0+      | false            |             |
| enable\_application\_foreground\_at\_sleep\_finish | 6.0.0+      | false            |             |
| enable\_application\_update                        | 2.0.0-5.1.0 | true             |             |
| enable\_exhibition\_mode                           | 2.0.0+      | false            |             |
| enable\_resume\_all                                | 5.0.0+      | false            |             |
| user\_index\_at\_launch                            | 6.0.0+      | \-1 (0xffffffff) |             |

# eclct

| Name                  | Versions | Default Values  | Description |
| --------------------- | -------- | --------------- | ----------- |
| analytics\_override   | 1.0.0+   | false           |             |
| analytics\_pollperiod | 1.0.0+   | 86400 (0x15180) |             |

# erpt

| Name             | Versions | Default Values | Description |
| ---------------- | -------- | -------------- | ----------- |
| production\_mode | 4.0.0+   | true           |             |

# err

| Name                | Versions | Default Values | Description |
| ------------------- | -------- | -------------- | ----------- |
| applet\_auto\_close | 1.0.0+   | false          |             |

# es

| Name                                          | Versions    | Default Values   | Description |
| --------------------------------------------- | ----------- | ---------------- | ----------- |
| device\_registration\_type                    | 7.0.0-7.0.1 | "ecc"            |             |
| 8.0.0+                                        | "auto"      |                  |             |
| unnecessary\_prepurchase\_record\_margin\_sec | 9.0.0+      | 604800 (0x93a80) |             |

# eupld

| Name            | Versions | Default Values | Description |
| --------------- | -------- | -------------- | ----------- |
| upload\_enabled | 1.0.0+   | true           |             |

# fatal

| Name                            | Versions | Default Values | Description |
| ------------------------------- | -------- | -------------- | ----------- |
| quest\_reboot\_interval\_second | 4.1.0+   | 300 (0x12c)    |             |
| show\_extra\_info               | 1.0.0+   | false          |             |
| transition\_to\_fatal           | 1.0.0+   | true           |             |

# friends

| Name                   | Versions | Default Values | Description |
| ---------------------- | -------- | -------------- | ----------- |
| background\_processing | 1.0.0+   | true           |             |

# gpu\_core\_dump

| Name                                 | Versions | Default Values | Description |
| ------------------------------------ | -------- | -------------- | ----------- |
| auto\_dump                           | 1.0.0+   | false          |             |
| global\_allocator\_is\_cache\_enable | 9.0.0+   | true           |             |

# hdcp

| Name                        | Versions | Default Values | Description |
| --------------------------- | -------- | -------------- | ----------- |
| authentication\_timeout\_ms | 4.0.0+   | 12000 (0x2ee0) |             |
| stub\_emulation             | 4.0.0+   | false          |             |

# hid\_debug

| Name                                       | Versions    | Default Values | Description |
| ------------------------------------------ | ----------- | -------------- | ----------- |
| ble\_disabled                              | 5.0.0+      | false          |             |
| disabled\_features\_per\_id                | 9.0.0+      | 0 (0x0)        |             |
| dscale\_disabled                           | 6.0.0-6.0.1 | true           |             |
| 6.1.0+                                     | false       |                |             |
| emulate\_firmware\_update\_failure         | 3.0.0+      | false          |             |
| emulate\_future\_device                    | 3.0.0+      | false          |             |
| emulate\_mcu\_hardware\_error              | 3.0.0+      | false          |             |
| enables\_debugpad                          | 1.0.0+      | false          |             |
| enables\_rail                              | 9.0.0+      | true           |             |
| firmware\_update\_failure\_emulation\_mode | 3.0.0+      | 0 (0x0)        |             |
| force\_handheld                            | 6.0.0+      | false          |             |
| manages\_devices                           | 1.0.0+      | true           |             |
| manages\_touch\_ic\_i2c                    | 6.0.0+      | true           |             |

# htc

| Name                     | Versions | Default Values | Description |
| ------------------------ | -------- | -------------- | ----------- |
| disconnection\_emulation | 1.0.0+   | false          |             |

# idle

| Name                     | Versions | Default Values | Description |
| ------------------------ | -------- | -------------- | ----------- |
| dim\_level\_percent\_lcd | 1.0.0+   | 10 (0xa)       |             |
| dim\_level\_percent\_tv  | 1.0.0+   | 70 (0x46)      |             |

# jit\_debug

| Name               | Versions | Default Values | Description |
| ------------------ | -------- | -------------- | ----------- |
| enable\_jit\_debug | 1.0.0+   | false          |             |

# lbl

| Name                                         | Versions | Default Values | Description |
| -------------------------------------------- | -------- | -------------- | ----------- |
| debug\_brightness\_mapping\_1st\_coefficient | 4.0.0+   | 1000 (0x3e8)   |             |
| debug\_brightness\_mapping\_2nd\_coefficient | 4.0.0+   | 0 (0x0)        |             |
| debug\_brightness\_mapping\_3rd\_coefficient | 4.0.0+   | 20 (0x14)      |             |
| debug\_brightness\_mapping\_enabled          | 4.0.0+   | false          |             |
| force\_disable\_als                          | 3.0.0+   | false          |             |
| vr\_brightness\_transition\_frame            | 5.0.0+   | 10 (0xa)       |             |

# lm

| Name                             | Versions | Default Values | Description |
| -------------------------------- | -------- | -------------- | ----------- |
| enable\_sd\_card\_logging        | 1.0.0+   | false          |             |
| sd\_card\_log\_output\_directory | 1.0.0+   | "NxBinLogs"    |             |

# migration

| Name                                                               | Versions | Default Values | Description |
| ------------------------------------------------------------------ | -------- | -------------- | ----------- |
| ldn\_connection\_timeout\_seconds                                  | 4.0.0+   | 1800 (0x708)   |             |
| save\_data\_migration\_transfer\_accept\_message\_timeout\_seconds | 8.0.0+   | 15 (0xf)       |             |
| save\_data\_migration\_wait\_acceptance\_timeout\_seconds          | 8.0.0+   | 1800 (0x708)   |             |
| transfer\_large\_data\_timeout\_seconds                            | 4.0.0+   | 3600 (0xe10)   |             |
| transfer\_low\_speed\_timeout\_seconds                             | 4.0.0+   | 300 (0x12c)    |             |
| transfer\_messaging\_timeout\_seconds                              | 4.0.0+   | 100 (0x64)     |             |
| transfer\_small\_data\_timeout\_seconds                            | 4.0.0+   | 300 (0x12c)    |             |
| ui\_acceptance\_wait\_timeout\_seconds                             | 4.0.0+   | 900 (0x384)    |             |

# mii

| Name                             | Versions | Default Values | Description |
| -------------------------------- | -------- | -------------- | ----------- |
| is\_db\_test\_mode\_enabled      | 1.0.0+   | false          |             |
| is\_img\_db\_test\_mode\_enabled | 5.0.0+   | false          |             |

# nd

| Name                           | Versions    | Default Values | Description |
| ------------------------------ | ----------- | -------------- | ----------- |
| development\_function\_enabled | 5.0.0-5.1.0 | false          |             |

# news

| Name            | Versions    | Default Values | Description |
| --------------- | ----------- | -------------- | ----------- |
| system\_version | 2.0.0-2.3.0 | 1 (0x1)        |             |
| 3.0.0-3.0.2     | 2 (0x2)     |                |             |
| 4.0.0-4.1.0     | 3 (0x3)     |                |             |
| 5.0.0-5.1.0     | 4 (0x4)     |                |             |
| 6.0.0-7.0.1     | 5 (0x5)     |                |             |
| 8.0.0+          | 6 (0x6)     |                |             |

# nfc

This class does not exist before 9.0.0.

| Name                           | Versions | Default Values | Description |
| ------------------------------ | -------- | -------------- | ----------- |
| millau\_h\_compatibility\_wait | 9.0.0+   | true           |             |

# nfp

| Name             | Versions | Default Values | Description |
| ---------------- | -------- | -------------- | ----------- |
| not\_locked\_tag | 2.0.0+   | true           |             |
| play\_report     | 2.0.0+   | false          |             |

# ngc.t

This class does not exist before 9.0.0.

| Name                             | Versions | Default Values | Description |
| -------------------------------- | -------- | -------------- | ----------- |
| auto\_reload\_enabled            | 9.0.0+   | true           |             |
| functionality\_override\_enabled | 9.0.0+   | false          |             |

# nifm

| Name                                           | Versions | Default Values | Description |
| ---------------------------------------------- | -------- | -------------- | ----------- |
| apply\_config\_timeout                         | 3.0.0+   | 30000 (0x7530) |             |
| connection\_test\_timeout                      | 3.0.0+   | 45000 (0xafc8) |             |
| ethernet\_adapter\_standby\_time               | 3.0.0+   | 10000 (0x2710) |             |
| is\_communication\_control\_enabled\_for\_test | 1.0.0+   | false          |             |

# nim.install

| Name                                        | Versions | Default Values | Description |
| ------------------------------------------- | -------- | -------------- | ----------- |
| apply\_delta\_stress\_storage               | 3.0.0+   | 0 (0x0)        |             |
| debug\_come\_back\_after                    | 6.0.0+   | false          |             |
| debug\_come\_back\_after\_second            | 6.0.0+   | 300 (0x12c)    |             |
| edge\_token\_expiration\_margin\_seconds    | 9.0.0+   | 600 (0x258)    |             |
| prefer\_delta\_evenif\_inefficient          | 2.0.0+   | false          |             |
| simulate\_eci\_delay\_response              | 4.0.0+   | false          |             |
| simulate\_eci\_still\_unavailable\_response | 4.0.0+   | false          |             |
| system\_update\_task\_meta\_version         | 9.0.0+   | 1 (0x1)        |             |

# notification.presenter

This class does not exist before 9.0.0.

| Name                                           | Versions | Default Values | Description |
| ---------------------------------------------- | -------- | -------------- | ----------- |
| alarm\_pattern\_total\_repeat\_count           | 9.0.0+   | 15 (0xf)       |             |
| alarm\_pattern\_with\_vibration\_repeat\_count | 9.0.0+   | 5 (0x5)        |             |
| connection\_retry\_count                       | 9.0.0+   | 5 (0x5)        |             |
| connection\_timeout\_in\_milliseconds          | 9.0.0+   | 4000 (0xfa0)   |             |
| debug\_presentation\_delay\_seconds            | 9.0.0+   | 5 (0x5)        |             |
| is\_debug\_presentation\_enabled               | 9.0.0+   | false          |             |
| notification\_led\_timeout\_in\_seconds        | 9.0.0+   | 60 (0x3c)      |             |
| snooze\_count                                  | 9.0.0+   | 2 (0x2)        |             |
| snooze\_interval\_in\_seconds                  | 9.0.0+   | 300 (0x12c)    |             |

# npns

| Name                       | Versions | Default Values | Description |
| -------------------------- | -------- | -------------- | ----------- |
| background\_processing     | 1.0.0+   | true           |             |
| logmanager\_redirection    | 1.0.0    | "false;"       |             |
| 2.0.0+                     | true     |                |             |
| sleep\_max\_try\_count     | 3.0.0+   | 5 (0x5)        |             |
| sleep\_periodic\_interval  | 2.0.0+   | 10800 (0x2a30) |             |
| sleep\_processing\_timeout | 2.0.0+   | 30 (0x1e)      |             |
| test\_mode                 | 3.0.0+   | false          |             |

# ns.applet

| Name                | Versions | Default Values       | Description                                              |
| ------------------- | -------- | -------------------- | -------------------------------------------------------- |
| overlay\_applet\_id | 1.0.0+   | "0x010000000000100c" |                                                          |
| shop\_applet\_id    | 3.0.0+   | "0x010000000000100b" |                                                          |
| system\_applet\_id  | 1.0.0+   | "0x0100000000001000" |                                                          |
| devmenu\_id         |          |                      | Only exists on devunits, titleID for DevMenu.            |
| devoverlaydisp\_id  |          |                      | Only exists on devunits, titleID for dev Overlay-applet. |

# ns.application

| Name                                                          | Versions | Default Values       | Description |
| ------------------------------------------------------------- | -------- | -------------------- | ----------- |
| application\_id\_on\_blacklist                                | 5.0.0+   | "0x0000000000000000" |             |
| application\_license\_flags\_for\_debug                       | 8.0.0+   | 0 (0x0)              |             |
| application\_version\_on\_blacklist                           | 5.0.0+   | 0 (0x0)              |             |
| assign\_all\_device\_linked\_elicenses                        | 6.0.0+   | true                 |             |
| cleanup\_add\_on\_content\_with\_no\_rights\_result\_value    | 4.0.0+   | 0 (0x0)              |             |
| cleanup\_cache\_storage\_enabled                              | 5.0.0+   | true                 |             |
| debug\_account\_restricted\_rights                            | 6.0.0+   | false                |             |
| initial\_waiting\_time\_of\_assigning\_elicenses\_for\_device | 6.0.0+   | 900 (0x384)          |             |
| max\_waiting\_time\_of\_assigning\_elicenses\_for\_device     | 6.0.0+   | 90000 (0x15f90)      |             |
| preomia\_application\_id                                      | 9.0.0+   | "0x010070000E3C0000" |             |
| redirected\_rom\_storage\_id\_for\_debug                      | 7.0.0+   | 0 (0x0)              |             |
| wait\_time\_after\_signal\_for\_dynamic\_rights\_observer     | 6.0.0+   | 15 (0xf)             |             |

# ns.autoboot

| Name    | Versions | Default Values | Description |
| ------- | -------- | -------------- | ----------- |
| enabled | 3.0.0+   | true           |             |

# ns.gamecard

| Name                                 | Versions | Default Values | Description |
| ------------------------------------ | -------- | -------------- | ----------- |
| check\_erase\_history\_flag          | 9.0.0+   | true           |             |
| mount\_gamecard\_result\_value       | 3.0.0+   | 0 (0x0)        |             |
| try\_gamecard\_access\_result\_value | 3.0.0+   | 0 (0x0)        |             |

# ns.notification

| Name                                                  | Versions    | Default Values | Description |
| ----------------------------------------------------- | ----------- | -------------- | ----------- |
| debug\_auto\_update\_waiting\_limit                   | 9.0.0+      | 0 (0x0)        |             |
| debug\_system\_update\_waiting\_limit                 | 9.0.0+      | 0 (0x0)        |             |
| debug\_version\_list\_waiting\_limit                  | 9.0.0+      | 0 (0x0)        |             |
| debug\_waiting\_limit                                 | 3.0.0-8.1.0 | 0 (0x0)        |             |
| enable\_download\_task\_list                          | 2.0.0+      | true           |             |
| enable\_download\_ticket                              | 4.0.0+      | true           |             |
| enable\_network\_update                               | 2.0.0+      | true           |             |
| enable\_random\_wait                                  | 3.0.0+      | true           |             |
| enable\_request\_on\_cold\_boot                       | 3.0.0+      | true           |             |
| enable\_send\_rights\_usage\_status\_request          | 6.0.0+      | true           |             |
| enable\_sync\_elicense\_request                       | 6.0.0+      | true           |             |
| enable\_version\_list                                 | 2.0.0+      | true           |             |
| result\_value\_to\_register\_nt\_for\_dynamic\_rights | 6.0.0-8.1.0 | 0 (0x0)        |             |
| retry\_interval                                       | 2.0.0-4.1.0 | 60 (0x3c)      |             |
| retry\_interval\_max                                  | 5.0.0+      | 900 (0x384)    |             |
| retry\_interval\_min                                  | 5.0.0+      | 60 (0x3c)      |             |
| version\_list\_waiting\_limit                         | 4.0.0-5.1.0 | 900 (0x384)    |             |
| version\_list\_waiting\_limit\_bias                   | 6.0.0+      | 48 (0x30)      |             |
| version\_list\_waiting\_limit\_min                    | 6.0.0+      | 1800 (0x708)   |             |

# ns.promotion

| Name                                        | Versions | Default Values | Description |
| ------------------------------------------- | -------- | -------------- | ----------- |
| enable\_update\_promotion\_info\_from\_bcat | 8.0.0+   | true           |             |

# ns.pseudodeviceid

| Name                      | Versions | Default Values | Description |
| ------------------------- | -------- | -------------- | ----------- |
| reset\_pseudo\_device\_id | 3.0.0+   | false          |             |

# ns.sdcard

| Name                           | Versions | Default Values | Description |
| ------------------------------ | -------- | -------------- | ----------- |
| cleanup\_sdcard\_result\_value | 5.0.0+   | 0 (0x0)        |             |
| compare\_sdcard                | 3.0.0+   | 0 (0x0)        |             |
| mount\_sdcard                  | 2.0.0+   | true           |             |

# ns.ticket

| Name                                         | Versions | Default Values | Description |
| -------------------------------------------- | -------- | -------------- | ----------- |
| next\_available\_time\_of\_unexpected\_error | 4.0.0+   | 300 (0x12c)    |             |

# ns.systemupdate

The default fields for this class only exist in the PlatformConfig\*
titles.

| Name                              | Versions | Default Values | Description |
| --------------------------------- | -------- | -------------- | ----------- |
| firmware\_variation               | ?        |                |             |
| t\_firmware\_variation            | ?        |                |             |
| updatable\_firmware\_group\_id    | ?        |                |             |
| t\_updatable\_firmware\_group\_id | ?        |                |             |

# nsd

| Name                    | Versions | Default Values | Description |
| ----------------------- | -------- | -------------- | ----------- |
| environment\_identifier | 1.0.0+   | "lp1"          |             |
| test\_mode              | 2.0.0+   | false          |             |

# ntc

| Name                                                          | Versions         | Default Values   | Description |
| ------------------------------------------------------------- | ---------------- | ---------------- | ----------- |
| autonomic\_correction\_failed\_retry\_interval\_seconds       | 1.0.0-2.3.0      | 3600 (0xe10)     |             |
| 3.0.0+                                                        | 1800 (0x708)     |                  |             |
| autonomic\_correction\_immediate\_try\_count\_max             | 1.0.0+           | 4 (0x4)          |             |
| autonomic\_correction\_immediate\_try\_interval\_milliseconds | 1.0.0+           | 5000 (0x1388)    |             |
| autonomic\_correction\_interval\_seconds                      | 1.0.0-2.1.0      | 864000 (0xd2f00) |             |
| 2.2.0+                                                        | 432000 (0x69780) |                  |             |
| is\_autonomic\_correction\_enabled                            | 1.0.0+           | true             |             |

# nv

| Name                                         | Versions    | Default Values | Description |
| -------------------------------------------- | ----------- | -------------- | ----------- |
| 00008600                                     | 1.0.0+      | ""             |             |
| 0007b25e                                     | 1.0.0+      | ""             |             |
| 0083e1                                       | 1.0.0+      | ""             |             |
| 01621887                                     | 1.0.0+      | ""             |             |
| 03134743                                     | 1.0.0+      | ""             |             |
| 0356afd0                                     | 1.0.0+      | ""             |             |
| 0356afd1                                     | 1.0.0+      | ""             |             |
| 0356afd2                                     | 1.0.0+      | ""             |             |
| 0356afd3                                     | 1.0.0+      | ""             |             |
| 094313                                       | 1.0.0+      | ""             |             |
| 0x04dc09                                     | 1.0.0+      | ""             |             |
| 0x111133                                     | 1.0.0+      | ""             |             |
| 0x1aa483                                     | 1.0.0+      | ""             |             |
| 0x1cb1cf                                     | 1.0.0+      | ""             |             |
| 0x1cb1d0                                     | 1.0.0+      | ""             |             |
| 0x1e3221                                     | 1.0.0+      | ""             |             |
| 0x300fc8                                     | 1.0.0+      | ""             |             |
| 0x301fc8                                     | 1.0.0+      | ""             |             |
| 0x302fc8                                     | 1.0.0+      | ""             |             |
| 0x3eec59                                     | 1.0.0+      | ""             |             |
| 0x46b3ed                                     | 1.0.0+      | ""             |             |
| 0x523dc0                                     | 1.0.0+      | ""             |             |
| 0x523dc1                                     | 1.0.0+      | ""             |             |
| 0x523dc2                                     | 1.0.0+      | ""             |             |
| 0x523dc3                                     | 1.0.0+      | ""             |             |
| 0x523dc4                                     | 1.0.0+      | ""             |             |
| 0x523dc5                                     | 1.0.0+      | ""             |             |
| 0x523dc6                                     | 1.0.0+      | ""             |             |
| 0x523dd0                                     | 1.0.0+      | ""             |             |
| 0x523dd1                                     | 1.0.0+      | ""             |             |
| 0x523dd3                                     | 1.0.0+      | ""             |             |
| 0x5344bb                                     | 1.0.0+      | ""             |             |
| 0x555237                                     | 1.0.0+      | ""             |             |
| 0x58a234                                     | 1.0.0+      | ""             |             |
| 0x7b4428                                     | 1.0.0+      | ""             |             |
| 0x923dc0                                     | 1.0.0+      | ""             |             |
| 0x923dc1                                     | 1.0.0+      | ""             |             |
| 0x923dc2                                     | 1.0.0+      | ""             |             |
| 0x923dc3                                     | 1.0.0+      | ""             |             |
| 0x923dc4                                     | 1.0.0+      | ""             |             |
| 0x923dd3                                     | 1.0.0+      | ""             |             |
| 0x9abdc5                                     | 1.0.0+      | ""             |             |
| 0x9abdc6                                     | 1.0.0+      | ""             |             |
| 0xaaa36c                                     | 1.0.0+      | ""             |             |
| 0xb09da0                                     | 1.0.0+      | ""             |             |
| 0xb09da1                                     | 1.0.0+      | ""             |             |
| 0xb09da2                                     | 1.0.0+      | ""             |             |
| 0xb09da3                                     | 1.0.0+      | ""             |             |
| 0xb09da4                                     | 1.0.0+      | ""             |             |
| 0xb09da5                                     | 1.0.0+      | ""             |             |
| 0xb0b348                                     | 1.0.0+      | ""             |             |
| 0xb0b349                                     | 1.0.0+      | ""             |             |
| 0xbb558f                                     | 1.0.0+      | ""             |             |
| 0xbd10fb                                     | 1.0.0+      | ""             |             |
| 0xc32ad3                                     | 1.0.0+      | ""             |             |
| 0xce2348                                     | 1.0.0+      | ""             |             |
| 0xcfd81f                                     | 1.0.0+      | ""             |             |
| 0xe0036b                                     | 1.0.0+      | ""             |             |
| 0xe01f2d                                     | 1.0.0+      | ""             |             |
| 0xe17212                                     | 1.0.0+      | ""             |             |
| 0xeae966                                     | 1.0.0+      | ""             |             |
| 0xed4f82                                     | 1.0.0+      | ""             |             |
| 0xf12335                                     | 1.0.0+      | ""             |             |
| 0xf12336                                     | 1.0.0+      | ""             |             |
| 10261989                                     | 1.0.0+      | ""             |             |
| 1042d483                                     | 1.0.0+      | ""             |             |
| 10572898                                     | 1.0.0+      | ""             |             |
| 115631                                       | 1.0.0+      | ""             |             |
| 12950094                                     | 1.0.0+      | ""             |             |
| 1314f311                                     | 1.0.0+      | ""             |             |
| 1314f312                                     | 1.0.0+      | ""             |             |
| 13279512                                     | 1.0.0+      | ""             |             |
| 13813496                                     | 1.0.0+      | ""             |             |
| 14507179                                     | 1.0.0+      | ""             |             |
| 15694569                                     | 1.0.0+      | ""             |             |
| 16936964                                     | 1.0.0+      | ""             |             |
| 17aa230c                                     | 1.0.0+      | ""             |             |
| 182054                                       | 1.0.0+      | ""             |             |
| 18273275                                     | 1.0.0+      | ""             |             |
| 18273276                                     | 1.0.0+      | ""             |             |
| 1854d03b                                     | 1.0.0+      | ""             |             |
| 18add00d                                     | 1.0.0+      | ""             |             |
| 19156670                                     | 1.0.0+      | ""             |             |
| 19286545                                     | 1.0.0+      | ""             |             |
| 1a298e9f                                     | 1.0.0+      | ""             |             |
| 1acf43fe                                     | 1.0.0+      | ""             |             |
| 1bda43fe                                     | 1.0.0+      | ""             |             |
| 1c3b92                                       | 1.0.0+      | ""             |             |
| 21509920                                     | 1.0.0+      | ""             |             |
| 215323457                                    | 1.0.0+      | ""             |             |
| 2165ad                                       | 1.0.0+      | ""             |             |
| 2165ae                                       | 1.0.0+      | ""             |             |
| 21be9c                                       | 1.0.0+      | ""             |             |
| 233264316                                    | 1.0.0+      | ""             |             |
| 234557580                                    | 1.0.0+      | ""             |             |
| 23cd0e                                       | 1.0.0+      | ""             |             |
| 24189123                                     | 1.0.0+      | ""             |             |
| 2443266                                      | 1.0.0+      | ""             |             |
| 25025519                                     | 1.0.0+      | ""             |             |
| 255e39                                       | 1.0.0+      | ""             |             |
| 2583364                                      | 1.0.0+      | ""             |             |
| 2888c1                                       | 1.0.0+      | ""             |             |
| 28ca3e                                       | 1.0.0+      | ""             |             |
| 29871243                                     | 1.0.0+      | ""             |             |
| 2a1f64                                       | 1.0.0+      | ""             |             |
| 2dc432                                       | 1.0.0+      | ""             |             |
| 2de437                                       | 1.0.0+      | ""             |             |
| 2f3bb89c                                     | 1.0.0+      | ""             |             |
| 2fd652                                       | 1.0.0+      | ""             |             |
| 3001ac                                       | 1.0.0+      | ""             |             |
| 31298772                                     | 1.0.0+      | ""             |             |
| 313233                                       | 1.0.0+      | ""             |             |
| 31f7d603                                     | 1.0.0+      | ""             |             |
| 320ce4                                       | 1.0.0+      | ""             |             |
| 32153248                                     | 1.0.0+      | ""             |             |
| 32153249                                     | 1.0.0+      | ""             |             |
| 335bca                                       | 1.0.0+      | ""             |             |
| 342abb                                       | 1.0.0+      | ""             |             |
| 34dfe6                                       | 1.0.0+      | ""             |             |
| 34dfe7                                       | 1.0.0+      | ""             |             |
| 34dfe8                                       | 1.0.0+      | ""             |             |
| 34dfe9                                       | 1.0.0+      | ""             |             |
| 35201578                                     | 1.0.0+      | ""             |             |
| 359278                                       | 1.0.0+      | ""             |             |
| 37f53a                                       | 1.0.0+      | ""             |             |
| 38144972                                     | 1.0.0+      | ""             |             |
| 38542646                                     | 1.0.0+      | ""             |             |
| 3b74c9                                       | 1.0.0+      | ""             |             |
| 3c136f                                       | 1.0.0+      | ""             |             |
| 3cf72823                                     | 1.0.0+      | ""             |             |
| 3d7af029                                     | 1.0.0+      | ""             |             |
| 3ff34782                                     | 1.0.0+      | ""             |             |
| 4129618                                      | 1.0.0+      | ""             |             |
| 4189fac3                                     | 1.0.0+      | ""             |             |
| 420bd4                                       | 1.0.0+      | ""             |             |
| 42a699                                       | 1.0.0+      | ""             |             |
| 441369                                       | 1.0.0+      | ""             |             |
| 4458713e                                     | 1.0.0+      | ""             |             |
| 4554b6                                       | 1.0.0+      | ""             |             |
| 457425                                       | 1.0.0+      | ""             |             |
| 4603b207                                     | 1.0.0+      | ""             |             |
| 46574957                                     | 1.0.0+      | ""             |             |
| 46574958                                     | 1.0.0+      | ""             |             |
| 46813529                                     | 1.0.0+      | ""             |             |
| 46f1e13d                                     | 1.0.0+      | ""             |             |
| 47534c43                                     | 1.0.0+      | ""             |             |
| 48550336                                     | 1.0.0+      | ""             |             |
| 48576893                                     | 1.0.0+      | ""             |             |
| 48576894                                     | 1.0.0+      | ""             |             |
| 4889ac02                                     | 1.0.0+      | ""             |             |
| 49005740                                     | 1.0.0+      | ""             |             |
| 49867584                                     | 1.0.0+      | ""             |             |
| 49960973                                     | 1.0.0+      | ""             |             |
| 4a5341                                       | 1.0.0+      | ""             |             |
| 4f4e48                                       | 1.0.0+      | ""             |             |
| 4f8a0a                                       | 1.0.0+      | ""             |             |
| 50299698                                     | 1.0.0+      | ""             |             |
| 50299699                                     | 1.0.0+      | ""             |             |
| 50361291                                     | 1.0.0+      | ""             |             |
| 5242ae                                       | 1.0.0+      | ""             |             |
| 53d30c                                       | 1.0.0+      | ""             |             |
| 56347a                                       | 1.0.0+      | ""             |             |
| 563a95f1                                     | 1.0.0+      | ""             |             |
| 573823                                       | 1.0.0+      | ""             |             |
| 58027529                                     | 1.0.0+      | ""             |             |
| 5d2d63                                       | 1.0.0+      | ""             |             |
| 5f7e3b                                       | 1.0.0+      | ""             |             |
| 60461793                                     | 1.0.0+      | ""             |             |
| 60d355                                       | 1.0.0+      | ""             |             |
| 616627aa                                     | 1.0.0+      | ""             |             |
| 62317182                                     | 1.0.0+      | ""             |             |
| 6253fa2e                                     | 1.0.0+      | ""             |             |
| 64100768                                     | 1.0.0+      | ""             |             |
| 64100769                                     | 1.0.0+      | ""             |             |
| 64100770                                     | 1.0.0+      | ""             |             |
| 647395                                       | 1.0.0+      | ""             |             |
| 66543234                                     | 1.0.0+      | ""             |             |
| 67674763                                     | 1.0.0+      | ""             |             |
| 67739784                                     | 1.0.0+      | ""             |             |
| 68fb9c                                       | 1.0.0+      | ""             |             |
| 69801276                                     | 1.0.0+      | ""             |             |
| 6af9fa2f                                     | 1.0.0+      | ""             |             |
| 6af9fa3f                                     | 1.0.0+      | ""             |             |
| 6af9fa4f                                     | 1.0.0+      | ""             |             |
| 6bd8c7                                       | 1.0.0+      | ""             |             |
| 6c7691                                       | 1.0.0+      | ""             |             |
| 6d4296ce                                     | 1.0.0+      | ""             |             |
| 6dd7e7                                       | 1.0.0+      | ""             |             |
| 6dd7e8                                       | 1.0.0+      | ""             |             |
| 6fe11ec1                                     | 1.0.0+      | ""             |             |
| 716511763                                    | 1.0.0+      | ""             |             |
| 72504593                                     | 1.0.0+      | ""             |             |
| 73304097                                     | 1.0.0+      | ""             |             |
| 73314098                                     | 1.0.0+      | ""             |             |
| 74095213                                     | 1.0.0+      | ""             |             |
| 74095213a                                    | 1.0.0+      | ""             |             |
| 74095213b                                    | 1.0.0+      | ""             |             |
| 74095214                                     | 1.0.0+      | ""             |             |
| 748f9649                                     | 1.0.0+      | ""             |             |
| 75494732                                     | 1.0.0+      | ""             |             |
| 78452832                                     | 1.0.0+      | ""             |             |
| 784561                                       | 1.0.0+      | ""             |             |
| 78e16b9c                                     | 1.0.0+      | ""             |             |
| 79251225                                     | 1.0.0+      | ""             |             |
| 7c128b                                       | 1.0.0+      | ""             |             |
| 7ccd93                                       | 1.0.0+      | ""             |             |
| 7df8d1                                       | 1.0.0+      | ""             |             |
| 800c2310                                     | 1.0.0+      | ""             |             |
| 80546710                                     | 1.0.0+      | ""             |             |
| 80772310                                     | 1.0.0+      | ""             |             |
| 808ee280                                     | 1.0.0+      | ""             |             |
| 81131154                                     | 1.0.0+      | ""             |             |
| 81274457                                     | 1.0.0+      | ""             |             |
| 8292291f                                     | 1.0.0+      | ""             |             |
| 83498426                                     | 1.0.0+      | ""             |             |
| 84993794                                     | 1.0.0+      | ""             |             |
| 84995585                                     | 1.0.0+      | ""             |             |
| 84a0a0                                       | 1.0.0+      | ""             |             |
| 852142                                       | 1.0.0+      | ""             |             |
| 85612309                                     | 1.0.0+      | ""             |             |
| 85612310                                     | 1.0.0+      | ""             |             |
| 85612311                                     | 1.0.0+      | ""             |             |
| 85612312                                     | 1.0.0+      | ""             |             |
| 8623ff27                                     | 1.0.0+      | ""             |             |
| 87364952                                     | 1.0.0+      | ""             |             |
| 87f6275666                                   | 1.0.0+      | ""             |             |
| 886748                                       | 1.0.0+      | ""             |             |
| 89894423                                     | 1.0.0+      | ""             |             |
| 8ad8a75                                      | 1.0.0+      | ""             |             |
| 8ad8ad00                                     | 1.0.0+      | ""             |             |
| 8bb815                                       | 1.0.0+      | ""             |             |
| 8bb817                                       | 1.0.0+      | ""             |             |
| 8bb818                                       | 1.0.0+      | ""             |             |
| 8bb819                                       | 1.0.0+      | ""             |             |
| 8e640cd1                                     | 1.0.0+      | ""             |             |
| 8f34971a                                     | 1.0.0+      | ""             |             |
| 8f773984                                     | 1.0.0+      | ""             |             |
| 8f7a7d                                       | 1.0.0+      | ""             |             |
| 902486209                                    | 1.0.0+      | ""             |             |
| 90482571                                     | 1.0.0+      | ""             |             |
| 91214835                                     | 1.0.0+      | ""             |             |
| 912848290                                    | 1.0.0+      | ""             |             |
| 915e56                                       | 1.0.0+      | ""             |             |
| 92179063                                     | 1.0.0+      | ""             |             |
| 92179064                                     | 1.0.0+      | ""             |             |
| 92179065                                     | 1.0.0+      | ""             |             |
| 92179066                                     | 1.0.0+      | ""             |             |
| 92350358                                     | 1.0.0+      | ""             |             |
| 92809063                                     | 1.0.0+      | ""             |             |
| 92809064                                     | 1.0.0+      | ""             |             |
| 92809065                                     | 1.0.0+      | ""             |             |
| 92809066                                     | 1.0.0+      | ""             |             |
| 92920143                                     | 1.0.0+      | ""             |             |
| 93a89b12                                     | 1.0.0+      | ""             |             |
| 93a89c0b                                     | 1.0.0+      | ""             |             |
| 94812574                                     | 1.0.0+      | ""             |             |
| 95282304                                     | 1.0.0+      | ""             |             |
| 95394027                                     | 1.0.0+      | ""             |             |
| 959b1f                                       | 1.0.0+      | ""             |             |
| 9638af                                       | 1.0.0+      | ""             |             |
| 96fd59                                       | 1.0.0+      | ""             |             |
| 97f6275666                                   | 1.0.0+      | ""             |             |
| 97f6275667                                   | 1.0.0+      | ""             |             |
| 97f6275668                                   | 1.0.0+      | ""             |             |
| 97f6275669                                   | 1.0.0+      | ""             |             |
| 97f627566a                                   | 1.0.0+      | ""             |             |
| 97f627566b                                   | 1.0.0+      | ""             |             |
| 97f627566d                                   | 1.0.0+      | ""             |             |
| 97f627566e                                   | 1.0.0+      | ""             |             |
| 97f627566f                                   | 1.0.0+      | ""             |             |
| 97f6275670                                   | 1.0.0+      | ""             |             |
| 97f6275671                                   | 1.0.0+      | ""             |             |
| 97f727566e                                   | 1.0.0+      | ""             |             |
| 98480775                                     | 1.0.0+      | ""             |             |
| 98480776                                     | 1.0.0+      | ""             |             |
| 98480777                                     | 1.0.0+      | ""             |             |
| 992431                                       | 1.0.0+      | ""             |             |
| 9aa29065                                     | 1.0.0+      | ""             |             |
| 9af32c                                       | 1.0.0+      | ""             |             |
| 9af32d                                       | 1.0.0+      | ""             |             |
| 9af32e                                       | 1.0.0+      | ""             |             |
| 9c108b71                                     | 1.0.0+      | ""             |             |
| 9f279065                                     | 1.0.0+      | ""             |             |
| \_\_gl\_                                     | 1.0.0+      | ""             |             |
| \_\_gl\_00008600                             | 1.0.0+      | ""             |             |
| \_\_gl\_0007b25e                             | 1.0.0+      | ""             |             |
| \_\_gl\_0083e1                               | 1.0.0+      | ""             |             |
| \_\_gl\_01621887                             | 1.0.0+      | ""             |             |
| \_\_gl\_03134743                             | 1.0.0+      | ""             |             |
| \_\_gl\_0356afd0                             | 1.0.0+      | ""             |             |
| \_\_gl\_0356afd1                             | 1.0.0+      | ""             |             |
| \_\_gl\_0356afd2                             | 1.0.0+      | ""             |             |
| \_\_gl\_0356afd3                             | 1.0.0+      | ""             |             |
| \_\_gl\_094313                               | 1.0.0+      | ""             |             |
| \_\_gl\_0x04dc09                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x111133                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x1aa483                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x1cb1cf                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x1cb1d0                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x1e3221                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x300fc8                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x301fc8                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x302fc8                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x3eec59                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x46b3ed                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x523dc0                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x523dc1                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x523dc2                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x523dc3                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x523dc4                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x523dc5                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x523dc6                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x523dd0                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x523dd1                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x523dd3                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x5344bb                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x555237                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x58a234                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x7b4428                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x923dc0                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x923dc1                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x923dc2                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x923dc3                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x923dc4                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x923dd3                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x9abdc5                             | 1.0.0+      | ""             |             |
| \_\_gl\_0x9abdc6                             | 1.0.0+      | ""             |             |
| \_\_gl\_0xaaa36c                             | 1.0.0+      | ""             |             |
| \_\_gl\_0xb09da0                             | 1.0.0+      | ""             |             |
| \_\_gl\_0xb09da1                             | 1.0.0+      | ""             |             |
| \_\_gl\_0xb09da2                             | 1.0.0+      | ""             |             |
| \_\_gl\_0xb09da3                             | 1.0.0+      | ""             |             |
| \_\_gl\_0xb09da4                             | 1.0.0+      | ""             |             |
| \_\_gl\_0xb09da5                             | 1.0.0+      | ""             |             |
| \_\_gl\_0xb0b348                             | 1.0.0+      | ""             |             |
| \_\_gl\_0xb0b349                             | 1.0.0+      | ""             |             |
| \_\_gl\_0xbb558f                             | 1.0.0+      | ""             |             |
| \_\_gl\_0xbd10fb                             | 1.0.0+      | ""             |             |
| \_\_gl\_0xc32ad3                             | 1.0.0+      | ""             |             |
| \_\_gl\_0xce2348                             | 1.0.0+      | ""             |             |
| \_\_gl\_0xcfd81f                             | 1.0.0+      | ""             |             |
| \_\_gl\_0xe0036b                             | 1.0.0+      | ""             |             |
| \_\_gl\_0xe01f2d                             | 1.0.0+      | ""             |             |
| \_\_gl\_0xe17212                             | 1.0.0+      | ""             |             |
| \_\_gl\_0xeae966                             | 1.0.0+      | ""             |             |
| \_\_gl\_0xed4f82                             | 1.0.0+      | ""             |             |
| \_\_gl\_0xf12335                             | 1.0.0+      | ""             |             |
| \_\_gl\_0xf12336                             | 1.0.0+      | ""             |             |
| \_\_gl\_10261989                             | 1.0.0+      | ""             |             |
| \_\_gl\_1042d483                             | 1.0.0+      | ""             |             |
| \_\_gl\_10572898                             | 1.0.0+      | ""             |             |
| \_\_gl\_115631                               | 1.0.0+      | ""             |             |
| \_\_gl\_12950094                             | 1.0.0+      | ""             |             |
| \_\_gl\_1314f311                             | 1.0.0+      | ""             |             |
| \_\_gl\_1314f312                             | 1.0.0+      | ""             |             |
| \_\_gl\_13279512                             | 1.0.0+      | ""             |             |
| \_\_gl\_13813496                             | 1.0.0+      | ""             |             |
| \_\_gl\_14507179                             | 1.0.0+      | ""             |             |
| \_\_gl\_15694569                             | 1.0.0+      | ""             |             |
| \_\_gl\_16936964                             | 1.0.0+      | ""             |             |
| \_\_gl\_17aa230c                             | 1.0.0+      | ""             |             |
| \_\_gl\_182054                               | 1.0.0+      | ""             |             |
| \_\_gl\_18273275                             | 1.0.0+      | ""             |             |
| \_\_gl\_18273276                             | 1.0.0+      | ""             |             |
| \_\_gl\_1854d03b                             | 1.0.0+      | ""             |             |
| \_\_gl\_18add00d                             | 1.0.0+      | ""             |             |
| \_\_gl\_19156670                             | 1.0.0+      | ""             |             |
| \_\_gl\_19286545                             | 1.0.0+      | ""             |             |
| \_\_gl\_1a298e9f                             | 1.0.0+      | ""             |             |
| \_\_gl\_1acf43fe                             | 1.0.0+      | ""             |             |
| \_\_gl\_1bda43fe                             | 1.0.0+      | ""             |             |
| \_\_gl\_1c3b92                               | 1.0.0+      | ""             |             |
| \_\_gl\_21509920                             | 1.0.0+      | ""             |             |
| \_\_gl\_215323457                            | 1.0.0+      | ""             |             |
| \_\_gl\_2165ad                               | 1.0.0+      | ""             |             |
| \_\_gl\_2165ae                               | 1.0.0+      | ""             |             |
| \_\_gl\_21be9c                               | 1.0.0+      | ""             |             |
| \_\_gl\_233264316                            | 1.0.0+      | ""             |             |
| \_\_gl\_234557580                            | 1.0.0+      | ""             |             |
| \_\_gl\_23cd0e                               | 1.0.0+      | ""             |             |
| \_\_gl\_24189123                             | 1.0.0+      | ""             |             |
| \_\_gl\_2443266                              | 1.0.0+      | ""             |             |
| \_\_gl\_25025519                             | 1.0.0+      | ""             |             |
| \_\_gl\_255e39                               | 1.0.0+      | ""             |             |
| \_\_gl\_2583364                              | 1.0.0+      | ""             |             |
| \_\_gl\_2888c1                               | 1.0.0+      | ""             |             |
| \_\_gl\_28ca3e                               | 1.0.0+      | ""             |             |
| \_\_gl\_29871243                             | 1.0.0+      | ""             |             |
| \_\_gl\_2a1f64                               | 1.0.0+      | ""             |             |
| \_\_gl\_2dc432                               | 1.0.0+      | ""             |             |
| \_\_gl\_2de437                               | 1.0.0+      | ""             |             |
| \_\_gl\_2f3bb89c                             | 1.0.0+      | ""             |             |
| \_\_gl\_2fd652                               | 1.0.0+      | ""             |             |
| \_\_gl\_3001ac                               | 1.0.0+      | ""             |             |
| \_\_gl\_31298772                             | 1.0.0+      | ""             |             |
| \_\_gl\_313233                               | 1.0.0+      | ""             |             |
| \_\_gl\_31f7d603                             | 1.0.0+      | ""             |             |
| \_\_gl\_320ce4                               | 1.0.0+      | ""             |             |
| \_\_gl\_32153248                             | 1.0.0+      | ""             |             |
| \_\_gl\_32153249                             | 1.0.0+      | ""             |             |
| \_\_gl\_335bca                               | 1.0.0+      | ""             |             |
| \_\_gl\_342abb                               | 1.0.0+      | ""             |             |
| \_\_gl\_34dfe6                               | 1.0.0+      | ""             |             |
| \_\_gl\_34dfe7                               | 1.0.0+      | ""             |             |
| \_\_gl\_34dfe8                               | 1.0.0+      | ""             |             |
| \_\_gl\_34dfe9                               | 1.0.0+      | ""             |             |
| \_\_gl\_35201578                             | 1.0.0+      | ""             |             |
| \_\_gl\_359278                               | 1.0.0+      | ""             |             |
| \_\_gl\_37f53a                               | 1.0.0+      | ""             |             |
| \_\_gl\_38144972                             | 1.0.0+      | ""             |             |
| \_\_gl\_38542646                             | 1.0.0+      | ""             |             |
| \_\_gl\_3b74c9                               | 1.0.0+      | ""             |             |
| \_\_gl\_3c136f                               | 1.0.0+      | ""             |             |
| \_\_gl\_3cf72823                             | 1.0.0+      | ""             |             |
| \_\_gl\_3d7af029                             | 1.0.0+      | ""             |             |
| \_\_gl\_3ff34782                             | 1.0.0+      | ""             |             |
| \_\_gl\_4129618                              | 1.0.0+      | ""             |             |
| \_\_gl\_4189fac3                             | 1.0.0+      | ""             |             |
| \_\_gl\_420bd4                               | 1.0.0+      | ""             |             |
| \_\_gl\_42a699                               | 1.0.0+      | ""             |             |
| \_\_gl\_441369                               | 1.0.0+      | ""             |             |
| \_\_gl\_4458713e                             | 1.0.0+      | ""             |             |
| \_\_gl\_4554b6                               | 1.0.0+      | ""             |             |
| \_\_gl\_457425                               | 1.0.0+      | ""             |             |
| \_\_gl\_4603b207                             | 1.0.0+      | ""             |             |
| \_\_gl\_46574957                             | 1.0.0+      | ""             |             |
| \_\_gl\_46574958                             | 1.0.0+      | ""             |             |
| \_\_gl\_46813529                             | 1.0.0+      | ""             |             |
| \_\_gl\_46f1e13d                             | 1.0.0+      | ""             |             |
| \_\_gl\_47534c43                             | 1.0.0+      | ""             |             |
| \_\_gl\_48550336                             | 1.0.0+      | ""             |             |
| \_\_gl\_48576893                             | 1.0.0+      | ""             |             |
| \_\_gl\_48576894                             | 1.0.0+      | ""             |             |
| \_\_gl\_4889ac02                             | 1.0.0+      | ""             |             |
| \_\_gl\_49005740                             | 1.0.0+      | ""             |             |
| \_\_gl\_49867584                             | 1.0.0+      | ""             |             |
| \_\_gl\_49960973                             | 1.0.0+      | ""             |             |
| \_\_gl\_4a5341                               | 1.0.0+      | ""             |             |
| \_\_gl\_4f4e48                               | 1.0.0+      | ""             |             |
| \_\_gl\_4f8a0a                               | 1.0.0+      | ""             |             |
| \_\_gl\_50299698                             | 1.0.0+      | ""             |             |
| \_\_gl\_50299699                             | 1.0.0+      | ""             |             |
| \_\_gl\_50361291                             | 1.0.0+      | ""             |             |
| \_\_gl\_5242ae                               | 1.0.0+      | ""             |             |
| \_\_gl\_53d30c                               | 1.0.0+      | ""             |             |
| \_\_gl\_56347a                               | 1.0.0+      | ""             |             |
| \_\_gl\_563a95f1                             | 1.0.0+      | ""             |             |
| \_\_gl\_573823                               | 1.0.0+      | ""             |             |
| \_\_gl\_58027529                             | 1.0.0+      | ""             |             |
| \_\_gl\_5d2d63                               | 1.0.0+      | ""             |             |
| \_\_gl\_5f7e3b                               | 1.0.0+      | ""             |             |
| \_\_gl\_60461793                             | 1.0.0+      | ""             |             |
| \_\_gl\_60d355                               | 1.0.0+      | ""             |             |
| \_\_gl\_616627aa                             | 1.0.0+      | ""             |             |
| \_\_gl\_62317182                             | 1.0.0+      | ""             |             |
| \_\_gl\_6253fa2e                             | 1.0.0+      | ""             |             |
| \_\_gl\_64100768                             | 1.0.0+      | ""             |             |
| \_\_gl\_64100769                             | 1.0.0+      | ""             |             |
| \_\_gl\_64100770                             | 1.0.0+      | ""             |             |
| \_\_gl\_647395                               | 1.0.0+      | ""             |             |
| \_\_gl\_66543234                             | 1.0.0+      | ""             |             |
| \_\_gl\_67674763                             | 1.0.0+      | ""             |             |
| \_\_gl\_67739784                             | 1.0.0+      | ""             |             |
| \_\_gl\_68fb9c                               | 1.0.0+      | ""             |             |
| \_\_gl\_69801276                             | 1.0.0+      | ""             |             |
| \_\_gl\_6af9fa2f                             | 1.0.0+      | ""             |             |
| \_\_gl\_6af9fa3f                             | 1.0.0+      | ""             |             |
| \_\_gl\_6af9fa4f                             | 1.0.0+      | ""             |             |
| \_\_gl\_6bd8c7                               | 1.0.0+      | ""             |             |
| \_\_gl\_6c7691                               | 1.0.0+      | ""             |             |
| \_\_gl\_6d4296ce                             | 1.0.0+      | ""             |             |
| \_\_gl\_6dd7e7                               | 1.0.0+      | ""             |             |
| \_\_gl\_6dd7e8                               | 1.0.0+      | ""             |             |
| \_\_gl\_6fe11ec1                             | 1.0.0+      | ""             |             |
| \_\_gl\_716511763                            | 1.0.0+      | ""             |             |
| \_\_gl\_72504593                             | 1.0.0+      | ""             |             |
| \_\_gl\_73304097                             | 1.0.0+      | ""             |             |
| \_\_gl\_73314098                             | 1.0.0+      | ""             |             |
| \_\_gl\_74095213                             | 1.0.0+      | ""             |             |
| \_\_gl\_74095213a                            | 1.0.0+      | ""             |             |
| \_\_gl\_74095213b                            | 1.0.0+      | ""             |             |
| \_\_gl\_74095214                             | 1.0.0+      | ""             |             |
| \_\_gl\_748f9649                             | 1.0.0+      | ""             |             |
| \_\_gl\_75494732                             | 1.0.0+      | ""             |             |
| \_\_gl\_78452832                             | 1.0.0+      | ""             |             |
| \_\_gl\_784561                               | 1.0.0+      | ""             |             |
| \_\_gl\_78e16b9c                             | 1.0.0+      | ""             |             |
| \_\_gl\_79251225                             | 1.0.0+      | ""             |             |
| \_\_gl\_7c128b                               | 1.0.0+      | ""             |             |
| \_\_gl\_7ccd93                               | 1.0.0+      | ""             |             |
| \_\_gl\_7df8d1                               | 1.0.0+      | ""             |             |
| \_\_gl\_800c2310                             | 1.0.0+      | ""             |             |
| \_\_gl\_80546710                             | 1.0.0+      | ""             |             |
| \_\_gl\_80772310                             | 1.0.0+      | ""             |             |
| \_\_gl\_808ee280                             | 1.0.0+      | ""             |             |
| \_\_gl\_81131154                             | 1.0.0+      | ""             |             |
| \_\_gl\_81274457                             | 1.0.0+      | ""             |             |
| \_\_gl\_8292291f                             | 1.0.0+      | ""             |             |
| \_\_gl\_83498426                             | 1.0.0+      | ""             |             |
| \_\_gl\_84993794                             | 1.0.0+      | ""             |             |
| \_\_gl\_84995585                             | 1.0.0+      | ""             |             |
| \_\_gl\_84a0a0                               | 1.0.0+      | ""             |             |
| \_\_gl\_852142                               | 1.0.0+      | ""             |             |
| \_\_gl\_85612309                             | 1.0.0+      | ""             |             |
| \_\_gl\_85612310                             | 1.0.0+      | ""             |             |
| \_\_gl\_85612311                             | 1.0.0+      | ""             |             |
| \_\_gl\_85612312                             | 1.0.0+      | ""             |             |
| \_\_gl\_8623ff27                             | 1.0.0+      | ""             |             |
| \_\_gl\_87364952                             | 1.0.0+      | ""             |             |
| \_\_gl\_87f6275666                           | 1.0.0+      | ""             |             |
| \_\_gl\_886748                               | 1.0.0+      | ""             |             |
| \_\_gl\_89894423                             | 1.0.0+      | ""             |             |
| \_\_gl\_8ad8a75                              | 1.0.0+      | ""             |             |
| \_\_gl\_8ad8ad00                             | 1.0.0+      | ""             |             |
| \_\_gl\_8bb815                               | 1.0.0+      | ""             |             |
| \_\_gl\_8bb817                               | 1.0.0+      | ""             |             |
| \_\_gl\_8bb818                               | 1.0.0+      | ""             |             |
| \_\_gl\_8bb819                               | 1.0.0+      | ""             |             |
| \_\_gl\_8e640cd1                             | 1.0.0+      | ""             |             |
| \_\_gl\_8f34971a                             | 1.0.0+      | ""             |             |
| \_\_gl\_8f773984                             | 1.0.0+      | ""             |             |
| \_\_gl\_8f7a7d                               | 1.0.0+      | ""             |             |
| \_\_gl\_902486209                            | 1.0.0+      | ""             |             |
| \_\_gl\_90482571                             | 1.0.0+      | ""             |             |
| \_\_gl\_91214835                             | 1.0.0+      | ""             |             |
| \_\_gl\_912848290                            | 1.0.0+      | ""             |             |
| \_\_gl\_915e56                               | 1.0.0+      | ""             |             |
| \_\_gl\_92179063                             | 1.0.0+      | ""             |             |
| \_\_gl\_92179064                             | 1.0.0+      | ""             |             |
| \_\_gl\_92179065                             | 1.0.0+      | ""             |             |
| \_\_gl\_92179066                             | 1.0.0+      | ""             |             |
| \_\_gl\_92350358                             | 1.0.0+      | ""             |             |
| \_\_gl\_92809063                             | 1.0.0+      | ""             |             |
| \_\_gl\_92809064                             | 1.0.0+      | ""             |             |
| \_\_gl\_92809065                             | 1.0.0+      | ""             |             |
| \_\_gl\_92809066                             | 1.0.0+      | ""             |             |
| \_\_gl\_92920143                             | 1.0.0+      | ""             |             |
| \_\_gl\_93a89b12                             | 1.0.0+      | ""             |             |
| \_\_gl\_93a89c0b                             | 1.0.0+      | ""             |             |
| \_\_gl\_94812574                             | 1.0.0+      | ""             |             |
| \_\_gl\_95282304                             | 1.0.0+      | ""             |             |
| \_\_gl\_95394027                             | 1.0.0+      | ""             |             |
| \_\_gl\_959b1f                               | 1.0.0+      | ""             |             |
| \_\_gl\_9638af                               | 1.0.0+      | ""             |             |
| \_\_gl\_96fd59                               | 1.0.0+      | ""             |             |
| \_\_gl\_97f6275666                           | 1.0.0+      | ""             |             |
| \_\_gl\_97f6275667                           | 1.0.0+      | ""             |             |
| \_\_gl\_97f6275668                           | 1.0.0+      | ""             |             |
| \_\_gl\_97f6275669                           | 1.0.0+      | ""             |             |
| \_\_gl\_97f627566a                           | 1.0.0+      | ""             |             |
| \_\_gl\_97f627566b                           | 1.0.0+      | ""             |             |
| \_\_gl\_97f627566d                           | 1.0.0+      | ""             |             |
| \_\_gl\_97f627566e                           | 1.0.0+      | ""             |             |
| \_\_gl\_97f627566f                           | 1.0.0+      | ""             |             |
| \_\_gl\_97f6275670                           | 1.0.0+      | ""             |             |
| \_\_gl\_97f6275671                           | 1.0.0+      | ""             |             |
| \_\_gl\_97f727566e                           | 1.0.0+      | ""             |             |
| \_\_gl\_98480775                             | 1.0.0+      | ""             |             |
| \_\_gl\_98480776                             | 1.0.0+      | ""             |             |
| \_\_gl\_98480777                             | 1.0.0+      | ""             |             |
| \_\_gl\_992431                               | 1.0.0+      | ""             |             |
| \_\_gl\_9aa29065                             | 1.0.0+      | ""             |             |
| \_\_gl\_9af32c                               | 1.0.0+      | ""             |             |
| \_\_gl\_9af32d                               | 1.0.0+      | ""             |             |
| \_\_gl\_9af32e                               | 1.0.0+      | ""             |             |
| \_\_gl\_9c108b71                             | 1.0.0+      | ""             |             |
| \_\_gl\_9f279065                             | 1.0.0+      | ""             |             |
| \_\_gl\_a01bc728                             | 1.0.0+      | ""             |             |
| \_\_gl\_a13b46c80                            | 1.0.0+      | ""             |             |
| \_\_gl\_a22eb0                               | 1.0.0+      | ""             |             |
| \_\_gl\_a2fb451e                             | 1.0.0+      | ""             |             |
| \_\_gl\_a3456abe                             | 1.0.0+      | ""             |             |
| \_\_gl\_a7044887                             | 1.0.0+      | ""             |             |
| \_\_gl\_a7149200                             | 1.0.0+      | ""             |             |
| \_\_gl\_a766215670                           | 1.0.0+      | ""             |             |
| \_\_gl\_aalinegamma                          | 1.0.0+      | ""             |             |
| \_\_gl\_aalinetweaks                         | 1.0.0+      | ""             |             |
| \_\_gl\_ab34ee01                             | 1.0.0+      | ""             |             |
| \_\_gl\_ab34ee02                             | 1.0.0+      | ""             |             |
| \_\_gl\_ab34ee03                             | 1.0.0+      | ""             |             |
| \_\_gl\_ac0274                               | 1.0.0+      | ""             |             |
| \_\_gl\_af73c63e                             | 1.0.0+      | ""             |             |
| \_\_gl\_af73c63f                             | 1.0.0+      | ""             |             |
| \_\_gl\_af9927                               | 1.0.0+      | ""             |             |
| \_\_gl\_afoverride                           | 1.0.0+      | ""             |             |
| \_\_gl\_allocdeviceevents                    | 1.0.0+      | ""             |             |
| \_\_gl\_app\_softimage                       | 1.0.0+      | ""             |             |
| \_\_gl\_app\_supportbits2                    | 1.0.0+      | ""             |             |
| \_\_gl\_applicationkey                       | 1.0.0+      | ""             |             |
| \_\_gl\_appreturnonlybasicglsltype           | 1.0.0+      | ""             |             |
| \_\_gl\_assumetextureismipmappedatcreation   | 1.0.0+      | ""             |             |
| \_\_gl\_b1fb0f01                             | 1.0.0+      | ""             |             |
| \_\_gl\_b3edd5                               | 1.0.0+      | ""             |             |
| \_\_gl\_b40d9e03d                            | 1.0.0+      | ""             |             |
| \_\_gl\_b7f6275666                           | 1.0.0+      | ""             |             |
| \_\_gl\_b812c1                               | 1.0.0+      | ""             |             |
| \_\_gl\_ba14ba1a                             | 1.0.0+      | ""             |             |
| \_\_gl\_ba14ba1b                             | 1.0.0+      | ""             |             |
| \_\_gl\_bd7559                               | 1.0.0+      | ""             |             |
| \_\_gl\_bd755a                               | 1.0.0+      | ""             |             |
| \_\_gl\_bd755c                               | 1.0.0+      | ""             |             |
| \_\_gl\_bd755d                               | 1.0.0+      | ""             |             |
| \_\_gl\_be58bb                               | 1.0.0+      | ""             |             |
| \_\_gl\_be92cb                               | 1.0.0+      | ""             |             |
| \_\_gl\_beefcba3                             | 1.0.0+      | ""             |             |
| \_\_gl\_beefcba4                             | 1.0.0+      | ""             |             |
| \_\_gl\_c023777f                             | 1.0.0+      | ""             |             |
| \_\_gl\_c09dc8                               | 1.0.0+      | ""             |             |
| \_\_gl\_c0d340                               | 1.0.0+      | ""             |             |
| \_\_gl\_c2ff374c                             | 1.0.0+      | ""             |             |
| \_\_gl\_c5e9d7a3                             | 1.0.0+      | ""             |             |
| \_\_gl\_c5e9d7a4                             | 1.0.0+      | ""             |             |
| \_\_gl\_c5e9d7b4                             | 1.0.0+      | ""             |             |
| \_\_gl\_c618f9                               | 1.0.0+      | ""             |             |
| \_\_gl\_ca345840                             | 1.0.0+      | ""             |             |
| \_\_gl\_cachedisable                         | 1.0.0+      | ""             |             |
| \_\_gl\_channelpriorityoverride              | 1.0.0+      | ""             |             |
| \_\_gl\_cleardatastorevidmem                 | 1.0.0+      | ""             |             |
| \_\_gl\_cmdbufmemoryspaceenables             | 1.0.0+      | ""             |             |
| \_\_gl\_cmdbufminwords                       | 1.0.0+      | ""             |             |
| \_\_gl\_cmdbufsizewords                      | 1.0.0+      | ""             |             |
| \_\_gl\_conformantblitframebufferscissor     | 1.0.0+      | ""             |             |
| \_\_gl\_conformantincompletetextures         | 1.0.0+      | ""             |             |
| \_\_gl\_copybuffermethod                     | 1.0.0+      | ""             |             |
| \_\_gl\_cubemapaniso                         | 1.0.0+      | ""             |             |
| \_\_gl\_cubemapfiltering                     | 1.0.0+      | ""             |             |
| \_\_gl\_d0e9a4d7                             | 1.0.0+      | ""             |             |
| \_\_gl\_d13733f12                            | 1.0.0+      | ""             |             |
| \_\_gl\_d1b399                               | 1.0.0+      | ""             |             |
| \_\_gl\_d2983c32                             | 1.0.0+      | ""             |             |
| \_\_gl\_d2983c33                             | 1.0.0+      | ""             |             |
| \_\_gl\_d2e71b                               | 1.0.0+      | ""             |             |
| \_\_gl\_d377dc                               | 1.0.0+      | ""             |             |
| \_\_gl\_d377dd                               | 1.0.0+      | ""             |             |
| \_\_gl\_d489f4                               | 1.0.0+      | ""             |             |
| \_\_gl\_d4bce1                               | 1.0.0+      | ""             |             |
| \_\_gl\_d518cb                               | 1.0.0+      | ""             |             |
| \_\_gl\_d518cd                               | 1.0.0+      | ""             |             |
| \_\_gl\_d518ce                               | 1.0.0+      | ""             |             |
| \_\_gl\_d518d0                               | 1.0.0+      | ""             |             |
| \_\_gl\_d518d1                               | 1.0.0+      | ""             |             |
| \_\_gl\_d518d2                               | 1.0.0+      | ""             |             |
| \_\_gl\_d518d3                               | 1.0.0+      | ""             |             |
| \_\_gl\_d518d4                               | 1.0.0+      | ""             |             |
| \_\_gl\_d518d5                               | 1.0.0+      | ""             |             |
| \_\_gl\_d59eda                               | 1.0.0+      | ""             |             |
| \_\_gl\_d83cbd                               | 1.0.0+      | ""             |             |
| \_\_gl\_d8e777                               | 1.0.0+      | ""             |             |
| \_\_gl\_debug\_level                         | 1.0.0+      | ""             |             |
| \_\_gl\_debug\_mask                          | 1.0.0+      | ""             |             |
| \_\_gl\_debug\_options                       | 1.0.0+      | ""             |             |
| \_\_gl\_devshmpageableallocations            | 1.0.0+      | ""             |             |
| \_\_gl\_df1f9812                             | 1.0.0+      | ""             |             |
| \_\_gl\_df783c                               | 1.0.0+      | ""             |             |
| \_\_gl\_diagenable                           | 1.0.0+      | ""             |             |
| \_\_gl\_disallowcemask                       | 1.0.0+      | ""             |             |
| \_\_gl\_disallowz16                          | 1.0.0+      | ""             |             |
| \_\_gl\_dlmemoryspaceenables                 | 1.0.0+      | ""             |             |
| \_\_gl\_e0bfec                               | 1.0.0+      | ""             |             |
| \_\_gl\_e433456d                             | 1.0.0+      | ""             |             |
| \_\_gl\_e435563f                             | 1.0.0+      | ""             |             |
| \_\_gl\_e4cd9c                               | 1.0.0+      | ""             |             |
| \_\_gl\_e5c972                               | 1.0.0+      | ""             |             |
| \_\_gl\_e639ef                               | 1.0.0+      | ""             |             |
| \_\_gl\_e802af                               | 1.0.0+      | ""             |             |
| \_\_gl\_eae964                               | 1.0.0+      | ""             |             |
| \_\_gl\_earlytexturehwallocation             | 1.0.0+      | ""             |             |
| \_\_gl\_eb92a3                               | 1.0.0+      | ""             |             |
| \_\_gl\_ebca56                               | 1.0.0+      | ""             |             |
| \_\_gl\_expert\_detail\_level                | 1.0.0+      | ""             |             |
| \_\_gl\_expert\_output\_mask                 | 1.0.0+      | ""             |             |
| \_\_gl\_expert\_report\_mask                 | 1.0.0+      | ""             |             |
| \_\_gl\_extensionstringnvarch                | 1.0.0+      | ""             |             |
| \_\_gl\_extensionstringversion               | 1.0.0+      | ""             |             |
| \_\_gl\_f00f1938                             | 1.0.0+      | ""             |             |
| \_\_gl\_f10736                               | 1.0.0+      | ""             |             |
| \_\_gl\_f1846870                             | 1.0.0+      | ""             |             |
| \_\_gl\_f33bc370                             | 1.0.0+      | ""             |             |
| \_\_gl\_f392a874                             | 1.0.0+      | ""             |             |
| \_\_gl\_f49ae8                               | 1.0.0+      | ""             |             |
| \_\_gl\_fa345cce                             | 1.0.0+      | ""             |             |
| \_\_gl\_fa35cc4                              | 1.0.0+      | ""             |             |
| \_\_gl\_faa14a                               | 1.0.0+      | ""             |             |
| \_\_gl\_faf8a723                             | 1.0.0+      | ""             |             |
| \_\_gl\_fastgs                               | 1.0.0+      | ""             |             |
| \_\_gl\_fbf4ac45                             | 1.0.0+      | ""             |             |
| \_\_gl\_fbo\_blit\_ignore\_srgb              | 1.0.0+      | ""             |             |
| \_\_gl\_fc64c7                               | 1.0.0+      | ""             |             |
| \_\_gl\_ff54ec97                             | 1.0.0+      | ""             |             |
| \_\_gl\_ff54ec98                             | 1.0.0+      | ""             |             |
| \_\_gl\_forceexitprocessdetach               | 1.0.0+      | ""             |             |
| \_\_gl\_forcerequestedesversion              | 1.0.0+      | ""             |             |
| \_\_gl\_glsynctovblank                       | 1.0.0+      | ""             |             |
| \_\_gl\_gvitimeoutcontrol                    | 1.0.0+      | ""             |             |
| \_\_gl\_hcctrl                               | 1.0.0+      | ""             |             |
| \_\_gl\_hwstate\_per\_ctx                    | 1.0.0+      | ""             |             |
| \_\_gl\_machinecachelimit                    | 1.0.0+      | ""             |             |
| \_\_gl\_maxframesallowed                     | 1.0.0+      | ""             |             |
| \_\_gl\_memmgrcachedalloclimit               | 1.0.0+      | ""             |             |
| \_\_gl\_memmgrcachedalloclimitratio          | 1.0.0+      | ""             |             |
| \_\_gl\_memmgrsysheapalloclimit              | 1.0.0+      | ""             |             |
| \_\_gl\_memmgrsysheapalloclimitratio         | 1.0.0+      | ""             |             |
| \_\_gl\_memmgrvidheapalloclimit              | 1.0.0+      | ""             |             |
| \_\_gl\_mosaic\_clip\_to\_subdev             | 1.0.0+      | ""             |             |
| \_\_gl\_mosaic\_clip\_to\_subdev\_h\_overlap | 1.0.0+      | ""             |             |
| \_\_gl\_mosaic\_clip\_to\_subdev\_v\_overlap | 1.0.0+      | ""             |             |
| \_\_gl\_overlaymergeblittimerms              | 1.0.0+      | ""             |             |
| \_\_gl\_perfmon\_mode                        | 1.0.0+      | ""             |             |
| \_\_gl\_pixbar\_mode                         | 1.0.0+      | ""             |             |
| \_\_gl\_qualityenhancements                  | 1.0.0+      | ""             |             |
| \_\_gl\_r27s18q28                            | 1.0.0+      | ""             |             |
| \_\_gl\_r2d7c1d8                             | 1.0.0+      | ""             |             |
| \_\_gl\_renderer                             | 1.0.0+      | ""             |             |
| \_\_gl\_renderqualityflags                   | 1.0.0+      | ""             |             |
| \_\_gl\_s3tcquality                          | 1.0.0+      | ""             |             |
| \_\_gl\_shader\_disk\_cache\_path            | 1.0.0+      | ""             |             |
| \_\_gl\_shader\_disk\_cache\_read\_only      | 1.0.0+      | ""             |             |
| \_\_gl\_shaderatomics                        | 1.0.0+      | ""             |             |
| \_\_gl\_shadercacheinitsize                  | 1.0.0+      | ""             |             |
| \_\_gl\_shaderobjects                        | 1.0.0+      | ""             |             |
| \_\_gl\_shaderportabilitywarnings            | 1.0.0+      | ""             |             |
| \_\_gl\_shaderwarningsaserrors               | 1.0.0+      | ""             |             |
| \_\_gl\_skiptexturehostcopies                | 1.0.0+      | ""             |             |
| \_\_gl\_sli\_dli\_control                    | 1.0.0+      | ""             |             |
| \_\_gl\_sparsetexture                        | 1.0.0+      | ""             |             |
| \_\_gl\_spinlooptimeout                      | 1.0.0+      | ""             |             |
| \_\_gl\_sync\_to\_vblank                     | 1.0.0+      | ""             |             |
| \_\_gl\_sysheapreuseratio                    | 1.0.0+      | ""             |             |
| \_\_gl\_sysmemtexturepromotion               | 1.0.0+      | ""             |             |
| \_\_gl\_targetflushcount                     | 1.0.0+      | ""             |             |
| \_\_gl\_tearingfreeswappresent               | 1.0.0+      | ""             |             |
| \_\_gl\_texclampbehavior                     | 1.0.0+      | ""             |             |
| \_\_gl\_texlodbias                           | 1.0.0+      | ""             |             |
| \_\_gl\_texmemoryspaceenables                | 1.0.0+      | ""             |             |
| \_\_gl\_textureprecache                      | 1.0.0+      | ""             |             |
| \_\_gl\_threadcontrol                        | 1.0.0+      | ""             |             |
| \_\_gl\_threadcontrol2                       | 1.0.0+      | ""             |             |
| \_\_gl\_usegvievents                         | 1.0.0+      | ""             |             |
| \_\_gl\_vbomemoryspaceenables                | 1.0.0+      | ""             |             |
| \_\_gl\_vertexlimit                          | 1.0.0+      | ""             |             |
| \_\_gl\_vidheapreuseratio                    | 1.0.0+      | ""             |             |
| \_\_gl\_vpipe                                | 1.0.0+      | ""             |             |
| \_\_gl\_vpipeformatbloatlimit                | 1.0.0+      | ""             |             |
| \_\_gl\_wglmessageboxonabort                 | 1.0.0+      | ""             |             |
| \_\_gl\_writeinfolog                         | 1.0.0+      | ""             |             |
| \_\_gl\_writeprogramobjectassembly           | 1.0.0+      | ""             |             |
| \_\_gl\_writeprogramobjectsource             | 1.0.0+      | ""             |             |
| \_\_gl\_xnvadapterpresent                    | 1.0.0+      | ""             |             |
| \_\_gl\_yield                                | 1.0.0+      | ""             |             |
| \_\_gl\_yieldfunction                        | 1.0.0+      | ""             |             |
| \_\_gl\_yieldfunctionfast                    | 1.0.0+      | ""             |             |
| \_\_gl\_yieldfunctionslow                    | 1.0.0+      | ""             |             |
| \_\_gl\_yieldfunctionwaitfordcqueue          | 1.0.0+      | ""             |             |
| \_\_gl\_yieldfunctionwaitforframe            | 1.0.0+      | ""             |             |
| \_\_gl\_yieldfunctionwaitforgpu              | 1.0.0+      | ""             |             |
| \_\_gl\_zbctableaddhysteresis                | 1.0.0+      | ""             |             |
| \_\_glslc\_debug\_filename                   | 1.0.0+      | ""             |             |
| \_\_glslc\_debug\_level                      | 1.0.0+      | ""             |             |
| \_\_glslc\_debug\_mask                       | 1.0.0+      | ""             |             |
| \_\_glslc\_debug\_options                    | 1.0.0+      | ""             |             |
| \_\_glslc\_version\_major\_override          | 4.0.0+      | ""             |             |
| \_\_glslc\_version\_minor\_override          | 4.0.0+      | ""             |             |
| a01bc728                                     | 1.0.0+      | ""             |             |
| a13b46c80                                    | 1.0.0+      | ""             |             |
| a22eb0                                       | 1.0.0+      | ""             |             |
| a2fb451e                                     | 1.0.0+      | ""             |             |
| a3456abe                                     | 1.0.0+      | ""             |             |
| a7044887                                     | 1.0.0+      | ""             |             |
| a7149200                                     | 1.0.0+      | ""             |             |
| a766215670                                   | 1.0.0+      | ""             |             |
| aac\_drc\_boost                              | 1.0.0+      | ""             |             |
| aac\_drc\_cut                                | 1.0.0+      | ""             |             |
| aac\_drc\_enc\_target\_level                 | 1.0.0+      | ""             |             |
| aac\_drc\_heavy                              | 1.0.0+      | ""             |             |
| aac\_drc\_reference\_level                   | 1.0.0+      | ""             |             |
| aalinegamma                                  | 1.0.0+      | ""             |             |
| aalinetweaks                                 | 1.0.0+      | ""             |             |
| ab34ee01                                     | 1.0.0+      | ""             |             |
| ab34ee02                                     | 1.0.0+      | ""             |             |
| ab34ee03                                     | 1.0.0+      | ""             |             |
| ac0274                                       | 1.0.0+      | ""             |             |
| af73c63e                                     | 1.0.0+      | ""             |             |
| af73c63f                                     | 1.0.0+      | ""             |             |
| af9927                                       | 1.0.0+      | ""             |             |
| afoverride                                   | 1.0.0+      | ""             |             |
| allocdeviceevents                            | 1.0.0+      | ""             |             |
| app\_softimage                               | 1.0.0+      | ""             |             |
| app\_supportbits2                            | 1.0.0+      | ""             |             |
| applicationkey                               | 1.0.0+      | ""             |             |
| appreturnonlybasicglsltype                   | 1.0.0+      | ""             |             |
| assumetextureismipmappedatcreation           | 1.0.0+      | ""             |             |
| b1fb0f01                                     | 1.0.0+      | ""             |             |
| b3edd5                                       | 1.0.0+      | ""             |             |
| b40d9e03d                                    | 1.0.0+      | ""             |             |
| b7f6275666                                   | 1.0.0+      | ""             |             |
| b812c1                                       | 1.0.0+      | ""             |             |
| ba14ba1a                                     | 1.0.0+      | ""             |             |
| ba14ba1b                                     | 1.0.0+      | ""             |             |
| bd7559                                       | 1.0.0+      | ""             |             |
| bd755a                                       | 1.0.0+      | ""             |             |
| bd755c                                       | 1.0.0+      | ""             |             |
| bd755d                                       | 1.0.0+      | ""             |             |
| be58bb                                       | 1.0.0+      | ""             |             |
| be92cb                                       | 1.0.0+      | ""             |             |
| beefcba3                                     | 1.0.0+      | ""             |             |
| beefcba4                                     | 1.0.0+      | ""             |             |
| c023777f                                     | 1.0.0+      | ""             |             |
| c09dc8                                       | 1.0.0+      | ""             |             |
| c0d340                                       | 1.0.0+      | ""             |             |
| c2ff374c                                     | 1.0.0+      | ""             |             |
| c5e9d7a3                                     | 1.0.0+      | ""             |             |
| c5e9d7a4                                     | 1.0.0+      | ""             |             |
| c5e9d7b4                                     | 1.0.0+      | ""             |             |
| c618f9                                       | 1.0.0+      | ""             |             |
| ca345840                                     | 1.0.0+      | ""             |             |
| cachedisable                                 | 1.0.0+      | ""             |             |
| cast.on                                      | 1.0.0+      | ""             |             |
| cde                                          | 1.0.0+      | ""             |             |
| channelpriorityoverride                      | 1.0.0+      | ""             |             |
| cleardatastorevidmem                         | 1.0.0+      | ""             |             |
| cmdbufmemoryspaceenables                     | 1.0.0+      | ""             |             |
| cmdbufminwords                               | 1.0.0+      | ""             |             |
| cmdbufsizewords                              | 1.0.0+      | ""             |             |
| conformantblitframebufferscissor             | 1.0.0+      | ""             |             |
| conformantincompletetextures                 | 1.0.0+      | ""             |             |
| copybuffermethod                             | 1.0.0+      | ""             |             |
| cubemapaniso                                 | 1.0.0+      | ""             |             |
| cubemapfiltering                             | 1.0.0+      | ""             |             |
| cuda\_auto\_boost                            | 4.0.0+      | ""             |             |
| cuda\_cache\_disable                         | 4.0.0+      | ""             |             |
| cuda\_cache\_maxsize                         | 4.0.0+      | ""             |             |
| cuda\_cache\_path                            | 4.0.0+      | ""             |             |
| cuda\_devcode\_path                          | 4.0.0+      | ""             |             |
| cuda\_device\_max\_connections               | 4.0.0+      | ""             |             |
| cuda\_device\_order                          | 4.0.0+      | ""             |             |
| cuda\_device\_waits\_on\_exception           | 4.0.0+      | ""             |             |
| cuda\_disable\_fast\_ecc                     | 4.0.0+      | ""             |             |
| cuda\_disable\_process\_error\_mode          | 4.0.0+      | ""             |             |
| cuda\_enable\_p2p\_no\_uva                   | 4.0.0+      | ""             |             |
| cuda\_force\_ptx\_jit                        | 4.0.0+      | ""             |             |
| cuda\_launch\_blocking                       | 4.0.0+      | ""             |             |
| cuda\_managed\_force\_device\_alloc          | 4.0.0+      | ""             |             |
| cuda\_set\_watchdog                          | 4.0.0+      | ""             |             |
| cuda\_va\_reservation\_chunk\_size           | 4.0.0+      | ""             |             |
| cuda\_visible\_devices                       | 4.0.0+      | ""             |             |
| d0e9a4d7                                     | 1.0.0+      | ""             |             |
| d13733f12                                    | 1.0.0+      | ""             |             |
| d1b399                                       | 1.0.0+      | ""             |             |
| d2983c32                                     | 1.0.0+      | ""             |             |
| d2983c33                                     | 1.0.0+      | ""             |             |
| d2e71b                                       | 1.0.0+      | ""             |             |
| d377dc                                       | 1.0.0+      | ""             |             |
| d377dd                                       | 1.0.0+      | ""             |             |
| d489f4                                       | 1.0.0+      | ""             |             |
| d4bce1                                       | 1.0.0+      | ""             |             |
| d518cb                                       | 1.0.0+      | ""             |             |
| d518cd                                       | 1.0.0+      | ""             |             |
| d518ce                                       | 1.0.0+      | ""             |             |
| d518d0                                       | 1.0.0+      | ""             |             |
| d518d1                                       | 1.0.0+      | ""             |             |
| d518d2                                       | 1.0.0+      | ""             |             |
| d518d3                                       | 1.0.0+      | ""             |             |
| d518d4                                       | 1.0.0+      | ""             |             |
| d518d5                                       | 1.0.0+      | ""             |             |
| d59eda                                       | 1.0.0+      | ""             |             |
| d83cbd                                       | 1.0.0+      | ""             |             |
| d8e777                                       | 1.0.0+      | ""             |             |
| debug\_level                                 | 1.0.0+      | ""             |             |
| debug\_mask                                  | 1.0.0+      | ""             |             |
| debug\_options                               | 1.0.0+      | ""             |             |
| devshmpageableallocations                    | 1.0.0+      | ""             |             |
| df1f9812                                     | 1.0.0+      | ""             |             |
| df783c                                       | 1.0.0+      | ""             |             |
| diagenable                                   | 1.0.0+      | ""             |             |
| disallowcemask                               | 1.0.0+      | ""             |             |
| disallowz16                                  | 1.0.0+      | ""             |             |
| dlmemoryspaceenables                         | 1.0.0+      | ""             |             |
| e0bfec                                       | 1.0.0+      | ""             |             |
| e433456d                                     | 1.0.0+      | ""             |             |
| e435563f                                     | 1.0.0+      | ""             |             |
| e4cd9c                                       | 1.0.0+      | ""             |             |
| e5c972                                       | 1.0.0+      | ""             |             |
| e639ef                                       | 1.0.0+      | ""             |             |
| e802af                                       | 1.0.0+      | ""             |             |
| eae964                                       | 1.0.0+      | ""             |             |
| earlytexturehwallocation                     | 1.0.0+      | ""             |             |
| eb92a3                                       | 1.0.0+      | ""             |             |
| ebca56                                       | 1.0.0+      | ""             |             |
| enable-noaud                                 | 1.0.0+      | ""             |             |
| enable-noavs                                 | 1.0.0+      | ""             |             |
| enable-prof                                  | 1.0.0+      | ""             |             |
| enable-sxesmode                              | 1.0.0+      | ""             |             |
| enable-ulld                                  | 1.0.0+      | ""             |             |
| expert\_detail\_level                        | 1.0.0+      | ""             |             |
| expert\_output\_mask                         | 1.0.0+      | ""             |             |
| expert\_report\_mask                         | 1.0.0+      | ""             |             |
| extensionstringnvarch                        | 1.0.0+      | ""             |             |
| extensionstringversion                       | 1.0.0+      | ""             |             |
| f00f1938                                     | 1.0.0+      | ""             |             |
| f10736                                       | 1.0.0+      | ""             |             |
| f1846870                                     | 1.0.0+      | ""             |             |
| f33bc370                                     | 1.0.0+      | ""             |             |
| f392a874                                     | 1.0.0+      | ""             |             |
| f49ae8                                       | 1.0.0+      | ""             |             |
| fa345cce                                     | 1.0.0+      | ""             |             |
| fa35cc4                                      | 1.0.0+      | ""             |             |
| faa14a                                       | 1.0.0+      | ""             |             |
| faf8a723                                     | 1.0.0+      | ""             |             |
| fastgs                                       | 1.0.0+      | ""             |             |
| fbf4ac45                                     | 1.0.0+      | ""             |             |
| fbo\_blit\_ignore\_srgb                      | 1.0.0+      | ""             |             |
| fc64c7                                       | 1.0.0+      | ""             |             |
| ff54ec97                                     | 1.0.0+      | ""             |             |
| ff54ec98                                     | 1.0.0+      | ""             |             |
| forceexitprocessdetach                       | 1.0.0+      | ""             |             |
| forcerequestedesversion                      | 1.0.0+      | ""             |             |
| glsynctovblank                               | 1.0.0+      | ""             |             |
| gpu\_debug\_mode                             | 3.0.0+      | ""             |             |
| gpu\_stay\_on                                | 1.0.0+      | ""             |             |
| gpu\_timeout\_ms\_max                        | 3.0.0+      | ""             |             |
| gvitimeoutcontrol                            | 1.0.0+      | ""             |             |
| hcctrl                                       | 1.0.0+      | ""             |             |
| hwstate\_per\_ctx                            | 1.0.0+      | ""             |             |
| libandroid\_enable\_log                      | 1.0.0+      | ""             |             |
| machinecachelimit                            | 1.0.0+      | ""             |             |
| maxframesallowed                             | 1.0.0+      | ""             |             |
| media.aac\_51\_output\_enabled               | 1.0.0+      | ""             |             |
| memmgrcachedalloclimit                       | 1.0.0+      | ""             |             |
| memmgrcachedalloclimitratio                  | 1.0.0+      | ""             |             |
| memmgrsysheapalloclimit                      | 1.0.0+      | ""             |             |
| memmgrsysheapalloclimitratio                 | 1.0.0+      | ""             |             |
| memmgrvidheapalloclimit                      | 1.0.0+      | ""             |             |
| mosaic\_clip\_to\_subdev                     | 1.0.0+      | ""             |             |
| mosaic\_clip\_to\_subdev\_h\_overlap         | 1.0.0+      | ""             |             |
| mosaic\_clip\_to\_subdev\_v\_overlap         | 1.0.0+      | ""             |             |
| nv\_decompression                            | 1.0.0+      | ""             |             |
| nv\_emc\_dvfs\_test                          | 1.0.0+      | ""             |             |
| nv\_emc\_init\_rate\_hz                      | 1.0.0+      | ""             |             |
| nv\_gmmu\_va\_page\_split                    | 1.0.0+      | ""             |             |
| nv\_gmmu\_va\_range                          | 1.0.0+      | ""             |             |
| nv\_graphics\_firmware\_memory\_margin       | 3.0.0+      | false          |             |
| nv\_memory\_profiler                         | 1.0.0+      | ""             |             |
| nv\_pllcx\_always\_on                        | 1.0.0+      | ""             |             |
| nv\_pllcx\_safe\_div                         | 1.0.0+      | ""             |             |
| nv\_usb\_plls\_hw\_ctrl                      | 1.0.0+      | ""             |             |
| nv\_winsys                                   | 1.0.0+      | ""             |             |
| nvblit.dump                                  | 1.0.0+      | ""             |             |
| nvblit.profile                               | 1.0.0+      | ""             |             |
| nvblit.twod                                  | 1.0.0+      | ""             |             |
| nvblit.vic                                   | 1.0.0+      | ""             |             |
| nvddk\_vic\_prevent\_use                     | 1.0.0+      | ""             |             |
| nvdisp\_bl\_ctrl                             | 1.0.0+      | "0"            |             |
| nvdisp\_debug\_mask                          | 1.0.0+      | ""             |             |
| nvdisp\_enable\_ts                           | 2.0.0+      | "0"            |             |
| nvhdcp\_max\_retries                         | 3.0.0-3.0.2 | "5"            |             |
| 4.0.0+                                       | ""          |                |             |
| nvhdcp\_timeout\_ms                          | 3.0.0-3.0.2 | "12000"        |             |
| 4.0.0+                                       | ""          |                |             |
| nvhost\_debug\_mask                          | 1.0.0+      | ""             |             |
| nvhost\_vic\_memory\_policy                  | 5.0.0-5.1.0 | "0"            |             |
| 6.0.0+                                       | "1"         |                |             |
| nvidia.hwc.control\_modeset                  | 5.0.0+      | ""             |             |
| nvidia.hwc.dump\_config                      | 1.0.0+      | ""             |             |
| nvidia.hwc.dump\_layerlist                   | 1.0.0+      | ""             |             |
| nvidia.hwc.dump\_windows                     | 1.0.0+      | ""             |             |
| nvidia.hwc.enable\_disp\_trans               | 1.0.0+      | ""             |             |
| nvidia.hwc.ftrace\_enable                    | 1.0.0+      | ""             |             |
| nvidia.hwc.hdcp\_enable                      | 1.0.0+      | ""             |             |
| nvidia.hwc.hidden\_window\_mask0             | 1.0.0+      | ""             |             |
| nvidia.hwc.hidden\_window\_mask1             | 1.0.0+      | ""             |             |
| nvidia.hwc.immediate\_modeset                | 3.0.0+      | ""             |             |
| nvidia.hwc.imp\_enable                       | 1.0.0+      | ""             |             |
| nvidia.hwc.no\_egl                           | 1.0.0+      | ""             |             |
| nvidia.hwc.no\_scratchblit                   | 1.0.0+      | ""             |             |
| nvidia.hwc.no\_vic                           | 1.0.0+      | ""             |             |
| nvidia.hwc.null\_display                     | 1.0.0+      | ""             |             |
| nvidia.hwc.scan\_props                       | 1.0.0+      | ""             |             |
| nvidia.hwc.swap\_interval                    | 1.0.0+      | ""             |             |
| nvidia.hwc.war\_1515812                      | 1.0.0+      | "0"            |             |
| nvmap\_debug\_mask                           | 1.0.0+      | ""             |             |
| nvn\_no\_vsync\_capability                   | 2.2.0+      | false          |             |
| nvn\_through\_opengl                         | 1.0.0+      | ""             |             |
| nvnflinger\_enable\_log                      | 1.0.0+      | ""             |             |
| nvnflinger\_flip\_policy                     | 1.0.0+      | ""             |             |
| nvnflinger\_hotplug\_autoswitch              | 1.0.0+      | "0"            |             |
| nvnflinger\_prefer\_primary\_layer           | 1.0.0+      | "0"            |             |
| nvnflinger\_service\_priority                | 1.0.0+      | ""             |             |
| nvnflinger\_service\_threads                 | 1.0.0+      | ""             |             |
| nvnflinger\_swap\_interval                   | 1.0.0+      | ""             |             |
| nvnflinger\_track\_perf                      | 1.0.0+      | ""             |             |
| nvnflinger\_virtualdisplay\_policy           | 1.0.0+      | "60hz"         |             |
| nvrm\_gpu\_36lvajow                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_554expuw                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_59ct6eds                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_6aqelj8y                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_6trs9rwi                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_apapy18r                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_channel\_interleave               | 1.0.0+      | ""             |             |
| nvrm\_gpu\_channel\_priority                 | 1.0.0+      | ""             |             |
| nvrm\_gpu\_channel\_timeslice                | 1.0.0+      | ""             |             |
| nvrm\_gpu\_ci4wetrn                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_default\_device\_index            | 1.0.0+      | ""             |             |
| nvrm\_gpu\_disable\_compression              | 5.0.0+      | ""             |             |
| nvrm\_gpu\_dm7xllka                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_dummy                             | 1.0.0+      | ""             |             |
| nvrm\_gpu\_eepyr4lp                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_gjwknsbf                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_gt1cb8jb                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_help                              | 1.0.0+      | ""             |             |
| nvrm\_gpu\_isewvh0s                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_lfkct7ht                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_liy1nc6l                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_m5qebtld                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_maiapsxj                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_nbbeyqfm                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_nvgpu\_disable                    | 1.0.0+      | ""             |             |
| nvrm\_gpu\_nvgpu\_do\_nfa\_partial\_map      | 1.0.0+      | ""             |             |
| nvrm\_gpu\_nvgpu\_ecc\_overrides             | 1.0.0+      | ""             |             |
| nvrm\_gpu\_nvgpu\_force\_immediate\_unmap    | 6.0.0+      | ""             |             |
| nvrm\_gpu\_nvgpu\_force\_scg                 | 6.0.0+      | ""             |             |
| nvrm\_gpu\_nvgpu\_no\_as\_get\_va\_regions   | 1.0.0+      | ""             |             |
| nvrm\_gpu\_nvgpu\_no\_channel\_abort         | 1.0.0+      | ""             |             |
| nvrm\_gpu\_nvgpu\_no\_cyclestats             | 1.0.0+      | ""             |             |
| nvrm\_gpu\_nvgpu\_no\_fixed                  | 1.0.0+      | ""             |             |
| nvrm\_gpu\_nvgpu\_no\_gpu\_characteristics   | 1.0.0+      | ""             |             |
| nvrm\_gpu\_nvgpu\_no\_ioctl\_mutex           | 1.0.0+      | ""             |             |
| nvrm\_gpu\_nvgpu\_no\_l3                     | 6.0.0+      | ""             |             |
| nvrm\_gpu\_nvgpu\_no\_map\_buffer\_ex        | 1.0.0+      | ""             |             |
| nvrm\_gpu\_nvgpu\_no\_probe\_dgpu            | 5.0.0+      | ""             |             |
| nvrm\_gpu\_nvgpu\_no\_probe\_igpu            | 5.0.0+      | ""             |             |
| nvrm\_gpu\_nvgpu\_no\_robustness             | 1.0.0+      | ""             |             |
| nvrm\_gpu\_nvgpu\_no\_sparse                 | 1.0.0+      | ""             |             |
| nvrm\_gpu\_nvgpu\_no\_syncpoints             | 1.0.0+      | ""             |             |
| nvrm\_gpu\_nvgpu\_no\_tsg                    | 1.0.0+      | ""             |             |
| nvrm\_gpu\_nvgpu\_no\_zbc                    | 1.0.0+      | ""             |             |
| nvrm\_gpu\_nvgpu\_no\_zcull                  | 1.0.0+      | ""             |             |
| nvrm\_gpu\_nvgpu\_wrap\_channels\_in\_tsgs   | 1.0.0+      | ""             |             |
| nvrm\_gpu\_omdtirby                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_ometcz6b                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_osawipsf                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_prevent\_use                      | 1.0.0+      | ""             |             |
| nvrm\_gpu\_trace                             | 1.0.0+      | ""             |             |
| nvrm\_gpu\_uzfvtuhi                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_v5tz4s00                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_vgeey2dw                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_xatkicfl                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_xzoebcw9                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_yrghr5g6                          | 6.0.0+      | ""             |             |
| nvrm\_gpu\_zugirozd                          | 6.0.0+      | ""             |             |
| nvsched\_debug\_mask                         | 1.0.0+      | ""             |             |
| nvsched\_force\_enable                       | 1.0.0+      | ""             |             |
| nvsched\_force\_log                          | 3.0.0+      | ""             |             |
| nvwsi\_dump                                  | 1.0.0+      | ""             |             |
| nvwsi\_fill                                  | 1.0.0+      | ""             |             |
| ogl\_                                        | 1.0.0+      | ""             |             |
| ogl\_0356afd0                                | 1.0.0+      | ""             |             |
| ogl\_0356afd1                                | 1.0.0+      | ""             |             |
| ogl\_0356afd2                                | 1.0.0+      | ""             |             |
| ogl\_0356afd3                                | 1.0.0+      | ""             |             |
| ogl\_0x923dc0                                | 1.0.0+      | ""             |             |
| ogl\_0x923dc1                                | 1.0.0+      | ""             |             |
| ogl\_0x923dc2                                | 1.0.0+      | ""             |             |
| ogl\_0x923dc3                                | 1.0.0+      | ""             |             |
| ogl\_0x923dc4                                | 1.0.0+      | ""             |             |
| ogl\_0x923dd3                                | 1.0.0+      | ""             |             |
| ogl\_0x9abdc5                                | 1.0.0+      | ""             |             |
| ogl\_0x9abdc6                                | 1.0.0+      | ""             |             |
| ogl\_0xbd10fb                                | 1.0.0+      | ""             |             |
| ogl\_0xce2348                                | 1.0.0+      | ""             |             |
| ogl\_10261989                                | 1.0.0+      | ""             |             |
| ogl\_1042d483                                | 1.0.0+      | ""             |             |
| ogl\_10572898                                | 1.0.0+      | ""             |             |
| ogl\_115631                                  | 1.0.0+      | ""             |             |
| ogl\_12950094                                | 1.0.0+      | ""             |             |
| ogl\_1314f311                                | 1.0.0+      | ""             |             |
| ogl\_1314f312                                | 1.0.0+      | ""             |             |
| ogl\_13279512                                | 1.0.0+      | ""             |             |
| ogl\_13813496                                | 1.0.0+      | ""             |             |
| ogl\_14507179                                | 1.0.0+      | ""             |             |
| ogl\_15694569                                | 1.0.0+      | ""             |             |
| ogl\_16936964                                | 1.0.0+      | ""             |             |
| ogl\_17aa230c                                | 1.0.0+      | ""             |             |
| ogl\_182054                                  | 1.0.0+      | ""             |             |
| ogl\_18273275                                | 1.0.0+      | ""             |             |
| ogl\_18273276                                | 1.0.0+      | ""             |             |
| ogl\_1854d03b                                | 1.0.0+      | ""             |             |
| ogl\_18add00d                                | 1.0.0+      | ""             |             |
| ogl\_19156670                                | 1.0.0+      | ""             |             |
| ogl\_19286545                                | 1.0.0+      | ""             |             |
| ogl\_1a298e9f                                | 1.0.0+      | ""             |             |
| ogl\_1acf43fe                                | 1.0.0+      | ""             |             |
| ogl\_1bda43fe                                | 1.0.0+      | ""             |             |
| ogl\_1c3b92                                  | 1.0.0+      | ""             |             |
| ogl\_21509920                                | 1.0.0+      | ""             |             |
| ogl\_215323457                               | 1.0.0+      | ""             |             |
| ogl\_2165ad                                  | 1.0.0+      | ""             |             |
| ogl\_2165ae                                  | 1.0.0+      | ""             |             |
| ogl\_21be9c                                  | 1.0.0+      | ""             |             |
| ogl\_233264316                               | 1.0.0+      | ""             |             |
| ogl\_234557580                               | 1.0.0+      | ""             |             |
| ogl\_23cd0e                                  | 1.0.0+      | ""             |             |
| ogl\_24189123                                | 1.0.0+      | ""             |             |
| ogl\_2443266                                 | 1.0.0+      | ""             |             |
| ogl\_25025519                                | 1.0.0+      | ""             |             |
| ogl\_255e39                                  | 1.0.0+      | ""             |             |
| ogl\_2583364                                 | 1.0.0+      | ""             |             |
| ogl\_2888c1                                  | 1.0.0+      | ""             |             |
| ogl\_28ca3e                                  | 1.0.0+      | ""             |             |
| ogl\_29871243                                | 1.0.0+      | ""             |             |
| ogl\_2a1f64                                  | 1.0.0+      | ""             |             |
| ogl\_2dc432                                  | 1.0.0+      | ""             |             |
| ogl\_2de437                                  | 1.0.0+      | ""             |             |
| ogl\_2f3bb89c                                | 1.0.0+      | ""             |             |
| ogl\_2fd652                                  | 1.0.0+      | ""             |             |
| ogl\_3001ac                                  | 1.0.0+      | ""             |             |
| ogl\_31298772                                | 1.0.0+      | ""             |             |
| ogl\_313233                                  | 1.0.0+      | ""             |             |
| ogl\_31f7d603                                | 1.0.0+      | ""             |             |
| ogl\_320ce4                                  | 1.0.0+      | ""             |             |
| ogl\_32153248                                | 1.0.0+      | ""             |             |
| ogl\_32153249                                | 1.0.0+      | ""             |             |
| ogl\_335bca                                  | 1.0.0+      | ""             |             |
| ogl\_342abb                                  | 1.0.0+      | ""             |             |
| ogl\_34dfe6                                  | 1.0.0+      | ""             |             |
| ogl\_34dfe7                                  | 1.0.0+      | ""             |             |
| ogl\_34dfe8                                  | 1.0.0+      | ""             |             |
| ogl\_34dfe9                                  | 1.0.0+      | ""             |             |
| ogl\_35201578                                | 1.0.0+      | ""             |             |
| ogl\_359278                                  | 1.0.0+      | ""             |             |
| ogl\_37f53a                                  | 1.0.0+      | ""             |             |
| ogl\_38144972                                | 1.0.0+      | ""             |             |
| ogl\_38542646                                | 1.0.0+      | ""             |             |
| ogl\_3b74c9                                  | 1.0.0+      | ""             |             |
| ogl\_3c136f                                  | 1.0.0+      | ""             |             |
| ogl\_3cf72823                                | 1.0.0+      | ""             |             |
| ogl\_3d7af029                                | 1.0.0+      | ""             |             |
| ogl\_3ff34782                                | 1.0.0+      | ""             |             |
| ogl\_4129618                                 | 1.0.0+      | ""             |             |
| ogl\_4189fac3                                | 1.0.0+      | ""             |             |
| ogl\_420bd4                                  | 1.0.0+      | ""             |             |
| ogl\_42a699                                  | 1.0.0+      | ""             |             |
| ogl\_441369                                  | 1.0.0+      | ""             |             |
| ogl\_4458713e                                | 1.0.0+      | ""             |             |
| ogl\_4554b6                                  | 1.0.0+      | ""             |             |
| ogl\_457425                                  | 1.0.0+      | ""             |             |
| ogl\_4603b207                                | 1.0.0+      | ""             |             |
| ogl\_46574957                                | 1.0.0+      | ""             |             |
| ogl\_46574958                                | 1.0.0+      | ""             |             |
| ogl\_46813529                                | 1.0.0+      | ""             |             |
| ogl\_46f1e13d                                | 1.0.0+      | ""             |             |
| ogl\_47534c43                                | 1.0.0+      | ""             |             |
| ogl\_48550336                                | 1.0.0+      | ""             |             |
| ogl\_48576893                                | 1.0.0+      | ""             |             |
| ogl\_48576894                                | 1.0.0+      | ""             |             |
| ogl\_4889ac02                                | 1.0.0+      | ""             |             |
| ogl\_49005740                                | 1.0.0+      | ""             |             |
| ogl\_49867584                                | 1.0.0+      | ""             |             |
| ogl\_49960973                                | 1.0.0+      | ""             |             |
| ogl\_4a5341                                  | 1.0.0+      | ""             |             |
| ogl\_4f4e48                                  | 1.0.0+      | ""             |             |
| ogl\_4f8a0a                                  | 1.0.0+      | ""             |             |
| ogl\_50299698                                | 1.0.0+      | ""             |             |
| ogl\_50299699                                | 1.0.0+      | ""             |             |
| ogl\_50361291                                | 1.0.0+      | ""             |             |
| ogl\_5242ae                                  | 1.0.0+      | ""             |             |
| ogl\_53d30c                                  | 1.0.0+      | ""             |             |
| ogl\_56347a                                  | 1.0.0+      | ""             |             |
| ogl\_563a95f1                                | 1.0.0+      | ""             |             |
| ogl\_573823                                  | 1.0.0+      | ""             |             |
| ogl\_58027529                                | 1.0.0+      | ""             |             |
| ogl\_5d2d63                                  | 1.0.0+      | ""             |             |
| ogl\_5f7e3b                                  | 1.0.0+      | ""             |             |
| ogl\_60461793                                | 1.0.0+      | ""             |             |
| ogl\_60d355                                  | 1.0.0+      | ""             |             |
| ogl\_616627aa                                | 1.0.0+      | ""             |             |
| ogl\_62317182                                | 1.0.0+      | ""             |             |
| ogl\_6253fa2e                                | 1.0.0+      | ""             |             |
| ogl\_64100768                                | 1.0.0+      | ""             |             |
| ogl\_64100769                                | 1.0.0+      | ""             |             |
| ogl\_64100770                                | 1.0.0+      | ""             |             |
| ogl\_647395                                  | 1.0.0+      | ""             |             |
| ogl\_66543234                                | 1.0.0+      | ""             |             |
| ogl\_67674763                                | 1.0.0+      | ""             |             |
| ogl\_67739784                                | 1.0.0+      | ""             |             |
| ogl\_68fb9c                                  | 1.0.0+      | ""             |             |
| ogl\_69801276                                | 1.0.0+      | ""             |             |
| ogl\_6af9fa2f                                | 1.0.0+      | ""             |             |
| ogl\_6af9fa3f                                | 1.0.0+      | ""             |             |
| ogl\_6af9fa4f                                | 1.0.0+      | ""             |             |
| ogl\_6bd8c7                                  | 1.0.0+      | ""             |             |
| ogl\_6c7691                                  | 1.0.0+      | ""             |             |
| ogl\_6d4296ce                                | 1.0.0+      | ""             |             |
| ogl\_6dd7e7                                  | 1.0.0+      | ""             |             |
| ogl\_6dd7e8                                  | 1.0.0+      | ""             |             |
| ogl\_6fe11ec1                                | 1.0.0+      | ""             |             |
| ogl\_716511763                               | 1.0.0+      | ""             |             |
| ogl\_72504593                                | 1.0.0+      | ""             |             |
| ogl\_73304097                                | 1.0.0+      | ""             |             |
| ogl\_73314098                                | 1.0.0+      | ""             |             |
| ogl\_74095213                                | 1.0.0+      | ""             |             |
| ogl\_74095213a                               | 1.0.0+      | ""             |             |
| ogl\_74095213b                               | 1.0.0+      | ""             |             |
| ogl\_74095214                                | 1.0.0+      | ""             |             |
| ogl\_748f9649                                | 1.0.0+      | ""             |             |
| ogl\_75494732                                | 1.0.0+      | ""             |             |
| ogl\_78452832                                | 1.0.0+      | ""             |             |
| ogl\_784561                                  | 1.0.0+      | ""             |             |
| ogl\_78e16b9c                                | 1.0.0+      | ""             |             |
| ogl\_79251225                                | 1.0.0+      | ""             |             |
| ogl\_7c128b                                  | 1.0.0+      | ""             |             |
| ogl\_7ccd93                                  | 1.0.0+      | ""             |             |
| ogl\_7df8d1                                  | 1.0.0+      | ""             |             |
| ogl\_800c2310                                | 1.0.0+      | ""             |             |
| ogl\_80546710                                | 1.0.0+      | ""             |             |
| ogl\_80772310                                | 1.0.0+      | ""             |             |
| ogl\_808ee280                                | 1.0.0+      | ""             |             |
| ogl\_81131154                                | 1.0.0+      | ""             |             |
| ogl\_81274457                                | 1.0.0+      | ""             |             |
| ogl\_8292291f                                | 1.0.0+      | ""             |             |
| ogl\_83498426                                | 1.0.0+      | ""             |             |
| ogl\_84993794                                | 1.0.0+      | ""             |             |
| ogl\_84995585                                | 1.0.0+      | ""             |             |
| ogl\_84a0a0                                  | 1.0.0+      | ""             |             |
| ogl\_852142                                  | 1.0.0+      | ""             |             |
| ogl\_85612309                                | 1.0.0+      | ""             |             |
| ogl\_85612310                                | 1.0.0+      | ""             |             |
| ogl\_85612311                                | 1.0.0+      | ""             |             |
| ogl\_85612312                                | 1.0.0+      | ""             |             |
| ogl\_8623ff27                                | 1.0.0+      | ""             |             |
| ogl\_87364952                                | 1.0.0+      | ""             |             |
| ogl\_87f6275666                              | 1.0.0+      | ""             |             |
| ogl\_886748                                  | 1.0.0+      | ""             |             |
| ogl\_89894423                                | 1.0.0+      | ""             |             |
| ogl\_8ad8a75                                 | 1.0.0+      | ""             |             |
| ogl\_8ad8ad00                                | 1.0.0+      | ""             |             |
| ogl\_8bb815                                  | 1.0.0+      | ""             |             |
| ogl\_8bb817                                  | 1.0.0+      | ""             |             |
| ogl\_8bb818                                  | 1.0.0+      | ""             |             |
| ogl\_8bb819                                  | 1.0.0+      | ""             |             |
| ogl\_8e640cd1                                | 1.0.0+      | ""             |             |
| ogl\_8f34971a                                | 1.0.0+      | ""             |             |
| ogl\_8f773984                                | 1.0.0+      | ""             |             |
| ogl\_8f7a7d                                  | 1.0.0+      | ""             |             |
| ogl\_902486209                               | 1.0.0+      | ""             |             |
| ogl\_90482571                                | 1.0.0+      | ""             |             |
| ogl\_91214835                                | 1.0.0+      | ""             |             |
| ogl\_912848290                               | 1.0.0+      | ""             |             |
| ogl\_915e56                                  | 1.0.0+      | ""             |             |
| ogl\_92179063                                | 1.0.0+      | ""             |             |
| ogl\_92179064                                | 1.0.0+      | ""             |             |
| ogl\_92179065                                | 1.0.0+      | ""             |             |
| ogl\_92179066                                | 1.0.0+      | ""             |             |
| ogl\_92350358                                | 1.0.0+      | ""             |             |
| ogl\_92809063                                | 1.0.0+      | ""             |             |
| ogl\_92809064                                | 1.0.0+      | ""             |             |
| ogl\_92809065                                | 1.0.0+      | ""             |             |
| ogl\_92809066                                | 1.0.0+      | ""             |             |
| ogl\_92920143                                | 1.0.0+      | ""             |             |
| ogl\_93a89b12                                | 1.0.0+      | ""             |             |
| ogl\_93a89c0b                                | 1.0.0+      | ""             |             |
| ogl\_94812574                                | 1.0.0+      | ""             |             |
| ogl\_95282304                                | 1.0.0+      | ""             |             |
| ogl\_95394027                                | 1.0.0+      | ""             |             |
| ogl\_959b1f                                  | 1.0.0+      | ""             |             |
| ogl\_9638af                                  | 1.0.0+      | ""             |             |
| ogl\_96fd59                                  | 1.0.0+      | ""             |             |
| ogl\_97f6275666                              | 1.0.0+      | ""             |             |
| ogl\_97f6275667                              | 1.0.0+      | ""             |             |
| ogl\_97f6275668                              | 1.0.0+      | ""             |             |
| ogl\_97f6275669                              | 1.0.0+      | ""             |             |
| ogl\_97f627566a                              | 1.0.0+      | ""             |             |
| ogl\_97f627566b                              | 1.0.0+      | ""             |             |
| ogl\_97f627566d                              | 1.0.0+      | ""             |             |
| ogl\_97f627566e                              | 1.0.0+      | ""             |             |
| ogl\_97f627566f                              | 1.0.0+      | ""             |             |
| ogl\_97f6275670                              | 1.0.0+      | ""             |             |
| ogl\_97f6275671                              | 1.0.0+      | ""             |             |
| ogl\_97f727566e                              | 1.0.0+      | ""             |             |
| ogl\_98480775                                | 1.0.0+      | ""             |             |
| ogl\_98480776                                | 1.0.0+      | ""             |             |
| ogl\_98480777                                | 1.0.0+      | ""             |             |
| ogl\_992431                                  | 1.0.0+      | ""             |             |
| ogl\_9aa29065                                | 1.0.0+      | ""             |             |
| ogl\_9af32c                                  | 1.0.0+      | ""             |             |
| ogl\_9af32d                                  | 1.0.0+      | ""             |             |
| ogl\_9af32e                                  | 1.0.0+      | ""             |             |
| ogl\_9c108b71                                | 1.0.0+      | ""             |             |
| ogl\_9f279065                                | 1.0.0+      | ""             |             |
| ogl\_a01bc728                                | 1.0.0+      | ""             |             |
| ogl\_a13b46c80                               | 1.0.0+      | ""             |             |
| ogl\_a22eb0                                  | 1.0.0+      | ""             |             |
| ogl\_a2fb451e                                | 1.0.0+      | ""             |             |
| ogl\_a3456abe                                | 1.0.0+      | ""             |             |
| ogl\_a7044887                                | 1.0.0+      | ""             |             |
| ogl\_a7149200                                | 1.0.0+      | ""             |             |
| ogl\_a766215670                              | 1.0.0+      | ""             |             |
| ogl\_aalinegamma                             | 1.0.0+      | ""             |             |
| ogl\_aalinetweaks                            | 1.0.0+      | ""             |             |
| ogl\_ab34ee01                                | 1.0.0+      | ""             |             |
| ogl\_ab34ee02                                | 1.0.0+      | ""             |             |
| ogl\_ab34ee03                                | 1.0.0+      | ""             |             |
| ogl\_ac0274                                  | 1.0.0+      | ""             |             |
| ogl\_af73c63e                                | 1.0.0+      | ""             |             |
| ogl\_af73c63f                                | 1.0.0+      | ""             |             |
| ogl\_af9927                                  | 1.0.0+      | ""             |             |
| ogl\_afoverride                              | 1.0.0+      | ""             |             |
| ogl\_allocdeviceevents                       | 1.0.0+      | ""             |             |
| ogl\_app\_softimage                          | 1.0.0+      | ""             |             |
| ogl\_app\_supportbits2                       | 1.0.0+      | ""             |             |
| ogl\_applicationkey                          | 1.0.0+      | ""             |             |
| ogl\_appreturnonlybasicglsltype              | 1.0.0+      | ""             |             |
| ogl\_assumetextureismipmappedatcreation      | 1.0.0+      | ""             |             |
| ogl\_b1fb0f01                                | 1.0.0+      | ""             |             |
| ogl\_b3edd5                                  | 1.0.0+      | ""             |             |
| ogl\_b40d9e03d                               | 1.0.0+      | ""             |             |
| ogl\_b7f6275666                              | 1.0.0+      | ""             |             |
| ogl\_b812c1                                  | 1.0.0+      | ""             |             |
| ogl\_ba14ba1a                                | 1.0.0+      | ""             |             |
| ogl\_ba14ba1b                                | 1.0.0+      | ""             |             |
| ogl\_bd7559                                  | 1.0.0+      | ""             |             |
| ogl\_bd755a                                  | 1.0.0+      | ""             |             |
| ogl\_bd755c                                  | 1.0.0+      | ""             |             |
| ogl\_bd755d                                  | 1.0.0+      | ""             |             |
| ogl\_be58bb                                  | 1.0.0+      | ""             |             |
| ogl\_be92cb                                  | 1.0.0+      | ""             |             |
| ogl\_beefcba3                                | 1.0.0+      | ""             |             |
| ogl\_beefcba4                                | 1.0.0+      | ""             |             |
| ogl\_c023777f                                | 1.0.0+      | ""             |             |
| ogl\_c09dc8                                  | 1.0.0+      | ""             |             |
| ogl\_c0d340                                  | 1.0.0+      | ""             |             |
| ogl\_c2ff374c                                | 1.0.0+      | ""             |             |
| ogl\_c5e9d7a3                                | 1.0.0+      | ""             |             |
| ogl\_c5e9d7a4                                | 1.0.0+      | ""             |             |
| ogl\_c5e9d7b4                                | 1.0.0+      | ""             |             |
| ogl\_c618f9                                  | 1.0.0+      | ""             |             |
| ogl\_ca345840                                | 1.0.0+      | ""             |             |
| ogl\_cachedisable                            | 1.0.0+      | ""             |             |
| ogl\_channelpriorityoverride                 | 1.0.0+      | ""             |             |
| ogl\_cleardatastorevidmem                    | 1.0.0+      | ""             |             |
| ogl\_cmdbufmemoryspaceenables                | 1.0.0+      | ""             |             |
| ogl\_cmdbufminwords                          | 1.0.0+      | ""             |             |
| ogl\_cmdbufsizewords                         | 1.0.0+      | ""             |             |
| ogl\_conformantblitframebufferscissor        | 1.0.0+      | ""             |             |
| ogl\_conformantincompletetextures            | 1.0.0+      | ""             |             |
| ogl\_copybuffermethod                        | 1.0.0+      | ""             |             |
| ogl\_cubemapaniso                            | 1.0.0+      | ""             |             |
| ogl\_cubemapfiltering                        | 1.0.0+      | ""             |             |
| ogl\_d0e9a4d7                                | 1.0.0+      | ""             |             |
| ogl\_d13733f12                               | 1.0.0+      | ""             |             |
| ogl\_d1b399                                  | 1.0.0+      | ""             |             |
| ogl\_d2983c32                                | 1.0.0+      | ""             |             |
| ogl\_d2983c33                                | 1.0.0+      | ""             |             |
| ogl\_d2e71b                                  | 1.0.0+      | ""             |             |
| ogl\_d377dc                                  | 1.0.0+      | ""             |             |
| ogl\_d377dd                                  | 1.0.0+      | ""             |             |
| ogl\_d489f4                                  | 1.0.0+      | ""             |             |
| ogl\_d4bce1                                  | 1.0.0+      | ""             |             |
| ogl\_d518cb                                  | 1.0.0+      | ""             |             |
| ogl\_d518cd                                  | 1.0.0+      | ""             |             |
| ogl\_d518ce                                  | 1.0.0+      | ""             |             |
| ogl\_d518d0                                  | 1.0.0+      | ""             |             |
| ogl\_d518d1                                  | 1.0.0+      | ""             |             |
| ogl\_d518d2                                  | 1.0.0+      | ""             |             |
| ogl\_d518d3                                  | 1.0.0+      | ""             |             |
| ogl\_d518d4                                  | 1.0.0+      | ""             |             |
| ogl\_d518d5                                  | 1.0.0+      | ""             |             |
| ogl\_d59eda                                  | 1.0.0+      | ""             |             |
| ogl\_d83cbd                                  | 1.0.0+      | ""             |             |
| ogl\_d8e777                                  | 1.0.0+      | ""             |             |
| ogl\_debug\_level                            | 1.0.0+      | ""             |             |
| ogl\_debug\_mask                             | 1.0.0+      | ""             |             |
| ogl\_debug\_options                          | 1.0.0+      | ""             |             |
| ogl\_devshmpageableallocations               | 1.0.0+      | ""             |             |
| ogl\_df1f9812                                | 1.0.0+      | ""             |             |
| ogl\_df783c                                  | 1.0.0+      | ""             |             |
| ogl\_diagenable                              | 1.0.0+      | ""             |             |
| ogl\_disallowcemask                          | 1.0.0+      | ""             |             |
| ogl\_disallowz16                             | 1.0.0+      | ""             |             |
| ogl\_dlmemoryspaceenables                    | 1.0.0+      | ""             |             |
| ogl\_e0bfec                                  | 1.0.0+      | ""             |             |
| ogl\_e433456d                                | 1.0.0+      | ""             |             |
| ogl\_e435563f                                | 1.0.0+      | ""             |             |
| ogl\_e4cd9c                                  | 1.0.0+      | ""             |             |
| ogl\_e5c972                                  | 1.0.0+      | ""             |             |
| ogl\_e639ef                                  | 1.0.0+      | ""             |             |
| ogl\_e802af                                  | 1.0.0+      | ""             |             |
| ogl\_eae964                                  | 1.0.0+      | ""             |             |
| ogl\_earlytexturehwallocation                | 1.0.0+      | ""             |             |
| ogl\_eb92a3                                  | 1.0.0+      | ""             |             |
| ogl\_ebca56                                  | 1.0.0+      | ""             |             |
| ogl\_expert\_detail\_level                   | 1.0.0+      | ""             |             |
| ogl\_expert\_output\_mask                    | 1.0.0+      | ""             |             |
| ogl\_expert\_report\_mask                    | 1.0.0+      | ""             |             |
| ogl\_extensionstringnvarch                   | 1.0.0+      | ""             |             |
| ogl\_extensionstringversion                  | 1.0.0+      | ""             |             |
| ogl\_f00f1938                                | 1.0.0+      | ""             |             |
| ogl\_f10736                                  | 1.0.0+      | ""             |             |
| ogl\_f1846870                                | 1.0.0+      | ""             |             |
| ogl\_f33bc370                                | 1.0.0+      | ""             |             |
| ogl\_f392a874                                | 1.0.0+      | ""             |             |
| ogl\_f49ae8                                  | 1.0.0+      | ""             |             |
| ogl\_fa345cce                                | 1.0.0+      | ""             |             |
| ogl\_fa35cc4                                 | 1.0.0+      | ""             |             |
| ogl\_faa14a                                  | 1.0.0+      | ""             |             |
| ogl\_faf8a723                                | 1.0.0+      | ""             |             |
| ogl\_fastgs                                  | 1.0.0+      | ""             |             |
| ogl\_fbf4ac45                                | 1.0.0+      | ""             |             |
| ogl\_fbo\_blit\_ignore\_srgb                 | 1.0.0+      | ""             |             |
| ogl\_fc64c7                                  | 1.0.0+      | ""             |             |
| ogl\_ff54ec97                                | 1.0.0+      | ""             |             |
| ogl\_ff54ec98                                | 1.0.0+      | ""             |             |
| ogl\_forceexitprocessdetach                  | 1.0.0+      | ""             |             |
| ogl\_forcerequestedesversion                 | 1.0.0+      | ""             |             |
| ogl\_glsynctovblank                          | 1.0.0+      | ""             |             |
| ogl\_gvitimeoutcontrol                       | 1.0.0+      | ""             |             |
| ogl\_hcctrl                                  | 1.0.0+      | ""             |             |
| ogl\_hwstate\_per\_ctx                       | 1.0.0+      | ""             |             |
| ogl\_machinecachelimit                       | 1.0.0+      | ""             |             |
| ogl\_maxframesallowed                        | 1.0.0+      | ""             |             |
| ogl\_memmgrcachedalloclimit                  | 1.0.0+      | ""             |             |
| ogl\_memmgrcachedalloclimitratio             | 1.0.0+      | ""             |             |
| ogl\_memmgrsysheapalloclimit                 | 1.0.0+      | ""             |             |
| ogl\_memmgrsysheapalloclimitratio            | 1.0.0+      | ""             |             |
| ogl\_memmgrvidheapalloclimit                 | 1.0.0+      | ""             |             |
| ogl\_mosaic\_clip\_to\_subdev                | 1.0.0+      | ""             |             |
| ogl\_mosaic\_clip\_to\_subdev\_h\_overlap    | 1.0.0+      | ""             |             |
| ogl\_mosaic\_clip\_to\_subdev\_v\_overlap    | 1.0.0+      | ""             |             |
| ogl\_overlaymergeblittimerms                 | 1.0.0+      | ""             |             |
| ogl\_perfmon\_mode                           | 1.0.0+      | ""             |             |
| ogl\_pixbar\_mode                            | 1.0.0+      | ""             |             |
| ogl\_qualityenhancements                     | 1.0.0+      | ""             |             |
| ogl\_r27s18q28                               | 1.0.0+      | ""             |             |
| ogl\_r2d7c1d8                                | 1.0.0+      | ""             |             |
| ogl\_renderer                                | 1.0.0+      | ""             |             |
| ogl\_renderqualityflags                      | 1.0.0+      | ""             |             |
| ogl\_s3tcquality                             | 1.0.0+      | ""             |             |
| ogl\_shader\_disk\_cache\_path               | 1.0.0+      | ""             |             |
| ogl\_shader\_disk\_cache\_read\_only         | 1.0.0+      | ""             |             |
| ogl\_shaderatomics                           | 1.0.0+      | ""             |             |
| ogl\_shadercacheinitsize                     | 1.0.0+      | ""             |             |
| ogl\_shaderobjects                           | 1.0.0+      | ""             |             |
| ogl\_shaderportabilitywarnings               | 1.0.0+      | ""             |             |
| ogl\_shaderwarningsaserrors                  | 1.0.0+      | ""             |             |
| ogl\_skiptexturehostcopies                   | 1.0.0+      | ""             |             |
| ogl\_sli\_dli\_control                       | 1.0.0+      | ""             |             |
| ogl\_sparsetexture                           | 1.0.0+      | ""             |             |
| ogl\_spinlooptimeout                         | 1.0.0+      | ""             |             |
| ogl\_sync\_to\_vblank                        | 1.0.0+      | ""             |             |
| ogl\_sysheapreuseratio                       | 1.0.0+      | ""             |             |
| ogl\_sysmemtexturepromotion                  | 1.0.0+      | ""             |             |
| ogl\_targetflushcount                        | 1.0.0+      | ""             |             |
| ogl\_tearingfreeswappresent                  | 1.0.0+      | ""             |             |
| ogl\_texclampbehavior                        | 1.0.0+      | ""             |             |
| ogl\_texlodbias                              | 1.0.0+      | ""             |             |
| ogl\_texmemoryspaceenables                   | 1.0.0+      | ""             |             |
| ogl\_textureprecache                         | 1.0.0+      | ""             |             |
| ogl\_threadcontrol                           | 1.0.0+      | ""             |             |
| ogl\_threadcontrol2                          | 1.0.0+      | ""             |             |
| ogl\_usegvievents                            | 1.0.0+      | ""             |             |
| ogl\_vbomemoryspaceenables                   | 1.0.0+      | ""             |             |
| ogl\_vertexlimit                             | 1.0.0+      | ""             |             |
| ogl\_vidheapreuseratio                       | 1.0.0+      | ""             |             |
| ogl\_vpipe                                   | 1.0.0+      | ""             |             |
| ogl\_vpipeformatbloatlimit                   | 1.0.0+      | ""             |             |
| ogl\_wglmessageboxonabort                    | 1.0.0+      | ""             |             |
| ogl\_writeinfolog                            | 1.0.0+      | ""             |             |
| ogl\_writeprogramobjectassembly              | 1.0.0+      | ""             |             |
| ogl\_writeprogramobjectsource                | 1.0.0+      | ""             |             |
| ogl\_xnvadapterpresent                       | 1.0.0+      | ""             |             |
| ogl\_yield                                   | 1.0.0+      | ""             |             |
| ogl\_yieldfunction                           | 1.0.0+      | ""             |             |
| ogl\_yieldfunctionfast                       | 1.0.0+      | ""             |             |
| ogl\_yieldfunctionslow                       | 1.0.0+      | ""             |             |
| ogl\_yieldfunctionwaitfordcqueue             | 1.0.0+      | ""             |             |
| ogl\_yieldfunctionwaitforframe               | 1.0.0+      | ""             |             |
| ogl\_yieldfunctionwaitforgpu                 | 1.0.0+      | ""             |             |
| ogl\_zbctableaddhysteresis                   | 1.0.0+      | ""             |             |
| overlaymergeblittimerms                      | 1.0.0+      | ""             |             |
| perfmon\_mode                                | 1.0.0+      | ""             |             |
| persist.sys.display.resolution               | 1.0.0+      | ""             |             |
| persist.tegra.composite.fallb                | 1.0.0+      | ""             |             |
| persist.tegra.composite.policy               | 1.0.0+      | ""             |             |
| persist.tegra.composite.range                | 1.0.0+      | ""             |             |
| persist.tegra.compositor                     | 1.0.0+      | ""             |             |
| persist.tegra.compositor.virt                | 1.0.0+      | ""             |             |
| persist.tegra.compression                    | 1.0.0+      | ""             |             |
| persist.tegra.cursor.enable                  | 1.0.0+      | ""             |             |
| persist.tegra.didim.enable                   | 1.0.0+      | ""             |             |
| persist.tegra.didim.normal                   | 1.0.0+      | ""             |             |
| persist.tegra.didim.video                    | 1.0.0+      | ""             |             |
| persist.tegra.disp.heads                     | 1.0.0+      | ""             |             |
| persist.tegra.gamma\_correction              | 1.0.0+      | ""             |             |
| persist.tegra.gpu\_mapping\_cache            | 1.0.0+      | ""             |             |
| persist.tegra.grlayout                       | 1.0.0+      | ""             |             |
| persist.tegra.hdmi.2020.10                   | 1.0.0+      | ""             |             |
| persist.tegra.hdmi.2020.fake                 | 1.0.0+      | ""             |             |
| persist.tegra.hdmi.2020.force                | 1.0.0+      | ""             |             |
| persist.tegra.hdmi.autorotate                | 1.0.0+      | ""             |             |
| persist.tegra.hdmi.hdr.fake                  | 1.0.0+      | ""             |             |
| persist.tegra.hdmi.ignore\_ratio             | 1.0.0+      | ""             |             |
| persist.tegra.hdmi.limit.clock               | 1.0.0+      | ""             |             |
| persist.tegra.hdmi.only\_16\_9               | 1.0.0+      | ""             |             |
| persist.tegra.hdmi.range                     | 1.0.0+      | ""             |             |
| persist.tegra.hdmi.resolution                | 1.0.0+      | ""             |             |
| persist.tegra.hdmi.underscan                 | 1.0.0+      | ""             |             |
| persist.tegra.hdmi.yuv.422                   | 1.0.0+      | ""             |             |
| persist.tegra.hdmi.yuv.444                   | 1.0.0+      | ""             |             |
| persist.tegra.hdmi.yuv.enable                | 1.0.0+      | ""             |             |
| persist.tegra.hdmi.yuv.force                 | 1.0.0+      | ""             |             |
| persist.tegra.hwc.nvdc                       | 1.0.0+      | ""             |             |
| persist.tegra.idle.minimum\_fps              | 1.0.0+      | ""             |             |
| persist.tegra.panel.rotation                 | 1.0.0+      | ""             |             |
| persist.tegra.scan\_props                    | 1.0.0+      | ""             |             |
| persist.tegra.stb.mode                       | 1.0.0+      | ""             |             |
| persist.tegra.zbc\_override                  | 1.0.0+      | ""             |             |
| pixbar\_mode                                 | 1.0.0+      | ""             |             |
| qualityenhancements                          | 1.0.0+      | ""             |             |
| r27s18q28                                    | 1.0.0+      | ""             |             |
| r2d7c1d8                                     | 1.0.0+      | ""             |             |
| renderer                                     | 1.0.0+      | ""             |             |
| renderqualityflags                           | 1.0.0+      | ""             |             |
| rmos\_debug\_mask                            | 1.0.0+      | ""             |             |
| rmos\_set\_production\_mode                  | 1.0.0+      | ""             |             |
| s3tcquality                                  | 1.0.0+      | ""             |             |
| shader\_disk\_cache\_path                    | 1.0.0+      | ""             |             |
| shader\_disk\_cache\_read\_only              | 1.0.0+      | ""             |             |
| shaderatomics                                | 1.0.0+      | ""             |             |
| shadercacheinitsize                          | 1.0.0+      | ""             |             |
| shaderobjects                                | 1.0.0+      | ""             |             |
| shaderportabilitywarnings                    | 1.0.0+      | ""             |             |
| shaderwarningsaserrors                       | 1.0.0+      | ""             |             |
| skiptexturehostcopies                        | 1.0.0+      | ""             |             |
| sli\_dli\_control                            | 1.0.0+      | ""             |             |
| sparsetexture                                | 1.0.0+      | ""             |             |
| spinlooptimeout                              | 1.0.0+      | ""             |             |
| sync\_to\_vblank                             | 1.0.0+      | ""             |             |
| sysheapreuseratio                            | 1.0.0+      | ""             |             |
| sysmemtexturepromotion                       | 1.0.0+      | ""             |             |
| targetflushcount                             | 1.0.0+      | ""             |             |
| tearingfreeswappresent                       | 1.0.0+      | ""             |             |
| tegra.refresh                                | 1.0.0+      | ""             |             |
| texclampbehavior                             | 1.0.0+      | ""             |             |
| texlodbias                                   | 1.0.0+      | ""             |             |
| texmemoryspaceenables                        | 1.0.0+      | ""             |             |
| textureprecache                              | 1.0.0+      | ""             |             |
| threadcontrol                                | 1.0.0+      | ""             |             |
| threadcontrol2                               | 1.0.0+      | ""             |             |
| tvmr.avp.logs                                | 1.0.0+      | ""             |             |
| tvmr.buffer.logs                             | 1.0.0+      | ""             |             |
| tvmr.dec.prof                                | 1.0.0+      | ""             |             |
| tvmr.deint.logs                              | 1.0.0+      | ""             |             |
| tvmr.dfs.logs                                | 1.0.0+      | ""             |             |
| tvmr.ffprof.logs                             | 1.0.0+      | ""             |             |
| tvmr.game.stream                             | 1.0.0+      | ""             |             |
| tvmr.general.logs                            | 1.0.0+      | ""             |             |
| tvmr.input.dump                              | 1.0.0+      | ""             |             |
| tvmr.seeking.logs                            | 1.0.0+      | ""             |             |
| tvmr.ts\_pulldown                            | 3.0.0+      | ""             |             |
| usegvievents                                 | 1.0.0+      | ""             |             |
| vbomemoryspaceenables                        | 1.0.0+      | ""             |             |
| vcc\_debug\_ip                               | 1.0.0+      | ""             |             |
| vcc\_verbose\_level                          | 1.0.0+      | ""             |             |
| vertexlimit                                  | 1.0.0+      | ""             |             |
| viccomposer.filter                           | 1.0.0+      | ""             |             |
| viccomposer.highpriority                     | 7.0.0-7.0.1 | ""             |             |
| 8.0.0-8.1.0                                  | "1"         |                |             |
| viccomposer.normalpriority                   | 9.0.0+      | ""             |             |
| videostats-enable                            | 1.0.0+      | ""             |             |
| vidheapreuseratio                            | 1.0.0+      | ""             |             |
| vpipe                                        | 1.0.0+      | ""             |             |
| vpipeformatbloatlimit                        | 1.0.0+      | ""             |             |
| wglmessageboxonabort                         | 1.0.0+      | ""             |             |
| writeinfolog                                 | 1.0.0+      | ""             |             |
| writeprogramobjectassembly                   | 1.0.0+      | ""             |             |
| writeprogramobjectsource                     | 1.0.0+      | ""             |             |
| xnvadapterpresent                            | 1.0.0+      | ""             |             |
| yield                                        | 1.0.0+      | ""             |             |
| yieldfunction                                | 1.0.0+      | ""             |             |
| yieldfunctionfast                            | 1.0.0+      | ""             |             |
| yieldfunctionslow                            | 1.0.0+      | ""             |             |
| yieldfunctionwaitfordcqueue                  | 1.0.0+      | ""             |             |
| yieldfunctionwaitforframe                    | 1.0.0+      | ""             |             |
| yieldfunctionwaitforgpu                      | 1.0.0+      | ""             |             |
| zbctableaddhysteresis                        | 1.0.0+      | ""             |             |

# olsc

| Name                                                        | Versions    | Default Values     | Description |
| ----------------------------------------------------------- | ----------- | ------------------ | ----------- |
| autonomy\_registration\_interval\_seconds                   | 6.0.0+      | 46800 (0xb6d0)     |             |
| default\_auto\_upload\_global\_setting                      | 6.0.0+      | true               |             |
| is\_global\_transfer\_task\_autonomy\_registration\_enabled | 6.0.0+      | true               |             |
| is\_on\_event\_transfer\_task\_registration\_enabled        | 6.0.0+      | true               |             |
| is\_periodic\_transfer\_task\_registration\_enabled         | 6.0.0+      | true               |             |
| long\_sleep\_detection\_seconds                             | 8.0.0+      | 1468800 (0x166980) |             |
| network\_connection\_polling\_interval\_seconds             | 7.0.0+      | 10800 (0x2a30)     |             |
| network\_service\_license\_info\_cache\_expiration\_seconds | 8.0.0+      | 457200 (0x6f9f0)   |             |
| network\_trouble\_detection\_span\_seconds                  | 7.0.0+      | 60 (0x3c)          |             |
| network\_trouble\_detection\_threshold                      | 7.0.0+      | 3 (0x3)            |             |
| postponed\_transfer\_task\_processing\_interval\_seconds    | 6.0.0+      | 46800 (0xb6d0)     |             |
| retry\_backoff\_scale                                       | 6.0.0+      | 10 (0xa)           |             |
| retry\_backoff\_unit\_seconds                               | 6.0.0+      | 127 (0x7f)         |             |
| retry\_lost\_connection\_interval\_seconds                  | 6.0.0-6.2.0 | 60 (0x3c)          |             |
| retry\_offset\_seconds                                      | 6.0.0+      | 600 (0x258)        |             |

# omm

| Name                                     | Versions   | Default Values | Description |
| ---------------------------------------- | ---------- | -------------- | ----------- |
| backlight\_off\_ms\_on\_handheld\_switch | 1.0.0+     | 150 (0x96)     |             |
| charging\_sign\_ms                       | 1.0.0+     | 3000 (0xbb8)   |             |
| hdcp\_failed\_emulation                  | 4.0.0+     | false          |             |
| low\_battery\_sign\_ms                   | 1.0.0+     | 3000 (0xbb8)   |             |
| operation\_mode\_policy                  | 1.0.0+     | "auto"         |             |
| sign\_fade\_in\_ms                       | 1.0.0+     | 0 (0x0)        |             |
| sign\_fade\_out\_ms                      | 1.0.0+     | 400 (0x190)    |             |
| sign\_wait\_layer\_visible\_ms           | 1.0.0+     | 100 (0x64)     |             |
| sleep\_fade\_in\_ms                      | 1.0.0+     | 50 (0x32)      |             |
| sleep\_fade\_out\_ms                     | 1.0.0      | 200 (0xc8)     |             |
| 2.0.0+                                   | 100 (0x64) |                |             |
| sleep\_on\_ac\_ok\_boot                  | 3.0.0+     | true           |             |
| startup\_fade\_in\_ms                    | 1.0.0+     | 200 (0xc8)     |             |
| startup\_fade\_out\_ms                   | 1.0.0+     | 400 (0x190)    |             |

# pcm

| Name   | Versions | Default Values | Description |
| ------ | -------- | -------------- | ----------- |
| enable | 2.0.0+   | true           |             |

# pctl

| Name                                  | Versions | Default Values | Description |
| ------------------------------------- | -------- | -------------- | ----------- |
| intermittent\_task\_interval\_seconds | 2.0.0+   | 21600 (0x5460) |             |
| post\_event\_interval\_seconds        | 6.0.0+   | 600 (0x258)    |             |

# pdm

| Name                              | Versions | Default Values | Description |
| --------------------------------- | -------- | -------------- | ----------- |
| force\_migrate\_account\_database | 4.0.0+   | false          |             |
| is\_production                    | 5.0.0+   | true           |             |
| save\_playlog                     | 1.0.0+   | true           |             |

# prepo

| Name                                   | Versions    | Default Values  | Description |
| -------------------------------------- | ----------- | --------------- | ----------- |
| background\_processing                 | 2.0.0+      | true            |             |
| buffer\_usage\_for\_immediately\_flush | 7.0.0+      | 50 (0x32)       |             |
| devmenu\_prepo\_page\_view             | 1.0.0+      | false           |             |
| output\_save\_log                      | 5.0.0-7.0.1 | false           |             |
| report\_data\_buffer\_time             | 7.0.0+      | 10 (0xa)        |             |
| save\_log\_level                       | 8.0.0+      | 0 (0x0)         |             |
| save\_system\_report                   | 7.0.0+      | true            |             |
| statistics\_post\_interval             | 6.0.0+      | 86400 (0x15180) |             |
| statistics\_save\_interval\_min        | 5.0.0-5.1.0 | 10 (0xa)        |             |
| 6.0.0+                                 | 60 (0x3c)   |                 |             |
| transmission\_interval\_in\_sleep      | 6.0.0+      | 10800 (0x2a30)  |             |
| transmission\_interval\_min            | 3.0.0+      | 10 (0xa)        |             |
| transmission\_retry\_interval          | 3.0.0-5.1.0 | 3600 (0xe10)    |             |
| transmission\_retry\_interval\_max     | 6.0.0+      | 7200 (0x1c20)   |             |
| transmission\_retry\_interval\_min     | 6.0.0+      | 3600 (0xe10)    |             |

# productinfo

| Name           | Versions | Default Values    | Description |
| -------------- | -------- | ----------------- | ----------- |
| cec\_osd\_name | 1.0.0+   | "NintendoSwitch"  |             |
| product\_name  | 1.0.0+   | "Nintendo Switch" |             |
| vendor\_name   | 4.0.0+   | "Nintendo"        |             |

# psm

| Name                                  | Versions         | Default Values | Description |
| ------------------------------------- | ---------------- | -------------- | ----------- |
| charge\_current\_limit\_milli\_ampere | 4.0.0-6.2.0      | 2048 (0x800)   |             |
| 7.0.0+                                | \-1 (0xffffffff) |                |             |
| evaluation\_log\_enabled              | 3.0.0+           | false          |             |

# push\_notification

| Name                         | Versions | Default Values | Description |
| ---------------------------- | -------- | -------------- | ----------- |
| nup\_notification\_topic\_id | 1.0.0    | "nx\_nup"      |             |
| retry\_interval              | 1.0.0    | 60 (0x3c)      |             |
| subscribe\_nup\_notification | 1.0.0    | true           |             |

# ro

| Name                   | Versions | Default Values | Description |
| ---------------------- | -------- | -------------- | ----------- |
| ease\_nro\_restriction | 3.0.0+   | false          |             |

# settings\_debug

| Name                                | Versions | Default Values | Description |
| ----------------------------------- | -------- | -------------- | ----------- |
| is\_debug\_mode\_enabled            | 1.0.0+   | false          |             |
| is\_hdmi\_cec\_suppression\_enabled | 4.0.0+   | false          |             |

# ssl.test

This class does not exist on retail firmware.

| Name                  | Versions | Default Values | Description                                                                                                                                                       |
| --------------------- | -------- | -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| initialize\_for\_test |          |                | Used by [SSL](SSL%20services.md "wikilink") when an input param is a certain value, however this func is never called with that value (on newer system-versions). |

# sio\_hoag

This class does not exist before 9.0.0.

| Name                                    | Versions | Default Values | Description |
| --------------------------------------- | -------- | -------------- | ----------- |
| mcu\_reset\_on\_command\_retry\_enabled | 9.0.0+   | true           |             |

# snap\_shot\_dump

| Name             | Versions | Default Values                           | Description |
| ---------------- | -------- | ---------------------------------------- | ----------- |
| auto\_dump       | 1.0.0+   | false                                    |             |
| full\_dump       | 1.0.0+   | false                                    |             |
| output\_all\_log | 6.0.0+   | false                                    |             |
| output\_dir      | 1.0.0+   | "%USERPROFILE%/Documents/Nintendo/NXDMP" |             |

# systemconfig

| Name           | Versions | Default Values | Description |
| -------------- | -------- | -------------- | ----------- |
| exhivision     | 1.0.0+   | false          |             |
| field\_testing | 1.0.0+   | false          |             |

# systempowerstate

| Name                                            | Versions | Default Values | Description |
| ----------------------------------------------- | -------- | -------------- | ----------- |
| always\_reboot                                  | 1.0.0+   | false          |             |
| power\_state\_message\_emulation\_trigger\_time | 1.0.0+   | 0 (0x0)        |             |
| power\_state\_message\_to\_emulate              | 1.0.0+   | 0 (0x0)        |             |

# systemreport

| Name    | Versions | Default Values | Description |
| ------- | -------- | -------------- | ----------- |
| enabled | 2.0.0+   | true           |             |

# systemsleep

| Name                                               | Versions    | Default Values | Description |
| -------------------------------------------------- | ----------- | -------------- | ----------- |
| disable\_auto\_sleep                               | 1.0.0+      | false          |             |
| disable\_tma\_sleep                                | 1.0.0+      | false          |             |
| dummy\_event\_auto\_wake                           | 2.0.0-3.0.2 | false          |             |
| enter\_sc7                                         | 1.0.0+      | true           |             |
| enter\_sleep                                       | 1.0.0+      | true           |             |
| hush\_time\_after\_brief\_power\_button\_press\_ms | 1.0.0+      | 1000 (0x3e8)   |             |
| keep\_vdd\_core                                    | 1.0.0+      | true           |             |
| override\_auto\_sleep\_time                        | 1.0.0+      | 0 (0x0)        |             |
| sleep\_pending\_time\_ms                           | 1.0.0+      | 15000 (0x3a98) |             |
| transition\_timeout\_sec                           | 1.0.0+      | 60 (0x3c)      |             |
| wake\_pin\_debug\_mode                             | 4.0.0+      | 0 (0x0)        |             |

# systemstartup

| Name            | Versions | Default Values | Description |
| --------------- | -------- | -------------- | ----------- |
| skip\_psc\_wait | 5.0.0+   | false          |             |

# systemupdate

| Name                                          | Versions | Default Values       | Description |
| --------------------------------------------- | -------- | -------------------- | ----------- |
| assumed\_system\_applet\_version              | 3.0.0+   | 0 (0x0)              |             |
| bgnup\_retry\_seconds                         | 1.0.0+   | 60 (0x3c)            |             |
| debug\_id                                     | 1.0.0+   | "0x0000000000000000" |             |
| debug\_id\_for\_content\_delivery             | 3.0.0+   | "0x0000000000000000" |             |
| debug\_version                                | 1.0.0+   | 0 (0x0)              |             |
| debug\_version\_for\_content\_delivery        | 3.0.0+   | 0 (0x0)              |             |
| enable\_background\_download\_stress\_testing | 1.0.0+   | false                |             |
| enable\_network\_service                      | 1.0.0    | false                |             |
| 2.0.0-2.3.0                                   | true     |                      |             |

# target\_manager

| Name         | Versions | Default Values | Description |
| ------------ | -------- | -------------- | ----------- |
| device\_name | 2.0.0+   | ""             |             |

# tc

| Name                                          | Versions                                                                                                                                       | Default Values                                                                                                                                                               | Description |
| --------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| iir\_filter\_gain\_pcb                        | 1.0.0+                                                                                                                                         | 100 (0x64)                                                                                                                                                                   |             |
| iir\_filter\_gain\_soc                        | 1.0.0+                                                                                                                                         | 100 (0x64)                                                                                                                                                                   |             |
| log\_enabled                                  | 1.0.0+                                                                                                                                         | false                                                                                                                                                                        |             |
| rate\_select                                  | 1.0.0+                                                                                                                                         | "both"                                                                                                                                                                       |             |
| sleep\_enabled                                | 2.0.0+                                                                                                                                         | true                                                                                                                                                                         |             |
| tskin\_pcb\_coefficients\_console             | 1.0.0-4.1.0                                                                                                                                    | "\[6182, 112480\]"                                                                                                                                                           |             |
| 5.0.0-5.1.0                                   | "\[6396, 119440\]"                                                                                                                             |                                                                                                                                                                              |             |
| tskin\_pcb\_coefficients\_console\_on\_fwdbg  | 6.0.0+                                                                                                                                         | "\[6396, 119440\]"                                                                                                                                                           |             |
| tskin\_pcb\_coefficients\_handheld            | 1.0.0-4.1.0                                                                                                                                    | "\[5464, 174190\]"                                                                                                                                                           |             |
| 5.0.0-5.1.0                                   | "\[5817, 129580\]"                                                                                                                             |                                                                                                                                                                              |             |
| tskin\_pcb\_coefficients\_handheld\_on\_fwdbg | 6.0.0+                                                                                                                                         | "\[5817, 129580\]"                                                                                                                                                           |             |
| tskin\_rate\_table\_console                   | 1.0.0-4.1.0                                                                                                                                    | "\[\[-1000000, 43000, 51, 51\], \[43000, 53000, 51, 153\], \[53000, 58000, 153, 255\], \[58000, 1000000, 255, 255\]\]"                                                       |             |
| 5.0.0+                                        | "\[\[-1000000, 40000, 0, 0\], \[36000, 43000, 51, 51\], \[43000, 53000, 51, 153\], \[53000, 58000, 153, 255\], \[58000, 1000000, 255, 255\]\]" |                                                                                                                                                                              |             |
| tskin\_rate\_table\_handheld                  | 1.0.0+                                                                                                                                         | "\[\[-1000000, 40000, 0, 0\], \[36000, 43000, 51, 51\], \[43000, 48000, 51, 102\], \[48000, 53000, 102, 153\], \[53000, 1000000, 153, 153\], \[48000, 1000000, 153, 153\]\]" |             |
| tskin\_select                                 | 1.0.0+                                                                                                                                         | "both"                                                                                                                                                                       |             |
| tskin\_soc\_coefficients\_console             | 1.0.0-5.1.0                                                                                                                                    | "\[6182, 112480\]"                                                                                                                                                           |             |
| tskin\_soc\_coefficients\_console\_on\_fwdbg  | 6.0.0+                                                                                                                                         | "\[6182, 112480\]"                                                                                                                                                           |             |
| tskin\_soc\_coefficients\_handheld            | 1.0.0-5.1.0                                                                                                                                    | "\[5464, 174190\]"                                                                                                                                                           |             |
| tskin\_soc\_coefficients\_handheld\_on\_fwdbg | 6.0.0+                                                                                                                                         | "\[5464, 174190\]"                                                                                                                                                           |             |
| use\_configurations\_on\_fwdbg                | 6.0.0+                                                                                                                                         | false                                                                                                                                                                        |             |

# tcap

| Name                                                | Versions | Default Values       | Description |
| --------------------------------------------------- | -------- | -------------------- | ----------- |
| continuous\_high\_skin\_temperature\_milli\_seconds | 5.0.0+   | 28800000 (0x1b77400) |             |
| thermal\_burn\_prevention\_mode\_enabled            | 5.0.0+   | true                 |             |

# time

| Name                                                    | Versions     | Default Values | Description |
| ------------------------------------------------------- | ------------ | -------------- | ----------- |
| notify\_time\_to\_fs\_interval\_seconds                 | 4.0.0+       | 600 (0x258)    |             |
| standard\_network\_clock\_sufficient\_accuracy\_minutes | 3.0.0+       | 43200 (0xa8c0) |             |
| standard\_steady\_clock\_rtc\_update\_interval\_minutes | 3.0.0+       | 5 (0x5)        |             |
| standard\_steady\_clock\_test\_offset\_minutes          | 1.0.0+       | 0 (0x0)        |             |
| standard\_user\_clock\_initial\_year                    | 5.0.0-7.0.1  | 2018 (0x7e2)   |             |
| 8.0.0+                                                  | 2019 (0x7e3) |                |             |

# usb

| Name                   | Versions | Default Values | Description |
| ---------------------- | -------- | -------------- | ----------- |
| show\_pdc\_boot\_fatal | 6.0.0+   | true           |             |
| usb30\_force\_enabled  | 3.0.0+   | false          |             |

# vulnerability

| Name                                 | Versions | Default Values | Description |
| ------------------------------------ | -------- | -------------- | ----------- |
| enable\_debug                        | 4.0.0+   | false          |             |
| needs\_update\_vulnerability\_policy | 2.0.0+   | 0 (0x0)        |             |

# wlan\_debug

| Name             | Versions    | Default Values | Description |
| ---------------- | ----------- | -------------- | ----------- |
| skip\_wlan\_boot | 1.0.0-6.2.0 | false          |             |

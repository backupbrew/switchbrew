This is the Switch equivalent of 3DS exheader. This is the 0x408-byte
file with extension ".npdm" in {Switch
ExeFS}.

| Offset | Size  | Description                                                                                    |
| ------ | ----- | ---------------------------------------------------------------------------------------------- |
| 0x0    | 0x80  | META                                                                                           |
| 0x80   | 0x200 | RSA-2048 signature, followed a RSA-2048 modulus for {Switch version of NCCH header}?(Like 3DS) |
| 0x280  | 0xD0  | ACID                                                                                           |
| 0x350  | 0xB8  | ACI0                                                                                           |

# META

Starts with magicnum "META". Switch version of 3DS "System Control
Info"?

# ACID

Starts with magicnum "ACID". Switch version of 3DS ACI(Access Control
Info)?

# ACI0

Starts with magicnum "ACI0". Switch version of AccessDesc?

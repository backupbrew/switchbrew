During [factory setup](Factory%20Setup.md "wikilink"), the Switch goes
through calibration and the generated data from this process is written
to two [NAND user partitions](Flash%20Filesystem.md "wikilink")
(**PRODINFO** and **PRODINFOF**).

**PRODINFOF** is a FAT12 compliant filesystem and it's structure can be
found [here](Flash%20Filesystem#PRODINFOF.md##PRODINFOF "wikilink").
It's mainly used to keep calibration logs and other assorted files.

**PRODINFO** is a raw binary blob containing the main calibration data,
which ranges from hardware IDs to system keys.

# CAL0

This is the raw data stored under the PRODINFO partition.

| Offset | Size   | Field                                           | Description                                                                           |
| ------ | ------ | ----------------------------------------------- | ------------------------------------------------------------------------------------- |
| 0x0000 | 0x04   | MagicNumber                                     | "CAL0" header magic.                                                                  |
| 0x0004 | 0x04   | Version                                         |                                                                                       |
| 0x0008 | 0x04   | BodySize                                        | Total size of calibration data starting at offset 0x40.                               |
| 0x000C | 0x02   | Model                                           |                                                                                       |
| 0x000E | 0x02   | UpdateCount                                     | Increases each time calibration data is installed.                                    |
| 0x0020 | 0x20   | BodyHash                                        | SHA256 hash calculated over calibration data.                                         |
| 0x0040 | 0x1E   | ConfigurationId1                                | Configuration ID string.                                                              |
| 0x0060 | 0x20   | Reserved                                        | Empty.                                                                                |
| 0x0080 | 0x04   | WlanCountryCodesNum                             | Number of elements in the WlanCountryCodes array.                                     |
| 0x0084 | 0x04   | WlanCountryCodesLastIndex                       | Index of the last element in the WlanCountryCodes array.                              |
| 0x0088 | 0x180  | WlanCountryCodes                                | Array of WLAN country code strings. Each element is 3 bytes (code + NULL terminator). |
| 0x0210 | 0x06   | WlanMacAddress                                  |                                                                                       |
| 0x0220 | 0x06   | BdAddress                                       |                                                                                       |
| 0x0230 | 0x06   | AccelerometerOffset                             |                                                                                       |
| 0x0238 | 0x06   | AccelerometerScale                              |                                                                                       |
| 0x0240 | 0x06   | GyroscopeOffset                                 |                                                                                       |
| 0x0248 | 0x06   | GyroscopeScale                                  |                                                                                       |
| 0x0250 | 0x18   | SerialNumber                                    |                                                                                       |
| 0x0270 | 0x30   | EccP256DeviceKey                                | Device key (ECC-P256 version; empty and unused).                                      |
| 0x02B0 | 0x180  | EccP256DeviceCertificate                        | Device certificate (ECC-P256 version; empty and unused).                              |
| 0x0440 | 0x30   | EccB233DeviceKey                                | Device key (ECC-B233 version; empty and unused).                                      |
| 0x0480 | 0x180  | EccB233DeviceCertificate                        | Device certificate (ECC-B233 version; active).                                        |
| 0x0610 | 0x30   | EccP256ETicketKey                               | ETicket key (ECC-P256 version; empty and unused).                                     |
| 0x0650 | 0x180  | EccP256ETicketCertificate                       | ETicket certificate (ECC-P256 version; empty and unused).                             |
| 0x07E0 | 0x30   | EccB233ETicketKey                               | ETicket key (ECC-B233 version; empty and unused).                                     |
| 0x0820 | 0x180  | EccB233ETicketCertificate                       | ETicket certificate (ECC-B233 version; empty and unused).                             |
| 0x09B0 | 0x110  | SslKey                                          | SSL key (empty and unused).                                                           |
| 0x0AD0 | 0x04   | SslCertificateSize                              | Total size of the SSL certificate.                                                    |
| 0x0AE0 | 0x800  | SslCertificate                                  | SSL certificate. Only SslCertificateSize bytes are used.                              |
| 0x12E0 | 0x20   | SslCertificateHash                              | SHA256 over the SSL certificate.                                                      |
| 0x1300 | 0x1000 | RandomNumber                                    | Random generated data.                                                                |
| 0x2300 | 0x20   | RandomNumberHash                                | SHA256 over the random data block.                                                    |
| 0x2320 | 0x110  | GameCardKey                                     | Gamecard key (empty and unused).                                                      |
| 0x2440 | 0x400  | GameCardCertificate                             | Gamecard certificate.                                                                 |
| 0x2840 | 0x20   | GameCardCertificateHash                         | SHA256 over the Gamecard certificate.                                                 |
| 0x2860 | 0x220  | Rsa2048ETicketKey                               | ETicket key (RSA-2048 version; empty and unused).                                     |
| 0x2A90 | 0x240  | Rsa2048ETicketCertificate                       | ETicket certificate (RSA-2048 version; active).                                       |
| 0x2CE0 | 0x18   | BatteryLot                                      | Battery lot string ID.                                                                |
| 0x2D00 | 0x800  | SpeakerCalibrationValue                         | Speaker calibration values. Only 0x5A bytes are used.                                 |
| 0x3510 | 0x04   | RegionCode                                      |                                                                                       |
| 0x3520 | 0x50   | AmiiboKey                                       | Amiibo key (ECQV and ECDSA versions).                                                 |
| 0x3580 | 0x14   | AmiiboEcqvCertificate                           | Amiibo certificate (ECQV version).                                                    |
| 0x35A0 | 0x70   | AmiiboEcdsaCertificate                          | Amiibo certificate (ECDSA version).                                                   |
| 0x3620 | 0x40   | AmiiboEcqvBlsKey                                | Amiibo key (ECQV-BLS version).                                                        |
| 0x3670 | 0x20   | AmiiboEcqvBlsCertificate                        | Amiibo certificate (ECQV-BLS version).                                                |
| 0x36A0 | 0x90   | AmiiboEcqvBlsRootCertificate                    | Amiibo root certificate (ECQV-BLS version).                                           |
| 0x3740 | 0x04   | ProductModel                                    | 1 = Nx, 2 = Copper                                                                    |
| 0x3750 | 0x06   | ColorVariation                                  |                                                                                       |
| 0x3760 | 0x0C   | LcdBacklightBrightnessMapping                   |                                                                                       |
| 0x3770 | 0x50   | ExtendedEccB233DeviceKey                        | Extended device key (ECC-B233 version; active).                                       |
| 0x37D0 | 0x50   | ExtendedEccP256ETicketKey                       | Extended ETicket key (ECC-P256 version; empty and unused).                            |
| 0x3830 | 0x50   | ExtendedEccB233ETicketKey                       | Extended ETicket key (ECC-B233 version; empty and unused).                            |
| 0x3890 | 0x240  | ExtendedRsa2048ETicketKey                       | Extended ETicket key (RSA-2048 version; active).                                      |
| 0x3AE0 | 0x130  | ExtendedSslKey                                  | Extended SSL key (active).                                                            |
| 0x3C20 | 0x130  | ExtendedGameCardKey                             | Extended Gamecard key (active).                                                       |
| 0x3D60 | 0x04   | LcdVendorId                                     |                                                                                       |
| 0x3D70 | 0x240  | \[5.0.0+\] ExtendedRsa2048DeviceKey             | Extended device key (RSA-2048 version; active).                                       |
| 0x3FC0 | 0x240  | \[5.0.0+\] Rsa2048DeviceCertificate             | Device certificate (RSA-2048 version; active).                                        |
| 0x4210 | 0x01   | \[5.0.0+\] UsbTypeCPowerSourceCircuitVersion    |                                                                                       |
| 0x4220 | 0x04   | \[9.0.0+\] HomeMenuSchemeSubColor               |                                                                                       |
| 0x4230 | 0x04   | \[9.0.0+\] HomeMenuSchemeBezelColor             |                                                                                       |
| 0x4240 | 0x04   | \[9.0.0+\] HomeMenuSchemeMainColor              |                                                                                       |
| 0x4250 | 0x04   | \[9.0.0+\] HomeMenuSchemeBackColor              |                                                                                       |
| 0x4260 | 0x04   | \[9.0.0+\] HomeMenuSchemeExtraColor             |                                                                                       |
| 0x4270 | 0x01   | \[9.0.0+\] AnalogStickModuleTypeL               |                                                                                       |
| 0x4280 | 0x12   | \[9.0.0+\] AnalogStickModelParameterL           |                                                                                       |
| 0x42A0 | 0x09   | \[9.0.0+\] AnalogStickFactoryCalibrationL       |                                                                                       |
| 0x42B0 | 0x01   | \[9.0.0+\] AnalogStickModuleTypeR               |                                                                                       |
| 0x42C0 | 0x12   | \[9.0.0+\] AnalogStickModelParameterR           |                                                                                       |
| 0x42E0 | 0x09   | \[9.0.0+\] AnalogStickFactoryCalibrationR       |                                                                                       |
| 0x42F0 | 0x01   | \[9.0.0+\] ConsoleSixAxisSensorModuleType       |                                                                                       |
| 0x4300 | 0x06   | \[9.0.0+\] ConsoleSixAxisSensorHorizontalOffset |                                                                                       |
| 0x4310 | 0x01   | \[6.0.0+\] BatteryVersion                       |                                                                                       |
| 0x4330 | 0x04   | \[9.0.0+\] HomeMenuSchemeModel                  |                                                                                       |

## Error detection

Each block of raw calibration data (with the exception of blocks with
SHA256 hashes) is padded to 16 bytes, being the last 2 bytes a CRC-16
over said block.

`XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX XX`  
`00 00 00 00 00 00 00 00 00 00 00 00 00 00 YY YY`  
  
`XX == data`  
`00 == padding`  
`YY == crc`

The CRC-16 is generated as follows:

`unsigned int crc_16_table[16] = {`  
` 0x0000, 0xCC01, 0xD801, 0x1400, 0xF001, 0x3C00, 0x2800, 0xE401,`  
` 0xA001, 0x6C00, 0x7800, 0xB401, 0x5000, 0x9C01, 0x8801, 0x4400 };`  
  
`unsigned short int get_crc_16 (char *p, int n) {`  
` unsigned short int crc = 0x55AA;`  
` int r;`  
  
` while (n-- > 0) {`  
`   r = crc_16_table[crc & 0xF];`  
`   crc = (crc >> 4) & 0x0FFF;`  
`   crc = crc ^ r ^ crc_16_table[*p & 0xF];`  
  
`   r = crc_16_table[crc & 0xF];`  
`   crc = (crc >> 4) & 0x0FFF;`  
`   crc = crc ^ r ^ crc_16_table[(*p >> 4) & 0xF];`  
  
`   p++;`  
` }`  
  
` return(crc);`  
`}`

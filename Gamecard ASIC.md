The Gamecard ASIC (known internally as the LOTUS3) is a separate chip on
the motherboard responsible for communicating with the
[Gamecard](Gamecard.md "wikilink").

It is the Tegra's SDMMC2 device on the Switch and
[FS](Filesystem%20services.md "wikilink") communicates with it using a
custom protocol based on vendor specific MMC commands.

# Protocol

All communication is done using the following MMC\_SEND\_MANUFACTURER
commands.

| Command | Name                                                   |
| ------- | ------------------------------------------------------ |
| 60      | [\#WriteOperation](#WriteOperation "wikilink")         |
| 61      | [\#GetOperationStatus](#GetOperationStatus "wikilink") |
| 62      | [\#PutToSleep](#PutToSleep "wikilink")                 |
| 63      | [\#ResetKeyData](#ResetKeyData "wikilink")             |

## WriteOperation

Submits a Gamecard ASIC [operation](#ASIC_commands "wikilink") using a
0x40 byte sized buffer as
follows.

### OperationBuffer

| Offset | Size | Description                                                  |
| ------ | ---- | ------------------------------------------------------------ |
| 0x0    | 0x1  | Gamecard ASIC [operation command](#ASIC_commands "wikilink") |
| 0x1    | 0x1F | Operation specific data                                      |
| 0x20   | 0x20 | Command verification value (secure mode only)                |

## GetOperationStatus

Returns the status of a completed operation.

## PutToSleep

Puts the Gamecard ASIC in sleep mode.

## ResetKeyData

Tells the Gamecard ASIC to generate new random key data.

# ASIC commands

The Gamecard ASIC supports a total of 19 operation commands. These
commands are passed to the ASIC using the
[\#WriteOperation](#WriteOperation "wikilink") MMC command.

Additional data buffers are then read/written using standard MMC
read/write
commands.

| Command | Name                                                                               |
| ------- | ---------------------------------------------------------------------------------- |
| 0x01    | [\#SetUserAsicFirmware](#SetUserAsicFirmware "wikilink")                           |
| 0x02    | [\#GetAsicCert](#GetAsicCert "wikilink")                                           |
| 0x03    | [\#SetEmmcEmbeddedSocCertificate](#SetEmmcEmbeddedSocCertificate "wikilink")       |
| 0x04    | [\#GetAsicEncryptedMessage](#GetAsicEncryptedMessage "wikilink")                   |
| 0x05    | [\#SetLibraryEncryptedMessage](#SetLibraryEncryptedMessage "wikilink")             |
| 0x06    | [\#GetAsicAuthenticationData](#GetAsicAuthenticationData "wikilink")               |
| 0x07    | [\#SetAsicAuthenticationDataHash](#SetAsicAuthenticationDataHash "wikilink")       |
| 0x08    | [\#SetLibraryAuthenticationData](#SetLibraryAuthenticationData "wikilink")         |
| 0x09    | [\#GetLibraryAuthenticationDataHash](#GetLibraryAuthenticationDataHash "wikilink") |
| 0x0A    | [\#EnterSecureAsicMode](#EnterSecureAsicMode "wikilink")                           |
| 0x0B    | [\#WriteAsicRegister](#WriteAsicRegister "wikilink")                               |
| 0x0C    | [\#ReadAsicRegister](#ReadAsicRegister "wikilink")                                 |
| 0x0D    | [\#ChangeDebugMode](#ChangeDebugMode "wikilink")                                   |
| 0x0E    | [\#GetCardHeader](#GetCardHeader "wikilink")                                       |
| 0x0F    | [\#GetCardKeyArea](#GetCardKeyArea "wikilink")                                     |
| 0x10    | [\#SendCardCommand](#SendCardCommand "wikilink")                                   |
| 0x11    | [\#EnableCardBus](#EnableCardBus "wikilink")                                       |
| 0x12    | [\#ExchangeRandomValuesInSecureMode](#ExchangeRandomValuesInSecureMode "wikilink") |
| 0x13    | [\#GetRmaInformation](#GetRmaInformation "wikilink")                               |

## SetUserAsicFirmware

Signals the Gamecard ASIC to receive a 0x7800 byte sized buffer
containing the [ASIC's user firmware](#User_firmware "wikilink").

## GetAsicCert

Signals the Gamecard ASIC to send a 0x400 byte sized buffer containing
the ASIC's certificate.

## SetEmmcEmbeddedSocCertificate

Signals the Gamecard ASIC to receive a 0x400 byte sized buffer
containing the certificate from
[GetGameCardCertificate](Settings%20services#GetGameCardCertificate.md##GetGameCardCertificate "wikilink").

## GetAsicEncryptedMessage

Signals the Gamecard ASIC to send a 0x100 byte sized buffer containing a
RSA-OAEP encrypted message to be decrypted by the host library. The
decrypted message will be used to generate a common AES-128 (CBC and
CTR) key and IV/CTR shared between the ASIC and the host library.

## SetLibraryEncryptedMessage

Signals the Gamecard ASIC to receive a 0x100 byte sized buffer
containing a RSA-OAEP encrypted message to be decrypted by the ASIC. The
decrypted message will be used to generate a common AES-128 (CBC and
CTR) key and IV/CTR shared between the ASIC and the host library.

## GetAsicAuthenticationData

Signals the Gamecard ASIC to send a 0x20 byte sized buffer containing
AES-128-CBC encrypted authentication data to be decrypted and hashed by
the host library.

## SetAsicAuthenticationDataHash

Signals the Gamecard ASIC to receive a 0x20 byte sized buffer containing
the AES-128-CBC encrypted hash of the ASIC authentication data.

## SetLibraryAuthenticationData

Signals the Gamecard ASIC to receive a 0x20 byte sized buffer containing
AES-128-CBC encrypted authentication data to be decrypted and hashed by
the ASIC.

## GetLibraryAuthenticationDataHash

Signals the Gamecard ASIC to send a 0x20 byte sized buffer containing
the AES-128-CBC encrypted hash of the library authentication data.

## EnterSecureAsicMode

Signals the Gamecard ASIC to enter secure mode. In secure mode, all
communication with the Gamecard ASIC must be AES-128-CTR encrypted.

## WriteAsicRegister

Signals the Gamecard ASIC to write an internal register. The register
value is passed in the first word of a 0x200 byte sized buffer while the
register index is passed in the actual
[\#OperationBuffer](#OperationBuffer "wikilink") as follows.

| Offset | Size | Description                            |
| ------ | ---- | -------------------------------------- |
| 0x0    | 0x1  | Gamecard ASIC operation command (0x0B) |
| 0x1    | 0x3  | Padding                                |
| 0x4    | 0x4  | Gamecard ASIC register index           |
| 0x8    | 0x18 | Empty                                  |
| 0x20   | 0x20 | Command verification value             |

## ReadAsicRegister

Signals the Gamecard ASIC to send a 0x30 byte sized buffer containing
the values of all ASIC registers.

## ChangeDebugMode

Signals the Gamecard ASIC to change into debug mode and send a 0x200
byte sized buffer containing information on the current Gamecard.

## GetCardHeader

Signals the Gamecard ASIC to send a 0x108 byte sized buffer containing
the current Gamecard's header data as
follows.

| Offset | Size  | Description                                                                                                   |
| ------ | ----- | ------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x8   | Unknown                                                                                                       |
| 0x8    | 0x100 | [Gamecard header](Gamecard%20Format#Gamecard%20Header.md##Gamecard_Header "wikilink") (without the signature) |

## GetCardKeyArea

Signals the Gamecard ASIC to send a 0x800 byte sized buffer containing
the current Gamecard's key area sectors.

## SendCardCommand

Signals the Gamecard ASIC to relay a specific
[command](#Gamecard_commands "wikilink") to the Gamecard. The command is
sent to the Gamecard using the
[\#OperationBuffer](#OperationBuffer "wikilink") as follows.

| Offset | Size | Description                            |
| ------ | ---- | -------------------------------------- |
| 0x0    | 0x1  | Gamecard ASIC operation command (0x10) |
| 0x1    | 0x7  | Unknown                                |
| 0x8    | 0x1  | Gamecard command                       |
| 0x9    | 0x17 | Command specific data                  |
| 0x20   | 0x20 | Command verification value             |

## EnableCardBus

Signals the Gamecard ASIC to enable the current Gamecard's bus line.

## ExchangeRandomValuesInSecureMode

Signals the Gamecard ASIC to exchange random authentication values with
the current Gamecard. The Gamecard response values are returned in a
0x20 sized buffer while the host values are passed in the actual
[\#OperationBuffer](#OperationBuffer "wikilink") as follows.

| Offset | Size | Description                            |
| ------ | ---- | -------------------------------------- |
| 0x0    | 0x1  | Gamecard ASIC operation command (0x12) |
| 0x1    | 0x1F | Random value from host                 |
| 0x20   | 0x20 | Command verification value             |

## GetRmaInformation

Signals the Gamecard ASIC to send a 0x200 byte sized buffer containing
information on the Gamecard ASIC. This is called by
[GetGameCardAsicInfo](Filesystem%20services#IDeviceOperator.md##IDeviceOperator "wikilink").

# Gamecard commands

These commands are issued by the Gamecard ASIC to the actual Gamecard
using the [\#OperationBuffer](#OperationBuffer "wikilink") passed to
[\#SendCardCommand](#SendCardCommand "wikilink").

| Command | Name            |
| ------- | --------------- |
| 0x10    | ReadId1Writer   |
| 0x11    | ReadId2Writer   |
| 0x12    | ReadId3Writer   |
| 0x15    | ReadCrc         |
| 0x16    | WritePage       |
| 0x18    | Erase           |
| 0x19    | ReadDevParam    |
| 0x20    | WriteDevParam   |
| 0x21    | ReadPageSecure  |
| 0x28    | ReadId2Normal   |
| 0x2E    |                 |
| 0x30    | ReadId3Secure   |
| 0x39    |                 |
| 0x56    | ReadId1Normal   |
| 0x83    | WritePageSecure |
| 0x5B    | ReadPage        |
| 0x67    | ReadId1Secure   |
| 0xA5    | ReadId3Normal   |
| 0xB8    |                 |
| 0xC4    | ReadId2Secure   |
| 0xE0    |                 |
| 0xE2    |                 |

# Modes

Both the Gamecard ASIC and the actual Gamecard can operate in different
modes.

## ASIC modes

| Mode | Name    |
| ---- | ------- |
| 0x00 | Initial |
| 0x01 | Secure  |

## Gamecard modes

| Mode | Name    |
| ---- | ------- |
| 0x00 | Initial |
| 0x01 | Normal  |
| 0x02 | Secure  |
| 0x03 | Write   |

# User firmware

[FS](Filesystem%20services.md "wikilink") provides the appropriate
Gamecard ASIC's user firmware (Lotus ASIC Firmware or LAFW) which is
encrypted, signed and follows the format below.

| Offset | Size   | Description                                    |
| ------ | ------ | ---------------------------------------------- |
| 0x0    | 0x100  | RSA-PKCS\#1 signature                          |
| 0x100  | 0x4    | Magic ("LAFW")                                 |
| 0x104  | 0x4    | Unknown (0xFF000000, 0xFFFF0000 or 0xFFFFFF00) |
| 0x108  | 0x4    |                                                |
| 0x10C  | 0x4    |                                                |
| 0x110  | 0x4    | Version (0, 1 or 3)                            |
| 0x114  | 0x4    | Unknown (0x80000000)                           |
| 0x118  | 0x4    | Data size                                      |
| 0x11C  | 0x4    |                                                |
| 0x120  | 0x10   | Data hash                                      |
| 0x130  | 0x10   | Placeholder string ("IDIDIDIDIDIDIDID")        |
| 0x140  | 0x40   | Empty                                          |
| 0x180  | 0x7680 | Encrypted data                                 |

## Types

Depending on it's purpose, multiple user firmware blobs exist.

### FwRead

Code for reading retail Gamecards. Only the normal and secure [Gamecard
modes](#Gamecard_modes "wikilink") are supported.

Found inside [FS](Filesystem%20services.md "wikilink").

\[4.0.0+\] This firmware blob was updated to provide support for new
Gamecards.

### FwWriter

Code for writing development Gamecards. Only the normal and write
[Gamecard modes](#Gamecard_modes "wikilink") are supported.

Found inside [FS](Filesystem%20services.md "wikilink").

### FwReadDev

Code for reading development Gamecards. Development Gamecards use common
[initial
data](Gamecard%20Format#Initial%20Data.md##Initial_Data "wikilink")
which justifies the need for a specialized read firmware.

Found inside [FS](Filesystem%20services.md "wikilink").

### FwDebug

Code for calling [\#GetRmaInformation](#GetRmaInformation "wikilink").
Must be passed as an argument for
[GetGameCardAsicInfo](Filesystem%20services#IDeviceOperator.md##IDeviceOperator "wikilink").

Never observed (possibly factory only).

## Anti-downgrade

Loading an user firmware blob with a certain version field will lock the
Gamecard ASIC to only allow running firmware blobs with the same or
higher version number. Therefore, it is speculated that the Gamecard
ASIC contains some sort of non-volatile memory bank which could be used
for this purpose (among others).

The [FwWriter](#FwWriter "wikilink") and
[FwReadDev](#FwReadDev "wikilink") blobs' version is always 0, but
[FwRead](#FwRead "wikilink") blob's version is either 1 or 3
(\[4.0.0+\]). This effectively locks retail consoles from using the
development firmware blobs.

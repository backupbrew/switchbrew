##### Pinout

![Gamecard-pinout.png](Gamecard-pinout.png
"Gamecard-pinout.png")

| Pin | Name     | Direction | Description                                                                      |
| --- | -------- | --------- | -------------------------------------------------------------------------------- |
| 0   | IRQ?     | Output    | Always wired to GND inside game cartridge; Possibly used for interrupt signaling |
| 1   | RCLK     | Output    | Return clock; Game cartridge sends back CLK signal delayed by a few ns           |
| 2   | CLK      | Input     | Clock, 25MHz                                                                     |
| 3   | CS       | Input     | Chip select; Switch pulls this LOW during a transfer                             |
| 4   | DAT0     | Inout     | Data bus pin 0                                                                   |
| 5   | DAT1     | Inout     | Data bus pin 1                                                                   |
| 6   | VCC 3.3v | Input     |                                                                                  |
| 7   | DAT2     | Inout     | Data bus pin 2                                                                   |
| 8   | DAT3     | Inout     | Data bus pin 3                                                                   |
| 9   | VCC 1.8v | Input     |                                                                                  |
| 10  | DAT4     | Inout     | Data bus pin 4                                                                   |
| 11  | DAT5     | Inout     | Data bus pin 5                                                                   |
| 12  | DAT6     | Inout     | Data bus pin 6                                                                   |
| 13  | DAT7     | Inout     | Data bus pin 7                                                                   |
| 14  | GND      |           |                                                                                  |
| 15  | RST      | Input     | Reset, active LOW.                                                               |
|     |          |           |                                                                                  |

All IO use 1.8V for logic HIGH and 0V for logic LOW.

##### Protocol

Switch game cartridges use a simple (but Nintendo proprietery) SPI-like
bus with 8-bit width (DAT7..0). It is very similar to the bus interface
of 3DS game cartridges, except with very different commands.

The Switch host starts a transfer by first pulling CS low, followed by
clocking a byte each clock cycle. The bus data will always be ready
before the rising edge of the CLK signal, so that it can be captured on
the rising edge. After command bytes are written to the bus, the
direction of the bus implicitly changes and the game cartridge responds.
The Switch host keeps clocking while the game cartridge responds. After
the transfer is ended, the CS line is pulled high again.

Commands are 16 bytes long, and followed immediately by a 4-byte CRC-32
over the command bytes. After this, the bus direction changes, and the
bus will be 'floating' for a few cycles (*TBD figure out if cartridge
can respond with NAK over bad CRC during floating bus*).

Before the game cartridge responds with the actual response data, it
will send busy bytes (LSB will be zero) to the Switch host, until it is
ready to send the real response. When the game cartridge is ready, it
will send 2 acknowledgement bytes (LSB will be one) to let the Switch
host know. After this, the game cartridge will send the actual response
bytes.

The actual response bytes are also followed immediately by a 4-byte
CRC-32 over the actual response
bytes.

##### Commands

| Command                            | Description                                                  |
| ---------------------------------- | ------------------------------------------------------------ |
| `5B000000000000010000000000000000` | Read sector 0, contains "HEAD" blob                          |
| `5B000000000000010000000000000000` | Read sector 0, contains "HEAD" blob                          |
| `56000000000000000000000000000000` | Read card id "AE F8 01 21"                                   |
| `28000000000000000000000000000000` | Read ??? "02 00 00 00"                                       |
| `A5000000000000000000000000000000` | Read ??? "00 00 00 00"                                       |
| `56000000000000000000000000000000` | Read card id "AE F8 01 21"                                   |
| `28000000000000000000000000000000` | Read ??? "02 00 00 00"                                       |
| `5B000000380000010000000000000000` | Read sector 0x38, contains "CERT" blob                       |
| `E2000000000000000000000000000000` | Read ??? "01 00 00 00"                                       |
| `E0000000000000000000000000000000` | Read crypto-challenge header                                 |
| `200838A25A344F818ABB6456694D4E8D` | Enter crypto mode with seed "0838A25A344F818ABB6456694D4E8D" |
| `7EE41FDF12C01C157CC899910673A0CF` | Encrypted command                                            |
| `263C8230EC15FAE3CE79365BD850F4BD` | Encrypted command                                            |
| `B6FDA6F37FFA29E18831D0B217DFBDBE` | Encrypted command                                            |
| `7B97F7DF07240AA9870E1C974336FA8A` | Encrypted command                                            |
|                                    |                                                              |

The meaning of some these commands are currently unknown.

##### Encryption

After a few initial plaintext commands, the Switch instructs the game
cartridge to enter into encrypted mode. From that point on, commands and
responses are sent encrypted over the bus. The encryption algorithm used
is currently unknown.

# 1,2 Switch

Credit images: smiba
([link](http://gbatemp.net/threads/switch-cartridge-reverse-engineering.464580/))

### Description

  - Package: TSOP-48
  - Manufacturer: Unknown

### Frontside

![CartridgeFront.jpeg](CartridgeFront.jpeg "CartridgeFront.jpeg")

### Frontside (bare)

![CartridgeFrontBare.jpeg](CartridgeFrontBare.jpeg
"CartridgeFrontBare.jpeg")

### Backside

![CartridgeBack.jpeg](CartridgeBack.jpeg "CartridgeBack.jpeg")

# Zelda: Breath of the wild

Credit images: Retr0id
([link](http://gbatemp.net/threads/switch-cartridge-reverse-engineering.464580/))

### Description

  - Package: Custom
  - Manufacturer: Macronix (MX)

### Overview

![CartridgeZelda.jpeg](CartridgeZelda.jpeg "CartridgeZelda.jpeg")

### Frontside

![CartridgeZeldaFront.jpeg](CartridgeZeldaFront.jpeg
"CartridgeZeldaFront.jpeg")

### Backside

![CartridgeZeldaBack.jpeg](CartridgeZeldaBack.jpeg
"CartridgeZeldaBack.jpeg")

# Schematic

Credit images: smiba
([link](http://gbatemp.net/threads/switch-cartridge-reverse-engineering.464580/))

### Connector Pinout Schematic

![CatridgePinout.png](CatridgePinout.png "CatridgePinout.png")

### Chip Pinout Schematic

![CartridgePinoutTsop.png](CartridgePinoutTsop.png
"CartridgePinoutTsop.png")

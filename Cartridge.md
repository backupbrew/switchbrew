|                                                                                                     |                                                                                         |
| --------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| ![A Switch game cartridge, frontside](ZeldaFront.jpg "A Switch game cartridge, frontside")          | ![A Switch game cartridge, backside](ZeldaBack.jpg "A Switch game cartridge, backside") |
| ![Close-up of frontside PCB](CartridgeFront.jpeg "Close-up of frontside PCB")                       | ![Close-up of backside PCB](CartridgeBack.jpeg "Close-up of backside PCB")              |
| ![Close-up of stripped frontside PCB](CartridgeFrontBare.jpeg "Close-up of stripped frontside PCB") |                                                                                         |
|                                                                                                     |                                                                                         |

## Pinout

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

## Protocol

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
CRC-32 over the actual response bytes.

## Commands

A typical boot up sequence of a game cartridge looks like
this:

| Command                            | Size  | Description                                                  |
| ---------------------------------- | ----- | ------------------------------------------------------------ |
| `5B000000000000010000000000000000` | 0x200 | Read sector 0, contains "HEAD" blob                          |
| `5B000000000000010000000000000000` | 0x200 | Read sector 0, contains "HEAD" blob                          |
| `56000000000000000000000000000000` | 0x4   | Read card id "AE F8 01 21"                                   |
| `28000000000000000000000000000000` | 0x4   | Read ??? "02 00 00 00"                                       |
| `A5000000000000000000000000000000` | 0x4   | Read ??? "00 00 00 00"                                       |
| `56000000000000000000000000000000` | 0x4   | Read card id "AE F8 01 21"                                   |
| `28000000000000000000000000000000` | 0x4   | Read ??? "02 00 00 00"                                       |
| `5B000000380000010000000000000000` | 0x200 | Read sector 0x38, contains "CERT" blob                       |
| `E2000000000000000000000000000000` | 0x4   | Read ??? "01 00 00 00"                                       |
| `E0000000000000000000000000000000` | 0x200 | Read crypto-challenge header                                 |
| `200838A25A344F818ABB6456694D4E8D` | 0     | Enter crypto mode with seed "0838A25A344F818ABB6456694D4E8D" |
| `7EE41FDF12C01C157CC899910673A0CF` | 0x40  | Encrypted command, possibly read UID?                        |
| `263C8230EC15FAE3CE79365BD850F4BD` | 0x0   | Encrypted command                                            |
| `B6FDA6F37FFA29E18831D0B217DFBDBE` | 0x4   | Encrypted command, possibly read card id?                    |
| `7B97F7DF07240AA9870E1C974336FA8A` | 0x4   | Encrypted command                                            |
|                                    |       |                                                              |

The meaning of some these commands are currently unknown.

## Encryption

After a few initial plaintext commands, the Switch instructs the game
cartridge to enter into encrypted mode. From that point on, commands and
responses are sent encrypted over the bus. The encryption algorithm used
is currently unknown.

## Manufacturers

  - Macronix (MX)  
    Uses package: BGA
    Uses card id: 0xC2
  - OKI Semiconductor  
    Uses package: TSOP-48
    Uses card id: 0xAE
  - SanDisk?  
    Uses package: ??
    Uses card id: 0x45 ?

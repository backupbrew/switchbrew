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
over the command bytes. After this, the Switch stops driving the data
bus, and the bus will be 'floating'. Due to the pull-ups on the bus, it
will slowly converge to logic HIGH state. The Switch will clock 2 cycles
to allow the bus to settle a direction change. The Switch host will then
clock another cycle and if the game cartridge didn't receive the CRC OK,
it will respond with "01". Otherwise it will respond with "00" and pull
DAT0 low on the next cycle to signal it is busy. The Switch host will
then keep clocking until the cartridge is ready.

When the game cartridge is ready to send the actual data response, it
will pull the DAT0 pin high for 2 cycles to let the Switch host know.
After this, the game cartridge will send the actual data response bytes.

The actual response bytes are also followed immediately by a 4-byte
CRC-32 over the actual data response bytes.

## Commands

A typical boot up sequence of a game cartridge (in this case, the game
"1,2 Switch") looks like
this:

| Command                            | Size  | Description                                                                  |
| ---------------------------------- | ----- | ---------------------------------------------------------------------------- |
| `5B000000000000010000000000000000` | 0x200 | Read sector 0, contains "HEAD" blob                                          |
| `5B000000000000010000000000000000` | 0x200 | Read sector 0, contains "HEAD" blob                                          |
| `56000000000000000000000000000000` | 0x4   | Read card id "AE F8 01 21"                                                   |
| `28000000000000000000000000000000` | 0x4   | Read ??? "02 00 00 00"                                                       |
| `A5000000000000000000000000000000` | 0x4   | Read ??? "00 00 00 00"                                                       |
| `56000000000000000000000000000000` | 0x4   | Read card id "AE F8 01 21"                                                   |
| `28000000000000000000000000000000` | 0x4   | Read ??? "02 00 00 00"                                                       |
| `5B000000380000010000000000000000` | 0x200 | Read sector 0x38, contains "CERT" blob                                       |
| `E2000000000000000000000000000000` | 0x4   | Read ??? "01 00 00 00"                                                       |
| `E0000000000000000000000000000000` | 0x200 | Read crypto-challenge header                                                 |
| `200838A25A344F818ABB6456694D4E8D` | 0     | Enter crypto mode1 with HOST-RANDOM "0838A25A344F818ABB6456694D4E8D"         |
| `7EE41FDF12C01C157CC899910673A0CF` | 0x40  | Encrypted crypto mode1 command, reads CART-RANDOM                            |
| `263C8230EC15FAE3CE79365BD850F4BD` | 0x0   | Encrypted mode1 command, enters crypto mode2 with (HOST-RANDOM, CART-RANDOM) |
| `B6FDA6F37FFA29E18831D0B217DFBDBE` | 0x4   | Encrypted mode2 command, possibly read card id?                              |
| `7B97F7DF07240AA9870E1C974336FA8A` | 0x4   | Encrypted mode2 command                                                      |
|                                    |       |                                                                              |

The meaning of some these commands are currently unknown.

## Observations

  - The "update" and "normal" partitions can be dumped using the
    plaintext 5B commands
  - The "secure" partition can only be read from encrypted mode.

## Encryption

After a few initial plaintext commands, the Switch instructs the game
cartridge to enter into encrypted mode. From that point on, commands and
responses are sent encrypted over the bus. The encryption algorithm used
is currently unknown.

There appear to be 2 kinds of crypto mode.

Crypto mode1 is initiated solely by the HOST-RANDOM as random session
seed. In that mode, the Switch host requests for the game cartridge
random seed, and then sends a command to enter crypto mode2.

Crypto mode2 takes into account the CART-RANDOM seed generated by the
cartridge, and possibly the previous HOST-RANDOM. The game cartridge
will always send a different CART-RANDOM even if the exact same command
sequence is replayed and thus with this scheme replay attacks are not
possible.

## Manufacturers

  - Macronix (MX)  
    Uses package: LGA
    Uses card id: 0xC2
  - OKI Semiconductor  
    Uses package: TSOP-48
    Uses card id: 0xAE
  - SanDisk?  
    Uses package: ??
    Uses card id: 0x45 ?

## Examples

The following examples are extracted from the game "1,2
Switch".

### HEAD blob

`00000000: 6c dc 15 86 fa 88 11 f6 2f 4c b0 b8 3d 3f e9 63  l......./L..=?.c`  
`00000010: e9 5d b7 41 80 d5 1d e4 99 fa 5b 17 8a f1 91 e4  .].A......[.....`  
`00000020: d0 4c de 68 c5 d7 57 64 b5 91 fd 68 36 f3 fe ce  .L.h..Wd...h6...`  
``00000030: c9 d1 fa 8e 9d ce 94 c2 55 a3 7a 60 f9 80 85 a8  ........U.z`....``  
`00000040: 44 18 a9 b3 29 20 42 8d 5f 7a 2f ae 50 81 46 9c  D...) B._z/.P.F.`  
`00000050: 81 a1 a0 e2 89 3a 46 37 19 c1 c6 11 07 f9 f8 74  .....:F7.......t`  
`00000060: 89 98 d0 96 8e 44 10 f7 ac 62 f6 4a 50 b9 3d dc  .....D...b.JP.=.`  
`00000070: c9 cd 62 20 df 44 c7 41 d1 50 49 3c 06 38 dd 52  ..b .D.A.PI<.8.R`  
`00000080: f2 84 bb 9f 63 e7 64 4f b9 db 7f a2 47 e2 2f 3c  ....c.dO....G./<`  
`00000090: ba 52 27 92 6d 17 e4 25 a6 90 99 d6 88 66 3a c1  .R'.m..%.....f:.`  
`000000a0: 52 54 6a c6 79 09 42 3c 3f 9e 33 32 f4 c6 eb 7d  RTj.y.B<?.32...}`  
``000000b0: 60 e5 f9 44 8b 6e ff 43 a6 13 6c 29 8e bd c8 6b  `..D.n.C..l)...k``  
`000000c0: 64 39 2d d5 f3 9a 4b 04 89 dc ac 0b b4 22 35 9f  d9-...K......"5.`  
`000000d0: df 74 2f f0 fb 6d a6 a4 56 ff 92 88 72 42 72 ea  .t/..m..V...rBr.`  
`000000e0: de f8 37 0e 46 77 04 05 43 df 59 2f 92 d1 3c 38  ..7.Fw..C.Y/..<8`  
`000000f0: 73 c8 64 e5 ea 2b 96 56 85 d2 9d a6 3a c4 46 1a  s.d..+.V....:.F.`  
`00000100: 48 45 41 44 40 02 0c 00 ff ff ff ff 00 f8 00 00  HEAD@...........`  
`00000110: 44 6c dd 95 4e c0 45 02 f1 27 38 00 00 00 00 00  Dl..N.E..'8.....`  
`00000120: 08 5a 9c f5 ab 2a 9d f5 da 96 ab 8e 7a e9 11 68  .Z...*......z..h`  
`00000130: 00 f0 00 00 00 00 00 00 00 02 00 00 00 00 00 00  ................`  
`00000140: 11 f7 72 54 a1 85 c0 cf 14 e9 99 f0 6a 1f c0 61  ..rT........j..a`  
`00000150: 05 74 33 f0 50 3e ee 78 68 7e f5 ef 33 da f1 1f  .t3.P>.xh~..3...`  
`00000160: 88 7f 7c a9 85 bd 0f 4e 2f fe cd 1f f4 26 74 29  ..|....N/....&t)`  
`00000170: 49 9d e5 d6 df c4 75 03 b9 9a b9 c7 8f 37 5c 88  I.....u......7\.`  
`00000180: 01 00 00 00 02 00 00 00 00 00 00 00 40 02 0c 00  ............@...`  
`00000190: ea a4 81 b6 30 4b 45 0c 71 5f a3 0c 5f 88 1f 9a  ....0KE.q_.._...`  
`000001a0: 67 9a e6 29 15 50 1a 46 98 a5 a1 af b1 07 ed 48  g..).P.F.......H`  
`000001b0: df a8 36 bb cd 2d d7 ba f5 c6 80 0a 03 ff 1f 73  ..6..-.........s`  
`000001c0: 2c bd 18 38 a0 49 24 c7 49 d1 94 52 ef 6a 7c 23  ,..8.I$.I..R.j|#`  
`000001d0: eb ca a4 35 52 59 e6 d3 98 ed b7 ec 11 cf 0b 1d  ...5RY..........`  
`000001e0: 29 f1 1d 43 e8 e0 2e 0f db 98 1a 88 47 fa 11 79  )..C........G..y`  
`000001f0: a8 ef 47 21 a1 bb de a6 dd b4 d6 27 8f 25 62 e4  ..G!.......'.%b.`

### CERT blob

`00000000: 72 cf 8c ed ce ed 43 fb 82 77 2c 86 2e da 1d 07  r.....C..w,.....`  
`00000010: 13 68 2e 1a fe 15 ac 6e 27 21 ec 3a 0f e9 fa 20  .h.....n'!.:...`  
`00000020: 7b 70 62 a4 c3 47 65 86 ca 73 08 f0 71 80 17 59  {pb..Ge..s..q..Y`  
`00000030: 6a c8 2e e9 42 f8 69 12 7c 9d 5d 02 24 6b 2b 5e  j...B.i.|.].$k+^`  
`00000040: c4 d2 c8 80 11 47 a2 5e 41 b3 a9 41 95 91 bd 8f  .....G.^A..A....`  
`00000050: 6b c1 f5 0b 9b 37 06 6b ea 8e cd e9 eb 1d 8e c7  k....7.k........`  
`00000060: 3e 83 f1 85 8b 85 c6 af bf 38 c1 0a 7c c0 d1 42  >........8..|..B`  
`00000070: 0c 0c 7c 22 cd 0f a3 8c ee 48 e5 32 9f 68 1c e5  ..|".....H.2.h..`  
`00000080: 13 4b d7 94 a1 c8 18 d0 1f 11 de 35 1e 34 a7 d1  .K.........5.4..`  
`00000090: 32 d8 d8 66 8b b1 db 1a 5b b6 1f fd 9a c9 a4 4b  2..f....[......K`  
`000000a0: 66 61 d9 52 5c f1 3c 8d de 25 f1 76 06 1b f2 37  fa.R\.<..%.v...7`  
`000000b0: a7 fb 1c f5 b8 20 67 ff 79 f2 a4 ab 8a 82 c4 97  ..... g.y.......`  
``000000c0: 9d 4c 01 e7 18 1f 91 60 f7 b8 68 da 73 b3 fa 47  .L.....`..h.s..G``  
`000000d0: 18 8f e8 ca e9 4b 08 1b 13 3e 17 e2 63 99 95 2f  .....K...>..c../`  
`000000e0: e6 d1 98 dc 50 77 7c 8a 25 eb 9e 34 0d e5 f1 93  ....Pw|.%..4....`  
`000000f0: b2 32 c5 da a1 ff 53 12 fb 5d bd 1f 67 6e 94 84  .2....S..]..gn..`  
`00000100: 43 45 52 54 00 00 00 00 00 00 00 00 00 00 00 00  CERT............`  
`00000110: 87 cd 3f 5c 04 49 6a 02 5f b1 7a 6a 13 d1 88 8f  ..?\.Ij._.zj....`  
`00000120: 00 10 00 00 00 00 00 00 00 00 09 52 b7 d5 d2 30  ...........R...0`  
`00000130: a3 13 4d 94 4b 0f 87 fe 2b da 37 ef 2d 38 25 75  ..M.K...+.7.-8%u`  
``00000140: d6 3e 94 7c 2a a0 f6 8a a3 60 40 18 5f 53 54 53  .>.|*....`@._STS``  
`00000150: fc 0f 1c 2d 10 92 f8 b6 d2 f2 97 df b2 13 2a 14  ...-..........*.`  
`00000160: ea c4 b1 9f 9c f4 b8 2f ef 5b 4f e3 8e d9 47 d7  ......./.[O...G.`  
`00000170: 2c 15 95 68 7e f4 e0 71 99 83 17 0c e1 fe 84 b5  ,..h~..q........`  
`00000180: a1 30 4c 33 c6 2c 13 fa 19 4d 37 48 e9 4e 3b a6  .0L3.,...M7H.N;.`  
`00000190: fa 0a 1e 13 46 f1 bf 15 88 5d 59 65 f7 a4 ad ba  ....F....]Ye....`  
`000001a0: d6 12 ce c2 33 b8 c3 c9 8f d3 34 c6 a5 6d 52 ff  ....3.....4..mR.`  
`000001b0: d9 55 96 5f cd 59 d5 0d 84 ff 83 7d f0 33 d8 32  .U._.Y.....}.3.2`  
`000001c0: ed 35 48 62 3a 68 2f 1e bf 22 1c fb cd e5 d9 b8  .5Hb:h/.."......`  
``000001d0: fc 24 e1 58 5d b3 4d 69 60 ab 8d 0e 17 28 24 43  .$.X].Mi`....($C``  
`000001e0: b7 a6 43 99 03 3c 1a 92 09 6b 8c 6f 09 37 6a 50  ..C..<...k.o.7jP`  
`000001f0: 46 91 d1 bf 7d 7a 32 a9 70 28 f1 5e 31 97 ac be  F...}z2.p(.^1...`

### Crypto-challenge header

`00000000: 44 6c dd 95 4e c0 45 02 00 00 00 00 00 00 00 00  Dl..N.E.........`  
`00000010: a0 27 b4 2d 32 91 a0 8f 06 10 cb b0 ff d1 1b b3  .'.-2...........`  
`00000020: aa 8a 9e 34 05 e0 81 42 4a 50 88 fc 5c 06 c6 c4  ...4...BJP..\...`  
`00000030: 5c 54 10 ee 66 07 0c a5 04 9f ef 9a 00 00 00 00  \T..f...........`  
`00000040: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`00000050: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`00000060: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`00000070: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`00000080: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`00000090: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`000000a0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`000000b0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`000000c0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`000000d0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`000000e0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`000000f0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`00000100: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`00000110: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`00000120: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`00000130: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`00000140: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`00000150: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`00000160: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`00000170: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`00000180: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`00000190: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`000001a0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`000001b0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`000001c0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`000001d0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`000001e0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`  
`000001f0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................`

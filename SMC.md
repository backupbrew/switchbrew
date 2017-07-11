# Secure Monitor Calls

The secure monitor provides two top level handlers of which each
provides a range of sub handlers.

Secure Monitor Calls follow the ARM SMC calling
convention:

| Bit number | Bit mask   | Description                                             |
| ---------- | ---------- | ------------------------------------------------------- |
| 31         | 0x80000000 | Set to 0 means Yielding Call; Set to 1 means Fast Call. |
| 30         | 0x40000000 | Set to 0 means SMC32 convention; Set to 1 means SMC64.  |
| 29-24      | 0x3F000000 | Service Call ranges.                                    |
| 23-16      | 0x00FF0000 | Must be zero.                                           |
| 15-0       | 0x0000FFFF | Function number within the range call type.             |

## Id 0

Cryptography related functions.

| Sub-Id     | Name                               | In | Out |
| ---------- | ---------------------------------- | -- | --- |
| 0xC3000401 | SetConfig                          |    |     |
| 0xC3000002 | GetConfig (Same as Id 1 Sub-Id 4.) |    |     |
| 0xC3000003 | CheckStatus\_5\_9\_F\_10           |    |     |
| 0xC3000404 | GetResult\_5\_9\_F\_10             |    |     |
| 0xC3000E05 | ExpMod                             |    |     |
| 0xC3000006 | PrngX931 (Same as Id 1 Sub-Id 5.)  |    |     |
| 0xC3000007 | Keygen7                            |    |     |
| 0xC3000008 | SetKeyslotFromXY                   |    |     |
| 0xC3000009 | SymmetricCrypto                    |    |     |
| 0xC300000A | KeygenA                            |    |     |
| 0xC300040B | CMAC                               |    |     |
| 0xC300100C | ImportParamsFor10                  |    |     |
| 0xC300100D | DecryptExpModParams                |    |     |
| 0xC300100E | ImportParamsForF                   |    |     |
| 0xC300060F | ExpMod                             |    |     |
| 0xC3000610 | ExpMod                             |    |     |
| 0xC3000011 | SetKeyslotFromX                    |    |     |
| 0xC3000012 | Keygen12                           |    |     |

## Id 1

General and power related functions.

| Sub-Id     | Name                               | In | Out |
| ---------- | ---------------------------------- | -- | --- |
| 0xC4000001 | CPU\_SUSPEND (oyasumi)             |    |     |
| 0x84000002 | CPU\_OFF                           |    |     |
| 0xC4000003 | CPU\_ON                            |    |     |
| 0xC3000004 | GetConfig (Same as Id 0 Sub-Id 2.) |    |     |
| 0xC3000005 | PrngX931 (Same as Id 0 Sub-Id 6.)  |    |     |
| 0xC3000006 | Panic                              |    |     |
| 0xC3000007 |                                    |    |     |
| 0xC3000008 | ReadWriteRegister                  |    |     |

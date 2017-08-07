# Secure Monitor Calls

The secure monitor provides two top level handlers of which each
provides a range of sub handlers.

Secure Monitor Calls follow the ARM SMC calling convention up to a small
change:

| Bit number | Bit mask   | Description                                                           |
| ---------- | ---------- | --------------------------------------------------------------------- |
| 31         | 0x80000000 | Set to 0 means Yielding Call; Set to 1 means Fast Call.               |
| 30         | 0x40000000 | Set to 0 means SMC32 convention; Set to 1 means SMC64.                |
| 29-24      | 0x3F000000 | Service Call ranges.                                                  |
| 23-16      | 0x00FF0000 | Must be zero.                                                         |
| 15-8       | 0x0000FF00 | Argument type. This is different from the ARM SMC calling convention. |
| 7-0        | 0x000000FF | Function number within the range call type.                           |

If bit *n* is set in the argument type then parameter X*n* is treated as
a pointer and the kernel will setup address translation for it in
[svcCallSecureMonitor](SVC#svcCallSecureMonitor.md##svcCallSecureMonitor "wikilink").

## Id 0

Functions exposed to user-mode processes using
[svcCallSecureMonitor](SVC.md "wikilink").

| Sub-Id     | Name                               | In | Out |
| ---------- | ---------------------------------- | -- | --- |
| 0xC3000401 | SetConfig                          |    |     |
| 0xC3000002 | GetConfig (Same as Id 1 Sub-Id 4.) |    |     |
| 0xC3000003 | CheckStatus\_5\_9\_F\_10           |    |     |
| 0xC3000404 | GetResult\_5\_9\_F\_10             |    |     |
| 0xC3000E05 | ExpMod                             |    |     |
| 0xC3000006 | PrngX931 (Same as Id 1 Sub-Id 5.)  |    |     |
| 0xC3000007 | KeygenAndSealX                     |    |     |
| 0xC3000008 | SetKeyslotFromXY                   |    |     |
| 0xC3000009 | SymmetricCrypto                    |    |     |
| 0xC300000A | KeygenA                            |    |     |
| 0xC300040B | CMAC                               |    |     |
| 0xC300100C | ImportParamsFor10WithXY            |    |     |
| 0xC300100D | DecryptExpModParamsWithXY          |    |     |
| 0xC300100E | ImportParamsForFWithXY             |    |     |
| 0xC300060F | ExpMod                             |    |     |
| 0xC3000610 | ExpModAndKeygenAndSealZ            |    |     |
| 0xC3000011 | SetKeyslotFromZ                    |    |     |
| 0xC3000012 | \[2.0.0\]+ KeygenAndSealZ          |    |     |

## Id 1

Functions exposed to the kernel internally.

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

# spl:

| Cmd | Name                                                                 | Notes                                                                                                                               |
| --- | -------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| 0   | [\#GetConfig](#GetConfig "wikilink")                                 | wrapper for [GetConfig](SMC#GetConfig.md##GetConfig "wikilink")                                                                     |
| 1   | ExpMod                                                               | user supplied modulus and exponent                                                                                                  |
| 2   | [\#KeygenAndSealX](#KeygenAndSealX "wikilink")                       | wrapper for [KeygenAndSealX](SMC#KeygenAndSealX.md##KeygenAndSealX "wikilink")                                                      |
| 3   | SetKeyslotFromXY                                                     | wrapper for [SetKeyslotFromXY](SMC#SetKeyslotFromXY.md##SetKeyslotFromXY "wikilink")                                                |
| 4   | DecryptAESCBCWithX                                                   | decrypts 16 bytes, uses [SetKeyslotFromXY](SMC#SetKeyslotFromXY.md##SetKeyslotFromXY "wikilink") with a fixed Y and a fixed CBC IV  |
| 5   | [\#SetConfig](#SetConfig "wikilink")                                 | wrapper for [SetConfig](SMC#SetConfig.md##SetConfig "wikilink")                                                                     |
| 7   | Prng                                                                 | uses [PrngX931](SMC#PrngX931.md##PrngX931 "wikilink")                                                                               |
| 9   | ImportExpModParams                                                   | wrapper for [ImportParamsForFWithXY](SMC#ImportParamsForFWithXY.md##ImportParamsForFWithXY "wikilink")                              |
| 10  | ExpMod                                                               | wrapper for [ExpMod](SMC#ExpMod.md##ExpMod "wikilink")                                                                              |
| 11  | [\#GetDevunitFlag](#GetDevunitFlag "wikilink")                       | uses [GetConfig](SMC#GetConfig.md##GetConfig "wikilink")                                                                            |
| 12  | KeygenA                                                              | wrapper for [KeygenA](SMC#KeygenA.md##KeygenA "wikilink")                                                                           |
| 13  | [\#DecryptExpModParamsWithXY](#DecryptExpModParamsWithXY "wikilink") | wrapper for [DecryptExpModParamsWithXY](SMC#DecryptExpModParamsWithXY.md##DecryptExpModParamsWithXY "wikilink")                     |
| 14  | DecryptAESCBC                                                        | decrypts 16 bytes, uses [SetKeyslotFromXY](SMC#SetKeyslotFromXY.md##SetKeyslotFromXY "wikilink") with fixed X, Y and a fixed CBC IV |
| 15  | SymmetricCrypto                                                      | wrapper for [SymmetricCrypto](SMC#SymmetricCrypto.md##SymmetricCrypto "wikilink")                                                   |
| 16  | CMAC                                                                 | wrapper for [CMAC](SMC#CMAC.md##CMAC "wikilink")                                                                                    |
| 17  | ImportExpModParams                                                   | wrapper for [ImportParamsFor10WithXY](SMC#ImportParamsFor10WithXY.md##ImportParamsFor10WithXY "wikilink")                           |
| 18  | ExpModAndKeygenAndSealZ                                              | wrapper for [ExpModAndKeygenAndSealZ](SMC#ExpModAndKeygenAndSealZ.md##ExpModAndKeygenAndSealZ "wikilink")                           |
| 19  | SetKeyslotFromZ                                                      | wrapper for [SetKeyslotFromZ](SMC#SetKeyslotFromZ.md##SetKeyslotFromZ "wikilink")                                                   |
| 20  | KeygenAndSealZ                                                       | wrapper for [KeygenAndSealZ](SMC#KeygenAndSealZ.md##KeygenAndSealZ "wikilink")                                                      |
| 21  |                                                                      |                                                                                                                                     |
| 22  |                                                                      |                                                                                                                                     |
| 23  | GetSplWaitEvent                                                      |                                                                                                                                     |

## GetConfig

Takes an input word (ConfigItem), and returns a u64 with the config
params.

| ConfigItem | Name                             |
| ---------- | -------------------------------- |
| 1          | DisableProgramVerification       |
| 2          | MemoryConfiguration              |
| 5          | HardwareType (0=Icosa, 1=Copper) |
| 7          | IsRecoveryBoot                   |
| 8          | DeviceId (byte7 clear).          |
| 9          | BootReason                       |
| 11         | AllowSkippingNrrSignatures       |
| 13         | BatteryProfile?                  |

Output from this when used by [NIM](NIM%20services.md "wikilink") must
match the [set:cal](Settings%20services.md "wikilink") DeviceId with
byte7 cleared, otherwise NIM will panic.

[RO](Loader%20services.md "wikilink") checks id11, if set then skipping
NRR rsa signatures is allowed.

## KeygenAndSealX

Takes 16-bytes as input and two u32s. Outputs random-looking 16-bytes.

Same input gives same output. Output changes when system is rebooted.

## SetConfig

Takes two input words, a ConfigItem and the value to set.

| ConfigItem | Name             |
| ---------- | ---------------- |
| 13         | Battery profile? |

## GetDevunitFlag

No input params.

Returns an u8 flag for whether the system is devunit. Output flag is 0
on retail.

## DecryptExpModParamsWithXY

Last SPL cmd used by [SSL](SSL%20services.md "wikilink")-sysmodule for
TLS client-privk.

# csrng

| Cmd | Name                                           |
| --- | ---------------------------------------------- |
| 0   | [\#GetRandomBytes](#GetRandomBytes "wikilink") |

## GetRandomBytes

Takes a type-6 buffer and fills it with random
data.

# spl:

| Cmd | Name                                                                 | Notes                                                                                                                               |
| --- | -------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| 0   | [\#GetConfig](#GetConfig "wikilink")                                 | wrapper for [GetConfig](SMC#GetConfig.md##GetConfig "wikilink")                                                                     |
| 1   |                                                                      | user supplied modulus and exponent                                                                                                  |
| 2   | [\#GenerateAesKek](#GenerateAesKek "wikilink")                       | wrapper for [KeygenAndSealX](SMC#KeygenAndSealX.md##KeygenAndSealX "wikilink")                                                      |
| 3   | LoadAesKey                                                           | wrapper for [SetKeyslotFromXY](SMC#SetKeyslotFromXY.md##SetKeyslotFromXY "wikilink")                                                |
| 4   | GenerateAesKey                                                       | decrypts 0x10 bytes using AES ECB, uses [SetKeyslotFromXY](SMC#SetKeyslotFromXY.md##SetKeyslotFromXY "wikilink") with a fixed Y     |
| 5   | [\#SetConfig](#SetConfig "wikilink")                                 | wrapper for [SetConfig](SMC#SetConfig.md##SetConfig "wikilink")                                                                     |
| 7   | GetRandom                                                            | uses [PrngX931](SMC#PrngX931.md##PrngX931 "wikilink")                                                                               |
| 9   |                                                                      | wrapper for [ImportParamsForFWithXY](SMC#ImportParamsForFWithXY.md##ImportParamsForFWithXY "wikilink")                              |
| 10  |                                                                      | wrapper for [ExpMod](SMC#ExpMod.md##ExpMod "wikilink")                                                                              |
| 11  | [\#IsDevelopment](#IsDevelopment "wikilink")                         |                                                                                                                                     |
| 12  | GenerateSpecificAesKey                                               | wrapper for [KeygenA](SMC#KeygenA.md##KeygenA "wikilink")                                                                           |
| 13  | [\#DecryptExpModParamsWithXY](#DecryptExpModParamsWithXY "wikilink") | wrapper for [DecryptExpModParamsWithXY](SMC#DecryptExpModParamsWithXY.md##DecryptExpModParamsWithXY "wikilink")                     |
| 14  |                                                                      | decrypts 0x10 bytes using AES ECB, uses [SetKeyslotFromXY](SMC#SetKeyslotFromXY.md##SetKeyslotFromXY "wikilink") with fixed X and Y |
| 15  | DecryptAesCtr                                                        | wrapper for [SymmetricCrypto](SMC#SymmetricCrypto.md##SymmetricCrypto "wikilink")                                                   |
| 16  | ComputeCmac                                                          | wrapper for [CMAC](SMC#CMAC.md##CMAC "wikilink")                                                                                    |
| 17  |                                                                      | wrapper for [ImportParamsFor10WithXY](SMC#ImportParamsFor10WithXY.md##ImportParamsFor10WithXY "wikilink")                           |
| 18  |                                                                      | wrapper for [ExpModAndKeygenAndSealZ](SMC#ExpModAndKeygenAndSealZ.md##ExpModAndKeygenAndSealZ "wikilink")                           |
| 19  |                                                                      | wrapper for [SetKeyslotFromZ](SMC#SetKeyslotFromZ.md##SetKeyslotFromZ "wikilink")                                                   |
| 20  |                                                                      | wrapper for [KeygenAndSealZ](SMC#KeygenAndSealZ.md##KeygenAndSealZ "wikilink")                                                      |
| 21  | [\#UninitializeSpl](#UninitializeSpl "wikilink")                     |                                                                                                                                     |
| 22  | [\#InitializeSpl](#InitializeSpl "wikilink")                         |                                                                                                                                     |
| 23  | GetSplWaitEvent                                                      |                                                                                                                                     |

## GetConfig

Takes an input word (ConfigItem), and returns a u64 with the config
params.

| ConfigItem | Name                                                                                                                                                                              |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1          | DisableProgramVerification                                                                                                                                                        |
| 2          | MemoryConfiguration                                                                                                                                                               |
| 5          | HardwareType (0=Icosa, 1=Copper)                                                                                                                                                  |
| 6          | IsRetail                                                                                                                                                                          |
| 7          | IsRecoveryBoot                                                                                                                                                                    |
| 8          | DeviceId (byte7 clear).                                                                                                                                                           |
| 9          | BootReason                                                                                                                                                                        |
| 10         | MemoryArrange                                                                                                                                                                     |
| 11         | AllowSkippingNrrSignatures. Also used by FS-sysmodule for non-RSA: when zero, bit62 in fsp-pr registration permissions are force-cleared to zero, otherwise the original is used. |
| 13         | BatteryProfile?                                                                                                                                                                   |

[PM](Process%20Manager%20services.md "wikilink") checks id1 and if
non-zero, calls fsp-pr SetEnabledProgramVerification(false).

[NIM](NIM%20services.md "wikilink") checks that id8 output must match
the [set:cal](Settings%20services.md "wikilink") DeviceId with byte7
cleared, otherwise panic.

[RO](Loader%20services.md "wikilink") checks id11, if set then skipping
NRR rsa signatures is allowed.

## GenerateAesKek

Takes a 16-byte seed ("BisEncryptionKeySourceForKek") and two words
("KeyGeneration" and "option") as input. KeyGeneration ranges from 0 to
2.

Same input gives same output. Output changes when system is rebooted.

## SetConfig

Takes two input words, a ConfigItem and the value to set.

| ConfigItem | Name             |
| ---------- | ---------------- |
| 13         | Battery profile? |

## IsDevelopment

No input params.

Uses [\#GetConfig](#GetConfig "wikilink") internally with id=6. Returns
true if output from that is 0, or if the SMC returned error 2.

Returns an u8 flag for whether the system is devunit. Output flag is 0
on retail.

## DecryptExpModParamsWithXY

Last SPL cmd used by [SSL](SSL%20services.md "wikilink")-sysmodule for
TLS client-privk.

## UninitializeSpl

Returns a single u32 (always 3?) only once.

## InitializeSpl

Takes a single u32 (always 3?) only once.

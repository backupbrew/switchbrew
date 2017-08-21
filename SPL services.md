# csrng

| Cmd | Name                                           |
| --- | ---------------------------------------------- |
| 0   | [\#GetRandomBytes](#GetRandomBytes "wikilink") |

## GetRandomBytes

Takes a type-6 buffer and fills it with random data. Same command for
"spl:" and "csrng" services.

# spl:

\[2.0.0+\] Where previously only one AES engine was utilized, there is
now support for 4 of them.

\[2.0.0+\] When the session closes, all AES engines that were locked are
automatically
unlocked.

| Cmd | Name                                                                 | Notes                                                                                                                               |
| --- | -------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| 0   | [\#GetConfig](#GetConfig "wikilink")                                 | wrapper for [GetConfig](SMC#GetConfig.md##GetConfig "wikilink")                                                                     |
| 1   |                                                                      | user supplied modulus and exponent                                                                                                  |
| 2   | [\#GenerateAesKek](#GenerateAesKek "wikilink")                       | wrapper for [KeygenAndSealX](SMC#KeygenAndSealX.md##KeygenAndSealX "wikilink")                                                      |
| 3   | [\#LoadAesKey](#LoadAesKey "wikilink")                               | wrapper for [SetKeyslotFromXY](SMC#SetKeyslotFromXY.md##SetKeyslotFromXY "wikilink")                                                |
| 4   | [\#GenerateAesKey](#GenerateAesKey "wikilink")                       | decrypts 0x10 bytes using AES ECB, uses [SetKeyslotFromXY](SMC#SetKeyslotFromXY.md##SetKeyslotFromXY "wikilink") with a fixed Y     |
| 5   | [\#SetConfig](#SetConfig "wikilink")                                 | wrapper for [SetConfig](SMC#SetConfig.md##SetConfig "wikilink")                                                                     |
| 7   | [\#GetRandomBytes](#GetRandomBytes "wikilink")                       | uses [PrngX931](SMC#PrngX931.md##PrngX931 "wikilink")                                                                               |
| 9   |                                                                      | wrapper for [ImportParamsForFWithXY](SMC#ImportParamsForFWithXY.md##ImportParamsForFWithXY "wikilink")                              |
| 10  |                                                                      | wrapper for [ExpMod](SMC#ExpMod.md##ExpMod "wikilink")                                                                              |
| 11  | [\#IsDevelopment](#IsDevelopment "wikilink")                         |                                                                                                                                     |
| 12  | GenerateSpecificAesKey                                               | wrapper for [KeygenA](SMC#KeygenA.md##KeygenA "wikilink")                                                                           |
| 13  | [\#DecryptExpModParamsWithXY](#DecryptExpModParamsWithXY "wikilink") | wrapper for [DecryptExpModParamsWithXY](SMC#DecryptExpModParamsWithXY.md##DecryptExpModParamsWithXY "wikilink")                     |
| 14  | [\#GenerateAesKeyOther](#GenerateAesKeyOther "wikilink")             | decrypts 0x10 bytes using AES ECB, uses [SetKeyslotFromXY](SMC#SetKeyslotFromXY.md##SetKeyslotFromXY "wikilink") with fixed X and Y |
| 15  | [\#DecryptAesCtr](#DecryptAesCtr "wikilink")                         | wrapper for [SymmetricCrypto](SMC#SymmetricCrypto.md##SymmetricCrypto "wikilink")                                                   |
| 16  | [\#ComputeCmac](#ComputeCmac "wikilink")                             | wrapper for [CMAC](SMC#CMAC.md##CMAC "wikilink")                                                                                    |
| 17  |                                                                      | wrapper for [ImportParamsFor10WithXY](SMC#ImportParamsFor10WithXY.md##ImportParamsFor10WithXY "wikilink")                           |
| 18  |                                                                      | wrapper for [ExpModAndKeygenAndSealZ](SMC#ExpModAndKeygenAndSealZ.md##ExpModAndKeygenAndSealZ "wikilink")                           |
| 19  | [\#SetKeyslotFromZ](#SetKeyslotFromZ "wikilink")                     | wrapper for [SetKeyslotFromZ](SMC#SetKeyslotFromZ.md##SetKeyslotFromZ "wikilink")                                                   |
| 20  | \[2.0.0+\]                                                           | wrapper for [KeygenAndSealZ](SMC#KeygenAndSealZ.md##KeygenAndSealZ "wikilink")                                                      |
| 21  | \[2.0.0+\] [\#LockAesEngine](#LockAesEngine "wikilink")              |                                                                                                                                     |
| 22  | \[2.0.0+\] [\#UnlockAesEngine](#UnlockAesEngine "wikilink")          |                                                                                                                                     |
| 23  | \[2.0.0+\] GetSplWaitEvent                                           |                                                                                                                                     |

## GetConfig

Takes an input word (ConfigItem), and returns a u64 with the config
params.

| ConfigItem | Name                             |
| ---------- | -------------------------------- |
| 1          | DisableProgramVerification       |
| 2          | MemoryConfiguration              |
| 5          | HardwareType (0=Icosa, 1=Copper) |
| 6          | IsRetail                         |
| 7          | IsRecoveryBoot                   |
| 8          | DeviceId (byte7 clear).          |
| 9          | BootReason                       |
| 10         | MemoryArrange                    |
| 11         | IsDebugMode                      |
| 12         | KernelMemoryConfiguration        |
| 13         | BatteryProfile?                  |

[PM](Process%20Manager%20services.md "wikilink") checks id1 and if
non-zero, calls fsp-pr SetEnabledProgramVerification(false).

[NIM](NIM%20services.md "wikilink") checks that id8 output must match
the [set:cal](Settings%20services.md "wikilink") DeviceId with byte7
cleared, otherwise panic.

\[3.0.0+\] [RO](Loader%20services.md "wikilink") checks id11, if set
then skipping NRR rsa signatures is allowed.

Kernel uses id11 to determine behavior of svcBreak positive arguments.
It will break instead of just force-exiting the process which is what
happens on retail.

Kernel uses id12 when setting up the available RAM size. If bit0 is set,
it will memset various allocated memory-regions with 0x58, 0x59, 0x60
('X', 'Y', 'Z') instead of zero. This allows Nintendo devs to find
uninitialized memory bugs.

## GenerateAesKek

Takes a 16-byte seed ("BisEncryptionKeySourceForKek") and two words
("KeyGeneration" and "option") as input. KeyGeneration ranges from 0 to
2.

Same input gives same output. Output changes when system is rebooted.

## LoadAesKey

\[2.0.0+\] Now verifies that the engine used (0..3) is locked/owned by
the current spl session, otherwise errors with 0xD21A. Previously engine
was hardcoded to 0.

## GenerateAesKey

\[2.0.0+\] Previously it used engine 0 always. Now it tries to allocate
an engine to be used, returns 0xD01A if they're all busy. After command
is done, the engine is released.

## SetConfig

Takes two input words, a ConfigItem and the value to set.

| ConfigItem | Name            |
| ---------- | --------------- |
| 13         | BatteryProfile? |

## IsDevelopment

No input params.

Uses [\#GetConfig](#GetConfig "wikilink") internally with id=6. Returns
true if output from that is 0, or if the SMC returned error 2.

Returns an u8 flag for whether the system is devunit. Output flag is 0
on retail.

## DecryptExpModParamsWithXY

Last SPL cmd used by [SSL](SSL%20services.md "wikilink")-sysmodule for
TLS client-privk.

## GenerateAesKeyOther

Scrambles with a different constant than non-"other" version.

\[2.0.0+\] Introduced same engine allocation code as for
[\#GenerateAesKey](#GenerateAesKey "wikilink").

## DecryptAesCtr

\[2.0.0+\] Verifies the engine is locked by current session, same change
as [\#LoadAesKey](#LoadAesKey "wikilink").

## ComputeCmac

\[2.0.0+\] Verifies the engine is locked by current session, same change
as [\#LoadAesKey](#LoadAesKey "wikilink").

## SetKeyslotFromZ

\[2.0.0+\] Verifies the engine is locked by current session, same change
as [\#LoadAesKey](#LoadAesKey "wikilink").

## LockAesEngine

Returns the id of the engine that was locked, or 0xD01A if all engines
are busy. You need to lock an engine before using AES functions.

## UnlockAesEngine

Takes a single u32 and unlocks the engine with that id. It must be owned
by current session otherwise 0xD21A will be returned.

# csrng

This is "nn::spl::detail::IRandomInterface".

| Cmd | Name                                           |
| --- | ---------------------------------------------- |
| 0   | [\#GetRandomBytes](#GetRandomBytes "wikilink") |

## GetRandomBytes

Takes a type-6 buffer and fills it with random data. Same command for
"spl:" and "csrng" services.

# spl:

This is "nn::spl::detail::IGeneralInterface".

\[2.0.0+\] Where previously only one AES engine was utilized, there is
now support for 4 of them.

\[2.0.0+\] When the session closes, all AES engines that were locked are
automatically
unlocked.

| Cmd | Name                                                                          | Notes                                                                                                                               |
| --- | ----------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| 0   | [\#GetConfig](#GetConfig "wikilink")                                          | Wrapper for [GetConfig SMC](SMC#GetConfig.md##GetConfig "wikilink").                                                                |
| 1   | [\#UserExpMod](#UserExpMod "wikilink")                                        | Speculative name. Wrapper for [ExpMod SMC](SMC#ExpMod.md##ExpMod "wikilink").                                                       |
| 2   | [\#GenerateAesKek](#GenerateAesKek "wikilink")                                | Wrapper for [GenerateAesKek SMC](SMC#GenerateAesKek.md##GenerateAesKek "wikilink").                                                 |
| 3   | [\#LoadAesKey](#LoadAesKey "wikilink")                                        | Wrapper for [LoadAesKey SMC](SMC#LoadAesKey.md##LoadAesKey "wikilink").                                                             |
| 4   | [\#GenerateAesKey](#GenerateAesKey "wikilink")                                | Decrypts 0x10 bytes using AES ECB and uses [LoadAesKey SMC](SMC#LoadAesKey.md##LoadAesKey "wikilink") with a fixed Y.               |
| 5   | [\#SetConfig](#SetConfig "wikilink")                                          | Wrapper for [SetConfig SMC](SMC#SetConfig.md##SetConfig "wikilink").                                                                |
| 7   | [\#GetRandomBytes](#GetRandomBytes "wikilink")                                | Uses [GetRandomBytes SMC](SMC#GetRandomBytes.md##GetRandomBytes "wikilink").                                                        |
| 9   | [\#DecryptImportPrivkForRsaOaep](#DecryptImportPrivkForRsaOaep "wikilink")    | Speculative name. Wrapper for [LoadRsaPublicKey SMC](SMC#LoadRsaPublicKey.md##LoadRsaPublicKey "wikilink").                         |
| 10  | [\#DecryptRsaOaep](#DecryptRsaOaep "wikilink")                                | Speculative name. Uses [PublicRsa SMC](SMC#PublicRsa.md##PublicRsa "wikilink").                                                     |
| 11  | [\#IsDevelopment](#IsDevelopment "wikilink")                                  |                                                                                                                                     |
| 12  | [\#GenerateSpecificAesKey](#GenerateSpecificAesKey "wikilink")                | Wrapper for [GenerateSpecificAesKey SMC](SMC#GenerateSpecificAesKey.md##GenerateSpecificAesKey "wikilink").                         |
| 13  | [\#DecryptPrivk](#DecryptPrivk "wikilink")                                    | Speculative name. Wrapper for [PrivateRsa SMC](SMC#PrivateRsa.md##PrivateRsa "wikilink").                                           |
| 14  | [\#DecryptAesKey](#DecryptAesKey "wikilink")                                  | Decrypts 0x10 bytes using AES ECB and uses [LoadAesKey SMC](SMC#LoadAesKey.md##LoadAesKey "wikilink") with fixed X and Y.           |
| 15  | [\#DecryptAesCtr](#DecryptAesCtr "wikilink")                                  | Wrapper for [CryptAes SMC](SMC#CryptAes.md##CryptAes "wikilink").                                                                   |
| 16  | [\#ComputeCmac](#ComputeCmac "wikilink")                                      | Wrapper for [ComputeCmac SMC](SMC#ComputeCmac.md##ComputeCmac "wikilink").                                                          |
| 17  | [\#DecryptImportPrivkForExpMod1](#DecryptImportPrivkForExpMod1 "wikilink")    | Speculative name. Wrapper for [LoadRsaPrivateKey SMC](SMC#LoadRsaPrivateKey.md##LoadRsaPrivateKey "wikilink").                      |
| 18  | [\#UnwrapRsaWrappedTitleKey](#UnwrapRsaWrappedTitleKey "wikilink")            | Speculative name. Wrapper for [UnwrapRsaWrappedTitleKey SMC](SMC#UnwrapRsaWrappedTitleKey.md##UnwrapRsaWrappedTitleKey "wikilink"). |
| 19  | [\#LoadTitleKey](#LoadTitleKey "wikilink")                                    | Wrapper for [LoadTitleKey SMC](SMC#LoadTitleKey.md##LoadTitleKey "wikilink").                                                       |
| 20  | \[2.0.0+\] [\#UnwrapAesWrappedTitleKey](#UnwrapAesWrappedTitleKey "wikilink") | Wrapper for [UnwrapAesWrappedTitleKey SMC](SMC#UnwrapAesWrappedTitleKey.md##UnwrapAesWrappedTitleKey "wikilink").                   |
| 21  | \[2.0.0+\] [\#LockAesEngine](#LockAesEngine "wikilink")                       |                                                                                                                                     |
| 22  | \[2.0.0+\] [\#UnlockAesEngine](#UnlockAesEngine "wikilink")                   |                                                                                                                                     |
| 23  | \[2.0.0+\] [\#GetSplWaitEvent](#GetSplWaitEvent "wikilink")                   |                                                                                                                                     |

## GetConfig

Takes a u32 (**ConfigItem**), and returns a u64 (**ConfigVal**).

| ConfigItem | Name                                                  |
| ---------- | ----------------------------------------------------- |
| 1          | DisableProgramVerification                            |
| 2          | MemoryConfiguration                                   |
| 3          | SecurityEngineIRQNumber                               |
| 4          | Returns 0x02?                                         |
| 5          | HardwareType (0=Icosa (nx-abca2), 1=Copper (nx-abcb)) |
| 6          | IsRetail                                              |
| 7          | IsRecoveryBoot                                        |
| 8          | DeviceId (byte7 clear)                                |
| 9          | BootReason                                            |
| 10         | MemoryArrange                                         |
| 11         | IsDebugMode                                           |
| 12         | KernelMemoryConfiguration                             |
| 13         | BatteryProfile                                        |

[PM](Process%20Manager%20services.md "wikilink") checks id1 and if
non-zero, calls fsp-pr SetEnabledProgramVerification(false).

[PCV](PCV%20services.md "wikilink") configures memory profiles based on
id2.

| Platform     | Version                                 | Revision | id2    |
| ------------ | --------------------------------------- | -------- | ------ |
| "jetson-tx1" | "11\_40800\_01\_V9.8.3\_V1.6"           | N/A      | N/A    |
| "nx-abcb"    | "10\_40800\_NoCfgVersion\_V9.8.4\_V1.6" | 0        | 0      |
| "nx-abca2"   | "10\_40800\_NoCfgVersion\_V9.8.7\_V1.6" | 0        | 0 or 3 |
| "nx-abca2"   | "10\_40800\_NoCfgVersion\_V9.8.7\_V1.6" | 1        | 4      |
| "nx-abca2"   | "10\_40800\_NoCfgVersion\_V9.8.7\_V1.6" | 2        | 1      |
| "nx-abca2"   | "10\_40800\_NoCfgVersion\_V9.8.7\_V1.6" | 3        | 2      |
|              |                                         |          |        |

SPL uses id3 for setting up the security engine IRQ.

[NIM](NIM%20services.md "wikilink") checks that id8 output must match
the [set:cal](Settings%20services.md "wikilink") DeviceId with byte7
cleared, otherwise panic.

\[3.0.0+\] [RO](Loader%20services.md "wikilink") checks id11, if set
then skipping NRR rsa signatures is allowed.

Kernel uses id11 to determine behavior of svcBreak positive arguments.
It will break instead of just force-exiting the process which is what
happens on retail. \[2.0.0+\] This is also used with certain debug
[SVCs](SVC.md "wikilink").

Kernel reads id12 when setting up memory-related code. If bit0 is set,
it will memset various allocated memory-regions with 0x58, 0x59, 0x5A
('X', 'Y', 'Z') instead of zero. This allows Nintendo devs to find
uninitialized memory bugs. If bit17-16 is 0b01, the kernel assumes 6GB
of DRAM instead of 4GB.

## UserExpMod

Takes one type-10 (C descriptor) buffer (**data\_out\_buf**) and 3
type-9 (X descriptor) buffers (**data\_in\_buf**, **exp\_in\_buf** and
**mod\_in\_buf**).

Performs asymmetric crypto with user supplied modulus and exponent.

## GenerateAesKek

Takes a 16-byte EKS (**Encryption Key Source**) and two words
(**KeyGeneration** and **option**) as input. **KeyGeneration** ranges
from 0 to 2.

Returns a scrambled sealed KEK (**Key Encryption Key** used as
**key\_x**).

## LoadAesKey

Takes a u32 (**keyslot**) and two 16-byte keys (**key\_x** and
**key\_y**).

Sets the specified **keyslot** with a key generated from **key\_x** and
**key\_y**.

\[2.0.0+\] Now verifies that the engine in use (0..3) is locked/owned by
the current spl session, otherwise errors with 0xD21A. Previously engine
was hardcoded to 0.

## GenerateAesKey

Takes a 16-byte KEK (**key\_x**) and a 16-byte encrypted key
(**enc\_key**).

Generates a new key by decrypting **enc\_key** with a key generated from
the supplied **key\_x** and a fixed **key\_y**.

\[2.0.0+\] Previously, it always used engine 0. Now it tries to allocate
an engine to be used and returns 0xD01A if they're all busy. When the
command is done, the engine is released.

## SetConfig

Takes a u32 (**ConfigItem**) and a u64 (**ConfigVal**).

| ConfigItem | Name           |
| ---------- | -------------- |
| 13         | BatteryProfile |

Any other **ConfigItem**, besides 13, can't be set.

## DecryptImportPrivkForRsaOaep

Takes one type-9 (X descriptor) buffer (**enc\_privk\_in\_buf**), a
16-byte KEK (**key\_x**), a 16-byte key (**key\_y**) and a u32
(**version**). **version** is 0 for normal keys or 1 for extended keys.

Decrypts **enc\_privk\_in\_buf** with a key generated from **key\_x**
and **key\_y** and imports it for later usage.

## DecryptRsaOaep

Takes one type-10 (C descriptor) buffer (**data\_out\_buf**) and 3
type-9 (X descriptor) buffers (**data\_in\_buf**, **mod\_in\_buf** and
**label\_hash\_in\_buf**).

Decrypts **data\_in\_buf** into **data\_out\_buf** using the private key
imported with
[\#DecryptImportPrivkForRsaOaep](#DecryptImportPrivkForRsaOaep "wikilink")
and the supplied **mod\_in\_buf**. Afterwards, verifies RSA-OAEP
encoding using **label\_hash\_in\_buf**.

Returns an u32 (**dec\_data\_size**).

## IsDevelopment

No input params.

Uses [\#GetConfig](#GetConfig "wikilink") internally with id=6. Returns
true if output from that is 0, or if the SMC returned error 2.

Returns an u8 flag for whether the system is devunit. Output flag is 0
on retail.

## GenerateSpecificAesKey

Takes a 16-byte seed (**key\_seed**) and two words (**KeyGeneration**
and **option**) as input. **KeyGeneration** ranges from 0 to 2.

Returns a scrambled key (**key\_a**).

## DecryptPrivk

Takes one type-10 (C descriptor) buffer (**dec\_privk\_out\_buf**), one
type-9 (X descriptor) buffer (**enc\_privk\_in\_buf**), a 16-byte KEK
(**key\_x**), a 16-byte key (**key\_y**) and a u32 (**version**).
**version** is 0 for normal keys or 1 for extended keys.

Decrypts **enc\_privk\_in\_buf** into **dec\_privk\_out\_buf** with a
key generated from **key\_x** and **key\_y**.

Used by [SSL](SSL%20services.md "wikilink")-sysmodule for TLS
client-privk.

## DecryptAesKey

Takes a 16-byte encrypted key (**enc\_key**) and two words
(**KeyGeneration** and **option**) as input. **KeyGeneration** ranges
from 0 to 2.

Decrypts **enc\_key** with a key generated from fixed **key\_x** and
**key\_y** and returns a 16-byte decrypted key (**dec\_key**).

\[2.0.0+\] Introduced same engine allocation code as for
[\#GenerateAesKey](#GenerateAesKey "wikilink").

## DecryptAesCtr

Takes a type-0x46 (B descriptor) buffer (**data\_out\_buf**), a u32
(**keyslot**), a type-0x45 (A descriptor) buffer (**data\_in\_buf**) and
a 16-byte CTR (**aes\_ctr**).

Decrypts **data\_in\_buf** into **data\_out\_buf** using the key set in
the specified **keyslot**.

\[2.0.0+\] Verifies the engine is locked by current session.

## ComputeCmac

Takes one type-9 (X descriptor) buffer (**data\_in\_buf**) and a u32
(**type?**).

Returns a 16-byte CMAC calculated over **data\_in\_buf**.

\[2.0.0+\] Verifies the engine is locked by current session.

## DecryptImportPrivkForExpMod1

Takes one type-9 (X descriptor) buffer (**enc\_privk\_in\_buf**), a
16-byte KEK (**key\_x**), a 16-byte key (**key\_y**) and a u32
(**version**). **version** is 0 for normal keys or 1 for extended keys.

Decrypts **enc\_privk\_in\_buf** with a key generated from **key\_x**
and **key\_y** and imports it for later usage.

## UnwrapRsaWrappedTitleKey

Takes 3 type-9 (X descriptor) buffers (**data\_in\_buf**,
**mod\_in\_buf** and **param0\_in\_buf**).

Decrypts **data\_in\_buf** using the private key imported with
[\#DecryptImportPrivkForExpMod1](#DecryptImportPrivkForExpMod1 "wikilink")
and the supplied **mod\_in\_buf** and **param0\_in\_buf**.

Generates and returns a 16-byte sealed titlekey.

## LoadTitleKey

Takes a u32 (**keyslot**) and a 16-byte sealed titlekey.

Sets the specified **keyslot** with the titlekey.

\[2.0.0+\] Verifies the engine is locked by current session.

## UnwrapAesWrappedTitleKey

Takes a 16-byte EKS (**Encryption Key Source**).

Returns a sealed titlekey.

## LockAesEngine

Returns the id of the engine that was locked, or 0xD01A if all engines
are busy. You need to lock an engine before using AES functions.

## UnlockAesEngine

Takes a single u32 and unlocks the engine with that id. It must be owned
by current session otherwise 0xD21A will be returned.

## GetSplWaitEvent

Returns an event handle for synchronizing with the locked AES engine.

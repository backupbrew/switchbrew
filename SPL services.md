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

| Cmd | Name                                                                          | Notes                                                                                                                                           |
| --- | ----------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| 0   | [\#GetConfig](#GetConfig "wikilink")                                          | Wrapper for [GetConfig SMC](SMC#GetConfig.md##GetConfig "wikilink").                                                                            |
| 1   | [\#UserExpMod](#UserExpMod "wikilink")                                        | Speculative name. Wrapper for [ExpMod SMC](SMC#ExpMod.md##ExpMod "wikilink").                                                                   |
| 2   | [\#GenerateAesKek](#GenerateAesKek "wikilink")                                | Wrapper for [GenerateAesKek SMC](SMC#GenerateAesKek.md##GenerateAesKek "wikilink").                                                             |
| 3   | [\#LoadAesKey](#LoadAesKey "wikilink")                                        | Wrapper for [LoadAesKey SMC](SMC#LoadAesKey.md##LoadAesKey "wikilink").                                                                         |
| 4   | [\#GenerateAesKey](#GenerateAesKey "wikilink")                                | Decrypts 0x10 bytes using AES ECB and uses [LoadAesKey SMC](SMC#LoadAesKey.md##LoadAesKey "wikilink") with a fixed Y.                           |
| 5   | [\#SetConfig](#SetConfig "wikilink")                                          | Wrapper for [SetConfig SMC](SMC#SetConfig.md##SetConfig "wikilink").                                                                            |
| 7   | [\#GetRandomBytes](#GetRandomBytes "wikilink")                                | Uses [GetRandomBytes SMC](SMC#GetRandomBytes.md##GetRandomBytes "wikilink").                                                                    |
| 9   | [\#LoadSecureExpModKey](#LoadSecureExpModKey "wikilink")                      | Speculative name. Wrapper for [LoadSecureExpModKey SMC](SMC#LoadSecureExpModKey.md##LoadSecureExpModKey "wikilink").                            |
| 10  | [\#SecureExpMod](#SecureExpMod "wikilink")                                    | Speculative name. Uses [SecureExpModSMC](SMC#SecureExpMod.md##SecureExpMod "wikilink").                                                         |
| 11  | [\#IsDevelopment](#IsDevelopment "wikilink")                                  |                                                                                                                                                 |
| 12  | [\#GenerateSpecificAesKey](#GenerateSpecificAesKey "wikilink")                | Wrapper for [GenerateSpecificAesKey SMC](SMC#GenerateSpecificAesKey.md##GenerateSpecificAesKey "wikilink").                                     |
| 13  | [\#DecryptPrivk](#DecryptPrivk "wikilink")                                    | Speculative name. Wrapper for [PrivateRsa SMC](SMC#PrivateRsa.md##PrivateRsa "wikilink").                                                       |
| 14  | [\#DecryptAesKey](#DecryptAesKey "wikilink")                                  | Decrypts 0x10 bytes using AES ECB and uses [LoadAesKey SMC](SMC#LoadAesKey.md##LoadAesKey "wikilink") with fixed X and Y.                       |
| 15  | [\#DecryptAesCtr](#DecryptAesCtr "wikilink")                                  | Wrapper for [CryptAes SMC](SMC#CryptAes.md##CryptAes "wikilink").                                                                               |
| 16  | [\#ComputeCmac](#ComputeCmac "wikilink")                                      | Wrapper for [ComputeCmac SMC](SMC#ComputeCmac.md##ComputeCmac "wikilink").                                                                      |
| 17  | [\#LoadRsaOaepKey](#LoadRsaOaepKey "wikilink")                                | Speculative name. Wrapper for [LoadRsaOaepKey SMC](SMC#LoadRsaOaepKey.md##LoadRsaOaepKey "wikilink").                                           |
| 18  | [\#UnwrapRsaOaepWrappedTitleKey](#UnwrapRsaOaepWrappedTitleKey "wikilink")    | Speculative name. Wrapper for [UnwrapRsaOaepWrappedTitleKey SMC](SMC#UnwrapRsaOaepWrappedTitleKey.md##UnwrapRsaOaepWrappedTitleKey "wikilink"). |
| 19  | [\#LoadTitleKey](#LoadTitleKey "wikilink")                                    | Wrapper for [LoadTitleKey SMC](SMC#LoadTitleKey.md##LoadTitleKey "wikilink").                                                                   |
| 20  | \[2.0.0+\] [\#UnwrapAesWrappedTitleKey](#UnwrapAesWrappedTitleKey "wikilink") | Wrapper for [UnwrapAesWrappedTitleKey SMC](SMC#UnwrapAesWrappedTitleKey.md##UnwrapAesWrappedTitleKey "wikilink").                               |
| 21  | \[2.0.0+\] [\#LockAesEngine](#LockAesEngine "wikilink")                       |                                                                                                                                                 |
| 22  | \[2.0.0+\] [\#UnlockAesEngine](#UnlockAesEngine "wikilink")                   |                                                                                                                                                 |
| 23  | \[2.0.0+\] [\#GetSplWaitEvent](#GetSplWaitEvent "wikilink")                   |                                                                                                                                                 |
| 24  | \[3.0.0+\] [\#SetSharedData](#SetSharedData "wikilink")                       |                                                                                                                                                 |
| 25  | \[3.0.0+\] [\#GetSharedData](#GetSharedData "wikilink")                       |                                                                                                                                                 |

## GetConfig

Takes a u32 (**ConfigItem**), and returns one or more u64s
(**ConfigVal**).

| ConfigItem | Name                                                                   |
| ---------- | ---------------------------------------------------------------------- |
| 1          | [\#DisableProgramVerification](#DisableProgramVerification "wikilink") |
| 2          | [\#DRAMId](#DRAMId "wikilink")                                         |
| 3          | [\#SecurityEngineIRQNumber](#SecurityEngineIRQNumber "wikilink")       |
| 4          | [\#Version](#Version "wikilink")                                       |
| 5          | [\#HardwareType](#HardwareType "wikilink")                             |
| 6          | [\#IsRetail](#IsRetail "wikilink")                                     |
| 7          | [\#IsRecoveryBoot](#IsRecoveryBoot "wikilink")                         |
| 8          | [\#DeviceId](#DeviceId "wikilink")                                     |
| 9          | \[1.0.0-4.0.0\] BootReason                                             |
| 10         | MemoryArrange                                                          |
| 11         | [\#IsDebugMode](#IsDebugMode "wikilink")                               |
| 12         | [\#KernelMemoryConfiguration](#KernelMemoryConfiguration "wikilink")   |
| 13         | [\#BatteryProfile](#BatteryProfile "wikilink")                         |
| 14         | \[4.0.0+\] [\#Unknown0](#Unknown0 "wikilink")                          |
| 15         | \[5.0.0+\] Unknown1                                                    |
| 16         | \[5.0.0+\] [\#IsT214](#IsT214 "wikilink")                              |
| 17         | \[5.0.0+\] [\#Package2Hash](#Package2Hash "wikilink")                  |

### DisableProgramVerification

[PM](Process%20Manager%20services.md "wikilink") checks this item and if
non-zero, calls fsp-pr SetEnabledProgramVerification(false).

### DRAMId

This is extracted directly from
[FUSE\_RESERVED\_ODM4](Fuse%20registers#FUSE%20RESERVED%20ODM4.md##FUSE_RESERVED_ODM4 "wikilink").

[PCV](PCV%20services.md "wikilink") configures memory profiles based on
DRAMId.

| Platform   | Version @ 40800                       | Revision | DRAMId |
| ---------- | ------------------------------------- | -------- | ------ |
| jetson-tx1 | 11\_40800\_01\_V9.8.3\_V1.6           | N/A      | N/A    |
| nx-abcb    | 10\_40800\_NoCfgVersion\_V9.8.4\_V1.6 | 0        | 0      |
| nx-abca2   | 10\_40800\_NoCfgVersion\_V9.8.7\_V1.6 | 0        | 0 or 3 |
| nx-abca2   | 10\_40800\_NoCfgVersion\_V9.8.7\_V1.6 | 1        | 4      |
| nx-abca2   | 10\_40800\_NoCfgVersion\_V9.8.7\_V1.6 | 2        | 1      |
| nx-abca2   | 10\_40800\_NoCfgVersion\_V9.8.7\_V1.6 | 3        | 2      |
|            |                                       |          |        |

nx-abcb (Copper) is the SDEV unit. Among other differences, this has
extra hardware to support HDMI output.

nx-abca2 (Icosa) hardware types are variations of the retail form
factor.

### SecurityEngineIRQNumber

SPL uses this for setting up the security engine IRQ.

### Version

The current [Package1 Maxver
Constant](Package2#Versions.md##Versions "wikilink") - 1.

### HardwareType

\[1.0.0+\] This item is obtained by checking bits 8 and 2 from
[FUSE\_RESERVED\_ODM4](Fuse%20registers#FUSE%20RESERVED%20ODM4.md##FUSE_RESERVED_ODM4 "wikilink").
It can be 0 (Icosa), 1 (Copper) or 3 (Invalid).

\[4.0.0+\] This item is obtained by checking bits 8, 2 and 16-19 from
[FUSE\_RESERVED\_ODM4](Fuse%20registers#FUSE%20RESERVED%20ODM4.md##FUSE_RESERVED_ODM4 "wikilink").
It can be 0 (Icosa), 1 (Copper), 3 (Unknown) or 4 (Invalid).

A value of 2 (Hoag?) is always mapped to 4 (Invalid).

### IsRetail

This item is obtained by checking bits 9 and 0-1 from
[FUSE\_RESERVED\_ODM4](Fuse%20registers#FUSE%20RESERVED%20ODM4.md##FUSE_RESERVED_ODM4 "wikilink").
It can be 0 (Debug), 1 (Retail) or 2 (Invalid).

### IsRecoveryBoot

Used to determine if the system is booting from SafeMode firmware.

### DeviceId

[NIM](NIM%20services.md "wikilink") checks if this item matches the
[set:cal](Settings%20services.md "wikilink") DeviceId with byte7
cleared. If they don't match, a panic is thrown.

### IsDebugMode

Kernel uses this to determine behavior of svcBreak positive arguments.
It will break instead of just force-exiting the process which is what
happens on retail.

\[2.0.0+\] This is also used with certain debug
[SVCs](SVC.md "wikilink").

\[3.0.0+\] [RO](Loader%20services.md "wikilink") checks this and if set
then skipping NRR rsa signatures is allowed.

### KernelMemoryConfiguration

Kernel reads this when setting up memory-related code. If bit0 is set,
it will memset various allocated memory-regions with 0x58, 0x59, 0x5A
('X', 'Y', 'Z') instead of zero. This allows Nintendo devs to find
uninitialized memory bugs. If bit17-16 is 0b01, the kernel assumes 6GB
of DRAM instead of 4GB.

### BatteryProfile

This tells if the TI Charger (bq24192) is active.

### IsT214

This item is obtained from
[FUSE\_RESERVED\_ODM2](Fuse%20registers#FUSE%20RESERVED%20ODM2.md##FUSE_RESERVED_ODM2 "wikilink")
if bit 11 from
[FUSE\_RESERVED\_ODM4](Fuse%20registers#FUSE%20RESERVED%20ODM4.md##FUSE_RESERVED_ODM4 "wikilink")
is set,
[FUSE\_RESERVED\_ODM0](Fuse%20registers#FUSE%20RESERVED%20ODM0.md##FUSE_RESERVED_ODM0 "wikilink")
matches 0x8E61ECAE and
[FUSE\_RESERVED\_ODM1](Fuse%20registers#FUSE%20RESERVED%20ODM1.md##FUSE_RESERVED_ODM1 "wikilink")
matches 0xF2BA3BB2.

This is speculated to be related to the new SoC T214.

### Unknown0

This item is bit 10 from
[FUSE\_RESERVED\_ODM4](Fuse%20registers#FUSE%20RESERVED%20ODM4.md##FUSE_RESERVED_ODM4 "wikilink").

### Package2Hash

This is a SHA-256 hash calculated over the
[package2](Package2.md "wikilink") image. Since the hash calculation is
an optional step in pkg2ldr, this item is only valid in recovery mode.
Otherwise, an error is returned instead.

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

## LoadRsaOaepKey

Takes one type-9 (X descriptor) buffer (**enc\_privk\_in\_buf**), a
16-byte KEK (**key\_x**), a 16-byte key (**key\_y**) and a u32
(**version**). **version** is 0 for normal keys or 1 for extended keys.

Decrypts **enc\_privk\_in\_buf** with a key generated from **key\_x**
and **key\_y** and imports it for later usage.

## UnwrapRsaOaepWrappedTitleKey

Takes one type-10 (C descriptor) buffer (**data\_out\_buf**) and 3
type-9 (X descriptor) buffers (**data\_in\_buf**, **mod\_in\_buf** and
**label\_hash\_in\_buf**).

Decrypts **data\_in\_buf** into **data\_out\_buf** using the private key
imported with
[\#UnwrapRsaOaepWrappedTitleKey](#UnwrapRsaOaepWrappedTitleKey "wikilink")
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

## LoadSecureExpModKey

Takes one type-9 (X descriptor) buffer (**enc\_privk\_in\_buf**), a
16-byte KEK (**key\_x**), a 16-byte key (**key\_y**) and a u32
(**version**). **version** is 0 for normal keys or 1 for extended keys.

Decrypts **enc\_privk\_in\_buf** with a key generated from **key\_x**
and **key\_y** and imports it for later usage.

## SecureExpMod

Takes 3 type-9 (X descriptor) buffers (**data\_in\_buf**,
**mod\_in\_buf** and **param0\_in\_buf**).

Decrypts **data\_in\_buf** using the private key imported with
[\#LoadSecureExpModKey](#LoadSecureExpModKey "wikilink") and the
supplied **mod\_in\_buf** and **param0\_in\_buf**.

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

## SetSharedData

Sets a static dword in spl .bss to the user input u32.

\[4.0.0+\] returns 0xD41A if a value has been previously set without
being [gotten](#GetSharedData "wikilink").

## GetSharedData

Returns the static dword in spl .bss that can be set via
[\#SetSharedData](#SetSharedData "wikilink").

\[4.0.0+\] returns 0xD61A if a value has not previously been set, and
unsets the value after getting it.

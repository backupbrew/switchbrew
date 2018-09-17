SPL is responsible for handling all cryptographic operations within the
system and relaying them to the [Secure Monitor](#SMC "wikilink") when
necessary.

During \[1.0.0-3.0.2\], the only existing services were "csrng" and
"spl:". However, in \[4.0.0+\] the "spl:" service was refactored and
split into new services with different permission levels. Each service
exposes the IPC command list differently in order to prevent
cryptographic operations to take place in the wrong context.

# csrng

This is "nn::spl::detail::IRandomInterface".

| Cmd | Name                                           |
| --- | ---------------------------------------------- |
| 0   | [\#GetRandomBytes](#GetRandomBytes "wikilink") |

## GetRandomBytes

Takes a type-6 buffer and fills it with random data from [GetRandomBytes
SMC](SMC#GetRandomBytes.md##GetRandomBytes "wikilink"). Same command for
"spl:" and "csrng" services.

# spl:, spl:mig, spl:fs, spl:ssl, spl:es, spl:manu

These are "nn::spl::detail::IGeneralInterface",
"nn::spl::detail::ICryptoInterface", "nn::spl::detail::IFsInterface",
"nn::spl::detail::ISslInterface", "nn::spl::detail::IEsInterface" and
"nn::spl::detail::IManuInterface"(?).

\[2.0.0+\] Where previously only one AES engine was utilized, there is
now support for 4 of them.

\[2.0.0+\] When the session closes, all AES engines that were locked are
automatically
unlocked.

| Cmd | Name                                                                          | Permissions                                      |
| --- | ----------------------------------------------------------------------------- | ------------------------------------------------ |
| 0   | [\#GetConfig](#GetConfig "wikilink")                                          | spl:, spl:mig, spl:fs, spl:ssl, spl:es, spl:manu |
| 1   | [\#UserExpMod](#UserExpMod "wikilink")                                        | spl:, spl:mig, spl:fs, spl:ssl, spl:es, spl:manu |
| 2   | [\#GenerateAesKek](#GenerateAesKek "wikilink")                                | spl:mig, spl:fs, spl:ssl, spl:es, spl:manu       |
| 3   | [\#LoadAesKey](#LoadAesKey "wikilink")                                        | spl:mig, spl:fs, spl:ssl, spl:es, spl:manu       |
| 4   | [\#GenerateAesKey](#GenerateAesKey "wikilink")                                | spl:mig, spl:fs, spl:ssl, spl:es, spl:manu       |
| 5   | [\#SetConfig](#SetConfig "wikilink")                                          | spl:, spl:mig, spl:fs, spl:ssl, spl:es, spl:manu |
| 7   | [\#GetRandomBytes](#GetRandomBytes "wikilink")                                | spl:, spl:mig, spl:fs, spl:ssl, spl:es, spl:manu |
| 9   | [\#LoadSecureExpModKey](#LoadSecureExpModKey "wikilink")                      | spl:fs                                           |
| 10  | [\#SecureExpMod](#SecureExpMod "wikilink")                                    | spl:fs                                           |
| 11  | [\#IsDevelopment](#IsDevelopment "wikilink")                                  | spl:, spl:mig, spl:fs, spl:ssl spl:es, spl:manu  |
| 12  | [\#GenerateSpecificAesKey](#GenerateSpecificAesKey "wikilink")                | spl:fs                                           |
| 13  | [\#DecryptRsaPrivateKey](#DecryptRsaPrivateKey "wikilink")                    | spl:ssl, spl:es, spl:manu                        |
| 14  | [\#DecryptAesKey](#DecryptAesKey "wikilink")                                  | spl:mig, spl:fs, spl:ssl, spl:es, spl:manu       |
| 15  | [\#DecryptAesCtr](#DecryptAesCtr "wikilink")                                  | spl:mig, spl:fs, spl:ssl, spl:es, spl:manu       |
| 16  | [\#ComputeCmac](#ComputeCmac "wikilink")                                      | spl:mig, spl:fs, spl:ssl, spl:es, spl:manu       |
| 17  | [\#LoadRsaOaepKey](#LoadRsaOaepKey "wikilink")                                | spl:es                                           |
| 18  | [\#UnwrapRsaOaepWrappedTitleKey](#UnwrapRsaOaepWrappedTitleKey "wikilink")    | spl:es                                           |
| 19  | [\#LoadTitleKey](#LoadTitleKey "wikilink")                                    | spl:fs                                           |
| 20  | \[2.0.0+\] [\#UnwrapAesWrappedTitleKey](#UnwrapAesWrappedTitleKey "wikilink") | spl:es                                           |
| 21  | \[2.0.0+\] [\#LockAesEngine](#LockAesEngine "wikilink")                       | spl:mig, spl:fs, spl:ssl, spl:es, spl:manu       |
| 22  | \[2.0.0+\] [\#UnlockAesEngine](#UnlockAesEngine "wikilink")                   | spl:mig, spl:fs, spl:ssl, spl:es, spl:manu       |
| 23  | \[2.0.0+\] [\#GetSplWaitEvent](#GetSplWaitEvent "wikilink")                   | spl:mig, spl:fs, spl:ssl, spl:es, spl:manu       |
| 24  | \[3.0.0+\] [\#SetSharedData](#SetSharedData "wikilink")                       | spl:, spl:mig, spl:fs, spl:ssl, spl:es, spl:manu |
| 25  | \[3.0.0+\] [\#GetSharedData](#GetSharedData "wikilink")                       | spl:, spl:mig, spl:fs, spl:ssl, spl:es, spl:manu |
| 26  | \[5.0.0+\] ImportSslRsaKey                                                    | spl:ssl                                          |
| 27  | \[5.0.0+\] SecureExpModWithSslKey                                             | spl:ssl                                          |
| 28  | \[5.0.0+\] ImportEsRsaKey                                                     | spl:es                                           |
| 29  | \[5.0.0+\] SecureExpModWithEsKey                                              | spl:es                                           |
| 30  | \[5.0.0+\] EncryptManuRsaKeyForImport                                         | spl:manu                                         |
| 31  | \[5.0.0+\] GetPackage2Hash                                                    | spl:fs                                           |

## GetConfig

Wrapper for [GetConfig SMC](SMC#GetConfig.md##GetConfig "wikilink").

Takes a u32 (**ConfigItem**), and returns one or more u64s
(**ConfigVal**).

## UserExpMod

Wrapper for [ExpMod SMC](SMC#ExpMod.md##ExpMod "wikilink").

Takes one type-10 (C descriptor) buffer (**data\_out\_buf**) and 3
type-9 (X descriptor) buffers (**data\_in\_buf**, **exp\_in\_buf** and
**mod\_in\_buf**).

Performs asymmetric crypto with user supplied modulus and exponent.

## GenerateAesKek

Wrapper for [GenerateAesKek
SMC](SMC#GenerateAesKek.md##GenerateAesKek "wikilink").

Takes a 16-byte EKS (**Encryption Key Source**) and two words
(**KeyGeneration** and **option**) as input.

Returns a scrambled sealed KEK (**Key Encryption Key** used as
**key\_x**).

## LoadAesKey

Wrapper for [LoadAesKey SMC](SMC#LoadAesKey.md##LoadAesKey "wikilink").

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

Generates a new key by decrypting (AES-ECB) **enc\_key** with a key
generated from the supplied **key\_x** and a fixed **key\_y** set with
[LoadAesKey SMC](SMC#LoadAesKey.md##LoadAesKey "wikilink").

\[2.0.0+\] Previously, it always used engine 0. Now it tries to allocate
an engine to be used and returns 0xD01A if they're all busy. When the
command is done, the engine is released.

## SetConfig

Wrapper for [SetConfig SMC](SMC#SetConfig.md##SetConfig "wikilink").

Takes a u32 (**ConfigItem**) and a u64 (**ConfigVal**).

| ConfigItem | Name           |
| ---------- | -------------- |
| 13         | BatteryProfile |

Any other **ConfigItem**, besides 13, can't be set.

## LoadSecureExpModKey

Wrapper for [LoadSecureExpModKey
SMC](SMC#LoadSecureExpModKey.md##LoadSecureExpModKey "wikilink").

Takes one type-9 (X descriptor) buffer (**enc\_privk\_in\_buf**), a
16-byte KEK (**key\_x**), a 16-byte key (**key\_y**) and a u32
(**version**). **version** is 0 for normal keys or 1 for extended keys.

Decrypts **enc\_privk\_in\_buf** with a key generated from **key\_x**
and **key\_y** and imports it for later usage.

\[5.0.0+\] This now calls [EncryptRsaKeyForImport
SMC](SMC#EncryptRsaKeyForImport.md##EncryptRsaKeyForImport "wikilink")
instead.

## SecureExpMod

Takes 3 type-9 (X descriptor) buffers (**data\_in\_buf**,
**mod\_in\_buf** and **param0\_in\_buf**).

Uses [SecureExpMod SMC](SMC#SecureExpMod.md##SecureExpMod "wikilink") to
decrypt **data\_in\_buf** using the private key imported with
[\#LoadSecureExpModKey](#LoadSecureExpModKey "wikilink") and the
supplied **mod\_in\_buf** and **param0\_in\_buf**.

Generates and returns a 16-byte sealed titlekey.

## IsDevelopment

No input params.

Uses [\#GetConfig](#GetConfig "wikilink") internally with id=6. Returns
true if output from that is 0, or if the SMC returned error 2.

Returns an u8 flag for whether the system is devunit. Output flag is 0
on retail.

## GenerateSpecificAesKey

Wrapper for [GenerateSpecificAesKey
SMC](SMC#GenerateSpecificAesKey.md##GenerateSpecificAesKey "wikilink").

Takes a 16-byte seed (**key\_seed**) and two words (**KeyGeneration**
and **option**) as input.

Returns a scrambled key (**key\_a**).

## DecryptRsaPrivateKey

Wrapper for [DecryptRsaPrivateKey
SMC](SMC#DecryptRsaPrivateKey.md##DecryptRsaPrivateKey "wikilink").

Takes one type-10 (C descriptor) buffer (**dec\_privk\_out\_buf**), one
type-9 (X descriptor) buffer (**enc\_privk\_in\_buf**), a 16-byte KEK
(**key\_x**), a 16-byte key (**key\_y**) and a u32 (**version**).
**version** is 0 for normal keys or 1 for extended keys.

Decrypts **enc\_privk\_in\_buf** into **dec\_privk\_out\_buf** with a
key generated from **key\_x** and **key\_y**.

Used by [SSL](SSL%20services.md "wikilink")-sysmodule for TLS
client-privk.

\[5.0.0+\] This now calls [DecryptOrImportRsaKey
SMC](SMC#DecryptOrImportRsaKey.md##DecryptOrImportRsaKey "wikilink")
instead.

## DecryptAesKey

Takes a 16-byte encrypted key (**enc\_key**) and two words
(**KeyGeneration** and **option**) as input.

Decrypts (AES-ECB) **enc\_key** with a key generated from fixed
**key\_x** and **key\_y** set with [LoadAesKey
SMC](SMC#LoadAesKey.md##LoadAesKey "wikilink") and returns a 16-byte
decrypted key (**dec\_key**).

\[2.0.0+\] Introduced same engine allocation code as for
[\#GenerateAesKey](#GenerateAesKey "wikilink").

## DecryptAesCtr

Takes a type-0x46 (B descriptor) buffer (**data\_out\_buf**), a u32
(**keyslot**), a type-0x45 (A descriptor) buffer (**data\_in\_buf**) and
a 16-byte CTR (**aes\_ctr**).

Uses [CryptAes SMC](SMC#CryptAes.md##CryptAes "wikilink") to decrypt
**data\_in\_buf** into **data\_out\_buf**, using the key set in the
specified **keyslot**.

\[2.0.0+\] Verifies the engine is locked by current session.

## ComputeCmac

Wrapper for [ComputeCmac
SMC](SMC#ComputeCmac.md##ComputeCmac "wikilink").

Takes one type-9 (X descriptor) buffer (**data\_in\_buf**) and a u32
(**type?**).

Returns a 16-byte CMAC calculated over **data\_in\_buf**.

\[2.0.0+\] Verifies the engine is locked by current session.

## LoadRsaOaepKey

Wrapper for [LoadRsaOaepKey
SMC](SMC#LoadRsaOaepKey.md##LoadRsaOaepKey "wikilink").

Takes one type-9 (X descriptor) buffer (enc\_privk\_in\_buf), a 16-byte
KEK (key\_x), a 16-byte key (key\_y) and a u32 (version). version is 0
for normal keys or 1 for extended keys.

Decrypts enc\_privk\_in\_buf with a key generated from key\_x and key\_y
and imports it for later usage.

## UnwrapRsaOaepWrappedTitleKey

Wrapper for [UnwrapRsaOaepWrappedTitleKey
SMC](SMC#UnwrapRsaOaepWrappedTitleKey.md##UnwrapRsaOaepWrappedTitleKey "wikilink").

Takes one type-10 (C descriptor) buffer (**data\_out\_buf**) and 3
type-9 (X descriptor) buffers (**data\_in\_buf**, **mod\_in\_buf** and
**label\_hash\_in\_buf**).

Decrypts **data\_in\_buf** into **data\_out\_buf** using the private key
imported with [\#LoadRsaOaepKey](#LoadRsaOaepKey "wikilink") and the
supplied **mod\_in\_buf**. Afterwards, verifies RSA-OAEP encoding using
**label\_hash\_in\_buf**.

Returns an u32 (**dec\_data\_size**).

## LoadTitleKey

Wrapper for [LoadTitleKey
SMC](SMC#LoadTitleKey.md##LoadTitleKey "wikilink").

Takes a u32 (**keyslot**) and a 16-byte sealed titlekey.

Sets the specified **keyslot** with the titlekey.

\[2.0.0+\] Verifies the engine is locked by current session.

## UnwrapAesWrappedTitleKey

Wrapper for [UnwrapAesWrappedTitleKey
SMC](SMC#UnwrapAesWrappedTitleKey.md##UnwrapAesWrappedTitleKey "wikilink").

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

[Category:Services](Category:Services "wikilink")

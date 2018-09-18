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

SMC arguments are passed using registers X0-X7 with X0 always sending
the call sub-id and returning the result of the call.

## ID 0

Functions exposed to user-mode processes using
[svcCallSecureMonitor](SVC.md "wikilink").

| Sub-ID                     | Name                                                                       | In | Out |
| -------------------------- | -------------------------------------------------------------------------- | -- | --- |
| 0xC3000401                 | SetConfig                                                                  |    |     |
| 0xC3000002                 | GetConfig (Same as ID 1, Sub-ID 4)                                         |    |     |
| 0xC3000003                 | CheckStatus                                                                |    |     |
| 0xC3000404                 | GetResult                                                                  |    |     |
| 0xC3000E05                 | ExpMod                                                                     |    |     |
| 0xC3000006                 | GetRandomBytes (Same as ID 1, Sub-ID 5)                                    |    |     |
| 0xC3000007                 | [\#GenerateAesKek](#GenerateAesKek "wikilink")                             |    |     |
| 0xC3000008                 | [\#LoadAesKey](#LoadAesKey "wikilink")                                     |    |     |
| 0xC3000009                 | [\#CryptAes](#CryptAes "wikilink")                                         |    |     |
| 0xC300000A                 | [\#GenerateSpecificAesKey](#GenerateSpecificAesKey "wikilink")             |    |     |
| 0xC300040B                 | [\#ComputeCmac](#ComputeCmac "wikilink")                                   |    |     |
| \[1.0.0-4.1.0\] 0xC300100C | [\#LoadRsaOaepKey](#LoadRsaOaepKey "wikilink")                             |    |     |
| \[5.0.0+\] 0xC300D60C      | [\#EncryptRsaKeyForImport](#EncryptRsaKeyForImport "wikilink")             |    |     |
| \[1.0.0-4.1.0\] 0xC300100D | [\#DecryptRsaPrivateKey](#DecryptRsaPrivateKey "wikilink")                 |    |     |
| \[5.0.0\] 0xC300100D       | [\#DecryptOrImportRsaKey](#DecryptOrImportRsaKey "wikilink")               |    |     |
| \[1.0.0-4.1.0\] 0xC300100E | [\#LoadSecureExpModKey](#LoadSecureExpModKey "wikilink")                   |    |     |
| 0xC300060F                 | [\#SecureExpMod](#SecureExpMod "wikilink")                                 |    |     |
| 0xC3000610                 | [\#UnwrapRsaOaepWrappedTitleKey](#UnwrapRsaOaepWrappedTitleKey "wikilink") |    |     |
| 0xC3000011                 | [\#LoadTitleKey](#LoadTitleKey "wikilink")                                 |    |     |
| 0xC3000012                 | \[2.0.0+\] UnwrapAesWrappedTitleKey                                        |    |     |

The overall concept here is the following:

  - All key material (AES and RSA) is stored in userspace, but it's
    encrypted with random AES kek's ("key encryption keys").
  - Each kek is generated as a function of an access key (picked at
    random).
  - The kek is generated differently depending on the
    [\#CryptoUsecase](#CryptoUsecase "wikilink") the key is used for.
      - This means: Each key is "locked" to the
        [\#CryptoUsecase](#CryptoUsecase "wikilink") it was designated
        for.
      - You can use a key for a different usecase, but you will only get
        garbage output.
  - After the kek has been generated, it is wrapped with a
    session-specific key and given back to userspace.
      - This means: Plaintext kek keys never leave TrustZone.
      - Further, this means: Actual AES/RSA keys never leave TrustZone.

Note: The [CryptoUsecase\_TitleKey](#enum_CryptoUsecase "wikilink")
represents a RSA wrapped AES key.

### GenerateAesKek

Takes an "access key" as input, an
[\#enum\_CryptoUsecase](#enum_CryptoUsecase "wikilink").

Returns a session-unique kek for said usecase.

### LoadAesKey

Takes a session kek created with
[\#GenerateAesKek](#GenerateAesKek "wikilink"), and a wrapped AES key.

The session kek must have been created with
[CryptoUsecase\_Aes](#enum_CryptoUsecase "wikilink").

### CryptAes

Encrypts/decrypts using Aes (CTR and CBC).

Key must be set prior using one of the
[\#LoadAesKey](#LoadAesKey "wikilink"),
[\#GenerateSpecificAesKey](#GenerateSpecificAesKey "wikilink") or
[\#LoadRsaWrappedAesKey](#LoadRsaWrappedAesKey "wikilink") commands.

### GenerateSpecificAesKey

Todo: This one seems unrelated to
[\#enum\_CryptoUsecase](#enum_CryptoUsecase "wikilink").

### LoadRsaOaepKey

Takes a session kek created with
[\#GenerateAesKek](#GenerateAesKek "wikilink"), a wrapped AES key, and a
wrapped RSA private key.

The session kek must have been created with
[CryptoUsecase\_RsaOaep](#enum_CryptoUsecase "wikilink").

This function was removed in [5.0.0](5.0.0.md "wikilink"), and replaced
with [\#EncryptRsaKeyForImport](#EncryptRsaKeyForImport "wikilink").

### EncryptRsaKeyForImport

Takes in two session keks created with
[\#GenerateAesKek](#GenerateAesKek "wikilink"), two wrapped AES keys, an
enum member, and a wrapped RSA private key.

Decrypts and validates the wrapped RSA private key with the first
kek/wrapped key, and re-encrypts it with the second if valid.

The re-encrypted key is then passed to the user, for use with
[\#DecryptOrImportRsaKey](#DecryptOrImportRsaKey "wikilink").

### DecryptRsaPrivateKey

Takes a session kek created with
[\#GenerateAesKek](#GenerateAesKek "wikilink"), a wrapped AES key, an
enum member, and a wrapped RSA private key.

The session kek must have been created with
[CryptoUsecase\_RsaPrivate](#enum_CryptoUsecase "wikilink").

\[4.0.0+\] The SMC handler when certain conditions pass and
SMC\_ID==0xC300100D now returns error 0x6 instead of calling the handler
funcptr.

### DecryptOrImportRsaKey

This function replaced
[\#DecryptRsaPrivateKey](#DecryptRsaPrivateKey "wikilink") in
[5.0.0](5.0.0.md "wikilink"), adding an additional enum member argument.

This SMC extends DecryptRsaPrivateKey's original functionality to enable
importing private keys into the security engine instead of decrypting
them, when certain enum members are passed.

### LoadSecureExpModKey

Takes a session kek created with
[\#GenerateAesKek](#GenerateAesKek "wikilink"), and a wrapped RSA key.

The session kek must have been created with
[CryptoUsecase\_RsaSecureExpMod](#enum_CryptoUsecase "wikilink").

This function was removed in [5.0.0](5.0.0.md "wikilink"), and replaced
with [\#EncryptRsaKeyForImport](#EncryptRsaKeyForImport "wikilink").

### SecureExpMod

Performs an Exp Mod operation using an exponent previously loaded with
the [\#LoadSecureExpModKey](#LoadSecureExpModKey "wikilink") command.

### UnwrapRsaOaepWrappedTitleKey

Takes an Rsa-Oaep-wrapped TitleKey, an RSA Public Key, and a label hash.

Performs an Exp Mod operation using an exponent previously loaded with
the [\#LoadRsaOaepKey](#LoadRsaOaepKey "wikilink") command, and then
validates/extracts a Titlekey from the resulting message.

Returns a session-unique AES key especially for use in
[\#LoadTitleKey](#LoadTitleKey "wikilink").

### LoadTitleKey

Takes a session-unique AES key from
[\#UnwrapAesWrappedTitleKey](#UnwrapAesWrappedTitleKey "wikilink") or
[\#UnwrapRsaOaepWrappedTitleKey](#UnwrapRsaOaepWrappedTitleKey "wikilink").

### enum CryptoUsecase

| Value | Name                           |
| ----- | ------------------------------ |
| 0     | CryptoUsecase\_Aes             |
| 1     | CryptoUsecase\_RsaPrivate      |
| 2     | CryptoUsecase\_RsaSecureExpMod |
| 3     | CryptoUsecase\_RsaOaep         |

## ID 1

Functions exposed to the kernel
internally.

| Sub-ID     | Name                                                                    | In                                                                        | Out                                         |
| ---------- | ----------------------------------------------------------------------- | ------------------------------------------------------------------------- | ------------------------------------------- |
| 0xC4000001 | [\#CpuSuspend](#CpuSuspend "wikilink")                                  | X1=power\_state, X2=entrypoint\_addr, X3=context\_id                      | None                                        |
| 0x84000002 | [\#CpuOff](#CpuOff "wikilink")                                          | None                                                                      | None                                        |
| 0xC4000003 | [\#CpuOn](#CpuOn "wikilink")                                            | X1=target\_cpu, X2=entrypoint\_addr, X3=context\_id, X4,X5,X6,X7=0        | X0=result                                   |
| 0xC3000004 | [\#GetConfig](#GetConfig "wikilink") (Same as ID 0, Sub-ID 2)           | W1=config\_item, X2,X3,X4,X5,X6,X7=0                                      | X0=result, X1,X2,X3,X4=config\_val          |
| 0xC3000005 | [\#GetRandomBytes](#GetRandomBytes "wikilink") (Same as ID 0, Sub-ID 6) | X1=size, X2,X3,X4,X5,X6,X7=0                                              | X0=result, X1,X2,X3,X4,X5,X6,X7=rand\_bytes |
| 0xC3000006 | [\#Panic](#Panic "wikilink")                                            | W1=panic\_color, X2,X3,X4,X5,X6,X7=0                                      | X0=result                                   |
| 0xC3000007 | \[2.0.0+\] [\#ConfigureCarveout](#ConfigureCarveout "wikilink")         | X1=carveout\_index, X2=region\_phys\_addr, X3=region\_size, X4,X5,X6,X7=0 | X0=result                                   |
| 0xC3000008 | \[2.0.0+\] [\#ReadWriteRegister](#ReadWriteRegister "wikilink")         | X1=reg\_addr, W2=rw\_mask, W3=in\_val, X4,X5,X6,X7=0                      | X0=result, W1=out\_val                      |

### CpuSuspend

Standard ARM PCSI SMC. Suspends the CPU (CPU0).

The kernel calls this SMC on shutdown with **power\_state** set to
0x0201001B (power level: 0x02==system; power type: 0x01==powerdown; ID:
0x1B).

### CpuOff

Standard ARM PCSI SMC. Turns off the CPU (CPU1, CPU2 or CPU3).

### CpuOn

Standard ARM PCSI SMC. Turns on the CPU (CPU1, CPU2 or CPU3).

### GetConfig

Takes a **config\_item** and returns an associated
**config\_val**.

| ConfigItem | Name                                                                   |
| ---------- | ---------------------------------------------------------------------- |
| 1          | [\#DisableProgramVerification](#DisableProgramVerification "wikilink") |
| 2          | [\#DramId](#DramId "wikilink")                                         |
| 3          | [\#SecurityEngineIrqNumber](#SecurityEngineIrqNumber "wikilink")       |
| 4          | [\#Version](#Version "wikilink")                                       |
| 5          | [\#HardwareType](#HardwareType "wikilink")                             |
| 6          | [\#IsRetail](#IsRetail "wikilink")                                     |
| 7          | [\#IsRecoveryBoot](#IsRecoveryBoot "wikilink")                         |
| 8          | [\#DeviceId](#DeviceId "wikilink")                                     |
| 9          | \[1.0.0-4.0.0\] [\#BootReason](#BootReason "wikilink")                 |
| 10         | [\#MemoryArrange](#MemoryArrange "wikilink")                           |
| 11         | [\#IsDebugMode](#IsDebugMode "wikilink")                               |
| 12         | [\#UnitConfiguration](#UnitConfiguration "wikilink")                   |
| 13         | [\#IsChargerHiZModeEnabled](#IsChargerHiZModeEnabled "wikilink")       |
| 14         | \[4.0.0+\] [\#IsKiosk](#IsKiosk "wikilink")                            |
| 15         | \[5.0.0+\] [\#NewHardwareType](#NewHardwareType "wikilink")            |
| 16         | \[5.0.0+\] [\#NewKeyGeneration](#NewKeyGeneration "wikilink")          |
| 17         | \[5.0.0+\] [\#Package2Hash](#Package2Hash "wikilink")                  |

#### DisableProgramVerification

[PM](Process%20Manager%20services.md "wikilink") checks this item and if
non-zero, calls fsp-pr SetEnabledProgramVerification(false).

#### DramId

This is extracted directly from
[FUSE\_RESERVED\_ODM4](Fuse%20registers#FUSE%20RESERVED%20ODM4.md##FUSE_RESERVED_ODM4 "wikilink").

| Value | Description                                 |
| ----- | ------------------------------------------- |
| 0     | DramId\_EristaIcosaSamsung4gb               |
| 1     | DramId\_EristaIcosaHynix4gb                 |
| 2     | DramId\_EristaIcosaMicron4gb                |
| 3     | Reserved                                    |
| 4     | DramId\_EristaIcosaSamsung6gb               |
| 5     | \[5.0.0+\] Reserved                         |
| 6     | \[5.0.0+\] Reserved                         |
| 7     | \[5.0.0+\] DramId\_MarikoIowax1x2Samsung4gb |
| 8     | \[5.0.0+\] DramId\_MarikoIowaSamsung4gb     |
| 9     | \[5.0.0+\] DramId\_MarikoIowaSamsung8gb     |
| 10    | \[5.0.0+\] Reserved                         |
| 11    | \[5.0.0+\] Reserved                         |
| 12    | \[5.0.0+\] DramId\_MarikoHoagSamsung4gb     |
| 13    | \[5.0.0+\] DramId\_MarikoHoagSamsung8gb     |

[PCV](PCV%20services.md "wikilink") configures memory profiles based on
DramId.

| Platform   | DramId                                        | Version                                |
| ---------- | --------------------------------------------- | -------------------------------------- |
| jetson-tx1 | N/A                                           | 11\_40800\_01\_V9.8.3\_V1.6            |
| nx-abcb    | EristaIcosaSamsung4gb                         | 10\_40800\_NoCfgVersion\_V9.8.7\_V1.6  |
| nx-abcb    | EristaIcosaMicron4gb                          | 10\_40800\_NoCfgVersion\_V9.8.4\_V1.6  |
| nx-abcb    | EristaIcosaHynix4gb                           | 10\_40800\_NoCfgVersion\_V9.8.4\_V1.6  |
| nx-abca2   | EristaIcosaSamsung4gb or EristaIcosaMicron4gb | 10\_40800\_NoCfgVersion\_V9.8.7\_V1.6  |
| nx-abca2   | EristaIcosaHynix4gb                           | 10\_40800\_NoCfgVersion\_V9.8.7\_V1.6  |
| nx-abca2   | EristaIcosaSamsung6gb                         | 10\_40800\_NoCfgVersion\_V9.8.7\_V1.6  |
| nx-abca2   | MarikoIowax1x2Samsung4gb                      | 01\_204000\_NoCfgVersion\_V0.3.1\_V2.0 |
| nx-abca2   | MarikoIowaSamsung4gb or MarikoHoagSamsung4gb  | 01\_204000\_NoCfgVersion\_V0.3.1\_V2.0 |
| nx-abca2   | MarikoIowaSamsung8gb or MarikoHoagSamsung8gb  | 01\_204000\_NoCfgVersion\_V0.4.2\_V2.0 |

nx-abcb (Copper) is the SDEV unit. Among other differences, this has
extra hardware to support HDMI output.

nx-abca2 (Icosa) hardware types are variations of the retail form
factor.

#### SecurityEngineIrqNumber

SPL uses this for setting up the security engine IRQ.

#### Version

The current [Package1 Maxver
Constant](Package2#Versions.md##Versions "wikilink") - 1.

#### HardwareType

\[1.0.0+\] This item is obtained by checking bits 8 and 2 from
[FUSE\_RESERVED\_ODM4](Fuse%20registers#FUSE%20RESERVED%20ODM4.md##FUSE_RESERVED_ODM4 "wikilink").
It can be 0 (Icosa), 1 (Copper) or 3 (Invalid).

\[4.0.0+\] This item is obtained by checking bits 8, 2 and 16-19 from
[FUSE\_RESERVED\_ODM4](Fuse%20registers#FUSE%20RESERVED%20ODM4.md##FUSE_RESERVED_ODM4 "wikilink").
It can be 0 (Icosa), 1 (Copper), 3 (Mariko) or 4 (Invalid).

A value of 2 (Hoag?) is always mapped to 4 (Invalid).

#### IsRetail

This item is obtained by checking bits 9 and 0-1 from
[FUSE\_RESERVED\_ODM4](Fuse%20registers#FUSE%20RESERVED%20ODM4.md##FUSE_RESERVED_ODM4 "wikilink").
It can be 0 (Debug), 1 (Retail) or 2 (Invalid).

#### IsRecoveryBoot

Used to determine if the system is booting from SafeMode firmware.

#### DeviceId

[NIM](NIM%20services.md "wikilink") checks if this item matches the
[set:cal](Settings%20services.md "wikilink") DeviceId with byte7
cleared. If they don't match, a panic is thrown.

#### BootReason

Used to determine how the system booted.

#### MemoryArrange

[PM](Process%20Manager%20services.md "wikilink") uses this item for
selecting the appropriate size for each
[LimitableResource\_Memory](SVC#LimitableResource.md##LimitableResource "wikilink").

#### IsDebugMode

Kernel uses this to determine behavior of svcBreak positive arguments.
It will break instead of just force-exiting the process which is what
happens on retail.

\[2.0.0+\] This is also used with certain debug
[SVCs](SVC.md "wikilink").

\[3.0.0+\] [RO](Loader%20services.md "wikilink") checks this and if set
then skipping NRR rsa signatures is allowed.

The value of this field is loaded from
[BootConfig](BootConfig.md "wikilink") unsigned-config+0x10 u8 bit1.

#### UnitConfiguration

Kernel reads this when setting up memory-related code. If bit0 is set,
it will memset various allocated memory-regions with 0x58, 0x59, 0x5A
('X', 'Y', 'Z') instead of zero. This allows Nintendo devs to find
uninitialized memory bugs. If bit17-16 is 0b01, the kernel assumes 6GB
of DRAM instead of 4GB.

bit1 and bit2 are boolean values. If bit15-8 is zero, kernel will loop
forever without calling smcPanic, nonzero smcPanics with 0xf00 and then
loops.

#### IsChargerHiZModeEnabled

This tells if the TI Charger (bq24192) is active.

#### NewKeyGeneration

This item is obtained from
[FUSE\_RESERVED\_ODM2](Fuse%20registers#FUSE%20RESERVED%20ODM2.md##FUSE_RESERVED_ODM2 "wikilink")
if bit 11 from
[FUSE\_RESERVED\_ODM4](Fuse%20registers#FUSE%20RESERVED%20ODM4.md##FUSE_RESERVED_ODM4 "wikilink")
is set,
[FUSE\_RESERVED\_ODM0](Fuse%20registers#FUSE%20RESERVED%20ODM0.md##FUSE_RESERVED_ODM0 "wikilink")
matches 0x8E61ECAE and
[FUSE\_RESERVED\_ODM1](Fuse%20registers#FUSE%20RESERVED%20ODM1.md##FUSE_RESERVED_ODM1 "wikilink")
matches 0xF2BA3BB2.

\[5.0.0+\] [FS](Filesystem%20services.md "wikilink") can now use this
value for the **KeyGeneration** parameter when calling
[GenerateAesKek](#GenerateAesKek "wikilink") during
"GetBisEncryptionKey".

#### IsKiosk

This item is bit 10 from
[FUSE\_RESERVED\_ODM4](Fuse%20registers#FUSE%20RESERVED%20ODM4.md##FUSE_RESERVED_ODM4 "wikilink").

\[4.0.0+\] [Settings](Settings%20services.md "wikilink") uses this value
to overwrite the quest flag from
[GetQuestFlag](Settings%20services#set:sys.md##set:sys "wikilink"). This
is used to detect if a Switch is a kiosk unit for display at retail
stores.

#### NewHardwareType

This item is currently hardcoded to 0.

\[5.0.0+\] [PCV](PCV%20services.md "wikilink") overrides the value from
[HardwareType](#HardwareType "wikilink") and configures PMIC devices
with this item.

| Value | Devices                                        |
| ----- | ---------------------------------------------- |
| 0     | max77620\_sd0, max77621\_cpu and max77621\_gpu |
| 1     | max77620\_sd0, max77812\_cpu and max77812\_gpu |
| 2     | max77620\_sd0, max77812\_cpu and max77812\_gpu |

#### Package2Hash

This is a SHA-256 hash calculated over the
[package2](Package2.md "wikilink") image. Since the hash calculation is
an optional step in pkg2ldr, this item is only valid in recovery mode.
Otherwise, an error is returned instead.

### GetRandomBytes

Takes a **size** and returns **rand\_bytes**.

The kernel limits **size** to 0x38 (for fitting in return registers).

### Panic

Issues a system panic.

The kernel always calls this with **panic\_color** set to 0xF00.

### ConfigureCarveout

Configures memory controller carveout regions.

If **carveout\_index** is 0, **region\_phys\_addr** and **region\_size**
are used to configure **MC\_SECURITY\_CARVEOUT4**. If
**carveout\_index** is 1, **region\_phys\_addr** and **region\_size**
are used to configure **MC\_SECURITY\_CARVEOUT5**. Any other
**carveout\_index** values are invalid.

The kernel calls this with **carveout\_index** set to 0,
**region\_phys\_addr** set to 0x80060000 and **region\_size** set to a
dynamically calculated size which covers all the kernel and built-in
sysmodules' DRAM regions.

### ReadWriteRegister

Relays
[svcReadWriteRegister](SVC#svcReadWriteRegister.md##svcReadWriteRegister "wikilink")
to the Secure Monitor.

# Errors

| Value | Description   |
| ----- | ------------- |
| 2     | Invalid input |
| 3     | Busy          |

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
[svcCallSecureMonitor](SVC.md "wikilink"). SMCs should be called from
CPUID 3 (where SPL runs).

| Sub-ID                     | Name                                                                       | In | Out |
| -------------------------- | -------------------------------------------------------------------------- | -- | --- |
| 0xC3000401                 | SetConfig                                                                  |    |     |
| 0xC3000002                 | GetConfig (Same as ID 1, Sub-ID 4)                                         |    |     |
| 0xC3000003                 | GetResult                                                                  |    |     |
| 0xC3000404                 | GetResultData                                                              |    |     |
| 0xC3000E05                 | ExpMod                                                                     |    |     |
| 0xC3000006                 | GenerateRandomBytes (Same as ID 1, Sub-ID 5)                               |    |     |
| 0xC3000007                 | [\#GenerateAesKek](#GenerateAesKek "wikilink")                             |    |     |
| 0xC3000008                 | [\#LoadAesKey](#LoadAesKey "wikilink")                                     |    |     |
| 0xC3000009                 | [\#ComputeAes](#ComputeAes "wikilink")                                     |    |     |
| 0xC300000A                 | [\#GenerateSpecificAesKey](#GenerateSpecificAesKey "wikilink")             |    |     |
| 0xC300040B                 | [\#ComputeCmac](#ComputeCmac "wikilink")                                   |    |     |
| \[1.0.0-4.1.0\] 0xC300100C | [\#ImportEsKey](#ImportEsKey "wikilink")                                   |    |     |
| \[5.0.0+\] 0xC300D60C      | [\#ReEncryptRsaPrivateKey](#ReEncryptRsaPrivateKey "wikilink")             |    |     |
| \[1.0.0-4.1.0\] 0xC300100D | [\#DecryptRsaPrivateKey](#DecryptRsaPrivateKey "wikilink")                 |    |     |
| \[5.0.0+\] 0xC300100D      | [\#DecryptOrImportRsaPrivateKey](#DecryptOrImportRsaPrivateKey "wikilink") |    |     |
| \[1.0.0-4.1.0\] 0xC300100E | [\#ImportLotusKey](#ImportLotusKey "wikilink")                             |    |     |
| 0xC300060F                 | [\#StorageExpMod](#StorageExpMod "wikilink")                               |    |     |
| 0xC3000610                 | [\#UnwrapTitleKey](#UnwrapTitleKey "wikilink")                             |    |     |
| 0xC3000011                 | [\#LoadTitleKey](#LoadTitleKey "wikilink")                                 |    |     |
| 0xC3000012                 | \[2.0.0+\] [\#UnwrapCommonTitleKey](#UnwrapCommonTitleKey "wikilink")      |    |     |

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

### GenerateAesKek

Takes an "access key" as input, an
[\#enum\_CryptoUsecase](#enum_CryptoUsecase "wikilink").

Returns a session-unique kek for said usecase.

### LoadAesKey

Takes a session kek created with
[\#GenerateAesKek](#GenerateAesKek "wikilink"), and a wrapped AES key.

The session kek must have been created with
[CryptoUsecase\_Aes](#enum_CryptoUsecase "wikilink").

### ComputeAes

Encrypts/decrypts using AES (CTR and CBC). Takes an
[\#enum\_CipherMode](#enum_CipherMode "wikilink").

Key must be set prior using one of the
[\#LoadAesKey](#LoadAesKey "wikilink") or
[\#GenerateSpecificAesKey](#GenerateSpecificAesKey "wikilink") commands.

### GenerateSpecificAesKey

Takes a wrapped AES key and decrypts it using static data.

### ComputeCmac

Calculates CMAC over input data.

### ImportEsKey

Takes a session kek created with
[\#GenerateAesKek](#GenerateAesKek "wikilink"), a wrapped AES key, and a
wrapped RSA private key.

The session kek must have been created with
[CryptoUsecase\_TitleKey](#enum_CryptoUsecase "wikilink").

\[5.0.0\] This function was removed and replaced with
[\#ReEncryptRsaPrivateKey](#ReEncryptRsaPrivateKey "wikilink").

### ReEncryptRsaPrivateKey

Takes in two session keks created with
[\#GenerateAesKek](#GenerateAesKek "wikilink"), two wrapped AES keys, an
enum member, and a wrapped RSA private key.

Decrypts and validates the wrapped RSA private key with the first
kek/wrapped key, and re-encrypts it with the second if valid.

The re-encrypted key is then passed to the user, for use with
[\#DecryptOrImportRsaPrivateKey](#DecryptOrImportRsaPrivateKey "wikilink").

### DecryptRsaPrivateKey

Takes a session kek created with
[\#GenerateAesKek](#GenerateAesKek "wikilink"), a wrapped AES key, an
enum member, and a wrapped RSA private key.

The session kek must have been created with
[CryptoUsecase\_RsaPrivate](#enum_CryptoUsecase "wikilink").

\[4.0.0+\] The SMC handler when certain conditions pass and
SMC\_ID==0xC300100D now returns error 0x6 instead of calling the handler
funcptr.

\[5.0.0+\] This function was replaced by
[\#DecryptOrImportRsaPrivateKey](#DecryptOrImportRsaPrivateKey "wikilink").

### DecryptOrImportRsaPrivateKey

This function replaced
[\#DecryptRsaPrivateKey](#DecryptRsaPrivateKey "wikilink") in
[5.0.0](5.0.0.md "wikilink"), adding an additional
[\#enum\_DecryptOrImportMode](#enum_DecryptOrImportMode "wikilink").

This SMC extends DecryptRsaPrivateKey's original functionality to enable
importing private keys into the security engine instead of decrypting
them, when certain enum members are passed.

### ImportLotusKey

Takes a session kek created with
[\#GenerateAesKek](#GenerateAesKek "wikilink"), and a wrapped RSA key.

The session kek must have been created with
[CryptoUsecase\_RsaSecureExpMod](#enum_CryptoUsecase "wikilink").

\[5.0.0\] This function was removed.

### SecureExpMod

Performs an ExpMod operation using an exponent previously loaded with
the [\#ImportLotusKey](#ImportLotusKey "wikilink") command.

\[5.0.0+\] This now uses any exponent previously loaded with
[\#DecryptOrImportRsaPrivateKey](#DecryptOrImportRsaPrivateKey "wikilink")
and takes an
[\#enum\_SecureExpModMode](#enum_SecureExpModMode "wikilink").

### UnwrapTitleKey

Takes an Rsa-Oaep-wrapped TitleKey, an RSA Public Key, and a label hash.

Performs an ExpMod operation using an exponent previously loaded with
the [\#ImportEsKey](#ImportEsKey "wikilink") command, and then
validates/extracts a Titlekey from the resulting message.

Returns a session-unique AES key especially for use in
[\#LoadTitleKey](#LoadTitleKey "wikilink").

\[5.0.0+\] This now uses any exponent previously loaded with
[\#DecryptOrImportRsaPrivateKey](#DecryptOrImportRsaPrivateKey "wikilink").

### LoadTitleKey

Takes a session-unique AES key from
[\#UnwrapCommonTitleKey](#UnwrapCommonTitleKey "wikilink") or
[\#UnwrapTitleKey](#UnwrapTitleKey "wikilink").

### UnwrapCommonTitleKey

Takes an AES-wrapped TitleKey and returns a sealed AES key.

### enum CryptoUsecase

| Value | Name                           |
| ----- | ------------------------------ |
| 0     | CryptoUsecase\_Aes             |
| 1     | CryptoUsecase\_RsaPrivate      |
| 2     | CryptoUsecase\_RsaSecureExpMod |
| 3     | CryptoUsecase\_TitleKey        |

Note: The [CryptoUsecase\_TitleKey](#enum_CryptoUsecase "wikilink")
represents a RSA wrapped AES key.

### enum CipherMode

| Value | Name                   |
| ----- | ---------------------- |
| 0     | CipherMode\_CbcEncrypt |
| 1     | CipherMode\_CbcDecrypt |
| 2     | CipherMode\_Ctr        |

### enum DecryptOrImportMode

| Value | Name                                      |
| ----- | ----------------------------------------- |
| 0     | DecryptOrImportMode\_DecryptRsaPrivateKey |
| 1     | DecryptOrImportMode\_ImportLotusKey       |
| 2     | DecryptOrImportMode\_ImportEsKey          |
| 3     | DecryptOrImportMode\_ImportSslKey         |
| 4     | DecryptOrImportMode\_ImportDrmKey         |

### enum SecureExpModMode

| Value | Name                    |
| ----- | ----------------------- |
| 0     | SecureExpModMode\_Lotus |
| 1     | SecureExpModMode\_Ssl   |
| 2     | SecureExpModMode\_Drm   |

## ID 1

Functions exposed to the kernel internally.

| Sub-ID     | Name                                                                              | In                                                                        | Out                                         |
| ---------- | --------------------------------------------------------------------------------- | ------------------------------------------------------------------------- | ------------------------------------------- |
| 0xC4000001 | [\#CpuSuspend](#CpuSuspend "wikilink")                                            | X1=power\_state, X2=entrypoint\_addr, X3=context\_id                      | None                                        |
| 0x84000002 | [\#CpuOff](#CpuOff "wikilink")                                                    | None                                                                      | None                                        |
| 0xC4000003 | [\#CpuOn](#CpuOn "wikilink")                                                      | X1=target\_cpu, X2=entrypoint\_addr, X3=context\_id, X4,X5,X6,X7=0        | X0=result                                   |
| 0xC3000004 | [\#GetConfig](#GetConfig "wikilink") (Same as ID 0, Sub-ID 2)                     | W1=config\_item, X2,X3,X4,X5,X6,X7=0                                      | X0=result, X1,X2,X3,X4=config\_val          |
| 0xC3000005 | [\#GenerateRandomBytes](#GenerateRandomBytes "wikilink") (Same as ID 0, Sub-ID 6) | X1=size, X2,X3,X4,X5,X6,X7=0                                              | X0=result, X1,X2,X3,X4,X5,X6,X7=rand\_bytes |
| 0xC3000006 | [\#Panic](#Panic "wikilink")                                                      | W1=panic\_color, X2,X3,X4,X5,X6,X7=0                                      | X0=result                                   |
| 0xC3000007 | \[2.0.0+\] [\#ConfigureCarveout](#ConfigureCarveout "wikilink")                   | X1=carveout\_index, X2=region\_phys\_addr, X3=region\_size, X4,X5,X6,X7=0 | X0=result                                   |
| 0xC3000008 | \[2.0.0+\] [\#ReadWriteRegister](#ReadWriteRegister "wikilink")                   | X1=reg\_addr, W2=rw\_mask, W3=in\_val, X4,X5,X6,X7=0                      | X0=result, W1=out\_val                      |

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

Takes a **config\_item** and returns an associated **config\_val**.

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
| 12         | [\#KernelConfiguration](#KernelConfiguration "wikilink")               |
| 13         | [\#IsChargerHiZModeEnabled](#IsChargerHiZModeEnabled "wikilink")       |
| 14         | \[4.0.0+\] [\#IsKiosk](#IsKiosk "wikilink")                            |
| 15         | \[5.0.0+\] [\#RegulatorType](#RegulatorType "wikilink")                |
| 16         | \[5.0.0+\] [\#KeyGeneration](#KeyGeneration "wikilink")                |
| 17         | \[5.0.0+\] [\#Package2Hash](#Package2Hash "wikilink")                  |

#### DisableProgramVerification

[PM](Process%20Manager%20services.md "wikilink") checks this item and if
non-zero, calls fsp-pr SetEnabledProgramVerification(false).

#### DramId

This is extracted directly from
[FUSE\_RESERVED\_ODM4](Fuse%20registers#FUSE%20RESERVED%20ODM4.md##FUSE_RESERVED_ODM4 "wikilink").

| Value | Description                                                            |
| ----- | ---------------------------------------------------------------------- |
| 0     | DramId\_EristaIcosaSamsung4gb                                          |
| 1     | DramId\_EristaIcosaHynix4gb                                            |
| 2     | DramId\_EristaIcosaMicron4gb                                           |
| 3     | Reserved                                                               |
| 4     | DramId\_EristaIcosaSamsung6gb                                          |
| 5     | \[4.0.0+\] Reserved                                                    |
| 6     | \[4.0.0+\] Reserved                                                    |
| 7     | \[5.0.0+\] DramId\_MarikoIowax1x2Samsung4gb (\[4.0.0-4.1.0\] Reserved) |
| 8     | \[5.0.0+\] DramId\_MarikoIowaSamsung4gb                                |
| 9     | \[5.0.0+\] DramId\_MarikoIowaSamsung8gb                                |
| 10    | \[6.0.0+\] DramId\_MarikoIowaHynix4gb (\[5.0.0-5.1.0\] Reserved)       |
| 11    | \[7.0.0+\] DramId\_MarikoIowaMicron4gb (\[5.0.0-6.2.0\] Reserved)      |
| 12    | \[5.0.0+\] DramId\_MarikoHoagSamsung4gb                                |
| 13    | \[5.0.0+\] DramId\_MarikoHoagSamsung8gb                                |
| 14    | \[7.0.0+\] DramId\_MarikoHoagHynix4gb (\[5.0.0-6.2.0\] Reserved)       |
| 15    | \[7.0.0+\] DramId\_MarikoHoagMicron4gb (\[5.0.0-6.2.0\] Reserved)      |
| 16    | \[8.0.0+\] DramId\_MarikoUnkSamsung4gb                                 |

[PCV](PCV%20services.md "wikilink") selects memory training tables based
on DramId.

<table>
<thead>
<tr class="header">
<th><p>SoC</p></th>
<th><p>Platform</p></th>
<th><p>DramId</p></th>
<th><p>Revision</p></th>
<th><p>DVFS version</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>T210</p></td>
<td><p>jetson-tx1</p></td>
<td><p>N/A</p></td>
<td><p>0x07</p></td>
<td><p><code>11_40800_01_V9.8.3_V1.6</code><br />
<code>11_68000_01_V9.8.3_V1.6</code><br />
<code>11_102000_01_V9.8.3_V1.6</code><br />
<code>11_204000_05_V9.8.3_V1.6</code><br />
<code>11_408000_02_V9.8.3_V1.6</code><br />
<code>11_665600_03_V9.8.3_V1.6</code><br />
<code>11_800000_01_V9.8.3_V1.6</code><br />
<code>11_1065600_01_V9.8.3_V1.6</code><br />
<code>11_1331200_01_V9.8.3_V1.6</code><br />
<code>11_1600000_02_V9.8.3_V1.6</code></p></td>
</tr>
<tr class="even">
<td><p>T210</p></td>
<td><p>nx-abcb</p></td>
<td><p>EristaIcosaSamsung4gb</p></td>
<td><p>0x07</p></td>
<td><p><code>10_40800_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_68000_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_102000_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_204000_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_408000_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_665600_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_800000_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_1065600_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_1331200_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_1600000_NoCfgVersion_V9.8.7_V1.6</code></p></td>
</tr>
<tr class="odd">
<td><p>T210</p></td>
<td><p>nx-abcb</p></td>
<td><p>EristaIcosaMicron4gb</p></td>
<td><p>0x07</p></td>
<td><p><code>10_40800_NoCfgVersion_V9.8.4_V1.6</code><br />
<code>10_68000_NoCfgVersion_V9.8.4_V1.6</code><br />
<code>10_102000_NoCfgVersion_V9.8.4_V1.6</code><br />
<code>10_204000_NoCfgVersion_V9.8.4_V1.6</code><br />
<code>10_408000_NoCfgVersion_V9.8.4_V1.6</code><br />
<code>10_665600_NoCfgVersion_V9.8.4_V1.6</code><br />
<code>10_800000_NoCfgVersion_V9.8.4_V1.6</code><br />
<code>10_1065600_NoCfgVersion_V9.8.4_V1.6</code><br />
<code>10_1331200_NoCfgVersion_V9.8.4_V1.6</code><br />
<code>10_1600000_NoCfgVersion_V9.8.4_V1.6</code></p></td>
</tr>
<tr class="even">
<td><p>T210</p></td>
<td><p>nx-abcb</p></td>
<td><p>EristaIcosaHynix4gb</p></td>
<td><p>0x07</p></td>
<td><p><code>10_40800_NoCfgVersion_V9.8.4_V1.6</code><br />
<code>10_68000_NoCfgVersion_V9.8.4_V1.6</code><br />
<code>10_102000_NoCfgVersion_V9.8.4_V1.6</code><br />
<code>10_204000_NoCfgVersion_V9.8.4_V1.6</code><br />
<code>10_408000_NoCfgVersion_V9.8.4_V1.6</code><br />
<code>10_665600_NoCfgVersion_V9.8.4_V1.6</code><br />
<code>10_800000_NoCfgVersion_V9.8.4_V1.6</code><br />
<code>10_1065600_NoCfgVersion_V9.8.4_V1.6</code><br />
<code>10_1331200_NoCfgVersion_V9.8.4_V1.6</code><br />
<code>10_1600000_NoCfgVersion_V9.8.4_V1.6</code></p></td>
</tr>
<tr class="odd">
<td><p>T210</p></td>
<td><p>nx-abca2</p></td>
<td><p>EristaIcosaSamsung4gb, EristaIcosaMicron4gb</p></td>
<td><p>0x07</p></td>
<td><p><code>10_40800_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_68000_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_102000_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_204000_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_408000_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_665600_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_800000_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_1065600_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_1331200_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_1600000_NoCfgVersion_V9.8.7_V1.6</code></p></td>
</tr>
<tr class="even">
<td><p>T210</p></td>
<td><p>nx-abca2</p></td>
<td><p>EristaIcosaHynix4gb</p></td>
<td><p>0x07</p></td>
<td><p><code>10_40800_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_68000_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_102000_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_204000_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_408000_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_665600_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_800000_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_1065600_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_1331200_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_1600000_NoCfgVersion_V9.8.7_V1.6</code></p></td>
</tr>
<tr class="odd">
<td><p>T210</p></td>
<td><p>nx-abca2</p></td>
<td><p>EristaIcosaSamsung6gb</p></td>
<td><p>0x07</p></td>
<td><p><code>10_40800_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_68000_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_102000_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_204000_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_408000_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_665600_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_800000_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_1065600_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_1331200_NoCfgVersion_V9.8.7_V1.6</code><br />
<code>10_1600000_NoCfgVersion_V9.8.7_V1.6</code></p></td>
</tr>
<tr class="even">
<td><p>T214</p></td>
<td><p>nx-abca2, nx-abcb, nx-abcc</p></td>
<td><p>MarikoIowax1x2Samsung4gb</p></td>
<td><p>0x03</p></td>
<td><p><code>01_204000_NoCfgVersion_V0.3.1_V2.0</code><br />
<code>01_1331200.0_NoCfgVersion_V0.3.1_V2.0</code><br />
<code>01_1600000_NoCfgVersion_V0.3.1_V2.0</code></p></td>
</tr>
<tr class="odd">
<td><p>T214</p></td>
<td><p>nx-abca2, nx-abcb, nx-abcc</p></td>
<td><p>MarikoIowaSamsung4gb, MarikoHoagSamsung4gb</p></td>
<td><p>0x03</p></td>
<td><p><code>01_204000_NoCfgVersion_V0.3.1_V2.0</code><br />
<code>01_1331200.0_NoCfgVersion_V0.3.1_V2.0</code><br />
<code>01_1600000_NoCfgVersion_V0.3.1_V2.0</code></p></td>
</tr>
<tr class="even">
<td><p>T214</p></td>
<td><p>nx-abca2, nx-abcb, nx-abcc</p></td>
<td><p>MarikoIowaSamsung8gb, MarikoHoagSamsung8gb</p></td>
<td><p>0x03</p></td>
<td><p><code>01_204000_NoCfgVersion_V0.4.2_V2.0</code><br />
<code>01_1331200.0_NoCfgVersion_V0.4.2_V2.0</code><br />
<code>01_1600000_NoCfgVersion_V0.4.2_V2.0</code></p></td>
</tr>
<tr class="odd">
<td><p>T214</p></td>
<td><p>nx-abca2, nx-abcb, nx-abcc</p></td>
<td><p>MarikoIowaHynix4gb, MarikoHoagHynix4gb</p></td>
<td><p>0x03</p></td>
<td><p><code>01_204000_NoCfgVersion_V0.3.1_V2.0</code><br />
<code>01_1331200.0_NoCfgVersion_V0.3.1_V2.0</code><br />
<code>01_1600000_NoCfgVersion_V0.3.1_V2.0</code></p></td>
</tr>
<tr class="even">
<td><p>T214</p></td>
<td><p>nx-abca2, nx-abcb, nx-abcc</p></td>
<td><p>MarikoIowaMicron4gb, MarikoHoagMicron4gb</p></td>
<td><p>0x03</p></td>
<td><p><code>01_204000_NoCfgVersion_V0.4.2_V2.0</code><br />
<code>01_1331200.0_NoCfgVersion_V0.4.2_V2.0</code><br />
<code>01_1600000_NoCfgVersion_V0.4.2_V2.0</code></p></td>
</tr>
<tr class="odd">
<td><p>T214</p></td>
<td><p>nx-abca2, nx-abcb, nx-abcc</p></td>
<td><p>MarikoUnkSamsung4gb</p></td>
<td><p>0x03</p></td>
<td><p><code>01_204000_NoCfgVersion_V0.4.2_V2.0</code><br />
<code>01_1331200.0_NoCfgVersion_V0.4.2_V2.0</code><br />
<code>01_1600000_NoCfgVersion_V0.4.2_V2.0</code></p></td>
</tr>
</tbody>
</table>

**nx-abca2** (**Icosa** or **Hoag** in **Erista**, **Iowa** or **Hoag**
in **Mariko**) hardware types are variations of the retail and EDEV form
factors.

**nx-abcb** (**Copper**) is the SDEV unit. Among other differences, this
has extra hardware to support HDMI output.

\[8.0.0+\] **nx-abcc** was added for **Mariko**.

**Erista** memory is LPDDR4, while **Mariko** memory is LPDDR4X.

#### SecurityEngineIrqNumber

SPL uses this for setting up the security engine IRQ.

#### Version

The current [Package1 Maxver
Constant](Package2#Versions.md##Versions "wikilink") - 1.

#### HardwareType

\[1.0.0+\] This item is obtained by checking bits 8 and 2 from
[FUSE\_RESERVED\_ODM4](Fuse%20registers#FUSE%20RESERVED%20ODM4.md##FUSE_RESERVED_ODM4 "wikilink").
It can be 0 (Icosa), 1 (Copper), 2 (Hoag) or 3 (Invalid).

\[4.0.0+\] This item is obtained by checking bits 8, 2 and 16-19 from
[FUSE\_RESERVED\_ODM4](Fuse%20registers#FUSE%20RESERVED%20ODM4.md##FUSE_RESERVED_ODM4 "wikilink").
It can be 0 (Icosa), 1 (Copper), 2 (Hoag), 3 (Iowa) or 4 (Invalid).

\[7.0.0+\] This item no longer depends on fuses and can only be 0
(Icosa) or 0xF (Invalid) in retail units.

\[8.0.0+\] This item can be 0 (Icosa), 1 (Copper), 2 (Hoag), 3 (Iowa), 4
(Unknown) or 5 (Invalid). It still can only be 0 (Icosa) or 0xF
(Invalid) in retail units.

#### IsRetail

This item is obtained by checking bits 9 and 0-1 from
[FUSE\_RESERVED\_ODM4](Fuse%20registers#FUSE%20RESERVED%20ODM4.md##FUSE_RESERVED_ODM4 "wikilink").
It can be 0 (Debug), 1 (Retail) or 2 (Invalid).

#### IsRecoveryBoot

Used to determine if the system is booting from SafeMode firmware.

Under normal circumstances, this just returns bit 0 of the active
[bootloader
info](BCT#bootloader0%20info.md##bootloader0_info "wikilink")'s
attribute field.

#### DeviceId

[NIM](NIM%20services.md "wikilink") checks if this item matches the
[set:cal](Settings%20services.md "wikilink") DeviceId with byte7
cleared. If they don't match, a panic is thrown.

#### BootReason

Used to determine how the system booted.

| Value | Description |
| ----- | ----------- |
| 0     | Invalid     |
| 1     | AcOk        |
| 2     | OnKey       |
| 3     | RtcAlarm1   |
| 4     | RtcAlarm2   |

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

#### KernelConfiguration

Kernel reads this when setting up memory-related code.

Bit 0 is a boolean determining whether kernel should it will memset
various allocated memory-regions with 0x58, 0x59, 0x5A ('X', 'Y', 'Z')
instead of zero. This allows Nintendo devs to find uninitialized memory
bugs.

Bit 1 is a boolean determining whether kernel should forcefully enable
usermode exception handlers (when false, only certain aborts (((1LL \<\<
(esr \>\> 26)) & 0x1115804400224001) == 0, typically data/prefetch
aborts) that occur when the faulting address is in a readable region
with MemoryType\_CodeStatic will trigger usermode exception handlers).

Bit 2 is a boolean determining whether kernel should enable usermode
access to the Performance Monitors (whether PMUSERENR\_EL0 should be 1
or 0).

\[8.0.0+\] Bit 3 is a boolean determining whether the kernldr should
allocate 0x68000 extra bytes before INI1 data

Bits 8-15 are a boolean determining whether kernel should call smcPanic
on error instead of infinite-looping.

Bits 16-17 determine how much memory is available. 00/03 = 4 GB, 01 = 6
GB, 02 = 8 GB.

#### IsChargerHiZModeEnabled

This tells if the TI Charger (bq24192) is active.

#### KeyGeneration

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

#### RegulatorType

This item is currently hardcoded to 0.

\[5.0.0+\] [PCV](PCV%20services.md "wikilink") uses this value in
combination with [HardwareType](#HardwareType "wikilink") to configure
power blocks and memory tables for different hardware.

| Value | SoC  | GPU           | Power Blocks                                   |
| ----- | ---- | ------------- | ---------------------------------------------- |
| 0     | T210 | GM20B (0x12B) | max77620\_sd0, max77621\_cpu and max77621\_gpu |
| 1     | T214 | GM2?? (0x12E) | max77620\_sd0, max77812\_cpu and max77812\_gpu |
| 2     | T214 | GM2?? (0x12E) | max77620\_sd0, max77812\_cpu and max77812\_gpu |

#### Package2Hash

This is a SHA-256 hash calculated over the
[package2](Package2.md "wikilink") image. Since the hash calculation is
an optional step in pkg2ldr, this item is only valid in recovery mode.
Otherwise, an error is returned instead.

### GenerateRandomBytes

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

| Value        | Description             |
| ------------ | ----------------------- |
| 0            | Success                 |
| 1            | Not implemented         |
| 2            | Invalid argument        |
| 3            | In progress             |
| 4            | No async operation      |
| 5            | Invalid async operation |
| \[8.0.0+\] 6 | Blacklisted             |

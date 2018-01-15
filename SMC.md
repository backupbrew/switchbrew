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

| Sub-ID     | Name                                                           | In | Out |
| ---------- | -------------------------------------------------------------- | -- | --- |
| 0xC3000401 | SetConfig                                                      |    |     |
| 0xC3000002 | GetConfig (Same as ID 1, Sub-ID 4)                             |    |     |
| 0xC3000003 | CheckStatus                                                    |    |     |
| 0xC3000404 | GetResult                                                      |    |     |
| 0xC3000E05 | ExpMod                                                         |    |     |
| 0xC3000006 | GetRandomBytes (Same as ID 1, Sub-ID 5)                        |    |     |
| 0xC3000007 | [\#GenerateAesKek](#GenerateAesKek "wikilink")                 |    |     |
| 0xC3000008 | [\#LoadAesKey](#LoadAesKey "wikilink")                         |    |     |
| 0xC3000009 | [\#CryptAes](#CryptAes "wikilink")                             |    |     |
| 0xC300000A | [\#GenerateSpecificAesKey](#GenerateSpecificAesKey "wikilink") |    |     |
| 0xC300040B | [\#ComputeCmac](#ComputeCmac "wikilink")                       |    |     |
| 0xC300100C | [\#LoadRsaPrivateKey](#LoadRsaPrivateKey "wikilink")           |    |     |
| 0xC300100D | [\#DecryptRsaPrivateKey](#DecryptRsaPrivateKey "wikilink")     |    |     |
| 0xC300100E | [\#LoadRsaPublicKey](#LoadRsaPublicKey "wikilink")             |    |     |
| 0xC300060F | [\#PublicRsa](#PublicRsa "wikilink")                           |    |     |
| 0xC3000610 | [\#UnwrapPreparedAesKey](#UnwrapPreparedAesKey "wikilink")     |    |     |
| 0xC3000011 | [\#LoadPreparedAesKey](#LoadPreparedAesKey "wikilink")         |    |     |
| 0xC3000012 | \[2.0.0+\] GeneratePreparedAesKek                              |    |     |

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

Note: The [CryptoUsecase\_PreparedAesKey](#CryptoUsecase "wikilink")
represents a RSA wrapped AES key.

### GenerateAesKek

Takes an "access key" as input, an
[\#CryptoUsecase](#CryptoUsecase "wikilink").

Returns a session-unique kek for said usecase.

### LoadAesKey

Takes a session kek created with
[\#GenerateAesKek](#GenerateAesKek "wikilink"), and a wrapped AES key.

The session kek must have been created with CryptoUsecase\_Aes.

### CryptAes

Encrypts/decrypts using Aes (CTR and CBC).

Key must be set prior using one of the
[\#LoadAesKey](#LoadAesKey "wikilink"),
[\#GenerateSpecificAesKey](#GenerateSpecificAesKey "wikilink") or
[\#LoadRsaWrappedAesKey](#LoadRsaWrappedAesKey "wikilink") commands.

### GenerateSpecificAesKey

Todo: This one seems unrelated to
[\#CryptoUsecase](#CryptoUsecase "wikilink").

### LoadRsaPrivateKey

Takes a session kek created with
[\#GenerateAesKek](#GenerateAesKek "wikilink"), a wrapped AES key, and a
wrapped RSA private key.

The session kek must have been created with
CryptoUsecase\_PreparedAesKey.

### DecryptRsaPrivateKey

Takes a session kek created with
[\#GenerateAesKek](#GenerateAesKek "wikilink"), a wrapped AES key, and a
wrapped RSA private key.

The session kek must have been created with CryptoUsecase\_PrivateRsa.

\[{Unknown version}+\] The SMC handler when certain conditions pass and
SMC\_ID==0xC300100D now returns error 0x6 instead of calling the handler
funcptr.

### LoadRsaPublicKey

Takes a session kek created with
[\#GenerateAesKek](#GenerateAesKek "wikilink"), and a wrapped RSA public
key.

The session kek must have been created with CryptoUsecase\_PublicRsa.

### PublicRsa

Encrypts using Rsa public key.

Key must be set prior using the
[\#LoadRsaPublicKey](#LoadRsaPublicKey "wikilink") command.

### UnwrapPreparedAesKey

Takes a session kek created with
[\#GenerateAesKek](#GenerateAesKek "wikilink"), and a wrapped RSA public
key.

Returns a session-unique AES key especially for use in
[\#LoadPreparedAesKey](#LoadPreparedAesKey "wikilink").

The session kek must have been created with
CryptoUsecase\_PreparedAesKey.

### LoadPreparedAesKey

Takes a session-unique AES key from
[\#UnwrapPreparedAesKey](#UnwrapPreparedAesKey "wikilink").

### enum CryptoUsecase

| Value | Name                          |
| ----- | ----------------------------- |
| 0     | CryptoUsecase\_Aes            |
| 1     | CryptoUsecase\_PrivateRsa     |
| 2     | CryptoUsecase\_PublicRsa      |
| 3     | CryptoUsecase\_PreparedAesKey |

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
| 0xC3000007 | \[2.0.0+\] [\#ProtectKernelRegion](#ProtectKernelRegion "wikilink")     | X1=carveout\_index, X2=region\_phys\_addr, X3=region\_size, X4,X5,X6,X7=0 | X0=result                                   |
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

Takes a **config\_item** and returns an associated **config\_val**.

### GetRandomBytes

Takes a **size** and returns **rand\_bytes**.

The kernel limits **size** to 0x38 (for fitting in return registers).

### Panic

Issues a system panic.

The kernel always calls this with **panic\_color** set to 0xF00.

### ProtectKernelRegion

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

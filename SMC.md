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

| Sub-Id     | Name                                                               | In | Out |
| ---------- | ------------------------------------------------------------------ | -- | --- |
| 0xC3000401 | SetConfig                                                          |    |     |
| 0xC3000002 | GetConfig (Same as Id 1 Sub-Id 4.)                                 |    |     |
| 0xC3000003 | CheckStatus                                                        |    |     |
| 0xC3000404 | GetResult                                                          |    |     |
| 0xC3000E05 | ExpMod                                                             |    |     |
| 0xC3000006 | GetRandomBytes (Same as Id 1 Sub-Id 5.)                            |    |     |
| 0xC3000007 | [\#GenerateAesKek](#GenerateAesKek "wikilink")                     |    |     |
| 0xC3000008 | [\#LoadAesKey](#LoadAesKey "wikilink")                             |    |     |
| 0xC3000009 | [\#CryptAes](#CryptAes "wikilink")                                 |    |     |
| 0xC300000A | [\#GenerateSpecificAesKey](#GenerateSpecificAesKey "wikilink")     |    |     |
| 0xC300040B | [\#ComputeCmac](#ComputeCmac "wikilink")                           |    |     |
| 0xC300100C | [\#LoadRsaPrivateKey](#LoadRsaPrivateKey "wikilink")               |    |     |
| 0xC300100D | [\#PrivateRsa](#PrivateRsa "wikilink")                             |    |     |
| 0xC300100E | [\#LoadRsaPublicKey](#LoadRsaPublicKey "wikilink")                 |    |     |
| 0xC300060F | [\#PublicRsa](#PublicRsa "wikilink")                               |    |     |
| 0xC3000610 | [\#UnwrapRsaEncryptedAesKey](#UnwrapRsaEncryptedAesKey "wikilink") |    |     |
| 0xC3000011 | [\#LoadRsaWrappedAesKey](#LoadRsaWrappedAesKey "wikilink")         |    |     |
| 0xC3000012 | \[2.0.0+\] GenerateRsaWrappedAesKek                                |    |     |

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
[\#GenerateAesKek](#GenerateAesKek "wikilink"), and a wrapped RSA
private key.

The session kek must have been created with CryptoUsecase\_PrivateRsa.

### PrivateRsa

Encrypts using Rsa private key.

Key must be set prior using the
[\#LoadRsaPrivateKey](#LoadRsaPrivateKey "wikilink") command.

### LoadRsaPublicKey

Takes a session kek created with
[\#GenerateAesKek](#GenerateAesKek "wikilink"), and a wrapped RSA public
key.

The session kek must have been created with CryptoUsecase\_PublicRsa.

### PublicRsa

Encrypts using Rsa public key.

Key must be set prior using the
[\#LoadRsaPublicKey](#LoadRsaPublicKey "wikilink") command.

### UnwrapRsaEncryptedAesKey

Takes a session kek created with
[\#GenerateAesKek](#GenerateAesKek "wikilink"), and a wrapped RSA public
key.

Returns a session-unique AES key especially for use in
[\#LoadRsaWrappedAesKey](#LoadRsaWrappedAesKey "wikilink").

The session kek must have been created with
CryptoUsecase\_RsaWrappedAesKey.

### LoadRsaWrappedAesKey

Takes a session-unique AES key from
[\#UnwrapRsaEncryptedAesKey](#UnwrapRsaEncryptedAesKey "wikilink").

### enum CryptoUsecase

| Value | Name                            |
| ----- | ------------------------------- |
| 0     | CryptoUsecase\_Aes              |
| 1     | CryptoUsecase\_PrivateRsa       |
| 2     | CryptoUsecase\_PublicRsa        |
| 3     | CryptoUsecase\_RsaWrappedAesKey |

## Id 1

Functions exposed to the kernel internally.

| Sub-Id     | Name                                    | In | Out |
| ---------- | --------------------------------------- | -- | --- |
| 0xC4000001 | CpuSuspend (oyasumi)                    |    |     |
| 0x84000002 | CpuOff                                  |    |     |
| 0xC4000003 | CpuOn                                   |    |     |
| 0xC3000004 | GetConfig (Same as Id 0 Sub-Id 2.)      |    |     |
| 0xC3000005 | GetRandomBytes (Same as Id 0 Sub-Id 6.) |    |     |
| 0xC3000006 | Panic                                   |    |     |
| 0xC3000007 | \[2.0.0+\] ProtectKernelRegion          |    |     |
| 0xC3000008 | \[2.0.0+\] ReadWriteRegister            |    |     |

# Errors

2: Invalid input 3: Busy

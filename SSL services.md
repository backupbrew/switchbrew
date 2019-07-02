# ssl

This is "nn::ssl::sf::ISslService".

| Cmd | Name                                                                |
| --- | ------------------------------------------------------------------- |
| 0   | [\#CreateContext](#CreateContext "wikilink")                        |
| 1   | GetContextCount                                                     |
| 2   | [\#GetCertificates](#GetCertificates "wikilink")                    |
| 3   | [\#GetCertificateBufSize](#GetCertificateBufSize "wikilink")        |
| 4   | \[3.0.0+\] [\#DebugIoctl](#DebugIoctl "wikilink")                   |
| 5   | \[3.0.0+\] [\#SetInterfaceVersion](#SetInterfaceVersion "wikilink") |
| 6   | \[5.0.0+\] FlushSessionCache                                        |
| 7   | \[6.0.0+\] [\#SetDebugOption](#SetDebugOption "wikilink")           |
| 8   | \[6.0.0+\] [\#GetDebugOption](#GetDebugOption "wikilink")           |

## CreateContext

Takes a PID, an input u32 [\#SslVersion](#SslVersion "wikilink"), an
input u64 pid\_placeholder, and returns an output
[\#ISslContext](#ISslContext "wikilink").

## GetCertificates

Takes a type-0x6 output buffer and a type-0x5 input buffer containing an
array of [\#CaCertificateId](#CaCertificateId "wikilink").

\[3.0.0+\] This now returns an output u32 for actual total output
entries.

The output buffer starts with an array of
[\#BuiltInCertificateInfo](#BuiltInCertificateInfo "wikilink"), with the
DER cert data following afterwards.

## GetCertificateBufSize

Takes a type-0x5 input buffer containing an array of
[\#CaCertificateId](#CaCertificateId "wikilink"), returns an output u32
for the size to use with
[\#GetCertificates](#GetCertificates "wikilink").

## DebugIoctl

Stubbed on retail, just returns an error.

## SetInterfaceVersion

Takes an input u32 **version**, no output.

Used by user-processes during service init.

## SetDebugOption

Takes an input u32 **DebugOptionType** and a type-0x5 input buffer, no
output.

The input u32 value must be 0, and the buffer addr/size must not be 0.

The u8 at buf+0 is copied to state.

## GetDebugOption

Takes an input u32 **DebugOptionType** and a type-0x6 output buffer.

Same as [\#SetDebugOption](#SetDebugOption "wikilink") except this
copies state to the buffer instead.

## ISslContext

This is "nn::ssl::sf::ISslContext".

| Cmd | Name                                               |
| --- | -------------------------------------------------- |
| 0   | SetOption                                          |
| 1   | GetOption                                          |
| 2   | [\#CreateConnection](#CreateConnection "wikilink") |
| 3   | GetConnectionCount                                 |
| 4   | ImportServerPki                                    |
| 5   | ImportClientPki                                    |
| 6   | RemoveServerPki                                    |
| 7   | RemoveClientPki                                    |
| 8   | RegisterInternalPki                                |
| 9   | AddPolicyOid                                       |
| 10  | \[3.0.0+\] ImportCrl                               |
| 11  | \[3.0.0+\] RemoveCrl                               |

### CreateConnection

No input, returns an [\#ISslConnection](#ISslConnection "wikilink").

### ISslConnection

This is "nn::ssl::sf::ISslConnection".

| Cmd | Name                          |
| --- | ----------------------------- |
| 0   | SetSocketDescriptor           |
| 1   | SetHostName                   |
| 2   | SetVerifyOption               |
| 3   | SetIoMode                     |
| 4   | GetSocketDescriptor           |
| 5   | GetHostName                   |
| 6   | GetVerifyOption               |
| 7   | GetIoMode                     |
| 8   | DoHandshake                   |
| 9   | DoHandshakeGetServerCert      |
| 10  | Read                          |
| 11  | Write                         |
| 12  | Pending                       |
| 13  | Peek                          |
| 14  | Poll                          |
| 15  | GetVerifyCertError            |
| 16  | GetNeededServerCertBufferSize |
| 17  | SetSessionCacheMode           |
| 18  | GetSessionCacheMode           |
| 19  | FlushSessionCache             |
| 20  | SetRenegotiationMode          |
| 21  | GetRenegotiationMode          |
| 22  | SetOption                     |
| 23  | GetOption                     |
| 24  | GetVerifyCertErrors           |
| 25  | \[4.0.0+\] GetCipherInfo      |

# SslVersion

This is the "nn::ssl::sf::SslVersion" enum.

# BuiltInCertificateInfo

| Offset | Size | Description                                          |
| ------ | ---- | ---------------------------------------------------- |
| 0x0    | 0x4  | CaCertificateId                                      |
| 0x4    | 0x4  | [\#BuiltinDataStatus](#BuiltinDataStatus "wikilink") |
| 0x8    | 0x8  | Data size                                            |
| 0x10   | 0x8  | Data offset                                          |

This is the struct returned by
[\#GetCertificates](#GetCertificates "wikilink"). Official sw converts
this to "nn::ssl::BuiltInManager::BuiltInCertificateInfo" with offset
converted to a ptr.

# BuiltinDataStatus

| Value | Description |
| ----- | ----------- |
| \-1   | Invalid     |
| 1     | Valid       |

This is the "nn::ssl::detail::BuiltinDataInfo::BuiltinDataStatus" enum.

# CaCertificateId

| Value | Description    |
| ----- | -------------- |
| 1     | Nintendo {...} |
| 2     | Nintendo {...} |

This is the "nn::ssl::CaCertificateId" enum.

# Client cert+privk

SSL-sysmodule uses [set:cal](Settings%20services.md "wikilink")
[GetSslKey](Settings%20services#GetSslKey.md##GetSslKey "wikilink") and
[GetSslCert](Settings%20services#GetSslCert.md##GetSslCert "wikilink").
The rest of this section documents handling for the former, which can be
decrypted with [SPL](SPL%20services.md "wikilink").

key\* below refers to the 3 0x10-byte input blocks passed to this code.

When actual\_size is:

  - 0x100+0x10: If the u32 actual\_size is less than (u32)-0x11, and the
    last 0x10-bytes of the actual-data are all-zero, the data is copied
    to the output as raw plaintext. If a non-zero byte is found, it will
    continue with [SPL](SPL%20services.md "wikilink") usage, skipping
    over the SPL block for the devunit flag. In this case, key=key0 and
    the flag passed to SPL later is set to 0.
  - 0x100+0x30: Size must match this if it's not the above, otherwise
    error 0xC81A is returned. The flag passed to SPL later is set to 1
    in this case. Runs the devunit-flag-block: uses
    [SPL\_services\#SPL\#GetDevunitFlag](SPL%20services#SPL#GetDevunitFlag.md##SPL#GetDevunitFlag "wikilink").
    key = key1 when out\_flag\!=0, key2 otherwise.

[Category:Services](Category:Services "wikilink")

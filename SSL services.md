# ssl

This is "nn::ssl::sf::ISslService".

| Cmd | Name                  |
| --- | --------------------- |
| 0   | CreateContext         |
| 1   | GetContextCount       |
| 2   | GetCertificates       |
| 3   | GetCertificateBufSize |
| 4   | DebugIoctl            |
| 5   | SetInterfaceVersion   |

## ISslContext

| Cmd | Name                |
| --- | ------------------- |
| 0   | SetOption           |
| 1   | GetOption           |
| 2   | CreateConnection    |
| 3   | GetConnectionCount  |
| 4   | ImportServerPki     |
| 5   | ImportClientPki     |
| 6   | RemoveServerPki     |
| 7   | RemoveClientPki     |
| 8   | RegisterInternalPki |
| 9   | AddPolicyOid        |
| 10  | ImportCrl           |
| 11  | RemoveCrl           |

### ISslConnection

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

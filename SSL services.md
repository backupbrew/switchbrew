# ssl

# Client cert+privk

SSL-sysmodule uses [set:cal](Settings%20services.md "wikilink")
GetTLSClientPrivk and GetTLSClientCert. The rest of this section
documents handling for the former, which can be decrypted with
[SPL](SPL%20services.md "wikilink").

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
    in this case.

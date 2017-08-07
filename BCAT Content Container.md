Content downloaded by [BCAT](BCAT%20services.md "wikilink") normally
uses this
container.

# Header

| Offset | Size  | Description                                                                                                |
| ------ | ----- | ---------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x4   | Magicnum "bcat"                                                                                            |
| 0x4    | 0x1   | ?                                                                                                          |
| 0x5    | 0x1   | Crypto type: 0x1 = AES-128-CTR, 0x2 = AES-192-CTR, 0x3 = AES-256-CTR. Everything else indicates plaintext. |
| 0x6    | 0x1   | RSA Hash Type: 0x1,0x3 = SHA256, 0x0,0x2 = SHA1                                                            |
| 0x7    | 0x1   | Secret-data index                                                                                          |
| 0x8    | 0x8   | Normally zero?                                                                                             |
| 0x10   | 0x10  | Base IV/CTR                                                                                                |
| 0x20   | 0x100 | RSA-2048 signature                                                                                         |

The header is 0x120-bytes.

# Key generation

The AES keydata is the output from pkcs5\_pbkdf2\_hmac, with SHA256:
password = <passphrase string loaded from file>, salt =
<below salt string>, and iteration\_count=4096.

The passphrase is loaded from "<basepath>/passphrase.bin".
passphrase\_len=strlen(passphrase). 0x40-bytes are read from the file,
with 0x0 being written to passphrase\[total\_read\_data\]. salt\_len =
strlen(salt).

salt is the snprintf output from "%016llx%s", where the former is the
titleID, while the latter is secretdata\_str. secretdata\_str =
secretdata\_array\[\<value of hdr+0x7\>\].

Settings config for 1-byte \<"bcat", "production\_mode"\> is loaded,
when retval\!=1 or output\_config\!=0, then secretdata\_array =
secretdata\_array0(retail), otherwise secretdata\_array =
secretdata\_array1(devunit). The latter only contains empty strings,
while the former contains lower-case hex strings. There are 16 entries
in each array.

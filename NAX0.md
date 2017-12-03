This is the format on the files stored on
[SD](SD%20Filesystem.md "wikilink") (Nintendo Aes Xts -- official name
is AesXtsFilesystem/AesXtsFile).

The data between this header and offset 0x4000 is unused/uninitialized
it appears. The actual content which is encrypted, starts at offset
0x4000 with the size from the header.

When a NAX0 file is recreated, the header and raw content in NAX0 are
completely different except for the magicnum and size-field. This is the
case when a title is redownloaded/reinstalled, and when "save/" files
are recreated after manual deletion.

[Error](Error%20codes.md "wikilink") 0x250E02 is returned by NCM when
attempting to access a NcaId where the NAX0 header HMAC validation
fails.

| Offset | Size | Description                                 |
| ------ | ---- | ------------------------------------------- |
| 0x0    | 0x20 | Header HMAC                                 |
| 0x20   | 0x8  | Magicnum "NAX0"                             |
| 0x28   | 0x20 | Encrypted AES-XTS Keys                      |
| 0x48   | 0x8  | Size of the file relative to offset 0x4000. |
| 0x50   | 0x30 | Padding                                     |

# Encryption

The actual content uses AES-XTS with the same non-standard tweak
(endianness swap) as usual, and sector size 0x4000.

Key derivation is as follows:

First, FS retrieves the 16-byte console-unique seed that NS registered
(data originates from the ns\_systemseed:/ [system
savegame](Flash%20Filesystem#System%20Savegames.md##System_Savegames "wikilink")).
Next, FS calculates encryptedSeedKeys = \<0x20 hardcoded keydata
depending on if this NAX0 is a save or an NCA\> XORed with the system
seed, calculates kek =
[GenerateAesKek](SPL%20services#GenerateAesKek.md##GenerateAesKek "wikilink")(<hardcoded keydata>,
0, 0), and then calculates decryptedSeedKeys by doing
decryptedSeedKeys\[i\] =
[GenerateAesKey](SPL%20services#GenerateAesKey.md##GenerateAesKey "wikilink")(kek,
encryptedSeedKeys\[i\]); for both keys.

Once the decryptedSeedKeys are calculated, FS calculates naxSpecificKeys
= hmac-sha256(key=decryptedSeedKeys\[0\], data=\<NAX0 path, relative to
/Nintendo/Contents\>); (example path:
'/registered/000000FF/cafebabecafebabecafebabecafebabe.nca'). Then, FS
does the following decryptions in place:
aes128\_ecb\_decrypt(key=naxSpecificKeys\[0\], data=Header + 0x28);
aes128\_ecb\_decrypt(key=naxSpecificKeys\[1\], data=Header + 0x38);
Finally, hmac-sha256(key=Header\[0x20:0x60\],
data=decryptedSeedKeys\[1\]) is calculated, and compared using a
constant-time memcmp to the hmac stored at Header + 0x0. If it matches,
decryption proceeds using the two decrypted keys at Header + 0x28 as an
AES-XTS keypair.

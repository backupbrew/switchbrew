# caps:a

This is "nn::capsrv::sf::IAlbumAccessorService".

| Cmd   | Name                                              |
| ----- | ------------------------------------------------- |
| 0     | GetAlbumFileCount                                 |
| 1     | GetAlbumFileList                                  |
| 2     | LoadAlbumFile                                     |
| 3     | DeleteAlbumFile                                   |
| 4     | StorageCopyAlbumFile                              |
| 5     | IsAlbumMounted                                    |
| 6     | GetAlbumUsage                                     |
| 7     | GetAlbumFileSize                                  |
| 8     | LoadAlbumFileThumbnail                            |
| 9     | \[2.0.0+\] LoadAlbumScreenShotImage               |
| 10    | \[2.0.0+\] LoadAlbumScreenShotThumbnailImage      |
| 11    | \[2.0.0+\] GetAlbumEntryFromApplicationAlbumEntry |
| 12    | \[3.0.0+\]                                        |
| 13    | \[3.0.0+\]                                        |
| 14    | \[3.0.0+\]                                        |
| 15    | \[4.0.0+\]                                        |
| 16    | \[4.0.0+\]                                        |
| 17    | \[4.0.0+\]                                        |
| 18    | \[6.0.0+\]                                        |
| 202   | \[1.0.0-2.3.0\] SaveEditedScreenShot              |
| 301   | GetLastThumbnail                                  |
| 302   | \[4.0.0+\]                                        |
| 401   | GetAutoSavingStorage                              |
| 501   | GetRequiredStorageSpaceSizeToCopyAll              |
| 1001  | \[3.0.0+\]                                        |
| 1002  | \[3.0.0+\]                                        |
| 1003  | \[4.0.0+\]                                        |
| 8001  | ForceAlbumUnmounted                               |
| 8002  | ResetAlbumMountStatus                             |
| 8011  | RefreshAlbumCache                                 |
| 8012  | GetAlbumCache                                     |
| 8013  | \[4.0.0+\]                                        |
| 8021  | GetAlbumEntryFromApplicationAlbumEntryAruid       |
| 10011 | SetInternalErrorConversionEnabled                 |
| 50000 | \[6.0.0+\]                                        |
| 60002 | \[4.0.0+\]                                        |

Cmd1002: Takes a total of 0x38-bytes of input, two type-0x5 input
buffers, and returns 0x20-bytes of output. \[4.0.0+\] No longer returns
output, and now takes the following buffers instead: type-0x16,
type-0x46, and type-0x6.

Cmd60002: Takes a total of 8-bytes of input, a PID, and returns an
[\#IAlbumAccessorSession](#IAlbumAccessorSession "wikilink").

## IAlbumAccessorSession

This is "nn::capsrv::sf::IAlbumAccessorSession".

This was added with \[4.0.0+\].

| Cmd  | Name |
| ---- | ---- |
| 2001 |      |
| 2002 |      |
| 2003 |      |
| 2004 |      |
| 2005 |      |
| 2006 |      |
| 2007 |      |
| 2008 |      |

# caps:c

This is "nn::capsrv::sf::IAlbumControlService".

| Cmd              | Name       | Notes                                                                                                               |
| ---------------- | ---------- | ------------------------------------------------------------------------------------------------------------------- |
| 33               | \[7.0.0+\] | Takes a total of 0x10-bytes of input, no output.                                                                    |
| 2001             |            |                                                                                                                     |
| 2002             |            |                                                                                                                     |
| 2011             |            |                                                                                                                     |
| 2012             |            |                                                                                                                     |
| 2013             |            |                                                                                                                     |
| 2014             |            |                                                                                                                     |
| 2101             |            | Takes an input u8 and u64, returns a 0x18-byte struct.                                                              |
| 2102             |            |                                                                                                                     |
| \[?-3.0.2\] 2201 |            |                                                                                                                     |
| 2202             | \[4.0.0+\] |                                                                                                                     |
| 2301             |            |                                                                                                                     |
| 2302             | \[4.0.0+\] |                                                                                                                     |
| 60001            | \[4.0.0+\] | Takes a total of 8-bytes of input and a PID, returns an [\#IAlbumControlSession](#IAlbumControlSession "wikilink"). |

## IAlbumControlSession

This is "nn::capsrv::sf::IAlbumControlSession".

This was added with \[4.0.0+\].

| Cmd  | Name       | Notes |
| ---- | ---------- | ----- |
| 2001 |            |       |
| 2002 |            |       |
| 2003 |            |       |
| 2004 |            |       |
| 2005 |            |       |
| 2006 |            |       |
| 2007 |            |       |
| 2008 |            |       |
| 2401 |            |       |
| 2402 |            |       |
| 2403 |            |       |
| 2404 |            |       |
| 2405 |            |       |
| 2406 | \[7.0.0+\] |       |
| 2411 |            |       |
| 2412 |            |       |
| 2413 |            |       |
| 2414 |            |       |
| 2421 |            |       |
| 2422 |            |       |
| 2424 |            |       |
| 2431 |            |       |
| 2433 |            |       |
| 2434 |            |       |

# caps:u

This is "nn::capsrv::sf::IAlbumApplicationService".

| Cmd   | Name                                                                    |
| ----- | ----------------------------------------------------------------------- |
| 32    | \[7.0.0+\] [\#SetShimLibraryVersion](#SetShimLibraryVersion "wikilink") |
| 102   | GetAlbumFileList0AafeAruidDeprecated                                    |
| 103   | DeleteAlbumFileByAruid                                                  |
| 104   | GetAlbumFileSizeByAruid                                                 |
| 105   | DeleteAlbumFileByAruidForDebug                                          |
| 110   | LoadAlbumScreenShotImageByAruid                                         |
| 120   | LoadAlbumScreenShotThumbnailImageByAruid                                |
| 130   | PrecheckToCreateContentsByAruid                                         |
| 140   | \[6.0.0+\] GetAlbumFileList1AafeAruidDeprecated                         |
| 141   | \[6.0.0+\] GetAlbumFileList2AafeUidAruidDeprecated                      |
| 142   | \[7.0.0+\] GetAlbumFileList3AaeAruid                                    |
| 143   | \[7.0.0+\] GetAlbumFileList4AaeUidAruid                                 |
| 60002 | OpenAccessorSessionForApplication                                       |

## SetShimLibraryVersion

Takes a total of 0x10-bytes of input and a PID, no output.

## IAlbumAccessorApplicationSession

This is "nn::capsrv::sf::IAlbumAccessorApplicationSession".

| Cmd  | Name                                  |
| ---- | ------------------------------------- |
| 2001 | OpenAlbumMovieReadStream              |
| 2002 | CloseAlbumMovieReadStream             |
| 2003 | GetAlbumMovieReadStreamMovieDataSize  |
| 2004 | ReadMovieDataFromAlbumMovieReadStream |
| 2005 | GetAlbumMovieReadStreamBrokenReason   |

# Notes

capsrv is responsible for validating the MACs for screenshots stored on
the SD card, if the setting
capsrv\!enable\_album\_screenshot\_filedata\_verification is non-zero.

Screenshots are validated as follows: The JPEG's MAC is extracted from
the EXIF maker note, and stored. A timestamp string is generated by
calling snprintf(\&str, 20, "%04d:%02d:%02d %02d:%02d:%02d", ...); with
stored timestamp values. If this doesn't match the timestamp string
stored in EXIF, then an error 0xA34CE is returned. Otherwise, the entire
JPEG is loaded into memory, and the stored EXIF maker note is cleared to
zeroes. Then, an HMAC-SHA256 is computed over the entire JPEG using a
hardcoded secret key. if (memcmp(calculated\_hmac, stored\_hmac, 0x10)
== 0), the screenshot is valid, else 0xA3ACE is returned.

In [3.0.0](3.0.0.md "wikilink"), MAC calculation was changed: now,
instead of calculating an HMAC, a plain SHA256 hash is calculated.
capsrv basically does screenshot\_kek =
spl::GenerateAesKek(<hardcoded screenshot_kek_source>);
spl::LoadAesKey(screenshot\_kek, <hardcoded screenshot_key_source>); MAC
= spl::ComputeCmac(hash);

## Videos

[4.0.0](4.0.0.md "wikilink") includes video playback etc support in
Album via mp4. These include a JPEG thumbnail, which is used for video
"validation". The EXIF is also much larger: the MakerNote is
0x498-bytes, with encrypted data starting at offset +0x8. This
encryption uses AES-CTR with hardcoded key/ctr. MAC calculation works
the same way as the [3.0.0](3.0.0.md "wikilink")+ JPEG MAC calculation,
except with a different movie\_kek\_source/movie\_key\_source.

Note: the Album process itself uses libstagefright for video playback.

[Category:Services](Category:Services "wikilink")

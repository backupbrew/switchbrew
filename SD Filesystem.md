## Overview

`sd`  
`└── Nintendo`  
`    ├── `[`Album`](#Album "wikilink")  
`    ├── Contents`  
`    └── save`

All files stored under the Contents sub-directories and save/ use the
[NAX0](NAX0.md "wikilink") format.

## Album

Contains the screenshots: "YYYY/MM/DD/<hex>.jpg". These are
[MAC](Capture%20services#Notes.md##Notes "wikilink")'d, contents with an
invalid MAC will display an error on view.

## save

Contains system-only savedata "8000000000000000" and "8000000000000124".

8000000000000000 is a [FS module](Filesystem%20services.md "wikilink")
save describing the other system savedata on the SD card (normally only
8000000000000124).

8000000000000124 is the [NCM module](NCM%20services.md "wikilink") save
describing what contents are installed to the SD card.

## Contents

It seems this directory didn't exist until [2.0.0](2.0.0.md "wikilink").

Contains directories "placehld" and "registered".

Also contains file "private", which stores the 0x10 [sd card seed
verification
vector](Filesystem%20services#SetSdCardEncryptionSeed.md##SetSdCardEncryptionSeed "wikilink").

### placehld and registered

"placehld" and "registered" store game contents; contents are initially
downloaded temporarily into the "placehld" folder, and then [moved into
the registered
folder](NCM%20services#IContentStorage.md##IContentStorage "wikilink")
when downloading is complete.

Some of the "placehld/<hex>" directories are temp-only and don't get
moved into "registered".

No titleIDs are stored in any directories/filenames here.

All hex IDs (shown below as 000000XX and
[NcaId](NCM%20services#NcaID.md##NcaID "wikilink")) used here are unique
per title/content. XX is calculated as the first byte from the output of
the binary SHA-256(Nca directory).

Game contents are stored inside [NAX0](NAX0.md "wikilink") archives; due
to the 4 GB filesize limit on FAT32, contents that are bigger than 4 GB
have additional file contents automatically split into separate files.
This automatic file-splitting occurs even on exFAT SD cards where it is
not necessary.

<sub-directory under Contents>  
`└── <directories with upper-case hex: 000000XX>`  
`    └── `<lower-case hex Nca directory>`.nca`  
`        └── 00 `[`actual`` ``file`` ``for`` ``data``
``storage`](NAX0.md "wikilink")  
`        └── 01 (storage for file data at +4GB in the actual NCA)`  
`        └── {etc}`

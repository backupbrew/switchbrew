This page is for the FS which can be mounted for
[NCAs](NCA.md "wikilink") with
[OpenFileSystem\*](Filesystem%20services.md "wikilink").
Filesystem\_services\#OpenFileSystem|OpenFileSystem\]\] throws errors
when trying to access a NCA-type with a
[FileSystemType](Filesystem%20services#FileSystemType.md##FileSystemType "wikilink")
not listed below.

# NCA-type0

## ContentMeta

Only contains the [.cnmt](NCA.md "wikilink") file. This also how the
0100000000000816 title is mounted.

# NCA-type1

## Logo

Contains the logo gfx displayed when an application is booted. Doesn't
include the "Licensed" gfx.

  - "/NintendoLogo.png" Nintendo logo displayed in the top-left of the
    screen.
  - "/StartupMovie.gif" Nintendo Switch animation displayed in the
    bottom-right of the screen.

# NCA-type2

## ContentData

What the nandsys 8XX SystemData titles
    use.

# NCA-type3

## ContentControl

  - "/[control.nacp](Control.nacp.md "wikilink")".
  - "/icon\_{[Language](Settings%20services#LanguageCode.md##LanguageCode "wikilink")}.dat",
    for every icon with an included language. Just a 256x256 JPEG, no
    MAC which [Album](Album.md "wikilink") screenshots use. EXIF info:
    "Camera Brand" = "Nintendo co., ltd", "Software" = "Nintendo
    AuthoringTool".

# NCA-type4

## ContentManual

# NCA-type5

## ContentManual

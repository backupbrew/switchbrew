This page is for the FS which can be mounted for
[NCAs](NCA.md "wikilink") with
[MountContent\*](Filesystem%20services.md "wikilink"). FS-type below is
the in32 for "MountContent". MountContent throws errors when trying to
access a NCA-type with a FS-type not listed below.

# NCA-type0

## FS-type5

Only contains the [.cnmt](NCA.md "wikilink") file. This also how the
0100000000000816 title is mounted.

# NCA-type1

## FS-type2

Contains the logo gfx displayed when an application is booted. Doesn't
include the "Licensed" gfx.

  - "/NintendoLogo.png" Nintendo logo displayed in the top-left of the
    screen.
  - "/StartupMovie.gif" Nintendo Switch animation displayed in the
    bottom-right of the screen.

# NCA-type2

What the nandsys 8XX SystemData titles use.

## FS-type6

# NCA-type3

## FS-type3

  - "/control.nacp". Roughly equivalent to non-gfx areas of 3DS SMDH.
    Also includes a string for the display-version of this title.
    Contains UTF-8 title name/etc strings, unlike SMDH which uses
    UTF-16.
  - "/icon\_{Language}.dat", for every icon with an included language.
    Just a 256x256 JPEG, no MAC which [Album](Album.md "wikilink")
    screenshots use. EXIF info: "Camera Brand" = "Nintendo co., ltd",
    "Software" = "Nintendo AuthoringTool".

# NCA-type4

## FS-type4

# NCA-type5

## FS-type4

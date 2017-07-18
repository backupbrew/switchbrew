Raw NCAs are encrypted.

The only known section which is not encrypted in the raw NCA is the logo
section, when the NCA includes that section.

## Logo section

Contains the raw FS for the logo FS, see
[here](NCA%20Content%20FS.md "wikilink") for mounted-FS contents.

This is a PFS0.

# PFS0

| Offset | Size | Description                              |
| ------ | ---- | ---------------------------------------- |
| 0x0    | X    | Table of hashes.                         |
| X      | Y    | Zeros for alignment to {alignment size}. |
| X+Y    |      | Start of the PFS0 header.                |

This is the FS which has magicnum "PFS0" at header+0.

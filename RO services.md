Prior to 3.0.0, ro was included as part of [Loader
services](Loader%20services.md "wikilink"). Despite the separation, the
service name ldr:ro is retained to maintain compatibility with old
games.

# ldr:ro, ro:1

\[1.0.0-2.3.0\] This is "nn::ldr::detail::IRoInterface"

\[3.0.0+\] This is "nn::ro::detail::IRoInterface".

\[7.0.0+\] ro:1 was added, and also creates nn::ro::detail::IRoInterface
objects.

| Cmd | Name                                            |
| --- | ----------------------------------------------- |
| 0   | [\#LoadNro](#LoadNro "wikilink")                |
| 1   | UnloadNro                                       |
| 2   | [\#LoadNrr](#LoadNrr "wikilink")                |
| 3   | UnloadNrr                                       |
| 4   | [\#Initialize](#Initialize "wikilink")          |
| 10  | \[7.0.0+\] [\#LoadNrrEx](#LoadNrrEx "wikilink") |

## LoadNro

| Word | Value                    |
| ---- | ------------------------ |
| 0    | 0x00000004               |
| 1    | 0x80000012               |
| 2    | 0x00000001               |
| 0-1  | Pid                      |
| 0    | "SCFI"                   |
| 1    | 0x00000000               |
| 2    | Always 0.                |
| 3    | Nro heap address         |
| 4    | Nro size                 |
| 5    | Bss backing heap address |
| 6    | Bss size                 |

## LoadNrr

\[7.0.0+\] A new 8-bit field at NRR + 0x33C (previously padding) must be
0 for this function to succeed.

| Word | Value       |
| ---- | ----------- |
| 0    | 0x00000004  |
| 1    | 0x8000000E  |
| 2    | 0x00000001  |
|      |             |
| 0-1  | Pid         |
| 0    | "SFCI"      |
| 1    | 0x00000002  |
| 2    | Always 0.   |
| 3    | Nrr address |
| 4    | Nrr size    |

## Initialize

| Word | Value                       |
| ---- | --------------------------- |
| 0    | 0x00000004                  |
| 1    | 0x8000000A                  |
| 2    | 0x00000003                  |
| 0-1  | Pid                         |
| 2    | Process handle (0xFFFF8001) |
| 0    | "SFCI"                      |
| 1    | 0x00000004                  |
| 2    | Always 0.                   |

## LoadNrrEx

Takes in a u64 nrr\_address, a u64 nrr\_size, a pid descriptor, and a
process handle.

First, this validates that the pid descriptor matches the pid for the
process handle sent to this-\>Initialize() earlier.

Then, this calls the same function as LoadNrr, except using the passed
process handle instead of the one sent to Initialize.

When called from an ro:1 session, the field at NRR header + 0x33C must
be 0x1. When called from ldr:ro session, the field at NRR header + 0x33C
must be 0x0.

[Category:Services](Category:Services "wikilink")

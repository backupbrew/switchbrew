# Loader services

## ldr:shel

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |

## ldr:ro

| Cmd | Name                                   |
| --- | -------------------------------------- |
| 0   | [\#LoadNro](#LoadNro "wikilink")       |
| 1   | [\#LoadNrr](#LoadNrr "wikilink")       |
| 2   |                                        |
| 3   |                                        |
| 4   | [\#Initialize](#Initialize "wikilink") |

### LoadNro

| Word | Value       |
| ---- | ----------- |
| 0    | 0x00000004  |
| 1    | 0x80000012  |
| 2    | 0x00000001  |
| 0-1  | Pid         |
| 0    | "SCFI"      |
| 1    | 0x00000000  |
| 2    | Always 0.   |
| 3    | Nro address |
| 4    | Nro size    |
| 5    |             |
| 6    | Bss size    |

### LoadNrr

| Word | Value       |
| ---- | ----------- |
| 0    | 0x00000004  |
| 1    | 0x8000000C  |
| 2    | 0x00000001  |
|      |             |
| 0-1  | Pid         |
| 0    | "SFCI"      |
| 1    | 0x00000001  |
| 2    | Nrr address |
| 3    | Nrr size    |

### Initialize

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

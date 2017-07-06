# ldr:dmnt

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |

# ldr:pm

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |
| 3   |      |

# ldr:ro

| Cmd | Name                                   |
| --- | -------------------------------------- |
| 0   | [\#LoadNro](#LoadNro "wikilink")       |
| 1   | UnloadNro                              |
| 2   | [\#LoadNrr](#LoadNrr "wikilink")       |
| 3   | UnloadNrr                              |
| 4   | [\#Initialize](#Initialize "wikilink") |

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

# ldr:shel

| Cmd | Name                                               |
| --- | -------------------------------------------------- |
| 0   | [\#LoadProcess](#LoadProcess "wikilink")           |
| 1   | [\#ClearProcessList](#ClearProcessList "wikilink") |

## LoadProcess

Takes a type-0x19 input buffer with launch arguments (as string), an u32
(size of arguments string), and an input title-id.

Loads a process for the specified title-id and passes along the supplied
arguments. Loaded processes are kept in a queue waiting for PM to launch
them. The maximum number of waiting processes in this list is 10.

## ClearProcessList

Clears the loaded processes waiting queue.

[Category:Services](Category:Services "wikilink")

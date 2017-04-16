Services are system processes running in the background which wait for
incoming requests. When a process wants to communicate with a service,
it first needs to get a handle to the named service, and then it can
communicate with the service via inter-process communication (each
service has a name up to 8 characters).

Handles for services are retrieved from the service manager port, "sm:".
Services are an abstraction of ports, they operate the same way except
regular ports can have their handles retrieved directly from a SVC.

# sm:

| Cmd | Name                                             |
| --- | ------------------------------------------------ |
| 0   | [\#Initialize](#Initialize "wikilink")           |
| 1   | [\#GetService](#GetService "wikilink")           |
| 2   | [\#RegisterService](#RegisterService "wikilink") |
| 3   |                                                  |

## Initialize

| Word | Value      |
| ---- | ---------- |
| 0    | 0x00000004 |
| 1    | 0x8000000A |
| 2    | 0x00000001 |
| 0-1  | Pid        |
| 0    | "SCFI"     |
| 1    | 0x00000000 |
| 2    | Always 0.  |

## GetService

| Word | Value                                        |
| ---- | -------------------------------------------- |
| 0    | 0x00000004                                   |
| 1    | 0x0000000A                                   |
| 0    | "SCFI"                                       |
| 1    | 0x00000001                                   |
| 2    | Service name, zero padded and casted to u64. |

## RegisterService

| Word | Value                                        |
| ---- | -------------------------------------------- |
| 0    | 0x00000004                                   |
| 1    | 0x0000000C                                   |
| 0    | "SCFI"                                       |
| 1    | 0x00000002                                   |
| 2    | Service name, zero padded and casted to u64. |
| 3    | Max sessions? 32-bit integer.                |
| 4    | Unknown bool                                 |

# List

| Service names                      | Description                                                            | Notes                                      |
| ---------------------------------- | ---------------------------------------------------------------------- | ------------------------------------------ |
| acc:u1, acc:su                     | [Account services](Account%20services.md "wikilink")                   | u1: for user 1?                            |
| appletAE                           | Applet Accessor services                                               |                                            |
| aoc:u                              | AddOn Content services                                                 |                                            |
| audren:u                           | Audio Renderer services                                                |                                            |
| audout:u                           | Audio Out services                                                     |                                            |
| bsd:u, bsd:s                       | Sockets services                                                       |                                            |
| caps:a, caps:c, caps:ss            | Capture services                                                       | a: Album, ss: Screenshot                   |
| fatal:u                            | Fatal Error services                                                   |                                            |
| fsp-srv                            | [Filesystem services](Filesystem%20services.md "wikilink")             |                                            |
| hid, hid:dbg, hid:sys              | HID services                                                           |                                            |
| ldn:m                              | Local Network Monitor services                                         |                                            |
| ldr:ro                             | RO services                                                            |                                            |
| ldr:shel                           | [Loader services](Loader%20services.md "wikilink")                     |                                            |
| lm                                 | Log services                                                           |                                            |
| lr                                 | ?                                                                      |                                            |
| erpt:c                             | ERPT(?) services                                                       |                                            |
| mii:u, mii:e                       | Mii services                                                           |                                            |
| mm:u                               | NvMM services                                                          |                                            |
| nifm:u, nifm:a, nifm:s             | Network Interface services                                             | u: User, a: Applet, s: System              |
| nim:shp                            | NIM services                                                           | shp: eShop                                 |
| ns:am, ns:su, ns:dev               | [NS Services](NS%20Services.md "wikilink")                             | am: Application Manager, su: System Update |
| nsd:u, nsd:a                       | NSD services                                                           |                                            |
| nvmemp                             | NVIDIA Memory Profiling services                                       |                                            |
| nvdrv:a                            | [NV services](NV%20services.md "wikilink")                             |                                            |
| ovln:rcv, ovln:snd                 | Overlay Notification services                                          |                                            |
| pdm:ntfy, pdm:qry                  | Play Log services                                                      |                                            |
| pl:u                               | Shared Font services                                                   |                                            |
| pm:bm, pm:shell                    | [Process Manager services](Process%20Manager%20services.md "wikilink") |                                            |
| prepo:u, prepo:s, prepo:m, prepo:a | Prepo(?) services                                                      |                                            |
| set, set:sys                       | Settings services                                                      | sys: System settings                       |
| sfdnsres                           | DNS resolver services                                                  |                                            |
| ssl                                | SSL services                                                           |                                            |
| time:u, time:a, time:s             | Time services                                                          |                                            |
| vi:m, vi:s, vi:u                   | VI (Camera?) services                                                  |                                            |

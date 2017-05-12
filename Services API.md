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
| 0    | "SFCI"     |
| 1    | 0x00000000 |
| 2    | Always 0.  |

## GetService

| Word | Value                                        |
| ---- | -------------------------------------------- |
| 0    | 0x00000004                                   |
| 1    | 0x0000000A                                   |
| 0    | "SFCI"                                       |
| 1    | 0x00000001                                   |
| 2    | Service name, zero padded and casted to u64. |

## RegisterService

| Word | Value                                        |
| ---- | -------------------------------------------- |
| 0    | 0x00000004                                   |
| 1    | 0x0000000C                                   |
| 0    | "SFCI"                                       |
| 1    | 0x00000002                                   |
| 2    | Service name, zero padded and casted to u64. |
| 3    | Max sessions? 32-bit integer.                |
| 4    | Unknown bool                                 |

# Service List

| Service names                                    | Description                                                                          | Notes                                      |
| ------------------------------------------------ | ------------------------------------------------------------------------------------ | ------------------------------------------ |
| acc:u1, acc:su                                   | [Account services](Account%20services.md "wikilink")                                 | u1: for user 1?                            |
| appletAE                                         | Applet Accessor services                                                             |                                            |
| aoc:u                                            | AddOn Content services                                                               |                                            |
| audren:u                                         | Audio Renderer services                                                              |                                            |
| audout:u                                         | Audio Out services                                                                   |                                            |
| bgtc:t, bgtc:sc                                  | Task services                                                                        |                                            |
| bsd:u, bsd:s                                     | Sockets services                                                                     |                                            |
| caps:a, caps:c, caps:ss                          | Capture services                                                                     | a: Album, ss: Screenshot                   |
| fatal:u                                          | Fatal Error services                                                                 |                                            |
| friend:u, friend:v, friend:m, friend:s, friend:a | Friend services                                                                      |                                            |
| fsp-srv                                          | [Filesystem services](Filesystem%20services.md "wikilink")                           |                                            |
| hid, hid:dbg, hid:sys                            | [HID services](HID%20services.md "wikilink")                                         |                                            |
| ldn:m                                            | [Local Network Monitor services](Local%20Network%20Monitor%20services.md "wikilink") |                                            |
| ldr:ro, ldr:shel                                 | [Loader services](Loader%20services.md "wikilink")                                   |                                            |
| lm                                               | Log services                                                                         |                                            |
| lr                                               | ?                                                                                    |                                            |
| erpt:c                                           | ERPT(?) services                                                                     |                                            |
| mii:u, mii:e                                     | Mii services                                                                         |                                            |
| nifm:u, nifm:a, nifm:s                           | [Network Interface services](Network%20Interface%20services.md "wikilink")           |                                            |
| nim:shp                                          | NIM services                                                                         | shp: eShop                                 |
| ns:am, ns:su, ns:dev                             | [NS Services](NS%20Services.md "wikilink")                                           | am: Application Manager, su: System Update |
| nsd:u, nsd:a                                     | [NSD services](NSD%20services.md "wikilink")                                         |                                            |
| nvdrv:a, nvmemp, mm:u                            | [NV services](NV%20services.md "wikilink")                                           |                                            |
| ovln:rcv, ovln:snd                               | Overlay Notification services                                                        |                                            |
| pctl, pctl:a, pctl:s, pctl:r                     | Parental Control services                                                            |                                            |
| pdm:ntfy, pdm:qry                                | Play Log services                                                                    |                                            |
| pl:u                                             | Shared Font services                                                                 |                                            |
| pm:bm, pm:shell                                  | [Process Manager services](Process%20Manager%20services.md "wikilink")               |                                            |
| prepo:u, prepo:s, prepo:m, prepo:a               | [Play Report services](Play%20Report%20services.md "wikilink")                       |                                            |
| set, set:sys                                     | [Settings services](Settings%20services.md "wikilink")                               | sys: System settings                       |
| sfdnsres                                         | DNS resolver services                                                                |                                            |
| ssl                                              | SSL services                                                                         |                                            |
| time:u, time:a, time:s                           | Time services                                                                        |                                            |
| vi:m, vi:s, vi:u                                 | [Display services](Display%20services.md "wikilink")                                 |                                            |

Services are system processes running in the background which wait for
incoming requests. When a process wants to communicate with a service,
it first needs to get a handle to the named service, and then it can
communicate with the service via inter-process communication (each
service has a name up to 8 characters).

Handles for services are retrieved from the service manager port, "sm:".
Manager service "sm:m" also exists. Services are an abstraction of
ports, they operate the same way except regular ports can have their
handles retrieved directly from a SVC.

# sm:

| Cmd | Name                                                 |
| --- | ---------------------------------------------------- |
| 0   | [\#Initialize](#Initialize "wikilink")               |
| 1   | [\#GetService](#GetService "wikilink")               |
| 2   | [\#RegisterService](#RegisterService "wikilink")     |
| 3   | [\#UnregisterService](#UnregisterService "wikilink") |

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

## UnregisterService

| Word | Value                                        |
| ---- | -------------------------------------------- |
| 0    | 0x00000004                                   |
| 1    | 0x0000000A                                   |
| 0    | "SFCI"                                       |
| 1    | 0x00000003                                   |
| 2    | Service name, zero padded and casted to u64. |

# sm:m

This service is presumably equivalent to 3DS
"srv:pm".

# Service List

| Service names                                                                                                               | Description                                                                          | Notes                                        |
| --------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ | -------------------------------------------- |
| acc:u0, acc:u1, acc:aa, acc:su                                                                                              | [Account services](Account%20services.md "wikilink")                                 | u1: User, su: Admin                          |
| aoc:u                                                                                                                       | AddOn Content services                                                               |                                              |
| appletAE, appletOE                                                                                                          | Applet services                                                                      |                                              |
| apm, apm:p, apm:sys                                                                                                         | ?                                                                                    |                                              |
| arp:r, arp:w                                                                                                                | Activity Report services?                                                            | r: Reader, w: Writer                         |
| audin:a, audin:d, audin:u, audout:a, audout:d, audout:u, audren:a, audren:d, audren:u, audrec:a, audrec:d, audrec:u, audctl | Audio services                                                                       |                                              |
| bcat:a, bcat:u, bcat:m, bcat:s                                                                                              | ?                                                                                    |                                              |
| bgtc:t, bgtc:sc                                                                                                             | Task services                                                                        |                                              |
| bpc, bpc:r                                                                                                                  | [BPC services](BPC%20services.md "wikilink")                                         |                                              |
| bsd:u, bsd:s, bsdcfg                                                                                                        | [Sockets services](Sockets%20services.md "wikilink")                                 |                                              |
| btdrv                                                                                                                       | Bluetooth Driver services?                                                           |                                              |
| btm, btm:dbg, btm:sys                                                                                                       | Bluetooth services?                                                                  |                                              |
| caps:a, caps:c, caps:sc, caps:ss                                                                                            | Capture services                                                                     | a: Album, ss: Screenshot                     |
| csrng                                                                                                                       | [Secure RNG services](Secure%20RNG%20services.md "wikilink")                         |                                              |
| erpt:c, erpt:r                                                                                                              | Error Report services                                                                |                                              |
| es                                                                                                                          | ETicket services?                                                                    |                                              |
| ethc:c, ethc:i                                                                                                              | ?                                                                                    |                                              |
| fan                                                                                                                         | ?                                                                                    |                                              |
| fatal:u, fatal:p                                                                                                            | Fatal Error services                                                                 | u: User, p: Privileged?                      |
| fgm, fgm:0, fgm:9                                                                                                           | ?                                                                                    |                                              |
| friend:u, friend:v, friend:m, friend:s, friend:a                                                                            | Friend services                                                                      |                                              |
| fsp-srv, fsp-ldr, fsp-pr                                                                                                    | [Filesystem services](Filesystem%20services.md "wikilink")                           | srv: Main, ldr: Loader, pr: Program Registry |
| gpio                                                                                                                        | GPIO services                                                                        |                                              |
| hid, hid:dbg, hid:sys                                                                                                       | [HID services](HID%20services.md "wikilink")                                         |                                              |
| hwopus                                                                                                                      | ?                                                                                    |                                              |
| i2c, i2c:pcv                                                                                                                | [I2C services](I2C%20services.md "wikilink")                                         |                                              |
| irs, irs:sys                                                                                                                | IR Sensor services?                                                                  |                                              |
| lbl                                                                                                                         | [Backlight services](Backlight%20services.md "wikilink")                             |                                              |
| ldn:m, ldn:s, ldn:u                                                                                                         | [Local Network Monitor services](Local%20Network%20Monitor%20services.md "wikilink") |                                              |
| ldr:pm, ldr:ro, ldr:shel, ldr:dmnt                                                                                          | [Loader services](Loader%20services.md "wikilink")                                   |                                              |
| lm                                                                                                                          | Log services                                                                         |                                              |
| lr                                                                                                                          | ?                                                                                    |                                              |
| mii:u, mii:e                                                                                                                | Mii services                                                                         |                                              |
| ncm                                                                                                                         | [Content Manager services](Content%20Manager%20services.md "wikilink")               |                                              |
| news:a, news:c, news:m, news:p, news:v                                                                                      | News Services                                                                        |                                              |
| nfc:am, nfc:mf:u, nfc:user, nfc:sys                                                                                         | NFC services                                                                         |                                              |
| nifm:u, nifm:a, nifm:s                                                                                                      | [Network Interface services](Network%20Interface%20services.md "wikilink")           |                                              |
| nim, nim:shp                                                                                                                | NIM services                                                                         | shp: eShop                                   |
| npns:u, npns:s                                                                                                              | ?                                                                                    |                                              |
| ns:am, ns:su, ns:dev                                                                                                        | [NS Services](NS%20Services.md "wikilink")                                           | am: Application Manager, su: System Update   |
| nsd:u, nsd:a                                                                                                                | [NSD services](NSD%20services.md "wikilink")                                         |                                              |
| ntc                                                                                                                         | ?                                                                                    |                                              |
| nvdrv:a, nvdrv:s, nvdrv:t, nvdrv, nvdrvdbg, nvmemp, mm:u                                                                    | [NV services](NV%20services.md "wikilink")                                           |                                              |
| omm                                                                                                                         | ?                                                                                    |                                              |
| ovln:rcv, ovln:snd                                                                                                          | Overlay Notification services                                                        | rcv: Receiver, snd: Sender                   |
| pcie                                                                                                                        | [PCIe services](PCIe%20services.md "wikilink")                                       |                                              |
| pctl, pctl:a, pctl:s, pctl:r                                                                                                | Parental Control services                                                            |                                              |
| pcv, pcv:imm                                                                                                                | ?                                                                                    |                                              |
| pdm:ntfy, pdm:qry                                                                                                           | Play Log services                                                                    |                                              |
| pinmux                                                                                                                      | ?                                                                                    |                                              |
| pl:u                                                                                                                        | Shared Font services                                                                 |                                              |
| pm:bm, pm:shell                                                                                                             | [Process Manager services](Process%20Manager%20services.md "wikilink")               |                                              |
| prepo:u, prepo:s, prepo:m, prepo:a                                                                                          | [Play Report services](Play%20Report%20services.md "wikilink")                       |                                              |
| psc:c, psc:m                                                                                                                | ?                                                                                    |                                              |
| psm                                                                                                                         | ?                                                                                    |                                              |
| pwm                                                                                                                         | ?                                                                                    |                                              |
| set, set:fd, set:cal, set:sys                                                                                               | [Settings services](Settings%20services.md "wikilink")                               | cal: Calendar?, sys: System Settings         |
| sfdnsres                                                                                                                    | DNS resolver services                                                                |                                              |
| spsm                                                                                                                        | Screen power-supply services?                                                        |                                              |
| ssl                                                                                                                         | SSL services                                                                         |                                              |
| spl:                                                                                                                        | [SPL services](SPL%20services.md "wikilink")                                         |                                              |
| tc                                                                                                                          | ?                                                                                    |                                              |
| time:u, time:a, time:s                                                                                                      | Time services                                                                        |                                              |
| ts                                                                                                                          | ?                                                                                    |                                              |
| uart                                                                                                                        | [UART services](UART%20services.md "wikilink")                                       |                                              |
| usb:ds, usb:hs, usb:pd, usb:pd:c, usb:pm                                                                                    | USB services                                                                         |                                              |
| vi:m, vi:s, vi:u                                                                                                            | [Display services](Display%20services.md "wikilink")                                 |                                              |

[Category:Services](Category:Services "wikilink")

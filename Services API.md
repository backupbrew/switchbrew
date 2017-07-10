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

| Service names                                                                                                                                 | Description                                                                                        | Notes                                        |
| --------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------- |
| acc:u0, acc:u1, acc:aa, acc:su                                                                                                                | [Account services](Account%20services.md "wikilink")                                               | u0: System, u1: User, su: Admin, aa: Baas    |
| ahid:cd, ahid:hdr, hid, hid:dbg, hid:sys, (htc?), irs, irs:sys, xcd:sys                                                                       | [HID services](HID%20services.md "wikilink")                                                       |                                              |
| appletAE, appletOE, idle:sys, omm, spsm                                                                                                       | Applet services, [OMM services](OMM%20services.md "wikilink")                                      |                                              |
| aoc:u, mii:u, mii:e, ns:am, ns:su, ns:dev, pl:u, ovln:rcv, ovln:snd, pdm:ntfy, pdm:qry                                                        | [NS Services](NS%20Services.md "wikilink")                                                         | am: Application Manager, su: System Update   |
| apm, apm:p, apm:sys, fgm, fgm:0, fgm:9, (fgm:dbg?)                                                                                            | [APM services](APM%20services.md "wikilink")                                                       |                                              |
| arp:r, arp:w, bgtc:t, bgtc:sc                                                                                                                 | Glue services                                                                                      | r: Reader, w: Writer                         |
| audin:a, audin:d, audin:u, audout:a, audout:d, audout:u, audren:a, audren:d, audren:u, audrec:a, audrec:d, audrec:u, audctl, codecctl, hwopus | Audio services                                                                                     |                                              |
| bcat:a, bcat:u, bcat:m, bcat:s, news:a, news:c, news:m, news:p, news:v, prepo:u, prepo:s, prepo:m, prepo:a                                    | [BCAT services](BCAT%20services.md "wikilink")                                                     |                                              |
| bpc, bpc:r, pcv, pcv:imm, time:u, time:a, time:s                                                                                              | [BPC services](BPC%20services.md "wikilink")                                                       |                                              |
| bsd:u, bsd:s, bsdcfg, ethc:c, ethc:i, nsd:u, nsd:a, sfdnsres                                                                                  | [Sockets services](Sockets%20services.md "wikilink"), [NSD services](NSD%20services.md "wikilink") |                                              |
| btdrv                                                                                                                                         | Bluetooth Driver services                                                                          |                                              |
| btm, btm:dbg, btm:sys                                                                                                                         | Battery services                                                                                   |                                              |
| caps:a, caps:c                                                                                                                                | Capture services                                                                                   | a: Album, ss: Screenshot                     |
| caps:sc, caps:ss, mm:u, vi:m, vi:s, vi:u, cec-mgr                                                                                             | [Display services](Display%20services.md "wikilink")                                               |                                              |
| csrng                                                                                                                                         | [Secure RNG services](Secure%20RNG%20services.md "wikilink")                                       |                                              |
| dispdrv                                                                                                                                       | Nvnflinger services                                                                                |                                              |
| erpt:c, erpt:r                                                                                                                                | Error Report services                                                                              |                                              |
| es                                                                                                                                            | ETicket services                                                                                   |                                              |
| fan, psm, tc, ts                                                                                                                              | PTM services                                                                                       |                                              |
| fatal:u, fatal:p                                                                                                                              | Fatal Error services                                                                               | u: User, p: Privileged                       |
| friend:u, friend:v, friend:m, friend:s, friend:a                                                                                              | Friend services                                                                                    |                                              |
| fsp-srv, fsp-ldr, fsp-pr                                                                                                                      | [Filesystem services](Filesystem%20services.md "wikilink")                                         | srv: Main, ldr: Loader, pr: Program Registry |
| gpio, i2c, i2c:pcv, pinmux, pwm, uart                                                                                                         | [Bus services](Bus%20services.md "wikilink")                                                       |                                              |
| lbl                                                                                                                                           | [Backlight services](Backlight%20services.md "wikilink")                                           |                                              |
| ldn:m, ldn:s, ldn:u                                                                                                                           | [Local Network Monitor services](Local%20Network%20Monitor%20services.md "wikilink")               |                                              |
| ldr:pm, ldr:ro, ldr:shel, ldr:dmnt                                                                                                            | [Loader services](Loader%20services.md "wikilink")                                                 |                                              |
| lm                                                                                                                                            | Log services                                                                                       |                                              |
| lr, ncm, ncm:v                                                                                                                                | [Location Resolver services](Location%20Resolver%20services.md "wikilink")                         |                                              |
| nfc:am, nfc:mf:u, nfc:user, nfc:sys                                                                                                           | NFC services                                                                                       |                                              |
| nifm:u, nifm:a, nifm:s                                                                                                                        | [Network Interface services](Network%20Interface%20services.md "wikilink")                         |                                              |
| nim, nim:shp, ntc                                                                                                                             | [NIM services](NIM%20services.md "wikilink")                                                       | shp: eShop                                   |
| npns:u, npns:s                                                                                                                                | NPNS services                                                                                      |                                              |
| nvdrv:a, nvdrv:s, nvdrv:t, nvdrv, nvdrvdbg, nvgem:c, nvgem:cd, nvmemp                                                                         | [NV services](NV%20services.md "wikilink")                                                         |                                              |
| pcie                                                                                                                                          | [PCIe services](PCIe%20services.md "wikilink")                                                     |                                              |
| pctl, pctl:a, pctl:s, pctl:r                                                                                                                  | Parental Control services                                                                          |                                              |
| pm:bm, pm:info, pm:shell                                                                                                                      | [Process Manager services](Process%20Manager%20services.md "wikilink")                             |                                              |
| psc:c, psc:m                                                                                                                                  | PSC services                                                                                       |                                              |
| set, set:fd, set:cal, set:sys                                                                                                                 | [Settings services](Settings%20services.md "wikilink")                                             | cal: calibration, sys: System Settings       |
| ssl                                                                                                                                           | [SSL services](SSL%20services.md "wikilink")                                                       |                                              |
| spl:                                                                                                                                          | [SPL services](SPL%20services.md "wikilink")                                                       |                                              |
| usb:ds, usb:hs, usb:pd, usb:pd:c, usb:pm                                                                                                      | USB services                                                                                       |                                              |
| wlan:inf, wlan:lcl, wlan:lg, wlan:lga, wlan:sg, wlan:soc                                                                                      | WLAN services                                                                                      |                                              |

[Category:Services](Category:Services "wikilink")

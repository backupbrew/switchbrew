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

| Cmd | Name              | Arguments                                                                       | Notes |
| --- | ----------------- | ------------------------------------------------------------------------------- | ----- |
| 0   | RegisterProcess   | u32 PID + 2 A Descriptors (unknown, probably service access lists of some kind) |       |
| 1   | UnregisterProcess | u32 PID                                                                         |       |

# Service List

<table>
<thead>
<tr class="header">
<th><p>Service names</p></th>
<th><p>Description</p></th>
<th><p>Notes</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>acc:u0, acc:u1, acc:aa, acc:su</p></td>
<td><p><a href="Account services.md" title="wikilink">Account services</a></p></td>
<td><p>u0: System, u1: User, su: Admin, aa: Baas</p></td>
</tr>
<tr class="even">
<td><p>ahid:cd, ahid:hdr, hid, hid:dbg, hid:sys, (htc?), irs, irs:sys, xcd:sys</p></td>
<td><p><a href="HID services.md" title="wikilink">HID services</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>appletAE, appletOE, idle:sys, omm, spsm</p></td>
<td><p>Applet services, <a href="OMM services.md" title="wikilink">OMM services</a></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>[ <a href="1.0.0.md" title="wikilink">1.0.0</a> +] aoc:u, mii:u, mii:e, ns:am, ns:su, ns:dev, pl:u, ovln:rcv, ovln:snd, pdm:ntfy, pdm:qry</p>
<p>[ <a href="3.0.0.md" title="wikilink">3.0.0</a> +] aoc:u, ns:am2, ns:dev, ns:ec, ns:rid, ns:rt, ns:su, ns:vm, ns:web, ovln:rcv, ovln:snd</p></td>
<td><p><a href="NS Services.md" title="wikilink">NS Services</a></p></td>
<td><p>am: Application Manager, su: System Update</p></td>
</tr>
<tr class="odd">
<td><p>apm, apm:p, apm:sys, fgm, fgm:0, fgm:9, (fgm:dbg?)</p></td>
<td><p><a href="APM services.md" title="wikilink">APM services</a></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>arp:r, arp:w, bgtc:t, bgtc:sc</p></td>
<td><p>Glue services</p></td>
<td><p>r: Reader, w: Writer</p></td>
</tr>
<tr class="odd">
<td><p>audin:a, audin:d, audin:u, audout:a, audout:d, audout:u, audren:a, audren:d, audren:u, audrec:a, audrec:d, audrec:u, audctl, codecctl, hwopus</p></td>
<td><p>Audio services</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>bcat:a, bcat:u, bcat:m, bcat:s, news:a, news:c, news:m, news:p, news:v, prepo:u, prepo:s, prepo:m, prepo:a</p></td>
<td><p><a href="BCAT services.md" title="wikilink">BCAT services</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>bpc, bpc:r, pcv, pcv:imm, time:u, time:a, time:s</p></td>
<td><p><a href="BPC services.md" title="wikilink">BPC services</a></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>bsd:u, bsd:s, bsdcfg, ethc:c, ethc:i, nsd:u, nsd:a, sfdnsres</p></td>
<td><p><a href="Sockets services.md" title="wikilink">Sockets services</a>, <a href="NSD services.md" title="wikilink">NSD services</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>btdrv</p></td>
<td><p><a href="Bluetooth Driver services.md" title="wikilink">Bluetooth Driver services</a></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>btm, btm:dbg, btm:sys</p></td>
<td><p>Battery services</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>caps:a, caps:c</p></td>
<td><p><a href="Capture services.md" title="wikilink">Capture services</a></p></td>
<td><p>a: AlbumAccessor, c: AlbumControl</p></td>
</tr>
<tr class="even">
<td><p>caps:sc, caps:ss, mm:u, vi:m, vi:s, vi:u, cec-mgr</p></td>
<td><p><a href="Display services.md" title="wikilink">Display services</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>csrng</p></td>
<td><p><a href="Secure RNG services.md" title="wikilink">Secure RNG services</a></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>dispdrv</p></td>
<td><p>Nvnflinger services</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>erpt:c, erpt:r</p></td>
<td><p>Error Report services</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>es</p></td>
<td><p>ETicket services</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>fan, psm, tc, ts</p></td>
<td><p>PTM services</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>fatal:u, fatal:p</p></td>
<td><p>Fatal Error services</p></td>
<td><p>u: User, p: Privileged</p></td>
</tr>
<tr class="odd">
<td><p>friend:u, friend:v, friend:m, friend:s, friend:a</p></td>
<td><p>Friend services</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>fsp-srv, fsp-ldr, fsp-pr</p></td>
<td><p><a href="Filesystem services.md" title="wikilink">Filesystem services</a></p></td>
<td><p>srv: Main, ldr: Loader, pr: Program Registry</p></td>
</tr>
<tr class="odd">
<td><p>gpio, i2c, i2c:pcv, pinmux, pwm, uart</p></td>
<td><p><a href="Bus services.md" title="wikilink">Bus services</a></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>lbl</p></td>
<td><p><a href="Backlight services.md" title="wikilink">Backlight services</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>ldn:m, ldn:s, ldn:u</p></td>
<td><p><a href="Local Network Monitor services.md" title="wikilink">Local Network Monitor services</a></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>[ <a href="1.0.0.md" title="wikilink">1.0.0</a>+ ] ldr:pm, ldr:ro, ldr:shel, ldr:dmnt</p>
<p>[ <a href="3.0.0.md" title="wikilink">3.0.0</a>+ ] ldr:pm, ldr:shell</p></td>
<td><p><a href="Loader services.md" title="wikilink">Loader services</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>lm</p></td>
<td><p>Log services</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>lr, ncm, ncm:v</p></td>
<td><p><a href="NCM services.md" title="wikilink">NCM services</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>nfc:am, nfc:mf:u, nfc:user, nfc:sys</p></td>
<td><p>NFC services</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>nifm:u, nifm:a, nifm:s</p></td>
<td><p><a href="Network Interface services.md" title="wikilink">Network Interface services</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>nim, nim:shp, ntc</p></td>
<td><p><a href="NIM services.md" title="wikilink">NIM services</a></p></td>
<td><p>shp: eShop</p></td>
</tr>
<tr class="even">
<td><p>npns:u, npns:s</p></td>
<td><p>NPNS services</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>nvdrv:a, nvdrv:s, nvdrv:t, nvdrv, nvdrvdbg, nvgem:c, nvgem:cd, nvmemp</p></td>
<td><p><a href="NV services.md" title="wikilink">NV services</a></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>pcie</p></td>
<td><p><a href="PCIe services.md" title="wikilink">PCIe services</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>pctl, pctl:a, pctl:s, pctl:r</p></td>
<td><p>Parental Control services</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>pm:bm, pm:info, pm:shell</p></td>
<td><p><a href="Process Manager services.md" title="wikilink">Process Manager services</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>psc:c, psc:m</p></td>
<td><p>PSC services</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>[ <a href="3.0.0.md" title="wikilink">3.0.0</a>+ ] ldr:ro, ro:dmnt</p></td>
<td><p><a href="Loader services.md" title="wikilink">RO services</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>set, set:fd, set:cal, set:sys</p></td>
<td><p><a href="Settings services.md" title="wikilink">Settings services</a></p></td>
<td><p>cal: calibration, sys: System Settings</p></td>
</tr>
<tr class="even">
<td><p>[ <a href="3.0.0.md" title="wikilink">3.0.0</a>+ ] mii:u, mii:e, pdm:ntfy, pdm:qry, pl:u</p></td>
<td><p>Shared Database Services</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>ssl</p></td>
<td><p><a href="SSL services.md" title="wikilink">SSL services</a></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>spl:</p></td>
<td><p><a href="SPL services.md" title="wikilink">SPL services</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>usb:ds, usb:hs, usb:pd, usb:pd:c, usb:pm</p></td>
<td><p>USB services</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>wlan:inf, wlan:lcl, wlan:lg, wlan:lga, wlan:sg, wlan:soc</p></td>
<td><p>WLAN services</p></td>
<td></td>
</tr>
</tbody>
</table>

[Category:Services](Category:Services "wikilink")

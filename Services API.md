Services are system processes running in the background which wait for
incoming requests. When a process wants to communicate with a service,
it first needs to get a handle to the named service, and then it can
communicate with the service via inter-process communication (each
service has a name up to 8 characters).

Handles for services are retrieved from the service manager port, "sm:",
and are released via svcCloseHandle or when a process is terminated or
crashes. Manager service "sm:m" also exists. Services are an abstraction
of ports, they operate the same way except regular ports can have their
handles retrieved directly from a SVC. Services are also able to limit
the number of handles given to other processes.

# sm:

| Cmd | Name                                                 |
| --- | ---------------------------------------------------- |
| 0   | [\#Initialize](#Initialize "wikilink")               |
| 1   | [\#GetService](#GetService "wikilink")               |
| 2   | [\#RegisterService](#RegisterService "wikilink")     |
| 3   | [\#UnregisterService](#UnregisterService "wikilink") |

## Initialize

Takes a pid descriptor and a reserved input u64.

## GetService

Takes a zero-padded service name encoded as an u64 integer. Returns a
handle.

## RegisterService

Takes a zero-padded service name encoded as an u64 integer, an u8 bool,
and an u32 at the next word. Returns a handle.

## UnregisterService

Takes a zero-padded service name encoded as an u64 integer.

# sm:m

| Cmd | Name                                                 |
| --- | ---------------------------------------------------- |
| 0   | [\#RegisterProcess](#RegisterProcess "wikilink")     |
| 1   | [\#UnregisterProcess](#UnregisterProcess "wikilink") |

## RegisterProcess

Takes a pid and two A descriptors with the ACID and ACI0 service lists.
That data originates from [NPDM](NPDM.md "wikilink").

## UnregisterProcess

Takes a pid.

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
<td><p>ahid:cd, ahid:hdr, hid, hid:dbg, hid:sys, irs, irs:sys, xcd:sys</p></td>
<td><p><a href="HID services.md" title="wikilink">HID services</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>appletAE, appletOE, idle:sys, omm, spsm</p></td>
<td><p><a href="AM services.md" title="wikilink">AM services</a></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>[1.0.0+] aoc:u, mii:u, mii:e, ns:am, ns:su, ns:dev, pl:u, ovln:rcv, ovln:snd, pdm:ntfy, pdm:qry</p>
<p>[3.0.0+] aoc:u, ns:am2, ns:dev, ns:ec, ns:rid, ns:rt, ns:su, ns:vm, ns:web, ovln:rcv, ovln:snd</p></td>
<td><p><a href="NS Services.md" title="wikilink">NS Services</a></p></td>
<td><p>am: Application Manager, su: System Update</p></td>
</tr>
<tr class="odd">
<td><p>apm, apm:p, apm:sys, fgm, fgm:0, fgm:9, (fgm:dbg?)</p></td>
<td><p><a href="APM services.md" title="wikilink">APM services</a></p></td>
<td><p>fgm: Fuel guage?</p></td>
</tr>
<tr class="even">
<td><p>arp:r, arp:w, bgtc:t, bgtc:sc</p></td>
<td><p><a href="Glue services.md" title="wikilink">Glue services</a></p></td>
<td><p>r: Reader, w: Writer</p></td>
</tr>
<tr class="odd">
<td><p>audin:a, audin:d, audin:u, audout:a, audout:d, audout:u, audren:a, audren:d, audren:u, audrec:a, audrec:d, audrec:u, audctl, codecctl, hwopus</p></td>
<td><p>Audio services</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>banana</p></td>
<td><p>?</p></td>
<td><p>Some games on [3.0.0+] have access to this service, but it doesn't appear to be present on retail devices.</p></td>
</tr>
<tr class="odd">
<td><p>bcat:a, bcat:u, bcat:m, bcat:s, news:a, news:c, news:m, news:p, news:v, prepo:u, prepo:s, prepo:m, prepo:a</p></td>
<td><p><a href="BCAT services.md" title="wikilink">BCAT services</a></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>bpc, bpc:r, pcv, pcv:arb, pcv:imm, time:u, time:a, time:s</p></td>
<td><p><a href="PCV services.md" title="wikilink">PCV services</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>bsd:u, bsd:s, bsdcfg, ethc:c, ethc:i, nsd:u, nsd:a, sfdnsres</p></td>
<td><p><a href="Sockets services.md" title="wikilink">Sockets services</a>, <a href="NSD services.md" title="wikilink">NSD services</a></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>btdrv</p></td>
<td><p><a href="Bluetooth Driver services.md" title="wikilink">Bluetooth Driver services</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>btm, btm:dbg, btm:sys</p></td>
<td><p>Battery services</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>caps:a, caps:c</p></td>
<td><p><a href="Capture services.md" title="wikilink">Capture services</a></p></td>
<td><p>a: AlbumAccessor, c: AlbumControl</p></td>
</tr>
<tr class="odd">
<td><p>caps:sc, caps:ss, mm:u, vi:m, vi:s, vi:u, cec-mgr</p></td>
<td><p><a href="Display services.md" title="wikilink">Display services</a></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>dispdrv</p></td>
<td><p>Nvnflinger services</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>erpt:c, erpt:r</p></td>
<td><p><a href="Error Report services.md" title="wikilink">Error Report services</a></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>es</p></td>
<td><p>ETicket services</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>fan, psm, tc, ts</p></td>
<td><p><a href="PTM services.md" title="wikilink">PTM services</a></p></td>
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
<td><p>htc, htcs, htc:tenv</p></td>
<td><p><a href="TMA services.md" title="wikilink">TMA services</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>lbl</p></td>
<td><p><a href="Backlight services.md" title="wikilink">Backlight services</a></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>ldn:m, ldn:s, ldn:u</p></td>
<td><p><a href="LDN services.md" title="wikilink">LDN services</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>[1.0.0+] ldr:pm, ldr:ro, ldr:shel, ldr:dmnt</p>
<p>[3.0.0+] ldr:pm, ldr:shel, ldr:dmnt</p></td>
<td><p><a href="Loader services.md" title="wikilink">Loader services</a></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>lm</p></td>
<td><p><a href="Log services.md" title="wikilink">Log services</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>manu</p></td>
<td><p><a href="Manu Services.md" title="wikilink">Manu Services</a></p></td>
<td><p>&quot;Manufacturing&quot;, present in factory firmware but not installed on retail systems.</p></td>
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
<td><p><a href="Parental Control services.md" title="wikilink">Parental Control services</a></p></td>
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
<td><p>[3.0.0+] ldr:ro, ro:dmnt</p></td>
<td><p><a href="Loader services.md" title="wikilink">RO services</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>set, set:fd, set:cal, set:sys</p></td>
<td><p><a href="Settings services.md" title="wikilink">Settings services</a></p></td>
<td><p>cal: calibration, sys: System Settings</p></td>
</tr>
<tr class="even">
<td><p>[3.0.0+] mii:u, mii:e, pdm:ntfy, pdm:qry, pl:u</p></td>
<td><p><a href="Shared Database services.md" title="wikilink">Shared Database services</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>ssl</p></td>
<td><p><a href="SSL services.md" title="wikilink">SSL services</a></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>csrng, spl:</p></td>
<td><p><a href="SPL services.md" title="wikilink">SPL services</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>usb:ds, usb:hs, usb:pd, usb:pd:c, usb:pm</p></td>
<td><p><a href="USB services.md" title="wikilink">USB services</a></p></td>
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

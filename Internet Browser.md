Nintendo Switch does not have a normal Internet Browser for user usage.
However, there is multiple browser applets. It is the [NetFront
NX](https://web.archive.org/web/20170304075230/https://gl.access-company.com/news_event/archives/2017/170303/)
browser, which is based on Webkit.

When linking the Nintendo Account with Facebook, the Facebook Auth
website will open, offering a search box that can be used to browse the
Internet ("LoginApplet"). Alternatively, it can be accessed with [custom
DNS
settings](https://gbatemp.net/threads/web-browser-kind-of-on-the-switch.463094/)
which simulate a Wi-Fi login page ("WifiWebAuthApplet" for
captive-portal).

## Known User Agent Strings

| System Version                                            | UA String                                                                                                                   |
| --------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| [1.0.0](1.0.0.md "wikilink")                              | Mozilla/5.0 (Nintendo Switch; <appletname>) AppleWebKit/601.6 (KHTML, like Gecko) NF/4.0.0.4.25 NintendoBrowser/5.1.0.11682 |
| [2.0.0](2.0.0.md "wikilink")                              | Mozilla/5.0 (Nintendo Switch; <appletname>) AppleWebKit/601.6 (KHTML, like Gecko) NF/4.0.0.5.9 NintendoBrowser/5.1.0.13341  |
| [2.1.0](2.1.0.md "wikilink")-[2.3.0](2.3.0.md "wikilink") | Mozilla/5.0 (Nintendo Switch; <appletname>) AppleWebKit/601.6 (KHTML, like Gecko) NF/4.0.0.5.10 NintendoBrowser/5.1.0.13343 |
| [3.0.0](3.0.0.md "wikilink")                              | Mozilla/5.0 (Nintendo Switch; <appletname>) AppleWebKit/601.6 (KHTML, like Gecko) NF/4.0.0.6.9 NintendoBrowser/5.1.0.14936  |
| [4.0.0](4.0.0.md "wikilink")                              | Mozilla/5.0 (Nintendo Switch; <appletname>) AppleWebKit/601.6 (KHTML, like Gecko) NF/4.0.0.7.9 NintendoBrowser/5.1.0.15785  |

The UA is generated with: "Mozilla/5.0 (Nintendo Switch; <appletname>)
AppleWebKit/<webkitver> (KHTML, like Gecko)
NF/<nfver0>.<nfver1>.<nfver2>
NintendoBrowser/5.<ninver0>.<ninver1>.<ninver2>"

## Browser Applets

| appletname (From UA) | Usage                                                                               | Invalid TLS cert handling                                | Uses whitelist | Title ID         | Notes |
| -------------------- | ----------------------------------------------------------------------------------- | -------------------------------------------------------- | -------------- | ---------------- | ----- |
| WebApplet            | General web-applet for use by applications(online manuals, ...).                    | Displays an error dialog without an option to ignore it. | Yes            | 010000000000100A |       |
| ShopN                | Actual eShop client                                                                 | Just displays an error-code.                             | Yes            | 010000000000100B |       |
| WebApplet            | Offline HTML display                                                                |                                                          |                | 010000000000100F |       |
| LoginApplet          | Nintendo Account linking                                                            | Just displays an error-code.                             | Yes            | 0100000000001010 |       |
| ShareApplet          | Posting screenshots to social media, and (optionally) linking social media accounts | Just displays an error-code.                             | Yes            | 0100000000001010 |       |
| LobbyApplet          | Related to online-multiplayer lobbies                                               | Just displays an error-code.                             | Yes            | 0100000000001010 |       |
| WifiWebAuthApplet    | Captive-portal                                                                      | Displays an error dialog with an option to ignore it.    | No             | 0100000000001011 |       |

When whitelisting is enabled, you can only load page domains included in
the whitelist, otherwise an error is displayed. This only applies to
page navigation. Videos via the

<video>

tag are not affected, likewise with network requests with JS.

No known applets can directly access the SD card via mounting it. This
includes ShareApplet (which posts screenshots from SD to social media).

## OSS

The NROs for the OSS are stored under a separate
[title](Title%20list.md "wikilink"). All of the web-applets use the same
OSS NROs via this title.

String from v2.0 in oss\_wkc.nro: "libcurl/7.50.1".

## Video Playback

WifiWebAuthApplet does not fully support playing videos. It will
[assert](Error%20codes.md "wikilink") with normal videos. The assert
triggers before it even starts MP4 parsing?(For example, selecting a
video from a video-tag will assert even though it doesn't send any
network request for it) However, in some cases with certain MP4s using
vulns it will display an error dialog instead.

With v3.0 WifiWebAuthApplet video-playback was disabled, it now throws
the following error when attempting to play a video: "Support Code:
2809-1212" "This feature is not available." On past system-versions it
would just trigger a fatal-error(see above). Video-playback which
already worked fine under whitelisted-applet, still works fine on v3.0.

## Trusted RootCAs

While the rootCA(s) for Let's Encrypt isn't included, Let's Encrypt is
indirectly trusted via "Digital Signature Trust Co.". This seems to be
only(?) the case for WifiWebAuthApplet, hence non-WifiWebAuthApplet
seems to have a different set of trusted rootCAs.

## WifiWebAuthApplet

When doing a connection-test in system-settings, it will detect that the
captive-portal is required and display an error for it when the response
for "<http://conntest.nintendowifi.net/>" doesn't include the
"X-Organization: Nintendo" HTTP header. The web-applet will not load
until something else attempts a conntest, for example when launching
eShop and prior to LoginApplet launching. The initial page loaded by
this applet is the above conntest URL.

This is only available starting with [2.0.0](2.0.0.md "wikilink").

Prior to version [3.0.0](3.0.0.md "wikilink"), this applet was launched
when attempting a system update from recovery mode if needed. This was
changed to display a "This feature is not available." popup instead.

## Whitelisted Applets

The v2.1 main-codebin page-aligned .text size is 0x1000-bytes larger
than ShopN.

The file at "<data:/whitelist/WhitelistLns.txt>" for
LoginApplet/ShareApplet/LobbyApplet, which doesn't exist in
WifiWebAuthApplet, contains the
following:

` ^https://([0-9A-Za-z\-]+\.)*nintendo\.net(/|$)`  
` ^https?://([0-9A-Za-z\-]+\.)*nintendo\.(co\.jp|com|eu|co\.uk|es|pt|ch|at|de|nl|be|ch|ru|fr|it|co\.za|co\.kr|tw|com\.hk|com\.au|ca|co\.nz)(/|$)`  
` ^https?://([0-9A-Za-z\-]+\.)*nintendo-europe\.com(/|$)`  
` ^https?://([0-9A-Za-z\-]+\.)*nintendoservicecentre\.co\.uk(/|$)`  
` ^https?://([0-9A-Za-z\-]+\.)*google\.(com|ad|ae|com\.af|com\.ag|com\.ai|al|am|co\.ao|com\.ar|as|at|com\.au|az|ba|com\.bd|be|bf|bg|com\.bh|bi|bj|com\.bn|com\.bo|com\.br|bs|bt|co\.bw|by|com\.bz|ca|cd|cf|cg|ch|ci|co\.ck|cl|cm|cn|com\.co|co\.cr|com\.cu|cv|com\.cy|cz|de|dj|dk|dm|com\.do|dz|com\.ec|ee|com\.eg|es|com\.et|fi|com\.fj|fm|fr|ga|ge|gg|com\.gh|com\.gi|gl|gm|gp|gr|com\.gt|gy|com\.hk|hn|hr|ht|hu|co\.id|ie|co\.il|im|co\.in|iq|is|it|je|com\.jm|jo|co\.jp|co\.ke|com\.kh|ki|kg|co\.kr|com\.kw|kz|la|com\.lb|li|lk|co\.ls|lt|lu|lv|com\.ly|co\.ma|md|me|mg|mk|ml|com\.mm|mn|ms|com\.mt|mu|mv|mw|com\.mx|com\.my|co\.mz|com\.na|com\.nf|com\.ng|com\.ni|ne|nl|no|com\.np|nr|nu|co\.nz|com\.om|com\.pa|com\.pe|com\.pg|com\.ph|com\.pk|pl|pn|com\.pr|ps|pt|com\.py|com\.qa|ro|ru|rw|com\.sa|com\.sb|sc|se|com\.sg|sh|si|sk|com\.sl|sn|so|sm|sr|st|com\.sv|td|tg|co\.th|com\.tj|tk|tl|tm|tn|to|com\.tr|tt|com\.tw|co\.tz|com\.ua|co\.ug|co\.uk|com\.uy|co\.uz|com\.vc|co\.ve|vg|co\.vi|com\.vn|vu|ws|rs|co\.za|co\.zm|co\.zw|cat)(/|$)`  
` ^https://([0-9A-Za-z\-]+\.)*facebook\.com(/|$)`  
` ^https://([0-9A-Za-z\-]+\.)*twitter\.com(/|$)`

### ShareApplet

The initial page loaded by this applet depends on a flag. non-val1:
"https://web-lp1.share.srv.nintendo.net/" val1:
"https://web-lp1.share.srv.nintendo.net/settings/"

The server will return a HTTP 302 redirect to "https://nintendo.com/"
when the specified User-Agent isn't the one for ShareApplet.

### LobbyApplet

The initial page loaded by this applet is:
"https://web-lp1.znc.srv.nintendo.net/lobby/".

The content of the above URL refers to "rooms",
"NxView\_Img\_Google\_Play\_Icon", etc.

And also:

` Your room has been created.`  
` `  
` You can invite friends to the room via`  
` the Nintendo Switch Online Lounge app.`

## ShopN

The initial page loaded by ShopN seems to be the following:
"https://bugyo.hac.lp1.eshop.nintendo.net/ashigaru/". This can be
accessed via computer possesed the certificat ShopN.

The file at "<data:/whitelist/WhitelistEc.txt>", which doesn't exist in
WifiWebAuthApplet, contains the following:

` ^https://([0-9A-Za-z\-]+\.)*eshop\.nintendo\.net($|/)`  
` ^https?://([0-9A-Za-z\-]+\.)*nintendo\.(co\.jp|com|de)($|/)`

## WebApplet

### 010000000000100A

The initial page loaded by this applet is specified by the title which
launched this applet. Plain HTTP is allowed.

The files under "<data:/>" are identical to WifiWebAuthApplet except
that the content of each file differs.

This applet uses a whitelist, but it doesn't come from "<data:/>" like
whitelisted-applet.

#### WebApplet launch with Tetris

The Tetris game/demo can be used to launch the online-WebApplet. This
*only* applies to the JPN region of the game/demo: "ぷよぷよ™テトリス®Ｓ"(aka
"Puyo Puyo Tetris"). Note that the gamecard for this can be used to
launch the online-WebApplet on system-version \>=1.0.0.

First, launch the offline-WebApplet for the manual:

  - Game: Main-menu -\> press A with the already selected top menu
    button -\> press the R button.
  - Demo: Main-menu -\> select menu button on the right side -\> press
    A.

Then in the manual:

  - Press A -\> select the bottom menu entry in the list.
  - Select the SEGA icon -\> press A.

The offline-WebApplet will then launch the online-WebApplet with the
plain-http "http://sega.jp/" URL. Non-JPN regions of Tetris don't have
any external link in the manual. For example, with your own DNS-server
setup to return your own server address for this domain, you can load
your own content for use with online-WebApplet.

As of 12/01/2017 this still works on the latest update for Tetris
(version 1.1.2).

#### WebApplet launch with Pinball FX3

The free game Pinball FX3 can also be used to launche the
online-WebApplet. I only tested it with the (Europe/German version yet).

  - First, launche the game and press A to go to the Main-menu.

Then open the privacy policy:

Option 1 if you havent connectet your Nintendo account with your Zen
account:

  - Press DPad-right to get to "Matchup" -\> Then press A -\> Press Y to
    see the privacy policy.

Option 2:

  - Press DPad-right 4 times until you reached options -\> A -\> Press 2
    times L -\> Press DPad-down 2 times -\> Press A

This will launch the online-WebApplet with the plain-http
"http://blog.zenstudios.com/privacy\_policy\_console\_de-de.html"(de-de
cause german version). With your own DNS-server you can now load your
own content.(Same as Tetris)

### Offline Applet

Minus TIDs, the [NPDM](NPDM.md "wikilink") is the same as
010000000000100A except 010000000000100A has access to more/other
services.

## Service/FS Access

All browser applets have access to the following services: acc:u1,
appletAE, audin:u, audren:u, audout:u, bsd:u, fatal:u, fsp-srv, hid,
hid:sys, irs, ldn:m, ldr:ro, lm, erpt:c, nifm:s, ns:am, nsd:u, nvdrv:a,
mm:u, pl:u, prepo:s, set, set:sys, sfdnsres, ssl, time:u, vi:s

LoginApplet/ShareApplet/LobbyApplet have access to the above + caps:a.

ShopN has access to the above + nim:shp.

Unlike the applets listed above, WebApplet TID 010000000000100A has
access to the [FS](Filesystem%20services.md "wikilink") MountContent\*
commands. This is so that it can load the whitelist from
"/accessible-urls/accessible-urls.txt" in the mounted FS, from
[NCA](NCA.md "wikilink")-type4 where titleID={application which launched
this applet}.

## Heap

The size used for [svcSetHeapSize](SVC.md "wikilink") by the web-applets
is 0x15600000. Under ShopN, the largest size that can be passed to this
without an error being returned, is 0x1B400000.

## Versions

### [1.0.0](1.0.0.md "wikilink")

"shareddata:/buildinfo/buildinfo.dat" content:

` r:11682`  
` p:NX64`  
` v:Pilot`  
` d:2016-11-25 23:30`  
` n:0.4.25`

### [2.0.0](2.0.0.md "wikilink")

"shareddata:/buildinfo/buildinfo.dat" content:

` r:13341`  
` p:NX64`  
` v:Release`  
` d:2017-02-13 22:57`  
` n:0.5.9`  
` `

### [2.1.0](2.1.0.md "wikilink")

See [here](Switch%20Userland%20Flaws.md "wikilink") for vuln-related
changes.

The WebKit NRO was updated. For the WebKit NRO, the page-aligned size
for the R-X, R--, and RW- pages are the same as v2.0.

  - The actual code in the NRO starts differing starting at offset
    0xE780. In v2.0 the offset following the last code instruction is
    text\_lastpage+0x3F8(text\_end-0xC08), while for v2.1 it's
    text\_lastpage+0xE60(text\_end-0x1A0). Compared to the previous
    version, there's a val0 u32(padding) inserted where the code for the
    import stubs begin, near the end of .text. Relative to that end
    offset going backwards, .text differs starting at v2.0
    textbase+0xD56530 / v2.1 textbase+0xD56F94.
  - The R-- section was updated. Besides the large table(?) which was
    updated(nothing was added/removed there), the strings containing
    "D:/for\_cruiser/release\_182/nx/webkit/" were updated: "182" was
    changed to "189". 0x10-bytes at offset 0x57292C were removed.
    0x8-bytes were inserted at offset 0x14B2B5C in the v2.1 section.
    0x8-bytes were inserted at offset 0x14B5C10 in the v2.1 section. ...
  - The RW- section was updated, mainly for different addrs. Nothing was
    added/removed. Most(?)/all(?) main-codebin func import-addrs
    relative to main-codebin-base are the same as v2.0.

Main-codebin region(titleID 010000000000100B):

  - rtld is same as before basically, minus addrs. Likewise for the
    "nnSdkEmpty" binary following the main-codebin.
  - Various byte values were changed in the main .text.
  - In the main R-- section:
      - The length of a string used with the user-agent changed, due to
        being changed from "{...}.9" to "{...}.10".
      - The version in the following string was changed from "1.2.2" to
        "1.2.3": "FS\_ACCESS: { sdk\_versio n: 1.2.3, spec: NX }"
      - The datetime strings following "b/23876444" was changed from
        "Feb 10 2017" "02:24:47" to "Mar 9 201 7" "21:41:27".
      - A 0x10-byte block prior to SDK library tag strings was updated.
        The version in those strings was changed from "1\_2\_2" to
        "1\_2\_3".
  - The main RW- section appears to be basically the same minus addrs.

All of the other NROs were updated in FS with only the following
changes:

  - The R-X section is identical to the previous version except for the
    0x10-byte block in the NRO header.
  - The R-- section only had version values in "/release\_{ver}/"
    strings updated, see the for\_cruiser path mentioned for WebKit NRO
    above. The only other change was that a 0x10-byte block following a
    "GNU" string was updated.

#### FS

The content of "blacklist:/" and "oceanShared:/" haven't changed. Only
the content of "shareddata:/" and "<data:/>" changed.

##### "shareddata:/"

The following files were updated here(nothing added/removed):

  - /buildinfo/buildinfo.dat
  - /dll/cairo\_wkc.nro
  - /dll/libfont.nro
  - /dll/oss\_wkc.nro
  - /dll/peer\_wkc.nro
  - /dll/webkit\_wkc.nro

That is, every .nro under the above directory was updated.

"shareddata:/buildinfo/buildinfo.dat" content:

` r:13343`  
` p::NX64`  
` v:Release`  
` d:2017-03-14 21:08`  
` n:0.5.10`

##### "<data:/>"

The following files were updated here(nothing added/removed):

  - /.nrr/netfront.nrr
  - /buildinfo/buildinfo.dat

### [3.0.1](3.0.1.md "wikilink")

While main-codebin .text was updated, no actual code was changed.

The .nss path string in main-codebin was changed from
"Q:\\work\\LibraryApplet\\..." to "Q:\\work\\nup\\LibraryApplet\\...".

See [here](3.0.1.md "wikilink") regarding "shareddata:/" buildinfo.

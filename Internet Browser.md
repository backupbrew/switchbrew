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
| [2.0.0](2.0.0.md "wikilink")                              | Mozilla/5.0 (Nintendo Switch; <appletname>) AppleWebKit/601.6 (KHTML, like Gecko) NF/4.0.0.5.9 NintendoBrowser/5.1.0.13341  |
| [2.1.0](2.1.0.md "wikilink")-[2.3.0](2.3.0.md "wikilink") | Mozilla/5.0 (Nintendo Switch; <appletname>) AppleWebKit/601.6 (KHTML, like Gecko) NF/4.0.0.5.10 NintendoBrowser/5.1.0.13343 |

The UA is generated with: "Mozilla/5.0 (Nintendo Switch; <appletname>)
AppleWebKit/<webkitver> (KHTML, like Gecko)
NF/<nfver0>.<nfver1>.<nfver2>
NintendoBrowser/5.<ninver0>.<ninver1>.<ninver2>"

## Browser Applets

| appletname (From UA) | Usage                                                            | Invalid TLS cert handling                                                                                                    | Uses whitelist | Title ID         | Notes |
| -------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | -------------- | ---------------- | ----- |
| WifiWebAuthApplet    | Captive-portal                                                   | Displays an error dialog with an option to ignore it.                                                                        | No             | 0100000000001011 |       |
| LoginApplet          | Nintendo Account linking                                         | Just displays an error-code.                                                                                                 | Yes            | 0100000000001010 |       |
| ShareApplet          | Posting screenshots to social media                              | Just displays an error-code.                                                                                                 | Yes            | 0100000000001010 |       |
| LobbyApplet          | ?                                                                | Just displays an error-code.                                                                                                 | Yes            | 0100000000001010 |       |
| ShopN                | Actual eShop client                                              | Just displays an error-code.                                                                                                 | Yes            | 010000000000100B |       |
| ?                    | General web-applet for use by applications(online manuals, ...). | Displays an error dialog without an option to ignore it.                                                                     |                | ?                |       |
| ?                    | News                                                             | With videos it doesn't accept the cert. It hangs during video loading without displaying any error, have to press B to exit. |                | ?                |       |

When whitelisting is enabled, you can only load page domains included in
the whitelist, otherwise an error is displayed. This only applies to
page navigation. Videos via the

<video>

tag are not affected, likewise with network requests with JS.

## OSS

The NROs for the OSS are stored under a separate
[title](Title%20list.md "wikilink"). All of the web-applets use the same
OSS NROs via this title.

String from v2.0 in oss\_wkc.nro: "libcurl/7.50.1".

## Video Playback

WifiWebAuthApplet does not fully support playing videos. It will crash
with normal videos. However, in some cases with certain MP4s using vulns
it will display an error dialog instead.

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

## Versions

### 2.0.0

"shareddata:/buildinfo/buildinfo.dat" content:

` r:13341`  
` p:NX64`  
` v:Release`  
` d:2017-02-13 22:57`  
` n:0.5.9`  
` `

### 2.1.0

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

"shareddata:/buildinfo/buildinfo.dat" content:

` r:13343`  
` p::NX64`  
` v:Release`  
` d:2017-03-14 21:08`  
` n:0.5.10`

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

| System Version               | UA String                                                                                                                   |
| ---------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| [2.0.0](2.0.0.md "wikilink") | Mozilla/5.0 (Nintendo Switch; <appletname>) AppleWebKit/601.6 (KHTML, like Gecko) NF/4.0.0.5.9 NintendoBrowser/5.1.0.13341  |
| [2.1.0](2.1.0.md "wikilink") | Mozilla/5.0 (Nintendo Switch; <appletname>) AppleWebKit/601.6 (KHTML, like Gecko) NF/4.0.0.5.10 NintendoBrowser/5.1.0.13343 |

The UA is generated with: "Mozilla/5.0 (Nintendo Switch; <appletname>)
AppleWebKit/<webkitver> (KHTML, like Gecko)
NF/<nfver0>.<nfver1>.<nfver2>
NintendoBrowser/5.<ninver0>.<ninver1>.<ninver2>".

## Browser Applets

| appletname (From UA) | Usage                                                            | Invalid TLS cert handling                                                                                                    | Uses whitelist | Notes |
| -------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | -------------- | ----- |
| WifiWebAuthApplet    | Captive-portal                                                   | Displays an error dialog with an option to ignore it.                                                                        | No             |       |
| LoginApplet          | Nintendo Account linking                                         | Just displays an error-code.                                                                                                 | Yes            |       |
| ShopN                | Actual eShop client                                              | Just displays an error-code.                                                                                                 |                |       |
| ?                    | General web-applet for use by applications(online manuals, ...). | Displays an error dialog without an option to ignore it.                                                                     |                |       |
| ?                    | News                                                             | With videos it doesn't accept the cert. It hangs during video loading without displaying any error, have to press B to exit. |                |       |

When whitelisting is enabled, you can only load page domains included in
the whitelist, otherwise an error is displayed. Videos via the

<video>

tag are not affected.

## Video Playback

WifiWebAuthApplet does not fully support playing videos. It will crash
with normal videos. However, in some cases with certain MP4s using vulns
it will display an error dialog instead.

## Trusted RootCAs

While the rootCA(s) for Let's Encrypt isn't included, Let's Encrypt is
indirectly trusted via "Digital Signature Trust Co.".

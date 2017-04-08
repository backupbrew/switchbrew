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
NintendoBrowser/5.<ninver0>.<ninver1>.<ninver2>". See above for the
appletname.

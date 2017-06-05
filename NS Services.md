This is the Switch equivalent of
[this](https://3dbrew.org/wiki/NS_and_APT_Services).

# ns:am

| Cmd  | Name                    |
| ---- | ----------------------- |
| 0    |                         |
| 1    |                         |
| 2    |                         |
| 3    |                         |
| 4    |                         |
| 5    |                         |
| 6    |                         |
| 7    |                         |
| 8    |                         |
| 9    |                         |
| 11   |                         |
| 13   |                         |
| 16   |                         |
| 17   |                         |
| 19   |                         |
| 21   |                         |
| 22   |                         |
| 23   |                         |
| 25   |                         |
| 27   |                         |
| 30   |                         |
| 31   |                         |
| 33   |                         |
| 35   |                         |
| 36   |                         |
| 37   |                         |
| 38   |                         |
| 39   |                         |
| 40   |                         |
| 41   |                         |
| 42   |                         |
| 43   |                         |
| 44   |                         |
| 45   |                         |
| 46   |                         |
| 47   |                         |
| 48   |                         |
| 49   |                         |
| 52   |                         |
| 53   |                         |
| 54   |                         |
| 55   |                         |
| 56   |                         |
| 57   |                         |
| 58   |                         |
| 59   |                         |
| 60   | GetLanguageIdFromString |
| 61   |                         |
| 62   |                         |
| 63   |                         |
| 64   |                         |
| 65   |                         |
| 100  |                         |
| 101  |                         |
| 102  |                         |
| 200  |                         |
| 201  |                         |
| 210  |                         |
| 220  |                         |
| 300  |                         |
| 301  |                         |
| 302  |                         |
| 303  |                         |
| 304  |                         |
| 305  |                         |
| 306  |                         |
| 307  |                         |
| 401  |                         |
| 402  |                         |
| 403  |                         |
| 404  |                         |
| 405  |                         |
| 502  |                         |
| 503  |                         |
| 504  |                         |
| 600  |                         |
| 601  |                         |
| 602  |                         |
| 603  |                         |
| 604  |                         |
| 605  |                         |
| 700  |                         |
| 701  |                         |
| 702  |                         |
| 703  |                         |
| 704  |                         |
| 705  |                         |
| 800  |                         |
| 801  |                         |
| 900  |                         |
| 901  |                         |
| 902  |                         |
| 903  |                         |
| 904  |                         |
| 905  |                         |
| 906  |                         |
| 907  |                         |
| 908  |                         |
| 1000 |                         |
| 1001 |                         |
| 1200 |                         |
| 1300 |                         |
| 1301 |                         |
| 1302 |                         |
| 1400 |                         |
| 1500 |                         |
| 1501 |                         |
| 1502 |                         |
| 1503 |                         |
| 1600 |                         |
| 1700 |                         |
| 1800 |                         |
| 1801 |                         |
| 1802 |                         |

# ns:su

# ns:dev

# AppIDs

| ID   | Description                                                                                                                                                          |
| ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0E | ErrorApplet                                                                                                                                                          |
| 0x10 | PlayerSelect                                                                                                                                                         |
| 0x11 | Swkbd (on-screen keyboard)                                                                                                                                           |
| 0x14 | Ec ([ShopN](Internet%20Browser.md "wikilink")) From ShopN string: "aInfo.appletId == ::nn::applet::AppletId\_LibraryAppletShop".                                     |
| 0x18 | [Whitelisted](Internet%20Browser.md "wikilink") web-applet (From whitelisted web-applet string: "aInfo.appletId == ::nn::applet::AppletId\_LibraryAppletLoginShare") |
| 0x19 | [WifiWebAuth](Internet%20Browser.md "wikilink") (From browser string: "aInfo.appletId == ::nn::applet::AppletId\_LibraryAppletWifiWebAuth")                          |

This seems to be the equivalent of
[this](https://3dbrew.org/wiki/NS_and_APT_Services#AppIDs) ("AppIDs" is
an unofficial name).

# args.shimKind

This is from strings and code in whitelisted web-applet.

"args.shimKind() == ::nn::web::common::ShimKind::Lobby ||
args.shimKind() == ::nn::web::common::ShimKind::Login || args.shimKind()
==
::nn::web::common::ShimKind::Share"

| shimKind value | Description                                                                     |
| -------------- | ------------------------------------------------------------------------------- |
| 2              | One of the types from the above "args.shimKind() ==" string, unknown which one. |
| 4              | One of the types from the above "args.shimKind() ==" string, unknown which one. |
| 7              | One of the types from the above "args.shimKind() ==" string, unknown which one. |

AM (Applet Manager) provides services for interacting with system
applets while abstracting several aspects of power and operation
management.

Contains multiple raw images, with at least the following:
"NN\_OMM\_CHARGING\_BIN\_{begin|end}"(charging icon), low-battery icon,
and the Nintendo Switch logo displayed during system boot.

# appletAE

| Cmd | Name                     |
| --- | ------------------------ |
| 100 | GetISystemAppletProxy    |
| 200 | GetILibraryAppletProxy   |
| 300 | GetIOverlayAppletProxy   |
| 350 | GetIApplicationProxy     |
| 400 | GetILibraryAppletCreator |
|     |                          |

## ISystemAppletProxy

| Cmd  | Name                         |
| ---- | ---------------------------- |
| 0    | GetICommonStateGetter        |
| 1    | GetISelfController           |
| 2    | GetIWindowController         |
| 3    | GetIAudioController          |
| 4    | GetIDisplayController        |
| 10   | GetIProcessWindingController |
| 11   | GetILibraryAppletCreator     |
| 20   | GetIHomeMenuFunctions        |
| 21   | GetIGlobalStateController    |
| 22   | GetIApplicationCreator       |
| 1000 | GetIDebugFunctions           |
|      |                              |

## ILibraryAppletProxy

| Cmd  | Name                          |
| ---- | ----------------------------- |
| 0    | GetICommonStateGetter         |
| 1    | GetISelfController            |
| 2    | GetIWindowController          |
| 3    | GetIAudioController           |
| 4    | GetIDisplayController         |
| 10   | GetIProcessWindingController  |
| 11   | GetILibraryAppletCreator      |
| 20   | GetILibraryAppletSelfAccessor |
| 1000 | GetIDebugFunctions            |
|      |                               |

## IOverlayAppletProxy

| Cmd  | Name                         |
| ---- | ---------------------------- |
| 0    | GetICommonStateGetter        |
| 1    | GetISelfController           |
| 2    | GetIWindowController         |
| 3    | GetIAudioController          |
| 4    | GetIDisplayController        |
| 10   | GetIProcessWindingController |
| 11   | GetILibraryAppletCreator     |
| 20   | GetIOverlayFunctions         |
| 1000 | GetIDebugFunctions           |
|      |                              |

## IApplicationProxy

| Cmd  | Name                         |
| ---- | ---------------------------- |
| 0    | GetICommonStateGetter        |
| 1    | GetISelfController           |
| 2    | GetIWindowController         |
| 3    | GetIAudioController          |
| 4    | GetIDisplayController        |
| 10   | GetIProcessWindingController |
| 11   | GetILibraryAppletCreator     |
| 20   | GetIApplicationFunctions     |
| 1000 | GetIDebugFunctions           |
|      |                              |

## ILibraryAppletCreator

| Cmd | Name                        |
| --- | --------------------------- |
| 0   | GetILibraryAppletAccessor   |
| 1   | TerminateAllLibraryApplets  |
| 2   | AreAnyLibraryAppletsLeft    |
| 10  | CreateStorage               |
| 11  | CreateTransferMemoryStorage |
| 12  | CreateHandleStorage         |
|     |                             |

# appletOE

| Cmd | Name                 |
| --- | -------------------- |
| 0   | GetIApplicationProxy |
|     |                      |

# idle:sys

# omm

Operation Mode Manager (OMM) is a service responsible for arbitrating
the operation changes between docked and handheld modes. Besides
[PTM\_services](PTM%20services.md "wikilink"), this is the only service
that interacts with the [Dock](Dock.md "wikilink") through
[usb:pd\*](USB%20services.md "wikilink").

| Cmd | Name             |
| --- | ---------------- |
| 0   | GetOperationMode |
| 1   | GetOmmWaitEvent  |
| 2   |                  |
| 3   |                  |
| 4   |                  |
| 5   |                  |
| 6   |                  |
| 7   |                  |
| 8   |                  |
| 9   |                  |

# spsm

# Enums

### AppletId

| ID   | Title-id         | Description                                                                                                      |
| ---- | ---------------- | ---------------------------------------------------------------------------------------------------------------- |
| 0x02 | 010000000000100C | "overlayDisp"                                                                                                    |
| 0x03 | 0100000000001000 | "qlaunch"                                                                                                        |
| 0x04 | 0100000000001012 | "starter"                                                                                                        |
| 0x0A | 0100000000001001 | "auth"                                                                                                           |
| 0x0B | 0100000000001002 | "cabinet"                                                                                                        |
| 0x0C | 0100000000001003 | "controller"                                                                                                     |
| 0x0D | 0100000000001004 | "dataErase"                                                                                                      |
| 0x0E | 0100000000001005 | "error"                                                                                                          |
| 0x0F | 0100000000001006 | "netConnect"                                                                                                     |
| 0x10 | 0100000000001007 | "playerSelect"                                                                                                   |
| 0x11 | 0100000000001008 | "swkbd"                                                                                                          |
| 0x12 | 0100000000001009 | "miiEdit"                                                                                                        |
| 0x13 | 010000000000100A | "LibAppletWeb" [WebApplet](Internet%20Browser#010000000000100A.md##010000000000100A "wikilink") applet           |
| 0x14 | 010000000000100B | "LibAppletShop" [ShopN](Internet%20Browser#ShopN.md##ShopN "wikilink") applet                                    |
| 0x15 | 010000000000100D | "photoViewer"                                                                                                    |
| 0x16 | 010000000000100E |                                                                                                                  |
| 0x17 | 010000000000100F | "LibAppletOff" [Offline](Internet%20Browser#Offline%20Applet.md##Offline_Applet "wikilink") applet               |
| 0x18 | 0100000000001010 | "LibAppletLns" [Whitelisted](Internet%20Browser#Whitelisted%20Applets.md##Whitelisted_Applets "wikilink") applet |
| 0x19 | 0100000000001011 | "LibAppletAuth" [WifiWebAuth](Internet%20Browser#WifiWebAuthApplet.md##WifiWebAuthApplet "wikilink") applet      |
| 0x1A | 0100000000001013 | "myPage"                                                                                                         |
|      |                  |                                                                                                                  |

### ShimKind

This is from strings and code in the [
web-applets](Internet%20Browser.md "wikilink").

This indicates the type of web-applet.

| shimKind value | Description       |
| -------------- | ----------------- |
| 2              | LoginApplet       |
| 4              | ShareApplet       |
| 5              | WebApplet         |
| 6              | WifiWebAuthApplet |
| 7              | LobbyApplet       |

[Category:Services](Category:Services "wikilink")

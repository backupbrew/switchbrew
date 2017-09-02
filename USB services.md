One symbol in USB-sysmodule is: "vtable for
nn::usb::detail::UsbComplexTegra21x".

# usb:ds

Used for Switch\<\>PC USB comms, aka Switch-as-device. This service is
used during [factory setup](Factory%20Setup.md "wikilink") by
[manu](Manu%20Services.md "wikilink").

| Cmd | Name                |
| --- | ------------------- |
| 0   | BindComplex         |
| 1   | BindClientProcess   |
| 2   | GetDsInterface      |
| 3   | GetStateChangeEvent |
| 4   |                     |
| 5   | SetVidPidBcd        |

## IDsInterface

| Cmd | Name                      |
| --- | ------------------------- |
| 0   | GetDsEndpoint             |
| 1   | GetSetupEvent             |
| 2   |                           |
| 3   | StartInterface            |
| 4   | StopInterface             |
| 5   |                           |
| 6   |                           |
| 7   | GetCtrlInCompletionEvent  |
| 8   |                           |
| 9   | GetCtrlOutCompletionEvent |
| 10  |                           |
| 11  |                           |

### IDsEndpoint

| Cmd | Name            |
| --- | --------------- |
| 0   | PostBufferAsync |
| 1   |                 |
| 2   |                 |
| 3   | GetReportData   |
| 4   |                 |
| 5   |                 |

# usb:hs

General USB devices usage, used by hid-sysmodule and
bsdsockets-sysmodule.

# usb:pd

Only system-titles with access to this are
[PTM](PTM%20services.md "wikilink") and
[AM](AM%20services.md "wikilink").

# usb:pd:c

USB-sysmodule symbols for this refer to "Cradle", which is the
[Dock](Dock.md "wikilink").

# usb:pm

Presumably Power Management, only system-title using this is
[PTM](PTM%20services.md "wikilink").

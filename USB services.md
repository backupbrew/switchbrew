One symbol in USB-sysmodule is: "vtable for
nn::usb::detail::UsbComplexTegra21x".

# usb:ds

Used for Switch\<\>PC USB comms, aka Switch-as-device. This service is
used during [factory setup](Factory%20Setup.md "wikilink") by
[manu](Manu%20Services.md "wikilink").

| Cmd | Name                                                     |
| --- | -------------------------------------------------------- |
| 0   | [\#BindComplex](#BindComplex "wikilink")                 |
| 1   | [\#BindClientProcess](#BindClientProcess "wikilink")     |
| 2   | [\#GetDsInterface](#GetDsInterface "wikilink")           |
| 3   | [\#GetStateChangeEvent](#GetStateChangeEvent "wikilink") |
| 4   |                                                          |
| 5   | [\#SetVidPidBcd](#SetVidPidBcd "wikilink")               |

## BindComplex

Takes an u32 (**complexId**). [Manu](Manu%20Services.md "wikilink")
sends 0x02.

## BindClientProcess

Takes 1 copy-handle for the current process (0xFFFF8001).

## GetDsInterface

Takes 2 type-5 buffers and returns an
[\#IDsInterface](#IDsInterface "wikilink").
[Manu](Manu%20Services.md "wikilink") sends a 0x09-byte command (e.g.:
0x09, 0x04, 0x04, 0x00, 0x00, 0xFF, 0xFF, 0xFF, 0x00) in the first
buffer and a string ("usb") in the second buffer.

## GetStateChangeEvent

Returns an event handle for state changes.

## SetVidPidBcd

Takes a type-5 buffer with 0x66 bytes of USB descriptor data (see
[manu](Manu%20Services#manu.md##manu "wikilink")).

## IDsInterface

| Cmd | Name                                                                 |
| --- | -------------------------------------------------------------------- |
| 0   | [\#GetDsEndpoint](#GetDsEndpoint "wikilink")                         |
| 1   | [\#GetSetupEvent](#GetSetupEvent "wikilink")                         |
| 2   |                                                                      |
| 3   | [\#EnableInterface](#EnableInterface "wikilink")                     |
| 4   | [\#DisableInterface](#DisableInterface "wikilink")                   |
| 5   |                                                                      |
| 6   |                                                                      |
| 7   | [\#GetCtrlInCompletionEvent](#GetCtrlInCompletionEvent "wikilink")   |
| 8   |                                                                      |
| 9   | [\#GetCtrlOutCompletionEvent](#GetCtrlOutCompletionEvent "wikilink") |
| 10  |                                                                      |
| 11  |                                                                      |

### GetDsEndpoint

Takes a type-5 buffer and returns an
[\#IDsEndpoint](#IDsEndpoint "wikilink").
[Manu](Manu%20Services.md "wikilink") sends a 0x07-byte command (e.g.:
0x07, 0x05, 0x80, 0x02, 0x00, 0x02, 0x00) in the first buffer.

### GetSetupEvent

Returns an event handle for interface setup changes.

### EnableInterface

Takes no arguments. Enables the current interface.

### DisableInterface

Takes no arguments. Disables the current interface.

### GetCtrlInCompletionEvent

Returns an event handle for polling the completion of input control
commands.

### GetCtrlOutCompletionEvent

Returns an event handle for polling the completion of output control
commands.

### IDsEndpoint

| Cmd | Name                                             |
| --- | ------------------------------------------------ |
| 0   | [\#PostBufferAsync](#PostBufferAsync "wikilink") |
| 1   |                                                  |
| 2   |                                                  |
| 3   | [\#GetReportData](#GetReportData "wikilink")     |
| 4   |                                                  |
| 5   |                                                  |

#### PostBufferAsync

Takes an u32 (**size**) and an u64 (**buffer**).

#### GetReportData

Returns 0x84 bytes of report data from the endpoint.

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

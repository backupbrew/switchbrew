One symbol in USB-sysmodule is: "vtable for
nn::usb::detail::UsbComplexTegra21x".

# usb:ds

This is "nn::usb::ds::IDsService".

Used for Switch\<\>PC USB comms, aka Switch-as-device. This seems to
only be usable in handheld-mode with the Switch directly connected to a
host via an USB cable, not(?) in docked-mode. This service is used
during [factory setup](Factory%20Setup.md "wikilink") by
[manu](Manu%20Services.md "wikilink").

This service session is used as an IPC
[domain](IPC%20Marshalling.md "wikilink") by
[manu](Manu%20Services.md "wikilink"). All of these {get-session}
commands also return an output u8 and the u32
\<[domainID](IPC%20Marshalling.md "wikilink")\>, for using those
sessions as
domains.

| Cmd | Name                                                     | Notes |
| --- | -------------------------------------------------------- | ----- |
| 0   | [\#BindDevice](#BindDevice "wikilink")                   |       |
| 1   | [\#BindClientProcess](#BindClientProcess "wikilink")     |       |
| 2   | [\#GetDsInterface](#GetDsInterface "wikilink")           |       |
| 3   | [\#GetStateChangeEvent](#GetStateChangeEvent "wikilink") |       |
| 4   | [\#GetState](#GetState "wikilink")                       |       |
| 5   | \[2.0.0+\] [\#SetVidPidBcd](#SetVidPidBcd "wikilink")    |       |

Initialization done by [manu](Manu%20Services.md "wikilink"):

  - Initial service init:
      - Get service/etc.
      - Uses [\#BindDevice](#BindDevice "wikilink").
      - Uses [\#BindClientProcess](#BindClientProcess "wikilink").
      - Uses [\#GetStateChangeEvent](#GetStateChangeEvent "wikilink").
      - Uses [\#SetVidPidBcd](#SetVidPidBcd "wikilink").
  - Interface init:
      - Uses [\#GetDsInterface](#GetDsInterface "wikilink"), then uses
        commands from that with the rest of the following.
      - Uses [\#GetSetupEvent](#GetSetupEvent "wikilink").
      - Uses
        [\#GetCtrlInCompletionEvent](#GetCtrlInCompletionEvent "wikilink").
      - Uses
        [\#GetCtrlOutCompletionEvent](#GetCtrlOutCompletionEvent "wikilink").
  - Initializes two endpoints via using
    [\#GetDsEndpoint](#GetDsEndpoint "wikilink") twice.

## Configuration

The following is the default USB config strings, while the usbds service
isn't being used. All of the below configuration will reset to the
defaults when all usbds-related sessions are closed. These can be set
with [\#SetVidPidBcd](#SetVidPidBcd "wikilink"). The default string for
Product is loaded from [settings](Settings%20services.md "wikilink")
config. The default is referred to by usb-sysmodule as "Dummy".

` Product: Nintendo Switch`  
` Manufacturer: Nintendo`  
` SerialNumber: SerialNumber`

The following is the default `lsusb -v {...}` output when the usbds
service wasn't used.

The endpoints are configured using
[\#GetDsEndpoint](#GetDsEndpoint "wikilink"), the total number of
endpoints is the number of open [\#IDsEndpoint](#IDsEndpoint "wikilink")
sessions. bInterfaceNumber is {0-based index for the enabled
[\#IDsInterface](#IDsInterface "wikilink") session.} Some of the
interface fields are configured using
[\#GetDsInterface](#GetDsInterface "wikilink").

Additional descriptors for use with interfaces and endpoints can't be
configured with usbds, even though the former is used for the default
HID interface. This seems to be the main(?) restriction with using usbds
for Switch-as-arbitrary-devices. The device class fields can't be
configured, interface class fields are set instead.

When usbds is in use where [\#SetVidPidBcd](#SetVidPidBcd "wikilink")
wasn't used, the VID/PID is 057e:3000.

` Bus 003 Device 006: ID 057e:2000 Nintendo Co., Ltd `  
` Couldn't open device, some information will be missing`  
` Device Descriptor:`  
`   bLength                18`  
`   bDescriptorType         1`  
`   bcdUSB               2.00`  
`   bDeviceClass            0 (Defined at Interface level)`  
`   bDeviceSubClass         0 `  
`   bDeviceProtocol         0 `  
`   bMaxPacketSize0        64`  
`   idVendor           0x057e Nintendo Co., Ltd`  
`   idProduct          0x2000 `  
`   bcdDevice            1.00`  
`   iManufacturer           1 `  
`   iProduct                2 `  
`   iSerial                 3 `  
`   bNumConfigurations      1`  
`   Configuration Descriptor:`  
`     bLength                 9`  
`     bDescriptorType         2`  
`     wTotalLength           34`  
`     bNumInterfaces          1`  
`     bConfigurationValue     1`  
`     iConfiguration          0 `  
`     bmAttributes         0xc0`  
`       Self Powered`  
`     MaxPower              {...}`  
`     Interface Descriptor:`  
`       bLength                 9`  
`       bDescriptorType         4`  
`       bInterfaceNumber        0`  
`       bAlternateSetting       0`  
`       bNumEndpoints           1`  
`       bInterfaceClass         3 Human Interface Device`  
`       bInterfaceSubClass      0 No Subclass`  
`       bInterfaceProtocol      0 None`  
`       iInterface              0 `  
`         HID Device Descriptor:`  
`           bLength                 9`  
`           bDescriptorType        33`  
`           bcdHID               2.00`  
`           bCountryCode            0 Not supported`  
`           bNumDescriptors         1`  
`           bDescriptorType        34 Report`  
`           wDescriptorLength      26`  
`          Report Descriptors: `  
`            ** UNAVAILABLE **`  
`       Endpoint Descriptor:`  
`         bLength                 7`  
`         bDescriptorType         5`  
`         bEndpointAddress     0x81  EP 1 IN`  
`         bmAttributes            3`  
`           Transfer Type            Interrupt`  
`           Synch Type               None`  
`           Usage Type               Data`  
`         wMaxPacketSize     0x0001  1x 1 bytes`  
`         bInterval              16`

## BindDevice

Takes an u32 (**complexId**). [Manu](Manu%20Services.md "wikilink")
sends 0x02.

Binding more than once with the current session is not allowed. Once
this command is used, the USB device will not be listed with `lsusb`
until [\#EnableInterface](#EnableInterface "wikilink") is used.

Returns a not-found error when complexId isn't 0x02, for values 0x0-0x4
at least.

## BindClientProcess

Takes 1 copy-handle for the current process (0xFFFF8001).

## GetDsInterface

Takes 2 type-5 buffers and returns an
[\#IDsInterface](#IDsInterface "wikilink").
[Manu](Manu%20Services.md "wikilink") sends a 0x09-byte command (e.g.:
0x09, 0x04, 0x04, 0x00, 0x00, 0xFF, 0xFF, 0xFF, 0x00) in the first
buffer and a string ("usb") in the second buffer.

When the strlen output for the second buffer is \>=0x40, size 0x40 is
used instead for copying the string. This is the interface name, it's
not sent over USB.

Returns an error when [\#BindDevice](#BindDevice "wikilink") wasn't
used.

Up to 4 interfaces can be used+[enabled](#EnableInterface "wikilink").

Structure of the first buffer(this is the same as
[libusb\_\_interface\_\_descriptor](http://libusb.sourceforge.net/api-1.0/structlibusb__interface__descriptor.html)):

| Offset | Size | Description                                                                                                                                                    |
| ------ | ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x1  | bLength. Must match 0x9.                                                                                                                                       |
| 0x1    | 0x1  | bDescriptorType. Must match 0x4.                                                                                                                               |
| 0x2    | 0x1  | bInterfaceNumber. When 0x4, the bInterfaceNumber is automatically allocated(error will be thrown if no space). Otherwise, it's used directly and must be \<=3. |
| 0x3    | 0x1  | bAlternateSetting. Must match 0x0.                                                                                                                             |
| 0x4    | 0x1  | bNumEndpoints. Ignored.                                                                                                                                        |
| 0x5    | 0x1  | bInterfaceClass                                                                                                                                                |
| 0x6    | 0x1  | bInterfaceSubClass                                                                                                                                             |
| 0x7    | 0x1  | bInterfaceProtocol                                                                                                                                             |
| 0x8    | 0x1  | iInterface. Ignored.                                                                                                                                           |

Only the first 0x9-bytes are used.

## GetStateChangeEvent

Returns an event handle for when the state returned by
[\#GetState](#GetState "wikilink") changes. Signalled when
Switch\<-\>host USB comms change between started/stopped. USB cable
connected/disconnected while at least 1 interface was enabled, or
interface enabled/disabled while the USB cable was connected which then
caused USB-comms state to change.

## GetState

No input. Returns an output u32. Returns an error when
[\#BindDevice](#BindDevice "wikilink") wasn't used.

Returns the current state. Values:

  - 0: Initial state.
  - 6: Device init starting.
  - 3: {Initialization}, previous state is 6.
  - 4: {Initialization}, previous state is 3.
  - 5: Initialization done, data-transfer is now available.

## SetVidPidBcd

Takes a type-5 buffer with 0x66 bytes of USB descriptor data (see
[manu](Manu%20Services#manu.md##manu "wikilink")).

| Offset | Size | Description     |
| ------ | ---- | --------------- |
| 0x0    | 0x2  | VID (idVendor)  |
| 0x2    | 0x2  | PID (idProduct) |
| 0x4    | 0x2  | bcdDevice       |
| 0x6    | 0x20 | Manufacturer    |
| 0x26   | 0x20 | Product         |
| 0x46   | 0x20 | SerialNumber    |

The last 3 blocks are ASCII strings. The data following each string is
all-zero, for padding to size 0x20.

## IDsInterface

This is
"nn::usb::ds::IDsInterface".

| Cmd | Name                                                                 | Notes                                                                                                                        |
| --- | -------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 0   | [\#GetDsEndpoint](#GetDsEndpoint "wikilink")                         |                                                                                                                              |
| 1   | [\#GetSetupEvent](#GetSetupEvent "wikilink")                         |                                                                                                                              |
| 2   |                                                                      | Takes a type-0x6 output buffer, no other output. Memcpys data to outbuf with outsize, uses size 0x8 if outsize is too large. |
| 3   | [\#EnableInterface](#EnableInterface "wikilink")                     |                                                                                                                              |
| 4   | [\#DisableInterface](#DisableInterface "wikilink")                   |                                                                                                                              |
| 5   | [\#CtrlInPostBufferAsync](#CtrlInPostBufferAsync "wikilink")         |                                                                                                                              |
| 6   | [\#CtrlOutPostBufferAsync](#CtrlOutPostBufferAsync "wikilink")       |                                                                                                                              |
| 7   | [\#GetCtrlInCompletionEvent](#GetCtrlInCompletionEvent "wikilink")   |                                                                                                                              |
| 8   | [\#GetCtrlInReportData](#GetCtrlInReportData "wikilink")             |                                                                                                                              |
| 9   | [\#GetCtrlOutCompletionEvent](#GetCtrlOutCompletionEvent "wikilink") |                                                                                                                              |
| 10  | [\#GetCtrlOutReportData](#GetCtrlOutReportData "wikilink")           |                                                                                                                              |
| 11  | [\#StallCtrl](#StallCtrl "wikilink")                                 |                                                                                                                              |

Commands cmd2,
[\#CtrlInPostBufferAsync](#CtrlInPostBufferAsync "wikilink"),
[\#CtrlOutPostBufferAsync](#CtrlOutPostBufferAsync "wikilink"), and
[\#StallCtrl](#StallCtrl "wikilink"), will throw an error if the
interface is not [enabled](#EnableInterface "wikilink").
[\#GetDsEndpoint](#GetDsEndpoint "wikilink") will throw an error if the
interface is [enabled](#EnableInterface "wikilink").

### GetDsEndpoint

Takes a type-5 buffer and returns an
[\#IDsEndpoint](#IDsEndpoint "wikilink").
[Manu](Manu%20Services.md "wikilink") uses this twice for getting two
endpoint sessions, with the following 0x7-byte buffer data:

  - First endpoint: 0x07, 0x05, 0x80, 0x02, 0x00, 0x02, 0x00
      - bLength=0x7
      - bDescriptorType=LIBUSB\_DT\_ENDPOINT
      - bEndpointAddress=LIBUSB\_ENDPOINT\_IN
      - bmAttributes=LIBUSB\_TRANSFER\_TYPE\_BULK
      - wMaxPacketSize=0x200
      - bInterval=0
  - Second endpoint: Same as above except byte2 is
    0x00(bEndpointAddress=LIBUSB\_ENDPOINT\_OUT).

Each field is an u8, except for offset 0x4-0x5 which is an u16.

This structure matches
[libusb\_endpoint\_descriptor](http://libusb.sourceforge.net/api-1.0/structlibusb__endpoint__descriptor.html),
with audio-only-devices fields bRefresh and bSynchAddress removed.

The buffer size must be \>=0x7. Only the first 0x7-bytes from the buffer
are used.

  - Byte0(bLength) must match 0x7.
  - Byte1(bDescriptorType) must match 0x5.
  - Byte2(bEndpointAddress) is only compared with 0x80 to determine
    whether to use an input or output endpoint, the actual
    endpoint-number is allocated automatically by checking state. Hence,
    all input endpoints must use bEndpointAddress==0x80. Up to
    endpoint-number 0xF can be allocated for each endpoint-direction,
    for a total of 16 endpoints including control, and 15 for
    non-control endpoints([\#IDsEndpoint](#IDsEndpoint "wikilink")
    sessions for each direction). This matches the Tegra maximum.

From the Tegra datasheet: "The maximum packet size supported on any
endpoint is 1024 bytes in high-speed mode, for both device and host
modes."

### GetSetupEvent

Returns an event handle. Unknown what triggers signalling, not signalled
during interface-enable / device\<\>host USB-comms init.

### EnableInterface

Takes no arguments. Enables the current interface.

Only one interface can be enabled at a time per bInterfaceNumber. When
bInterfaceNumber is auto-allocate(0x4) for
[\#GetDsEndpoint](#GetDsEndpoint "wikilink") this isn't an issue since
the final bInterfaceNumber will be unique.

Once enabled, the device/interface can then actually be used over USB.

### DisableInterface

Takes no arguments. Disables the current interface.

### CtrlInPostBufferAsync

Same as [\#PostBufferAsync](#PostBufferAsync "wikilink")(with same
input/output), except this uses control input endpoint 0x80.

### CtrlOutPostBufferAsync

Same as [\#PostBufferAsync](#PostBufferAsync "wikilink")(with same
input/output), except this uses control output endpoint 0x00.

### GetCtrlInCompletionEvent

Returns an event handle for polling the completion of input control
commands. Same as
[\#GetCompletionEvent](#GetCompletionEvent "wikilink"), except this uses
control input endpoint 0x80.

### GetCtrlInReportData

Same as [\#GetReportData](#GetReportData "wikilink")(with same
input/output), except this uses control input endpoint 0x80.

### GetCtrlOutCompletionEvent

Returns an event handle for polling the completion of output control
commands. Same as
[\#GetCompletionEvent](#GetCompletionEvent "wikilink"), except this uses
control output endpoint 0x00.

### GetCtrlOutReportData

Same as [\#GetReportData](#GetReportData "wikilink")(with same
input/output), except this uses control output endpoint 0x00.

### StallCtrl

No input/output.

Calls a function with both control endpoints(0x80 and 0x00) with the
same function. From strings: "m\_pProtocol-\>Stall(0x80)"
"m\_pProtocol-\>Stall(0x00)".

### IDsEndpoint

This is
"nn::usb::ds::IDsEndpoint".

| Cmd | Name                                                   | Notes                         |
| --- | ------------------------------------------------------ | ----------------------------- |
| 0   | [\#PostBufferAsync](#PostBufferAsync "wikilink")       |                               |
| 1   |                                                        | No input/output.              |
| 2   | [\#GetCompletionEvent](#GetCompletionEvent "wikilink") |                               |
| 3   | [\#GetReportData](#GetReportData "wikilink")           |                               |
| 4   | [\#Stall](#Stall "wikilink")                           |                               |
| 5   |                                                        | Takes an input u8, no output. |

#### PostBufferAsync

Takes an u32 (**size**) and an u64 (**buffer**). Returns an output u32
(**urbId**). The output urbId can then be used while parsing the output
of [\#GetReportData](#GetReportData "wikilink"), after waiting for the
CompletionEvent to be signalled.

The buffer address must be 0x1000-byte aligned. The input size doesn't
matter. It helps to use svcSetMemoryAttribute to turn off caching on the
buffer.

Used for data-transfer with input/output endpoints.

The user-process must flush dcache for the buffer before using this
command.

When sending data where size is larger than wMaxPacketSize, it will
automatically send multiple USB packets where last packet size =
{remaining size}. Every {wMaxPacketSize}-bytes is a different packet.
This only occurs in some cases. When **size** is ~0x1000000(exact size
unknown), Switch-side silently hangs, while host-side will timeout(no
traffic on USB bus indicating failure).

For receiving data, if size is less than {actual received USB packet
size} the rest of the packet will be discarded. Later PostBufferAsync
cmd(s) will only return data from new packets, not the remainder of the
earlier packet(s).

#### GetCompletionEvent

No input. Returns an output event handle for polling the completion of
[\#PostBufferAsync](#PostBufferAsync "wikilink"), even when it finished
via [\#Stall](#Stall "wikilink").

#### GetReportData

No input. Returns 0x84 bytes of report data from the endpoint. Seems to
be eventually loaded from state, since this doesn't trigger any USB bus
activity. All-zero before PostBufferAsync was used at least
once.

| Offset | Size            | Description                                  |
| ------ | --------------- | -------------------------------------------- |
| 0x0    | 0x10\*0x8(0x80) | 0x8 entries 0x10-bytes each for each report. |
| 0x80   | 0x4             | u32 report count                             |

Entry
data:

| Offset | Size | Description                                                                                                        |
| ------ | ---- | ------------------------------------------------------------------------------------------------------------------ |
| 0x0    | 0x4  | u32 id (urbId from post-buffer commands)                                                                           |
| 0x4    | 0x4  | u32 requestedSize                                                                                                  |
| 0x8    | 0x4  | u32 transferredSize                                                                                                |
| 0xC    | 0x4  | u32 urb status, converted to error-codes. 0x3 = success, 0x4 = 0x828c, 0x5 = 0x748c. All other values are invalid. |
|        |      |                                                                                                                    |

#### Stall

No input/output.

Calls the same function used by [\#StallCtrl](#StallCtrl "wikilink"),
except this uses the endpoint associated with the current session.

Stops in-progress data-transfer done by
[\#PostBufferAsync](#PostBufferAsync "wikilink").

# usb:hs

This is "nn::usb::hs::IClientRootSession".

General USB devices usage, used by hid-sysmodule and
bsdsockets-sysmodule.

# usb:pd

This is "nn::usb::pd::detail::IPdManager".

Only system-titles with access to this are
[PTM](PTM%20services.md "wikilink") and
[AM](AM%20services.md "wikilink").

# usb:pd:c

This is "nn::usb::pd::detail::IPdCradleManager".

USB-sysmodule symbols for this refer to "Cradle", which is the
[Dock](Dock.md "wikilink").

| Cmd | Name | Notes                                   |
| --- | ---- | --------------------------------------- |
| 0   |      | Returns a session handle for the below. |

## Session

This is
"nn::usb::pd::detail::IPdCradleSession".

| Cmd | Name              | Notes                                                                                                                             |
| --- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| 0   | VdmUserWrite      | Input { u32 value; u32 VdmUserId; }. Output {}. If Cradle or RelayBox is connected, issues given VDM with value.                  |
| 1   | VdmUserRead       | Input { u32 VdmUserId; }. Output { u32 value; }. If Cradle or RelayBox is connected, returns u32 response from issuing given VDM. |
| 2   | Vdm20Init         | No input/output. If Cradle or RelayBox is connected, caches result of VDM 0x20.                                                   |
| 3   | GetFwType         | No input. Returns an output u16.                                                                                                  |
| 4   | GetFwRevision     | No input. Returns an output u16.                                                                                                  |
| 5   | GetManufacturerId | No input. Returns an output u16.                                                                                                  |
| 6   | GetDeviceId       | No input. Returns an output u16.                                                                                                  |

Note: The VdmUserId given to VdmUserRead/VdmUserWrite is translated from
the given (enum) value to the actual cmd to send.

# usb:pm

This is "nn::usb::pm::IPmService".

Presumably Power Management, only system-title using this is
[PTM](PTM%20services.md "wikilink").

[Category:Services](Category:Services "wikilink")

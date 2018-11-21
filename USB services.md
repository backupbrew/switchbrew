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
[domainID](IPC%20Marshalling.md "wikilink"), for using those sessions as
domains.

This service can be used by multiple processes at the same time, with
separate interfaces. However, if one process does usbds shutdown, usbds
will reset to defaults even if there's a process still using
it.

| Cmd               | Name                                                     |
| ----------------- | -------------------------------------------------------- |
| 0                 | [\#BindDevice](#BindDevice "wikilink")                   |
| 1                 | [\#BindClientProcess](#BindClientProcess "wikilink")     |
| 2                 | [\#GetDsInterface](#GetDsInterface "wikilink")           |
| 3                 | [\#GetStateChangeEvent](#GetStateChangeEvent "wikilink") |
| 4                 | [\#GetState](#GetState "wikilink")                       |
| \[2.0.0-4.1.0\] 5 | [\#SetVidPidBcd](#SetVidPidBcd "wikilink")               |
| \[5.0.0+\] 5      | ClearDeviceData                                          |
| 6                 | \[5.0.0+\] AddUsbStringDescriptor                        |
| 7                 | \[5.0.0+\] DeleteUsbStringDescriptor                     |
| 8                 | \[5.0.0+\] SetUsbDeviceDescriptor                        |
| 9                 | \[5.0.0+\] SetBinaryObjectStore                          |
| 10                | \[5.0.0+\] Enable                                        |
| 11                | \[5.0.0+\] Disable                                       |

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

pre-5.0.0: The endpoints are configured using
[\#GetDsEndpoint](#GetDsEndpoint "wikilink"), the total number of
endpoints is the number of open [\#IDsEndpoint](#IDsEndpoint "wikilink")
sessions. bInterfaceNumber is {0-based index for the enabled
[\#IDsInterface](#IDsInterface "wikilink") session.} Some of the
interface fields are configured using
[\#GetDsInterface](#GetDsInterface "wikilink").

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
| 12  | \[5.0.0+\] AppendConfigurationData                                   |                                                                                                                              |

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
This only occurs in some cases. When **size** is \~0x1000000(exact size
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

This is
"nn::usb::hs::IClientRootSession".

| Cmd | Name                                                                           |
| --- | ------------------------------------------------------------------------------ |
| 0   | [\#BindClientProcess](#BindClientProcess_2 "wikilink")                         |
| 1   | [\#QueryAllInterfaces](#QueryAllInterfaces "wikilink")                         |
| 2   | [\#QueryAvailableInterfaces](#QueryAvailableInterfaces "wikilink")             |
| 3   | [\#QueryAcquiredInterfaces](#QueryAcquiredInterfaces "wikilink")               |
| 4   | [\#CreateInterfaceAvailableEvent](#CreateInterfaceAvailableEvent "wikilink")   |
| 5   | [\#DestroyInterfaceAvailableEvent](#DestroyInterfaceAvailableEvent "wikilink") |
| 6   | [\#GetInterfaceStateChangeEvent](#GetInterfaceStateChangeEvent "wikilink")     |
| 7   | [\#AcquireUsbIf](#AcquireUsbIf "wikilink")                                     |
| 8   | \[6.0.0+\]                                                                     |

General USB devices usage, used by [hid](HID%20services.md "wikilink"),
[bsdsockets](Sockets%20services.md "wikilink"), and \[5.1.0+\]
[audio](Audio%20services.md "wikilink").

Get-service-handle will fail if the current process is already using
usb:ds, however it's successful if it's done separately from the process
using usb:ds.

## BindClientProcess

Takes 1 copy-handle for the current process (0xFFFF8001).

## QueryAllInterfaces

Takes a 0x10-byte input struct and a type-0x6 output buffer, returns an
output u32 total\_entries.

The output buffer contains an array of
[\#UsbHsInterface](#UsbHsInterface "wikilink").

## QueryAvailableInterfaces

Takes a 0x10-byte input struct and a type-0x6 output buffer, returns an
output s32 total\_entries.

The output buffer contains an array of
[\#UsbHsInterface](#UsbHsInterface "wikilink").

HID-sysmodule uses the following for the input struct:
`80 00 00 00 00 00 00 00 00 00 00 00 00 03 00 00`

## QueryAcquiredInterfaces

Takes a type-0x6 output buffer and returns an output s32 total\_entries.

The output buffer contains an array of
[\#UsbHsInterface](#UsbHsInterface "wikilink"), for each interface which
was acquired with [\#AcquireUsbIf](#AcquireUsbIf "wikilink").

## CreateInterfaceAvailableEvent

Takes an input u8 and a 0x10-byte struct, and returns an output handle.
The input value must be 0..2. This is used as an index in a table.

The struct is located at +2 from the u8 in IPC rawdata. This struct is
the same as the one used for
[\#QueryAvailableInterfaces](#QueryAvailableInterfaces "wikilink").

When signaled, this indicates that the user-process should use
[\#QueryAvailableInterfaces](#QueryAvailableInterfaces "wikilink") and
[\#AcquireUsbIf](#AcquireUsbIf "wikilink") with the output interfaces
(and the rest of interface setup).

## DestroyInterfaceAvailableEvent

Takes an input u8, no output. The input value must be 0..2.

Clears state associated with the input index. This is the same state
setup by
[\#CreateInterfaceAvailableEvent](#CreateInterfaceAvailableEvent "wikilink").

## GetInterfaceStateChangeEvent

No input, returns an output event handle with autoclear disabled.

When signaled, this indicates that the user-process should use
[\#QueryAcquiredInterfaces](#QueryAcquiredInterfaces "wikilink") and
cleanup state for interfaces which were already initialized.

## AcquireUsbIf

Takes an input u32 and a type-0x6 output buffer, returns an
[\#IClientIfSession](#IClientIfSession "wikilink").

The input u32 is from the u32 at entry+0 from the associated
[\#QueryAvailableInterfaces](#QueryAvailableInterfaces "wikilink")
output entry. User-processes use size 0x1B8 for the output buffer. The
output buffer contains the first 0x1B8-bytes from
[\#UsbHsInterface](#UsbHsInterface "wikilink").

## IClientIfSession

This is
"nn::usb::hs::IClientIfSession".

| Cmd | Name                                                         | Notes                                                                                                    |
| --- | ------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------- |
| 0   |                                                              | No input, returns an output handle.                                                                      |
| 1   | [\#SetInterface](#SetInterface "wikilink")                   |                                                                                                          |
| 2   | [\#GetInterface](#GetInterface "wikilink")                   |                                                                                                          |
| 3   | [\#GetAlternateInterface](#GetAlternateInterface "wikilink") |                                                                                                          |
| 4   | [\#GetCurrentFrame](#GetCurrentFrame "wikilink")             |                                                                                                          |
| 5   | [\#CtrlXferAsync](#CtrlXferAsync "wikilink")                 |                                                                                                          |
| 6   |                                                              | No input, returns an output handle. Signaled when [\#CtrlXferAsync](#CtrlXferAsync "wikilink") finishes. |
| 7   | [\#GetCtrlXferReport](#GetCtrlXferReport "wikilink")         |                                                                                                          |
| 8   | [\#ResetDevice](#ResetDevice "wikilink")                     |                                                                                                          |
| 9   | [\#OpenUsbEp](#OpenUsbEp "wikilink")                         |                                                                                                          |

Official sw uses autoclear=false for the above events.

Immediately after opening the session, official sw uses cmd0 and cmd6.

### SetInterface

Takes an input u8 and a type-0x6 output buffer, no output. The output
buffer contains the first 0x1B8-bytes from
[\#UsbHsInterface](#UsbHsInterface "wikilink").

### GetInterface

Takes a type-0x6 output buffer, no output. The output buffer contains
the first 0x1B8-bytes from
[\#UsbHsInterface](#UsbHsInterface "wikilink").

### GetAlternateInterface

Takes an input u8 and a type-0x6 output buffer, no output. The output
buffer contains the first 0x1B8-bytes from
[\#UsbHsInterface](#UsbHsInterface "wikilink").

### GetCurrentFrame

No input, returns an output u32.

### CtrlXferAsync

Takes 2 input u8s (**bmRequestType** and **bRequest**), 3 input u16s
(**wValue**, **wIndex**, and **wLength**), and an input u64 **buffer**,
no output.

### GetCtrlXferReport

Takes a type-0x6 output buffer, no output. The output buffer contains a
[\#XferReport](#XferReport "wikilink").

### ResetDevice

No input/output.

### OpenUsbEp

Takes an input u16 and 4 input u32s, returns a 0x7-byte output struct
and an [\#IClientEpSession](#IClientEpSession "wikilink").

The user-process loads the input params from the endpoint descriptor.
The u16 is libusb\_transfer\_type+1. However, audio-sysmodule passes
hard-coded values for wMaxPacketSize, including 0.

The u32s are: **bEndpointAddress & LIBUSB\_ENDPOINT\_ADDRESS\_MASK**,
**endpoint\_dir**, **unk**, and **wMaxPacketSize**. Where
**endpoint\_dir** is 0x1 for LIBUSB\_ENDPOINT\_OUT, and 0x2 for
LIBSB\_ENDPOINT\_IN.

HID-sysmodule passes hard-coded value 0x1 for **unk**, varies for other
sysmodules.

### IClientEpSession

This is
"nn::usb::hs::IClientEpSession".

| Cmd | Name                                               | Notes                                                                                                          |
| --- | -------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| 0   | [\#Open](#Open "wikilink")                         |                                                                                                                |
| 1   | [\#Close](#Close "wikilink")                       |                                                                                                                |
| 2   |                                                    | No input, returns an output handle. Signaled when [\#PostBufferAsync](#PostBufferAsync_2 "wikilink") finishes. |
| 3   | [\#Populate](#Populate "wikilink")                 |                                                                                                                |
| 4   | [\#PostBufferAsync](#PostBufferAsync_2 "wikilink") |                                                                                                                |
| 5   | [\#GetXferReport](#GetXferReport "wikilink")       |                                                                                                                |
| 6   |                                                    | Takes 3 input u32s, 2 input u64s, and a type-0x5 input buffer, returns an output u32.                          |
| 7   | \[4.0.0+\]                                         |                                                                                                                |
| 8   | \[4.0.0+\]                                         |                                                                                                                |

Official sw uses autoclear=false for the above event.

Immediately after opening the endpoint session, official sw uses
[\#Populate](#Populate "wikilink") and cmd2.

#### Open

No input/output.

#### Close

No input/output.

Used by official sw prior to closing the endpoint session.

#### Populate

No input/output.

Used after opening the endpoint session (see above).

#### PostBufferAsync

Takes an input u32 **size**, an input u64 **buffer**, and an input u64,
returns an output u32 **xferId**.

HID-sysmodule passes value 0 for the last u64.

#### GetXferReport

Takes an input u32 and a type-0x6 output buffer, returns an output u32
**count**.

The input u32 specifies the total number of entries to read, this must
fit within the specified buffer size. The output u32 is the total actual
output entries.

The buffer contains an array of
[\#XferReport](#XferReport "wikilink").

# UsbHsInterface

| Offset | Size | Description                                                                                                                                             |
| ------ | ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x0    | 0x4  | ID value passed to other cmds. This is -1 with [\#QueryAllInterfaces](#QueryAllInterfaces "wikilink") output, hence this field is unused with that cmd. |
| 0x4    | 0x4? | deviceID                                                                                                                                                |
| 0x8    | 0x4? | ?                                                                                                                                                       |
| 0xC    |      | usb\_interface\_descriptor                                                                                                                              |
| 0x23   | 0x69 | OUTPUT usb\_endpoint\_descriptors, 15 max.                                                                                                              |
| 0x8C   | 0x69 | INPUT usb\_endpoint\_descriptors, 15 max.                                                                                                               |
| 0x1B8  | ?    | "HsDevice-/L<unk0>/P<portnum>/A<unk1>" string (this is "FsDevice..." for the Dock USB 3.0 bus).                                                         |
| 0x1F8  | 0x4? | busID                                                                                                                                                   |
| 0x1FC  | 0x4? | Duplicate of +0x4.                                                                                                                                      |
| 0x200  |      | usb\_device\_descriptor, then usb\_config\_descriptor immediately afterwards.                                                                           |
| 0x220  | 0x8  | Unknown u64 timestamp for when the device was inserted?                                                                                                 |

This is a 0x228-byte struct (unofficial name).

# XferReport

| Offset | Size | Description              |
| ------ | ---- | ------------------------ |
| 0x0    | 0x4  | ?                        |
| 0x4    | 0x4  | Result                   |
| 0x8    | 0x4  | ?                        |
| 0xC    | 0x4  | Actual transferred size. |
| 0x10   | 0x8? | ?                        |

This is a 0x18-byte struct.

Official sw only uses the Result/size fields.

# usb:pd

This is "nn::usb::pd::detail::IPdManager".

| Cmd | Name         |
| --- | ------------ |
| 0   | GetPdSession |

Only system-titles with access to this are
[ptm](PTM%20services.md "wikilink") and
[am](AM%20services.md "wikilink").

## IPdSession

This is "nn::usb::pd::detail::IPdSession".

| Cmd | Name                      |
| --- | ------------------------- |
| 0   | BindNoticeEvent           |
| 1   | UnbindNoticeEvent         |
| 2   | GetStatus                 |
| 3   | GetNotice                 |
| 4   | EnablePowerRequestNotice  |
| 5   | DisablePowerRequestNotice |
| 6   | ReplyPowerRequest         |

# usb:pd:c

This is "nn::usb::pd::detail::IPdCradleManager".

| Cmd | Name               | Notes                                   |
| --- | ------------------ | --------------------------------------- |
| 0   | GetPdCradleSession | Returns a session handle for the below. |

USB-sysmodule symbols for this refer to "Cradle", which is the
[Dock](Dock.md "wikilink").

## IPdCradleSession

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
| 7   | \[3.0.0+\]        |                                                                                                                                   |
| 8   | \[3.0.0+\]        |                                                                                                                                   |

Note: The VdmUserId given to VdmUserRead/VdmUserWrite is translated from
the given (enum) value to the actual cmd to send.

# usb:pm

This is "nn::usb::pm::IPmService".

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |
| 3   |      |
| 4   |      |
| 5   |      |

USB Port Manager, only system-title using this is
[ptm](PTM%20services.md "wikilink").

[Category:Services](Category:Services "wikilink")

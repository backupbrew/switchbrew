This process was added in firmware version 4.0.0.

Safemode can be launched by a button combo at boot and has the task of
performing any pending system updates.

# Initialization

It calls
[GetServiceDiscoveryControlSettings](Settings%20services#set:sys.md##set:sys "wikilink")
to check whether updates need to be installed or not. If no updates need
to be installed it calls
[RebootSystem](PCV%20services#bpc.md##bpc "wikilink"), otherwise, the
process continues.

It creates and starts a new thread with the sole purpose of setting up
the display and showing a progress bar using raw graphics data embedded
in the sysmodule's binary.

The display is configured as
follows:

`*(u32 *)DC_CMD_DISPLAY_WINDOW_HEADER = 0x00000040;    // WINDOW_C_SELECT`  
`*(u32 *)DC_WIN_WIN_OPTIONS = 0x00000000;              // NO_OPTIONS`  
`*(u32 *)DC_CMD_DISPLAY_WINDOW_HEADER = 0x00000020;    // WINDOW_B_SELECT`  
`*(u32 *)DC_WIN_WIN_OPTIONS = 0x00000000;              // NO_OPTIONS`  
`*(u32 *)DC_CMD_DISPLAY_WINDOW_HEADER = 0x00000010;    // WINDOW_A_SELECT`  
`*(u32 *)DC_WIN_WIN_OPTIONS = 0x00000000;              // NO_OPTIONS`  
`*(u32 *)DC_DISP_DISP_WIN_OPTIONS = 0x20000000;        // DSI_ENABLE`  
`*(u32 *)DC_WIN_COLOR_DEPTH = 0x0000000D;              // WIN_COLOR_DEPTH_R8G8B8A8`  
`*(u32 *)DC_WIN_WIN_OPTIONS = 0x00000000;              // NO_OPTIONS`  
`*(u32 *)DC_WIN_WIN_OPTIONS = 0x00000000;              // NO_OPTIONS`  
`*(u32 *)DC_WIN_POSITION = 0x00000000;`  
`*(u32 *)DC_WIN_H_INITIAL_DDA = 0x00000000;`  
`*(u32 *)DC_WIN_V_INITIAL_DDA = 0x00000000;`  
`*(u32 *)DC_WIN_PRESCALED_SIZE = 0x05000B40;           // H_PRESCALED_SIZE=1280, V_PRESCALED_SIZE=2880`  
`*(u32 *)DC_WIN_DDA_INCREMENT = 0x10001000;            // H_DDA_INC=0x1000, V_DDA_INC=0x1000`  
`*(u32 *)DC_WIN_SIZE = 0x050002D0;                     // H_SIZE=1280, V_SIZE=720`  
`*(u32 *)DC_WIN_LINE_STRIDE = 0x06000C00;              // UV_LINE_STRIDE=0x600, LINE_STRIDE=0xC00`  
`*(u32 *)DC_WIN_BUFFER_CONTROL = 0x00000000;           // BUFFER_CONTROL_HOST`  
`*(u32 *)DC_WIN_BUFFER_SURFACE_KIND = 0x00000000;      // DC_WIN_BUFFER_SURFACE_PITCH`  
`*(u32 *)DC_WINBUF_START_ADDR = 0xC0000000;`  
`*(u32 *)DC_WINBUF_ADDR_H_OFFSET = 0x00000000;`  
`*(u32 *)DC_WINBUF_ADDR_V_OFFSET = 0x00000000;`  
`*(u32 *)DC_WIN_WIN_OPTIONS = 0x00000000;              // NO_OPTIONS`  
`*(u32 *)DC_DISP_DISP_WIN_OPTIONS = 0x20000000;        // DSI_ENABLE`  
`*(u32 *)DC_WIN_WIN_OPTIONS = 0x00000000;              // NO_OPTIONS`  
`*(u32 *)DC_DISP_DISP_WIN_OPTIONS = 0x20000000;        // DSI_ENABLE`  
`*(u32 *)DC_WIN_WIN_OPTIONS = 0x00000000;              // NO_OPTIONS`  
`*(u32 *)DC_DISP_DISP_WIN_OPTIONS = 0x20000000;        // DSI_ENABLE`  
`*(u32 *)DC_WIN_WIN_OPTIONS = 0x40000000;              // WIN_ENABLE`  
`*(u32 *)DC_CMD_DISPLAY_COMMAND = 0x00000020;          // DISP_CTRL_MODE_C_DISPLAY`  
`*(u32 *)DC_CMD_STATE_CONTROL = 0x00000300;            // GENERAL_UPDATE | WIN_A_UPDATE`  
`*(u32 *)DC_CMD_STATE_CONTROL = 0x00000003;            // GENERAL_ACT_REQ | WIN_A_ACT_REQ`

While this thread is running, safemode proceeds with the actual update
process.

## System update

Safemode sets up service sessions for
[ns:su](NS%20Services.md "wikilink") and
[nifm:u](Network%20Interface%20services#nifm:u.md##nifm:u "wikilink").

It calls [CreateRequest
](Network%20Interface%20services#nifm:u.md##nifm:u "wikilink") with
**request\_id** 0x02.

Then calls
[GetSystemEventReadableHandles](Network%20Interface%20services#nifm:u.md##nifm:u "wikilink")
on the returned
[IRequest](Network%20Interface%20services#IRequest.md##IRequest "wikilink")
and creates an event object.

It uses
[GetRequestState](Network%20Interface%20services#nifm:u.md##nifm:u "wikilink")
and
[GetResult](Network%20Interface%20services#nifm:u.md##nifm:u "wikilink")
for synchronizing with the request object, calls
[Submit](Network%20Interface%20services#IRequest.md##IRequest "wikilink")
on the request and waits for it to finish.

After submitting the first request, safemode repeats the request process
again and waits for it to finish. If the request fails to finish at this
point, [RebootSystem](PCV%20services#bpc.md##bpc "wikilink") is called.

It calls
[GetISystemUpdateControl](NS%20Services#ns:su.md##ns:su "wikilink") and
creates a system update event by
    calling:

  - [GetClientId](Network%20Interface%20services#nifm:u.md##nifm:u "wikilink")
    to obtain the current client's
    ID;
  - [IsAnyInternetRequestAccepted](Network%20Interface%20services#nifm:u.md##nifm:u "wikilink")
    with the returned client ID (if no request was accepted, error
    0x2A810 is returned);
  - [ISystemUpdateControl
    cmd2](NS%20Services#ns:su.md##ns:su "wikilink").

After this, an event object is created and safemode loops waiting on it
while calling [ISystemUpdateControl
cmd3](NS%20Services#ns:su.md##ns:su "wikilink") (update event?).

When the system update event is signalled, safemode calls [ns:su
cmd0](NS%20Services#ns:su.md##ns:su "wikilink") (get update status?) and
if this fails, [RebootSystem](PCV%20services#bpc.md##bpc "wikilink") is
called.

Finally, [ISystemUpdateControl
cmd4](NS%20Services#ns:su.md##ns:su "wikilink") is called and the
process exits.

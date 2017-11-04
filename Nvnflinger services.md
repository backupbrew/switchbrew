Nvnflinger is responsible for mediating the communication between
[vi](Display%20services.md "wikilink") and
[nvservices](NV%20services.md "wikilink"). The
[vi](Display%20services.md "wikilink") sysmodule relays display accesses
to nvnflinger which in turn uses
[/dev/nvdisp-ctrl](NV%20services#.2Fdev.2Fnvdisp-ctrl.md##.2Fdev.2Fnvdisp-ctrl "wikilink")
and [/dev/nvdisp-disp0,
/dev/nvdisp-disp1](NV%20services#.2Fdev.2Fnvdisp-disp0.2C%20.2Fdev.2Fnvdisp-disp1.md##.2Fdev.2Fnvdisp-disp0.2C_.2Fdev.2Fnvdisp-disp1 "wikilink")
from [nvservices](NV%20services.md "wikilink").

# dispdrv

This is "nns::hosbinder::IHOSBinderDriver".

| Cmd | Name                                                   |
| --- | ------------------------------------------------------ |
| 0   | [\#TransactParcel](#TransactParcel "wikilink")         |
| 1   | [\#AdjustRefcount](#AdjustRefcount "wikilink")         |
| 2   | [\#GetNativeHandle](#GetNativeHandle "wikilink")       |
| 3   | [\#TransactParcelAuto](#TransactParcelAuto "wikilink") |

This uses Android code.

Command(s) from here are constantly used while displaying gfx.

TransactParcel is used by 1.0.0 official user-processes, while starting
with {unknown version} TransactParcelAuto is used instead.

For IHOSBinderDriver, the below **ID** is loaded from the layer's
[Display\_services\#NativeWindow](Display%20services#NativeWindow.md##NativeWindow "wikilink").

## TransactParcel

Takes a s32 (**ID**), an u32 (**code**), a type-0x5 input buffer
(**parcel\_data**), a type-0x6 output buffer (**parcel\_reply**) and an
input u32 (**flags**). Each word is placed immediately after the
previous word.

Analogous to "onTransact" from "android.os.IServiceManager".

## AdjustRefcount

Takes 3 input s32s: **ID**, **addval**, and **type**. Each word
immediately follows the previous word. No additional output.

| Called by official function          | addval | type |
| ------------------------------------ | ------ | ---- |
| "android::BpBinder::onFirstRef"      | 1      | 1    |
| "android::BpBinder::onLastStrongRef" | \-1    | 1    |
| ?                                    | 1      | 0    |
| ?                                    | \-1    | 0    |

During init, {addval=1, type=0} is used then {addval=1, type=1} is used.

## GetNativeHandle

Takes an input s32 (**ID**) and u32, with the latter immediately
following the previous word. Returns an output event handle.

## TransactParcelAuto

Takes a s32 (**ID**), an u32 (**code**), a type-0x21 input buffer
(**parcel\_data**), a type-0x22 output buffer (**parcel\_reply**) and an
input u32 (**flags**). Each word is placed immediately after the
previous word.

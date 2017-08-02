This process is launched by [NS](NS%20Services.md "wikilink") when
[PM](Process%20Manager%20services.md "wikilink") signals that there is a
crashing process.

Creport takes a string containing a pid formatted in base10 as input,
and generates an error report. This error report can later be sent to
the cloud server by [Eupld services](Eupld%20services.md "wikilink").

\[2.1.0+\]: An additional input argument string is now used. Only the
first byte is used: `inarg_flag = u8 inarg[1][0];`

## Crash dumping

It uses the [svcDebugActiveProcess](SVC.md "wikilink") to start a
debug-session for the pid. It loops
[svcGetDebugEvent](SVC.md "wikilink") to fetch all debug events.

It has a event buffer of 128 u64's that starts with
"CREP\\x01\\x00\\x00\\x00".

It only cares about type `EXCEPTION` and `ATTACH_PROCESS` events.

For `ATTACH_PROCESS` events it saves the title-id of the crashed process
(this is the first u64 of the type-specific data), and a flag whether to
dump stack.

For `EXCEPTION` events, it adds records to the buffer.

Each exception record starts with 2x u64's: exception type, and
exception address.

Then depending on exception type it stores:

  - `UNDEFINED_INSTRUCTION (0)`: Always (u64) 0.
  - `PREFETCH_ABORT (1)`: Always (u64) 0.
  - `DATA_ABORT (2)`: (u64) Fault register.
  - `UNALIGNED_ACCESS (3)`: (u64) Fault register.
  - `UNDEFINED_SYSCALL (8)`: (u64) Syscall id.
  - `? (9)`: Always (u64) 0.

For all exceptions, it then adds more data from
svcGetDebugThreadParam/svcGetDebugThreadContext. "Usually" (when is this
not the case?), this data includes a size u64 for the register dump
region + the values of all general purpose registers+SP and PC, as well
as 0x80 of stack. This reads the flag from `ATTACH_PROCESS` to determine
whether to read 0x10 bytes using svcReadDebugProcessMemory.

All other events (`USER_BREAK`, etc) don't store any extra data except
type and address.

After it has fetched all events, if it didn't encounter `USER_BREAK` it
constructs an error report:

  - Field10 "ErrorCode": (String) Error-code string formatted with
    ["%04d-%04d"](Error%20codes.md "wikilink").
  - Field115 "ProgramId": (String) Title-id snprintf'ed as "%08llx".
  - Field116 "AbortFlag": (Bool) 0.

It does \*not\* add the event buffer to the report(blacklisted) if
title-id is any of the following(swkbd and all
[web-applets](Internet%20Browser.md "wikilink") except offline-applet):

  - 0100000000001008
  - 010000000000100A
  - 010000000000100B
  - 0100000000001010
  - 0100000000001011

\[2.1.0+\]:

  - If the TID is not one of the above, it then checks if the TID
    matches the creport-sysmodule. If so, it's flagged as blacklisted
    like the above.
  - Then, if inarg\_flag(see above) is set to '1', the following
    titleIDs are checked. When set to '1', and the titleID matches one
    of the checked tittleIDs, it will continue as normal. Otherwise,
    it's handled as if it's blacklisted. Hence, end-result is that the
    checked TIDs are handled the same way as past system-versions, while
    non-checked TIDs are
blacklisted.

` if(tid > 0x0100704000B39FFF)`  
` {`  
`     if(tid <= 0x01009b500007BFFF)`  
`     {`  
`         if(tid == 0x0100704000B3A000)`<continue as normal>`;//"Snipperclips" (Game)`  
`         if(tid == 0x01007EF00011E000)`<continue as normal>`;//"The Legend of Zelda: Breath of the Wild"`  
`     }`  
`     else`  
`     {`  
`         if(tid == 0x01009B500007C000)`<continue as normal>`;//"ARMS"`  
`         if(tid == 0x0100D87002EE0000)`<continue as normal>`;//"Snipperclips - Cut it out, together!"`  
`         if(tid == 0x0100F8F0000A2000)`<continue as normal>`;//"Splatoon 2" (EUR)`  
`     }`  
` }`  
` else if(tid <= 0x0100152000021FFF)`  
` {`  
`     if(tid == 0x010000A00218E000)`<continue as normal>`;//"Splatoon 2 Global Testfire"`  
`     if(tid == 0x01000320000CC000)`<continue as normal>`;//"1-2 Switch"`  
` }`  
` else`  
` {`  
`     if(tid == 0x0100152000022000)`<continue as normal>`;//"Mario Kart 8 Deluxe"`  
`     if(tid == 0x01003BC0000A0000)`<continue as normal>`;//"Splatoon 2" (USA)`  
`     if(tid == 0x01003C700009C000)`<continue as normal>`;//"Splatoon 2" (JPN)`  
` }`

This is probably because of privacy concerns (software keyboard +
browser could contain passwords and personal info).

For all other title-ids, it generates a random AES-128 key and CTR using
`csrng`.

It encrypts the entire event buffer with this AES key and CTR. Then it
encrypts the key-iv-pair using RSA-PSS with a hardcoded pubkey and
exponent `0x10001`.

These are added to the error report:

  - Field206 "EncryptionKey": (Raw) RSA-encrypted AES-key.
  - Field207 "EncryptedExceptionInfo": (Raw) Encrypted crash-info.

Thus you need the private key to decrypt the crash dump.

Finally, the error report is sent to "erpt:c" cmd1.

It uses "ns:dev" to terminate the pid, and then it throws the following
fatal-err depending on exception type

  - 0 -\> 0xA8
  - 1 -\> 0x2A8
  - 2 -\> 0x4A8,
  - 3 -\> 0x6A8,
  - 6 -\> No fatal-err
  - 8 -\> 0x10A8
  - Default: 0x4A2

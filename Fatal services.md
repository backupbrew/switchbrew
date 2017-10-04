# fatal:u

| Cmd | Name                                                           |
| --- | -------------------------------------------------------------- |
| 0   |                                                                |
| 1   |                                                                |
| 2   | [\#TransitionToFatalError](#TransitionToFatalError "wikilink") |

## TransitionToFatalError

Takes an input u64 errorcode and an unknown u64(TID maybe?). It also
takes a type-0x15 error buffer and a pid-descriptor. The error buffer
contains a stack trace. The stack trace address count is stored at
errorbuffer+0x240 and the addresses are stored at errorbuffer+0x130+i\*8
where i = 0-\>address count

# fatal:p

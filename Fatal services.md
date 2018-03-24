# fatal:u

This is
"nn::fatalsrv::IService".

| Cmd | Name                                                               |
| --- | ------------------------------------------------------------------ |
| 0   | ThrowFatal                                                         |
| 1   | ThrowFatalWithPolicy                                               |
| 2   | [\#ThrowFatalWithCpuContext](#ThrowFatalWithCpuContext "wikilink") |

## ThrowFatalWithCpuContext

Takes an input u64 errorcode and an unknown u64(TID maybe?). It also
takes a type-0x15 error buffer and a pid-descriptor. The error buffer
contains a stack trace. The stack trace address count is stored at
errorbuffer+0x240 and the addresses are stored at errorbuffer+0x130+i\*8
where i = 0-\>address count

# fatal:p

This is "nn::fatalsrv::IPrivateService".

| Cmd | Name          |
| --- | ------------- |
| 0   | GetFatalEvent |

[Category:Services](Category:Services "wikilink")

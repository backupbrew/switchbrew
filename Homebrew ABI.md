### Entrypoint

Entrypoint is at binary\_ptr+0. At this offset, there is a branch
instruction that jumps past the NRO0 header. This is for (.text) file
format polyglot compatibility with NSO0.

Every application should clean itself up before returning to loader.

This includes tasks like:

  - Not leaking handles
  - Resetting MemoryState
  - No leftover threads running in the background

Original LR given to entrypoint should be returned to, X0 contains an
error code. If original LR is NULL, svcExitProcess should be used.

### Entrypoint Arguments

**NSO0:** the system executes binary\_ptr+0 with X0=NULL,
X1=main\_thread\_handle.

**NRO0:** the homebrew loader puts X0=loader\_config\_ptr,
X1=0xFFFFFFFFFFFFFFFF.

### Loader Config

Loader config allows overriding functionality to workaround limitations
in a limited homebrew environment.

It is an array of tuples:

`struct LoaderConfig {`  
`  LoaderConfigEntry Entries[];`  
`};`

Each entry is key-value pair:

`struct LoaderConfigEntry {`  
`  u32 Key;`  
`  u32 Flags;`  
`  u64 Value[2];`  
`};`

`enum LoaderConfigFlags {`  
`  IsMandatory = BIT(0),`  
`};`

### Loader Config Keys

A loader key can be marked as mandatory or not in its `Flags` field.

If a key is marked as mandatory it means that the application cannot
safely ignore it.

Thus if said key is not recognized by the application, it should exit
with `result_code=346 | ((100 + key) << 9);`, as the default behaviour
may be unsafe.

If a key that is required is not found (for example with an outdated
loader), use `result_code=346 | ((200 + key) << 9);`.

If there is some error encountered while validating an entry's values,
use `result_code = 346 | ((300 + key) << 9);`.

  - 0: [\#EndOfList](#EndOfList "wikilink"): Must be present

<!-- end list -->

  - 1: [\#MainThreadHandle](#MainThreadHandle "wikilink"): Must be
    present

<!-- end list -->

  - 2: [\#NextLoadPath](#NextLoadPath "wikilink")

<!-- end list -->

  - 3: [\#OverrideHeap](#OverrideHeap "wikilink"): If present, must not
    be ignored

<!-- end list -->

  - 4: [\#OverrideService](#OverrideService "wikilink")

<!-- end list -->

  - 5: [\#Argv](#Argv "wikilink")

<!-- end list -->

  - 6: [\#SyscallAvailableHint](#SyscallAvailableHint "wikilink")

<!-- end list -->

  - 7: [\#AppletType](#AppletType "wikilink"): Must be present

<!-- end list -->

  - 8: [\#AppletWorkaround](#AppletWorkaround "wikilink"): If present,
    must not be ignored

<!-- end list -->

  - 9: [\#StdioSockets](#StdioSockets "wikilink")

<!-- end list -->

  - 10: [\#ProcessHandle](#ProcessHandle "wikilink")

<!-- end list -->

  - 11: [\#LastLoadResult](#LastLoadResult "wikilink")

#### EndOfList

EndOfList is the final entry in the LoaderConfig.

  - **Key:** 0
  - **Value\[0\]:** Ignored.
  - **Value\[1\]:** Ignored.

#### MainThreadHandle

This is the handle to the thread that is executing the entrypoint.
Required for mutex to function.

  - **Key:** 1
  - **Value\[0\]:** Handle to the main thread.
  - **Value\[1\]:** Ignored.
  - **DefaultBehavior:** Use main thread handle from entry function
    arguments.

#### NextLoadPath

Homebrew menu uses this pointer to write the path of next NRO to load,
before returning back to Homebrew loader.

  - **Key:** 2
  - **Value\[0\]:** Pointer to buffer of size 512. NRO file path, should
    start with "sdmc:/".
  - **Value\[1\]:** Pointer to buffer of size 2048. Argv string to boot
    NRO with.

#### OverrideHeap

If the NRO loader has reserved some space in the heap for itself, the
application must not manipulate the heap.

  - **Key:** 3
  - **Value\[0\]:** Base address of heap. Must be MemoryType 4, 5, or 9
    with all reference counts being zero.
  - **Value\[1\]:** Size of heap.
  - **DefaultBehavior:** Allocates heap using svcSetHeapSize instead.

#### OverrideService

The NRO loader should be able to steal handles from more priliveged
processes. In this case, the homebrew should use this handle instead of
the normal one.

Homebrew should allow up to 32 service overrides.

Note: Overridden service handles should not be converted to domains or
closed. If they are domain, they should be converted to sessions before
passed to the homebrew application.

Note: For services that authenticate with pid, the app should not
attempt re-authentication with an overridden handle.

Note: There needs be special handling for the file system service. If
the original fsp-srv handle doesn't allow MountSdcard, it shall fallback
to the stolen one, etc etc.

  - **Key:** 4
  - **Value\[0\]:** Name of service, same format as for sm.
  - **Value\[1\]:** Lower 32-bits: Service handle
  - **DefaultBehavior:** Fetches service from "sm:" named port.

#### Argv

The NRO loader should be able to send argv.

  - **Key:** 5
  - **Value\[0\]:** Ignored.
  - **Value\[1\]:** Argv string pointer.
  - **DefaultBehavior:** Setting (argc == 1, argv\[0\] == "", argv\[1\]
    == NULL), or argv parsed in NSO0 fashion.

#### SyscallAvailableHint

Homebrew doesn't know if any privileged syscalls are available.

This entry allows loader to give hints about having access to rare
syscalls (such as JIT).

  - **Key:** 6
  - **Value\[0\]:** 64-bit mask for the 0-0x3F SVC range. n:th bit set
    means SVC is accessible.
  - **Value\[1\]:** 64-bit mask for the 0x40-0x7F SVC range.
  - **DefaultBehavior:** If NSO0, assume kernelhax thus all rare
    syscalls are allowed. If NRO0, assume all rare syscalls are
    inaccessible.

#### AppletType

Specifies the [AM](AM%20services.md "wikilink") AppletType, used for
selecting which Open\*Proxy command to use.

  - **Key:** 7
  - **Value\[0\]:** AppletType
  - **Value\[1\]:** Ignored.

`enum LoaderConfigAppletType {`  
`  LoaderConfigAppletType_Application = 0,`  
`  LoaderConfigAppletType_SystemApplet = 1,`  
`  LoaderConfigAppletType_LibraryApplet = 2,`  
`  LoaderConfigAppletType_OverlayApplet = 3,`  
`  LoaderConfigAppletType_SystemApplication = 4,`  
`};`

#### AppletWorkaround

This flag means that AM services is broken, and must not be used.

  - **Key:** 8
  - **Value\[0\]:** AppletResourceUserId
  - **Value\[1\]:** Ignored.

#### StdioSockets

Use these sockets for standard input/output/error. There must be an
[\#OverrideService](#OverrideService "wikilink") key present for either
`bsd:u` or `bsd:s`, depending on which is indicated.

  - **Key:** 9
  - **Value\[0\]:** First word: stdout file descriptor, second word:
    stdin file descriptor
  - **Value\[1\]:** Third word: stderr file descriptor, fourth word:
    SocketService

`enum LoaderConfigSocketService {`  
`  LoaderConfigSocketService_BsdU = 0,`  
`  LoaderConfigSocketService_BsdS = 1,`  
`};`

#### ProcessHandle

Handle to self process.

  - **Key:** 10
  - **Value\[0\]:** Process handle.
  - **Value\[1\]:** Ignored.

#### LastLoadResult

This is used to feed the last NRO error code back to the Homebrew Menu
so that an error dialog can be displayed.

  - **Key:** 11
  - **Value\[0\]:** Result.
  - **Value\[1\]:** Ignored.

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

When X0 is non-zero and X1 is not 0xFFFFFFFFFFFFFFFF, the application
must handle userland
[exceptions](SVC#Exception%20Handling.md##Exception_Handling "wikilink")
(with the same entrypoint args described there). This must be done
without corrupting registers for this (x8..x29).

The loader should forward exceptions to the mapped NRO by just jumping
to the NRO entrypoint, without the above register corruption. When the
NRO is not mapped the loader can run: `svcReturnFromException(0xf801);
while(1);`

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

  - 9: [\#Reserved9](#Reserved9 "wikilink")

<!-- end list -->

  - 10: [\#ProcessHandle](#ProcessHandle "wikilink")

<!-- end list -->

  - 11: [\#LastLoadResult](#LastLoadResult "wikilink")

<!-- end list -->

  - 12: [\#AllocPages](#AllocPages "wikilink")

<!-- end list -->

  - 13: [\#LockRegion](#LockRegion "wikilink"): If present, must not be
    ignored

<!-- end list -->

  - 14: [\#RandomSeed](#RandomSeed "wikilink")

<!-- end list -->

  - 15: [\#UserIdStorage](#UserIdStorage "wikilink")

<!-- end list -->

  - 16: [\#HosVersion](#HosVersion "wikilink")

#### EndOfList

EndOfList is the final entry in the LoaderConfig. It also provides
optional human readable information about the Homebrew loader.

  - **Key:** 0
  - **Value\[0\]:** Pointer to loader information string, or zero if not
    present.
  - **Value\[1\]:** Size in bytes of the information string, or zero if
    not present.

#### MainThreadHandle

This is the handle to the thread that is executing the entrypoint.
Required for mutex to function.

  - **Key:** 1
  - **Value\[0\]:** Handle to the main thread.
  - **Value\[1\]:** Reserved/should be zero.
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
application must not manipulate the heap. If an
[\#AllocPages](#AllocPages "wikilink") key is present, the region this
points to should be accepted by `free_pages`.

  - **Key:** 3
  - **Value\[0\]:** Base address of heap. Must be MemoryType 4, 5, or 9
    with all reference counts being zero.
  - **Value\[1\]:** Size of heap.
  - **DefaultBehavior:** Allocates heap using svcSetHeapSize instead.

#### OverrideService

The NRO loader should be able to steal handles from more priliveged
processes. In this case, homebrew should use this handle instead of the
normal one.

Homebrew should allow at least 32 service overrides.

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
  - **Value\[0\]:** Reserved/should be zero.
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
  - **Value\[1\]:** AppletFlags

AppletFlags ApplicationOverride: Use AppletType\_Application instead of
AppletType\_SystemApplication, only when AppletType is
SystemApplication. This should only be handled when
AppletType\_Application is properly supported where applet may have been
previously initialized in the context of the current process, for
AppletType\_Application. This avoids breaking backwards-compatibility
with apps which don't support AppletType\_Application as previously
described.

`enum LoaderConfigAppletType {`  
`  LoaderConfigAppletType_Application = 0,`  
`  LoaderConfigAppletType_SystemApplet = 1,`  
`  LoaderConfigAppletType_LibraryApplet = 2,`  
`  LoaderConfigAppletType_OverlayApplet = 3,`  
`  LoaderConfigAppletType_SystemApplication = 4,`  
`};`

`enum LoaderConfigAppletFlags {`  
`  LoaderConfigAppletFlags_ApplicationOverride = BIT(0),`  
`};`

#### AppletWorkaround

This flag means that AM services is broken, and must not be used.

  - **Key:** 8
  - **Value\[0\]:** AppletResourceUserId
  - **Value\[1\]:** Reserved/should be zero.

#### Reserved9

This key has been deleted/reserved for future use.

#### ProcessHandle

Handle to self process.

  - **Key:** 10
  - **Value\[0\]:** Process handle.
  - **Value\[1\]:** Reserved/should be zero.

#### LastLoadResult

This is used to feed the last NRO error code back to the Homebrew Menu
so that an error dialog can be displayed.

  - **Key:** 11
  - **Value\[0\]:** Result.
  - **Value\[1\]:** Reserved/should be zero.

#### AllocPages

This key is used to provide function pointers for a memory allocator. If
an [\#OverrideHeap](#OverrideHeap "wikilink") key is present and this
key is recognized, `free_pages` may be called with the address of the
overridden heap as an argument. There may not be more than one
[\#AllocPages](#AllocPages "wikilink") key.

If this key is recognized, applications should not attempt to use heap
regions without first obtaining them through `alloc_pages`. If
applications should not manage the heap themselves, an
[\#OverrideHeap](#OverrideHeap "wikilink") key should be passed in case
this key is not recognized. If an
[\#OverrideHeap](#OverrideHeap "wikilink") key is not present,
applications may attempt to manage the heap themselves. Any regions of
memory within the heap that would be unsafe for an application to
overwrite (such as the application's own stack) must be specified by a
[\#LockRegion](#LockRegion "wikilink") key.

  -   
    `void *alloc_pages(size_t min, size_t max, size_t *actual)`:

<!-- end list -->

  - 
    
      -   
        This function shall allocate a page-aligned region of memory
        with a page-aligned size between `min` and `max` bytes
        (inclusive). If a failure is encountered, it shall return NULL.
        If `actual` is not NULL, the value it points to shall be
        overwritten with the actual size of the allocated region.
        Regions of memory allocated by this function may be passed to
        `free_pages` to mark them as eligible to be allocated again.

<!-- end list -->

  - 
    
      -   
        Regions of memory returned from this function must be read/write
        type-5 (HEAP) pages with no memory attributes set.

<!-- end list -->

  -   
    `bool free_pages(void *pages)`:

<!-- end list -->

  - 
    
      -   
        This function shall mark a region of memory either previously
        returned by `alloc_pages` or passed by the
        [\#OverrideHeap](#OverrideHeap "wikilink") key as being eligible
        for future allocations. If any failure is encountered, a value
        of `TRUE` shall be returned. Otherwise, a value of `FALSE` is
        returned.

<!-- end list -->

  - **Key**: 12
  - **Value\[0\]:** `void *(*alloc_pages)(size_t min, size_t max, size_t
    *actual)`
  - **Value\[1\]:** `bool (*free_pages)(void *pages)`

#### LockRegion

This key is used to hint to the application that a certain region of the
heap is unsafe to overwrite. There is no limit on the number of
[\#LockRegion](#LockRegion "wikilink") keys that may be passed. If an
application is unable to process the number of regions that are locked,
it must exit before overwriting any heap memory. It is an error for this
key to be present in the same configuration as an
[\#OverrideHeap](#OverrideHeap "wikilink") or
[\#AllocPages](#AllocPages "wikilink") key.

  - **Key**: 13
  - **Value\[0\]:** Pointer to region to lock
  - **Value\[1\]:** Size of region to lock

#### RandomSeed

This key is used to provide an extra entropy source to the application
(in addition to the seed provided by the kernel), allowing it to
generate different pseudo-random numbers every time it's launched from
within the same process.

  - **Key**: 14
  - **Value\[0\]:** Random data.
  - **Value\[1\]:** More random data.

#### UserIdStorage

This key is used to provide persistent storage space for the preselected
user id when launching homebrew under an application that has an account
selection screen.

  - **Key**: 15
  - **Value\[0\]:** Pointer to a buffer containing enough space (16
    bytes) to store a user id.
  - **Value\[1\]:** Reserved/should be zero.

#### HosVersion

This key provides the currently running version of Horizon OS.

  - **Key**: 16
  - **Value\[0\]:** HOS version, formatted using libnx's [MAKEHOSVERSION
    macro](https://github.com/switchbrew/libnx/blob/master/nx/include/switch/runtime/hosversion.h#L11).
  - **Value\[1\]:** Reserved/should be zero.

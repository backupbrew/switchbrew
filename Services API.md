Just like the 3DS/N3DS, the Switch exposes an API which communicates
with certain services. Services are system processes running in the
background which wait for incoming requests. When a process wants to
communicate with a service, it first needs to get a handle to the named
service, and then it can communicate with the service via inter-process
communication (each service has a name up to 8 characters).

Handles for services are retrieved from the service manager port, "sm:".
Services are an abstraction of ports, they operate the same way except
regular ports can have their handles retrieved directly from a SVC.

List of services
(non-exhaustive):

| Service names                      | Description                     | Notes                                 |
| ---------------------------------- | ------------------------------- | ------------------------------------- |
| nvmemp                             | NVIDIA Memory Profiling service |                                       |
| nvdrv:a                            | NVIDIA Graphics Driver service  |                                       |
| acc:u1                             | Account System service          | u1: for user 1?                       |
| appletAE                           | Applet Accessor service         |                                       |
| audren:u                           | Audio Renderer service          |                                       |
| audout:u                           | Audio Out service               |                                       |
| caps:a, caps:ss                    | Capture service                 | a: Album, ss: Screenshot              |
| nim:shp                            | NIM service                     | shp: eShop                            |
| fatal:u                            | Fatal service                   |                                       |
| fsp-srv                            | File System Proxy service       |                                       |
| hid, hid:dbg, hid:sys              | HID service                     |                                       |
| ldn:m                              | Local Network Monitor service   |                                       |
| lm                                 | Log service                     |                                       |
| nifm:u, nifm:a, nifm:s             | Network Interface service       | u: User?, a: Application?, s: Static? |
| ns:am                              | NS service                      | am: Application Manager               |
| nsd:u, nsd:a                       | NSD service                     |                                       |
| pl:u                               | Shared Font Manager service     |                                       |
| prepo:u, prepo:s, prepo:m, prepo:a | Prepo(?) service                |                                       |
| set, set:sys                       | Settings service                | sys: System settings                  |
| bsd:u, bsd:s                       | Sockets service                 |                                       |
| sfdnsres                           | DNS resolver service            |                                       |
| ssl                                | SSL service                     |                                       |
| time:u, time:a, time:s             | Time service                    |                                       |
| vi:m, vi:s, vi:u                   | VI (Camera?) service            |                                       |
| erpt:c                             | ERPT(?) service                 |                                       |
| ldr:ro                             | RO service                      |                                       |
| mm:u                               | NvMM service                    |                                       |

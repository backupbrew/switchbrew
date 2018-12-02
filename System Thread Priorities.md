This is a list of threads executing on the system during normal
operation.

# Production devices

| Thread Priority | Thread Name                             | Owner Process | Notes                                                                |
| --------------- | --------------------------------------- | ------------- | -------------------------------------------------------------------- |
| 16              | nn.usb.MainThread                       | usb           |                                                                      |
| 16              | nn.usb.DsIpcServer                      | usb           | usb spawns four copies of this thread to handle usb:ds IPC requests. |
| 16              | nn.usb.DsProtocol                       | usb           |                                                                      |
| 16              | nn.usb.DsThread                         | usb           |                                                                      |
| 16              | nn.usb.HsIpcServer                      | usb           | usb spawns two copies of this thread to handle hs IPC requests.      |
| 16              | nn.usb.HsThread                         | usb           |                                                                      |
| 16              | nn.usb.InterruptHandler                 | usb           |                                                                      |
| 16              | nn.usb.PmIpcServer                      | usb           |                                                                      |
| 27              | nn.boot.Main                            | boot          | This is the real name for nn.boot.MainThread.                        |
| 27              | nn.spl.MainThread                       | spl           |                                                                      |
| 27              | nn.sm.MainThread                        | sm            |                                                                      |
| 30              | nn.pcie.Main                            | pcie          | This is the real name for nn.pcie.MainThread.                        |
| 30              | nn.pcie.InterruptHandler                | pcie          |                                                                      |
| 37              | nn.psc.Main                             | psc           | This is the real name for nn.psc.MainThread.                         |
| 37              | nn.psc.IpcServer                        | psc           |                                                                      |
| 37              | nn.psc.PmControl                        | psc           |                                                                      |
| 37              | nn.srepo.IpcServer                      | psc           |                                                                      |
| 37              | nn.usb.PdAlert                          | usb           |                                                                      |
| 37              | nn.usb.PdExecute                        | usb           |                                                                      |
| 37              | nn.usb.PdReceiveVdm                     | usb           |                                                                      |
| 37              | nn.usb.PdServer                         | usb           |                                                                      |
| 37              | nn.usb.InputNotifier                    | usb           |                                                                      |
| 38              | nn.usb.PdCradleServer                   | usb           |                                                                      |
| 39              | nn.gc.DeviceDetector                    | fs            |                                                                      |
| 39              | nn.sdmmc.DeviceDetector                 | fs            |                                                                      |
| 44              | nn.fs.WorkerThreadPool                  | fs            |                                                                      |
| 45              | nn.fs.MainThread                        | fs            |                                                                      |
| 46              | nn.fs.WorkerNormalPriorityAccess        | fs            | fs spawns five copies of this thread to handle fsp-srv IPC requests  |
| 48              | nn.boot2.MainThread                     | boot2         |                                                                      |
| 49              | nn.ncm.MainWaitThreads                  | ncm           | This is the real name for nn.ncm.MainThread.                         |
| 49              | nn.ncm.ContentManagerServerIpcSession   | ncm           |                                                                      |
| 49              | nn.ncm.LocationResolverServerIpcSession | ncm           |                                                                      |
| 49              | nn.Loader.MainThread                    | Loader        |                                                                      |
| 49              | nn.pm.MainThread                        | pm            |                                                                      |
| 49              | nn.pm.ProcessTrack                      | pm            |                                                                      |
| 49              | nn.settings.Main                        | settings      | This is the real name for nn.settings.MainThread.                    |
| 49              | nn.settings.IpcServer                   | settings      |                                                                      |
| 49              | nn.settings.LazyWriter                  | settings      |                                                                      |
| 58              | nn.fs.PatrolReader                      | fs            |                                                                      |

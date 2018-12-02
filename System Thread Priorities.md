This is a list of threads executing on the system during normal
operation.

# Production devices

| Thread Priority | Thread Name                             | Owner Process | Notes                                             |
| --------------- | --------------------------------------- | ------------- | ------------------------------------------------- |
| 27              | nn.boot.Main                            | boot          | This is the real name for nn.boot.MainThread.     |
| 27              | nn.spl.MainThread                       | spl           |                                                   |
| 27              | nn.sm.MainThread                        | sm            |                                                   |
| 39              | nn.gc.DeviceDetector                    | fs            |                                                   |
| 39              | nn.sdmmc.DeviceDetector                 | fs            |                                                   |
| 44              | nn.fs.WorkerThreadPool                  | fs            |                                                   |
| 45              | nn.fs.MainThread                        | fs            |                                                   |
| 46              | nn.fs.WorkerNormalPriorityAccess0       | fs            |                                                   |
| 46              | nn.fs.WorkerNormalPriorityAccess1       | fs            |                                                   |
| 46              | nn.fs.WorkerNormalPriorityAccess2       | fs            |                                                   |
| 46              | nn.fs.WorkerNormalPriorityAccess3       | fs            |                                                   |
| 46              | nn.fs.WorkerNormalPriorityAccess4       | fs            |                                                   |
| 47              | nn.psc.Main                             | psc           | This is the real name for nn.psc.MainThread.      |
| 47              | nn.psc.IpcServer                        | psc           |                                                   |
| 47              | nn.psc.PmControl                        | psc           |                                                   |
| 47              | nn.srepo.IpcServer                      | psc           |                                                   |
| 48              | nn.boot2.MainThread                     | boot2         |                                                   |
| 49              | nn.ncm.MainWaitThreads                  | ncm           | This is the real name for nn.ncm.MainThread.      |
| 49              | nn.ncm.ContentManagerServerIpcSession   | ncm           |                                                   |
| 49              | nn.ncm.LocationResolverServerIpcSession | ncm           |                                                   |
| 49              | nn.Loader.MainThread                    | Loader        |                                                   |
| 49              | nn.pm.MainThread                        | pm            |                                                   |
| 49              | nn.pm.ProcessTrack                      | pm            |                                                   |
| 49              | nn.settings.Main                        | settings      | This is the real name for nn.settings.MainThread. |
| 49              | nn.settings.IpcServer                   | settings      |                                                   |
| 49              | nn.settings.LazyWriter                  | settings      |                                                   |
| 58              | nn.fs.PatrolReader                      | fs            |                                                   |

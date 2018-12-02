This is a list of threads executing on the system during normal
operation.

# Production devices

| Thread Priority | Thread Name                             | Owner Process | Notes                                         |
| --------------- | --------------------------------------- | ------------- | --------------------------------------------- |
| 11              | nn.gc.DeviceDetector                    | fs            |                                               |
| 11              | nn.sdmmc.DeviceDetector                 | fs            |                                               |
| 16              | nn.fs.WorkerThreadPool                  | fs            |                                               |
| 17              | nn.fs.MainThread                        | fs            |                                               |
| 18              | nn.fs.WorkerNormalPriorityAccess0       | fs            |                                               |
| 18              | nn.fs.WorkerNormalPriorityAccess1       | fs            |                                               |
| 18              | nn.fs.WorkerNormalPriorityAccess2       | fs            |                                               |
| 18              | nn.fs.WorkerNormalPriorityAccess3       | fs            |                                               |
| 18              | nn.fs.WorkerNormalPriorityAccess4       | fs            |                                               |
| 21              | nn.ncm.MainWaitThreads                  | ncm           | This is the real name for nn.ncm.MainThread.  |
| 21              | nn.ncm.ContentManagerServerIpcSession   | ncm           |                                               |
| 21              | nn.ncm.LocationResolverServerIpcSession | ncm           |                                               |
| 21              | nn.Loader.MainThread                    | Loader        |                                               |
| 21              | nn.pm.MainThread                        | pm            |                                               |
| 21              | nn.pm.ProcessTrack                      | pm            |                                               |
| 27              | nn.boot.Main                            | boot          | This is the real name for nn.boot.MainThread. |
| 27              | nn.spl.MainThread                       | spl           |                                               |
| 27              | nn.sm.MainThread                        | sm            |                                               |
| 30              | nn.fs.PatrolReader                      | fs            |                                               |
|                 |                                         |               |                                               |

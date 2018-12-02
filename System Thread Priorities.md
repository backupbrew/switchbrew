This is a list of threads executing on the system during normal
operation.

# Production devices

| Thread Priority | Thread Name                       | Owner Process | Notes |
| --------------- | --------------------------------- | ------------- | ----- |
| 27              | nn.boot.MainThread                | boot          |       |
| 39              | nn.gc.DeviceDetector              | FS            |       |
| 39              | nn.sdmmc.DeviceDetector           | FS            |       |
| 44              | nn.fs.WorkerThreadPool            | FS            |       |
| 45              | nn.fs.MainThread                  | FS            |       |
| 46              | nn.fs.WorkerNormalPriorityAccess0 | FS            |       |
| 46              | nn.fs.WorkerNormalPriorityAccess1 | FS            |       |
| 46              | nn.fs.WorkerNormalPriorityAccess2 | FS            |       |
| 46              | nn.fs.WorkerNormalPriorityAccess3 | FS            |       |
| 46              | nn.fs.WorkerNormalPriorityAccess4 | FS            |       |
| 58              | nn.fs.PatrolReader                | FS            |       |
|                 |                                   |               |       |

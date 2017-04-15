The Switch makes use of a customized NVIDIA driver.

# nvdrv:a

| Cmd | Name                       |
| --- | -------------------------- |
| 0   | Open                       |
| 1   | Ioctl                      |
| 2   | Close                      |
| 3   | Initialize                 |
| 4   | QueryEvent                 |
| 5   | MapSharedMem               |
| 6   |                            |
| 7   |                            |
| 8   | Audio render related init? |
| 9   | ?                          |

## Ioctls

The ioctl number is generated with the following primitive (see Linux
kernel):

`#define _IOC(inout, group, num, len) \`  
`   (inout | ((len & IOCPARM_MASK) << 16) | ((group) << 8) | (num))`

The following table contains known
ioctls.

| Device               | Value      | Description                                   | Notes                              |
| -------------------- | ---------- | --------------------------------------------- | ---------------------------------- |
| /dev/nvhost-\*       | 0xC0??0001 | NVHOST32\_IOCTL\_CHANNEL\_SUBMIT              | ?? == size is unknown              |
| /dev/nvhost-\*       | 0xC0080002 | NVHOST\_IOCTL\_CHANNEL\_GET\_SYNCPOINT        |                                    |
| /dev/nvhost-\*       | 0xC0080003 | NVHOST\_IOCTL\_CHANNEL\_GET\_WAITBASE         |                                    |
| /dev/nvhost-\*       | 0xC0080004 | NVHOST\_IOCTL\_CHANNEL\_SET\_TIMEOUT\_EX      |                                    |
| /dev/nvhost-\*       | 0xC01C0009 | NVHOST\_IOCTL\_CHANNEL\_SUBMIT(?)             |                                    |
| /dev/nvhost-\*       | 0xC01C000A | NVHOST\_IOCTL\_CHANNEL\_MODULE\_REGRDWR(?)    |                                    |
| /dev/nvhost-\*       | 0xC0080014 | NVHOST\_IOCTL\_CTRL\_SYNCPT\_READ             |                                    |
| /dev/nvhost-\*       | 0x40040015 | NVHOST\_IOCTL\_CTRL\_SYNCPT\_INCR             |                                    |
| /dev/nvhost-\*       | 0xC00C0016 | NVHOST\_IOCTL\_CTRL\_SYNCPT\_WAIT             |                                    |
| /dev/nvhost-\*       | 0x40080017 | NVHOST\_IOCTL\_CTRL\_MODULE\_MUTEX            |                                    |
| /dev/nvhost-\*       | 0xC0180018 | NVHOST32\_IOCTL\_CTRL\_MODULE\_REGRDWR        |                                    |
| /dev/nvhost-\*       | 0xC0100019 | NVHOST\_IOCTL\_CTRL\_SYNCPT\_WAITEX           |                                    |
| /dev/nvhost-\*       | 0xC008001A | NVHOST\_IOCTL\_CTRL\_SYNCPT\_READ\_MAX        |                                    |
| /dev/nvhost-\*       | 0xC004001C | NVHOST\_IOCTL\_CTRL\_GET\_VERSION(?)          |                                    |
| /dev/nvhost-\*       | 0xC010001D |                                               | NvRmSyncWaitEvent (wait on event?) |
| /dev/nvhost-\*       | 0xC010001E |                                               | NvRmSyncWaitEvent (wait on event?) |
| /dev/nvhost-\*       | 0xC004001F |                                               | NvRmSyncWaitEvent (signal event?)  |
| /dev/nvhost-\*       | 0xC0040020 |                                               | NvRmSyncWaitEvent (signal event?)  |
| /dev/nvhost-\*       | 0x40080021 |                                               | Returns busy?                      |
| /dev/nvmap           | 0xC0080101 | NVMAP\_IOC\_CREATE                            |                                    |
| /dev/nvmap           | 0xC0080103 | NVMAP\_IOC\_FROM\_ID                          |                                    |
| /dev/nvmap           | 0xC0200104 | NVMAP\_IOC\_ALLOC                             |                                    |
| /dev/nvmap           | 0xC0180105 | NVMAP\_IOC\_FREE                              |                                    |
| /dev/nvmap           | 0xC00C0109 | NVMAP\_IOC\_PARAM                             |                                    |
| /dev/nvmap           | 0xC008010E | NVMAP\_IOC\_GET\_ID                           |                                    |
| /dev/nvhost-as-gpu   | 0x40044101 | NVGPU\_AS\_IOCTL\_BIND\_CHANNEL               |                                    |
| /dev/nvhost-as-gpu   | 0xC0184102 | NVGPU32\_AS\_IOCTL\_ALLOC\_SPACE              |                                    |
| /dev/nvhost-as-gpu   | 0xC0104103 | NVGPU\_AS\_IOCTL\_FREE\_SPACE                 |                                    |
| /dev/nvhost-as-gpu   | 0xC0184104 | NVGPU\_AS\_IOCTL\_MAP\_BUFFER                 |                                    |
| /dev/nvhost-as-gpu   | 0xC0084105 | NVGPU\_AS\_IOCTL\_UNMAP\_BUFFER               |                                    |
| /dev/nvhost-as-gpu   | 0xC0284106 | NVGPU\_AS\_IOCTL\_ALLOC\_SPACE                |                                    |
| /dev/nvhost-as-gpu   | 0x40104107 |                                               |                                    |
| /dev/nvhost-as-gpu   | 0xC0404108 |                                               |                                    |
| /dev/nvhost-as-gpu   | 0x40284109 |                                               |                                    |
| /dev/nvhost-as-gpu   | 0xC0144114 |                                               |                                    |
| /dev/nvhost-dbg-gpu  | 0xC0??4402 | NVGPU\_DBG\_GPU\_IOCTL\_REG\_OPS              | ?? == size is unknown              |
| /dev/nvhost-ctrl-gpu | 0x80044701 | NVGPU\_GPU\_IOCTL\_ZCULL\_GET\_CTX\_SIZE      |                                    |
| /dev/nvhost-ctrl-gpu | 0x80284702 | NVGPU\_GPU\_IOCTL\_ZCULL\_GET\_INFO           |                                    |
| /dev/nvhost-ctrl-gpu | 0x402C4703 | NVGPU\_GPU\_IOCTL\_ZBC\_SET\_TABLE            |                                    |
| /dev/nvhost-ctrl-gpu | 0xC0344704 | NVGPU\_GPU\_IOCTL\_ZBC\_QUERY\_TABLE          |                                    |
| /dev/nvhost-ctrl-gpu | 0xC0B04705 | NVGPU\_GPU\_IOCTL\_GET\_CHARACTERISTICS       |                                    |
| /dev/nvhost-ctrl-gpu | 0xC0184706 | NVGPU\_AS\_IOCTL\_ALLOC\_SPACE                |                                    |
| /dev/nvhost-ctrl-gpu | 0x40084707 |                                               |                                    |
| /dev/nvhost-ctrl-gpu | 0x4008470E |                                               |                                    |
| /dev/nvhost-ctrl-gpu | 0x4010470F |                                               |                                    |
| /dev/nvhost-ctrl-gpu | 0xC0084710 |                                               |                                    |
| /dev/nvhost-ctrl-gpu | 0x80084711 |                                               |                                    |
| /dev/nvhost-ctrl-gpu | 0x80084714 |                                               |                                    |
| /dev/nvhost-ctrl-gpu | 0xC008471B |                                               |                                    |
| /dev/nvhost-ctrl-gpu | 0xC010471C |                                               |                                    |
| /dev/nvhost-\*       | 0x40044801 | NVGPU\_IOCTL\_CHANNEL\_SET\_NVMAP\_FD         |                                    |
| /dev/nvhost-\*       | 0x40044803 | NVGPU\_IOCTL\_CHANNEL\_SET\_TIMEOUT(?)        |                                    |
| /dev/nvhost-\*       | 0x40084805 | NVGPU\_IOCTL\_CHANNEL\_SET\_TIMEOUT\_EX(?)    |                                    |
| /dev/nvhost-\*       | 0xC0044807 | NVGPU\_IOCTL\_CHANNEL\_CYCLE\_STATS           |                                    |
| /dev/nvhost-\*       | 0xC0184808 | NVGPU\_IOCTL\_CHANNEL\_SUBMIT\_GPFIFO         |                                    |
| /dev/nvhost-\*       | 0xC0104809 | NVGPU\_IOCTL\_CHANNEL\_ALLOC\_OBJ\_CTX        |                                    |
| /dev/nvhost-\*       | 0x4008480A | NVGPU\_IOCTL\_CHANNEL\_FREE\_OBJ\_CTX         |                                    |
| /dev/nvhost-\*       | 0xC010480B | NVGPU\_IOCTL\_CHANNEL\_ZCULL\_BIND            |                                    |
| /dev/nvhost-\*       | 0xC018480C | NVGPU\_IOCTL\_CHANNEL\_SET\_ERROR\_NOTIFIER   |                                    |
| /dev/nvhost-\*       | 0x4004480D | NVGPU\_IOCTL\_CHANNEL\_OPEN                   |                                    |
| /dev/nvhost-\*       | 0x0000480E | NVGPU\_IOCTL\_CHANNEL\_ENABLE                 |                                    |
| /dev/nvhost-\*       | 0x0000480F | NVGPU\_IOCTL\_CHANNEL\_DISABLE                |                                    |
| /dev/nvhost-\*       | 0x00004810 | NVGPU\_IOCTL\_CHANNEL\_PREEMPT                |                                    |
| /dev/nvhost-\*       | 0x00004811 | NVGPU\_IOCTL\_CHANNEL\_FORCE\_RESET           |                                    |
| /dev/nvhost-\*       | 0x40084812 | NVGPU\_IOCTL\_CHANNEL\_EVENTS\_CTRL           |                                    |
| /dev/nvhost-\*       | 0xC0104813 | NVGPU\_IOCTL\_CHANNEL\_CYCLE\_STATS\_SNAPSHOT |                                    |
| /dev/nvhost-\*       | 0x80804816 |                                               |                                    |
| /dev/nvhost-\*       | 0xC0104817 |                                               |                                    |
| /dev/nvhost-\*       | 0x40204818 |                                               |                                    |
| /dev/nvhost-\*       | 0xC0184819 |                                               |                                    |
| /dev/nvhost-\*       | 0xC020481A |                                               |                                    |

The Switch makes use of a customized NVIDIA driver that is exposed
through multiple services. Communication with these services goes
through IPC, as usual.

# nvdrv:a

| Cmd | Name                                       | Format |
| --- | ------------------------------------------ | ------ |
| ??? | NvOsDrvOpen                                |        |
| ??? | NvOsDrvClose                               |        |
| ??? | [\#NvOsDrvIoctl](#NvOsDrvIoctl "wikilink") |        |
| ??? | NvOsDrvMapSharedMem                        |        |
| ??? | NvOsDrvQueryEvent                          |        |
|     |                                            |        |

## NvOsDrvIoctl

Just like any standard build of the NVIDIA graphics' drivers, the
nvdrv:a service operates mainly by processing requests and sending them
to the kernel (not verified) through IOCtl commands. Note that these
commands are generated with the following primitive (see Linux
kernel):

`#define _IOC(inout, group, num, len) (inout | ((len & IOCPARM_MASK) << 16) | ((group) << 8) | (num))`

The following table contains valid commands for group 0x00. This group
consists in commands for the "/dev/nvhost-ctrl" interface and a few
global commands for every nvhost channel (e.g.:
"/dev/nvhost-gpu").

| Value      | Description                                | Notes                              |
| ---------- | ------------------------------------------ | ---------------------------------- |
| 0xC0??0001 | NVHOST32\_IOCTL\_CHANNEL\_SUBMIT           | ?? == size is unknown              |
| 0xC0080002 | NVHOST\_IOCTL\_CHANNEL\_GET\_SYNCPOINT     |                                    |
| 0xC0080003 | NVHOST\_IOCTL\_CHANNEL\_GET\_WAITBASE      |                                    |
| 0xC0080004 | NVHOST\_IOCTL\_CHANNEL\_SET\_TIMEOUT\_EX   |                                    |
| 0xC01C0009 | NVHOST\_IOCTL\_CHANNEL\_SUBMIT(?)          |                                    |
| 0xC01C000A | NVHOST\_IOCTL\_CHANNEL\_MODULE\_REGRDWR(?) |                                    |
| 0xC0080014 | NVHOST\_IOCTL\_CTRL\_SYNCPT\_READ          |                                    |
| 0x40040015 | NVHOST\_IOCTL\_CTRL\_SYNCPT\_INCR          |                                    |
| 0xC00C0016 | NVHOST\_IOCTL\_CTRL\_SYNCPT\_WAIT          |                                    |
| 0x40080017 | NVHOST\_IOCTL\_CTRL\_MODULE\_MUTEX         |                                    |
| 0xC0180018 | NVHOST32\_IOCTL\_CTRL\_MODULE\_REGRDWR     |                                    |
| 0xC0100019 | NVHOST\_IOCTL\_CTRL\_SYNCPT\_WAITEX        |                                    |
| 0xC008001A | NVHOST\_IOCTL\_CTRL\_SYNCPT\_READ\_MAX     |                                    |
| 0xC004001C | NVHOST\_IOCTL\_CTRL\_GET\_VERSION(?)       |                                    |
| 0xC010001D | Unknown                                    | NvRmSyncWaitEvent (wait on event?  |
| 0xC010001E | Unknown                                    | NvRmSyncWaitEvent (wait on event?) |
| 0xC004001F | Unknown                                    | NvRmSyncWaitEvent (signal event?)  |
| 0xC0040020 | Unknown                                    | NvRmSyncWaitEvent (signal event?)  |
| 0x40080021 | Unknown                                    | Returns busy?                      |
|            |                                            |                                    |

The following table contains valid commands for group 0x01. This group
consists in commands for the "/dev/nvmap" interface.

| Value      | Description          | Notes |
| ---------- | -------------------- | ----- |
| 0xC0080101 | NVMAP\_IOC\_CREATE   |       |
| 0xC0080103 | NVMAP\_IOC\_FROM\_ID |       |
| 0xC0200104 | NVMAP\_IOC\_ALLOC    |       |
| 0xC0180105 | NVMAP\_IOC\_FREE     |       |
| 0xC00C0109 | NVMAP\_IOC\_PARAM    |       |
| 0xC008010E | NVMAP\_IOC\_GET\_ID  |       |
|            |                      |       |

The following table contains valid commands for group 0x41 ('A'). This
group consists in commands for the "/dev/nvhost-as-gpu" interface.

| Value      | Description                      | Notes |
| ---------- | -------------------------------- | ----- |
| 0x40044101 | NVGPU\_AS\_IOCTL\_BIND\_CHANNEL  |       |
| 0xC0184102 | NVGPU32\_AS\_IOCTL\_ALLOC\_SPACE |       |
| 0xC0104103 | NVGPU\_AS\_IOCTL\_FREE\_SPACE    |       |
| 0xC0184104 | NVGPU\_AS\_IOCTL\_MAP\_BUFFER    |       |
| 0xC0084105 | NVGPU\_AS\_IOCTL\_UNMAP\_BUFFER  |       |
| 0xC0284106 | NVGPU\_AS\_IOCTL\_ALLOC\_SPACE   |       |
| 0x40104107 | Unknown                          |       |
| 0xC0404108 | Unknown                          |       |
| 0x40284109 | Unknown                          |       |
| 0xC0144114 | Unknown                          |       |
|            |                                  |       |

The following table contains valid commands for group 0x44 ('D'). This
group consists in commands for the "/dev/nvhost-dbg-gpu"
interface.

| Value      | Description                      | Notes                 |
| ---------- | -------------------------------- | --------------------- |
| 0xC0??4402 | NVGPU\_DBG\_GPU\_IOCTL\_REG\_OPS | ?? == size is unknown |
|            |                                  |                       |

The following table contains valid commands for group 0x47 ('G'). This
group consists in commands for the "/dev/nvhost-ctrl-gpu" interface.

| Value      | Description                              | Notes |
| ---------- | ---------------------------------------- | ----- |
| 0x80044701 | NVGPU\_GPU\_IOCTL\_ZCULL\_GET\_CTX\_SIZE |       |
| 0x80284702 | NVGPU\_GPU\_IOCTL\_ZCULL\_GET\_INFO      |       |
| 0x402C4703 | NVGPU\_GPU\_IOCTL\_ZBC\_SET\_TABLE       |       |
| 0xC0344704 | NVGPU\_GPU\_IOCTL\_ZBC\_QUERY\_TABLE     |       |
| 0xC0B04705 | NVGPU\_GPU\_IOCTL\_GET\_CHARACTERISTICS  |       |
| 0xC0184706 | NVGPU\_AS\_IOCTL\_ALLOC\_SPACE           |       |
| 0x40084707 | Unknown                                  |       |
| 0x4008470E | Unknown                                  |       |
| 0x4010470F | Unknown                                  |       |
| 0xC0084710 | Unknown                                  |       |
| 0x80084711 | Unknown                                  |       |
| 0x80084714 | Unknown                                  |       |
| 0xC008471B | Unknown                                  |       |
| 0xC010471C | Unknown                                  |       |
|            |                                          |       |

The following table contains valid commands for group 0x48 ('H'). This
group consists in commands common to all nvhost channels (depending if
they implement them or not), but they are only listed here in relation
to the interface "/dev/nvhost-gpu" for convenience.

| Value      | Description                                   | Notes |
| ---------- | --------------------------------------------- | ----- |
| 0x40044801 | NVGPU\_IOCTL\_CHANNEL\_SET\_NVMAP\_FD         |       |
| 0x40044803 | NVGPU\_IOCTL\_CHANNEL\_SET\_TIMEOUT(?)        |       |
| 0x40084805 | NVGPU\_IOCTL\_CHANNEL\_SET\_TIMEOUT\_EX(?)    |       |
| 0xC0044807 | NVGPU\_IOCTL\_CHANNEL\_CYCLE\_STATS           |       |
| 0xC0184808 | NVGPU\_IOCTL\_CHANNEL\_SUBMIT\_GPFIFO         |       |
| 0xC0104809 | NVGPU\_IOCTL\_CHANNEL\_ALLOC\_OBJ\_CTX        |       |
| 0x4008480A | NVGPU\_IOCTL\_CHANNEL\_FREE\_OBJ\_CTX         |       |
| 0xC010480B | NVGPU\_IOCTL\_CHANNEL\_ZCULL\_BIND            |       |
| 0xC018480C | NVGPU\_IOCTL\_CHANNEL\_SET\_ERROR\_NOTIFIER   |       |
| 0x4004480D | NVGPU\_IOCTL\_CHANNEL\_OPEN                   |       |
| 0x0000480E | NVGPU\_IOCTL\_CHANNEL\_ENABLE                 |       |
| 0x0000480F | NVGPU\_IOCTL\_CHANNEL\_DISABLE                |       |
| 0x00004810 | NVGPU\_IOCTL\_CHANNEL\_PREEMPT                |       |
| 0x00004811 | NVGPU\_IOCTL\_CHANNEL\_FORCE\_RESET           |       |
| 0x40084812 | NVGPU\_IOCTL\_CHANNEL\_EVENTS\_CTRL           |       |
| 0xC0104813 | NVGPU\_IOCTL\_CHANNEL\_CYCLE\_STATS\_SNAPSHOT |       |
| 0x80804816 | Unknown                                       |       |
| 0xC0104817 | Unknown                                       |       |
| 0x40204818 | Unknown                                       |       |
| 0xC0184819 | Unknown                                       |       |
| 0xC020481A | Unknown                                       |       |
|            |                                               |       |

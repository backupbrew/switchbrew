Subchannels:

| Id     | Subchannel (nvn) | Name             |
| ------ | ---------------- | ---------------- |
| 0xB197 | 0                | 3D               |
| 0xB1C0 | 1                | Compute          |
| 0xA140 | 2                | Inline-to-Memory |
| 0x902D | 3                | 2D               |
| 0xB0B5 | 4                | DMA              |

# DMA

| Register | Name         | Notes             |
| -------- | ------------ | ----------------- |
| 0x0C0    | DmaControl   | Seen 0x186.       |
| 0x100    | DmaSrcAddrHi |                   |
| 0x101    | DmaSrcAddrLo |                   |
| 0x102    | DmaDstAddrHi |                   |
| 0x103    | DmaDstAddrLo |                   |
| 0x106    | DmaLength    | At most 0x3FFFFF. |

Subchannels:

| Id     | Subchannel (nvn) | Name             |
| ------ | ---------------- | ---------------- |
| 0xB197 | 0                | 3D               |
| 0xB1C0 | 1                | Compute          |
| 0xA140 | 2                | Inline-to-Memory |
| 0x902D | 3                | 2D               |
| 0xB0B5 | 4                | DMA              |

# 3D

| Register   | Name                           | Notes                                                                                            |
| ---------- | ------------------------------ | ------------------------------------------------------------------------------------------------ |
| 0xC9       | Tesselation\_OuterLevel0       |                                                                                                  |
| 0xCA       | Tesselation\_OuterLevel1       |                                                                                                  |
| 0xCB       | Tesselation\_OuterLevel2       |                                                                                                  |
| 0xCC       | Tesselation\_OuterLevel3       |                                                                                                  |
| 0xCD       | Tesselation\_InnerLevel0       |                                                                                                  |
| 0xCE       | Tesselation\_InnerLevel1       |                                                                                                  |
| 0xDF       | RasterizerDiscard\_Enable      | 1 means enabled, 0 means disabled.                                                               |
| 0x1D1      | TransformFeedback\_Pause       |                                                                                                  |
| 0x1FA      | ZCullCtx\_Addr0Hi              |                                                                                                  |
| 0x1FB      | ZCullCtx\_Addr0Lo              |                                                                                                  |
| 0x1FC      | ZCullCtx\_Addr1Hi              |                                                                                                  |
| 0x1FD      | ZCullCtx\_Addr1Lo              |                                                                                                  |
| 0x285+8\*N | DepthRange\_Unk0\_N            |                                                                                                  |
| 0x302+4\*N | DepthRange\_Unk1\_N            |                                                                                                  |
| 0x303+4\*N | DepthRange\_Unk2\_N            |                                                                                                  |
| 0x373      | PatchSize                      | Small value, always fits in 12 bits.                                                             |
| 0x381+4\*N | Scissor0\_N                    |                                                                                                  |
| 0x382+4\*N | Scissor1\_N                    |                                                                                                  |
| 0x3D5      | StencilMask1\_Ref              | 1 means enabled, 0 means disabled.                                                               |
| 0x3D6      | StencilMask1\_Enable           | 1 means enabled, 0 means disabled.                                                               |
| 0x3D7      | StencilMask1\_ValueMask        | 1 means enabled, 0 means disabled.                                                               |
| 0x3E7      | DepthBounds\_Bound0            | Float is written here.                                                                           |
| 0x3E8      | DepthBounds\_Bound1            | Float is written here.                                                                           |
| 0x3EF      | SampleMask0                    |                                                                                                  |
| 0x3F0      | SampleMask1                    |                                                                                                  |
| 0x3F1      | SampleMask2                    |                                                                                                  |
| 0x3F2      | SampleMask3                    |                                                                                                  |
| 0x452      | Raster\_Enable                 | 1 means enabled, 0 means disabled.                                                               |
| 0x4E5      | StencilMask0\_Ref              | 1 means enabled, 0 means disabled.                                                               |
| 0x4E6      | StencilMask0\_ValueMask        | 1 means enabled, 0 means disabled.                                                               |
| 0x4E7      | StencilMask0\_Enable           | 1 means enabled, 0 means disabled.                                                               |
| 0x4EC      | LineWidth0                     |                                                                                                  |
| 0x4ED      | LineWidth1                     |                                                                                                  |
| 0x4C4      | AlphaRef                       | Float is written here.                                                                           |
| 0x4C7      | BlendColor0                    |                                                                                                  |
| 0x4C8      | BlendColor1                    |                                                                                                  |
| 0x4C9      | BlendColor2                    |                                                                                                  |
| 0x4CA      | BlendColor3                    |                                                                                                  |
| 0x47F      | DepthBuffer\_Resolve           | 1 is written here to trigger.                                                                    |
| 0x519      | ZCullCtx\_Save                 | 0 is written here to trigger ctx-save, uses both ZCullCtx\_Addr0/1.                              |
| 0x51F      | PolygonOffsetClamp0            | Float is written here.                                                                           |
| 0x540      | ZCullCtx\_Restore              | 0 is written here to trigger ctx-restore, uses both ZCullCtx\_Addr0/1.                           |
| 0x546      | PointSize                      | Float is written here.                                                                           |
| 0x554      | RendererEnableConditionAddrHi  |                                                                                                  |
| 0x555      | RendererEnableConditionAddrLo  |                                                                                                  |
| 0x556      | RendererEnable                 | 0=disabled unconditional, 1=enabled unconditional, 3=unknown conditional, 4=unknown conditional, |
| 0x54C      | Counter\_Reset                 | Value written decides which counter to reset.                                                    |
| 0x55B      | PolygonOffsetClamp1            | Float is written here.                                                                           |
| 0x56F      | PolygonOffsetClamp2            | Float multiplied by 2 is written here.                                                           |
| 0x591      | PrimitiveRestart\_Enable       | 1 means enabled, 0 means disabled.                                                               |
| 0x592      | PrimitiveRestart\_Value        |                                                                                                  |
| 0x64F      | DepthClamp                     | 0x101A is written when enabled, 0x181D when disabled.                                            |
| 0x66F      | DepthBounds\_Enable            | 1 means enabled, 0 means disabled.                                                               |
| 0x68B      | Barrier?                       | Always 0 is written here. During zcull ctx-save, spammed when enabling raster, ...               |
| 0x6C0      | Poke\_AddrHi                   |                                                                                                  |
| 0x6C1      | Poke\_AddrLo                   |                                                                                                  |
| 0x6C2      | Poke\_WriteVal                 | 0 is written here during most queries.                                                           |
| 0x6C3      | Poke\_Control                  | Big bitfield. After write, the result of query is written to 4 bytes at Poke\_Addr.              |
| 0xD34      |                                | Used by SetConservativeRasterDilate.                                                             |
| 0xE0A      |                                | Used by SetConservativeRasterDilate.                                                             |
| 0xE0B      |                                | Used by SetConservativeRasterDilate.                                                             |
| 0xE20      |                                | Another barrier? Used by SetConservativeRasterDilate.                                            |
| 0xE2A      | DebugGroupPush\_DynamicControl |                                                                                                  |
| 0xE2B      | DebugGroupPush\_DynamicValue   | This one can be written a variable number of times.                                              |
| 0xE2C      | DebugGroupPush\_StaticControl  |                                                                                                  |
| 0xE2D      | DebugGroupPush\_StaticValue    | This is written 3 times after DebugGroupPush\_StaticControl.                                     |
| 0xE2E      | DebugGroupPop\_Control         |                                                                                                  |
| 0xE2F      | DebugGroupPop\_GroupId         | This is written once after DebugGroupPop\_Control.                                               |

TODO: SetRenderTargets, SetSubpixelPrecisionBias, SetTiledCacheAction,
SetTiledCacheTileSize, SetViewports, UpdateUniformBuffer,
TiledDownSample

# DMA

| Register | Name            | Notes                                 |
| -------- | --------------- | ------------------------------------- |
| 0x0C0    | Dma\_Control    | With 0x186 Src/DstStride is not used. |
| 0x100    | Dma\_SrcAddrHi  |                                       |
| 0x101    | Dma\_SrcAddrLo  |                                       |
| 0x102    | Dma\_DstAddrHi  |                                       |
| 0x103    | Dma\_DstAddrLo  |                                       |
| 0x104    | Dma\_SrcStride? |                                       |
| 0x105    | Dma\_DstStride? |                                       |
| 0x106    | Dma\_Count      | At most 0x3FFFFF.                     |

## MemoryState

| Bits | Description                                                                                                                                                                |
| ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 7-0  | Type                                                                                                                                                                       |
| 8    | [PermissionChangeAllowed](#svcSetMemoryPermission "wikilink")                                                                                                              |
| 9    | ForceReadWritableByDebugSyscalls                                                                                                                                           |
| 10   | IpcSendAllowed\_Type0                                                                                                                                                      |
| 11   | IpcSendAllowed\_Type3                                                                                                                                                      |
| 12   | IpcSendAllowed\_Type1                                                                                                                                                      |
| 14   | [ProcessPermissionChangeAllowed](#svcSetProcessMemoryPermission "wikilink")                                                                                                |
| 15   | [MapAllowed](#svcMapMemory "wikilink")                                                                                                                                     |
| 16   | [UnmapProcessCodeMemoryAllowed](#svcUnmapProcessCodeMemory "wikilink")                                                                                                     |
| 17   | [TransferMemoryAllowed](#svcCreateTransferMemory "wikilink")                                                                                                               |
| 18   | [QueryPhysicalAddressAllowed](#svcQueryPhysicalAddress "wikilink")                                                                                                         |
| 19   | MapDeviceAllowed ([\#svcMapDeviceAddressSpace](#svcMapDeviceAddressSpace "wikilink") and [\#svcMapDeviceAddressSpaceByForce](#svcMapDeviceAddressSpaceByForce "wikilink")) |
| 20   | [MapDeviceAlignedAllowed](#svcMapDeviceAddressSpaceAligned "wikilink")                                                                                                     |
| 21   | [IpcBufferAllowed](#svcSendSyncRequestWithUserBuffer "wikilink")                                                                                                           |
| 22   | IsPoolAllocated/IsReferenceCounted                                                                                                                                         |
| 23   | [MapProcessAllowed](#svcMapProcessMemory "wikilink")                                                                                                                       |
| 24   | [AttributeChangeAllowed](#svcSetMemoryAttribute "wikilink")                                                                                                                |
| 25   | UnknownMemoryAllowed                                                                                                                                                       |

<table>
<thead>
<tr class="header">
<th><p>Value</p></th>
<th><p>Type</p></th>
<th><p>Meaning</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x00000000</p></td>
<td><p>MemoryType_Unmapped</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>0x00002001</p></td>
<td><p>MemoryType_Io</p></td>
<td><p>Mapped by kernel capability parsing in <a href="#svcCreateProcess" class="uri" title="wikilink">#svcCreateProcess</a>.</p></td>
</tr>
<tr class="odd">
<td><p>0x00042002</p></td>
<td><p>MemoryType_Normal</p></td>
<td><p>Mapped by kernel capability parsing in <a href="#svcCreateProcess" class="uri" title="wikilink">#svcCreateProcess</a>.</p></td>
</tr>
<tr class="even">
<td><p>0x00DC7E03</p></td>
<td><p>MemoryType_CodeStatic</p></td>
<td><p>Mapped during <a href="#svcCreateProcess" class="uri" title="wikilink">#svcCreateProcess</a>.</p></td>
</tr>
<tr class="odd">
<td><p>[1.0.0-3.0.1]</p>
<p>0x01FEBD04</p>
<p>[4.0.0+]</p>
<p>0x03FEBD04</p></td>
<td><p>MemoryType_CodeMutable</p></td>
<td><p>Transition from 0xDC7E03 performed by <a href="#svcSetProcessMemoryPermission" class="uri" title="wikilink">#svcSetProcessMemoryPermission</a>.</p></td>
</tr>
<tr class="even">
<td><p>[1.0.0-3.0.1]</p>
<p>0x017EBD05</p>
<p>[4.0.0+]</p>
<p>0x037EBD05</p></td>
<td><p>MemoryType_Heap</p></td>
<td><p>Mapped using <a href="#svcSetHeapSize" class="uri" title="wikilink">#svcSetHeapSize</a>.</p></td>
</tr>
<tr class="odd">
<td><p>0x00402006</p></td>
<td><p>MemoryType_SharedMemory</p></td>
<td><p>Mapped using <a href="#svcMapSharedMemory" class="uri" title="wikilink">#svcMapSharedMemory</a>.</p></td>
</tr>
<tr class="even">
<td><p>0x00482907</p></td>
<td><p>[1.0.0] MemoryType_WeirdSharedMemory</p></td>
<td><p>Mapped using <a href="#svcMapMemory" class="uri" title="wikilink">#svcMapMemory</a>.</p></td>
</tr>
<tr class="odd">
<td><p>0x00DD7E08</p></td>
<td><p>MemoryType_ModuleCodeStatic</p></td>
<td><p>Mapped using <a href="#svcMapProcessCodeMemory" class="uri" title="wikilink">#svcMapProcessCodeMemory</a>.</p></td>
</tr>
<tr class="even">
<td><p>[1.0.0-3.0.1]</p>
<p>0x01FFBD09</p>
<p>[4.0.0+]</p>
<p>0x03FFBD09</p></td>
<td><p>MemoryType_ModuleCodeMutable</p></td>
<td><p>Transition from 0xDD7E08 performed by <a href="#svcSetProcessMemoryPermission" class="uri" title="wikilink">#svcSetProcessMemoryPermission</a>.</p></td>
</tr>
<tr class="odd">
<td><p>0x005C3C0A</p></td>
<td><p><a href="IPC Marshalling.md" title="wikilink">MemoryType_IpcBuffer0</a></p></td>
<td><p>IPC buffers with descriptor flags=0.</p></td>
</tr>
<tr class="even">
<td><p>0x005C3C0B</p></td>
<td><p>MemoryType_MappedMemory</p></td>
<td><p>Mapped using <a href="#svcMapMemory" class="uri" title="wikilink">#svcMapMemory</a>.</p></td>
</tr>
<tr class="odd">
<td><p>0x0040200C</p></td>
<td><p><a href="Thread Local Storage.md" title="wikilink">MemoryType_ThreadLocal</a></p></td>
<td><p>Mapped during <a href="#svcCreateThread" class="uri" title="wikilink">#svcCreateThread</a>.</p></td>
</tr>
<tr class="even">
<td><p>0x015C3C0D</p></td>
<td><p>MemoryType_TransferMemoryIsolated</p></td>
<td><p>Mapped using <a href="#svcMapTransferMemory" class="uri" title="wikilink">#svcMapTransferMemory</a> when the owning process has perm=0.</p></td>
</tr>
<tr class="odd">
<td><p>0x005C380E</p></td>
<td><p>MemoryType_TransferMemory</p></td>
<td><p>Mapped using <a href="#svcMapTransferMemory" class="uri" title="wikilink">#svcMapTransferMemory</a> when the owning process has perm!=0.</p></td>
</tr>
<tr class="even">
<td><p>0x0040380F</p></td>
<td><p>MemoryType_ProcessMemory</p></td>
<td><p>Mapped using <a href="#svcMapProcessMemory" class="uri" title="wikilink">#svcMapProcessMemory</a>.</p></td>
</tr>
<tr class="odd">
<td><p>0x00000010</p></td>
<td><p>MemoryType_Reserved</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>0x005C3811</p></td>
<td><p><a href="IPC Marshalling.md" title="wikilink">MemoryType_IpcBuffer1</a></p></td>
<td><p>IPC buffers with descriptor flags=1.</p></td>
</tr>
<tr class="odd">
<td><p>0x004C2812</p></td>
<td><p><a href="IPC Marshalling.md" title="wikilink">MemoryType_IpcBuffer3</a></p></td>
<td><p>IPC buffers with descriptor flags=3.</p></td>
</tr>
<tr class="even">
<td><p>0x00002013</p></td>
<td><p>MemoryType_KernelStack</p></td>
<td><p>Mapped in kernel during <a href="#svcCreateThread" class="uri" title="wikilink">#svcCreateThread</a>.</p></td>
</tr>
</tbody>
</table>

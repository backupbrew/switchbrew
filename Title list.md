## System Modules

Note: Unlike 3DS, Switch doesn't have a dedicated HTTP-sysmodule.
Instead, processes using HTTP(S) just use libcurl + socket/ssl services.

As of [2.0.0](2.0.0.md "wikilink"), the only sysmodule with a RomFS is
[hid-sysmodule](HID%20services.md "wikilink").

Decimal versions use the format:

  - Bit31-Bit26: Major
  - Bit25-Bit20: Middle
  - Bit19-Bit16: Minor
  - Bit15-Bit0: Build?

<table>
<thead>
<tr class="header">
<th><p>Title-id</p></th>
<th><p>Versions</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0100000000000000</p></td>
<td><p>[bundled with kernel]</p></td>
<td><p><a href="Filesystem services.md" title="wikilink">FS</a></p></td>
</tr>
<tr class="even">
<td><p>0100000000000001</p></td>
<td><p>[bundled with kernel]</p></td>
<td><p><a href="Loader services.md" title="wikilink">Loader</a></p></td>
</tr>
<tr class="odd">
<td><p>0100000000000002</p></td>
<td><p>[bundled with kernel]</p></td>
<td><p><a href="NCM services.md" title="wikilink">NCM</a></p></td>
</tr>
<tr class="even">
<td><p>0100000000000003</p></td>
<td><p>[bundled with kernel]</p></td>
<td><p><a href="Process Manager services.md" title="wikilink">ProcessMana</a></p></td>
</tr>
<tr class="odd">
<td><p>0100000000000004</p></td>
<td><p>[bundled with kernel]</p></td>
<td><p><a href="Services API.md" title="wikilink">sm</a></p></td>
</tr>
<tr class="even">
<td><p>0100000000000005</p></td>
<td><p>[bundled with kernel]</p></td>
<td><p><a href="Boot.md" title="wikilink">boot</a></p></td>
</tr>
<tr class="odd">
<td><p>0100000000000006</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="USB services.md" title="wikilink">usb</a></p></td>
</tr>
<tr class="even">
<td><p>0100000000000007</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="TMA services.md" title="wikilink">tma</a></p></td>
</tr>
<tr class="odd">
<td><p>0100000000000008</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="Boot2.md" title="wikilink">boot2</a> (debug)<br />
<a href="Boot2.md" title="wikilink">boot2.prodBoot</a> (retail)<br />
<a href="Boot2.md" title="wikilink">boot2.manuBoot</a> (factory)</p></td>
</tr>
<tr class="even">
<td><p>0100000000000009</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="Settings services.md" title="wikilink">settings</a></p></td>
</tr>
<tr class="odd">
<td><p>010000000000000A</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="Bus services.md" title="wikilink">bus</a></p></td>
</tr>
<tr class="even">
<td><p>010000000000000B</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="Bluetooth Driver services.md" title="wikilink">bluetooth</a></p></td>
</tr>
<tr class="odd">
<td><p>010000000000000C</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="3.0.2.md" title="wikilink">v201457684</a> (3.0.2.20)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="BCAT services.md" title="wikilink">bcat</a></p></td>
</tr>
<tr class="even">
<td><p>010000000000000D</p></td>
<td></td>
<td><p>dmnt (currently not present on retail devices)</p></td>
</tr>
<tr class="odd">
<td><p>010000000000000E</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="Friend services.md" title="wikilink">friends</a></p></td>
</tr>
<tr class="even">
<td><p>010000000000000F</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131082</a> (0.0.2.10)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="Network Interface services.md" title="wikilink">nifm</a></p></td>
</tr>
<tr class="odd">
<td><p>0100000000000010</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131132</a> (0.0.2.60)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.0.2.md" title="wikilink">v335675432</a> (5.0.2.40)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="PTM services.md" title="wikilink">ptm</a></p></td>
</tr>
<tr class="even">
<td><p>0100000000000011</p></td>
<td></td>
<td><p>shell (currently not present on retail devices)</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000012</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.3.0.md" title="wikilink">v131092</a> (0.0.2.20)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="3.0.2.md" title="wikilink">v201457684</a> (3.0.2.20)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.0.2.md" title="wikilink">v335675432</a> (5.0.2.40)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="Sockets services.md" title="wikilink">bsdsockets</a></p></td>
</tr>
<tr class="even">
<td><p>0100000000000013</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131132</a> (0.0.2.60)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="4.1.0.md" title="wikilink">v269484082</a> (4.1.0.50)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.0.2.md" title="wikilink">v335675432</a> (5.0.2.40)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="HID services.md" title="wikilink">hid</a></p></td>
</tr>
<tr class="odd">
<td><p>0100000000000014</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="Audio services.md" title="wikilink">audio</a></p></td>
</tr>
<tr class="even">
<td><p>0100000000000015</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="Log services.md" title="wikilink">LogManager</a> (debug)<br />
<a href="Log services.md" title="wikilink">LogManager.Prod</a> (retail)</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000016</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131082</a> (0.0.2.10)<br />
<a href="2.2.0.md" title="wikilink">v196608</a> (0.0.3.0)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="3.0.2.md" title="wikilink">v201457684</a> (3.0.2.20)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="WLAN services.md" title="wikilink">wlan</a></p></td>
</tr>
<tr class="even">
<td><p>0100000000000017</p></td>
<td></td>
<td><p>cs (currently not present on retail devices)</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000018</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="LDN services.md" title="wikilink">ldn</a></p></td>
</tr>
<tr class="even">
<td><p>0100000000000019</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131082</a> (0.0.2.10)<br />
<a href="2.3.0.md" title="wikilink">v196628</a> (0.0.3.20)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="3.0.2.md" title="wikilink">v201457684</a> (3.0.2.20)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="4.0.1.md" title="wikilink">v268501002</a> (4.0.1.10)<br />
<a href="4.1.0.md" title="wikilink">v269484082</a> (4.1.0.50)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="NV services.md" title="wikilink">nvservices</a></p></td>
</tr>
<tr class="odd">
<td><p>010000000000001A</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="PCV services.md" title="wikilink">pcv</a></p></td>
</tr>
<tr class="even">
<td><p>010000000000001B</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.0.2.md" title="wikilink">v335675432</a> (5.0.2.40)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="PPC services.md" title="wikilink">ppc</a></p></td>
</tr>
<tr class="odd">
<td><p>010000000000001C</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131082</a> (0.0.2.10)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="4.1.0.md" title="wikilink">v269484082</a> (4.1.0.50)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="Nvnflinger services.md" title="wikilink">nvnflinger</a></p></td>
</tr>
<tr class="even">
<td><p>010000000000001D</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="PCIe services.md" title="wikilink">pcie</a> (debug)<br />
<a href="PCIe services.md" title="wikilink">pcie.withoutHb</a> (retail)</p></td>
</tr>
<tr class="odd">
<td><p>010000000000001E</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="3.0.2.md" title="wikilink">v201457684</a> (3.0.2.20)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="Account services.md" title="wikilink">account</a></p></td>
</tr>
<tr class="even">
<td><p>010000000000001F</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131132</a> (0.0.2.60)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="NS Services.md" title="wikilink">ns</a></p></td>
</tr>
<tr class="odd">
<td><p>0100000000000020</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.2.0.md" title="wikilink">v131072</a> (0.0.2.0)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="NFC services.md" title="wikilink">nfc</a></p></td>
</tr>
<tr class="even">
<td><p>0100000000000021</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="PSC services.md" title="wikilink">psc</a></p></td>
</tr>
<tr class="odd">
<td><p>0100000000000022</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="Capture services.md" title="wikilink">capsrv</a></p></td>
</tr>
<tr class="even">
<td><p>0100000000000023</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131132</a> (0.0.2.60)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="AM services.md" title="wikilink">am</a></p></td>
</tr>
<tr class="odd">
<td><p>0100000000000024</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="SSL services.md" title="wikilink">ssl</a></p></td>
</tr>
<tr class="even">
<td><p>0100000000000025</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131082</a> (0.0.2.10)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="4.1.0.md" title="wikilink">v269484082</a> (4.1.0.50)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="NIM services.md" title="wikilink">nim</a></p></td>
</tr>
<tr class="odd">
<td><p>0100000000000028</p></td>
<td><p>[bundled with kernel]</p></td>
<td><p><a href="SPL services.md" title="wikilink">spl</a></p></td>
</tr>
<tr class="even">
<td><p>0100000000000029</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="Backlight services.md" title="wikilink">lbl</a></p></td>
</tr>
<tr class="odd">
<td><p>010000000000002A</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="BTM services.md" title="wikilink">btm</a></p></td>
</tr>
<tr class="even">
<td><p>010000000000002B</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131132</a> (0.0.2.60)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="Error Report services.md" title="wikilink">erpt</a></p></td>
</tr>
<tr class="odd">
<td><p>010000000000002D</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="Display services.md" title="wikilink">vi</a></p></td>
</tr>
<tr class="even">
<td><p>010000000000002E</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131082</a> (0.0.2.10)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="Parental Control services.md" title="wikilink">pctl</a></p></td>
</tr>
<tr class="odd">
<td><p>010000000000002F</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="NPNS services.md" title="wikilink">npns</a></p></td>
</tr>
<tr class="even">
<td><p>0100000000000030</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131132</a> (0.0.2.60)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="Error Upload services.md" title="wikilink">eupld</a></p></td>
</tr>
<tr class="odd">
<td><p>0100000000000031</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>[1.0.0] arp<br />
[2.0.0+] <a href="Glue services.md" title="wikilink">glue</a></p></td>
</tr>
<tr class="even">
<td><p>0100000000000032</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>eclct</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000033</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="ETicket services.md" title="wikilink">es</a></p></td>
</tr>
<tr class="even">
<td><p>0100000000000034</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131132</a> (0.0.2.60)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="4.1.0.md" title="wikilink">v269484082</a> (4.1.0.50)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="Fatal services.md" title="wikilink">fatal</a></p></td>
</tr>
<tr class="odd">
<td><p>0100000000000035</p></td>
<td><p><a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>[4.0.0+] <a href="GRC services.md" title="wikilink">grc</a></p></td>
</tr>
<tr class="even">
<td><p>0100000000000036</p></td>
<td><p><a href="2.0.0.md" title="wikilink">v260</a> (0.0.0.260)<br />
<a href="2.1.0.md" title="wikilink">v65596</a> (0.0.1.60)<br />
<a href="2.3.0.md" title="wikilink">v131092</a> (0.0.2.20)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="3.0.2.md" title="wikilink">v201457684</a> (3.0.2.20)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p><a href="Creport.md" title="wikilink">creport</a></p></td>
</tr>
<tr class="odd">
<td><p>0100000000000037</p></td>
<td><p><a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>[3.0.0+] <a href="Loader services#ldr:ro.md##ldr:ro" title="wikilink">ro</a></p></td>
</tr>
<tr class="even">
<td><p>0100000000000038</p></td>
<td></td>
<td><p><a href="Profiler services.md" title="wikilink">profiler</a> (currently not present on retail devices)</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000039</p></td>
<td><p><a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>[3.0.0+] <a href="Shared Database services.md" title="wikilink">sdb</a></p></td>
</tr>
<tr class="even">
<td><p>010000000000003A</p></td>
<td><p><a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>[4.0.0+] <a href="Migration services.md" title="wikilink">migration</a></p></td>
</tr>
<tr class="odd">
<td><p>010000000000003B</p></td>
<td></td>
<td><p><a href="JIT services.md" title="wikilink">jit</a> (currently not present on retail devices)</p></td>
</tr>
<tr class="even">
<td><p>010000000000003C</p></td>
<td><p><a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>[4.0.0+] <a href="Jpegdec services.md" title="wikilink">jpegdec</a></p></td>
</tr>
<tr class="odd">
<td><p>010000000000003D</p></td>
<td><p><a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>[4.0.0+] <a href="Safemode.md" title="wikilink">safemode</a></p></td>
</tr>
</tbody>
</table>

## System Data Archives

<table>
<thead>
<tr class="header">
<th><p>Title-id</p></th>
<th><p>Versions</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0100000000000800</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v260</a> (0.0.0.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;CertStore&quot; - SSL trusted certificates.</p></td>
</tr>
<tr class="even">
<td><p>0100000000000801</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.2.0.md" title="wikilink">v196628</a> (0.0.3.20)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.2.md" title="wikilink">v201457684</a> (3.0.2.20)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;ErrorMessage&quot; - Stores the message strings for Support Error Codes. There's &quot;/DatabaseInfo&quot; at FS root, then the rest is stored at &quot;/{first 4 error digits}/{last 4 error digits}/&quot;.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000802</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;MiiModel&quot;</p></td>
</tr>
<tr class="even">
<td><p>0100000000000803</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v196628</a> (0.0.3.20)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;BrowserDll&quot; - Mounted as &quot;shareddata:/&quot;. Contains various browser data: emojis, OSS NROs, &quot;buildinfo/buildinfo.dat&quot;, ...</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000804</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;Help&quot; - HTML resources: Open-source licenses (&quot;Intellectual Property Notices&quot;) and seizure warnings(&quot;Health &amp; Safety Information&quot;). The former is stored at FS &quot;/legallines.htdocs/&quot;<br />
while the latter is at &quot;/safe.htdocs/&quot;.</p></td>
</tr>
<tr class="even">
<td><p>0100000000000805</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;SharedFont&quot; - Chinese and Korean dictionaries.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000806</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.2.md" title="wikilink">v201457684</a> (3.0.2.20)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;NgWord&quot; - Bad words.</p></td>
</tr>
<tr class="even">
<td><p>0100000000000807</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v260</a> (0.0.0.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;SsidList&quot; - <a href="Hotspot List.md" title="wikilink">Hotspot List</a>.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000808</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)</p></td>
<td><p>&quot;Dictionary&quot; - European, English, and Japanese dictionaries.</p></td>
</tr>
<tr class="even">
<td><p>0100000000000809</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v196628</a> (0.0.3.20)<br />
<a href="2.2.0.md" title="wikilink">v196628</a> (0.0.3.20)<br />
<a href="2.3.0.md" title="wikilink">v262164</a> (0.0.4.20)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="3.0.2.md" title="wikilink">v201457684</a> (3.0.2.20)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="4.0.1.md" title="wikilink">v268501002</a> (4.0.1.10)<br />
<a href="4.1.0.md" title="wikilink">v269484082</a> (4.1.0.50)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.0.1.md" title="wikilink">v335609886</a> (5.0.1.30)<br />
<a href="5.0.2.md" title="wikilink">v335675432</a> (5.0.2.40)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;SystemVersion&quot; - <a href="System Version Title.md" title="wikilink">System Version Title</a>.</p></td>
</tr>
<tr class="odd">
<td><p>010000000000080A</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;AvatarImage&quot; - Background and Character images for user avatars (RGBA format &amp; Yaz0 compression).</p></td>
</tr>
<tr class="even">
<td><p>010000000000080B</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;LocalNews&quot; - Tutorial images and strings. Used for the offline news by the News applet.</p></td>
</tr>
<tr class="odd">
<td><p>010000000000080C</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)</p></td>
<td><p>&quot;Eura&quot; - EULA. Also accessed by <a href="NS Services.md" title="wikilink">NS</a>.</p></td>
</tr>
<tr class="even">
<td><p>010000000000080D</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;UrlBlackList&quot;</p></td>
</tr>
<tr class="odd">
<td><p>010000000000080E</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;TimeZoneBinary&quot;</p></td>
</tr>
<tr class="even">
<td><p>010000000000080F</p></td>
<td></td>
<td><p>&quot;BrowserCertStore&quot; (currently not present on retail devices)</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000810</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;FontNintendoExtension&quot;</p></td>
</tr>
<tr class="even">
<td><p>0100000000000811</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;FontStandard&quot;</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000812</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;FontKorean&quot;</p></td>
</tr>
<tr class="even">
<td><p>0100000000000813</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;FontChineseTraditional&quot;</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000814</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;FontChineseSimple&quot;</p></td>
</tr>
<tr class="even">
<td><p>0100000000000815</p></td>
<td></td>
<td><p>&quot;FontBfcpx&quot; (currently not present on retail devices)</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000816</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131162</a> (0.0.2.90)<br />
<a href="2.2.0.md" title="wikilink">v196628</a> (0.0.3.20)<br />
<a href="2.3.0.md" title="wikilink">v262164</a> (0.0.4.20)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="3.0.2.md" title="wikilink">v201457684</a> (3.0.2.20)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="4.0.1.md" title="wikilink">v268501002</a> (4.0.1.10)<br />
<a href="4.1.0.md" title="wikilink">v269484082</a> (4.1.0.50)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.0.1.md" title="wikilink">v335609886</a> (5.0.1.30)<br />
<a href="5.0.2.md" title="wikilink">v335675432</a> (5.0.2.40)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>Contains the title-listing for the associated sysupdate in the <a href="NCA.md" title="wikilink">NCA</a>-type0 .cnmt.</p></td>
</tr>
<tr class="even">
<td><p>0100000000000818</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.3.0.md" title="wikilink">v131082</a> (0.0.2.10)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="4.1.0.md" title="wikilink">v269484082</a> (4.1.0.50)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.0.1.md" title="wikilink">v335609886</a> (5.0.1.30)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>System config.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000819</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131082</a> (0.0.2.10)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="3.0.2.md" title="wikilink">v201457684</a> (3.0.2.20)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="4.1.0.md" title="wikilink">v269484082</a> (4.1.0.50)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>Firmware Package A: Normal Firmware.</p></td>
</tr>
<tr class="even">
<td><p>010000000000081A</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131082</a> (0.0.2.10)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="3.0.2.md" title="wikilink">v201457684</a> (3.0.2.20)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="4.1.0.md" title="wikilink">v269484082</a> (4.1.0.50)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>Firmware Package B: SafeMode Firmware. See <a href="Boot Modes#Safe Mode.md##Safe_Mode" title="wikilink">Safe Mode</a>.</p></td>
</tr>
<tr class="odd">
<td><p>010000000000081B</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131082</a> (0.0.2.10)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="3.0.2.md" title="wikilink">v201457684</a> (3.0.2.20)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="4.1.0.md" title="wikilink">v269484082</a> (4.1.0.50)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>Firmware Package C: Normal Firmware (exFAT variant). Identical to 0100000000000819 with different FS sysmodule. Requires a device ID to download from CDN.</p></td>
</tr>
<tr class="even">
<td><p>010000000000081C</p></td>
<td><p><a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="4.1.0.md" title="wikilink">v269484082</a> (4.1.0.50)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>Firmware Package D: SafeMode Firmware (exFAT variant). Identical to 010000000000081A with different FS sysmodule. Requires a device ID to download from CDN.</p></td>
</tr>
<tr class="odd">
<td><p>010000000000081D</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>Errdisp strings.</p></td>
</tr>
<tr class="even">
<td><p>010000000000081E</p></td>
<td><p><a href="2.0.0.md" title="wikilink">v260</a> (0.0.0.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>Controller gfx/icon data + dummy file.</p></td>
</tr>
<tr class="odd">
<td><p>010000000000081F</p></td>
<td><p><a href="2.0.0.md" title="wikilink">v260</a> (0.0.0.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>Icosa system config.</p></td>
</tr>
<tr class="even">
<td><p>0100000000000820</p></td>
<td><p><a href="2.0.0.md" title="wikilink">v260</a> (0.0.0.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>Copper system config.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000821</p></td>
<td><p><a href="2.0.0.md" title="wikilink">v260</a> (0.0.0.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>Hoag system config.</p></td>
</tr>
<tr class="even">
<td><p>0100000000000822</p></td>
<td><p><a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.2.md" title="wikilink">v201457684</a> (3.0.2.20)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>Firmware binaries for peripherals (hardware within Joy-Cons/etc).</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000823</p></td>
<td><p><a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>Contains version.dat and ac_*_nx files. All of the *_nx files stored under here are compressed with gzip.</p></td>
</tr>
<tr class="even">
<td><p>0100000000000824</p></td>
<td><p><a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>IcosaMariko system config.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000825</p></td>
<td><p><a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>Application blacklist. Used by <a href="NS Services.md" title="wikilink">NS</a> for restricting application installation and updates.</p></td>
</tr>
<tr class="even">
<td><p>0100000000000826</p></td>
<td><p><a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>Rebootless system update version file.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000827</p></td>
<td><p><a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td></td>
</tr>
</tbody>
</table>

## System Applets

<table>
<thead>
<tr class="header">
<th><p>Title-id</p></th>
<th><p>Versions</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0100000000001000</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131162</a> (0.0.2.90)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.0.1.md" title="wikilink">v335609886</a> (5.0.1.30)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;SystemAppletMenu&quot; - <a href="Qlaunch.md" title="wikilink">qlaunch</a> system applet, launched by NS with TID loaded from system-config-title.</p></td>
</tr>
<tr class="even">
<td><p>0100000000001001</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;LibraryAppletAuth&quot;</p></td>
</tr>
<tr class="odd">
<td><p>0100000000001002</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;LibraryAppletCabinet&quot;</p></td>
</tr>
<tr class="even">
<td><p>0100000000001003</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;LibraryAppletController&quot;</p></td>
</tr>
<tr class="odd">
<td><p>0100000000001004</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;LibraryAppletDataErase&quot;</p></td>
</tr>
<tr class="even">
<td><p>0100000000001005</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;LibraryAppletError&quot;</p></td>
</tr>
<tr class="odd">
<td><p>0100000000001006</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;LibraryAppletNetConnect&quot;</p></td>
</tr>
<tr class="even">
<td><p>0100000000001007</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;LibraryAppletPlayerSelect&quot;</p></td>
</tr>
<tr class="odd">
<td><p>0100000000001008</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131132</a> (0.0.2.60)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;LibraryAppletSwkbd&quot;</p></td>
</tr>
<tr class="even">
<td><p>0100000000001009</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;LibraryAppletMiiEdit&quot;</p></td>
</tr>
<tr class="odd">
<td><p>010000000000100A</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131162</a> (0.0.2.90)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;LibraryAppletWeb&quot; - <a href="Internet Browser.md" title="wikilink">WebApplet</a>.</p></td>
</tr>
<tr class="even">
<td><p>010000000000100B</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131162</a> (0.0.2.90)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;LibraryAppletShop&quot; - <a href="Internet Browser.md" title="wikilink">ShopN</a> applet.</p></td>
</tr>
<tr class="odd">
<td><p>010000000000100C</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;OverlayApplet&quot; - TID is loaded by NS from system-config-title.</p></td>
</tr>
<tr class="even">
<td><p>010000000000100D</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;LibraryAppletPhotoViewer&quot;</p></td>
</tr>
<tr class="odd">
<td><p>010000000000100E</p></td>
<td></td>
<td><p>&quot;LibraryAppletSet&quot; (currently not present on retail devices)</p></td>
</tr>
<tr class="even">
<td><p>010000000000100F</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131162</a> (0.0.2.90)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;LibraryAppletOfflineWeb&quot; - <a href="Internet Browser.md" title="wikilink">Offline</a> web-applet.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000001010</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131162</a> (0.0.2.90)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;LibraryAppletLoginShare&quot; - <a href="Internet Browser.md" title="wikilink">Whitelisted</a> applet. (LoginApplet+ShareApplet+LobbyApplet)</p></td>
</tr>
<tr class="even">
<td><p>0100000000001011</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131162</a> (0.0.2.90)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;LibraryAppletWifiWebAuth&quot; - <a href="Internet Browser.md" title="wikilink">WifiWebAuth</a> applet.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000001012</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;Starter&quot;</p></td>
</tr>
<tr class="even">
<td><p>0100000000001013</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.0.1.md" title="wikilink">v335609886</a> (5.0.1.30)<br />
<a href="5.0.2.md" title="wikilink">v335675432</a> (5.0.2.40)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)</p></td>
<td><p>&quot;LibraryAppletMyPage&quot;</p></td>
</tr>
<tr class="odd">
<td><p>0100000000001015</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;MaintenanceMenu&quot; - Initial applet displayed when booting into <a href="Recovery Mode.md" title="wikilink">Recovery_Mode</a>. This title is launched by <a href="NS Services.md" title="wikilink">NS</a> when a state flag is val1 indicating that this title should be launched instead of the above &quot;SystemAppletMenu&quot; title.</p></td>
</tr>
<tr class="even">
<td><p>0100000000001016</p></td>
<td></td>
<td><p>TitleID used by <a href="NS Services.md" title="wikilink">NS</a> when a certain flag is non-zero, in multiple places including around code using string &quot;application_install&quot;. This title doesn't seem to exist for retail.</p></td>
</tr>
<tr class="odd">
<td><p>010000000000101E</p></td>
<td></td>
<td><p>This title is referenced by [5.0.0+] <a href="NIM services.md" title="wikilink">NIM</a> when it accesses the <a href="Network#pearljam.md##pearljam" title="wikilink">pearljam</a> server, but does not exist on retail systems currently.</p></td>
</tr>
</tbody>
</table>

## System Debug Applets

Note: No 01000000000020XX titles exist on retail
systems.

| Title-id         | Versions | Description                                                                                           |
| ---------------- | -------- | ----------------------------------------------------------------------------------------------------- |
| 0100000000002000 |          | "BoardTest"                                                                                           |
| 0100000000002001 |          | "BoardWireless"                                                                                       |
| 0100000000002002 |          | C1LcdAndKey - "LcdAndKey". LCD/Keyboard testing.                                                      |
| 0100000000002003 |          | C2UsbHpmic - "UsbAndHPMicTest". USB and audio testing.                                                |
| 0100000000002004 |          | C3Aging - "Aging". Graphics/Framerate testing.                                                        |
| 0100000000002005 |          | C4SixAxis - "6axisTest". Sixaxis (controller peripheral) testing.                                     |
| 0100000000002006 |          | C5Wireless - "AssembledWireless". Wireless testing.                                                   |
| 0100000000002007 |          | "FinalCheck"                                                                                          |
| 0100000000002041 |          | recovery                                                                                              |
| 0100000000002044 |          | "HB-TBIntegrationTest"                                                                                |
| 010000000000204D |          | BackupSaveData                                                                                        |
| 010000000000204E |          | A4BoardCalWriti - "BoardCalWriting". Writes calibration data to NAND.                                 |
| 0100000000002055 |          | GameCardWriter                                                                                        |
| 0100000000002054 |          | RepairSslCertif - "RepairSslCertificate".                                                             |
| 0100000000002064 |          | DevMenu                                                                                               |
| 0100000000002071 |          | "snap\_shot\_dump" - Used by [NS](NS%20Services.md "wikilink").                                       |
| 010000000000209B |          | "am.debug" - Used by [AM](AM%20services.md "wikilink").                                               |
| 010000000000209C |          | TestApplication - "TestApplicationLauncher". Factory qlaunch replacement, used to launch other tests. |
| 01000000000020F0 |          | "devmenuapp\_installer" - Launched by [boot2](Boot2.md "wikilink").                                   |

## Target Tools

| Title-id         | Versions | Description                                      |
| ---------------- | -------- | ------------------------------------------------ |
| 1000000000000001 |          | [SystemInitializ](Factory%20Setup.md "wikilink") |
| 1000000000000004 |          | [CalWriterManu](Factory%20Setup.md "wikilink")   |
| 1000000000000005 |          | DevMenuCommand                                   |
| 1000000000000006 |          | SettingsManager                                  |
| 1000000000000007 |          | "ApplicationLauncer"                             |
| 100000000000000B |          | SnapShotDumper                                   |
| 100000000000000C |          | SystemUpdater                                    |
| 100000000000000E |          | ControllerFirmw - "ControllerFirmwareUpdater".   |

## Factory System Modules

| Title-id         | Versions | Description                                                                                                                                         |
| ---------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| 100000000000B120 |          | Launched by maintenance mode [boot2.manuBoot](Boot2.md "wikilink"), but not present in retail or [factory firmware](Factory%20Setup.md "wikilink"). |
| 100000000000B14A |          | [manu](Manu%20Services.md "wikilink") - installed in [factory firmware](Factory%20Setup.md "wikilink").                                             |

## System Applications

<table>
<thead>
<tr class="header">
<th><p>Title-id</p></th>
<th><p>Versions</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>01008BB00013C000</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)</p></td>
<td><p>&quot;<a href="Flog.md" title="wikilink">flog</a>&quot; NES emulator.</p></td>
</tr>
<tr class="even">
<td><p>0100069000078000</p></td>
<td><p>v0</p></td>
<td><p>&quot;Retail Interactive Display Menu&quot;. This title can be launched by <a href="Qlaunch.md" title="wikilink">qlaunch</a>, but is not normally installed on retail systems.</p></td>
</tr>
</tbody>
</table>

## eShop Games / Applications

Note: Nintendo Switch game and application titles follow a higher
entropy TitleID scheme than previous generation consoles.  
Refer to the [Games List](Title%20list%20Games.md "wikilink") for more
information.

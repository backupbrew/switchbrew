## System Modules

Note: Unlike 3DS, Switch doesn't have a dedicated HTTP-sysmodule.
Instead, processes using HTTP(S) just use libcurl + socket/ssl services.

As of [2.0.0](2.0.0.md "wikilink"), the only sysmodule with a RomFS is
[hid-sysmodule](HID%20services.md "wikilink").

Decimal versions use the format:

  - Bit31-Bit26: Major
  - Bit25-Bit20: Minor
  - Bit19-Bit16: Micro
  - Bit15-Bit0: Bugfix

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
<td><p><a href="Filesystem services.md" title="wikilink">fs</a></p></td>
</tr>
<tr class="even">
<td><p>0100000000000001</p></td>
<td><p>[bundled with kernel]</p></td>
<td><p><a href="Loader services.md" title="wikilink">ldr (Loader)</a></p></td>
</tr>
<tr class="odd">
<td><p>0100000000000002</p></td>
<td><p>[bundled with kernel]</p></td>
<td><p><a href="NCM services.md" title="wikilink">ncm</a></p></td>
</tr>
<tr class="even">
<td><p>0100000000000003</p></td>
<td><p>[bundled with kernel]</p></td>
<td><p><a href="Process Manager services.md" title="wikilink">pm (ProcessMana)</a></p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="7.0.1.md" title="wikilink">v469827614</a> (7.0.1.30)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.0.1.md" title="wikilink">v536936528</a> (8.0.1.80)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.0.1.md" title="wikilink">v402718730</a> (6.0.1.10)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.0.1.md" title="wikilink">v536936528</a> (8.0.1.80)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.0.1.md" title="wikilink">v402718730</a> (6.0.1.10)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="7.0.1.md" title="wikilink">v469827614</a> (7.0.1.30)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.0.1.md" title="wikilink">v536936528</a> (8.0.1.80)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="7.0.1.md" title="wikilink">v469827614</a> (7.0.1.30)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.0.1.md" title="wikilink">v536936528</a> (8.0.1.80)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p><a href="NIM services.md" title="wikilink">nim</a></p></td>
</tr>
<tr class="odd">
<td><p>0100000000000026</p></td>
<td></td>
<td><p>cec (currently not present on retail devices)</p></td>
</tr>
<tr class="even">
<td><p>0100000000000027</p></td>
<td></td>
<td><p>tspm (currently not present on retail devices)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="7.0.1.md" title="wikilink">v469827614</a> (7.0.1.30)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p><a href="Error Report services.md" title="wikilink">erpt</a></p></td>
</tr>
<tr class="odd">
<td><p>010000000000002C</p></td>
<td></td>
<td><p>time (currently not present on retail devices)</p></td>
</tr>
<tr class="even">
<td><p>010000000000002D</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p><a href="Display services.md" title="wikilink">vi</a></p></td>
</tr>
<tr class="odd">
<td><p>010000000000002E</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131082</a> (0.0.2.10)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p><a href="Parental Control services.md" title="wikilink">pctl</a></p></td>
</tr>
<tr class="even">
<td><p>010000000000002F</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.0.1.md" title="wikilink">v536936528</a> (8.0.1.80)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p><a href="NPNS services.md" title="wikilink">npns</a></p></td>
</tr>
<tr class="odd">
<td><p>0100000000000030</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131132</a> (0.0.2.60)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p><a href="Error Upload services.md" title="wikilink">eupld</a></p></td>
</tr>
<tr class="even">
<td><p>0100000000000031</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>[1.0.0] arp<br />
[2.0.0+] <a href="Glue services.md" title="wikilink">glue</a></p></td>
</tr>
<tr class="odd">
<td><p>0100000000000032</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>eclct</p></td>
</tr>
<tr class="even">
<td><p>0100000000000033</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="7.0.1.md" title="wikilink">v469827614</a> (7.0.1.30)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p><a href="ETicket services.md" title="wikilink">es</a></p></td>
</tr>
<tr class="odd">
<td><p>0100000000000034</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131132</a> (0.0.2.60)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="4.1.0.md" title="wikilink">v269484082</a> (4.1.0.50)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p><a href="Fatal services.md" title="wikilink">fatal</a></p></td>
</tr>
<tr class="even">
<td><p>0100000000000035</p></td>
<td><p><a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>[4.0.0+] <a href="GRC services.md" title="wikilink">grc</a></p></td>
</tr>
<tr class="odd">
<td><p>0100000000000036</p></td>
<td><p><a href="2.0.0.md" title="wikilink">v260</a> (0.0.0.260)<br />
<a href="2.1.0.md" title="wikilink">v65596</a> (0.0.1.60)<br />
<a href="2.3.0.md" title="wikilink">v131092</a> (0.0.2.20)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="3.0.2.md" title="wikilink">v201457684</a> (3.0.2.20)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p><a href="Creport.md" title="wikilink">creport</a></p></td>
</tr>
<tr class="even">
<td><p>0100000000000037</p></td>
<td><p><a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>[3.0.0+] <a href="Loader services#ldr:ro.md##ldr:ro" title="wikilink">ro</a></p></td>
</tr>
<tr class="odd">
<td><p>0100000000000038</p></td>
<td></td>
<td><p><a href="Profiler services.md" title="wikilink">profiler</a> (currently not present on retail devices)</p></td>
</tr>
<tr class="even">
<td><p>0100000000000039</p></td>
<td><p><a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>[3.0.0+] <a href="Shared Database services.md" title="wikilink">sdb</a></p></td>
</tr>
<tr class="odd">
<td><p>010000000000003A</p></td>
<td><p><a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>[4.0.0+] <a href="Migration services.md" title="wikilink">migration</a></p></td>
</tr>
<tr class="even">
<td><p>010000000000003B</p></td>
<td></td>
<td><p><a href="JIT services.md" title="wikilink">jit</a> (currently not present on retail devices)</p></td>
</tr>
<tr class="odd">
<td><p>010000000000003C</p></td>
<td><p><a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>[4.0.0+] <a href="Jpegdec services.md" title="wikilink">jpegdec</a></p></td>
</tr>
<tr class="even">
<td><p>010000000000003D</p></td>
<td><p><a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>[4.0.0+] <a href="Safemode.md" title="wikilink">safemode</a></p></td>
</tr>
<tr class="odd">
<td><p>010000000000003E</p></td>
<td><p><a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>[6.0.0+] <a href="OLSC services.md" title="wikilink">olsc</a></p></td>
</tr>
<tr class="even">
<td><p>010000000000003F</p></td>
<td></td>
<td><p>dt (currently not present on retail devices)</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000040</p></td>
<td></td>
<td><p>nd (currently not present on retail devices)</p></td>
</tr>
<tr class="even">
<td><p>0100000000000041</p></td>
<td><p><a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>[9.0.0+] <a href="NGCT services.md" title="wikilink">ngct</a></p></td>
</tr>
</tbody>
</table>

## System Data Archives

<table>
<thead>
<tr class="header">
<th><p>Title-id</p></th>
<th><p>Versions</p></th>
<th><p>Name</p></th>
<th><p>Notes</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0100000000000800</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v260</a> (0.0.0.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p><a href="SSL services#CertStore.md##CertStore" title="wikilink">CertStore</a></p></td>
<td><p>SSL trusted certificates.</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>ErrorMessage</p></td>
<td><p>Stores the message strings for Support Error Codes. There's "/DatabaseInfo" at FS root, then the rest is stored at "/{first 4 error digits}/{last 4 error digits}/".</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000802</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>MiiModel</p></td>
<td></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>BrowserDll</p></td>
<td><p>Mounted as "shareddata:/". Contains various browser data: emojis, OSS NROs, "buildinfo/buildinfo.dat", ...</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000804</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>Help</p></td>
<td><p>HTML resources: Open-source licenses ("Intellectual Property Notices") and seizure warnings("Health &amp; Safety Information"). The former is stored at FS "/legallines.htdocs/"<br />
while the latter is at "/safe.htdocs/".</p></td>
</tr>
<tr class="even">
<td><p>0100000000000805</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>SharedFont</p></td>
<td><p>Chinese and Korean dictionaries.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000806</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.2.md" title="wikilink">v201457684</a> (3.0.2.20)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>NgWord</p></td>
<td><p>Bad words.</p></td>
</tr>
<tr class="even">
<td><p>0100000000000807</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v260</a> (0.0.0.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>SsidList</p></td>
<td><p><a href="Hotspot List.md" title="wikilink">Hotspot List</a>.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000808</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)</p></td>
<td><p>Dictionary</p></td>
<td><p>European, English, and Japanese dictionaries.</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.0.1.md" title="wikilink">v402718730</a> (6.0.1.10)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="7.0.1.md" title="wikilink">v469827614</a> (7.0.1.30)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.0.1.md" title="wikilink">v536936528</a> (8.0.1.80)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>SystemVersion</p></td>
<td><p><a href="System Version Title.md" title="wikilink">System Version Title</a>.</p></td>
</tr>
<tr class="odd">
<td><p>010000000000080A</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>AvatarImage</p></td>
<td><p>Background and Character images for user avatars (RGBA format &amp; Yaz0 compression).</p></td>
</tr>
<tr class="even">
<td><p>010000000000080B</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>LocalNews</p></td>
<td><p>Tutorial images and strings. Used for the offline news by the News applet.</p></td>
</tr>
<tr class="odd">
<td><p>010000000000080C</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>Eula (Eura)</p></td>
<td><p>Accessed by <a href="NS Services.md" title="wikilink">NS</a>.</p></td>
</tr>
<tr class="even">
<td><p>010000000000080D</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)</p></td>
<td><p>UrlBlackList</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>010000000000080E</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>TimeZoneBinary</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>010000000000080F</p></td>
<td></td>
<td><p>CertStoreCruiser (BrowserCertStore)</p></td>
<td><p>Currently not present on retail devices.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000810</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>FontNintendoExtension</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>0100000000000811</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>FontStandard</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>0100000000000812</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>FontKorean</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>0100000000000813</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>FontChineseTraditional</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>0100000000000814</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>FontChineseSimple</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>0100000000000815</p></td>
<td></td>
<td><p>FontBfcpx</p></td>
<td><p>Currently not present on retail devices.</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.0.1.md" title="wikilink">v402718730</a> (6.0.1.10)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="7.0.1.md" title="wikilink">v469827614</a> (7.0.1.30)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.0.1.md" title="wikilink">v536936528</a> (8.0.1.80)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>SystemUpdate</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>FirmwareDebugSettings</p></td>
<td><p><a href="System Settings.md" title="wikilink">System config</a>.</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="7.0.1.md" title="wikilink">v469827614</a> (7.0.1.30)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>BootImagePackage</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="7.0.1.md" title="wikilink">v469827614</a> (7.0.1.30)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>BootImagePackageSafe</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="7.0.1.md" title="wikilink">v469827614</a> (7.0.1.30)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>BootImagePackageExFat</p></td>
<td><p>Firmware Package C: Normal Firmware (exFAT variant). Identical to 0100000000000819 with different FS sysmodule. Requires a device ID to download from CDN.</p></td>
</tr>
<tr class="even">
<td><p>010000000000081C</p></td>
<td><p><a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="4.1.0.md" title="wikilink">v269484082</a> (4.1.0.50)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="7.0.1.md" title="wikilink">v469827614</a> (7.0.1.30)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>BootImagePackageExFatSafe</p></td>
<td><p>Firmware Package D: SafeMode Firmware (exFAT variant). Identical to 010000000000081A with different FS sysmodule. Requires a device ID to download from CDN.</p></td>
</tr>
<tr class="odd">
<td><p>010000000000081D</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>FatalMessage</p></td>
<td><p>Errdisp strings.</p></td>
</tr>
<tr class="even">
<td><p>010000000000081E</p></td>
<td><p><a href="2.0.0.md" title="wikilink">v260</a> (0.0.0.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>ControllerIcon</p></td>
<td><p>Controller gfx/icon data + dummy file.</p></td>
</tr>
<tr class="odd">
<td><p>010000000000081F</p></td>
<td><p><a href="2.0.0.md" title="wikilink">v260</a> (0.0.0.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>PlatformConfigIcosa</p></td>
<td><p>Icosa system config.</p></td>
</tr>
<tr class="even">
<td><p>0100000000000820</p></td>
<td><p><a href="2.0.0.md" title="wikilink">v260</a> (0.0.0.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>PlatformConfigCopper</p></td>
<td><p>Copper system config.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000821</p></td>
<td><p><a href="2.0.0.md" title="wikilink">v260</a> (0.0.0.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>PlatformConfigHoag</p></td>
<td><p>Hoag system config.</p></td>
</tr>
<tr class="even">
<td><p>0100000000000822</p></td>
<td><p><a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.2.md" title="wikilink">v201457684</a> (3.0.2.20)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>ControllerFirmware</p></td>
<td><p>Firmware binaries for peripherals (hardware within Joy-Cons/etc).</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000823</p></td>
<td><p><a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>NgWord2</p></td>
<td><p>Contains version.dat and ac_*_nx files. All of the *_nx files stored under here are compressed with gzip.</p></td>
</tr>
<tr class="even">
<td><p>0100000000000824</p></td>
<td><p><a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>PlatformConfigIcosaMariko</p></td>
<td><p>IcosaMariko system config.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000825</p></td>
<td><p><a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>ApplicationBlackList</p></td>
<td><p>Used by <a href="NS Services.md" title="wikilink">NS</a> for restricting application installation and updates.</p></td>
</tr>
<tr class="even">
<td><p>0100000000000826</p></td>
<td><p><a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>RebootlessSystemUpdateVersion</p></td>
<td><p>Rebootless system update version file.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000827</p></td>
<td><p><a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>ContentActionTable</p></td>
<td><p>Used by <a href="AM services.md" title="wikilink">AM</a>.</p></td>
</tr>
<tr class="even">
<td><p>0100000000000828</p></td>
<td><p><a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>FunctionBlackList</p></td>
<td><p>Used for restricting specific features in applications.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000829</p></td>
<td></td>
<td><p>PlatformConfigCalcio</p></td>
<td><p>Currently not present on retail devices.</p></td>
</tr>
<tr class="even">
<td><p>0100000000000830</p></td>
<td><p><a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>NgWordT</p></td>
<td><p>Bad words for China region (Tencent).</p></td>
</tr>
</tbody>
</table>

## System Applets

<table>
<thead>
<tr class="header">
<th><p>Title-id</p></th>
<th><p>Versions</p></th>
<th><p>Name</p></th>
<th><p>Notes</p></th>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.0.1.md" title="wikilink">v402718730</a> (6.0.1.10)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.0.1.md" title="wikilink">v536936528</a> (8.0.1.80)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>qlaunch (SystemAppletMenu)</p></td>
<td><p><a href="Qlaunch.md" title="wikilink">qlaunch</a> system applet, launched by NS with TID loaded from system-config-title.</p></td>
</tr>
<tr class="even">
<td><p>0100000000001001</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p><a href="Auth Applet.md" title="wikilink">auth</a> (LibraryAppletAuth)</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>0100000000001002</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>cabinet (LibraryAppletCabinet)</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>0100000000001003</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>controller (LibraryAppletController)</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>0100000000001004</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>dataErase (LibraryAppletDataErase)</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>0100000000001005</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>error (LibraryAppletError)</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>0100000000001006</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>netConnect (LibraryAppletNetConnect)</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>0100000000001007</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p><a href="Profile Selector.md" title="wikilink">playerSelect (LibraryAppletPlayerSelect)</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>0100000000001008</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131132</a> (0.0.2.60)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p><a href="Software Keyboard.md" title="wikilink">swkbd (LibraryAppletSwkbd)</a></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>0100000000001009</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>miiEdit (LibraryAppletMiiEdit)</p></td>
<td></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>web (LibraryAppletWeb)</p></td>
<td><p><a href="Internet Browser.md" title="wikilink">WebApplet</a>.</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>shop (LibraryAppletShop)</p></td>
<td><p><a href="Internet Browser.md" title="wikilink">ShopN</a> applet.</p></td>
</tr>
<tr class="odd">
<td><p>010000000000100C</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>overlayDisp (OverlayApplet)</p></td>
<td><p>TID is loaded by NS from system-config-title.</p></td>
</tr>
<tr class="even">
<td><p>010000000000100D</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p><a href="Album Applet.md" title="wikilink">photoViewer (LibraryAppletPhotoViewer)</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>010000000000100E</p></td>
<td></td>
<td><p>set (LibraryAppletSet)</p></td>
<td><p>Currently not present on retail devices.</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>offlineWeb (LibraryAppletOfflineWeb)</p></td>
<td><p><a href="Internet Browser.md" title="wikilink">Offline</a> web-applet.</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>loginShare (LibraryAppletLoginShare)</p></td>
<td><p><a href="Internet Browser.md" title="wikilink">Whitelisted</a> applet. (LoginApplet+ShareApplet+LobbyApplet)</p></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.1.0.md" title="wikilink">v403701850</a> (6.1.0.90)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="8.1.0.md" title="wikilink">v537919608</a> (8.1.0.120)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>wifiWebAuth (LibraryAppletWifiWebAuth)</p></td>
<td><p><a href="Internet Browser.md" title="wikilink">WifiWebAuth</a> applet.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000001012</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>starter (DummyStarter)</p></td>
<td></td>
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
<a href="5.1.0.md" title="wikilink">v336592976</a> (5.1.0.80)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p><a href="MyPage Applet.md" title="wikilink">myPage (LibraryAppletMyPage)</a></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>0100000000001014</p></td>
<td></td>
<td><p>PlayReport</p></td>
<td><p>Currently not present on retail devices.</p></td>
</tr>
<tr class="even">
<td><p>0100000000001015</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)<br />
<a href="6.0.0.md" title="wikilink">v402653544</a> (6.0.0.360)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)<br />
<a href="7.0.0.md" title="wikilink">v469762248</a> (7.0.0.200)<br />
<a href="8.0.0.md" title="wikilink">v536871442</a> (8.0.0.530)<br />
<a href="9.0.0.md" title="wikilink">v603980216</a> (9.0.0.440)</p></td>
<td><p>MaintenanceMenu</p></td>
<td><p>Initial applet displayed when booting into <a href="Recovery Mode.md" title="wikilink">Recovery_Mode</a>. This title is launched by <a href="NS Services.md" title="wikilink">NS</a> when a state flag is val1 indicating that this title should be launched instead of the above "SystemAppletMenu" title.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000001016</p></td>
<td></td>
<td></td>
<td><p>TitleID used by <a href="NS Services.md" title="wikilink">NS</a> when a certain flag is non-zero, in multiple places including around code using string "application_install". This title doesn't seem to exist for retail.</p></td>
</tr>
<tr class="even">
<td><p>010000000000101A</p></td>
<td></td>
<td><p>gift (LibraryAppletGift)</p></td>
<td><p>Currently not present on retail devices.</p></td>
</tr>
<tr class="odd">
<td><p>010000000000101B</p></td>
<td></td>
<td><p>DummyECApplet (LibraryAppletDummyShop)</p></td>
<td><p>Currently not present on retail devices.</p></td>
</tr>
<tr class="even">
<td><p>010000000000101C</p></td>
<td></td>
<td><p>userMigration (LibraryAppletUserMigration)</p></td>
<td><p>Currently not present on retail devices.</p></td>
</tr>
<tr class="odd">
<td><p>010000000000101D</p></td>
<td></td>
<td><p>EncounterSys (LibraryAppletPreomiaSys)</p></td>
<td><p>Currently not present on retail devices.</p></td>
</tr>
<tr class="even">
<td><p>010000000000101E</p></td>
<td></td>
<td></td>
<td><p>This title is referenced by [5.0.0+] <a href="NIM services.md" title="wikilink">NIM</a> when it accesses the <a href="Network#pearljam.md##pearljam" title="wikilink">pearljam</a> server, but does not exist on retail systems currently.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000001020</p></td>
<td></td>
<td><p>story (LibraryAppletStory)</p></td>
<td><p>Currently not present on retail devices.</p></td>
</tr>
<tr class="even">
<td><p>0100000000001031</p></td>
<td></td>
<td></td>
<td><p>This title is referenced by [8.0.0+] <a href="NS Services.md" title="wikilink">NS</a>, but does not exist on retail systems currently.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000001033</p></td>
<td></td>
<td><p>promotion</p></td>
<td><p>This title is referenced by [8.0.0+] <a href="NS Services.md" title="wikilink">NS</a>, but does not exist on retail systems currently.</p></td>
</tr>
<tr class="even">
<td><p>0100000000001FFF</p></td>
<td></td>
<td><p>EndOceanProgramId</p></td>
<td><p>Placeholder for the last valid applet ID.</p></td>
</tr>
</tbody>
</table>

## System Debug Applets

Note: No 01000000000020XX titles exist on retail systems.

| Title-id         | Versions | Name                                                                 | Notes                                                    |
| ---------------- | -------- | -------------------------------------------------------------------- | -------------------------------------------------------- |
| 0100000000002000 |          | A2BoardFunction                                                      |                                                          |
| 0100000000002001 |          | A3Wireless                                                           |                                                          |
| 0100000000002002 |          | C1LcdAndKey (LcdAndKey)                                              | LCD/Keyboard testing.                                    |
| 0100000000002003 |          | C2UsbHpmic (UsbAndHPMicTest)                                         | USB and audio testing.                                   |
| 0100000000002004 |          | C3Aging (Aging)                                                      | Graphics/Framerate testing.                              |
| 0100000000002005 |          | C4SixAxis (6axisTest)                                                | Sixaxis (controller peripheral) testing.                 |
| 0100000000002006 |          | C5Wireless (AssembledWireless)                                       | Wireless testing.                                        |
| 0100000000002007 |          | C7FinalCheck (FinalCheck)                                            |                                                          |
| 010000000000203F |          | AutoCapture                                                          |                                                          |
| 0100000000002040 |          | DevMenuCommandSystem                                                 |                                                          |
| 0100000000002041 |          | recovery                                                             |                                                          |
| 0100000000002042 |          | DevMenuSystem                                                        |                                                          |
| 0100000000002044 |          | HB-TBIntegrationTest                                                 |                                                          |
| 010000000000204D |          | BackupSaveData                                                       |                                                          |
| 010000000000204E |          | A4BoardCalWriti (BoardCalWriting)                                    | Writes calibration data to NAND.                         |
| 0100000000002054 |          | RepairSslCertificate                                                 |                                                          |
| 0100000000002055 |          | GameCardWriter                                                       |                                                          |
| 0100000000002056 |          | UsbPdTestTool                                                        |                                                          |
| 0100000000002057 |          | RepairDeletePctl                                                     |                                                          |
| 0100000000002058 |          | RepairBackup                                                         |                                                          |
| 0100000000002059 |          | RepairRestore                                                        |                                                          |
| 010000000000205A |          | RepairAccountTransfer                                                |                                                          |
| 010000000000205B |          | RepairAutoNetworkUpdater                                             |                                                          |
| 010000000000205C |          | RefurbishReset                                                       |                                                          |
| 010000000000205D |          | RepairAssistCup                                                      |                                                          |
| 010000000000205E |          | RepairPairingCutter                                                  |                                                          |
| 0100000000002064 |          | DevMenu                                                              |                                                          |
| 0100000000002065 |          | DevMenuApp                                                           |                                                          |
| 0100000000002066 |          | GetGameCardAsicInfo                                                  |                                                          |
| 0100000000002068 |          | NfpDebugToolSystem                                                   |                                                          |
| 0100000000002069 |          | AlbumSynchronizer                                                    |                                                          |
| 0100000000002071 |          | SnapShotDumper                                                       | Used by [NS](NS%20Services.md "wikilink").               |
| 0100000000002073 |          | DevMenuSystemApp                                                     |                                                          |
| 0100000000002099 |          | DevOverlayDisp                                                       |                                                          |
| 010000000000209A |          | NandVerifier                                                         |                                                          |
| 010000000000209B |          | GpuCoreDumper                                                        | Used by [AM](AM%20services.md "wikilink").               |
| 010000000000209C |          | TestApplication (TestApplicationLauncher)                            | Factory qlaunch replacement, used to launch other tests. |
| 010000000000209E |          | HelloWorld                                                           |                                                          |
| 01000000000020A0 |          | XcieWriter                                                           |                                                          |
| 01000000000020A1 |          | GpuOverrunNotifier                                                   |                                                          |
| 01000000000020C8 |          | NfpDebugTool                                                         |                                                          |
| 01000000000020CA |          | NoftWriter                                                           |                                                          |
| 01000000000020D0 |          | BcatSystemDebugTool                                                  |                                                          |
| 01000000000020D1 |          | DevSafeModeUpdater                                                   |                                                          |
| 01000000000020D3 |          | ControllerConnectionAnalyzer                                         |                                                          |
| 01000000000020D4 |          | DevKitUpdater                                                        |                                                          |
| 01000000000020D6 |          | RepairTimeReviser                                                    |                                                          |
| 01000000000020D7 |          | RepairReinitializeFuelGauge                                          |                                                          |
| 01000000000020DA |          | RepairAbortMigration                                                 |                                                          |
| 01000000000020DC |          | RepairShowDeviceId                                                   |                                                          |
| 01000000000020DD |          | RepairSetCycleCountReliability                                       |                                                          |
| 01000000000020E1 |          | AlbumDownloader                                                      |                                                          |
| 01000000000020E3 |          | FuelGaugeDumper                                                      |                                                          |
| 01000000000020E4 |          | UnsafeExtract                                                        |                                                          |
| 01000000000020E5 |          | UnsafeEngrave                                                        |                                                          |
| 01000000000020EE |          | BluetoothSettingTool                                                 |                                                          |
| 01000000000020F0 |          | ApplicationInstallerRomfs (devmenuapp\_installer)                    | Launched by [boot2](Boot2.md "wikilink").                |
| 0100000000002100 |          | DevMenuLotcheckDownloader                                            |                                                          |
| 0100000000002101 |          | DevMenuCommand                                                       |                                                          |
| 0100000000002102 |          | ExportPartition                                                      |                                                          |
| 0100000000002103 |          | [SystemInitializer](Factory%20Setup.md "wikilink") (SystemInitializ) |                                                          |
| 0100000000002104 |          | SystemUpdaterHostFs                                                  |                                                          |
| 0100000000002105 |          | WriteToStorage                                                       |                                                          |
| 0100000000002106 |          | [CalWriter](Factory%20Setup.md "wikilink") (CalWriterManu)           |                                                          |
| 0100000000002107 |          | SettingsManager                                                      |                                                          |
| 0100000000002109 |          | testBuildSystemIris                                                  |                                                          |
| 010000000000210A |          | SystemUpdater                                                        |                                                          |
| 010000000000210B |          | nvnflinger\_util                                                     |                                                          |
| 010000000000210C |          | ControllerFirmwareUpdater                                            |                                                          |
| 010000000000210D |          | testBuildSystemNintendoWare (Test)                                   |                                                          |
| 0100000000002110 |          | TestSaveDataCreator                                                  |                                                          |
| 0100000000002111 |          | C9LcdSpker                                                           |                                                          |
| 0100000000002114 |          | RankTurn                                                             |                                                          |
| 0100000000002116 |          | BleTestTool                                                          |                                                          |
| 010000000000211A |          | PreinstallAppWriter                                                  |                                                          |
| 010000000000211C |          | ControllerSerialFlashTool                                            |                                                          |
| 010000000000211D |          | ControllerFlashWriter                                                |                                                          |
| 0100000000002120 |          | ControllerTestApp                                                    |                                                          |
| 0100000000002121 |          | HidInspectionTool                                                    |                                                          |
| 0100000000002124 |          | BatteryCyclesEditor                                                  |                                                          |
| 0100000000002125 |          | UsbFirmwareUpdater                                                   |                                                          |
| 0100000000002126 |          | PalmaSerialCodeTool                                                  |                                                          |
| 0100000000002127 |          | renderdoccmd                                                         |                                                          |
| 0100000000002128 |          | HidInspectionToolProd                                                |                                                          |
| 010000000000212C |          | ExhibitionMenu                                                       |                                                          |
| 0100000000002130 |          | LuciaConverter                                                       |                                                          |
| 0100000000002133 |          | CalDumper                                                            |                                                          |
| 0100000000002134 |          | AnalogStickEvaluationTool                                            |                                                          |

## System Debug Modules

| Title-id         | Versions | Name             | Notes |
| ---------------- | -------- | ---------------- | ----- |
| 0100000000003002 |          | DummyProcess     |       |
| 0100000000003003 |          | DebugMonitor0    |       |
| 0100000000003004 |          | SystemHelloWorld |       |

## Target Tools

| Title-id         | Versions | Name                                                                 | Notes |
| ---------------- | -------- | -------------------------------------------------------------------- | ----- |
| 1000000000000001 |          | [SystemInitializer](Factory%20Setup.md "wikilink") (SystemInitializ) |       |
| 1000000000000004 |          | [CalWriter](Factory%20Setup.md "wikilink") (CalWriterManu)           |       |
| 1000000000000005 |          | DevMenuCommand                                                       |       |
| 1000000000000006 |          | SettingsManager                                                      |       |
| 1000000000000007 |          | ApplicationLauncer                                                   |       |
| 100000000000000B |          | SnapShotDumper                                                       |       |
| 100000000000000C |          | SystemUpdater                                                        |       |
| 100000000000000E |          | ControllerFirmwareUpdater                                            |       |

## Factory System Modules

| Title-id         | Versions | Name                                  | Notes                                                                                                                                               |
| ---------------- | -------- | ------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| 010000000000B120 |          | nvdbgsvc                              | Launched by maintenance mode [boot2.manuBoot](Boot2.md "wikilink"), but not present in retail or [factory firmware](Factory%20Setup.md "wikilink"). |
| 010000000000B14A |          | [manu](Manu%20Services.md "wikilink") | Installed in [factory firmware](Factory%20Setup.md "wikilink").                                                                                     |
| 010000000000B14B |          | ManuUsbLoopBack                       |                                                                                                                                                     |
| 010000000000B1B8 |          | DevFwdbgHbPackage                     |                                                                                                                                                     |
| 010000000000B1B9 |          | DevFwdbgUsbPackage                    |                                                                                                                                                     |
| 010000000000B1BA |          | ProdFwdbgPackage                      |                                                                                                                                                     |
| 010000000000B22A |          | scs                                   |                                                                                                                                                     |
| 010000000000B22B |          | ControllerFirmwareDebug               |                                                                                                                                                     |
| 010000000000B240 |          | htc                                   |                                                                                                                                                     |
| 010000000000C600 |          | BdkSample01                           |                                                                                                                                                     |
| 010000000000C601 |          | BdkSample02                           |                                                                                                                                                     |
| 010000000000C602 |          | BdkSample03                           |                                                                                                                                                     |
| 010000000000C603 |          | BdkSample04                           |                                                                                                                                                     |

## System Applications

<table>
<thead>
<tr class="header">
<th><p>Title-id</p></th>
<th><p>Versions</p></th>
<th><p>Name</p></th>
<th><p>Notes</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>01008BB00013C000</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="6.2.0.md" title="wikilink">v404750376</a> (6.2.0.40)</p></td>
<td><p><a href="Flog.md" title="wikilink">flog</a></p></td>
<td><p>NES emulator.</p></td>
</tr>
<tr class="even">
<td><p>0100069000078000</p></td>
<td><p>v0</p></td>
<td><p>RetailInteractiveDisplayMenu (DevQuestMenu)</p></td>
<td><p>This title can be launched by <a href="Qlaunch.md" title="wikilink">qlaunch</a>, but is not normally installed on retail systems.</p></td>
</tr>
<tr class="odd">
<td><p>010000B003486000</p></td>
<td></td>
<td><p>AudioUsbMicDebugTool</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>0100458001E04000</p></td>
<td></td>
<td><p>BcatTestApp01</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>0100F910020F8000</p></td>
<td></td>
<td><p>BcatTestApp02</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>0100B7D0020FC000</p></td>
<td></td>
<td><p>BcatTestApp03</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>0100132002100000</p></td>
<td></td>
<td><p>BcatTestApp04</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>0100935002116000</p></td>
<td></td>
<td><p>BcatTestApp05</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>0100DA4002130000</p></td>
<td></td>
<td><p>BcatTestApp06</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>0100B0F002104000</p></td>
<td></td>
<td><p>BcatTestApp07</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>010051E002132000</p></td>
<td></td>
<td><p>BcatTestApp08</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>01004CB0015C8000</p></td>
<td></td>
<td><p>BcatTestApp09</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>01009720015CA000</p></td>
<td></td>
<td><p>BcatTestApp10</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>01002F20015C6000</p></td>
<td></td>
<td><p>BcatTestApp11</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>0100204001F90000</p></td>
<td></td>
<td><p>BcatTestApp12</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>0100060001F92000</p></td>
<td></td>
<td><p>BcatTestApp13</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>0100C26001F94000</p></td>
<td></td>
<td><p>BcatTestApp14</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>0100462001F96000</p></td>
<td></td>
<td><p>BcatTestApp15</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>01005C6001F98000</p></td>
<td></td>
<td><p>BcatTestApp16</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>010070000E3C0000</p></td>
<td></td>
<td><p>EncounterUsr (LibraryAppletPreomiaUsr)</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>010086000E49C000</p></td>
<td></td>
<td><p>EncounterUsrDummy (LibraryAppletPreomiaUsrDummy)</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>0100810002D5A000</p></td>
<td></td>
<td><p>ShopMonitaringTool</p></td>
<td></td>
</tr>
</tbody>
</table>

## eShop Games / Applications

Note: Nintendo Switch game and application titles follow a higher
entropy TitleID scheme than previous generation consoles.  
Refer to the [Games List](Title%20list%20Games.md "wikilink") for more
information.

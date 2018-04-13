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
<td><p>FS</p></td>
</tr>
<tr class="even">
<td><p>0100000000000001</p></td>
<td><p>[bundled with kernel]</p></td>
<td><p>Loader</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000002</p></td>
<td><p>[bundled with kernel]</p></td>
<td><p>NCM</p></td>
</tr>
<tr class="even">
<td><p>0100000000000003</p></td>
<td><p>[bundled with kernel]</p></td>
<td><p>ProcessMana</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000004</p></td>
<td><p>[bundled with kernel]</p></td>
<td><p>sm</p></td>
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
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>usb</p></td>
</tr>
<tr class="even">
<td><p>0100000000000007</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>tma</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000008</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p><a href="Boot2.md" title="wikilink">boot2</a></p></td>
</tr>
<tr class="even">
<td><p>0100000000000009</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>settings</p></td>
</tr>
<tr class="odd">
<td><p>010000000000000A</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>bus</p></td>
</tr>
<tr class="even">
<td><p>010000000000000B</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>bluetooth</p></td>
</tr>
<tr class="odd">
<td><p>010000000000000C</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="3.0.2.md" title="wikilink">v201457684</a> (3.0.2.20)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>bcat</p></td>
</tr>
<tr class="even">
<td><p>010000000000000D</p></td>
<td></td>
<td><p>Launched by maintenance mode <a href="Boot2.md" title="wikilink">boot2.manuBoot</a>, but not present in retail or <a href="Factory Setup.md" title="wikilink">factory firmware</a>.</p></td>
</tr>
<tr class="odd">
<td><p>010000000000000E</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>friends</p></td>
</tr>
<tr class="even">
<td><p>010000000000000F</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131082</a> (0.0.2.10)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>nifm</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000010</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131132</a> (0.0.2.60)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>ptm</p></td>
</tr>
<tr class="even">
<td><p>0100000000000011</p></td>
<td></td>
<td><p>Launched by maintenance mode <a href="Boot2.md" title="wikilink">boot2.manuBoot</a>, but not present in retail or <a href="Factory Setup.md" title="wikilink">factory firmware</a>.</p></td>
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
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>bsdsockets</p></td>
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
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>hid</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000014</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>audio</p></td>
</tr>
<tr class="even">
<td><p>0100000000000015</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>LogManager.Prod</p></td>
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
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>wlan</p></td>
</tr>
<tr class="even">
<td><p>0100000000000017</p></td>
<td></td>
<td><p>Launched by maintenance mode <a href="Boot2.md" title="wikilink">boot2.manuBoot</a>, but not present in retail or <a href="Factory Setup.md" title="wikilink">factory firmware</a>.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000018</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>ldn</p></td>
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
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>nvservices</p></td>
</tr>
<tr class="odd">
<td><p>010000000000001A</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>pcv</p></td>
</tr>
<tr class="even">
<td><p>010000000000001B</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>ppc</p></td>
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
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>nvnflinger</p></td>
</tr>
<tr class="even">
<td><p>010000000000001D</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>pcie.withoutHb</p></td>
</tr>
<tr class="odd">
<td><p>010000000000001E</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="3.0.2.md" title="wikilink">v201457684</a> (3.0.2.20)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>account</p></td>
</tr>
<tr class="even">
<td><p>010000000000001F</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131132</a> (0.0.2.60)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>ns</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000020</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.2.0.md" title="wikilink">v131072</a> (0.0.2.0)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>nfc</p></td>
</tr>
<tr class="even">
<td><p>0100000000000021</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>psc</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000022</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>capsrv</p></td>
</tr>
<tr class="even">
<td><p>0100000000000023</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131132</a> (0.0.2.60)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>am</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000024</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>ssl</p></td>
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
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>nim</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000028</p></td>
<td><p>[bundled with kernel]</p></td>
<td><p>spl</p></td>
</tr>
<tr class="even">
<td><p>0100000000000029</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>lbl</p></td>
</tr>
<tr class="odd">
<td><p>010000000000002A</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>btm</p></td>
</tr>
<tr class="even">
<td><p>010000000000002B</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131132</a> (0.0.2.60)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>erpt</p></td>
</tr>
<tr class="odd">
<td><p>010000000000002D</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>vi</p></td>
</tr>
<tr class="even">
<td><p>010000000000002E</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131082</a> (0.0.2.10)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>pctl</p></td>
</tr>
<tr class="odd">
<td><p>010000000000002F</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>npns</p></td>
</tr>
<tr class="even">
<td><p>0100000000000030</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131132</a> (0.0.2.60)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p><a href="Eupld services.md" title="wikilink">eupld</a></p></td>
</tr>
<tr class="odd">
<td><p>0100000000000031</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>[1.0.0] arp<br />
[2.0.0+] glue</p></td>
</tr>
<tr class="even">
<td><p>0100000000000032</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>eclct</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000033</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>es</p></td>
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
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>fatal</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000035</p></td>
<td><p><a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>[4.0.0+] grc</p></td>
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
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p><a href="Creport.md" title="wikilink">creport</a></p></td>
</tr>
<tr class="odd">
<td><p>0100000000000037</p></td>
<td><p><a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>[3.0.0+] ro</p></td>
</tr>
<tr class="even">
<td><p>0100000000000038</p></td>
<td></td>
<td><p>This title is referenced by <a href="3.0.0.md" title="wikilink">3.0.0</a> boot2.prodBoot, but does not exist on retail systems.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000039</p></td>
<td><p><a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>[3.0.0+] sdb</p></td>
</tr>
<tr class="even">
<td><p>010000000000003A</p></td>
<td><p><a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>[4.0.0+] migration</p></td>
</tr>
<tr class="odd">
<td><p>010000000000003B</p></td>
<td></td>
<td><p>This title is launched by [5.0.0+] <a href="AM services#PrepareForJit.md##PrepareForJit" title="wikilink">AM_services#PrepareForJit</a>, but does not exist on retail systems currently.</p></td>
</tr>
<tr class="even">
<td><p>010000000000003C</p></td>
<td><p><a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>[4.0.0+] jpegdec</p></td>
</tr>
<tr class="odd">
<td><p>010000000000003D</p></td>
<td><p><a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>[4.0.0+] <a href="Safemode.md" title="wikilink">safemode</a></p></td>
</tr>
</tbody>
</table>

## System Debug Applets

Note: No 01000000000020XX titles exist on retail
systems.

| Title-id         | Versions | Description                                                                                            |
| ---------------- | -------- | ------------------------------------------------------------------------------------------------------ |
| 0100000000002000 |          | "BoardTest"                                                                                            |
| 0100000000002001 |          | "BoardWireless"                                                                                        |
| 0100000000002002 |          | C1LcdAndKey ("LcdAndKey") - LCD/Keyboard testing.                                                      |
| 0100000000002003 |          | C2UsbHpmic ("UsbAndHPMicTest") - USB and audio testing.                                                |
| 0100000000002004 |          | C3Aging ("Aging") - Graphics/Framerate testing.                                                        |
| 0100000000002005 |          | C4SixAxis ("6axisTest") - Sixaxis (controller peripheral) testing.                                     |
| 0100000000002006 |          | C5Wireless ("AssembledWireless") - Wireless testing.                                                   |
| 0100000000002007 |          | "FinalCheck"                                                                                           |
| 0100000000002044 |          | "HB-TBIntegrationTest"                                                                                 |
| 010000000000204E |          | A4BoardCalWriti ("BoardCalWriting") - Writes calibration data to NAND.                                 |
| 010000000000209B |          | "am.debug" - Used by [AM](AM%20services.md "wikilink").                                                |
| 010000000000209C |          | TestApplication ("TestApplicationLauncher") - Factory qlaunch replacement. Used to launch other tests. |
| 0100000000002071 |          | "snap\_shot\_dump" - Used by [NS](NS%20Services.md "wikilink").                                        |
| 01000000000020F0 |          | "devmenuapp\_installer" - Launched by [boot2](Boot2.md "wikilink").                                    |

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
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
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
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>Stores the message strings for Support Error Codes. There's &quot;/DatabaseInfo&quot; at FS root, then the rest is stored at &quot;/{first 4 error digits}/{last 4 error digits}/&quot;.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000802</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>Random textures?</p></td>
</tr>
<tr class="even">
<td><p>0100000000000803</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v196628</a> (0.0.3.20)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>Mounted as &quot;shareddata:/&quot;. Contains various browser data: emojis, OSS NROs, &quot;buildinfo/buildinfo.dat&quot;, ...</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000804</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>HTML resources: Open-source licenses(&quot;Intellectual Property Notices&quot;) and seizure warnings(&quot;Health &amp; Safety Information&quot;). The former is stored at FS &quot;/legallines.htdocs/&quot;<br />
while the latter is at &quot;/safe.htdocs/&quot;.</p></td>
</tr>
<tr class="even">
<td><p>0100000000000805</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)</p></td>
<td><p>Chinese and Korean dictionaries.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000806</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.2.md" title="wikilink">v201457684</a> (3.0.2.20)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>Bad words.</p></td>
</tr>
<tr class="even">
<td><p>0100000000000807</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v260</a> (0.0.0.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p><a href="Hotspot List.md" title="wikilink">Hotspot List</a></p></td>
</tr>
<tr class="odd">
<td><p>0100000000000808</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)</p></td>
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
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p><a href="System Version Title.md" title="wikilink">System Version Title</a></p></td>
</tr>
<tr class="odd">
<td><p>010000000000080A</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>Background and Character images for user avatars (RGBA format &amp; Yaz0 compression).</p></td>
</tr>
<tr class="even">
<td><p>010000000000080B</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>Tutorial images and strings. Used for the offline news by the News applet.</p></td>
</tr>
<tr class="odd">
<td><p>010000000000080C</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)</p></td>
<td><p>EULA. Also accessed by <a href="NS Services.md" title="wikilink">NS</a>.</p></td>
</tr>
<tr class="even">
<td><p>010000000000080D</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>URL blacklist.</p></td>
</tr>
<tr class="odd">
<td><p>010000000000080E</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>Geo Zoneinfo.</p></td>
</tr>
<tr class="even">
<td><p>0100000000000810</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>Extended font.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000811</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>Standard font.</p></td>
</tr>
<tr class="even">
<td><p>0100000000000812</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>Korean font.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000813</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>Taiwanese font.</p></td>
</tr>
<tr class="even">
<td><p>0100000000000814</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>Chinese font.</p></td>
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
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
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
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
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
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
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
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>Firmware Package B: SafeMode Firmware. While all data under RomFS differs from Normal, the only actual difference code-wise is that the FS and boot sysmodules .text differ.</p></td>
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
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>Firmware Package C: Normal Firmware (exFAT variant). Identical to 0100000000000819 with different package2. Requires a device ID to download from CDN.</p></td>
</tr>
<tr class="even">
<td><p>010000000000081C</p></td>
<td><p><a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="4.1.0.md" title="wikilink">v269484082</a> (4.1.0.50)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>Firmware Package D: SafeMode Firmware (exFAT variant). Identical to 010000000000081A with different package2.</p></td>
</tr>
<tr class="odd">
<td><p>010000000000081D</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
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
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>Icosa system config.</p></td>
</tr>
<tr class="even">
<td><p>0100000000000820</p></td>
<td><p><a href="2.0.0.md" title="wikilink">v260</a> (0.0.0.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>Copper system config.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000821</p></td>
<td><p><a href="2.0.0.md" title="wikilink">v260</a> (0.0.0.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>Hoag system config.</p></td>
</tr>
<tr class="even">
<td><p>0100000000000822</p></td>
<td><p><a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.2.md" title="wikilink">v201457684</a> (3.0.2.20)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>Firmware binaries for peripherals (hardware within Joy-Cons/etc).</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000823</p></td>
<td><p><a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>Contains version.dat and ac_*_nx files. All of the *_nx files stored under here are compressed with gzip.</p></td>
</tr>
<tr class="even">
<td><p>0100000000000824</p></td>
<td><p><a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>IcosaMariko system config.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000000825</p></td>
<td><p><a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>Application blacklist. Used by <a href="NS Services.md" title="wikilink">NS</a> for restricting application installation and updates.</p></td>
</tr>
<tr class="even">
<td><p>0100000000000826</p></td>
<td><p><a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>Rebootless system update version file.</p></td>
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
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;<a href="Qlaunch.md" title="wikilink">qlaunch</a>&quot; System applet (Launched by NS with TID loaded from system-config-title)</p></td>
</tr>
<tr class="even">
<td><p>0100000000001001</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;auth&quot;</p></td>
</tr>
<tr class="odd">
<td><p>0100000000001002</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;cabinet&quot;</p></td>
</tr>
<tr class="even">
<td><p>0100000000001003</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;controller&quot;</p></td>
</tr>
<tr class="odd">
<td><p>0100000000001004</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;dataErase&quot;</p></td>
</tr>
<tr class="even">
<td><p>0100000000001005</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;error&quot;</p></td>
</tr>
<tr class="odd">
<td><p>0100000000001006</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;netConnect&quot;</p></td>
</tr>
<tr class="even">
<td><p>0100000000001007</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;playerSelect&quot;</p></td>
</tr>
<tr class="odd">
<td><p>0100000000001008</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131132</a> (0.0.2.60)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;swkbd&quot;</p></td>
</tr>
<tr class="even">
<td><p>0100000000001009</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;miiEdit&quot;</p></td>
</tr>
<tr class="odd">
<td><p>010000000000100A</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131162</a> (0.0.2.90)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;LibAppletWeb&quot; <a href="Internet Browser.md" title="wikilink">WebApplet</a></p></td>
</tr>
<tr class="even">
<td><p>010000000000100B</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131162</a> (0.0.2.90)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;LibAppletShop&quot; <a href="Internet Browser.md" title="wikilink">ShopN</a> applet</p></td>
</tr>
<tr class="odd">
<td><p>010000000000100C</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;overlayDisp&quot; Overlay applet (TID is loaded by NS from system-config-title)</p></td>
</tr>
<tr class="even">
<td><p>010000000000100D</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;photoViewer&quot;</p></td>
</tr>
<tr class="odd">
<td><p>010000000000100F</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131162</a> (0.0.2.90)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;LibAppletOff&quot; <a href="Internet Browser.md" title="wikilink">Offline</a> web-applet</p></td>
</tr>
<tr class="even">
<td><p>0100000000001010</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131162</a> (0.0.2.90)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;LibAppletLns&quot; <a href="Internet Browser.md" title="wikilink">Whitelisted</a> applet (LoginApplet+ShareApplet+LobbyApplet)</p></td>
</tr>
<tr class="odd">
<td><p>0100000000001011</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="2.1.0.md" title="wikilink">v131162</a> (0.0.2.90)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="3.0.1.md" title="wikilink">v201392178</a> (3.0.1.50)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;LibAppletAuth&quot; <a href="Internet Browser.md" title="wikilink">WifiWebAuth</a> applet</p></td>
</tr>
<tr class="even">
<td><p>0100000000001012</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;starter&quot;</p></td>
</tr>
<tr class="odd">
<td><p>0100000000001013</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;myPage&quot;</p></td>
</tr>
<tr class="even">
<td><p>0100000000001015</p></td>
<td><p><a href="1.0.0.md" title="wikilink">v450</a> (0.0.0.450)<br />
<a href="2.0.0.md" title="wikilink">v65796</a> (0.0.1.260)<br />
<a href="3.0.0.md" title="wikilink">v201327002</a> (3.0.0.410)<br />
<a href="4.0.0.md" title="wikilink">v268435656</a> (4.0.0.200)<br />
<a href="5.0.0.md" title="wikilink">v335544750</a> (5.0.0.430)</p></td>
<td><p>&quot;maintenance&quot; Initial applet displayed when booting into <a href="Recovery Mode.md" title="wikilink">Recovery Mode</a>. This title is launched by <a href="NS Services.md" title="wikilink">NS</a> when a state flag is val1 indicating that this title should be launched instead of the above &quot;System applet&quot; title.</p></td>
</tr>
<tr class="odd">
<td><p>0100000000001016</p></td>
<td></td>
<td><p>TitleID used by <a href="NS Services.md" title="wikilink">NS</a> when a certain flag is non-zero, in multiple places including around code using string &quot;application_install&quot;. This title doesn't seem to exist for retail.</p></td>
</tr>
</tbody>
</table>

## Factory System Modules

| Title-id         | Versions | Description                                                                                                                                         |
| ---------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| 100000000000B120 |          | Launched by maintenance mode [boot2.manuBoot](Boot2.md "wikilink"), but not present in retail or [factory firmware](Factory%20Setup.md "wikilink"). |
| 100000000000B14A |          | [manu](Manu%20Services.md "wikilink") - installed in [factory firmware](Factory%20Setup.md "wikilink").                                             |

## Target Tools

| Title-id         | Versions | Description                                      |
| ---------------- | -------- | ------------------------------------------------ |
| 1000000000000001 |          | [SystemInitializ](Factory%20Setup.md "wikilink") |
| 1000000000000004 |          | [CalWriterManu](Factory%20Setup.md "wikilink")   |
| 1000000000000007 |          | "ApplicationLauncer"                             |

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

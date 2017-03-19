## Components

<table>
<thead>
<tr class="header">
<th><p>Function</p></th>
<th><p>Component</p></th>
<th><p>Notes</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DP-&gt;HDMI Converter</p></td>
<td><p>MegaChips STDP2550 &quot;Mystique&quot;</p></td>
<td><p>2Mb flash contains firmware</p></td>
</tr>
<tr class="even">
<td><p>USB Hub</p></td>
<td><p>VIA Labs VL210 USB 3.0 Hub Controller</p></td>
<td><p>512Kb flash is configuration storage</p></td>
</tr>
<tr class="odd">
<td><p>USB Device</p></td>
<td><p>Cortex-M0 based (STM32F0-ish)<br />
&quot;32P048&quot;</p></td>
<td><p>SWD clearly labelled and enabled<br />
Provides control of the Mystique<br />
Dumps (fw-1.0.0):<br />
<a href=":File:Dock.stm.08000000-08008000.bin.md" title="wikilink">flash</a><br />
<a href=":File:Dock.stm.1fffc400-1ffffc00.bin.md" title="wikilink">sysmem</a><br />
<a href=":File:Dock.stm.20000000-20001800.bin.md" title="wikilink">SRAM</a><br />
<a href="http://www.st.com/content/ccc/resource/technical/document/reference_manual/c2/f8/8a/f2/18/e6/43/96/DM00031936.pdf/files/DM00031936.pdf/jcr:content/translations/en.DM00031936.pdf">Relevant manual</a></p></td>
</tr>
<tr class="even">
<td><p>Flash</p></td>
<td><p>Macronix MX25L512E 512Kb CMOS</p></td>
<td><p><a href=":File:Dock.512K.bin.md" title="wikilink">dump (fw-1.0.0)</a></p></td>
</tr>
<tr class="odd">
<td><p>Macronix MX25V2006E 2Mb CMOS</p></td>
<td><p><a href=":File:Dock.2M.bin.md" title="wikilink">dump (fw-1.0.0)</a></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Unknown</p></td>
<td><p>M92T17 623382</p></td>
<td><p>Similar part on the console mainboard</p></td>
</tr>
<tr class="odd">
<td><p>M92T55 633416</p></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

## Other Resources

1.  [ifixit
    teardown](https://www.ifixit.com/Teardown/Nintendo+Switch+Teardown/78263)
2.  [dekuNukem's
    RE](https://github.com/dekuNukem/Nintendo_Switch_Reverse_Engineering)

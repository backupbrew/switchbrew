All elements in the Switch's boot chain up to the kernel have the
ability to issue a system panic.

Panics are handled by writing a panic code in the **PMC\_SCRATCH200**
register and requesting a reboot by programming a dedicated hardware
watchdog (**WDT4**). The bootloaders and the Secure Monitor are able to
do this right away, but the kernel must invoke the [Panic
SMC](SMC#Panic.md##Panic "wikilink").

When the system reboots, the [encrypted
bootloader](Package1#Section%201.md##Section_1 "wikilink") checks if the
reset was requested by the watchdog (**PMC\_RST\_STATUS** register is
set to 0x01) and parses the panic code stored in **PMC\_SCRATCH200**.

If a panic did occur, the Switch will paint the main screen with a solid
color and halt execution.

# Structure

| Bits  | Field       |
| ----- | ----------- |
| 31-28 | Blue value  |
| 27-24 | Green value |
| 23-20 | Red value   |
| 19-0  | Description |

The blue, green and red values are nibbles which represent the color
that will fill the panic screen. Each nibble is duplicated to form a
full byte before writing the final color to the display's MMIO.

## Panic colors

Different colors are used to represent panic events coming from
different execution levels within the system.

<table>
<thead>
<tr class="header">
<th><p>Color</p></th>
<th><p>Value</p></th>
<th><p>Level</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><div style="width: 60px; height: 20px; background:#000000;">
</div></td>
<td><p>0x000000</p></td>
<td><p>Default</p></td>
</tr>
<tr class="even">
<td><div style="width: 60px; height: 20px; background:#FFAA00;">
</div></td>
<td><p>0xFFAA00</p></td>
<td><p>GPU</p></td>
</tr>
<tr class="odd">
<td><div style="width: 60px; height: 20px; background:#0000FF;">
</div></td>
<td><p>0x0000FF</p></td>
<td><p>Kernel</p></td>
</tr>
<tr class="even">
<td><div style="width: 60px; height: 20px; background:#00FFFF;">
</div></td>
<td><p>0x00FFFF</p></td>
<td><p>Secure Monitor (general errors)</p></td>
</tr>
<tr class="odd">
<td><div style="width: 60px; height: 20px; background:#00AAFF;">
</div></td>
<td><p>0x00AAFF</p></td>
<td><p>Secure Monitor (deep sleep) [1.0.0+]</p></td>
</tr>
<tr class="even">
<td><div style="width: 60px; height: 20px; background:#FF77FF;">
</div></td>
<td><p>0xFF77FF</p></td>
<td><p>Secure Monitor (deep sleep) [4.0.0+]</p></td>
</tr>
<tr class="odd">
<td><div style="width: 60px; height: 20px; background:#AA00FF;">
</div></td>
<td><p>0xAA00FF</p></td>
<td><p>Bootloader (general errors)</p></td>
</tr>
<tr class="even">
<td><div style="width: 60px; height: 20px; background:#FFFFAA;">
</div></td>
<td><p>0xFFFFAA</p></td>
<td><p>Bootloader (wrong bootloader)</p></td>
</tr>
</tbody>
</table>

## Panic codes

While any combination of panic colors and codes is possible, several
panic codes are specifically tied to a certain color.

<table>
<thead>
<tr class="header">
<th><p>Value</p></th>
<th><p>Color</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x0</p></td>
<td><p>Any</p></td>
<td><p>No information</p></td>
</tr>
<tr class="even">
<td><p>0x1</p></td>
<td><div style="width: 60px; height: 20px; background:#0000FF;">
</div></td>
<td><p>Package2 signature verification failed</p></td>
</tr>
<tr class="odd">
<td><p>0x2</p></td>
<td><div style="width: 60px; height: 20px; background:#0000FF;">
</div></td>
<td><p>Package2 meta verification failed</p></td>
</tr>
<tr class="even">
<td><p>0x3</p></td>
<td><div style="width: 60px; height: 20px; background:#0000FF;">
</div></td>
<td><p>Package2 version check failed</p></td>
</tr>
<tr class="odd">
<td><p>0x4</p></td>
<td><div style="width: 60px; height: 20px; background:#0000FF;">
</div></td>
<td><p>Package2 payload verification failed</p></td>
</tr>
<tr class="even">
<td><p>0x5</p></td>
<td><div style="width: 60px; height: 20px; background:#00FFFF;">
</div></td>
<td><p>Unknown SMC</p></td>
</tr>
<tr class="odd">
<td><p>0x6</p></td>
<td><div style="width: 60px; height: 20px; background:#00FFFF;">
</div></td>
<td><p>Unknown Abort</p></td>
</tr>
<tr class="even">
<td><p>0x7</p></td>
<td><div style="width: 60px; height: 20px; background:#FF77FF;">
</div></td>
<td><p>Invalid CPU context</p></td>
</tr>
<tr class="odd">
<td><p>0x8</p></td>
<td><div style="width: 60px; height: 20px; background:#FF77FF;">
</div></td>
<td><p>Invalid SE state</p></td>
</tr>
<tr class="even">
<td><p>0x9</p></td>
<td><div style="width: 60px; height: 20px; background:#FF77FF;">
</div></td>
<td><p>CPU is already awake [2.0.0+]</p></td>
</tr>
<tr class="odd">
<td><p>0x10</p></td>
<td><p>Any</p></td>
<td><p>Unknown exception</p></td>
</tr>
<tr class="even">
<td><p>0x20</p></td>
<td><div style="width: 60px; height: 20px; background:#000000;">
</div></td>
<td><p>Rebooting into SafeMode</p></td>
</tr>
<tr class="odd">
<td><p>0x21</p></td>
<td><div style="width: 60px; height: 20px; background:#000000;">
</div></td>
<td><p>Rebooting for anti-downgrade</p></td>
</tr>
<tr class="even">
<td><p>0x30</p></td>
<td><div style="width: 60px; height: 20px; background:#AA00FF;">
</div></td>
<td><p>General bootloader error</p></td>
</tr>
<tr class="odd">
<td><p>0x31</p></td>
<td><div style="width: 60px; height: 20px; background:#AA00FF;">
</div></td>
<td><p>Invalid DRAM ID</p></td>
</tr>
<tr class="even">
<td><p>0x32</p></td>
<td><div style="width: 60px; height: 20px; background:#AA00FF;">
</div></td>
<td><p>Invalid size</p></td>
</tr>
<tr class="odd">
<td><p>0x33</p></td>
<td><div style="width: 60px; height: 20px; background:#AA00FF;">
</div></td>
<td><p>Invalid argument</p></td>
</tr>
<tr class="even">
<td><p>0x34</p></td>
<td><div style="width: 60px; height: 20px; background:#AA00FF;">
</div></td>
<td><p>Bad GPT</p></td>
</tr>
<tr class="odd">
<td><p>0x35</p></td>
<td><div style="width: 60px; height: 20px; background:#AA00FF;">
</div></td>
<td><p>Failed to boot SafeMode</p></td>
</tr>
<tr class="even">
<td><p>0x36</p></td>
<td><div style="width: 60px; height: 20px; background:#AA00FF;">
</div></td>
<td><p>Activity Monitor fired [4.0.0+]</p></td>
</tr>
<tr class="odd">
<td><p>0x40</p></td>
<td><div style="width: 60px; height: 20px; background:#0000FF;">
</div></td>
<td><p>Show error called (kernel panic)</p></td>
</tr>
</tbody>
</table>

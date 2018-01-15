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
<td><p>Secure Monitor (deep sleep)</p></td>
</tr>
<tr class="even">
<td><div style="width: 60px; height: 20px; background:#AA00FF;">
</div></td>
<td><p>0xAA00FF</p></td>
<td><p>Bootloader (general errors)</p></td>
</tr>
<tr class="odd">
<td><div style="width: 60px; height: 20px; background:#FFFFAA;">
</div></td>
<td><p>0xFFFFAA</p></td>
<td><p>Bootloader (wrong bootloader)</p></td>
</tr>
</tbody>
</table>

## Panic codes

While any combination of panic colors and codes is possible, several
panic codes are specifically tied to a certain execution level.

| Value | Level            | Description                            |
| ----- | ---------------- | -------------------------------------- |
| 0x0   | Any              | No information                         |
| 0x1   | Kernel           | Package2 signature verification failed |
| 0x2   | Kernel           | Package2 meta verification failed      |
| 0x3   | Kernel           | Package2 version check failed          |
| 0x4   | Kernel           | Package2 payload verification failed   |
| 0x5   | Secure Monitor   | Unknown SMC                            |
| 0x6   | Secure Monitor   | Unknown Abort                          |
| 0x7   | Secure Monitor   | Invalid CPU context                    |
| 0x8   | Secure Monitor   | Invalid SE state                       |
| 0x9   | Secure Monitor   | CPU is already awake                   |
| 0x10  | Any              | Unknown exception                      |
| 0x20  | Bootloader       | Rebooting into SafeMode                |
| 0x21  | Bootloader       | Rebooting for anti-downgrade           |
| 0x30  | Bootloader       | General bootloader error               |
| 0x31  | Bootloader       | Invalid DRAM ID                        |
| 0x32  | Bootloader       | Invalid size                           |
| 0x33  | Bootloader       | Invalid argument                       |
| 0x34  | Bootloader       | Bad GPT                                |
| 0x35  | Bootloader       | Failed to boot SafeMode                |
| 0x36  | Bootloader-color | \[4.0.0+\]                             |
| 0x40  | Kernel           | Show error called (kernel panic)       |

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
| 31-28 | Red value   |
| 27-24 | Green value |
| 23-20 | Blue value  |
| 19-0  | Description |

The red, green and blue values are nibbles which represent the color
that will fill the panic screen. Each nibble is duplicated to form a
full byte before writing the final color to the display's MMIO.

## Panic colors

| Color    | Value                         |
| -------- | ----------------------------- |
| 0xFF0000 | Kernel                        |
| 0xFFFF00 | Secure Monitor                |
| 0xFFAA00 | Hardware?                     |
| 0xFF00AA | Bootloader (general errors)   |
| 0xAAFFFF | Bootloader (wrong bootloader) |

## Panic codes

| Value | Description                            |
| ----- | -------------------------------------- |
| 0x0   | No information                         |
| 0x1   | Package2 signature verification failed |
| 0x2   | Package2 meta verification failed      |
| 0x3   | Package2 version check failed          |
| 0x4   | Package2 payload verification failed   |
| 0x5   | Unknown SMC                            |
| 0x6   | Unknown Abort                          |
| 0x7   |                                        |
| 0x8   |                                        |
| 0x9   | CPU is already awake                   |
| 0x10  | Unknown exception                      |
| 0x20  | Rebooting into SafeMode                |
| 0x21  | Rebooting for anti-downgrade           |
| 0x30  | General bootloader error               |
| 0x31  | Invalid DRAM ID                        |
| 0x32  | Invalid size                           |
| 0x33  | Invalid argument                       |
| 0x34  | Bad GPT                                |
| 0x35  | Failed to boot SafeMode                |
| 0x40  | Show error called (kernel panic)       |

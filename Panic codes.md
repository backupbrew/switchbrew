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

Different colors are used to represent panic events coming from
different execution levels within the system.

| Color    | Level                           |
| -------- | ------------------------------- |
| 0xFF0000 | Kernel                          |
| 0xFFFF00 | Secure Monitor (general errors) |
| 0xFFAA00 | Secure Monitor (deep sleep)     |
| 0xFF00AA | Bootloader (general errors)     |
| 0xAAFFFF | Bootloader (wrong bootloader)   |

## Panic codes

While any combination of panic colors and codes is possible, several
panic codes are specifically tied to a certain execution level.

| Value | Level          | Description                            |
| ----- | -------------- | -------------------------------------- |
| 0x0   | Any            | No information                         |
| 0x1   | Kernel         | Package2 signature verification failed |
| 0x2   | Kernel         | Package2 meta verification failed      |
| 0x3   | Kernel         | Package2 version check failed          |
| 0x4   | Kernel         | Package2 payload verification failed   |
| 0x5   | Secure Monitor | Unknown SMC                            |
| 0x6   | Secure Monitor | Unknown Abort                          |
| 0x7   | Secure Monitor |                                        |
| 0x8   | Secure Monitor |                                        |
| 0x9   | Secure Monitor | CPU is already awake                   |
| 0x10  | Any            | Unknown exception                      |
| 0x20  | Bootloader     | Rebooting into SafeMode                |
| 0x21  | Bootloader     | Rebooting for anti-downgrade           |
| 0x30  | Bootloader     | General bootloader error               |
| 0x31  | Bootloader     | Invalid DRAM ID                        |
| 0x32  | Bootloader     | Invalid size                           |
| 0x33  | Bootloader     | Invalid argument                       |
| 0x34  | Bootloader     | Bad GPT                                |
| 0x35  | Bootloader     | Failed to boot SafeMode                |
| 0x40  | Kernel         | Show error called (kernel panic)       |

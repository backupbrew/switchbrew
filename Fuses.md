The Nintendo Switch makes use of Tegra's efuse driver for a number of
operations. This driver is mapped to physical address 0x7000F800 with a
total size of 0x400 bytes and exposes several registers for fuse
programming and other miscellaneous functions.

## Registers

Below is a list of fuse driver registers used by the Switch's
bootloaders.

| Name                                                                   | Address    | Width |
| ---------------------------------------------------------------------- | ---------- | ----- |
| [FUSE\_CTRL](#FUSE_CTRL "wikilink")                                    | 0x7000F800 | 0x04  |
| [FUSE\_REG\_ADDR](#FUSE_REG_ADDR "wikilink")                           | 0x7000F804 | 0x04  |
| [FUSE\_REG\_READ](#FUSE_REG_READ "wikilink")                           | 0x7000F808 | 0x04  |
| [FUSE\_REG\_WRITE](#FUSE_REG_WRITE "wikilink")                         | 0x7000F80C | 0x04  |
| [FUSE\_TIME\_PGM2](#FUSE_TIME_PGM2 "wikilink")                         | 0x7000F81C | 0x04  |
| [FUSE\_DIS\_PGM](#FUSE_DIS_PGM "wikilink")                             | 0x7000F82C | 0x04  |
| [FUSE\_WRITE\_ACCESS](#FUSE_WRITE_ACCESS "wikilink")                   | 0x7000F830 | 0x04  |
| [FUSE\_SKU\_INFO](#FUSE_SKU_INFO "wikilink")                           | 0x7000F910 | 0x04  |
| [FUSE\_SPEEDO\_1\_CALIB\_0](#FUSE_SPEEDO_1_CALIB_0 "wikilink")         | 0x7000F938 | 0x04  |
| FUSE\_GCPLEX\_CONFIG\_FUSE\_0                                          | 0x7000F9C8 | 0x04  |
| FUSE\_GCPLEX\_CONFIG\_FUSE\_1                                          | 0x7000F9CC | 0x04  |
| FUSE\_GCPLEX\_CONFIG\_FUSE\_2                                          | 0x7000F9D0 | 0x04  |
| FUSE\_GCPLEX\_CONFIG\_FUSE\_3                                          | 0x7000F9D4 | 0x04  |
| [FUSE\_GCPLEX\_CONFIG\_FUSE\_4](#FUSE_GCPLEX_CONFIG_FUSE_4 "wikilink") | 0x7000F9D8 | 0x04  |
| FUSE\_GCPLEX\_CONFIG\_FUSE\_5                                          | 0x7000F9DC | 0x04  |
| [FUSE\_BURNT\_FUSE\_COUNT\_0](#FUSE_BURNT_FUSE_COUNT_0 "wikilink")     | 0x7000F9E0 | 0x04  |
| [FUSE\_BURNT\_FUSE\_COUNT\_1](#FUSE_BURNT_FUSE_COUNT_1 "wikilink")     | 0x7000F9E4 | 0x04  |
| [FUSE\_MASTER\_KEY\_VER](#FUSE_MASTER_KEY_VER "wikilink")              | 0x7000FB94 | 0x04  |
|                                                                        |            |       |

### FUSE\_CTRL

| Bits | Description                                                     |
| ---- | --------------------------------------------------------------- |
| 0-1  | Fuse command (1 = FUSE\_READ; 2 = FUSE\_WRITE; 3 = FUSE\_SENSE) |
| 26   | Fuse power down mode flag (FUSE\_CTRL\_PD)                      |
|      |                                                                 |

Before fuse reading/writing the power down mode must be disabled.

### FUSE\_REG\_ADDR

This register takes the address of the fuse to be read/written/sensed.

### FUSE\_REG\_READ

This register receives the value read from the fuse.

### FUSE\_REG\_WRITE

This register takes the value to be written to the fuse.

### FUSE\_TIME\_PGM2

This register takes the fuse programming pulse (0xC0 == 19200 kHz).

### FUSE\_DIS\_PGM

If set to 0x01, this register disables fuse programming.

### FUSE\_WRITE\_ACCESS

If set to 0x01, this register disables software writes to the fuse
registers.

### FUSE\_SKU\_INFO

Stores the SKU ID (must be 0x83).

### FUSE\_SPEEDO\_1\_CALIB\_0

Seems to store the bootrom patch version.

### FUSE\_GCPLEX\_CONFIG\_FUSE\_4

| Bits | Description                               |
| ---- | ----------------------------------------- |
| 0-1  | Unit type (3 = debug; 0 = retail)         |
| 2    | Unknown config (must be 1 on retail)      |
| 8    | Unknown config mask (must be 0 on retail) |
| 9    | Unit type mask (0 = debug; 1 = retail)    |
|      |                                           |

This stores some device configuration parameters.

### FUSE\_MASTER\_KEY\_VER

Must be non-zero on retail units, otherwise the first bootloader panics.
On debug units it can be zero, which tells the bootloader to choose from
two debug master key seeds. If set to non-zero on a debug unit, it tells
the bootloader to choose from two retail master key seeds (only the last
one matches the retail master key seed).

### FUSE\_BURNT\_FUSE\_COUNT\_0

This register returns the value programmed into offset 0x3A of the fuse
array.

### FUSE\_BURNT\_FUSE\_COUNT\_1

This register returns the value programmed into offset 0x3C of the fuse
array.

## eFuses

The actual hardware fuses can be programmed through the fuse driver
after enabling fuse programming.

Below is a list of common fuse offsets used by Tegra devices (and
applicable to the Switch). Note that offsets are relative to the start
of the fuse array and a single fuse write operation always writes the
same word at both (fuse\_offset + 0) and (fuse\_offset + 1).

| Name                                      | Offset | Bits |
| ----------------------------------------- | ------ | ---- |
| jtag\_disable                             | 0x00   | 1    |
| odm\_production\_mode                     | 0x00   | 1    |
| odm\_lock                                 | 0x00   | 4    |
| public\_key                               | 0x0C   | 256  |
| secure\_boot\_key                         | 0x22   | 128  |
| device\_key                               | 0x2A   | 32   |
| sec\_boot\_dev\_cfg                       | 0x2C   | 16   |
| sec\_boot\_dev\_sel                       | 0x2C   | 3    |
| sw\_reserved                              | 0x2E   | 12   |
| ignore\_dev\_sel\_straps                  | 0x2E   | 1    |
| [odm\_reserved](#odm_reserved "wikilink") | 0x2E   | 256  |
| pkc\_disable                              | 0x52   | 1    |
|                                           |        |      |

### odm\_reserved

The first bootloader only burns fuses in this region. Both fuse offsets
0x3A (odm\_reserved + 0x0C) and 0x3C (odm\_reserved + 0x0E) are used for
anti-downgrade control.

## Anti-downgrade

The first bootloader verifies
[FUSE\_BURNT\_FUSE\_COUNT\_1](#FUSE_BURNT_FUSE_COUNT_1 "wikilink") to
prevent downgrading. How many fuses are expected to be burnt depends the
device's unit type as
below.

| System version | Expected number of burnt fuses (retail) | Expected number of burnt fuses (non-retail) |
| -------------- | --------------------------------------- | ------------------------------------------- |
| 1.0.0          | 1                                       | 0                                           |
| 2.0.0-2.3.0    | 2                                       | 0                                           |
| 3.0.0          | 3                                       | 1                                           |
| 3.0.1          | 4                                       | 1                                           |

If too many fuses are burnt the bootloader will panic immediately.

If too few are burnt, the bootloader will enable fuse programming and
write the expected value to fuse offsets 0x3A and 0x3C. Afterwards, fuse
programming is disabled and a magic value (0x21 == TEGRA210) is written
to an unknown PMC register (0x7000EC40). Finally, the watchdog timer is
initialized and programmed to force a reset.

On a subsequent boot, after the anti-downgrade fuses are checked again,
PMC\_RST\_STATUS (0x7000E5B4) is checked and if set to 0x01 (watchdog
reset) the unknown PMC register (0x7000EC40) will be checked for the
magic value 0x21. PMC\_RST\_STATUS will only be set back to 0 (power on
reset) if the fuse count matches the new expected value, otherwise the
system will panic.

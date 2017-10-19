The Nintendo Switch makes use of Tegra's fuse driver for a number of
operations. This driver is mapped to physical address 0x7000F800 with a
total size of 0x400 bytes and exposes several registers for fuse
programming.

Registers from 0x7000F800 to 0x7000F800 + 0xFF can be used to directly
program the hardware fuse array, while registers from 0x7000F800 + 0x100
(FUSE\_CHIP\_REG\_START\_OFFSET) to 0x7000F800 + 0x3FC
(FUSE\_CHIP\_REG\_END\_OFFSET) represent cached values read from certain
fuses.

## Registers

Below is a list of fuse driver registers used by the Switch's
bootloaders.

### Driver registers

| Name                                                 | Address    |
| ---------------------------------------------------- | ---------- |
| [FUSE\_CTRL](#FUSE_CTRL "wikilink")                  | 0x7000F800 |
| [FUSE\_REG\_ADDR](#FUSE_REG_ADDR "wikilink")         | 0x7000F804 |
| [FUSE\_REG\_READ](#FUSE_REG_READ "wikilink")         | 0x7000F808 |
| [FUSE\_REG\_WRITE](#FUSE_REG_WRITE "wikilink")       | 0x7000F80C |
| FUSE\_TIME\_RD1                                      | 0x7000F810 |
| FUSE\_TIME\_RD2                                      | 0x7000F814 |
| FUSE\_TIME\_PGM1                                     | 0x7000F818 |
| [FUSE\_TIME\_PGM2](#FUSE_TIME_PGM2 "wikilink")       | 0x7000F81C |
| FUSE\_PRIV2INTFC                                     | 0x7000F820 |
| FUSE\_FUSEBYPASS                                     | 0x7000F824 |
| FUSE\_PRIVATEKEYDISABLE                              | 0x7000F828 |
| [FUSE\_DIS\_PGM](#FUSE_DIS_PGM "wikilink")           | 0x7000F82C |
| [FUSE\_WRITE\_ACCESS](#FUSE_WRITE_ACCESS "wikilink") | 0x7000F830 |
| FUSE\_PWR\_GOOD\_SW                                  | 0x7000F834 |
|                                                      |            |

#### FUSE\_CTRL

| Bits | Description                                                     |
| ---- | --------------------------------------------------------------- |
| 0-1  | Fuse command (1 = FUSE\_READ; 2 = FUSE\_WRITE; 3 = FUSE\_SENSE) |
| 26   | Fuse power down mode flag (FUSE\_CTRL\_PD)                      |
|      |                                                                 |

Before fuse reading/writing the power down mode must be disabled.
FUSE\_SENSE mode flushes programmed values into the [cache
registers](Fuses#Cache%20registers.md##Cache_registers "wikilink").

#### FUSE\_REG\_ADDR

This register takes the address of the fuse to be read/written/sensed.

#### FUSE\_REG\_READ

This register receives the value read from the fuse.

#### FUSE\_REG\_WRITE

This register takes the value to be written to the fuse.

#### FUSE\_TIME\_PGM2

This register takes the fuse programming pulse (0xC0 == 19200 kHz).

#### FUSE\_DIS\_PGM

If set to 0x01, this register disables fuse programming.

#### FUSE\_WRITE\_ACCESS

If set to 0x01, this register disables software writes to the fuse
driver registers.

### Cache registers

| Name                                                   | Address    |
| ------------------------------------------------------ | ---------- |
| [FUSE\_SKU\_INFO](#FUSE_SKU_INFO "wikilink")           | 0x7000F910 |
| FUSE\_CPU\_SPEEDO\_0                                   | 0x7000F914 |
| FUSE\_CPU\_IDDQ                                        | 0x7000F918 |
| FUSE\_FT\_REV                                          | 0x7000F928 |
| FUSE\_CPU\_SPEEDO\_1                                   | 0x7000F92C |
| FUSE\_CPU\_SPEEDO\_2                                   | 0x7000F930 |
| FUSE\_SOC\_SPEEDO\_0                                   | 0x7000F934 |
| [FUSE\_SOC\_SPEEDO\_1](#FUSE_SOC_SPEEDO_1 "wikilink")  | 0x7000F938 |
| FUSE\_SOC\_SPEEDO\_2                                   | 0x7000F93C |
| FUSE\_SOC\_IDDQ                                        | 0x7000F940 |
| [FUSE\_FA](#FUSE_FA "wikilink")                        | 0x7000F948 |
| [FUSE\_PUBLIC\_KEY0](#FUSE_PUBLIC_KEY "wikilink")      | 0x7000F964 |
| [FUSE\_PUBLIC\_KEY1](#FUSE_PUBLIC_KEY "wikilink")      | 0x7000F968 |
| [FUSE\_PUBLIC\_KEY2](#FUSE_PUBLIC_KEY "wikilink")      | 0x7000F96C |
| [FUSE\_PUBLIC\_KEY3](#FUSE_PUBLIC_KEY "wikilink")      | 0x7000F970 |
| [FUSE\_PUBLIC\_KEY4](#FUSE_PUBLIC_KEY "wikilink")      | 0x7000F974 |
| [FUSE\_PUBLIC\_KEY5](#FUSE_PUBLIC_KEY "wikilink")      | 0x7000F978 |
| [FUSE\_PUBLIC\_KEY6](#FUSE_PUBLIC_KEY "wikilink")      | 0x7000F97C |
| [FUSE\_PUBLIC\_KEY7](#FUSE_PUBLIC_KEY "wikilink")      | 0x7000F980 |
| FUSE\_TSENSOR\_1                                       | 0x7000F984 |
| FUSE\_TSENSOR\_2                                       | 0x7000F988 |
| FUSE\_CP\_REV                                          | 0x7000F990 |
| FUSE\_TSENSOR\_0                                       | 0x7000F998 |
| FUSE\_FIRST\_BOOTROM\_PATCH\_SIZE\_REG                 | 0x7000F99C |
| [FUSE\_PRIVATE\_KEY0](#FUSE_PRIVATE_KEY "wikilink")    | 0x7000F9A4 |
| [FUSE\_PRIVATE\_KEY1](#FUSE_PRIVATE_KEY "wikilink")    | 0x7000F9A8 |
| [FUSE\_PRIVATE\_KEY2](#FUSE_PRIVATE_KEY "wikilink")    | 0x7000F9AC |
| [FUSE\_PRIVATE\_KEY3](#FUSE_PRIVATE_KEY "wikilink")    | 0x7000F9B0 |
| [FUSE\_PRIVATE\_KEY4](#FUSE_PRIVATE_KEY "wikilink")    | 0x7000F9B4 |
| FUSE\_VP8\_ENABLE                                      | 0x7000F9C4 |
| FUSE\_RESERVED\_ODM0                                   | 0x7000F9C8 |
| FUSE\_RESERVED\_ODM1                                   | 0x7000F9CC |
| FUSE\_RESERVED\_ODM2                                   | 0x7000F9D0 |
| FUSE\_RESERVED\_ODM3                                   | 0x7000F9D4 |
| [FUSE\_RESERVED\_ODM4](#FUSE_RESERVED_ODM4 "wikilink") | 0x7000F9D8 |
| FUSE\_RESERVED\_ODM5                                   | 0x7000F9DC |
| [FUSE\_RESERVED\_ODM6](#FUSE_RESERVED_ODM6 "wikilink") | 0x7000F9E0 |
| [FUSE\_RESERVED\_ODM7](#FUSE_RESERVED_ODM7 "wikilink") | 0x7000F9E4 |
| FUSE\_SKU\_USB\_CALIB                                  | 0x7000F9F0 |
| FUSE\_SKU\_DIRECT\_CONFIG                              | 0x7000F9F4 |
| FUSE\_VENDOR\_CODE                                     | 0x7000FA00 |
| FUSE\_FAB\_CODE                                        | 0x7000FA04 |
| FUSE\_LOT\_CODE\_0                                     | 0x7000FA08 |
| FUSE\_LOT\_CODE\_1                                     | 0x7000FA0C |
| FUSE\_WAFER\_ID                                        | 0x7000FA10 |
| FUSE\_X\_COORDINATE                                    | 0x7000FA14 |
| FUSE\_Y\_COORDINATE                                    | 0x7000FA18 |
| FUSE\_GPU\_IDDQ                                        | 0x7000FA28 |
| FUSE\_TSENSOR\_3                                       | 0x7000FA2C |
| FUSE\_OPT\_SUBREVISION                                 | 0x7000FA48 |
| FUSE\_TSENSOR\_4                                       | 0x7000FA54 |
| FUSE\_TSENSOR\_5                                       | 0x7000FA58 |
| FUSE\_TSENSOR\_6                                       | 0x7000FA5C |
| FUSE\_TSENSOR\_7                                       | 0x7000FA60 |
| FUSE\_OPT\_PRIV\_SEC\_DIS                              | 0x7000FA64 |
| FUSE\_TSENSOR\_COMMON                                  | 0x7000FA80 |
| FUSE\_TSENSOR\_8                                       | 0x7000FAD4 |
| FUSE\_RESERVED\_CALIB                                  | 0x7000FB04 |
| FUSE\_TSENSOR\_9                                       | 0x7000FB1C |
| FUSE\_USB\_CALIB\_EXT                                  | 0x7000FB50 |
| FUSE\_SPARE\_BIT\_0                                    | 0x7000FB80 |
| FUSE\_SPARE\_BIT\_1                                    | 0x7000FB84 |
| FUSE\_SPARE\_BIT\_2                                    | 0x7000FB88 |
| FUSE\_SPARE\_BIT\_3                                    | 0x7000FB8C |
| FUSE\_SPARE\_BIT\_4                                    | 0x7000FB90 |
| [FUSE\_SPARE\_BIT\_5](#FUSE_SPARE_BIT_5 "wikilink")    | 0x7000FB94 |
| FUSE\_SPARE\_BIT\_6                                    | 0x7000FB98 |
| FUSE\_SPARE\_BIT\_7                                    | 0x7000FB9C |
| FUSE\_SPARE\_BIT\_8                                    | 0x7000FBA0 |
| FUSE\_SPARE\_BIT\_9                                    | 0x7000FBA4 |
| FUSE\_SPARE\_BIT\_10                                   | 0x7000FBA8 |
| FUSE\_SPARE\_BIT\_11                                   | 0x7000FBAC |
| FUSE\_SPARE\_BIT\_12                                   | 0x7000FBB0 |
| FUSE\_SPARE\_BIT\_13                                   | 0x7000FBB4 |
| FUSE\_SPARE\_BIT\_14                                   | 0x7000FBB8 |
| FUSE\_SPARE\_BIT\_15                                   | 0x7000FBBC |
| FUSE\_SPARE\_BIT\_16                                   | 0x7000FBC0 |
| FUSE\_SPARE\_BIT\_17                                   | 0x7000FBC4 |
| FUSE\_SPARE\_BIT\_18                                   | 0x7000FBC8 |
| FUSE\_SPARE\_BIT\_19                                   | 0x7000FBCC |
| FUSE\_SPARE\_BIT\_20                                   | 0x7000FBD0 |
| FUSE\_SPARE\_BIT\_21                                   | 0x7000FBD4 |
| FUSE\_SPARE\_BIT\_22                                   | 0x7000FBD8 |
| FUSE\_SPARE\_BIT\_23                                   | 0x7000FBDC |
| FUSE\_SPARE\_BIT\_24                                   | 0x7000FBE0 |
| FUSE\_SPARE\_BIT\_25                                   | 0x7000FBE4 |
| FUSE\_SPARE\_BIT\_26                                   | 0x7000FBE8 |
| FUSE\_SPARE\_BIT\_27                                   | 0x7000FBEC |
| FUSE\_SPARE\_BIT\_28                                   | 0x7000FBF0 |
| FUSE\_SPARE\_BIT\_29                                   | 0x7000FBF4 |
| FUSE\_SPARE\_BIT\_30                                   | 0x7000FBF8 |
| FUSE\_SPARE\_BIT\_31                                   | 0x7000FBFC |
|                                                        |            |

#### FUSE\_SKU\_INFO

Stores the SKU ID (must be 0x83).

#### FUSE\_FA

Stores failure analysis mode.

#### FUSE\_SOC\_SPEEDO\_1

Stores the bootrom patch version.

#### FUSE\_RESERVED\_ODM4

| Bits | Description                               |
| ---- | ----------------------------------------- |
| 0-1  | Unit type (3 = debug; 0 = retail)         |
| 2    | Unknown config (must be 1 on retail)      |
| 8    | Unknown config mask (must be 0 on retail) |
| 9    | Unit type mask (0 = debug; 1 = retail)    |
|      |                                           |

This stores some device configuration parameters.

#### FUSE\_RESERVED\_ODM6

This register returns the value programmed into index 0x3A of the fuse
array.

#### FUSE\_RESERVED\_ODM7

This register returns the value programmed into index 0x3C of the fuse
array.

#### FUSE\_SPARE\_BIT\_5

Must be non-zero on retail units, otherwise the first bootloader panics.
On debug units it can be zero, which tells the bootloader to choose from
two debug master key seeds. If set to non-zero on a debug unit, it tells
the bootloader to choose from two retail master key seeds (only the last
one matches the retail master key seed).

#### FUSE\_PRIVATE\_KEY

This stores the 160-bit private key (128 bit SBK + 32-bit device key).
Reads to these registers after the SBK is locked out produce all-FF
output.

#### FUSE\_PUBLIC\_KEY

This stores the SHA256 hash of the 2048-bit RSA key expected at
BCT+0x210.

## eFuses

The actual hardware fuses can be programmed through the fuse driver
after enabling fuse programming.

Below is a list of common fuse indexes used by Tegra devices (and
applicable to the Switch). Note that the indexes are relative to the
start of the fuse array and each element is a 4 byte word. A single fuse
write operation always writes the same word at both fuse\_array + 0
(PRIMARY\_ALIAS) and fuse\_array + 1 (REDUNDANT\_ALIAS).

| Name                                          | Index | Bits |
| --------------------------------------------- | ----- | ---- |
| jtag\_disable                                 | 0x00  | 1    |
| odm\_production\_mode                         | 0x00  | 1    |
| odm\_lock                                     | 0x00  | 4    |
| public\_key                                   | 0x0C  | 256  |
| secure\_boot\_key                             | 0x22  | 128  |
| device\_key                                   | 0x2A  | 32   |
| sec\_boot\_dev\_cfg                           | 0x2C  | 16   |
| sec\_boot\_dev\_sel                           | 0x2C  | 3    |
| sw\_reserved                                  | 0x2E  | 12   |
| ignore\_dev\_sel\_straps                      | 0x2E  | 1    |
| [odm\_reserved](#odm_reserved "wikilink")     | 0x2E  | 256  |
| pkc\_disable                                  | 0x52  | 1    |
| [bootrom\_ipatch](#bootrom_ipatch "wikilink") | 0x72  | 624  |
|                                               |       |      |

### odm\_reserved

The first bootloader only burns fuses in this region. Both fuse indexes
0x3A (odm\_reserved + 0x0C) and 0x3C (odm\_reserved + 0x0E) are used for
anti-downgrade control. These fuses will have their values cached into
[FUSE\_RESERVED\_ODM6](#FUSE_RESERVED_ODM6 "wikilink") and
[FUSE\_RESERVED\_ODM7](#FUSE_RESERVED_ODM7 "wikilink").

### bootrom\_ipatch

Tegra210 based hardware such as the Switch provides support for bootrom
patches. The patch data is burned to the hardware fuse array using a
specific format (see [shuffle2's ipatch
decoder](https://gist.github.com/shuffle2/f8728159da100e9df2606d43925de0af))
and is executed by the bootrom, replacing it's original code.

The following represents the patch data dumped from a 2.0.0 Switch
console:

`Patch address       Patch data `  
`0x001016AE          0xDF00    // svc #0x00 (offset 0x48)`  
`0x00103040          0xDF22    // svc #0x22 (offset 0x8c)`  
`0x00106F2E          0xDF26    // svc #0x26 (offset 0x94)`  
`0x0010FB3C          0x2000    // movs r0, #0x00`  
`0x00100856          0xDF2C    // svc #0x2c (offset 0xa0)`  
`0x00106F54          0xDF42    // svc #0x42 (offset 0xcc)`  
`0x001012E4          0xDF4B    // svc #0x4b (offset 0xde)`  
`0x00104526          0xDF54    // svc #0x54 (offset 0xf0)`  
`0x001043F4          0xDF5D    // svc #0x5d (offset 0x102)`  
`0x00117744          0xAC57    // data`  
`0x00117758          0x3D19    // data`  
`0x00103D2A          0x2001    // movs r0, #0x01`

The last 4 patches are exclusive to the Switch, while the remaining ones
are often included in most Tegra210 based devices.

## Anti-downgrade

The first bootloader verifies
[FUSE\_RESERVED\_ODM7](#FUSE_RESERVED_ODM7 "wikilink") to prevent
downgrading. How many fuses are expected to be burnt depends the
device's unit type as
below.

| System version | Expected number of burnt fuses (retail) | Expected number of burnt fuses (non-retail) |
| -------------- | --------------------------------------- | ------------------------------------------- |
| 1.0.0          | 1                                       | 0                                           |
| 2.0.0-2.3.0    | 2                                       | 0                                           |
| 3.0.0          | 3                                       | 1                                           |
| 3.0.1-3.0.2    | 4                                       | 1                                           |
| 4.0.0          | 5                                       | 1                                           |

If too many fuses are burnt the bootloader will panic immediately.

If too few are burnt, the bootloader will enable fuse programming and
write the expected value to fuse indexes 0x3A and 0x3C. Afterwards, fuse
programming is disabled and a magic value (0x21 == TEGRA210) is written
to PMC\_SCRATCH200 register (0x7000EC40). Finally, the watchdog timer is
initialized and programmed to force a reset.

On a subsequent boot, after the anti-downgrade fuses are checked again,
the PMC\_RST\_STATUS register (0x7000E5B4) is checked and if set to 0x01
(watchdog reset) the PMC\_SCRATCH200 register (0x7000EC40) will be
checked for the magic value (0x21 == TEGRA210). PMC\_RST\_STATUS will
only be set back to 0 (power on reset) if the fuse count matches the new
expected value, otherwise the system will panic.

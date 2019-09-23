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

| Name                                                          | Address    |
| ------------------------------------------------------------- | ---------- |
| [FUSE\_FUSECTRL](#FUSE_FUSECTRL "wikilink")                   | 0x7000F800 |
| [FUSE\_FUSEADDR](#FUSE_FUSEADDR "wikilink")                   | 0x7000F804 |
| [FUSE\_FUSERDATA](#FUSE_FUSERDATA "wikilink")                 | 0x7000F808 |
| [FUSE\_FUSEWDATA](#FUSE_FUSEWDATA "wikilink")                 | 0x7000F80C |
| FUSE\_FUSETIME\_RD1                                           | 0x7000F810 |
| FUSE\_FUSETIME\_RD2                                           | 0x7000F814 |
| FUSE\_FUSETIME\_PGM1                                          | 0x7000F818 |
| [FUSE\_FUSETIME\_PGM2](#FUSE_FUSETIME_PGM2 "wikilink")        | 0x7000F81C |
| [FUSE\_PRIV2INTFC\_START](#FUSE_PRIV2INTFC_START "wikilink")  | 0x7000F820 |
| FUSE\_FUSEBYPASS                                              | 0x7000F824 |
| FUSE\_PRIVATEKEYDISABLE                                       | 0x7000F828 |
| [FUSE\_DISABLEREGPROGRAM](#FUSE_DISABLEREGPROGRAM "wikilink") | 0x7000F82C |
| [FUSE\_WRITE\_ACCESS\_SW](#FUSE_WRITE_ACCESS_SW "wikilink")   | 0x7000F830 |
| FUSE\_PWR\_GOOD\_SW                                           | 0x7000F834 |
| FUSE\_PRIV2RESHIFT                                            | 0x7000F83C |
| FUSE\_FUSETIME\_RD3                                           | 0x7000F84C |
| FUSE\_PRIVATE\_KEY0\_NONZERO                                  | 0x7000F880 |
| FUSE\_PRIVATE\_KEY1\_NONZERO                                  | 0x7000F884 |
| FUSE\_PRIVATE\_KEY2\_NONZERO                                  | 0x7000F888 |
| FUSE\_PRIVATE\_KEY3\_NONZERO                                  | 0x7000F88C |
| FUSE\_PRIVATE\_KEY4\_NONZERO                                  | 0x7000F890 |

#### FUSE\_FUSECTRL

<table>
<thead>
<tr class="header">
<th><p>Bits</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0-1</p></td>
<td><p>FUSE_FUSECTRL_CMD</p>
<p><code>0x00: IDLE</code><br />
<code>0x01: READ</code><br />
<code>0x02: WRITE</code><br />
<code>0x03: SENSE_CTRL</code></p></td>
</tr>
<tr class="even">
<td><p>16-20</p></td>
<td><p>FUSE_FUSECTRL_STATE</p>
<p><code>0x00: STATE_RESET</code><br />
<code>0x01: STATE_POST_RESET</code><br />
<code>0x02: STATE_LOAD_ROW0</code><br />
<code>0x03: STATE_LOAD_ROW1</code><br />
<code>0x04: STATE_IDLE</code><br />
<code>0x05: STATE_READ_SETUP</code><br />
<code>0x06: STATE_READ_STROBE</code><br />
<code>0x07: STATE_SAMPLE_FUSES</code><br />
<code>0x08: STATE_READ_HOLD</code><br />
<code>0x09: STATE_FUSE_SRC_SETUP</code><br />
<code>0x0A: STATE_WRITE_SETUP</code><br />
<code>0x0B: STATE_WRITE_ADDR_SETUP</code><br />
<code>0x0C: STATE_WRITE_PROGRAM</code><br />
<code>0x0D: STATE_WRITE_ADDR_HOLD</code><br />
<code>0x0E: STATE_FUSE_SRC_HOLD</code><br />
<code>0x0F: STATE_READ_BEFORE_WRITE_SETUP</code></p></td>
</tr>
<tr class="odd">
<td><p>21</p></td>
<td><p>FUSE_FUSECTRL_MARGIN_READ</p></td>
</tr>
<tr class="even">
<td><p>22</p></td>
<td><p>FUSE_FUSECTRL_RWL</p></td>
</tr>
<tr class="odd">
<td><p>23</p></td>
<td><p>FUSE_FUSECTRL_TRCS</p></td>
</tr>
<tr class="even">
<td><p>24</p></td>
<td><p>FUSE_FUSECTRL_AT1</p></td>
</tr>
<tr class="odd">
<td><p>25</p></td>
<td><p>FUSE_FUSECTRL_AT0</p></td>
</tr>
<tr class="even">
<td><p>26</p></td>
<td><p>FUSE_FUSECTRL_PD_CTRL</p></td>
</tr>
<tr class="odd">
<td><p>30</p></td>
<td><p>FUSE_FUSECTRL_FUSE_SENSE_DONE</p></td>
</tr>
<tr class="even">
<td><p>31</p></td>
<td><p>FUSE_FUSECTRL_RECORD_SHIFT_DONE</p></td>
</tr>
</tbody>
</table>

Before fuse reading/writing the power down mode must be disabled.
SENSE\_CTRL mode flushes programmed values into the [cache
registers](Fuses#Cache%20registers.md##Cache_registers "wikilink").

#### FUSE\_FUSEADDR

This register takes the address of the fuse to be read/written/sensed.

#### FUSE\_FUSERDATA

This register receives the value read from the fuse.

#### FUSE\_FUSEWDATA

This register takes the value to be written to the fuse.

#### FUSE\_FUSETIME\_PGM2

This register takes the fuse programming pulse (0xC0 == 19200 kHz).

#### FUSE\_PRIV2INTFC\_START

| Bits | Description                            |
| ---- | -------------------------------------- |
| 0    | FUSE\_PRIV2INTFC\_START\_DATA          |
| 1    | FUSE\_PRIV2INTFC\_START\_SKIP\_RECORDS |

#### FUSE\_DISABLEREGPROGRAM

If set to 0x01, this register disables fuse programming.

#### FUSE\_WRITE\_ACCESS\_SW

If set to 0x01, this register disables software writes to the fuse
driver registers.

### Cache registers

| Name                                                               | Address    |
| ------------------------------------------------------------------ | ---------- |
| FUSE\_PRODUCTION\_MODE                                             | 0x7000F900 |
| FUSE\_JTAG\_SECUREID\_VALID                                        | 0x7000F904 |
| FUSE\_ODM\_LOCK                                                    | 0x7000F908 |
| FUSE\_OPT\_OPENGL\_EN                                              | 0x7000F90C |
| [FUSE\_SKU\_INFO](#FUSE_SKU_INFO "wikilink")                       | 0x7000F910 |
| FUSE\_CPU\_SPEEDO\_0\_CALIB                                        | 0x7000F914 |
| FUSE\_CPU\_IDDQ\_CALIB                                             | 0x7000F918 |
| FUSE\_DAC\_CRT\_CALIB                                              | 0x7000F91C |
| FUSE\_DAC\_HDTV\_CALIB                                             | 0x7000F920 |
| FUSE\_DAC\_SDTV\_CALIB                                             | 0x7000F924 |
| [FUSE\_OPT\_FT\_REV](#FUSE_OPT_FT_REV "wikilink")                  | 0x7000F928 |
| FUSE\_CPU\_SPEEDO\_1\_CALIB                                        | 0x7000F92C |
| FUSE\_CPU\_SPEEDO\_2\_CALIB                                        | 0x7000F930 |
| FUSE\_SOC\_SPEEDO\_0\_CALIB                                        | 0x7000F934 |
| [FUSE\_SOC\_SPEEDO\_1\_CALIB](#FUSE_SOC_SPEEDO_1_CALIB "wikilink") | 0x7000F938 |
| FUSE\_SOC\_SPEEDO\_2\_CALIB                                        | 0x7000F93C |
| FUSE\_SOC\_IDDQ\_CALIB                                             | 0x7000F940 |
| FUSE\_RESERVED\_PRODUCTION\_WP                                     | 0x7000F944 |
| [FUSE\_FA](#FUSE_FA "wikilink")                                    | 0x7000F948 |
| FUSE\_RESERVED\_PRODUCTION                                         | 0x7000F94C |
| FUSE\_HDMI\_LANE0\_CALIB                                           | 0x7000F950 |
| FUSE\_HDMI\_LANE1\_CALIB                                           | 0x7000F954 |
| FUSE\_HDMI\_LANE2\_CALIB                                           | 0x7000F958 |
| FUSE\_HDMI\_LANE3\_CALIB                                           | 0x7000F95C |
| FUSE\_ENCRYPTION\_RATE                                             | 0x7000F960 |
| [FUSE\_PUBLIC\_KEY0](#FUSE_PUBLIC_KEY "wikilink")                  | 0x7000F964 |
| [FUSE\_PUBLIC\_KEY1](#FUSE_PUBLIC_KEY "wikilink")                  | 0x7000F968 |
| [FUSE\_PUBLIC\_KEY2](#FUSE_PUBLIC_KEY "wikilink")                  | 0x7000F96C |
| [FUSE\_PUBLIC\_KEY3](#FUSE_PUBLIC_KEY "wikilink")                  | 0x7000F970 |
| [FUSE\_PUBLIC\_KEY4](#FUSE_PUBLIC_KEY "wikilink")                  | 0x7000F974 |
| [FUSE\_PUBLIC\_KEY5](#FUSE_PUBLIC_KEY "wikilink")                  | 0x7000F978 |
| [FUSE\_PUBLIC\_KEY6](#FUSE_PUBLIC_KEY "wikilink")                  | 0x7000F97C |
| [FUSE\_PUBLIC\_KEY7](#FUSE_PUBLIC_KEY "wikilink")                  | 0x7000F980 |
| FUSE\_TSENSOR1\_CALIB                                              | 0x7000F984 |
| FUSE\_TSENSOR2\_CALIB                                              | 0x7000F988 |
| FUSE\_VSENSOR\_CALIB                                               | 0x7000F98C |
| [FUSE\_OPT\_CP\_REV](#FUSE_OPT_CP_REV "wikilink")                  | 0x7000F990 |
| FUSE\_OPT\_PFG                                                     | 0x7000F994 |
| FUSE\_TSENSOR0\_CALIB                                              | 0x7000F998 |
| FUSE\_FIRST\_BOOTROM\_PATCH\_SIZE                                  | 0x7000F99C |
| FUSE\_SECURITY\_MODE                                               | 0x7000F9A0 |
| [FUSE\_PRIVATE\_KEY0](#FUSE_PRIVATE_KEY "wikilink")                | 0x7000F9A4 |
| [FUSE\_PRIVATE\_KEY1](#FUSE_PRIVATE_KEY "wikilink")                | 0x7000F9A8 |
| [FUSE\_PRIVATE\_KEY2](#FUSE_PRIVATE_KEY "wikilink")                | 0x7000F9AC |
| [FUSE\_PRIVATE\_KEY3](#FUSE_PRIVATE_KEY "wikilink")                | 0x7000F9B0 |
| [FUSE\_PRIVATE\_KEY4](#FUSE_PRIVATE_KEY "wikilink")                | 0x7000F9B4 |
| FUSE\_ARM\_JTAG\_DIS                                               | 0x7000F9B8 |
| FUSE\_BOOT\_DEVICE\_INFO                                           | 0x7000F9BC |
| [FUSE\_RESERVED\_SW](#FUSE_RESERVED_SW "wikilink")                 | 0x7000F9C0 |
| FUSE\_OPT\_VP9\_DISABLE                                            | 0x7000F9C4 |
| [FUSE\_RESERVED\_ODM0](#FUSE_RESERVED_ODM0 "wikilink")             | 0x7000F9C8 |
| [FUSE\_RESERVED\_ODM1](#FUSE_RESERVED_ODM1 "wikilink")             | 0x7000F9CC |
| [FUSE\_RESERVED\_ODM2](#FUSE_RESERVED_ODM2 "wikilink")             | 0x7000F9D0 |
| [FUSE\_RESERVED\_ODM3](#FUSE_RESERVED_ODM3 "wikilink")             | 0x7000F9D4 |
| [FUSE\_RESERVED\_ODM4](#FUSE_RESERVED_ODM4 "wikilink")             | 0x7000F9D8 |
| FUSE\_RESERVED\_ODM5                                               | 0x7000F9DC |
| [FUSE\_RESERVED\_ODM6](#FUSE_RESERVED_ODM6 "wikilink")             | 0x7000F9E0 |
| [FUSE\_RESERVED\_ODM7](#FUSE_RESERVED_ODM7 "wikilink")             | 0x7000F9E4 |
| FUSE\_OBS\_DIS                                                     | 0x7000F9E8 |
| FUSE\_NOR\_INFO                                                    | 0x7000F9EC |
| FUSE\_USB\_CALIB                                                   | 0x7000F9F0 |
| FUSE\_SKU\_DIRECT\_CONFIG                                          | 0x7000F9F4 |
| FUSE\_KFUSE\_PRIVKEY\_CTRL                                         | 0x7000F9F8 |
| FUSE\_PACKAGE\_INFO                                                | 0x7000F9FC |
| FUSE\_OPT\_VENDOR\_CODE                                            | 0x7000FA00 |
| FUSE\_OPT\_FAB\_CODE                                               | 0x7000FA04 |
| FUSE\_OPT\_LOT\_CODE\_0                                            | 0x7000FA08 |
| FUSE\_OPT\_LOT\_CODE\_1                                            | 0x7000FA0C |
| FUSE\_OPT\_WAFER\_ID                                               | 0x7000FA10 |
| FUSE\_OPT\_X\_COORDINATE                                           | 0x7000FA14 |
| FUSE\_OPT\_Y\_COORDINATE                                           | 0x7000FA18 |
| FUSE\_OPT\_SEC\_DEBUG\_EN                                          | 0x7000FA1C |
| FUSE\_OPT\_OPS\_RESERVED                                           | 0x7000FA20 |
| FUSE\_SATA\_CALIB                                                  | 0x7000FA24 |
| FUSE\_GPU\_IDDQ\_CALIB                                             | 0x7000FA28 |
| FUSE\_TSENSOR3\_CALIB                                              | 0x7000FA2C |
| FUSE\_SKU\_BOND\_OUT\_L                                            | 0x7000FA30 |
| FUSE\_SKU\_BOND\_OUT\_H                                            | 0x7000FA34 |
| FUSE\_SKU\_BOND\_OUT\_U                                            | 0x7000FA38 |
| FUSE\_SKU\_BOND\_OUT\_V                                            | 0x7000FA3C |
| FUSE\_SKU\_BOND\_OUT\_W                                            | 0x7000FA40 |
| FUSE\_OPT\_SAMPLE\_TYPE                                            | 0x7000FA44 |
| FUSE\_OPT\_SUBREVISION                                             | 0x7000FA48 |
| FUSE\_OPT\_SW\_RESERVED\_0                                         | 0x7000FA4C |
| FUSE\_OPT\_SW\_RESERVED\_1                                         | 0x7000FA50 |
| FUSE\_TSENSOR4\_CALIB                                              | 0x7000FA54 |
| FUSE\_TSENSOR5\_CALIB                                              | 0x7000FA58 |
| FUSE\_TSENSOR6\_CALIB                                              | 0x7000FA5C |
| FUSE\_TSENSOR7\_CALIB                                              | 0x7000FA60 |
| FUSE\_OPT\_PRIV\_SEC\_EN                                           | 0x7000FA64 |
| [FUSE\_PKC\_DISABLE](#FUSE_PKC_DISABLE "wikilink")                 | 0x7000FA68 |
| FUSE\_FUSE2TSEC\_DEBUG\_DISABLE                                    | 0x7000FA7C |
| FUSE\_TSENSOR\_COMMON                                              | 0x7000FA80 |
| FUSE\_OPT\_CP\_BIN                                                 | 0x7000FA84 |
| FUSE\_OPT\_GPU\_DISABLE                                            | 0x7000FA88 |
| FUSE\_OPT\_FT\_BIN                                                 | 0x7000FA8C |
| FUSE\_OPT\_DONE\_MAP                                               | 0x7000FA90 |
| FUSE\_APB2JTAG\_DISABLE                                            | 0x7000FA98 |
| FUSE\_ODM\_INFO                                                    | 0x7000FA9C |
| FUSE\_ARM\_CRYPT\_DE\_FEATURE                                      | 0x7000FAA8 |
| FUSE\_WOA\_SKU\_FLAG                                               | 0x7000FAC0 |
| FUSE\_ECO\_RESERVE\_1                                              | 0x7000FAC4 |
| FUSE\_GCPLEX\_CONFIG\_FUSE                                         | 0x7000FAC8 |
| FUSE\_PRODUCTION\_MONTH                                            | 0x7000FACC |
| FUSE\_RAM\_REPAIR\_INDICATOR                                       | 0x7000FAD0 |
| FUSE\_TSENSOR9\_CALIB                                              | 0x7000FAD4 |
| FUSE\_VMIN\_CALIBRATION                                            | 0x7000FADC |
| FUSE\_AGING\_SENSOR\_CALIBRATION                                   | 0x7000FAE0 |
| FUSE\_DEBUG\_AUTHENTICATION                                        | 0x7000FAE4 |
| FUSE\_SECURE\_PROVISION\_INDEX                                     | 0x7000FAE8 |
| FUSE\_SECURE\_PROVISION\_INFO                                      | 0x7000FAEC |
| FUSE\_OPT\_GPU\_DISABLE\_CP1                                       | 0x7000FAF0 |
| FUSE\_SPARE\_ENDIS                                                 | 0x7000FAF4 |
| FUSE\_ECO\_RESERVE\_0                                              | 0x7000FAF8 |
| FUSE\_SPARE\_REALIGNMENT\_REG\_OLD                                 | 0x7000FAFC |
| FUSE\_RESERVED\_CALIB0                                             | 0x7000FB04 |
| FUSE\_RESERVED\_CALIB1                                             | 0x7000FB08 |
| FUSE\_OPT\_GPU\_TPC0\_DISABLE                                      | 0x7000FB0C |
| FUSE\_OPT\_GPU\_TPC0\_DISABLE\_CP1                                 | 0x7000FB10 |
| FUSE\_OPT\_CPU\_DISABLE                                            | 0x7000FB14 |
| FUSE\_OPT\_CPU\_DISABLE\_CP1                                       | 0x7000FB18 |
| FUSE\_TSENSOR10\_CALIB                                             | 0x7000FB1C |
| FUSE\_TSENSOR10\_CALIB\_AUX                                        | 0x7000FB20 |
| FUSE\_OPT\_RAM\_SVOP\_DP                                           | 0x7000FB24 |
| FUSE\_OPT\_RAM\_SVOP\_PDP                                          | 0x7000FB28 |
| FUSE\_OPT\_RAM\_SVOP\_REG                                          | 0x7000FB2C |
| FUSE\_OPT\_RAM\_SVOP\_SP                                           | 0x7000FB30 |
| FUSE\_OPT\_RAM\_SVOP\_SMPDP                                        | 0x7000FB34 |
| FUSE\_OPT\_GPU\_TPC0\_DISABLE\_CP2                                 | 0x7000FB38 |
| FUSE\_OPT\_GPU\_TPC1\_DISABLE                                      | 0x7000FB3C |
| FUSE\_OPT\_GPU\_TPC1\_DISABLE\_CP1                                 | 0x7000FB40 |
| FUSE\_OPT\_GPU\_TPC1\_DISABLE\_CP2                                 | 0x7000FB44 |
| FUSE\_OPT\_CPU\_DISABLE\_CP2                                       | 0x7000FB48 |
| FUSE\_OPT\_GPU\_DISABLE\_CP2                                       | 0x7000FB4C |
| FUSE\_USB\_CALIB\_EXT                                              | 0x7000FB50 |
| FUSE\_RESERVED\_FIELD                                              | 0x7000FB54 |
| FUSE\_OPT\_ECC\_EN                                                 | 0x7000FB58 |
| FUSE\_SPARE\_REALIGNMENT\_REG                                      | 0x7000FB7C |
| FUSE\_SPARE\_BIT\_0                                                | 0x7000FB80 |
| FUSE\_SPARE\_BIT\_1                                                | 0x7000FB84 |
| [FUSE\_SPARE\_BIT\_2](#FUSE_SPARE_BIT_2 "wikilink")                | 0x7000FB88 |
| [FUSE\_SPARE\_BIT\_3](#FUSE_SPARE_BIT_3 "wikilink")                | 0x7000FB8C |
| [FUSE\_SPARE\_BIT\_4](#FUSE_SPARE_BIT_4 "wikilink")                | 0x7000FB90 |
| [FUSE\_SPARE\_BIT\_5](#FUSE_SPARE_BIT_5 "wikilink")                | 0x7000FB94 |
| FUSE\_SPARE\_BIT\_6                                                | 0x7000FB98 |
| FUSE\_SPARE\_BIT\_7                                                | 0x7000FB9C |
| FUSE\_SPARE\_BIT\_8                                                | 0x7000FBA0 |
| FUSE\_SPARE\_BIT\_9                                                | 0x7000FBA4 |
| FUSE\_SPARE\_BIT\_10                                               | 0x7000FBA8 |
| FUSE\_SPARE\_BIT\_11                                               | 0x7000FBAC |
| FUSE\_SPARE\_BIT\_12                                               | 0x7000FBB0 |
| FUSE\_SPARE\_BIT\_13                                               | 0x7000FBB4 |
| FUSE\_SPARE\_BIT\_14                                               | 0x7000FBB8 |
| FUSE\_SPARE\_BIT\_15                                               | 0x7000FBBC |
| FUSE\_SPARE\_BIT\_16                                               | 0x7000FBC0 |
| FUSE\_SPARE\_BIT\_17                                               | 0x7000FBC4 |
| FUSE\_SPARE\_BIT\_18                                               | 0x7000FBC8 |
| FUSE\_SPARE\_BIT\_19                                               | 0x7000FBCC |
| FUSE\_SPARE\_BIT\_20                                               | 0x7000FBD0 |
| FUSE\_SPARE\_BIT\_21                                               | 0x7000FBD4 |
| FUSE\_SPARE\_BIT\_22                                               | 0x7000FBD8 |
| FUSE\_SPARE\_BIT\_23                                               | 0x7000FBDC |
| FUSE\_SPARE\_BIT\_24                                               | 0x7000FBE0 |
| FUSE\_SPARE\_BIT\_25                                               | 0x7000FBE4 |
| FUSE\_SPARE\_BIT\_26                                               | 0x7000FBE8 |
| FUSE\_SPARE\_BIT\_27                                               | 0x7000FBEC |
| FUSE\_SPARE\_BIT\_28                                               | 0x7000FBF0 |
| FUSE\_SPARE\_BIT\_29                                               | 0x7000FBF4 |
| FUSE\_SPARE\_BIT\_30                                               | 0x7000FBF8 |
| FUSE\_SPARE\_BIT\_31                                               | 0x7000FBFC |

#### FUSE\_SKU\_INFO

Stores the SKU ID (must be 0x83).

#### FUSE\_OPT\_FT\_REV

Stores the FT (Final Test) revision.

Original launch units have this value set to 0xA0 (revision 5.0). The
first batch of patched units have this value set to 0xC0 (revision 6.0).
The second batch of patched units have this value set to 0xE0 (revision
7.0)

#### FUSE\_FA

Stores failure analysis mode.

#### FUSE\_SOC\_SPEEDO\_1\_CALIB

Stores the bootrom patch version.

#### FUSE\_RESERVED\_ODM0

This stores an hardware ID.

#### FUSE\_RESERVED\_ODM1

This stores an hardware ID.

#### FUSE\_RESERVED\_ODM2

| Bits | Description                                            |
| ---- | ------------------------------------------------------ |
| 0-4  | \[5.0.0+\] Used as key generation (patched units only) |

This stores an hardware ID in original launch units, but in patched
units it stores a single value (key generation).

#### FUSE\_RESERVED\_ODM3

This stores an hardware ID in original launch units, but in patched
units it's empty.

#### FUSE\_RESERVED\_ODM4

| Bits                               | Description                                                        |
| ---------------------------------- | ------------------------------------------------------------------ |
| 0-1                                | Unit type (3 = debug; 0 = retail)                                  |
| 2                                  | Unknown config (must be 1 on retail)                               |
| \[1.0.0-3.0.2\] 3-5 \[4.0.0+\] 3-7 | DRAM ID                                                            |
| 8                                  | Unknown config mask (must be 0 on retail)                          |
| 9                                  | Unit type mask (0 = debug; 1 = retail)                             |
| 10                                 | \[3.0.0+\] Kiosk mode (0 = retail; 1 = kiosk)                      |
| 11                                 | \[5.0.0+\] Unit patch flag (0 = unpatched; 1 = patched)            |
| 16-19                              | \[4.0.0+\] New unit type (0 = Erista; 1 = Mariko; 2 = Mariko Lite) |

This stores some device configuration parameters.

#### FUSE\_RESERVED\_ODM6

This register returns the value programmed into fuse
[reserved\_odm6](#reserved_odm6 "wikilink").

#### FUSE\_RESERVED\_ODM7

This register returns the value programmed into fuse
[reserved\_odm7](#reserved_odm7 "wikilink").

#### FUSE\_PUBLIC\_KEY

This stores the SHA256 hash of the 2048-bit RSA key expected at
BCT+0x210.

#### FUSE\_OPT\_CP\_REV

Stores the CP (Chip Probing) revision.

Original launch units have this value set to 0xA0 (revision 5.0).
Patched units have this value set to 0x103 (revision 8.3).

#### FUSE\_PRIVATE\_KEY

This stores the 160-bit private key (128 bit SBK + 32-bit device key).
Reads to these registers after the SBK is locked out produce all-FF
output.

#### FUSE\_RESERVED\_SW

| Bits | Description                                                             |
| ---- | ----------------------------------------------------------------------- |
| 0-2  | Boot device                                                             |
| 3    | Skip device selection straps (0 = don't skip; 1 = skip)                 |
| 4    | ENABLE\_CHARGER\_DETECT                                                 |
| 5    | ENABLE\_WATCHDOG                                                        |
| 6    | Forced RCM two button mode (0 = Only VOLUME\_UP; 1 = VOLUME\_UP + HOME) |
| 7    | RCM USB controller mode (0 = USB 2.0; 1 = XUSB)                         |

This caches the value of the reserved\_sw fuse from the hardware bitmap.

Original launch units have the RCM USB controller mode set to USB 2.0,
while the first batch of patched units have the RCM USB controller mode
set to XUSB.

#### FUSE\_PKC\_DISABLE

This caches the value of the pkc\_disable fuse from the hardware array.

#### FUSE\_SPARE\_BIT\_2

Stores part of the speedo fusing revision.

#### FUSE\_SPARE\_BIT\_3

Stores part of the speedo fusing revision.

#### FUSE\_SPARE\_BIT\_4

Stores part of the speedo fusing revision.

#### FUSE\_SPARE\_BIT\_5

Must be non-zero on retail units, otherwise the first bootloader panics.
On debug units it can be zero, which tells the bootloader to choose from
two debug master key seeds. If set to non-zero on a debug unit, it tells
the bootloader to choose from two master key seeds (with the second one
being the retail master key seed).

\[4.0.0+\] This value is no longer used during boot.

## Bitmap

The actual hardware fuses are stored in a bitmap and may be programmed
through the fuse driver after enabling fuse programming.

Fuse numbers are relative to the start of the fuse bitmap where each
element is a 4 byte word and has a redundant alias. A single fuse write
operation must always write the same value to **fuse\_bitmap +
((fuse\_number + 0) \<\< 2)** (PRIMARY\_ALIAS) and **fuse\_bitmap +
((fuse\_number + 1) \<\< 2)** (REDUNDANT\_ALIAS). However, after offset
0x180 in the fuse bitmap, fuses no longer have a redundant alias.

Below is a list of common fuses used by Tegra devices (and applicable to
the Switch).

| Name                                        | Number | Redundant number | Bits     |
| ------------------------------------------- | ------ | ---------------- | -------- |
| enable\_fuse\_program                       | 0      | 1                | 0        |
| disable\_fuse\_program                      | 0      | 1                | 1        |
| bypass\_fuses                               | 0      | 1                | 2        |
| jtag\_direct\_access\_disable               | 0      | 1                | 3        |
| production\_mode                            | 0      | 1                | 4        |
| jtag\_secureid\_valid                       | 0      | 1                | 5        |
| odm\_lock                                   | 0      | 1                | 6-9      |
| fa\_mode                                    | 0      | 1                | 10       |
| security\_mode                              | 0      | 1                | 11       |
| arm\_debug\_dis                             | 0      | 1                | 12       |
| obs\_dis                                    | 0      | 1                | 13       |
| public\_key0                                | 10     | 11               | 30-31    |
| public\_key0                                | 12     | 13               | 0-29     |
| public\_key1                                | 12     | 13               | 30-31    |
| public\_key1                                | 14     | 15               | 0-29     |
| public\_key2                                | 14     | 15               | 30-31    |
| public\_key2                                | 16     | 17               | 0-29     |
| public\_key3                                | 16     | 17               | 30-31    |
| public\_key3                                | 18     | 19               | 0-29     |
| public\_key4                                | 18     | 19               | 30-31    |
| public\_key4                                | 20     | 21               | 0-29     |
| public\_key5                                | 20     | 21               | 30-31    |
| public\_key5                                | 22     | 23               | 0-29     |
| public\_key6                                | 22     | 23               | 30-31    |
| public\_key6                                | 24     | 25               | 0-29     |
| public\_key7                                | 24     | 25               | 30-31    |
| public\_key7                                | 26     | 27               | 0-29     |
| private\_key0                               | 34     | 35               | 12-31    |
| private\_key0                               | 36     | 37               | 0-11     |
| private\_key1                               | 36     | 37               | 12-31    |
| private\_key1                               | 38     | 39               | 0-11     |
| private\_key2                               | 38     | 39               | 12-31    |
| private\_key2                               | 40     | 41               | 0-11     |
| private\_key3                               | 40     | 41               | 12-31    |
| private\_key3                               | 42     | 43               | 0-11     |
| private\_key4                               | 42     | 43               | 12-31    |
| private\_key4                               | 44     | 45               | 0-11     |
| boot\_device\_info                          | 44     | 45               | 12-27    |
| reserved\_sw                                | 44     | 45               | 28-31    |
| reserved\_sw                                | 46     | 47               | 0-3      |
| reserved\_odm0                              | 46     | 47               | 5-31     |
| reserved\_odm0                              | 48     | 49               | 0-4      |
| reserved\_odm1                              | 48     | 49               | 5-31     |
| reserved\_odm1                              | 50     | 51               | 0-4      |
| reserved\_odm2                              | 50     | 51               | 5-31     |
| reserved\_odm2                              | 52     | 53               | 0-4      |
| reserved\_odm3                              | 52     | 53               | 5-31     |
| reserved\_odm3                              | 54     | 55               | 0-4      |
| reserved\_odm4                              | 54     | 55               | 5-31     |
| reserved\_odm4                              | 56     | 57               | 0-4      |
| reserved\_odm5                              | 56     | 57               | 5-31     |
| reserved\_odm5                              | 58     | 59               | 0-4      |
| [reserved\_odm6](#reserved_odm6 "wikilink") | 58     | 59               | 5-31     |
| [reserved\_odm6](#reserved_odm6 "wikilink") | 60     | 61               | 0-4      |
| [reserved\_odm7](#reserved_odm7 "wikilink") | 60     | 61               | 5-31     |
| [reserved\_odm7](#reserved_odm7 "wikilink") | 62     | 63               | 0-4      |
| kfuse\_privkey\_ctrl                        | 64     | 65               | 13-14    |
| package\_info                               | 64     | 65               | 15-18    |
| opt\_vendor\_code                           | 64     | 65               | 19-22    |
| opt\_fab\_code                              | 64     | 65               | 23-28    |
| opt\_lot\_code\_0                           | 64     | 65               | 29-31    |
| opt\_lot\_code\_0                           | 66     | 67               | 0-28     |
| opt\_lot\_code\_1                           | 66     | 67               | 29-31    |
| opt\_lot\_code\_1                           | 68     | 69               | 0-24     |
| opt\_wafer\_id                              | 68     | 69               | 25-30    |
| opt\_x\_coordinate                          | 68     | 69               | 31       |
| opt\_x\_coordinate                          | 70     | 71               | 0-7      |
| opt\_y\_coordinate                          | 70     | 71               | 8-16     |
| opt\_sec\_debug\_en                         | 70     | 71               | 17       |
| opt\_ops\_reserved                          | 70     | 71               | 18-23    |
| sata\_calib                                 | 70     | 71               | 24-25    |
| opt\_priv\_sec\_en                          | 90     | 91               | 8        |
| pkc\_disable                                | 90     | 91               | 9        |
| fuse2tsec\_debug\_disable                   | 90     | 91               | 10       |
| secure\_provision\_index                    | 90     | 91               | 24-27    |
| secure\_provision\_info                     | 90     | 91               | 28-29    |
| aid                                         | 103    | None             | 0-31     |
| [irom\_patch](#irom_patch "wikilink")       | 114    | None             | Variable |

### reserved\_odm6

Used for anti-downgrade control.

### reserved\_odm7

Used for anti-downgrade control.

### irom\_patch

Tegra210 based hardware such as the Switch provides support for bootrom
patches. The patch data is burned to the hardware fuse bitmap using a
specific format (see [shuffle2's ipatch
decoder](https://gist.github.com/shuffle2/f8728159da100e9df2606d43925de0af)).
The bootrom reads these fuses in order to initialize the IPATCH
hardware, which allows overriding data returned for code and data
fetches done by BPMP.

The following represents the patch data dumped from a Switch console:

    RAM:00000000 ; =============== S U B R O U T I N E =======================================
    RAM:00000000
    RAM:00000000
    RAM:00000000 irom_svc_dispatch
    RAM:00000000   STMFD   SP!, {R0-R2}                  ; ipatches (new):
    RAM:00000000                                         ;  0  b57df00     16ae     df00 : svc #0x00 (offset 0x48)
    RAM:00000000                                         ;  1 1820df22     3040     df22 : svc #0x22 (offset 0x8c)
    RAM:00000000                                         ;  2 3797df26     6f2e     df26 : svc #0x26 (offset 0x94)
    RAM:00000000                                         ;  3 3b4d2100     769a     2100 : movs r1, #0x00
    RAM:00000000                                         ;  4  42bdf2c      856     df2c : svc #0x2c (offset 0xa0)
    RAM:00000000                                         ;  5 37aadf42     6f54     df42 : svc #0x42 (offset 0xcc)
    RAM:00000000                                         ;  6  972df4b     12e4     df4b : svc #0x4b (offset 0xde)
    RAM:00000000                                         ;  7 2293df54     4526     df54 : svc #0x54 (offset 0xf0)
    RAM:00000000                                         ;  8 21fadf5d     43f4     df5d : svc #0x5d (offset 0x102)
    RAM:00000000                                         ;  9 bba2ac57    17744     ac57 : data
    RAM:00000000                                         ; 10 bbac3d19    17758     3d19 : data
    RAM:00000000                                         ; 11 1e952001     3d2a     2001 : movs r0, #0x01
    RAM:00000000                                         ; 
    RAM:00000000                                         ; ipatches (old):
    RAM:00000000                                         ;  0  b57df00     16ae     df00 : svc #0x00 (offset 0x48)
    RAM:00000000                                         ;  1 1820df22     3040     df22 : svc #0x22 (offset 0x8c)
    RAM:00000000                                         ;  2 3797df26     6f2e     df26 : svc #0x26 (offset 0x94)
    RAM:00000000                                         ;  3 7d9e2000     fb3c     2000 : movs r0, #0x00
    RAM:00000000                                         ;  4  42bdf2c      856     df2c : svc #0x2c (offset 0xa0)
    RAM:00000000                                         ;  5 37aadf42     6f54     df42 : svc #0x42 (offset 0xcc)
    RAM:00000000                                         ;  6  972df4b     12e4     df4b : svc #0x4b (offset 0xde)
    RAM:00000000                                         ;  7 2293df54     4526     df54 : svc #0x54 (offset 0xf0)
    RAM:00000000                                         ;  8 21fadf5d     43f4     df5d : svc #0x5d (offset 0x102)
    RAM:00000000                                         ;  9 bba2ac57    17744     ac57 : data
    RAM:00000000                                         ; 10 bbac3d19    17758     3d19 : data
    RAM:00000000                                         ; 11 1e952001     3d2a     2001 : movs r0, #0x01
    RAM:00000004   MOV     R2, LR
    RAM:00000008   SUB     R2, R2, #2
    RAM:0000000C   LDR     R2, [R2]
    RAM:00000010   AND     R2, R2, #0xFF
    RAM:00000014   MOV     R2, R2,LSL#1
    RAM:00000018   LDR     R0, =0x1007B0
    RAM:0000001C   LDR     R1, =0x1007F8
    RAM:00000020   SUB     R1, R1, R0
    RAM:00000024   LDR     R0, =0x40004C30
    RAM:00000028   ADD     R0, R0, R1
    RAM:0000002C   ADD     R2, R2, R0
    RAM:00000030   ORR     R2, R2, #1
    RAM:00000034   LDMFD   SP!, {R0,R1}
    RAM:00000038   BX      R2
    RAM:00000038 ; End of function irom_svc_dispatch
    RAM:00000038
    RAM:00000038 ; ---------------------------------------------------------------------------
    RAM:0000003C dword_3C DCD 0x1007B0                   ; DATA XREF: irom_svc_dispatch+18↑r
    RAM:00000040 dword_40 DCD 0x1007F8                   ; DATA XREF: irom_svc_dispatch+1C↑r
    RAM:00000044 dword_44 DCD 0x40004C30                 ; DATA XREF: irom_svc_dispatch+24↑r
    RAM:00000048   CODE16
    RAM:00000048
    RAM:00000048 ; =============== S U B R O U T I N E =======================================
    RAM:00000048
    RAM:00000048
    RAM:00000048 sub_48
    RAM:00000048   MOVS    R2, #0                        ; 0  b57df00     16ae     df00 : svc #0x00 (offset 0x48)
    RAM:0000004A   MVNS    R2, R2
    RAM:0000004C   LDR     R1, =0x60006410
    RAM:0000004E   STR     R2, [R1,#0x30]
    RAM:00000050   STR     R2, [R1,#0x38]
    RAM:00000052   LDR     R1, =0x600060F8
    RAM:00000054   STR     R2, [R1]
    RAM:00000056   STR     R2, [R1,#4]
    RAM:00000058   LDR     R1, =0x60006284
    RAM:0000005A   STR     R2, [R1]
    RAM:0000005C   STR     R2, [R1,#0x18]
    RAM:0000005E   ADDS    R1, #0x80
    RAM:00000060   ADDS    R1, #0x1C
    RAM:00000062   STR     R2, [R1]
    RAM:00000064   STR     R2, [R1,#8]
    RAM:00000066   STR     R2, [R1,#0x10]
    RAM:00000068   ADDS    R1, #0x80
    RAM:0000006A   STR     R2, [R1]
    RAM:0000006C   STR     R2, [R1,#4]
    RAM:0000006E   LDR     R1, =0x60006554
    RAM:00000070   STR     R2, [R1]
    RAM:00000072   MOVS    R2, #0xA0000000
    RAM:00000076   LDR     R1, =0x60006148
    RAM:00000078   STR     R2, [R1]
    RAM:0000007A   ADDS    R1, #0x38 ; '8'
    RAM:0000007C   STR     R2, [R1]
    RAM:0000007E   MOVS    R2, #0xE0000000
    RAM:00000082   LDR     R1, =0x600066A0
    RAM:00000084   STR     R2, [R1]
    RAM:00000086   MOVS    R1, #0
    RAM:00000088   MOVS    R0, #0xE
    RAM:0000008A   B       pop_r2_mov_pc_lr
    RAM:0000008A ; End of function sub_48
    RAM:0000008A
    RAM:0000008C
    RAM:0000008C ; =============== S U B R O U T I N E =======================================
    RAM:0000008C
    RAM:0000008C
    RAM:0000008C sub_8C
    RAM:0000008C   LDR     R0, [R1,#0x18]                ; 1 1820df22     3040     df22 : svc #0x22 (offset 0x8c)
    RAM:0000008E   MOVS    R2, #1
    RAM:00000090   ORRS    R0, R2
    RAM:00000092   B       pop_r2_mov_pc_lr
    RAM:00000092 ; End of function sub_8C
    RAM:00000092
    RAM:00000094
    RAM:00000094 ; =============== S U B R O U T I N E =======================================
    RAM:00000094
    RAM:00000094
    RAM:00000094 sub_94
    RAM:00000094   LDR     R2, [R4,#0x50]                ; 2 3797df26     6f2e     df26 : svc #0x26 (offset 0x94)
    RAM:00000096   ADDS    R2, R2, #2
    RAM:00000098   STR     R2, [R4,#0x50]
    RAM:0000009A   SUBS    R1, #0x80
    RAM:0000009C   STR     R1, [R4,#0x34]
    RAM:0000009E   B       pop_r2_mov_pc_lr
    RAM:0000009E ; End of function sub_94
    RAM:0000009E
    RAM:000000A0
    RAM:000000A0 ; =============== S U B R O U T I N E =======================================
    RAM:000000A0
    RAM:000000A0
    RAM:000000A0 sub_A0
    RAM:000000A0
    RAM:000000A0 ; FUNCTION CHUNK AT RAM:00000148 SIZE 00000004 BYTES
    RAM:000000A0
    RAM:000000A0   MOVS    R0, #0x70000000               ; 4  42bdf2c      856     df2c : svc #0x2c (offset 0xa0)
    RAM:000000A4   LDR     R6, =dword_7000EF14
    RAM:000000A6   LDR     R2, =dword_7000E5B4
    RAM:000000A8   LDR     R2, [R2]
    RAM:000000AA   CMP     R2, #0
    RAM:000000AC   BEQ     loc_B4
    RAM:000000AE   LDR     R2, [R6]
    RAM:000000B0   STR     R2, [R0,#8]
    RAM:000000B2   B       loc_BC
    RAM:000000B4 ; ---------------------------------------------------------------------------
    RAM:000000B4
    RAM:000000B4 loc_B4                                  ; CODE XREF: sub_A0+C↑j
    RAM:000000B4   LDR     R2, [R0,#8]
    RAM:000000B6   LSRS    R0, R0, #0x12
    RAM:000000B8   ORRS    R2, R0
    RAM:000000BA   STR     R2, [R6]
    RAM:000000BC
    RAM:000000BC loc_BC                                  ; CODE XREF: sub_A0+12↑j
    RAM:000000BC   LDR     R6, =dword_7000E9C0
    RAM:000000BE   LDR     R0, [R6]
    RAM:000000C0   MOVS    R2, #0x4000
    RAM:000000C4   ORRS    R2, R0
    RAM:000000C6   STR     R2, [R6]
    RAM:000000C8   LDR     R0, [R5,#0x10]
    RAM:000000CA   B       pop_r2_mov_pc_lr
    RAM:000000CA ; End of function sub_A0
    RAM:000000CA
    RAM:000000CC
    RAM:000000CC ; =============== S U B R O U T I N E =======================================
    RAM:000000CC
    RAM:000000CC
    RAM:000000CC sub_CC
    RAM:000000CC   MOVS    R2, #0xF000000                ; 5 37aadf42     6f54     df42 : svc #0x42 (offset 0xcc)
    RAM:000000D0   BICS    R1, R2
    RAM:000000D2   STR     R1, [R4,#0x10]
    RAM:000000D4   LDR     R1, [R4,#0x50]
    RAM:000000D6   MOVS    R2, #7
    RAM:000000D8   BICS    R1, R2
    RAM:000000DA   STR     R1, [R4,#0x50]
    RAM:000000DC   B       pop_r2_mov_pc_lr
    RAM:000000DC ; End of function sub_CC
    RAM:000000DC
    RAM:000000DE
    RAM:000000DE ; =============== S U B R O U T I N E =======================================
    RAM:000000DE
    RAM:000000DE
    RAM:000000DE sub_DE
    RAM:000000DE   LDR     R2, =dword_7000FA9C           ; 6  972df4b     12e4     df4b : svc #0x4b (offset 0xde)
    RAM:000000E0   LDR     R2, [R2]
    RAM:000000E2   LSRS    R2, R2, #8
    RAM:000000E4   LSLS    R2, R2, #1
    RAM:000000E6   LDR     R1, [R4]
    RAM:000000E8   BICS    R1, R2
    RAM:000000EA   STR     R1, [R4]
    RAM:000000EC   CMP     R0, #0
    RAM:000000EE   B       pop_r2_mov_pc_lr
    RAM:000000EE ; End of function sub_DE
    RAM:000000EE
    RAM:000000F0
    RAM:000000F0 ; =============== S U B R O U T I N E =======================================
    RAM:000000F0
    RAM:000000F0
    RAM:000000F0 sub_F0
    RAM:000000F0
    RAM:000000F0 arg_0=  0
    RAM:000000F0
    RAM:000000F0   LDR     R0, =0x400049F0               ; 7 2293df54     4526     df54 : svc #0x54 (offset 0xf0)
    RAM:000000F2   LDR     R2, [R0]
    RAM:000000F4   STR     R2, [SP,#arg_0]
    RAM:000000F6   LDR     R0, =0x40010000
    RAM:000000F8   LSRS    R2, R2, #17
    RAM:000000FA   BEQ     pop_r2_mov_pc_lr              ; if ([0x400049F0] >> 17) == 0) {
    RAM:000000FA                                         ;   r2 = [0x400049F0];
    RAM:000000FA                                         ; } else {
    RAM:000000FC   LDR     R0, =APBDEV_PMC_CNTRL_0
    RAM:000000FE   STR     R4, [R0]                      ;  write APBDEV_PMC_CNTRL
    RAM:00000100
    RAM:00000100 loc_100                                 ; CODE XREF: sub_F0:loc_100↓j
    RAM:00000100   B       loc_100                       ;  hang
    RAM:00000100 ; End of function sub_F0                ; }
    RAM:00000100
    RAM:00000102
    RAM:00000102 ; =============== S U B R O U T I N E =======================================
    RAM:00000102
    RAM:00000102
    RAM:00000102 sub_102
    RAM:00000102
    RAM:00000102 arg_0=  0
    RAM:00000102
    RAM:00000102   LDR     R2, =0x40010220               ; 8 21fadf5d     43f4     df5d : svc #0x5d (offset 0x102)
    RAM:00000104   STR     R2, [SP,#arg_0]               ; set r2 retval = [0x40010220]
    RAM:00000106   LDR     R2, [R2,#0x18]
    RAM:00000108   ADDS    R0, #0xFC
    RAM:0000010A   STR     R2, [R0,#0x1C]                ; [r0+0x118] = [0x40010220 + 0x18]
    RAM:0000010C   B       pop_r2_mov_pc_lr
    RAM:0000010C ; End of function sub_102
    RAM:0000010C
    RAM:0000010C ; ---------------------------------------------------------------------------
    RAM:0000010E   DCB    0
    RAM:0000010F   DCB    0
    RAM:00000110 off_110 DCD 0x60006410                  ; DATA XREF: sub_48+4↑r
    RAM:00000114 off_114 DCD 0x600060F8                  ; DATA XREF: sub_48+A↑r
    RAM:00000118 off_118 DCD 0x60006284                  ; DATA XREF: sub_48+10↑r
    RAM:0000011C off_11C DCD 0x60006554                  ; DATA XREF: sub_48+26↑r
    RAM:00000120 off_120 DCD 0x60006148                  ; DATA XREF: sub_48+2E↑r
    RAM:00000124 off_124 DCD 0x600066A0                  ; DATA XREF: sub_48+3A↑r
    RAM:00000128 off_128 DCD dword_7000EF14              ; DATA XREF: sub_A0+4↑r
    RAM:0000012C off_12C DCD dword_7000E5B4              ; DATA XREF: sub_A0+6↑r
    RAM:00000130 off_130 DCD dword_7000E9C0              ; DATA XREF: sub_A0:loc_BC↑r
    RAM:00000134 off_134 DCD dword_7000FA9C              ; DATA XREF: sub_DE↑r
    RAM:00000138 off_138 DCD 0x400049F0                  ; DATA XREF: sub_F0↑r
    RAM:0000013C dword_13C DCD 0x40010000                ; DATA XREF: sub_F0+6↑r
    RAM:00000140 off_140 DCD APBDEV_PMC_CNTRL_0          ; DATA XREF: sub_F0+C↑r
    RAM:00000144 off_144 DCD 0x40010220                  ; DATA XREF: sub_102↑r
    RAM:00000148 ; ---------------------------------------------------------------------------
    RAM:00000148 ; START OF FUNCTION CHUNK FOR sub_A0
    RAM:00000148
    RAM:00000148 pop_r2_mov_pc_lr                        ; CODE XREF: sub_48+42↑j
    RAM:00000148                                         ; sub_8C+6↑j ...
    RAM:00000148   POP     {R2}
    RAM:0000014A   MOV     PC, LR
    RAM:0000014A ; END OF FUNCTION CHUNK FOR sub_A0

The last 4 patches are exclusive to the Switch, while the remaining ones
are often included in most Tegra210 based devices.

#### IROM patch 0

This patch configures clock enables and clock gate overrides for new
hardware.

``` c
 u32 CLK_ENB_H_SET = 0x60006328;
 u32 CLK_ENB_L_SET = 0x60006320;
 u32 CLK_ENB_U_SET = 0x60006330; 
 u32 CLK_ENB_V_SET = 0x60006440;
 u32 CLK_ENB_W_SET = 0x60006448;
 u32 CLK_ENB_X_SET = 0x60006284;
 u32 CLK_ENB_Y_SET = 0x6000629C;
 u32 LVL2_CLK_GATE_OVRA = 0x600060F8;
 u32 LVL2_CLK_GATE_OVRB = 0x600060FC;
 u32 LVL2_CLK_GATE_OVRC = 0x600063A0;
 u32 LVL2_CLK_GATE_OVRD = 0x600063A4;
 u32 LVL2_CLK_GATE_OVRE = 0x60006554;
 u32 CLK_SOURCE_VI = 0x60006148;
 u32 CLK_SOURCE_HOST1X = 0x60006180;
 u32 CLK_SOURCE_NVENC = 0x600066A0; 

 // Set all clock enables and overrides
 *(u32 *)CLK_ENB_V_SET = 0xFFFFFFFF;
 *(u32 *)CLK_ENB_W_SET = 0xFFFFFFFF;
 *(u32 *)LVL2_CLK_GATE_OVRA = 0xFFFFFFFF;
 *(u32 *)LVL2_CLK_GATE_OVRB = 0xFFFFFFFF;
 *(u32 *)CLK_ENB_X_SET = 0xFFFFFFFF;
 *(u32 *)CLK_ENB_Y_SET = 0xFFFFFFFF;
 *(u32 *)CLK_ENB_L_SET = 0xFFFFFFFF;
 *(u32 *)CLK_ENB_H_SET = 0xFFFFFFFF;
 *(u32 *)CLK_ENB_U_SET = 0xFFFFFFFF;
 *(u32 *)LVL2_CLK_GATE_OVRC = 0xFFFFFFFF;
 *(u32 *)LVL2_CLK_GATE_OVRD = 0xFFFFFFFF;
 *(u32 *)LVL2_CLK_GATE_OVRE = 0xFFFFFFFF;

 // Set VI, HOST1X and NVENC clock sources to CLK_M
 *(u32 *)CLK_SOURCE_VI = 0xA0000000;
 *(u32 *)CLK_SOURCE_HOST1X = 0xA0000000;
 *(u32 *)CLK_SOURCE_NVENC = 0xE0000000;

 /*
     Untranslated instructions:

     MOVS    R1, #0
     MOVS    R0, #0xE
 */
 
 return;
```

#### IROM patch 1

This patch is a bugfix.

LP0 resume code expects APBDEV\_PMC\_SCRATCH190\_0 to be set to 0x01,
but the bootrom didn't set it.

``` c
 u32 APBDEV_PMC_SCRATCH190_0 = 0x7000EC18;
 u32 pmc_scratch190_val = *(u32 *)APBDEV_PMC_SCRATCH190_0;
 
 return (pmc_scratch190_val | 0x01);
```

#### IROM patch 2

This patch adjusts USB configurations.

``` c
 u32 USB1_UTMIP_SPARE_CFG0_0 = 0x7D000834;
 u32 USB1_UTMIP_BIAS_CFG2_0 = 0x7D000850;
 
 // Increase UTMIP_HSSQUELCH_LEVEL_NEW by 0x02
 *(u32 *)USB1_UTMIP_BIAS_CFG2_0 += 0x02;

 // Clear FUSE_HS_IREF_CAP_CFG
 *(u32 *)USB1_UTMIP_SPARE_CFG0_0 = ((*(u32 *)USB1_UTMIP_SPARE_CFG0_0 & ~(0x118)) - 0x80);
 
 return;
```

#### IROM patch 3

This patch ensures that waiting on PRC\_PENDING from the XUSB\_DEV
register T\_XUSB\_DEV\_XHCI\_PORTSC never fails.

In the second batch of patched units
([FUSE\_OPT\_FT\_REV](#FUSE_OPT_FT_REV "wikilink") set to revision 7.0)
this patch has been replaced with a fix for
[CVE-2018-6242](Switch%20System%20Flaws#Hardware.md##Hardware "wikilink")
(arbitrary copy when handling USB control requests in RCM). By setting
R1 to 0 at address 0x0010769A in the bootrom, the upper 16 bits of the
USB control request's wLength field are cleared out, effectively
limiting the request's size to a maximum of 255 bytes.

#### IROM patch 4

This patch allows backing up and restoring strapping options for
warmboot.

``` c
 u32 APBDEV_PMC_SCRATCH0_0 = 0x7000E450;
 u32 APBDEV_PMC_RST_STATUS_0 = 0x7000E5B4;
 u32 APBDEV_PMC_SEC_DISABLE8_0 = 0x7000E9C0;
 u32 APBDEV_PMC_SECURE_SCRATCH111_0 = 0x7000EF14;
 u32 APB_MISC_PP_STRAPPING_OPT_A_0 = 0x70000008; 

 u32 reset_status = *(u32 *)APBDEV_PMC_RST_STATUS_0;

 // Check for regular power on
 if (reset_status == 0)
 {    
     // Set all buttons in RCM_STRAPS and backup to PMC scratch
     *(u32 *)APBDEV_PMC_SECURE_SCRATCH111_0 = (*(u32 *)APB_MISC_PP_STRAPPING_OPT_A_0 | 0x1C00);
 }
 else
 {
     // Restore strapping options from PMC scratch
     *(u32 *)APB_MISC_PP_STRAPPING_OPT_A_0 = *(u32 *)APBDEV_PMC_SECURE_SCRATCH111_0;
 }

 // Disable write access to APBDEV_PMC_SECURE_SCRATCH111_0
 *(u32 *)APBDEV_PMC_SEC_DISABLE8_0 |= 0x4000;
 
 return *(u32 *)APBDEV_PMC_SCRATCH0_0;
```

#### IROM patch 5

This patch adjusts USB configurations.

``` c
 u32 USB1_UTMIP_HSRX_CFG0_0 = 0x7D000810;
 u32 USB1_UTMIP_BIAS_CFG2_0 = 0x7D000850;

 // Clear UTMIP_IDLE_WAIT, UTMIP_ELASTIC_LIMIT and UTMIP_PCOUNT_UPDN_DIV,
 // and set UTMIP_IDLE_WAIT to 0x11 and UTMIP_ELASTIC_LIMIT to 0x10 
 *(u32 *)USB1_UTMIP_HSRX_CFG0_0 = ((*(u32 *)USB1_UTMIP_HSRX_CFG0_0 & ~(0xF8000) + 0x88000 & ~(0x7C00) + 0x4000) & ~(0xF000000));
 
 // Clear UTMIP_HSSQUELCH_LEVEL_NEW
 *(u32 *)USB1_UTMIP_BIAS_CFG2_0 &= ~(0x07);
 
 return;
```

#### IROM patch 6

This patch is a factory backdoor.

It allows controlling the debug authentication configuration using a
fuse.

``` c
 u32 FUSE_ODM_INFO = 0x7000FA9C;

 u32 odm_info = *(u32 *)FUSE_ODM_INFO;
 debug_auth_override_val = ((odm_info >> 0x08) << 0x01);

 // Override debug authentication value stored in IRAM
 *(u32 *)0x400028E4 &= ~(debug_auth_override_val);

 /*
     Untranslated instructions:
 
     CMP     R0, #0
 */
 
 return;
```

#### IROM patch 7

This patch is a bugfix.

It prevents overflowing IRAM (0x40010000) when copying the warmboot
binary from DRAM.

``` c
 u32 APBDEV_PMC_CNTRL_0 = 0x7000E400;
 
 u32 warmboot_header_addr = 0x400049F0;
 u32 warmboot_bin_size = *(u32 *)warmboot_bin_header_addr;
 
 // Invalid warmboot binary size
 if (warmboot_size >> 0x11)
 {
     // Assert MAIN_RST
     // 0x40004BF0 comes from R4 and the bootrom doesn't bother to change it
     *(u32 *)APBDEV_PMC_CNTRL_0 = 0x40004BF0;

     // Deadlock
     while(1);
 }
 
 /*
     Untranslated instructions:
 
     LDR     R0, =0x40010000
     LDR     R2, [warmboot_bin_header_addr]
 */

 return;
```

#### IROM patch 8

This patch is a bugfix.

It sets the correct warmboot binary entrypoint address for RSA signature
verification, which would be done in DRAM instead of IRAM without this
patch.

``` c
 u32 warmboot_addr_ptr = 0x40010238;
 u32 warmboot_entry_addr_ptr = 0x40004C28;

 *(u32 *)warmboot_entry_addr_ptr = *(u32 *)warmboot_addr_ptr;

 /*
     Untranslated instructions:
 
     LDR     R2, [warmboot_addr_ptr]
 */
 
 return;
```

#### IROM patches 9 and 10

These patches modify the 256-bit Secure Provisioning AES key with index
0x3A.

#### IROM patch 11

This patch forces the value of
[SE\_TZRAM\_SECURITY](Security%20Engine.md "wikilink") to be 0x01
instead of restoring it from the saved SE context.

## Anti-downgrade

The first bootloader verifies
[FUSE\_RESERVED\_ODM7](#FUSE_RESERVED_ODM7 "wikilink") to prevent
downgrading. How many fuses are expected to be burnt depends the
device's unit type as below.

| System version | Expected number of burnt fuses (retail) | Expected number of burnt fuses (non-retail) |
| -------------- | --------------------------------------- | ------------------------------------------- |
| 1.0.0          | 1                                       | 0                                           |
| 2.0.0-2.3.0    | 2                                       | 0                                           |
| 3.0.0          | 3                                       | 1                                           |
| 3.0.1-3.0.2    | 4                                       | 1                                           |
| 4.0.0-4.1.0    | 5                                       | 1                                           |
| 5.0.0-5.1.0    | 6                                       | 1                                           |
| 6.0.0-6.1.0    | 7                                       | 1                                           |
| 6.2.0          | 8                                       | 1                                           |
| 7.0.0-8.0.1    | 9                                       | 1                                           |
| 8.1.0          | 10                                      | 1                                           |
| 9.0.0          | 11                                      | 1                                           |

If too many fuses are burnt the bootloader will panic immediately.

If too few are burnt, the bootloader will enable fuse programming and
write the expected value to fuses
[reserved\_odm6](#reserved_odm6 "wikilink") and
[reserved\_odm7](#reserved_odm7 "wikilink"). Afterwards, fuse
programming is disabled and the panic value 0x21 is written to
PMC\_SCRATCH200 register (0x7000EC40). Finally, the watchdog timer is
initialized and programmed to force a reset.

On a subsequent boot, after the anti-downgrade fuses are checked again,
the PMC\_RST\_STATUS register (0x7000E5B4) is checked and if set to 0x01
(watchdog reset) the PMC\_SCRATCH200 register (0x7000EC40) will be
checked for the panic value 0x21. PMC\_RST\_STATUS will only be set back
to 0 (power on reset) if the fuse count matches the new expected value,
otherwise the system will panic.

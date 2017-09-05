BCT (Boot Configuration Table) is a data structure present on Tegra
based devices that supplies boot time configuration parameters.

The Switch's BCT is included in the firmware package titles
(0100000000000819 and 010000000000081A) and is installed into eMMC
storage's [boot partition
0](Flash%20Filesystem#Boot%20Partitions.md##Boot_Partitions "wikilink").
A total of four BCT copies can be installed into the system: normal,
normal backup, safe mode and safe mode backup.

By design, the BCT's data is only signed after offset 0x0510. Therefore,
regions like [customer\_data](#customer_data "wikilink") can be freely
modified without resigning. This is done by
[NS](NS%20Services.md "wikilink") when injecting a new
[keyblob](Flash%20Filesystem#Keyblob.md##Keyblob "wikilink") during a
system update, for example.

During boot, the boot ROM parses the appropriate BCT from eMMC storage
and stores a copy of it in IRAM at address 0x40000000.

# Structure

## NAND

Below is the BCT structure used by the Switch, which is a minimal
variation of the Tegra 210 BCT format.

<table>
<thead>
<tr class="header">
<th><p>Offset</p></th>
<th><p>Size</p></th>
<th><p>Field</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x0000</p></td>
<td><p>0x210</p></td>
<td><p>bad_block_table</p></td>
<td><p>Table containing information on bad blocks</p>
<p><code>0x0000: num_entries (0x200)</code><br />
<code>0x0004: virtual_block_size (0x0F)</code><br />
<code>0x0005: block_size (0x0E)</code><br />
<code>0x0006: bad_blocks</code><br />
<code>0x0206: reserved</code></p></td>
</tr>
<tr class="even">
<td><p>0x0210</p></td>
<td><p>0x100</p></td>
<td><p>bct_key</p></td>
<td><p>BCT RSA key modulus</p></td>
</tr>
<tr class="odd">
<td><p>0x0310</p></td>
<td><p>0x110</p></td>
<td><p>bct_signature</p></td>
<td><p>BCT object signature</p>
<p><code>0x0310: hash (empty)</code><br />
<code>0x0320: rsa_pss_signature</code></p></td>
</tr>
<tr class="even">
<td><p>0x0420</p></td>
<td><p>0x04</p></td>
<td><p>sec_provisioning_key_num_insecure</p></td>
<td><p>Used for Factory Secure Provisioning. Always 0.</p></td>
</tr>
<tr class="odd">
<td><p>0x0424</p></td>
<td><p>0x20</p></td>
<td><p>sec_provisioning_key</p></td>
<td><p>Used for Factory Secure Provisioning. Always empty.</p></td>
</tr>
<tr class="even">
<td><p>0x0444</p></td>
<td><p>0xC4</p></td>
<td><p><a href="#customer_data" title="wikilink">customer_data</a></p></td>
<td><p>Data block available for the customer. Used in key generation.</p>
<p><code>0x0444: padding_0x0C</code><br />
<code>0x0450: keyblob_0xB0</code><br />
<code>0x0500: padding_0x08</code></p></td>
</tr>
<tr class="odd">
<td><p>0x0508</p></td>
<td><p>0x04</p></td>
<td><p>odm_data</p></td>
<td><p>Legacy field. Unused.</p></td>
</tr>
<tr class="even">
<td><p>0x050C</p></td>
<td><p>0x04</p></td>
<td><p>reserved0</p></td>
<td><p>Legacy field. Unused.</p></td>
</tr>
<tr class="odd">
<td><p>0x0510</p></td>
<td><p>0x10</p></td>
<td><p>random_aes_block</p></td>
<td><p>Always empty.</p></td>
</tr>
<tr class="even">
<td><p>0x0520</p></td>
<td><p>0x10</p></td>
<td><p>unique_chip_id</p></td>
<td><p>Always empty.</p></td>
</tr>
<tr class="odd">
<td><p>0x0530</p></td>
<td><p>0x04</p></td>
<td><p>boot_data_version</p></td>
<td><p>Set to 0x00210001 (BOOTDATA_VERSION_T210).</p></td>
</tr>
<tr class="even">
<td><p>0x0534</p></td>
<td><p>0x04</p></td>
<td><p>block_size_log2</p></td>
<td><p>Always 0x0E.</p></td>
</tr>
<tr class="odd">
<td><p>0x0538</p></td>
<td><p>0x04</p></td>
<td><p>page_size_log2</p></td>
<td><p>Always 0x09.</p></td>
</tr>
<tr class="even">
<td><p>0x053C</p></td>
<td><p>0x04</p></td>
<td><p>partition_size</p></td>
<td><p>Always 0x01000000.</p></td>
</tr>
<tr class="odd">
<td><p>0x0540</p></td>
<td><p>0x04</p></td>
<td><p>num_param_sets</p></td>
<td><p>Number of device parameter sets. Always 0x01.</p></td>
</tr>
<tr class="even">
<td><p>0x0544</p></td>
<td><p>0x04</p></td>
<td><p>dev_type</p></td>
<td><p>Device type. Set to 0x04 (dev_type_sdmmc).</p></td>
</tr>
<tr class="odd">
<td><p>0x0548</p></td>
<td><p>0x40</p></td>
<td><p>dev_params</p></td>
<td><p>Device parameters</p>
<p><code> 0x0548: sdmmc_clock_divider (0x09 == 24MHz)</code><br />
<code> 0x054C: sdmmc_data_width (0x02 == sdmmc_data_width_8bit)</code></p></td>
</tr>
<tr class="even">
<td><p>0x0588</p></td>
<td><p>0x04</p></td>
<td><p>num_sdram_sets</p></td>
<td><p>Number of SDRAM parameter sets. Always set to 0 (parameters unused).</p></td>
</tr>
<tr class="odd">
<td><p>0x058C</p></td>
<td><p>0x768</p></td>
<td><p>sdram_params0. Default values filled in, but not used</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>0x0CF4</p></td>
<td><p>0x768</p></td>
<td><p>sdram_params1. Default values filled in, but not used</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>0x145C</p></td>
<td><p>0x768</p></td>
<td><p>sdram_params2. Default values filled in, but not used</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>0x1BC4</p></td>
<td><p>0x768</p></td>
<td><p>sdram_params3. Default values filled in, but not used</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>0x232C</p></td>
<td><p>0x04</p></td>
<td><p>num_bootloaders</p></td>
<td><p>Number of bootloaders installed. Always 0x02 (maximum is 0x04).</p></td>
</tr>
<tr class="even">
<td><p>0x2330</p></td>
<td><p>0x12C</p></td>
<td><p><a href="#bootloader0_info" title="wikilink">bootloader0_info</a></p></td>
<td><p>Configuration parameters for bootloader 0 (normal).</p>
<p><code>0x2330: version (variable)</code><br />
<code>0x2334: start_block (0x00000040)</code><br />
<code>0x2338: start_page (0x00000000)</code><br />
<code>0x233C: length (variable)</code><br />
<code>0x2340: load_addr (0x40010000)</code><br />
<code>0x2344: entry_point (0x40010020)</code><br />
<code>0x2348: attribute (0x00000000)</code><br />
<code>0x234C: bootloader0_hash (empty)</code><br />
<code>0x235C: bootloader0_rsa_pss_signature</code></p></td>
</tr>
<tr class="odd">
<td><p>0x245C</p></td>
<td><p>0x12C</p></td>
<td><p>bootloader1_info</p></td>
<td><p>Configuration parameters for bootloader 1 (safe mode).</p>
<p><code>0x245C: version (variable)</code><br />
<code>0x2460: start_block (0x00000050)</code><br />
<code>0x2464: start_page (0x00000000)</code><br />
<code>0x2468: length (variable)</code><br />
<code>0x246C: load_addr (0x40010000)</code><br />
<code>0x2470: entry_point (0x40010020)</code><br />
<code>0x2474: attribute (0x00000000)</code><br />
<code>0x2478: bootloader1_hash (empty)</code><br />
<code>0x2488: bootloader1_rsa_pss_signature</code></p></td>
</tr>
<tr class="even">
<td><p>0x2588</p></td>
<td><p>0x258</p></td>
<td><p>reserved1</p></td>
<td><p>Reserved space for bootloaders 2 and 3 (currently unused).</p></td>
</tr>
<tr class="odd">
<td><p>0x27E0</p></td>
<td><p>0x01</p></td>
<td><p>enable_fail_back</p></td>
<td><p>Always 0.</p></td>
</tr>
<tr class="even">
<td><p>0x27E1</p></td>
<td><p>0x04</p></td>
<td><p>secure_debug_control</p></td>
<td><p>Always 0.</p></td>
</tr>
<tr class="odd">
<td><p>0x27E5</p></td>
<td><p>0x04</p></td>
<td><p>sec_provisioning_key_num_secure</p></td>
<td><p>Used for Factory Secure Provisioning. Always 0.</p></td>
</tr>
<tr class="even">
<td><p>0x27E9</p></td>
<td><p>0x12</p></td>
<td><p>reserved2</p></td>
<td><p>Always starts with 0x80000000 (NVBOOT padding pattern).</p></td>
</tr>
<tr class="odd">
<td><p>0x27FB</p></td>
<td><p>0x05</p></td>
<td><p>padding</p></td>
<td><p>Empty. Not part of BCT data.</p></td>
</tr>
<tr class="even">
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

### customer\_data

This data block is ignored by the boot ROM, therefore is available for
the programmer to use freely. The Switch uses 0xB0 bytes of this area,
at offset 0x0450, to store the active
[keyblob](Flash%20Filesystem#Keyblob.md##Keyblob "wikilink"). All
remaining bytes are zero.

The first bootloader validates and decrypts this block for further key
generation. The decrypted keyblob payload is as
follows.

| Offset | Size | Description                                              |
| ------ | ---- | -------------------------------------------------------- |
| 0x0    | 0x80 | Array of master static key encryption keys               |
| 0x80   | 0x10 | [Stage 1](Package1#Stage%201.md##Stage_1 "wikilink") key |

### bootloader0\_info

#### 1.0.0 - 2.3.0

The version field is set to 0x01, meaning that the first keyblob is to
be used.

#### 3.0.0

The version field was changed to 0x02, meaning that the second keyblob
is now used.

#### 3.0.1

The version field was changed to 0x03, meaning that the third keyblob is
now used.

## IRAM

When copied to IRAM, the BCT has an additional header as follows.

<table>
<thead>
<tr class="header">
<th><p>Offset</p></th>
<th><p>Size</p></th>
<th><p>Field</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x00</p></td>
<td><p>0x50</p></td>
<td><p>bct_global_header</p></td>
<td><p>Contains pointers to actual BCT data.</p>
<p><code>0x4C: bct_data_addr (address of the actual BCT)</code></p></td>
</tr>
<tr class="even">
<td><p>0x50</p></td>
<td><p>0x18</p></td>
<td><p>bootloader0_header</p></td>
<td><p>Unknown structure.</p>
<p><code>0x00: is_active (if set to 0x01, bootloader0 is used) </code></p></td>
</tr>
<tr class="odd">
<td><p>0x68</p></td>
<td><p>0x18</p></td>
<td><p>bootloader1_header</p></td>
<td><p>Unknown structure.</p>
<p><code>0x00: is_active (if set to 0x01, bootloader1 is used) </code></p></td>
</tr>
<tr class="even">
<td><p>0x80</p></td>
<td><p>0x18</p></td>
<td><p>bootloader2_header</p></td>
<td><p>Unknown structure.</p>
<p><code>0x00: is_active (if set to 0x01, bootloader2 is used) </code></p></td>
</tr>
<tr class="odd">
<td><p>0x98</p></td>
<td><p>0x18</p></td>
<td><p>bootloader3_header</p></td>
<td><p>Unknown structure.</p>
<p><code>0x00: is_active (if set to 0x01, bootloader3 is used) </code></p></td>
</tr>
<tr class="even">
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

BCT (Boot Configuration Table) is a data structure present on Tegra
based devices that supplies boot time configuration parameters.

The Switch's BCT is included in the firmware package titles
(0100000000000819 and 010000000000081A) and is installed into eMMC
storage's [boot partition
0](Flash%20Filesystem#Boot%20Partitions.md##Boot_Partitions "wikilink").
A total of four BCT copies can be installed into the system: normal,
normal backup, safe mode and safe mode backup.

By design, the BCT's data is only signed after offset 0x0510. Therefore,
regions like [CustomerData](#CustomerData "wikilink") can be freely
modified without resigning. This is done by
[NS](NS%20Services.md "wikilink") when injecting a new
[keyblob](Flash%20Filesystem#Keyblob.md##Keyblob "wikilink") during a
system update, for example.

During boot, the boot ROM parses the appropriate BCT from eMMC storage
and stores a copy of it in IRAM at address 0x40000000.

# Structure

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
<td><p>BadBlockTable</p></td>
<td><p>Table containing information on bad blocks</p>
<p><code>0x0000: EntriesUsed (0x200)</code><br />
<code>0x0004: VirtualBlockSizeLog2 (0x0F)</code><br />
<code>0x0005: BlockSizeLog2 (0x0E)</code><br />
<code>0x0006: BadBlocks</code><br />
<code>0x0206: Reserved</code></p></td>
</tr>
<tr class="even">
<td><p>0x0210</p></td>
<td><p>0x100</p></td>
<td><p>Key</p></td>
<td><p>BCT RSA public key's modulus</p></td>
</tr>
<tr class="odd">
<td><p>0x0310</p></td>
<td><p>0x110</p></td>
<td><p>Signature</p></td>
<td><p>BCT object signature</p>
<p><code>0x0310: CryptoHash (empty)</code><br />
<code>0x0320: RsaPssSig</code></p></td>
</tr>
<tr class="even">
<td><p>0x0420</p></td>
<td><p>0x04</p></td>
<td><p>SecProvisioningKeyNumInsecure</p></td>
<td><p>Used for Factory Secure Provisioning. Always 0.</p></td>
</tr>
<tr class="odd">
<td><p>0x0424</p></td>
<td><p>0x20</p></td>
<td><p>SecProvisioningKey</p></td>
<td><p>Used for Factory Secure Provisioning. Always empty.</p></td>
</tr>
<tr class="even">
<td><p>0x0444</p></td>
<td><p>0xC4</p></td>
<td><p><a href="#CustomerData" title="wikilink">CustomerData</a></p></td>
<td><p>Data block available for the customer. Used in key generation.</p>
<p><code>0x0444: Reserved (0x0C bytes)</code><br />
<code>0x0450: </code><a href="Flash Filesystem#Keyblob.md##Keyblob" title="wikilink"><code>Keyblob</code></a><code> (0xB0 bytes)</code><br />
<code>0x0500: Reserved (0x08 bytes)</code></p></td>
</tr>
<tr class="odd">
<td><p>0x0508</p></td>
<td><p>0x04</p></td>
<td><p>OdmData</p></td>
<td><p>Legacy field. Unused.</p></td>
</tr>
<tr class="even">
<td><p>0x050C</p></td>
<td><p>0x04</p></td>
<td><p>Reserved</p></td>
<td><p>Legacy field. Unused.</p></td>
</tr>
<tr class="odd">
<td><p>0x0510</p></td>
<td><p>0x10</p></td>
<td><p>RandomAesBlock</p></td>
<td><p>Always empty.</p></td>
</tr>
<tr class="even">
<td><p>0x0520</p></td>
<td><p>0x10</p></td>
<td><p>UniqueChipId</p></td>
<td><p>Always empty.</p></td>
</tr>
<tr class="odd">
<td><p>0x0530</p></td>
<td><p>0x04</p></td>
<td><p>BootDataVersion</p></td>
<td><p>Set to 0x00210001 (BOOTDATA_VERSION_T210).</p></td>
</tr>
<tr class="even">
<td><p>0x0534</p></td>
<td><p>0x04</p></td>
<td><p>BlockSizeLog2</p></td>
<td><p>Always 0x0E.</p></td>
</tr>
<tr class="odd">
<td><p>0x0538</p></td>
<td><p>0x04</p></td>
<td><p>PageSizeLog2</p></td>
<td><p>Always 0x09.</p></td>
</tr>
<tr class="even">
<td><p>0x053C</p></td>
<td><p>0x04</p></td>
<td><p>PartitionSize</p></td>
<td><p>Always 0x01000000.</p></td>
</tr>
<tr class="odd">
<td><p>0x0540</p></td>
<td><p>0x04</p></td>
<td><p>NumParamSets</p></td>
<td><p>Number of device parameter sets. Always 0x01.</p></td>
</tr>
<tr class="even">
<td><p>0x0544</p></td>
<td><p>0x04</p></td>
<td><p>DevType</p></td>
<td><p>Device type. Set to 0x04 (dev_type_sdmmc).</p></td>
</tr>
<tr class="odd">
<td><p>0x0548</p></td>
<td><p>0x40</p></td>
<td><p>DevParams</p></td>
<td><p>Device parameters</p>
<p><code> 0x0548: sdmmc_clock_divider (0x09 == 24MHz)</code><br />
<code> 0x054C: sdmmc_data_width (0x02 == sdmmc_data_width_8bit)</code></p></td>
</tr>
<tr class="even">
<td><p>0x0588</p></td>
<td><p>0x04</p></td>
<td><p>NumSdramSets</p></td>
<td><p>Number of SDRAM parameter sets. Always set to 0, but parameters are used despite this.</p></td>
</tr>
<tr class="odd">
<td><p>0x058C</p></td>
<td><p>0x768</p></td>
<td><p>SdramParams0</p></td>
<td><p>Default values filled in.</p></td>
</tr>
<tr class="even">
<td><p>0x0CF4</p></td>
<td><p>0x768</p></td>
<td><p>SdramParams1</p></td>
<td><p>Default values filled in.</p></td>
</tr>
<tr class="odd">
<td><p>0x145C</p></td>
<td><p>0x768</p></td>
<td><p>SdramParams2</p></td>
<td><p>Default values filled in.</p></td>
</tr>
<tr class="even">
<td><p>0x1BC4</p></td>
<td><p>0x768</p></td>
<td><p>SdramParams3</p></td>
<td><p>Default values filled in.</p></td>
</tr>
<tr class="odd">
<td><p>0x232C</p></td>
<td><p>0x04</p></td>
<td><p>BootLoadersUsed</p></td>
<td><p>Number of bootloaders installed. Always 0x02 (maximum is 0x04).</p></td>
</tr>
<tr class="even">
<td><p>0x2330</p></td>
<td><p>0x12C</p></td>
<td><p><a href="#BootLoader0" title="wikilink">BootLoader0</a></p></td>
<td><p>Configuration parameters for bootloader 0 (normal).</p>
<p><code>0x2330: Version (variable)</code><br />
<code>0x2334: StartBlock (0x00000040)</code><br />
<code>0x2338: StartPage (0x00000000)</code><br />
<code>0x233C: Length (variable)</code><br />
<code>0x2340: LoadAddress (0x40010000)</code><br />
<code>0x2344: EntryPoint (0x40010020 for 1.0.0-3.0.2, 0x40010040 for 4.0.0+)</code><br />
<code>0x2348: Attribute (0x00000000)</code><br />
<code>0x234C: CryptoHash (empty)</code><br />
<code>0x235C: RsaPssSig</code></p></td>
</tr>
<tr class="odd">
<td><p>0x245C</p></td>
<td><p>0x12C</p></td>
<td><p>BootLoader1</p></td>
<td><p>Configuration parameters for bootloader 1 (safe mode).</p>
<p><code>0x245C: Version (variable)</code><br />
<code>0x2460: StartBlock (0x00000050)</code><br />
<code>0x2464: StartPage (0x00000000)</code><br />
<code>0x2468: Length (variable)</code><br />
<code>0x246C: LoadAddress (0x40010000)</code><br />
<code>0x2470: EntryPoint (0x40010020 for 1.0.0-3.0.2, 0x40010040 for 4.0.0+)</code><br />
<code>0x2474: Attribute (0x00000000)</code><br />
<code>0x2478: CryptoHash (empty)</code><br />
<code>0x2488: RsaPssSig</code></p></td>
</tr>
<tr class="even">
<td><p>0x2588</p></td>
<td><p>0x12C</p></td>
<td><p>BootLoader2</p></td>
<td><p>Reserved space for bootloader 2 (unused).</p></td>
</tr>
<tr class="odd">
<td><p>0x26B4</p></td>
<td><p>0x12C</p></td>
<td><p>BootLoader3</p></td>
<td><p>Reserved space for bootloader 3 (unused).</p></td>
</tr>
<tr class="even">
<td><p>0x27E0</p></td>
<td><p>0x01</p></td>
<td><p>EnableFailBack</p></td>
<td><p>Always 0.</p></td>
</tr>
<tr class="odd">
<td><p>0x27E1</p></td>
<td><p>0x04</p></td>
<td><p>SecureJtagControl</p></td>
<td><p>Always 0.</p></td>
</tr>
<tr class="even">
<td><p>0x27E5</p></td>
<td><p>0x04</p></td>
<td><p>SecProvisioningKeyNumSecure</p></td>
<td><p>Used for Factory Secure Provisioning. Always 0.</p></td>
</tr>
<tr class="odd">
<td><p>0x27E9</p></td>
<td><p>0x12</p></td>
<td><p>Reserved</p></td>
<td><p>Always starts with 0x80000000 (NVBOOT padding pattern).</p></td>
</tr>
<tr class="even">
<td><p>0x27FB</p></td>
<td><p>0x05</p></td>
<td><p>Padding</p></td>
<td><p>Empty. Not part of BCT data.</p></td>
</tr>
</tbody>
</table>

## CustomerData

This data block is ignored by the boot ROM, therefore is available for
the programmer to use freely. The Switch uses 0xB0 bytes of this area,
at offset 0x0450, to store the active
[keyblob](Flash%20Filesystem#Keyblob.md##Keyblob "wikilink"). All
remaining bytes are zero.

The first bootloader validates and decrypts this block for further key
generation. The decrypted keyblob payload is as follows.

| Offset | Size | Description                                               |
| ------ | ---- | --------------------------------------------------------- |
| 0x0    | 0x80 | Array of master static key encryption keys                |
| 0x80   | 0x10 | [PK11](Package1#PK11%20Blob.md##PK11_Blob "wikilink") key |

## BootLoader0

The version field controls which keyblob is used, where 0x01 is the
first one. See [Cryptosystem](Cryptosystem.md "wikilink") for the
keyblobs used by each system-version.

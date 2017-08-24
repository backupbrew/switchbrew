boot is a built-in sysmodule.

# Boot

First, it initializes gpios and sets the gpio voltage to 1.8v.

Then it checks battery charge and SoC temperature using i2c. If either
is bad, it shows one of two different bitmaps from .data in the
framebuffer.

Because most sysmodules have not yet booted, this all uses raw IO pokes
when it comes to gpio and i2c interfacing.

Otherwise, it continues by reading the bad\_block\_table.num\_entries
field from the [BCT](BCT.md "wikilink") located at offset 0x00C000 in
the NAND [boot partition
0](Flash%20Filesystem#Boot%20Partitions.md##Boot_Partitions "wikilink")
(safe mode backup).

If bad\_block\_table.num\_entries byte0 is non-zero, it does a repair
with type=4. If byte1 is non-zero, it does a repair with type=5. The
number of entires in the bad block table should always be 0x200 by
default (represents partition\_size). Values from 0x200 to 0x20F
represent bad blocks in the NAND [boot partition
0](Flash%20Filesystem#Boot%20Partitions.md##Boot_Partitions "wikilink")
while values from 0x210 to 0x21F represent bad blocks in NAND [boot
partition
1](Flash%20Filesystem#Boot%20Partitions.md##Boot_Partitions "wikilink").

## Repair

It uses the NCM
[IContentMetaDatabase](NCM%20services#IContentMetaDatabase.md##IContentMetaDatabase "wikilink")
Iterate command with the supplied type value in order to look up the
firmware package ("bip") title-id (0100000000000819 or
010000000000081A).

It then mounts the firmware package at "bip" and reads the
[BCT](BCT.md "wikilink") from the "bip:/nx/bct" file in that filesystem.
Afterwards, the console's
[keyblob](Flash%20Filesystem#Keyblob.md##Keyblob "wikilink") is read
from the NAND keyblob array using
[bootloader0\_info.version](BCT#bootloader0%20info.md##bootloader0_info "wikilink")
as index and the selected keyblob is then injected into the BCT's
[customer\_data](BCT#customer%20data.md##customer_data "wikilink")
region.

A SHA-256 hash is then calculated over this new BCT and compared against
calculated hashes of the actual BCTs stored in NAND. For a type4 repair
process, the comparison is performed with "normal" and "normal backup"
BCTs (offsets 0x0000 and 0x8000 in NAND). For a type5 repair process,
the comparison is performed with "safe mode" and "safe mode backup" BCTs
(offsets 0x4000 and 0xC000 in NAND). If either hash doesn't match the
calculated one, it returns error 0xC9E.

The same process is repeated for the [package1](Package1.md "wikilink")
file in "bip:/nx/package1". This file's SHA-256 hash is compared against
calculated hashes over the package1 copy stored in NAND. For a type4
repair process, the comparison is performed with "normal" and "normal
backup" package1 (offsets 0x100000 and 0x140000 in NAND boot partition
0). For a type5 repair process, the comparison is performed with "safe
mode" and "safe mode backup" package1 (offsets 0x00000 and 0x40000 in
NAND boot partition 1). If either hash doesn't match the calculated one,
it returns error 0xC9E.

Finally, the process is repeated once more for the "bip:/nx/package2".
Error 0xC9E is returned in case of mismatch.

If this function returns 0xC9E, it calls a function to repair the NAND.

## Done

When done it calls the
[pm:shell](Process%20Manager%20services.md "wikilink")
NotifyBootCompleted (which launches [boot2](Boot2.md "wikilink")), and
exits itself.

# Changelog

## 2.0.0

  - All panic strings were removed/censored.
  - Code to initialize gpio differently for Copper/Icosa (based on spl
    HardwareType flag) was removed.
  - The "WecDriver" now uses svcReadWriteRegister instead of
    svcQueryIoMapping to write to 0x7000E400 MMIO (PMC).

## 2.1.0

  - Code was updated with changes to the NCM interface.

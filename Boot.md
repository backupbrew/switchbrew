boot is a built-in sysmodule.

\[2.0.0+\] all panic strings were removed/censored.

\[2.1.0+\] code was updated with changes to the ncm interface.

# Boot

First up it initializes gpios and sets the gpio voltage to 1.8v.

\[2.0.0+\] Code to initialize gpio differently for Copper/Icosa (based
on spl HardwareType flag) was removed.

\[2.0.0+\] the "WecDriver" now uses svcReadWriteRegister instead of
svcQueryIoMapping to write to 0x7000E400 io (PMC).

Then it checks battery charge and SoC temperature using i2c. If either
is bad, it shows one of two different bitmaps from .data in the
framebuffer.

Because most sysmodules have not yet booted, this all uses raw IO pokes
when it comes to gpio and i2c interfacing.

Otherwise, it continues by reading the first two bytes of the BCT at
+0xC000 of NAND partition 0.

If byte0 is non-zero, it does a repair with type=4. If byte1 is
non-zero, it does a repair with type=5.

## Repair

It uses ncm IContentMetaDatabase Iterate with supplied type value. The
purpose of this ncm usage is to look up the "bip" title-id
(0100000000000819 or 010000000000081A) for said type.

It mounts the found bip title-id at "bip", reads the "bip:/nx/bct" file
in that filesystem. Then it reads the console-unique keyblobs from NAND,
and injects the keyblob based on the u32-index at BCT+0x2330 into the
BCT buffer+0x450.

It calculates a sha256 of this "constructed" bct buffer.

Then it hashes two bcts from actual in partition 0 (type4: NAND+0x0000
and NAND+0x8000, type5: NAND+0x4000 and NAND+0xC000). If either hash
doesn't match the calculated one, it returns error 0xC9E.

Then it reads and hashes entire "bip:/nx/package1" using sha256. It
checks if this matches a hash of the two real pkg1 stored in (type4:
partition0 NAND+0x100000 and NAND+0x140000, type5: partition1 NAND+0 and
NAND+0x40000). Same error is returned on hash mismatch.

After that it also checks the hash of "nx/package2" against two pkg2s
stored in NAND, also error 0xC9E if hash doesn't match.

If this function returns 0xC9E, it calls a function to repair the NAND.

## Done

When done it calls the
[pm:shell](Process%20Manager%20services.md "wikilink")
NotifyBootCompleted (which launches [boot2](Boot2.md "wikilink")), and
exits itself.

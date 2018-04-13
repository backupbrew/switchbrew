The Recovery Mode (also known as Maintenance Mode in firmware version
1.0.0) can be accessed when turning on the Nintendo Switch while
performing a button combo.

# Description

After [package1ldr](Package1#Package1ldr.md##Package1ldr "wikilink")
decrypts and validates
[package1](Package1#Package1%20.28PK11.29.md##Package1_.28PK11.29 "wikilink"),
execution carries over into the [NX
bootloader](Package1#Section%201.md##Section_1 "wikilink").

Among various tasks, this bootloader checks for a button combination to
determine if the system should enter Recovery Mode. If the combination
is performed, the bootloader reads the [SafeMode Firmware
BCT](Flash%20Filesystem#Boot%20Partitions.md##Boot_Partitions "wikilink")
from the eMMC, swaps the normal [BCT](BCT.md "wikilink") with it and
performs a Watchdog reset after writing [panic code
0x20](Panic%20codes.md "wikilink") to **PMC\_SCRATCH200**.

# Button combination

In order to enter Recovery Mode, the following combination must be
performed:

\[1.0.0-3.0.2\]

  - With the system powered off, press and hold Volume Down + Volume Up;
  - Press the Power button while still holding Volume Down + Volume Up;
  - Let go of the Power button and keep holding Volume Down + Volume Up
    until the
    [maintenance](Title%20list#System%20Applets.md##System_Applets "wikilink")
    applet shows up.

This results in the system booting into a menu that allows to update
your Nintendo Switch through the internet and format/initialize the
console with or without keeping user info, screenshots and saves. It is
possible to use this menu to delete the nagging update message if your
console downloaded an update.

The \[1.0.0\] variant (known as Maintenance Mode) does not have the
system update option. However, downloaded update data is still deleted
when this menu is accessed.

\[4.0.0+\]

  - With the system powered off, press and hold Volume Down;
  - Press the Power button while still holding Volume Down;
  - Keep pressing the Power button, but let go of Volume Down and press
    and hold Volume Up;
  - Let go of the Power button and keep holding Volume Up until the
    [safemode](Safemode.md "wikilink") system module starts.

This results in the system booting into
[safemode](Safemode.md "wikilink") and automatically finding and
installing new updates from the internet.

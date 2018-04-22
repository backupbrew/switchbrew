The Nintendo Switch's Horizon OS supports different boot modes to allow
system recovery and general maintenance.

# Recovery Mode

The Recovery Mode (also known as Maintenance Mode in firmware version
1.0.0) can be accessed when turning on the Nintendo Switch while
performing a button combo.

## Description

The [boot2](Boot2.md "wikilink") sysmodule is responsible for checking
whether the system should go into Recovery Mode or not. This is done by
looking for a particular system setting ("force\_maintenance") or by
checking the GPIOs for a specific button combination.

## Button combination

In order to enter Recovery Mode, the following combination must be
performed:

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

# Safe Mode

The Safe Mode can be accessed when turning on the Nintendo Switch while
performing a button combo.

## Description

After [package1ldr](Package1#Package1ldr.md##Package1ldr "wikilink")
decrypts and validates
[package1](Package1#Package1%20.28PK11.29.md##Package1_.28PK11.29 "wikilink"),
execution carries over into the [NX
bootloader](Package1#Section%201.md##Section_1 "wikilink").

Among various tasks, this bootloader checks for a button combination to
determine if the system should enter Safe Mode. If the combination is
performed, the bootloader reads the [SafeMode Firmware
BCT](Flash%20Filesystem#Boot%20Partitions.md##Boot_Partitions "wikilink")
from the eMMC, swaps the normal [BCT](BCT.md "wikilink") with it and
performs a Watchdog reset after writing [panic code
0x20](Panic%20codes.md "wikilink") to **PMC\_SCRATCH200**.

\[1.0.0-3.0.2\] Entering Safe Mode forces the system to use [Firmware
Package
B](Title%20list#System%20Data%20Archives.md##System_Data_Archives "wikilink"),
which is nearly identical to [Firmware Package
A](Title%20list#System%20Data%20Archives.md##System_Data_Archives "wikilink"),
with the exception of containing different code for the built-in
sysmodules [FS](Filesystem%20services.md "wikilink") and
[boot](Boot.md "wikilink").

When coming from the Watchdog reset, the [NX
bootloader](Package1#Section%201.md##Section_1 "wikilink") checks if the
system is running in Safe Mode by looking at the current bootloader's
index. If the index is not 0, the screen is briefly painted with the
[panic color 0xFFFFAA](Panic%20codes.md "wikilink") and execution
continues into the [Recovery Mode](Recovery%20Mode.md "wikilink").

\[4.0.0+\] Entering Safe Mode forces the system to use [Firmware Package
B](Title%20list#System%20Data%20Archives.md##System_Data_Archives "wikilink")
or [Firmware Package
D](Title%20list#System%20Data%20Archives.md##System_Data_Archives "wikilink"),
but these now differ significantly from their normal counterparts. In
addition to containing different code for the
[FS](Filesystem%20services.md "wikilink") and [boot](Boot.md "wikilink")
built-in sysmodules, [NCM](NCM%20services.md "wikilink") and
[PM](Process%20Manager%20services.md "wikilink") are now changed to
allow content database reconstruction and booting the new
[safemode](Safemode.md "wikilink") sysmodule. Due to the additional
dependencies of this process [PCV](PCV%20services.md "wikilink"),
[psc](PSC%20services.md "wikilink") and
[bus](Bus%20services.md "wikilink") sysmodules are now bundled with the
kernel (only in Safe Mode firmware).

The screen painting routine when coming from the Watchdog reset was
removed.

## Button combination

In order to enter Safe Mode, the following combination must be
performed:

\[1.0.0-3.0.2\]

Same combination used for [Recovery
Mode](Recovery%20Mode.md "wikilink").

\[4.0.0+\]

  - With the system powered off, press and hold Volume Down;
  - Press the Power button while still holding Volume Down;
  - Keep pressing the Power button, but let go of Volume Down and press
    and hold Volume Up;
  - Let go of the Power button and keep holding Volume Up until the
    [safemode](Safemode.md "wikilink") system module starts.

This results in the system booting the
[safemode](Safemode.md "wikilink") sysmodule and automatically finding
and installing new updates from the internet.

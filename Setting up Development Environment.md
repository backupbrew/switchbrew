# Setup

Install [devkitA64](https://devkitpro.org/). If it's already installed,
update it using sudo (dkp-)pacman -Syu. On Windows, there's a [graphical
installer](https://github.com/devkitPro/installer/releases/latest). On
Unix-like platforms such as Linux/macOS, there's
[pacman](https://github.com/devkitPro/pacman/releases/latest).

[devkitPro](https://devkitpro.org) also provides a set of [Docker
images](https://hub.docker.com/u/devkitpro/) which come pre-installed
with all the portlibs packages.

**Please note: devkitPro is the organisation that provides the tools.
They are not a software package, they don't have version numbers and the
only way to have them compile your code is to pay them (or maybe if you
ask nicely when you need help figuring out an issue)**

## Windows

devkitPro provides 64-bit precompiled Windows binaries of devkitA64
which can be run directly on Windows.

  - If you already use msys2 then you can follow the instructions at
    <https://github.com/devkitPro/pacman/releases/latest> to add the
    devkitPro repositories.

Otherwise

  - [download the latest version of the graphical
    installer](https://github.com/devkitPro/installer/releases) from
    github and run it, following the instructions as you go.
  - An Internet connection is required.
  - Ensure at least "Switch Development" is ticked - you can also leave
    the other options ticked if you wish.
  - Once the installer has finished, launch MSYS from:
      - Windows 7 and earlier: Start -\> All Programs -\> devkitPro -\>
        MSYS
      - Windows 8 and 8.1: Right click on the Start screen and select
        'All Apps'. You should find MSYS there.
      - Windows 10 (pre-Anniversary Update): Start -\> All Apps -\>
        devkitPro -\> MSYS
      - Windows 10 (post-Anniversary Update): Start -\> devkitPro -\>
        MSYS

## Unix-like platforms

Currently devkitPro provides precompiled versions of devkitA64 for the
following Unix-like platforms: Linux (x86\_64), macOS (x86\_64). Note
that Linux x86\_64 binaries are usable under WSL.

  - Follow the instructions to install pacman found at
    <https://github.com/devkitPro/pacman/releases/latest>
  - run sudo (dkp-)pacman -S switch-dev to install the tools and
    libraries for switch development
  - logout and login again to get the environment settings needed.

# Building the examples

Switch examples are still being created; however, there are a growing
number of examples available from the [switchbrew/switch-examples GitHub
repository](https://github.com/switchbrew/switch-examples). These are
downloaded by the installer and can be found in
$DEVKITPRO/examples/switch

These can be built from the command line.

To start a new homebrew project from the `bash` shell, simply type the
following (replacing **`~/projects/myswitchproject`** with the place you
would like your project to be stored, with `~` meaning your HOME
directory):

`cp -r $DEVKITPRO/examples/switch/templates/application `**`~/projects/myswitchproject`**  
`cd `**`~/projects/myswitchproject`**

The standard Makefile will use the folder as the name of the .nro that
will be built. You can keep that behaviour or simply change the `TARGET
:= $(notdir $(CURDIR))` line in the Makefile to explicitly name your
project.

To compile it, type `make` in the project directory.

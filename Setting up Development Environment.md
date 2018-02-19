# Setup

Install [devkitA64](http://devkitpro.org/). If it's already installed,
update it. On Windows, there's a [graphical
installer](https://github.com/devkitPro/installer/releases). On
Unix-like platforms such as Linux/macOS, there's a [Perl
script](https://github.com/devkitPro/installer/blob/master/perl/devkitA64update.pl).
Make sure you also select libnx and the switch examples when installing.

## Windows

devkitPro provides 64bit precompiled windows binaries of devkitA64 which
can be run directly on Windows.

  - [download the latest version of the graphical
    installer](https://github.com/devkitPro/installer/releases) from
    github and run it, following the instructions as you go.
  - An Internet connection is required.
  - You will want to make sure devkitA64 is selected during the
    installation process to develop for the Switch - you can also
    install devkitARM (for 3DS, DS and GBA) and devkitPPC (for
    GameCube/Wii development) if you wish.
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

Currently devkitPro provides precompiled versions of devkitARM for the
following Unix-like platforms: Linux (x86\_64), macOS (x86\_64). Note
that Linux x86\_64 binaries are usable under WSL.

  - First, you need to install curl so the installer can download the
    devkitARM packages, and you should also install Git - you'll need it
    to update libnx or share your code on GitHub, among many other
    things. If you are running Linux, you'll also need wget; it comes
    preinstalled on most distributions, but not all.

<!-- end list -->

  - Find your way into a shell (eg. by opening a Terminal window), and
    follow the instructions for your OS:
      - Debian/Ubuntu/Linux Mint/Ubuntu on WSL: `sudo apt-get install
        git curl`
      - Fedora/CentOS/RHEL: `sudo yum install git curl`
      - openSUSE: `sudo zypper install git curl`
      - Arch Linux/ALWSL: `sudo pacman -S git curl wget`
      - macOS: Download Git from [1](http://git-scm.com/download/mac)
        and install it. Curl is included with the OS.

<!-- end list -->

  - We can set the DEVKITPRO environment variable first so the script
    knows where to install or we can set the variable later to the value
    the script tells us. The script will default this to ~/devkitPro

<!-- end list -->

    echo "export DEVKITPRO=/opt/devkitpro" >> ~/.bashrc
    source ~/.bashrc

  - Next, we need to download, make executable and run the devkitARM
    updater (don't worry, the updater is also the
    installer.)

<!-- end list -->

    curl -L https://github.com/devkitPro/installer/blob/master/perl/devkitA64update.pl -o devkitA64update.pl
    chmod +x ./devkitA64update.pl
    ./devkitA64update.pl

You may need to use sudo here if you set DEVKITPRO to a path not
writable by your user.

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

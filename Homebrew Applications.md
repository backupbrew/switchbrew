## Installing

Applications are installed by copying the necessary files directly to
the `switch/` folder in the root of the SD card, or in a subdirectory of
`switch/`, in which case said subfolder must be named identically to its
executable. Normally the former should be used. The latter should be
used if the application uses anything from FS current-working-directory
(directory where the NRO is located). Applications come with the
following:

  - `[appname].nro`: The executable.

The Homebrew Menu will scan the SD card for all `.nro` files, but will
only display an icon for those who have one according to the format
described above. You can also freely navigate the filesystem to select
an application.

Icon/metadata for each application is loaded from data embedded in the
NRO (custom assets section), if
available.

## List

### Launchers

| Name                                                     | Description                   | Author                                                                   | Download                                                 | Open-Source |
| -------------------------------------------------------- | ----------------------------- | ------------------------------------------------------------------------ | -------------------------------------------------------- | ----------- |
| [Homebrew Menu](https://github.com/switchbrew/nx-hbmenu) | Run homebrew on your Switch\! | [Yellows8](User:Yellows8 "wikilink"), [plutooo](User:plutooo "wikilink") | [Here](https://github.com/switchbrew/nx-hbmenu/releases) | Yes         |
|                                                          |                               |                                                                          |                                                          |             |

### Applications

| Name                                                              | Description                                                                                        | Author                                       | Download                                               | Open-Source                                   | Last Updated |
| ----------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------- | ------------------------------------------------------ | --------------------------------------------- | ------------ |
| [switch\_sysmodule](https://github.com/yellows8/switch_sysmodule) | RPC over USB, etc. Originally a sysmodule, however this can also be used as a regular application. | [Yellows8](User:Yellows8 "wikilink")         |                                                        | Yes                                           |              |
| [AppStore NX](https://www.switchbru.com/appstore/)                | Download and manage homebrew apps                                                                  | vgmoose                                      | [Here](https://github.com/vgmoose/appstorenx/releases) | [Yes](https://github.com/vgmoose/appstorenx/) | 2018-03-05   |
| Pynx                                                              | Allows you to run homebrew applications written in Python on the Switch.                           | [AileenLumina](User:AileenLumina "wikilink") | [Here](https://github.com/nx-python/Pynx/releases)     | [Yes](https://github.com/nx-python/Pynx/)     | 2018-03-19   |
|                                                                   |                                                                                                    |                                              |                                                        |                                               |              |

### Game Engines

| Name                                                                                                         | Description                                      | Author                        | Download                                      | Open-Source                                              | Last Updated |
| ------------------------------------------------------------------------------------------------------------ | ------------------------------------------------ | ----------------------------- | --------------------------------------------- | -------------------------------------------------------- | ------------ |
| LovePotion                                                                                                   | [Love2D](https://love2d.org) for Nintendo Switch | TurtleP                       |                                               | [Yes](https://github.com/TurtleP/LovePotion/tree/switch) | 2018-04-11   |
| [EasyRPG Player](https://blog.easyrpg.org/2018/03/easyrpg-player-now-available-as-nintendo-switch-homebrew/) | RPG Maker 2000/2003 game interpreter             | Rinnegatamante & EasyRPG team | [here](https://easyrpg.org/player/downloads/) | [Yes](https://github.com/EasyRPG/Player)                 | 2018-03-09   |
|                                                                                                              |                                                  |                               |                                               |                                                          |              |

### Games

| Name                   | Description                                                                                                                                                                                                                                                                                                                                                             | Author                                     | Download                                                                         | Open-Source                                                  | Last Updated |
| ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------ | -------------------------------------------------------------------------------- | ------------------------------------------------------------ | ------------ |
| Useless Homebrew       | A "useless machine"-like software, ported from DS                                                                                                                                                                                                                                                                                                                       | Tcm0, Rydian (DS)                          | [Here](https://gbatemp.net/threads/useless-homebrew-for-nintendo-switch.497041/) | Yes                                                          | 2018-03-03   |
| Space Game NX          | Space game is a graphical shooter game on the Switch ported from Wii U\!                                                                                                                                                                                                                                                                                                | vgmoose                                    | [Here](https://github.com/vgmoose/spacenx/releases)                              | [Yes](https://github.com/vgmoose/spacenx/)                   | 2018-02-19   |
| Pixel-Painter          | A simple drawing homebrew                                                                                                                                                                                                                                                                                                                                               | 8BitWonder                                 | [Here](https://github.com/16BitWonder/Pixel-Painter-Switch/releases)             | [Yes](https://github.com/16BitWonder/Pixel-Painter-Switch)   | 2018-02-21   |
| Hamsters NX            | A breeding of Hamsters game in text mode.                                                                                                                                                                                                                                                                                                                               | Cid2mizard                                 | [Here](https://github.com/Cid2mizard/Hamsters_NX/releases)                       | [Yes](https://github.com/Cid2mizard/Hamsters_NX)             | 2018-02-28   |
| OpenBOR                | OpenBOR is the ultimate 2D gaming engine with over 10+ years of active development behind it. With OpenBOR you can build anything from simple button mashers to elaborate projects rivaling the most lavish professional offerings. Download one of the dozens of ready to play game modules available here, or grab the development kit and start up one of your own\! | cpasjuste                                  | [Here](https://github.com/Cpasjuste/openbor/releases)                            | [Yes](https://github.com/Cpasjuste/openbor)                  | 2018-03-18   |
| TicTacToe              | A Tic Tac Toe implementation for Switch.                                                                                                                                                                                                                                                                                                                                | SH3RLOCK                                   | [Here](https://sh3rlock.ch/ttt.nro)                                              | [Yes](https://sh3rlock.ch/ttt.zip)                           | 2018-02-23   |
| SDLLopan               | A classic remake of Linux Lopan (a Mahjong solitaire clone) by Dave Ashley.                                                                                                                                                                                                                                                                                             | nop90                                      | [Here](https://github.com/Nop90-Switch/SDLLopan-SWITCH/releases)                 | [Yes](https://github.com/Nop90-Switch/SDLLopan-SWITCH)       | 2018-03-02   |
| Tetriswitch            | A Tetris clone for Nintendo Switch.                                                                                                                                                                                                                                                                                                                                     | Ryuzaki\_MrL                               | [Here](https://github.com/Ryuzaki-MrL/tetriswitch/releases)                      | [Yes](https://github.com/Ryuzaki-MrL/tetriswitch)            | 2018-03-13   |
| Snake                  | A minimalistic Snake clone for Switch made with LovePotion.                                                                                                                                                                                                                                                                                                             | Shrike                                     | [Here](https://github.com/Ryuzaki-MrL/tetriswitch/releases)                      |                                                              | 2018-03-10   |
| Meritous               | Top View Dungeon Game                                                                                                                                                                                                                                                                                                                                                   | nop90                                      | [Here](https://github.com/Nop90-Switch/Meritous-Switch/releases)                 | [Yes](https://github.com/Nop90-Switch/Meritous-Switch)       | 2018-03-17   |
| HCL-switch             | A port of Hydra Castle Labyrinth for PSVITA.                                                                                                                                                                                                                                                                                                                            | Rinnegatamante                             | [Here](https://www.switchbru.com/appstore/zips/HCL-switch.zip)                   | [Yes](https://github.com/Rinnegatamante/HCL-Switch)          | 2018-03-03   |
| REminiscence           | REminiscence is a re-implementation of the engine used in the game Flashback made by Delphine Software and released in 1992.                                                                                                                                                                                                                                            | Cpasjuste                                  | [Here](https://github.com/Cpasjuste/REminiscence/releases)                       | [Yes](https://github.com/Cpasjuste/REminiscence)             | 2018-03-28   |
| Super Methane Brothers | An elimination platformer remake similar to Bubble Bobble (originally released for AMIGA in 1993). Blast baddies with your methane gun and survive 100 floors in the tower of time.                                                                                                                                                                                     | [carstene1ns](User:carstene1ns "wikilink") | [Here](https://f4ke.de/dev/switch/)                                              | [Yes](https://github.com/carstene1ns/super-methane-brothers) | 2018-04-07   |
|                        |                                                                                                                                                                                                                                                                                                                                                                         |                                            |                                                                                  |                                                              |              |

### Emulators

| Name                      | Description                                                                                               | Author                             | Download                                                               | Open-Source                                             | Last Updated |
| ------------------------- | --------------------------------------------------------------------------------------------------------- | ---------------------------------- | ---------------------------------------------------------------------- | ------------------------------------------------------- | ------------ |
| ScummVM                   | ScummVM is a program which allows you to run certain classic graphical point-and-click adventure games... | Cpasjuste                          | [Here](https://github.com/Cpasjuste/scummvm/releases)                  | [Yes](https://github.com/Cpasjuste/scummvm/tree/switch) | 2018-03-01   |
| pFBA                      | A port of final burn alpha to multiple platforms                                                          | Cpasjuste                          | [Here](https://github.com/Cpasjuste/pfba/releases)                     | [Yes](https://github.com/Cpasjuste/pfba)                | 2018-02-20   |
| Snes9x 2010               | Super Nintendo Entertainment System (SNES) Emulator                                                       |                                    | [Here](https://gbatemp.net/attachments/snes2x2010-rar.116906/)         |                                                         | 2018-03-08   |
| FCEUmm RetroArch          | Nintendo Entertainment System (NES) Emulator                                                              |                                    | [Here](https://gbatemp.net/attachments/libretro-fceumm-rar.116907/)    |                                                         | 2018-03-08   |
| Virtual Jaguar RetroArch  | Atari Jaguar Emulator                                                                                     |                                    | [Here](https://gbatemp.net/attachments/virtual_jaguar-nro-zip.117971/) |                                                         | 2018-03-19   |
| mGBA RetroArch            | Gameboy, Gameboy Color, and Gameboy Advance Emulator. Unofficial build.                                   | [endrift](User:Endrift "wikilink") | [Here](https://gbatemp.net/attachments/mgba-nro-zip.116720/)           |                                                         | 2018-03-19   |
| GearBoy RetroArch         | Gameboy and Gameboy Color Emulator                                                                        |                                    | [Here](https://gbatemp.net/attachments/gearboy-nro-zip.116723/)        |                                                         | 2018-01-18   |
| gambatte RetroArch        | Gameboy and Gameboy Color Emulator                                                                        | sinamas                            | [Here](https://gbatemp.net/attachments/gambatte_fix-nro-zip.117249/)   |                                                         | 2018-01-18   |
| Picodrive RetroArch       | Genesis, MegaDrive, Master System, 32x, and Sega CD Emulator                                              |                                    | [Here](https://gbatemp.net/attachments/picodrive-nro-zip.117920/)      |                                                         | 2018-03-19   |
| Genesis Plus GX RetroArch | Genesis, MegaDrive, Master System, Game Gear, and Sega CD Emulator                                        | eke-eke                            | [Here](https://gbatemp.net/attachments/genesisgx-nro-zip.116038/)      |                                                         | 2018-03-19   |
| MAME 2003 RetroArch       | Multi-purpose emulation framework, Arcade game Emulator                                                   |                                    | [Here](https://gbatemp.net/attachments/mame2003-nro-zip.117945/)       |                                                         | 2018-03-19   |
| Beetle PSX RetroArch      | Playstation Emulator                                                                                      | Ryphecha                           | [Here](https://gbatemp.net/attachments/beetlepsx-nro-zip.116708/)      |                                                         | 2018-03-19   |

### Title managers

| Name | Description | Author | Download | Open-Source | Last Updated |
| ---- | ----------- | ------ | -------- | ----------- | ------------ |
|      |             |        |          |             |              |

### Save managers

| Name | Description | Author | Download | Open-Source | Last Updated |
| ---- | ----------- | ------ | -------- | ----------- | ------------ |
|      |             |        |          |             |              |

### File servers

| Name | Description             | Author         | Download                                                 | Open-Source                                         | Last Updated |
| ---- | ----------------------- | -------------- | -------------------------------------------------------- | --------------------------------------------------- | ------------ |
| Ftpd | A port of ftpd for 3DS. | mtheall, TuxSH | [Here](https://www.switchbru.com/appstore/zips/ftpd.zip) | [Yes](https://github.com/TuxSH/ftpd/tree/switch_pr) | 2018-02-27   |
|      |                         |                |                                                          |                                                     |              |

### Demos

| Name      | Description                                    | Author                           | Download                                        | Open-Source | Last Updated |
| --------- | ---------------------------------------------- | -------------------------------- | ----------------------------------------------- | ----------- | ------------ |
| 34c3-demo | Demo from the 34c3 for Homebrew on the Switch. | [plutoo](User:plutoo "wikilink") | [Here](https://github.com/switchbrew/34c3-demo) | Yes         | 2018-02-19   |
|           |                                                |                                  |                                                 |             |              |

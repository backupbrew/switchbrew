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

| Name                                                              | Description                                                                                        | Author                               | Download | Open-Source | Last Updated |
| ----------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- | ------------------------------------ | -------- | ----------- | ------------ |
| [switch\_sysmodule](https://github.com/yellows8/switch_sysmodule) | RPC over USB, etc. Originally a sysmodule, however this can also be used as a regular application. | [Yellows8](User:Yellows8 "wikilink") |          | Yes         |              |

### Game Engines

| Name                                                                                                         | Description                                      | Author                        | Download                                      | Open-Source                                              | Last Updated |
| ------------------------------------------------------------------------------------------------------------ | ------------------------------------------------ | ----------------------------- | --------------------------------------------- | -------------------------------------------------------- | ------------ |
| LovePotion                                                                                                   | [Love2D](https://love2d.org) for Nintendo Switch | TurtleP                       |                                               | [Yes](https://github.com/TurtleP/LovePotion/tree/switch) | 2018-03-02   |
| [EasyRPG Player](https://blog.easyrpg.org/2018/03/easyrpg-player-now-available-as-nintendo-switch-homebrew/) | RPG Maker 2000/2003 game interpreter             | Rinnegatamante & EasyRPG team | [here](https://easyrpg.org/player/downloads/) | [Yes](https://github.com/EasyRPG/Player)                 | 2018-03-09   |
|                                                                                                              |                                                  |                               |                                               |                                                          |              |

### Games

| Name             | Description                                                                                                                                                                                                                                                                                                                                                             | Author            | Download                                                                         | Open-Source                                                | Last Updated |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- | -------------------------------------------------------------------------------- | ---------------------------------------------------------- | ------------ |
| Useless Homebrew | A "useless machine"-like software, ported from DS                                                                                                                                                                                                                                                                                                                       | Tcm0, Rydian (DS) | [Here](https://gbatemp.net/threads/useless-homebrew-for-nintendo-switch.497041/) | Yes                                                        | 2018-03-03   |
| Space Game NX    | Space game is a graphical shooter game on the Switch ported from Wii U\!                                                                                                                                                                                                                                                                                                | vgmoose           | [Here](https://github.com/vgmoose/spacenx/releases)                              | [Yes](https://github.com/vgmoose/spacenx/)                 | 2018-02-19   |
| Pixel-Painter    | A simple drawing homebrew                                                                                                                                                                                                                                                                                                                                               | 8BitWonder        | [Here](https://github.com/16BitWonder/Pixel-Painter-Switch/releases)             | [Yes](https://github.com/16BitWonder/Pixel-Painter-Switch) | 2018-02-21   |
| Hamsters NX      | A breeding of Hamsters game in text mode.                                                                                                                                                                                                                                                                                                                               | Cid2mizard        | [Here](https://github.com/Cid2mizard/Hamsters_NX/releases)                       | [Yes](https://github.com/Cid2mizard/Hamsters_NX)           | 2018-02-28   |
| OpenBOR          | OpenBOR is the ultimate 2D gaming engine with over 10+ years of active development behind it. With OpenBOR you can build anything from simple button mashers to elaborate projects rivaling the most lavish professional offerings. Download one of the dozens of ready to play game modules available here, or grab the development kit and start up one of your own\! | cpasjuste         | [Here](https://github.com/Cpasjuste/openbor/releases)                            | [Yes](https://github.com/Cpasjuste/openbor)                | 2018-03-18   |
| TicTacToe        | A Tic Tac Toe implementation for Switch.                                                                                                                                                                                                                                                                                                                                | SH3RLOCK          | [Here](https://sh3rlock.ch/ttt.nro)                                              | [Yes](https://sh3rlock.ch/ttt.zip)                         | 2018-02-23   |
| SDLLopan         | A classic remake of Linux Lopan (a Mahjong solitaire clone) by Dave Ashley.                                                                                                                                                                                                                                                                                             | nop90             | [Here](https://github.com/Nop90-Switch/SDLLopan-SWITCH/releases)                 | [Yes](https://github.com/Nop90-Switch/SDLLopan-SWITCH)     | 2018-03-02   |
| Tetriswitch      | A Tetris clone for Nintendo Switch.                                                                                                                                                                                                                                                                                                                                     | Ryuzaki\_MrL      | [Here](https://github.com/Ryuzaki-MrL/tetriswitch/releases)                      | [Yes](https://github.com/Ryuzaki-MrL/tetriswitch)          | 2018-03-13   |
| Snake            | A minimalistic Snake clone for Switch made with LovePotion.                                                                                                                                                                                                                                                                                                             | Shrike            | [Here](https://github.com/Ryuzaki-MrL/tetriswitch/releases)                      |                                                            | 2018-03-10   |
| Meritous         | Top View Dungeon Game                                                                                                                                                                                                                                                                                                                                                   | nop90             | [Here](https://github.com/Nop90-Switch/Meritous-Switch/releases)                 | [Yes](https://github.com/Nop90-Switch/Meritous-Switch)     | 2018-03-17   |
| HCL-switch       | A port of Hydra Castle Labyrinth for PSVITA.                                                                                                                                                                                                                                                                                                                            | Rinnegatamante    | [Here](https://www.switchbru.com/appstore/zips/HCL-switch.zip)                   | [Yes](https://github.com/Rinnegatamante/HCL-Switch)        | 2018-03-03   |
|                  |                                                                                                                                                                                                                                                                                                                                                                         |                   |                                                                                  |                                                            |              |

### Emulators

| Name                    | Description                                                        | Author    | Download                                                               | Open-Source                              | Last Updated |
| ----------------------- | ------------------------------------------------------------------ | --------- | ---------------------------------------------------------------------- | ---------------------------------------- | ------------ |
| pFBA                    | A port of final burn alpha to multiple platforms                   | cpasjuste | [Here](https://github.com/Cpasjuste/pfba/releases)                     | [Yes](https://github.com/Cpasjuste/pfba) | 2018-02-20   |
| Snes9x 2010             | Super Nintendo Entertainment System (SNES) Emulator                |           | [Here](https://gbatemp.net/attachments/snes2x2010-rar.116906/)         |                                          | 2018-03-08   |
| FCEUMM (NES)            | Nintendo Entertainment System (NES) Emulator                       |           | [Here](https://gbatemp.net/attachments/libretro-fceumm-rar.116907/)    |                                          | 2018-03-08   |
| Virtual Jaguar          | Atari Jaguar Emulator                                              |           | [Here](https://gbatemp.net/attachments/virtual_jaguar-nro-zip.117971/) |                                          | 2018-01-18   |
| mGBA (GB, GBC, GBA)     | Gameboy, Gameboy Color, and Gameboy Advance Emulator               |           | [Here](https://gbatemp.net/attachments/mgba-nro-zip.116720/)           |                                          | 2018-03-19   |
| VBA Next (GB, GBC, GBA) | Gameboy, Gameboy Color, and Gameboy Advance Emulator               |           | [Here](https://gbatemp.net/attachments/vba-next-rar.116908/)           |                                          | 2018-01-09   |
| GearBoy (GB, GBC)       | Gameboy and Gameboy Color Emulator                                 |           | [Here](https://gbatemp.net/attachments/gearboy-nro-zip.116723/)        |                                          | 2018-01-18   |
| Gambattle (GB, GBC)     | Gameboy and Gameboy Color Emulator                                 |           | [Here](https://gbatemp.net/attachments/gambatte_fix-nro-zip.117249/)   |                                          | 2018-01-18   |
| Picodrive               | Genesis, MegaDrive, Master System, 32x, and Sega CD Emulator       |           | [Here](https://gbatemp.net/attachments/picodrive-nro-zip.117920/)      |                                          | 2018-03-19   |
| Genesis Plus GX         | Genesis, MegaDrive, Master System, Game Gear, and Sega CD Emulator |           | [Here](https://gbatemp.net/attachments/genesisgx-nro-zip.116038/)      |                                          | 2018-03-19   |
| MAME 2003               | Multi-purpose emulation framework, Arcade game Emulator            |           | [Here](https://gbatemp.net/attachments/mame2003-nro-zip.117945/)       |                                          | 2018-03-19   |
| Beetle PSX              | Playstation Emulator                                               |           | [Here](https://gbatemp.net/attachments/beetlepsx-nro-zip.116708/)      |                                          | 2018-03-19   |

### Title managers

| Name | Description | Author | Download | Open-Source | Last Updated |
| ---- | ----------- | ------ | -------- | ----------- | ------------ |
|      |             |        |          |             |              |

### Save managers

| Name | Description | Author | Download | Open-Source | Last Updated |
| ---- | ----------- | ------ | -------- | ----------- | ------------ |
|      |             |        |          |             |              |

### File servers

| Name | Description | Author | Download | Open-Source | Last Updated |
| ---- | ----------- | ------ | -------- | ----------- | ------------ |
|      |             |        |          |             |              |

### Demos

| Name      | Description                                    | Author                           | Download                                        | Open-Source | Last Updated |
| --------- | ---------------------------------------------- | -------------------------------- | ----------------------------------------------- | ----------- | ------------ |
| 34c3-demo | Demo from the 34c3 for Homebrew on the Switch. | [plutoo](User:plutoo "wikilink") | [Here](https://github.com/switchbrew/34c3-demo) | Yes         | 2018-02-19   |
|           |                                                |                                  |                                                 |             |              |

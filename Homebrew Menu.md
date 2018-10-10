The [Homebrew Menu](https://github.com/switchbrew/nx-hbmenu) (hbmenu) is
the menu for launching homebrew applications. Applications are launched
using the Homebrew ABI, hence normally
[nx-hbloader](https://github.com/switchbrew/nx-hbloader) will do the
actual launching.

# Usage

See [Homebrew Applications](Homebrew%20Applications.md "wikilink") for
SD layout etc.

# Controls

Use the D-Pad/joystick to select the app/directory, up/down can be used
for faster scrolling. Press A to launch the app. Navigating directories
is supported, press A to enter a directory and press B to leave the
current directory. Press Y to activate netloader and press B to
deactivate netloader.

## Touch controls

NOTE: This is not yet available with the latest hbmenu release.

To navigate through the list of folders and applications you can swipe
left and right on the bottom list. To open an item you can tap on it in
the list or with it highlighted tap the `Open` or `Launch` button prompt
in the bottom right. To go back a folder you can swipe up or tap the
`Back` button prompt in the bottom right. To activate the netloader you
can swipe down on the screen.

# Battery

NOTE: This is not yet available with the latest hbmenu release.

The battery/charge status can be displayed, however this is only
displayed when the required service is available/accessible.

# Netloader

NOTE: This is not yet available with the latest hbmenu release.

With netloader activated as described above you can load apps over the
network with nxlink. With the
[toolchain](Setting%20up%20Development%20Environment.md "wikilink")
setup run `nxlink `<nrofile> if your network can handle UDP broadcast
messages. If nxlink fails with "No response from Switch\!" you can use
`-a `<ip address> before <nrofile> for the address to send the app to.
See nxlink help for more options.

# Themes

NOTE: This is not yet available with the latest hbmenu release.

Themes can be optionally loaded from SD "/config/nx-hbmenu/themes/". The
theme (or the default) can be selected using the Theme Menu via the -
button. This uses
[libconfig](https://hyperrealm.github.io/libconfig/libconfig_manual.html).
Default settings will be used for any settings not specified in the
theme (including themeInfo).

The string used for displaying the buttons can be set with buttonAText,
buttonBText, and buttonMText, but normally this can be left at the
defaults. Change the value of the enableWaveBlending field to 1 to
enable wave blending.

There's also borderColor and borderTextColor fields which can be set
like the other color fields.

The color fields are RGBA.

Sample theme file (.cfg file extension):

`themeInfo={`  
`    name="Theme Name";`  
`    author="Theme Author Name";`  
`    version="1.0.0";`  
`};`  
  
`lightTheme={`  
`    textColor=(0,0,0,255);`  
`    frontWaveColor=(255,102,204,255);`  
`    middleWaveColor=(255,51,153,255);`  
`    backWaveColor=(204,0,153,255);`  
`    backgroundColor=(233,236,241,255);`  
`    highlightColor=(255,77,166,255);`  
`    separatorColor=(128,0,128,255);`  
`    enableWaveBlending=0;`  
`};`  
  
`darkTheme={`  
`    textColor=(255,255,255,255);`  
`    frontWaveColor=(255,51,153,255);`  
`    middleWaveColor=(255,102,204,255);`  
`    backWaveColor=(204,0,153,255);`  
`    backgroundColor=(0,0,0,255);`  
`    highlightColor=(255,77,166,255);`  
`    separatorColor=(255,255,255,255);`  
`    enableWaveBlending=0;`  
`};`

# File Associations

NOTE: This is not yet available with the latest hbmenu release. This is
not yet implemented.

File-association cfg files can optionally be loaded from SD
"/config/nx-hbmenu/fileassoc/" during startup. There's 1 .cfg file for
each app. During normal menu scanning, hbmenu will check for
file\_extensions/filenames from fileassoc cfg with the dir-list
filename, when the file is not recognized otherwise (likewise for
directories). This is processed in the same order that the cfg was
loaded from SD / same order specified in the cfg file.

When processing directories where no NRO was detected, hbmenu will go
through the dir-listing and use the first entry where the filename
matches a fileassoc entry where `filename` is specified (file\_extension
entries are skipped).

The generated menu entry launches the specified app\_path where the
first passed argument (argv\[1\] in the launched app) is the absolute
filepath for the associated file. See below regarding the icon used for
the menu entry. The author and version fields for the menu entry are
loaded from app\_path, while the name is the filename (unless a
directory is being processed, in this case the directory name is used).

The only optional setting is icon\_path. All paths are absolute. Icon
will attempted to be loaded from the following: {$FILEPATH with
extension changed to .jpg} -\> icon\_path setting if it exists (target
setting -\> main file\_assoc setting) -\> icon from app\_path.

If you have targets where file\_extension and filename both have the
same extension, the filename target should be located before that
file\_extension target in the cfg. Targets which have both
file\_extension and filename settings are ignored.

Sample fileassoc file:

`fileassoc={`  
`  app_path="/switch/myapp/app.nro";`  
`  icon_path="/switch/myapp/myicon.jpg";`  
  
`  targets=(`  
`    {`  
`      file_extension=".ext3";`  
`      icon_path="/switch/myapp/myicon2.jpg";`  
`    },`  
`    {`  
`      file_extension=".ext4";`  
`      icon_path="/switch/myapp/myicon3.jpg";`  
`    },`  
`    {`  
`      filename="main.py";`  
`      icon_path="/switch/myapp/myicon4.jpg";`  
`    }`  
`  );`  
`};`

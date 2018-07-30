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

# Netloader

NOTE: This is not yet available with the latest hbmenu release.

With netloader activated as described above you can load apps over the
network with nxlink. With the
[toolchain](Setting%20up%20Development%20Environment.md "wikilink")
setup run `nxlink `<nrofile> if your network can handle UDP broadcast
messages. If nxlink fails with "No response from Switch\!" you can use
`-a `<ip address> before <nrofile> for the address to send the app to.
See nxlink help for more options.

This is the system "flog" 01008BB00013C000
[title](Title%20list.md "wikilink"). This is a NES emulator. Installed
on retail systems since [1.0.0](1.0.0.md "wikilink").

The titleID for "flog" is used by 3 funcs in
[qlaunch](Qlaunch.md "wikilink"): 1 for checking whether to launch it, 1
for launching(?), and 1 that compares flog titleID with a field.

The ROM is not loaded via [FS](Filesystem%20services.md "wikilink") but
is embedded in the main binary.

"flog" == "golf" backwards. This runs the NES "Golf" game. {1/2}-player
via joy-con is supported. Controls are "d-pad" buttons + stick, however
motion control while holding the Z{L/R} button is also supported instead
of using buttons.

## Official Launch

The checks for this only run while Home Menu is active, aka main-menu.

It checks exactly the following:

  - Both Joy-Cons must be detached from the system.
  - The same motion checks for both Joy-Cons must pass, at the same
    time. The motion seems to be a reference to
    [this](https://www.youtube.com/watch?time_continue=17&v=BdQg43n2OaM).
    Hold the Joy-Cons pointing forwards/downwards, then move Joy-Cons to
    a vertical position, and hold it there for a bit. The Joy-Con grip
    can be used for this.
  - The month+day must match the date of Iwata's
    [death](https://en.wikipedia.org/wiki/Satoru_Iwata): July 11. The
    loaded date originates from network-time-sync'd time, regardless of
    whether the user has it enabled or not. When the system was never
    connected to the Internet, it comes from the user-specified date
    instead.
  - The output from a certain function must return 0, 1, or 2. On one
    system this was tested with, this check would pass.
  - Lastly a nsam cmd is used. Probably to verify that the title is
    installed?

Once everything passes it continues to the code which launches(?) flog.

## Screenshots

These screenshots were originally taken by executing flog with an
unofficial method.

![Flog main-screen](Flog0.jpg "Flog main-screen") ![Flog
1-player](Flog1.jpg "Flog 1-player") ![Flog 2-player mode as
player-1.](Flog2.jpg "Flog 2-player mode as player-1.") ![Flog 2-player
mode as player-2.](Flog3.jpg "Flog 2-player mode as player-2.")

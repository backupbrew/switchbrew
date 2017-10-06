This is the system "flog" 01008BB00013C000
[title](Title%20list.md "wikilink"). "flog" is a full-fledged NES
emulator and is installed on retail systems since
[1.0.0](1.0.0.md "wikilink").

The titleID for "flog" is used by 3 functions in
[qlaunch](Qlaunch.md "wikilink"): 1 for checking whether to launch it, 1
for registering it as an
[applet](AM%20services#appletAE.md##appletAE "wikilink") and 1 to launch
it.

The ROM is not loaded via [FS](Filesystem%20services.md "wikilink") but
is embedded in the main binary.

"flog" == "golf" backwards. This runs the NES "Golf" game. {1/2}-player
via joy-con is supported. Controls are "d-pad" buttons + stick, however
motion control while holding the Z{L/R} button is also supported instead
of using buttons.

## Official Launch

[qlaunch](Qlaunch.md "wikilink") periodically checks if the user is in
"/RootScene/SceneResidentMenu", which represents the Home Menu (aka
main-menu). If so, the following checks are then performed in order:

  - The Joy-Cons' state is read from [HID shared
    memory](HID%20Shared%20Memory.md "wikilink") and both must be active
    and detached from the console.
  - "StartSixAxisSensor" [hid](HID%20services#hid.md##hid "wikilink")
    command is called for each Joy-Con so motion data can be captured.
  - After capturing the motion data, the same motion checks for both
    Joy-Cons must pass at the same time. This motion data is analyzed in
    a small state machine consisting of a total of 7 steps and the
    motion itself is a reference to [Iwata's Direct
    gesture](https://www.youtube.com/watch?v=BdQg43n2OaM&t=17s). Hold
    the Joy-Cons pointing forwards/downwards, then move Joy-Cons to a
    vertical position, and hold it there for a bit. The Joy-Con grip can
    be used for this.
  - The system's month and day must be July 11th, which is the date of
    Iwata's [passing](https://en.wikipedia.org/wiki/Satoru_Iwata). The
    loaded date originates from network-time-sync'd time, regardless of
    whether the user has it enabled or not. When the system was never
    connected to the Internet and is on [1.0.0](1.0.0.md "wikilink") it
    comes from the user-specified date instead. For newer systems,
    trying to load the network time if it was never set will result in
    an error: they won't ever be able to launch flog without a time-sync
    with Nintendo servers. This is loaded from the
    [time](PCV%20services.md "wikilink") service-cmds, with the actual
    time-sync being handled by [NIM](NIM%20services.md "wikilink").
  - A wrapper for "GetLanguageCode"
    [set](Settings%20services#set.md##set "wikilink") command is called
    and the returned code must be 0 (JPja), 1 (USen) or 2 (EUen). Other
    combinations of region and language may have it's code translated
    internally to a valid one (0, 1 or 2), which seems to be the case
    for 12 (CNzh), 13 (KRko) and 14 (TWzh).
  - Lastly, "IsSystemProgramInstalled"
    [ns:am](NS%20Services#ns:am.md##ns:am "wikilink") command is called,
    which should return 1 if the "flog" title is installed.

Once everything passes it continues to the code which launches "flog".
When "flog" is launched a small audio clip named "SeTestTone" is played
which matches
[this](https://www.youtube.com/embed/SeVTJu_Yn2Y?start=17&end=18).

## Screenshots

These screenshots were originally taken by executing flog with an
unofficial method.

![Flog main-screen](Flog0.jpg "Flog main-screen") ![Flog
1-player](Flog1.jpg "Flog 1-player") ![Flog 2-player mode as
player-1.](Flog2.jpg "Flog 2-player mode as player-1.") ![Flog 2-player
mode as player-2.](Flog3.jpg "Flog 2-player mode as player-2.")

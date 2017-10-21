Displays news downloaded in the background. News pages can link to
specific eShop pages, network videos, ...

This runs under [qlaunch](Qlaunch.md "wikilink").

The video URLs use HTTPS with the bugyo domain. Video playback is
handled by launching
[WebApplet](Internet%20Browser.md "wikilink")/LibAppletWeb(titleID
010000000000100A) just for the media-player. This doesn't seem to use a
WebApplet whitelist loaded from any RomFS.

# Invalid TLS Cert Handling

With videos it doesn't accept the cert. It hangs during video loading
without displaying any error, have to press B to exit.

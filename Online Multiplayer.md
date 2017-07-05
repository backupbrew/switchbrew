This page is for the Switch equivalent of online/local protocol
[PRUDP](https://www.3dbrew.org/wiki/PRUDP).

Note: the wifi protocol used for local-WLAN is different from UDS, which
3DS and Wii U used.

While the Switch still uses UDP for peer to peer communication (packets
starting with 0x32AB9864), it doesn't seem to be using PRUDP anymore.
Instead, a bunch of https requests are made.

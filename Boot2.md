boot2 is the first non-built-in sysmodule. It's presumably hardcoded to
be the first sysmodule launched by PM.

It connects to "pm:shell" service and launches the following titles in
this order:

  - 0100000000000021 (psc)
  - 0100000000000009 (settings)
  - 0100000000000006 (usb)
  - 010000000000001D (pcie)
  - 010000000000000A (bus)
  - 0100000000000007 (tma)
  - 010000000000001A (pcv)

Then it connects to "set:sys" and reads a bool from "boot" section
called "force\_maintenance" with default value true.

If the value reads successfully as false, it initializes "gpio" and
opens sessions for GPIOs 26 and 25. If both GPIOs read as zero, then
[maintenance mode](Recovery%20Mode.md "wikilink") is forced despite the
setting being false. This probably checks if both volume up and down
keys are held down at the same time?

If it's in maintenance mode then it opens a session to "pm:bm" and calls
cmd1.

Then depending on maintenance mode or not it launches the following
titles in this order:

  - 0100000000000023 (am)
  - 0100000000000019 (nvservices)
  - 010000000000001C (nvnflinger)
  - 010000000000002D (vi)
  - 010000000000001F (ns)
  - 0100000000000015 (lm)
  - 010000000000001B (ppc)
  - 0100000000000010 (ptm)
  - 0100000000000013 (hid)
  - 0100000000000014 (audio)
  - 0100000000000029 (lbl)
  - 0100000000000016 (wlan)
  - 010000000000000B (bluetooth)
  - 0100000000000012 (bsdsockets)
  - 010000000000000F (nifm)
  - 0100000000000018 (ldn)
  - 010000000000001E (account)
  - 010000000000000E (friends) \[skipped in maintenance\]
  - 0100000000000020 (nfc)
  - 0100000000000022 (capsrv)
  - 0100000000000024 (ssl)
  - 0100000000000025 (nim)
  - 010000000000000C (bcat) \[skipped in maintenance\]
  - 010000000000002B (erpt)
  - 0100000000000033 (es)
  - 010000000000002E (pctl)
  - 010000000000002A (btm)
  - 0100000000000030 (eupld) \[skipped in maintenance\]
  - 0100000000000031 (glue)
  - 0100000000000032 (eclct)
  - 010000000000002F (npns) \[skipped in maintenance\]
  - 0100000000000034 (fatal)
  - 0100000000000037 (ro) \[3.0.0+\]
  - 0100000000000038 (doesn't exist on retail systems) \[3.0.0+\]
  - 0100000000000039 (sdb) \[3.0.0+\]

This list is probably optimized for boot-time. It launches
display-related things first presumably to make sure it displays
something as soon as possible.

After that, the process exits itself.

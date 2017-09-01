Manu ("Manufacturing") services are provided by the 010000000000B14A
sysmodule, which is installed at the
[factory](Factory%20Setup.md "wikilink") but not on normal retail
systems.

# manu

| Cmd | Name | Notes                                                                                            |
| --- | ---- | ------------------------------------------------------------------------------------------------ |
| 0   |      | Takes 4 bytes of input, and produces 0 bytes output.                                             |
| 1   |      | Takes an X descriptor, and produces, 8 bytes output.                                             |
| 2   |      | Takes 0x18 bytes of input, a B descriptor, and an X descriptor, and produces 0 bytes of output.  |
| 3   |      | Takes 0x18 bytes of input, an A descriptor, and an X descriptor, and produces 0 bytes of output. |
| 4   |      | Takes 4 bytes of input, and produces 0 bytes of output.                                          |
| 5   |      | Takes 0x10 bytes of input and a B descriptor, and produces 8 bytes of output.                    |
| 6   |      | Takes 0x10 bytes of input and an A descriptor, and produces 8 bytes of output.                   |
|     |      |                                                                                                  |

This seems to interface with [usb:ds](USB%20services.md "wikilink").
SystemInitializer only uses cmd1..cmd3.

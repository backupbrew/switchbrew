Manu ("Manufacturing") services are provided by the 010000000000B14A
sysmodule, which is installed at the
[factory](Factory%20Setup.md "wikilink") but not on normal retail
systems.

# manu

| Cmd | Name                      | Notes                                                                                            |
| --- | ------------------------- | ------------------------------------------------------------------------------------------------ |
| 0   | InitUsbTransferPipeFsFile | Takes 4 bytes of input, and produces 0 bytes output.                                             |
| 1   | FsFile\_Exists            | Takes an X descriptor, and produces, 8 bytes output.                                             |
| 2   | FsFile\_Read              | Takes 0x18 bytes of input, a B descriptor, and an X descriptor, and produces 0 bytes of output.  |
| 3   | FsFile\_Write             | Takes 0x18 bytes of input, an A descriptor, and an X descriptor, and produces 0 bytes of output. |
| 4   | InitUsbTransferPipeRaw    | Takes 4 bytes of input, and produces 0 bytes of output.                                          |
| 5   | Raw\_Read                 | Takes 0x10 bytes of input and a B descriptor, and produces 8 bytes of output.                    |
| 6   | Raw\_Write                | Takes 0x10 bytes of input and an A descriptor, and produces 8 bytes of output.                   |
|     |                           |                                                                                                  |

All commands are wrappers for [usb:ds](USB%20services.md "wikilink")
requests with USB configured as:

`VID:           0x057E (Nintendo Co., Ltd)`  
`PID:           0x3000`  
`bcdDevice:     0x0100 (1.00)`  
`Manufacturer:  "Nintendo"`  
`Product:       "NintendoSdkDebugger"`  
`SerialNumber:  "SerialNumber"`

[SystemInitializer](SystemInitializer.md "wikilink") only uses
cmd1..cmd3.

## InitUsbTransferPipeFsFile

Takes an unknown u32 (ID?) and configures a transfer pipe over
[usb:ds](USB%20services.md "wikilink") for file access mode.

## FsFile\_Exists

Takes an input path string (type-0x9 buffer), returns 8-bytes for the
output u8 flag.

Checks whether the specified file exists.

This is "FsFile::Exists" in SystemInitializer.

## FsFile\_Read

Takes a type-0x6 output buffer and a type-0x9 input string path buffer,
and 3 u64s: <same size value from databuf>, unk,
<same size value from databuf>. Where unk is probably offset?

Reads data from the specified file.

## FsFile\_Write

Same as FsFile\_Read except the databuf is a type-0x5 input buffer.

Writes data to the specified file.

SystemInitializer also uses this as "FsFile::Create" with all input u64s
set to 0.

## InitUsbTransferPipeRaw

Takes an unknown u32 (ID?) and configures a transfer pipe over
[usb:ds](USB%20services.md "wikilink") for raw access mode.

## Raw\_Read

Takes a type-0x6 output buffer and 2 u64s: **offset** and **size**.

Reads raw data from the device.

## Raw\_Write

Takes a type-0x5 input buffer and 2 u64s: **offset** and **size**.

Writes raw data to the device.

[Category:Services](Category:Services "wikilink")

# pcie

This is "nn::pcie::detail::IManager".

| Cmd | Name                                                                   |
| --- | ---------------------------------------------------------------------- |
| 0   | [\#RegisterClassDriver](#RegisterClassDriver "wikilink")               |
| 1   | [\#QueryFunctionsUnregistered](#QueryFunctionsUnregistered "wikilink") |

## RegisterClassDriver

Takes the current process handle (0xFFFF8001).

Returns an event handle and session handle to a
[\#ISession](#ISession "wikilink").

## QueryFunctionsUnregistered

Takes a type-6 buffer.

Returns a list of connected PCIe endpoint devices.

## ISession

This is "nn::pcie::detail::ISession".

| Cmd | Name                   |
| --- | ---------------------- |
| 0   | QueryFunctions         |
| 1   | AcquireFunction        |
| 2   | ReleaseFunction        |
| 3   | GetFunctionState       |
| 4   | GetBarProfile          |
| 5   | ReadConfig             |
| 6   | WriteConfig            |
| 7   | ReadBarRegion          |
| 8   | WriteBarRegion         |
| 9   | FindCapability         |
| 10  | FindExtendedCapability |
| 11  | MapDma                 |
| 12  | UnmapDma               |
| 13  | UnmapDmaBusAddress     |
| 14  | GetDmaBusAddress       |
| 15  | GetDmaBusAddressRange  |
| 16  | SetDmaEnable           |
| 17  | AcquireIrq             |
| 18  | ReleaseIrq             |
| 19  | SetIrqEnable           |
| 20  | SetAspmEnable          |
| 21  | \[3.0.0+\]             |
| 22  | \[4.0.0+\]             |
| 23  | \[7.0.0+\]             |

\[5.0.0+\] The buffer types for ReadBarRegion/WriteBarRegion were
changed: 0x6 changed to 0x22, and 0x5 changed to 0x21.

\[7.0.0+\] AcquireIrq now takes an additional 4-bytes of input, and no
longer returns an output handle. SetAspmEnable now returns an output
handle.

# pcie:log

This was added with \[6.0.0+\].

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |

[Category:Services](Category:Services "wikilink")

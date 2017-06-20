System Flaws are used to execute unofficial code (homebrew) on the
Nintendo Switch. This page is a list of known and public Switch System
Flaws.

# List of Switch System Flaws

There are currently no public Switch System
Flaws.

## Hardware

| Summary                     | Description | Fixed with hardware model/revision | Newest hardware model/revision this flaw was checked for | Timeframe this was discovered | Discovered by |
| --------------------------- | ----------- | ---------------------------------- | -------------------------------------------------------- | ----------------------------- | ------------- |
| No public hardware exploits |             |                                    |                                                          |                               |               |
|                             |             |                                    |                                                          |                               |               |

## ARM TrustZone software

### ARM TrustZone

| Summary                          | Description | Successful exploitation result | Fixed in system version | Last system version this flaw was checked for | Timeframe this was discovered | Public disclosure timeframe | Discovered by |
| -------------------------------- | ----------- | ------------------------------ | ----------------------- | --------------------------------------------- | ----------------------------- | --------------------------- | ------------- |
| No public ARM TrustZone exploits |             |                                |                         |                                               |                               |                             |               |
|                                  |             |                                |                         |                                               |                               |                             |               |

## Kernel software

### Kernel

| Summary                   | Description | Successful exploitation result | Fixed in system version | Last system version this flaw was checked for | Timeframe this was discovered | Public disclosure timeframe | Discovered by |
| ------------------------- | ----------- | ------------------------------ | ----------------------- | --------------------------------------------- | ----------------------------- | --------------------------- | ------------- |
| No public Kernel exploits |             |                                |                         |                                               |                               |                             |               |
|                           |             |                                |                         |                                               |                               |                             |               |

### System Modules

| Summary                                                                  | Description                                                                                                                                                                                                                                                                                                                                                                                                                     | Successful exploitation result                                                                                                                 | Fixed in system version      | Last system version this flaw was checked for | Timeframe this was discovered | Public disclosure timeframe                      | Discovered by                           |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------- | --------------------------------------------- | ----------------------------- | ------------------------------------------------ | --------------------------------------- |
| OOB Read in NS system module (pl:utoohax, pl:utonium, maybe other names) | Prior to [3.0.0](3.0.0.md "wikilink"), pl:u (Shared Font services implemented in the NS sysmodule) service commands 1,2,3 took in a signed 32-bit index and returned that index of an array but did not check that index at all. This allowed for an arbitrary read within a 34-bit range (33-bit signed) from pl:u .bss. In [3.0.0](3.0.0.md "wikilink"), sending out of range indexes causes error code 0x60A to be returned. | Dumping pl:u (part of the the NS module)'s virtual memory (including code); obtaining base addresses for NS module .text (thus defeating ASLR) | [3.0.0](3.0.0.md "wikilink") | [3.0.0](3.0.0.md "wikilink")                  | April 2017                    | On exploit's fix in [3.0.0](3.0.0.md "wikilink") | qlutoo, Reswitched team (independently) |
|                                                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                 |                                                                                                                                                |                              |                                               |                               |                                                  |                                         |

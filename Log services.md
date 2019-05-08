# lm

This is "nn::lm::ILogService".

| Cmd | Name                                   |
| --- | -------------------------------------- |
| 0   | [\#OpenLogger](#OpenLogger "wikilink") |

## OpenLogger

Takes an input u64 value representing a process ID and returns an
[\#ILogger](#ILogger "wikilink") instance.

## ILogger

This is "nn::lm::ILogger".

| Cmd | Name                                                      |
| --- | --------------------------------------------------------- |
| 0   | [\#Log](#Log "wikilink")                                  |
| 1   | \[3.0.0+\] [\#SetDestination](#SetDestination "wikilink") |

## Log

Takes an input buffer containing the message to log. Will always return
successfully.

## SetDestination

Takes an input u32 mask value indicating the logging destinations to
send incoming log messages to. The mask entries are as follows:

| Value  | Description             |
| ------ | ----------------------- |
| 1      | Unknown                 |
| 2      | UART                    |
| 4      | UART when sleeping      |
| 0xFFFF | Log to all destinations |

# lm:get

This is "nn::lm::ILogGetter".

| Cmd | Name         |
| --- | ------------ |
| 0   | StartLogging |
| 1   | StopLogging  |
| 2   | GetLog       |

This service doesn't normally exist on retail.

[Category:Services](Category:Services "wikilink")

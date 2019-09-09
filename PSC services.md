PSC (Power State Control) provides services related to power state
changes in the system.

# Concept

psc:m allows a process to register a module that depends on power
management in some way. A client calls GetPmModule to receive an
IPmModule (Power Managed Module), and then calls
IPmModule-\>Initialize(module\_id, module\_dependency\_list) where
module\_id is the ModuleId enum member for the client, and the
dependency list is an array of module IDs for the modules that this
depends on. Initialize() returns an event handle that the client can
wait on to be notified of a power state change.

psc:c allows a module to the power state controller for the system (in
practice, AM is the only client to the controller).
IPmControl-\>DispatchRequest() is used notify all IPmModules of a state
change.

For example, FS registers itself as an IPmModule with dependencies on
pinmux, gpio, pcv, tma, and initializes the SD card once those
dependencies have registered..

It then does (basically) the following pseudocode (actual code located
at .text + 0xB2DB0 in 6.0.0 FS):

`   while (true) {`  
`       Fs_IPmModule->WaitSignaled();`  
`       `  
`       Fs_IPmModule->GetRequest(&state);`  
`       switch (state) {`  
`           case WakingUp:`  
`               /* hardware devices are woken up here */`  
`           case GoingToSleep:`  
`               /* hardware devices are put to sleep here */`  
`           case ShuttingDown:`  
`               /* hardware devices are turned off here */`  
`       }`  
`       `  
`       Fs_IPmModule->Acknowledge(state);`  
`   }`

# psc:c

This is "nn::psc::sf::IPmControl".

| Cmd               | Name                   |
| ----------------- | ---------------------- |
| 0                 | Initialize             |
| 1                 | DispatchRequest        |
| 2                 | GetResult              |
| 3                 | GetState               |
| 4                 | Cancel                 |
| \[1.0.0-6.2.0\] 5 | PrintModuleInformation |
| 6                 | GetModuleInformation   |

# psc:m

This is "nn::psc::sf::IPmService".

| Cmd | Name        | Notes                                            |
| --- | ----------- | ------------------------------------------------ |
| 0   | GetPmModule | Returns an [\#IPmModule](#IPmModule "wikilink"). |

## IPmModule

This is "nn::psc::sf::IPmModule".

| Cmd | Name                     |
| --- | ------------------------ |
| 0   | Initialize               |
| 1   | GetRequest               |
| 2   | Acknowledge              |
| 3   | Finalize                 |
| 4   | \[5.1.0+\] AcknowledgeEx |

# srepo:u, srepo:a

These are "nn::srepo::detail::ipc::ISrepoService".

| Cmd   | Name       |
| ----- | ---------- |
| 10100 |            |
| 10101 | \[6.0.0+\] |
| 10200 | \[6.0.0+\] |
| 10201 | \[6.0.0+\] |
| 11000 | \[6.0.0+\] |
| 11001 | \[6.0.0+\] |
| 11002 | \[6.0.0+\] |
| 11003 | \[6.0.0+\] |
| 11004 | \[6.0.0+\] |
| 11100 | \[6.0.0+\] |
| 11200 | \[6.0.0+\] |
| 11300 | \[6.0.0+\] |
| 11400 | \[6.0.0+\] |
| 11500 | \[6.0.0+\] |
| 11600 | \[6.0.0+\] |
| 11601 | \[6.0.0+\] |
| 11602 | \[6.0.0+\] |
| 11700 | \[6.0.0+\] |
| 11800 | \[6.0.0+\] |
| 11801 | \[6.0.0+\] |
| 11810 | \[8.0.0+\] |
| 11811 | \[8.0.0+\] |
| 12000 | \[8.0.0+\] |
| 12001 | \[8.0.0+\] |
| 13000 | \[8.0.0+\] |
| 13001 | \[8.0.0+\] |
| 20100 |            |
| 20200 |            |
| 20300 | \[6.0.0+\] |
| 20400 | \[6.0.0+\] |
| 20401 | \[6.0.0+\] |
| 20402 | \[7.0.0+\] |
| 20500 | \[8.0.0+\] |

# ovln:rcv

This is "nn::ovln::IReceiverService".

| Cmd | Name         |
| --- | ------------ |
| 0   | OpenReceiver |

## IReceiver

This is "nn::ovln::IReceiver".

| Cmd | Name                  |
| --- | --------------------- |
| 0   | AddSource             |
| 1   | RemoveSource          |
| 2   | GetReceiveEventHandle |
| 3   | Receive               |
| 4   | ReceiveWithTick       |

# ovln:snd

This is "nn::ovln::ISenderService".

| Cmd | Name       |
| --- | ---------- |
| 0   | OpenSender |

## ISender

This is "nn::ovln::ISender".

| Cmd | Name                      |
| --- | ------------------------- |
| 0   | Send                      |
| 1   | GetUnreceivedMessageCount |

# PSC Module IDs

| ID   | Module                                                   |
| ---- | -------------------------------------------------------- |
| 0x03 |                                                          |
| 0x04 | [USB](USB%20services.md "wikilink")                      |
| 0x05 |                                                          |
| 0x07 | [Pcv](PCV%20services.md "wikilink")                      |
| 0x08 | [Pcv:Imm](PCV%20services.md "wikilink")                  |
| 0x09 | [Gpio](Bus%20services.md "wikilink")                     |
| 0x0A | [Pinmux](Bus%20services.md "wikilink")                   |
| 0x0B | [Uart](Bus%20services.md "wikilink")                     |
| 0x0C | [I2c](Bus%20services.md "wikilink")                      |
| 0x0D | [I2c:Pcv](Bus%20services.md "wikilink")                  |
| 0x0E | [Sasbus](Bus%20services.md "wikilink")                   |
| 0x0F | [Pwm](Bus%20services.md "wikilink")                      |
| 0x10 |                                                          |
| 0x13 | [PCIe](PCIe%20services.md "wikilink")                    |
| 0x14 | [Backlight](Backlight%20services.md "wikilink")          |
| 0x15 | [Nvnflinger](Nvnflinger%20services.md "wikilink")        |
| 0x18 | [nn::psc::PmModuleId\_Hid](HID%20services.md "wikilink") |
| 0x1B |                                                          |
| 0x1C | [Audio](Audio%20services.md "wikilink")                  |
| 0x1E |                                                          |
| 0x1F | [Bluetooth](Bluetooth%20Driver%20services.md "wikilink") |
| 0x20 | [Bpc](PCV%20services.md "wikilink")                      |
| 0x21 | [Ptm](PTM%20services.md "wikilink")                      |
| 0x23 | [nn::psc::PmModuleId\_Nfc](NFC%20services.md "wikilink") |
| 0x24 | [Ppc](PPC%20services.md "wikilink")                      |
| 0x25 |                                                          |
| 0x26 | [Nifm](Network%20Interface%20services.md "wikilink")     |
| 0x28 | [Npns](NPNS%20services.md "wikilink")                    |
| 0x29 | [nn::psc::PmModuleId\_Lm](Log%20services.md "wikilink")  |
| 0x2A | [Bcat](BCAT%20services.md "wikilink")                    |
| 0x2B | [Time](PCV%20services.md "wikilink")                     |
| 0x2C | [Pctl](Parental%20Control%20services.md "wikilink")      |
| 0x2D | [Erpt](Error%20Report%20services.md "wikilink")          |
| 0x2E | [Eupld](Error%20Upload%20services.md "wikilink")         |
| 0x2F | [Friend](Friend%20services.md "wikilink")                |
| 0x30 | [Glue](Glue%20services.md "wikilink")                    |
| 0x31 | [Account](Account%20services.md "wikilink")              |
| 0x32 | [SasBus](Bus%20services.md "wikilink")                   |
| 0x65 | [NV](NV%20services.md "wikilink")                        |

# Power Management States

| ID                  | Name | Description                             |
| ------------------- | ---- | --------------------------------------- |
| Awake               | 0    | Everything is awake.                    |
| ReadyAwaken         | 1    | Preparing to transition to awake.       |
| ReadySleep          | 2    | Preparing to transition to sleep.       |
| ReadySleepCritical  | 3    | Critical services are ready to sleep.   |
| ReadyAwakenCritical | 4    | Critical services are ready to wake up. |
| ReadyShutdown       | 5    | Preparing to transition to shutdown.    |

[Category:Services](Category:Services "wikilink")

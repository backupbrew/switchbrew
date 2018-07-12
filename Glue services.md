# arp:r

This is "nn::arp::detail::IReader".

| Cmd | Name                                           |
| --- | ---------------------------------------------- |
| 0   | GetApplicationLaunchProperty                   |
| 1   | GetApplicationLaunchPropertyWithApplicationId  |
| 2   | GetApplicationControlProperty                  |
| 3   | GetApplicationControlPropertyWithApplicationId |

## GetApplicationControlPropertyWithApplicationId

Takes in a title id and a type-0x16 buffer. This is filled with the
contents of control.nacp for that application.

# arp:w

This is "nn::arp::detail::IWriter".

| Cmd | Name             |
| --- | ---------------- |
| 0   | AcquireRegistrar |
| 1   | DeleteProperties |

## IRegistrar

This is "nn::arp::detail::IRegistrar".

| Cmd | Name                          |
| --- | ----------------------------- |
| 0   | Issue                         |
| 1   | SetApplicationLaunchProperty  |
| 2   | SetApplicationControlProperty |

### Launch Property Format

| Offset | Size | Description          |
| ------ | ---- | -------------------- |
| 0x0    | 0x8  | Title ID             |
| 0x8    | 0x4  | Version              |
| 0xC    | 0x1  | Base Game Storage ID |
| 0xD    | 0x1  | Update Storage ID    |
| 0xE    | 0x2  | Padding              |

[Category:Services](Category:Services "wikilink")

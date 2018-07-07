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

[Category:Services](Category:Services "wikilink")

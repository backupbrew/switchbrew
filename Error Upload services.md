The "Error upload" service reads and uploads error reports from `erpt:r`
to a cloud server.

This includes crash dumps with full exception info created by
[creport](Creport.md "wikilink").

It periodically uploads them to the following URL:

<https://receive-%.er.srv.nintendo.net/post>

The functionality can be disabled from `set:sys` by setting ("eupld",
"upload\_enabled") to anything but 1.

# eupld:c

This is "nn::eupld::sf::IControl".

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |
| 3   |      |

# eupld:r

This is "nn::eupld::sf::IRequest".

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |
| 3   |      |
| 4   |      |
| 5   |      |

[Category:Services](Category:Services "wikilink")

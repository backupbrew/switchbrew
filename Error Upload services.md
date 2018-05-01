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

| Cmd | Name          |
| --- | ------------- |
| 0   | SetUrl        |
| 1   | ImportCrt     |
| 2   | ImportPki     |
| 3   | SetAutoUpload |

# eupld:r

This is "nn::eupld::sf::IRequest".

| Cmd | Name            |
| --- | --------------- |
| 0   | Initialize      |
| 1   | UploadAll       |
| 2   | UploadSelected  |
| 3   | GetUploadStatus |
| 4   | CancelUpload    |
| 5   | GetResult       |

[Category:Services](Category:Services "wikilink")

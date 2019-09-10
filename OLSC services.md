OLSC (OnLine Savedata Cloud?) is a sysmodule designed for handling the
new online savedata cloud backup system.

# olsc:s

This is "nn::olsc::srv::IOlscServiceForSystemService".

| Cmd  | Name            | Notes                                                                               |
| ---- | --------------- | ----------------------------------------------------------------------------------- |
| 0    |                 | Returns an [\#ITransferTaskListController](#ITransferTaskListController "wikilink") |
| 1    |                 | Returns an [\#IRemoteStorageController](#IRemoteStorageController "wikilink")       |
| 2    |                 | Returns an [\#IDaemonController](#IDaemonController "wikilink")                     |
| 10   |                 |                                                                                     |
| 11   |                 |                                                                                     |
| 12   |                 |                                                                                     |
| 100  |                 |                                                                                     |
| 101  |                 |                                                                                     |
| 102  |                 |                                                                                     |
| 103  |                 |                                                                                     |
| 104  | \[7.0.0+\]      | Returns an [\#INativeHandleHolder](#INativeHandleHolder "wikilink")                 |
| 105  | \[8.0.0+\]      |                                                                                     |
| 200  |                 |                                                                                     |
| 201  |                 |                                                                                     |
| 202  | \[6.0.0-7.0.1\] | Returns an [\#IAsyncResult](#IAsyncResult "wikilink")                               |
| 203  | \[7.0.0+\]      | Returns an [\#IAsyncResult](#IAsyncResult "wikilink")                               |
| 204  | \[7.0.0+\]      |                                                                                     |
| 300  | \[8.0.0+\]      |                                                                                     |
| 301  | \[8.0.0+\]      |                                                                                     |
| 900  |                 |                                                                                     |
| 902  |                 |                                                                                     |
| 903  |                 |                                                                                     |
| 904  |                 |                                                                                     |
| 905  |                 |                                                                                     |
| 906  |                 |                                                                                     |
| 907  |                 |                                                                                     |
| 908  |                 |                                                                                     |
| 909  |                 |                                                                                     |
| 910  | \[8.0.0+\]      |                                                                                     |
| 1000 | \[7.0.0-8.1.0\] | Returns an [\#IAsyncResult](#IAsyncResult "wikilink")                               |
| 1010 | \[7.0.0-8.1.0\] |                                                                                     |
| 1011 | \[7.0.0-8.1.0\] |                                                                                     |
| 1012 | \[7.0.0-8.1.0\] |                                                                                     |
| 1013 | \[7.0.0-8.1.0\] |                                                                                     |
| 1014 | \[7.0.0-8.1.0\] |                                                                                     |
| 1020 | \[7.0.0-8.1.0\] | Returns an [\#IAsyncResult](#IAsyncResult "wikilink")                               |
| 1021 | \[7.0.0-8.1.0\] | Returns an [\#IAsyncResult](#IAsyncResult "wikilink")                               |
| 1022 | \[7.0.0-8.1.0\] | Returns an [\#IAsyncResult](#IAsyncResult "wikilink")                               |
| 1023 | \[7.0.0-8.1.0\] | Returns an [\#IAsyncResult](#IAsyncResult "wikilink")                               |
| 1024 | \[7.0.0-8.1.0\] |                                                                                     |
| 1100 | \[9.0.0+\]      | Returns an [\#IAsyncResult](#IAsyncResult "wikilink")                               |
| 1110 | \[9.0.0+\]      |                                                                                     |
| 1111 | \[9.0.0+\]      |                                                                                     |
| 1112 | \[9.0.0+\]      |                                                                                     |
| 1113 | \[9.0.0+\]      |                                                                                     |
| 1114 | \[9.0.0+\]      |                                                                                     |
| 1120 | \[9.0.0+\]      | Returns an [\#IAsyncResult](#IAsyncResult "wikilink")                               |
| 1121 | \[9.0.0+\]      | Returns an [\#IAsyncResult](#IAsyncResult "wikilink")                               |
| 1122 | \[9.0.0+\]      | Returns an [\#IAsyncResult](#IAsyncResult "wikilink")                               |
| 1123 | \[9.0.0+\]      | Returns an [\#IAsyncResult](#IAsyncResult "wikilink")                               |
| 1124 | \[9.0.0+\]      |                                                                                     |

## ITransferTaskListController

This is "nn::olsc::srv::ITransferTaskListController".

| Cmd | Name       | Notes                                                               |
| --- | ---------- | ------------------------------------------------------------------- |
| 0   |            |                                                                     |
| 1   |            |                                                                     |
| 2   |            |                                                                     |
| 3   |            |                                                                     |
| 4   |            |                                                                     |
| 5   |            | Returns an [\#INativeHandleHolder](#INativeHandleHolder "wikilink") |
| 6   |            |                                                                     |
| 7   |            |                                                                     |
| 8   |            | Returns an [\#IStopperObject](#IStopperObject "wikilink")           |
| 9   |            | Returns an [\#INativeHandleHolder](#INativeHandleHolder "wikilink") |
| 10  |            |                                                                     |
| 11  |            |                                                                     |
| 12  |            |                                                                     |
| 13  | \[9.0.0+\] |                                                                     |
| 14  | \[9.0.0+\] |                                                                     |
| 15  | \[9.0.0+\] |                                                                     |

## INativeHandleHolder

This is "nn::olsc::srv::INativeHandleHolder".

| Cmd | Name            | Notes |
| --- | --------------- | ----- |
| 0   | GetNativeHandle |       |

## IRemoteStorageController

This is "nn::olsc::srv::IRemoteStorageController".

| Cmd | Name            | Notes                                                                |
| --- | --------------- | -------------------------------------------------------------------- |
| 0   |                 |                                                                      |
| 1   |                 |                                                                      |
| 2   | \[6.0.0-7.0.1\] |                                                                      |
| 3   |                 |                                                                      |
| 4   | \[6.0.0-7.0.1\] |                                                                      |
| 6   |                 |                                                                      |
| 7   |                 |                                                                      |
| 8   |                 | Returns an [\#IAsyncResult](#IAsyncResult "wikilink")                |
| 9   |                 | Returns an [\#IAsyncResult](#IAsyncResult "wikilink")                |
| 10  |                 |                                                                      |
| 11  |                 | Returns an [\#IAsyncResult](#IAsyncResult "wikilink")                |
| 12  |                 |                                                                      |
| 13  |                 | Returns an [\#IAsyncResult](#IAsyncResult "wikilink")                |
| 14  |                 |                                                                      |
| 15  |                 |                                                                      |
| 16  |                 | Returns an [\#IAsyncResult](#IAsyncResult "wikilink")                |
| 17  | \[7.0.0+\]      |                                                                      |
| 18  | \[7.0.0+\]      |                                                                      |
| 19  | \[7.0.0+\]      | Returns an [\#INativeHandleHolder](#INativeHandleHolder "wikilink"). |

## IAsyncResult

This is "nn::olsc::srv::IAsyncResult".

| Cmd | Name           | Notes |
| --- | -------------- | ----- |
| 0   | GetResult      |       |
| 1   | Cancel         |       |
| 2   | IsAvailable    |       |
| 3   | GetSystemEvent |       |

## IDaemonController

This is "nn::olsc::srv::IDaemonController".

| Cmd | Name | Notes                                                                                 |
| --- | ---- | ------------------------------------------------------------------------------------- |
| 0   |      |                                                                                       |
| 1   |      |                                                                                       |
| 2   |      |                                                                                       |
| 3   |      |                                                                                       |
| 4   |      |                                                                                       |
| 8   |      |                                                                                       |
| 9   |      |                                                                                       |
| 10  |      | Returns an [\#IForbiddenSaveDataIndication](#IForbiddenSaveDataIndication "wikilink") |
| 11  |      | Returns an [\#IStopperObject](#IStopperObject "wikilink")                             |
| 12  |      |                                                                                       |

## IForbiddenSaveDataIndication

This is "nn::olsc::srv::IForbiddenSaveDataIndication".

| Cmd | Name   | Notes |
| --- | ------ | ----- |
| 0   | Update |       |

[Category:Services](Category:Services "wikilink")

OLSC (OnLine Savedata Cloud?) is a sysmodule designed for handling the
new online savedata cloud backup system.

# olsc:s

This is
"nn::olsc::srv::IOlscServiceForSystemService".

| Cmd | Name | Notes                                                                               |
| --- | ---- | ----------------------------------------------------------------------------------- |
| 0   |      | Returns an [\#ITransferTaskListController](#ITransferTaskListController "wikilink") |
| 1   |      | Returns an [\#IRemoteStorageController](#IRemoteStorageController "wikilink")       |
| 2   |      | Returns an [\#IDaemonController](#IDaemonController "wikilink")                     |
| 10  |      |                                                                                     |
| 11  |      |                                                                                     |
| 12  |      |                                                                                     |
| 100 |      |                                                                                     |
| 101 |      |                                                                                     |
| 102 |      |                                                                                     |
| 103 |      |                                                                                     |
| 200 |      |                                                                                     |
| 201 |      |                                                                                     |
| 202 |      | Returns an [\#IAsyncResult](#IAsyncResult "wikilink")                               |
| 900 |      |                                                                                     |
| 902 |      |                                                                                     |
| 903 |      |                                                                                     |
| 904 |      |                                                                                     |
| 905 |      |                                                                                     |
| 906 |      |                                                                                     |
| 907 |      |                                                                                     |
| 908 |      |                                                                                     |
| 909 |      |                                                                                     |

## ITransferTaskListController

This is
"nn::olsc::srv::ITransferTaskListController".

| Cmd | Name | Notes                                                               |
| --- | ---- | ------------------------------------------------------------------- |
| 0   |      |                                                                     |
| 1   |      |                                                                     |
| 2   |      |                                                                     |
| 3   |      |                                                                     |
| 4   |      |                                                                     |
| 5   |      | Returns an [\#INativeHandleHolder](#INativeHandleHolder "wikilink") |
| 6   |      |                                                                     |
| 7   |      |                                                                     |
| 8   |      | Returns an [\#IStopperObject](#IStopperObject "wikilink")           |
| 9   |      | Returns an [\#INativeHandleHolder](#INativeHandleHolder "wikilink") |
| 10  |      |                                                                     |
| 11  |      |                                                                     |
| 12  |      |                                                                     |
|     |      |                                                                     |

## INativeHandleHolder

This is "nn::olsc::srv::INativeHandleHolder".

| Cmd | Name            | Notes |
| --- | --------------- | ----- |
| 0   | GetNativeHandle |       |
|     |                 |       |

## IRemoteStorageController

This is "nn::olsc::srv::IRemoteStorageController".

| Cmd | Name | Notes                                                 |
| --- | ---- | ----------------------------------------------------- |
| 0   |      |                                                       |
| 1   |      |                                                       |
| 2   |      |                                                       |
| 3   |      |                                                       |
| 4   |      |                                                       |
| 6   |      |                                                       |
| 7   |      |                                                       |
| 8   |      | Returns an [\#IAsyncResult](#IAsyncResult "wikilink") |
| 9   |      | Returns an [\#IAsyncResult](#IAsyncResult "wikilink") |
| 10  |      |                                                       |
| 11  |      | Returns an [\#IAsyncResult](#IAsyncResult "wikilink") |
| 12  |      |                                                       |
| 13  |      | Returns an [\#IAsyncResult](#IAsyncResult "wikilink") |
| 14  |      |                                                       |
| 15  |      |                                                       |
| 16  |      | Returns an [\#IAsyncResult](#IAsyncResult "wikilink") |
|     |      |                                                       |

## IAsyncResult

This is "nn::olsc::srv::IAsyncResult".

| Cmd | Name           | Notes |
| --- | -------------- | ----- |
| 0   | GetResult      |       |
| 1   | Cancel         |       |
| 2   | IsAvailable    |       |
| 3   | GetSystemEvent |       |
|     |                |       |

## IDaemonController

This is
"nn::olsc::srv::IDaemonController".

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
|     |      |                                                                                       |

## IForbiddenSaveDataIndication

This is "nn::olsc::srv::IForbiddenSaveDataIndication".

| Cmd | Name   | Notes |
| --- | ------ | ----- |
| 0   | Update |       |
|     |        |       |

[Category:Services](Category:Services "wikilink")

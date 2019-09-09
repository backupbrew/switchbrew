This is the MyPage applet launched by Home Menu. Official sw uses this
under `nn::friends`. See
[AM\_services\#Library\_Applets](AM%20services#Library%20Applets.md##Library_Applets "wikilink").

## Arg

| Offset | Size | Description                                                 |
| ------ | ---- | ----------------------------------------------------------- |
| 0x0    | 0x4  | [\#Type](#Type "wikilink")                                  |
| 0x4    | 0x4  | Padding                                                     |
| 0x8    | 0x10 | u128 userID                                                 |
| 0x18   | 0x8  | [NetworkServiceAccountId](Account%20services.md "wikilink") |
| 0x20   | 0x48 | [InAppScreenName](Friend%20services.md "wikilink")          |
| 0x68   | 0x48 | [InAppScreenName](Friend%20services.md "wikilink")          |

The is the 0xB0-byte struct pushed for the input storage.

The fields following the userID are only set for
[\#Type](#Type "wikilink") ShowUserDetailInfo/StartSendingFriendRequest,
for everything else these are cleared.

## Type

| Name                              | Type value | PlayStartupSound | Description                                             |
| --------------------------------- | ---------- | ---------------- | ------------------------------------------------------- |
| ShowFriendList                    | 0          | false            |                                                         |
| ShowUserDetailInfo                | 1          | false            |                                                         |
| StartSendingFriendRequest         | 2          | false            |                                                         |
| ShowMethodsOfSendingFriendRequest | 3          | false            |                                                         |
| StartFacedFriendRequest           | 4          | false            |                                                         |
| ShowReceivedFriendRequestList     | 5          | false            |                                                         |
| ShowBlockedUserList               | 6          | false            |                                                         |
| ShowMyProfile                     | 7          | false            |                                                         |
| ShowMyProfileForHomeMenu          | 7          | true             | Identical to ShowMyProfile except for PlayStartupSound. |

## Usage

User-processes should push a common arguments struct (version=0x1) as
well as an [\#Arg](#Arg "wikilink") struct. See
[\#Type](#Type "wikilink") for the commonargs PlayStartupSound flag
value. After starting the applet, official sw immediately closes it (no
output storage is handled) - except for StartSendingFriendRequest, which
returns an output storage containing the Result.

[Category:Library Applets](Category:Library_Applets "wikilink")

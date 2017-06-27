# nsd:u

| Cmd | Name                 |
| --- | -------------------- |
| 10  |                      |
| 11  |                      |
| 12  |                      |
| 13  |                      |
| 14  |                      |
| 20  | Resolve              |
| 21  | ResolveEx            |
| 30  | GetToken             |
| 31  | GetTokenEx           |
| 40  | GetAccountsLink      |
| 41  | GetAccountsLinkEx    |
| 42  | GetApiAccountsLink   |
| 43  | GetApiAccountsLinkEx |
| 50  |                      |
| 60  |                      |
| 61  |                      |
| 62  |                      |

## Cmd11

Takes a type-0x16 buffer with size 8. Returns a string.

The output string is used by [NIM](NIM%20services.md "wikilink") for the
"eid:%s" in the User-Agent strings.

[Category:Services](Category:Services "wikilink")

# nim

| Cmd | Name |
| --- | ---- |
| 1   |      |
| 2   |      |

## Cmd1

Takes a 0x10-byte input struct, from the output of cmd2.

## Cmd2

Takes a type-0x6 output buffer, for an array of 0x10-byte entries.
Returns an u32 for total output entries.

Doesn't return anything on a v2.1 system where sysupdate domains are
blocked.

# nim:shp

# ntc

Presumably Network Time
    Sync?

# Network

  - https://sun.hac.%%.d4c.nintendo.net/v1/system\_update\_meta?device\_id=%016llx
  - https://aqua.hac.%%.d4c.nintendo.net/required\_system\_update\_meta?device\_id=%016llx
  - https://%s.hac.%%.d4c.nintendo.net/t/%c/%016llx/%u?device\_id=%016llx
    Returns content like the below URL. This is the content for
    [NCA](NCA.md "wikilink")-type0. See below for %c. %016llx is
    titleID, %u is title-version.
  - https://%s.hac.%%.d4c.nintendo.net/c/%c/%s Used for downloading
    content. First %s is atumn or atum. %c is one of: 'c', 'a', or 's'.
    %s is just the hex-string NcaId. The server also returns two HTTP
    headers: "X-Nintendo-Content-Hash: {entire lowercase hex-string of
    the content SHA256 hash}" and "X-Nintendo-Content-ID: {lowercase
    hex-string for NcaId}"
  - https://superfly.hac.%%.d4c.nintendo.net/v1/t/%016llx/dv %016llx is
    titleID, only for eShop titles it appears. Returns .json title-info.
  - https://superfly.hac.%%.d4c.nintendo.net/v1/a/%016llx/dv %016llx is
    titleID, only for eShop titles it appears. Output is similar to
    above
    URL.
  - https://aauth-%.ndas.srv.nintendo.net/v1/time
  - https://beach.hac.%.eshop.nintendo.net/v1/rom\_cards?application\_id=%016llx\&rom\_card\_cert=%s
  - https://beach.hac.%.eshop.nintendo.net/v1/rom\_cards/register?application\_id=%016llx\&rom\_card\_cert=%s\&expected\_gold\_point=%d
  - https://beach.hac.%.eshop.nintendo.net/v1/my/devices/hac/link?lang=en
  - https://beach.hac.%.eshop.nintendo.net/v1/my/virtual\_account?lang=en
  - https://tagaya.hac.%.eshop.nintendo.net/tagaya/hac\_versionlist
  - ...
  - "https://dauth-%.ndas.srv.nintendo.net/v1/device\_auth\_token"
    CURLOPT\_POSTFIELDS is set to the output from: snprintf(...,
    "system\_version=%08x\&client\_id=%s",
    <output parsed from a func>
    , "<hard-coded hex string>");

These are not accessible without the required TLS client cert+privk,
minus the time URL which can be accessed without any client cert+privk
at all.

The returned content data from CDN, for both system-titles and
eShop-titles, is identical to the data readable by
[Content\_Manager\_services\#ReadEntryRaw](Content%20Manager%20services#ReadEntryRaw.md##ReadEntryRaw "wikilink").

While atumn seems to be for system-titles, and atum for eShop titles,
the latter titles are accessible fine with atumn(with "/t/" for
NCA-type0 at least).

'a' is used when an input u8 is not 0x3, otherwise 's' is used. This is
[title-type](Content%20Manager%20services#Title%20Types.md##Title_Types "wikilink")?
A seperate function using the ".../c/" URL is hard-coded to use 'c'.
This appears to match 's' usage attempts: the only URL that returned
actual data with 's' was with titleID 0100000000000816.

As of June 30, 2017, accessing old content via the atumn "/c/" and "/t/"
URLs works fine.

Going by strings in NIM, it appears SOAP isn't used anymore. ecs appears
to use REST API?

## User-Agent

NIM generates two User-Agent
strings:

` snprintf(..., "User-Agent: NintendoSDK Firmware/%s-%u (platform:%s; did:%016llx; eid:%s)", <string at `[`sysver`](System%20Version%20Title.md "wikilink")`+0x68>, {u32 from `[`sysver`](System%20Version%20Title.md "wikilink")`+4}, "NX", DeviceId, {`[`NSD`](NSD%20services.md "wikilink")` cmd11 output});`  
` snprintf(..., "User-Agent: NintendoSDK Firmware/%s-%u (platform:%s; eid:%s)", <string at `[`sysver`](System%20Version%20Title.md "wikilink")`+0x68>, {u32 from `[`sysver`](System%20Version%20Title.md "wikilink")`+4}, "NX", DeviceId, {`[`NSD`](NSD%20services.md "wikilink")` cmd11 output});`

Where the 64bit DeviceId is parsed from the 0x10-bytes at outbuf+0xC6
from [set:cal](Settings%20services.md "wikilink")
GetDeviceCert(DeviceCert\_certname+2, aka where the hex string for the
DeviceId is).

## sun

NIM sends a HTTP GET with the sun URL listed above to get the
title-listing of the latest system-titles, as .json. The deviceid in the
URL is the same one in the above User-Agent section. HTTP header
"Accept:application/json" is sent in the request.

The response is json with a "system\_update\_metas" block, containing
"title\_id" and "title\_version" entries. The actual server response
only contains 1 title.

Example, from 2.0
system:

`{"timestamp":REDACTED-TIMESTSAMP,"system_update_metas":[{"title_id":"0100000000000816","title_version":201327002}]}`

## aqua

The following response is json from accessing the above aqua URL:

`{` `"contents_delivery_required_title_id": "0100000000000816",`
`"contents_delivery_required_title_version": 0` `}`

A while after [3.0.0](3.0.0.md "wikilink") release, the above
title-version was changed to the one for v3.0("Last-Modified: Thu, 29
Jun 2017 00:00:04 GMT").

# nim

# nim:shp

# ntc

Presumably Network Time
    Sync?

# Network

  - https://sun.hac.%%.d4c.nintendo.net/v1/system\_update\_meta?device\_id=%016llx
  - ...
  - https://aqua.hac.%%.d4c.nintendo.net/required\_system\_update\_meta?device\_id=%016llx
  - https://%s.hac.%%.d4c.nintendo.net/t/%c/%016llx/%u?device\_id=%016llx
  - https://%s.hac.%%.d4c.nintendo.net/c/%c/%s
  - https://aauth-%.ndas.srv.nintendo.net/v1/time
  - ...
  - "https://dauth-%.ndas.srv.nintendo.net/v1/device\_auth\_token"
    CURLOPT\_POSTFIELDS is set to the output from: snprintf(...,
    "system\_version=%08x\&client\_id=%s",
    <output parsed from a func>
    , "<hard-coded hex string>");

These are not accessible without the required TLS client cert+privk,
minus the time URL which can be accessed without any client cert+privk
at all.

## User-Agent

NIM generates two User-Agent
strings:

` snprintf(..., "User-Agent: NintendoSDK Firmware/%s-%u (platform:%s; did:%016llx; eid:%s)", <string at `[`sysver`](System%20Version%20Title.md "wikilink")`+0x68>, {u32 from `[`sysver`](System%20Version%20Title.md "wikilink")`+4}, "NX", DeviceId, {`[`NSD`](NSD%20services.md "wikilink")` cmd11 output});`  
` snprintf(..., "User-Agent: NintendoSDK Firmware/%s-%u (platform:%s; eid:%s)", <string at `[`sysver`](System%20Version%20Title.md "wikilink")`+0x68>, {u32 from `[`sysver`](System%20Version%20Title.md "wikilink")`+4}, "NX", DeviceId, {`[`NSD`](NSD%20services.md "wikilink")` cmd11 output});`

Where the 64bit DeviceId is parsed from the 0x10-bytes at outbuf+0xC6
from [set:cal](Settings%20services.md "wikilink")
GetDeviceCert(DeviceCert\_certname+2, aka where the hex string for the
DeviceId is) This hex string is parsed as little-endian.

## sun

NIM sends a HTTP GET with the sun URL listed above to get the
title-listing of the latest system-titles, as .json. The deviceid in the
URL is the same one in the above User-Agent section. HTTP header
"Accept:application/json" is sent in the request.

The response is json with a "system\_update\_metas" block, containing
"title\_id" and "title\_version" entries.

Example, from 2.0
system:

`{"timestamp":REDACTED-TIMESTSAMP,"system_update_metas":[{"title_id":"0100000000000816","title_version":201327002}]}`

## aqua

The following response is json from accessing the above aqua URL:

`{` `"contents_delivery_required_title_id": "0100000000000816",`
`"contents_delivery_required_title_version": 0` `}`

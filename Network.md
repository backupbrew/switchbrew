This page documents DNS domains and lists information relevant to the
online services used by the Switch.

# Domains

Only HTTPS is used with these domains unless noted otherwise.

## CDN

The URLs for content delivery network servers on the Switch usually
follow this
format:

`{server_name}.hac.{environment}.{serverset}.nintendo.net`

Where:

`{server_name}: One of the registered server names.`  
`{environment}: "lp1" (production), "dd1" (development) or "sp1" (production lottest staging).`  
`{serverset}: "eshop" (online shop) or "d4c" (content delivery).`

### Servers

  - "[sun.hac.%.d4c.nintendo.net](#sun "wikilink")"
  - "[aqua.hac.%.d4c.nintendo.net](#aqua "wikilink")"
  - "[atum.hac.%.d4c.nintendo.net](#atum/atumn "wikilink")"
  - "[atumn.hac.%.d4c.nintendo.net](#atum/atumn "wikilink")"
  - "[superfly.hac.%.d4c.nintendo.net](#superfly "wikilink")"
  - "bugyo.hac.%.eshop.nintendo.net"
  - "[beach.hac.%.eshop.nintendo.net](#beach "wikilink")"
  - "pushmo.hac.%.eshop.nintendo.net"
  - "[tagaya.hac.%.eshop.nintendo.net](#tagaya "wikilink")"
  - \[5.0.0+\]
    "[pearljam.hac.%.eshop.nintendo.net](#pearljam "wikilink")"

#### sun

Used for checking whether a sysupdate is available. Equivalent to
NetUpdateSOAP from past systems.

[NIM](NIM%20services.md "wikilink") sends a HTTP GET with the sun URL to
get the title-listing of the latest system-titles, as .json. The
deviceid in the URL is the same one in the above User-Agent section.
HTTP header "Accept:application/json" is sent in the request.

The response is json with a "system\_update\_metas" block, containing
"title\_id" and "title\_version" entries. The actual server response
only contains 1 title.

Example, from 2.0
system:

`{"timestamp":REDACTED-TIMESTSAMP,"system_update_metas":[{"title_id":"0100000000000816","title_version":201327002}]}`

URLs:

`"https://sun.hac.%%.d4c.nintendo.net/v1/system_update_meta?device_id=%016llx"`

#### aqua

The following response is json from accessing the aqua URL:

`{` `"contents_delivery_required_title_id": "0100000000000816",`
`"contents_delivery_required_title_version": 0` `}`

A while after [3.0.0](3.0.0.md "wikilink") release, the above
title-version was changed to the one for v3.0("Last-Modified: Thu, 29
Jun 2017 00:00:04
GMT").

URLs:

`"https://aqua.hac.%%.d4c.nintendo.net/required_system_update_meta?device_id=%016llx"`

#### atum/atumn

CDN for system-titles.

While "atumn" seems to be for system-titles and "atum" for eShop titles,
the latter titles are accessible fine with atumn (with "/t/" for
NCA-type0 at least).

'a' is used when an input u8 is not 0x3, otherwise 's' is used. A
seperate function using the ".../c/" URL is hard-coded to use 'c'. This
appears to match 's' usage attempts: the only URL that returned actual
data with 's' was with titleID 0100000000000816.

As of June 30, 2017, accessing old content via the atumn "/c/" and "/t/"
URLs works
fine.

URLs:

`"https://%s.hac.%%.d4c.nintendo.net/t/%c/%016llx/%u?device_id=%016llx"`  
`Returns content like the below URL. First %s is atumn or atum. This is the content for `[`NCA`](NCA.md "wikilink")`-type0. See below for %c. %016llx is titleID, %u is title-version.`  
  
`"https://%s.hac.%%.d4c.nintendo.net/c/%c/%s"`  
`Used for downloading content. First %s is atumn or atum. %c is one of: 'c', 'a', or 's'. %s is just the hex-string NcaId. The server also returns two HTTP headers: "X-Nintendo-Content-Hash: {entire lowercase hex-string of the content SHA256 hash}" and "X-Nintendo-Content-ID: {lowercase hex-string for NcaId}"`

#### superfly

URLs:

`"https://superfly.hac.%%.d4c.nintendo.net/v1/t/%016llx/dv"`  
`%016llx is titleID, only for eShop titles it appears. Returns .json title-info.`  
  
`"https://superfly.hac.%%.d4c.nintendo.net/v1/a/%016llx/dv"`  
`%016llx is titleID, only for eShop titles it appears. Output is similar to above URL.`

#### tagaya

VersionList for eShop
titles.

URLs:

`"https://tagaya.hac.%.eshop.nintendo.net/tagaya/hac_versionlist"`

#### beach

URLs:

`"https://beach.hac.%.eshop.nintendo.net/v1/rom_cards?application_id=%016llx&rom_card_cert=%s"`  
`"https://beach.hac.%.eshop.nintendo.net/v1/rom_cards/register?application_id=%016llx&rom_card_cert=%s&expected_gold_point=%d"`  
`"https://beach.hac.%.eshop.nintendo.net/v1/my/devices/hac/link?lang=en"`  
`"https://beach.hac.%.eshop.nintendo.net/v1/my/virtual_account?lang=en"`

#### pearljam

URLs:

`[5.0.0+] "https://pearljam.hac.%.eshop.nintendo.net/sugar"`  
`[5.0.0+] "https://pearljam.hac.%.eshop.nintendo.net/civil"`

## Shop API

Domains for interacting with the online shop
API.

### Servers

  - "[ecs-%.hac.shop.nintendo.net](#ecs "wikilink")"
  - "[ias-%.hac.shop.nintendo.net](#ias "wikilink")"

#### ecs

URLs:

`"https://ecs-%.hac.shop.nintendo.net/ecs/services/rest/AccountGetETickets"`  
`"https://ecs-%.hac.shop.nintendo.net/ecs/services/rest/GetAccountStatus"`

#### ias

URLs:

`"https://ias-%.hac.shop.nintendo.net/ias/services/rest/Register"`  
`"https://ias-%.hac.shop.nintendo.net/ias/services/rest/GetChallenge"`  
`"https://ias-%.hac.shop.nintendo.net/ias/services/rest/Unregister"`  
`"https://ias-%.hac.shop.nintendo.net/ias/services/rest/GetRegistrationInfo"`  
`"https://ias-%.hac.shop.nintendo.net/ias/services/rest/CompleteETicketSync"`  
`"https://ias-%.hac.shop.nintendo.net/ias/services/rest/AccountTransfer"`  
`"https://ias-%.hac.shop.nintendo.net/ias/services/rest/SyncRegistration"`

## Services

The URLs for general online service servers on the Switch usually follow
one of these
formats:

`{server_name}.{environment}.{service_name}.srv.nintendo.net`  
`{server_name}-{environment}.{service_name}.srv.nintendo.net`

Where:

`{server_name}: One of the registered server names.`  
`{environment}: "lp1" (production), "dd1" (development) or "sp1" (production lottest staging).`  
`{service_name}: One of the various service names.`

### Servers

  - "[aauth-%.ndas.srv.nintendo.net](#aauth "wikilink")"
  - "[dauth-%.ndas.srv.nintendo.net](#dauth "wikilink")"
  - "[api-%.znc.srv.nintendo.net](#znc "wikilink")"
  - "api-%.pctl.srv.nintendo.net"
  - "api-%.frs.srv.nintendo.net"
  - "app-b01.%.npns.srv.nintendo.net"
  - "broker.%.npns.srv.nintendo.net"
  - "consumer.%.npns.srv.nintendo.net"
  - "receive-%.dg.srv.nintendo.net"
  - "receive-%.er.srv.nintendo.net"

#### aauth

Application authentication.

URLs:

`"https://aauth-%.ndas.srv.nintendo.net/v1/application_auth_token"`  
`"https://aauth-%.ndas.srv.nintendo.net/v1/time"`

#### dauth

Device
authentication.

URLs:

`"https://dauth-%.ndas.srv.nintendo.net/v1/device_auth_token"`  
`CURLOPT_POSTFIELDS is set to the output from: snprintf(..., "system_version=%08x&client_id=%s", <byte-swapped first 3 bytes from `[`System_Version_Title`](System%20Version%20Title.md "wikilink")` loaded via `[`settings`](Settings%20services.md "wikilink")` cmd>, "`<hard-coded hex string>`");`

#### znc

Used by the Switch Online app to get app data, like the list of
game-specific services to display.

## Others

Miscellaneous domains for various APIs and tests.

### Servers

Account metadata:

  - "e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com"
  - "api.accounts.nintendo.com"

News and game content:

  - "bcat-topics-%.cdn.nintendo.net"
  - "bcat-list-%.cdn.nintendo.net"
  - "service-status-%.cdn.nintendo.net"
  - "g<game_server_id>-%.s.n.srv.nintendo.net"

Connection:

  - "ctest.cdn.nintendo.net" (replaces "conntest.nintendowifi.net")
  - "nasc.nintendowifi.net"

# User-Agent

[NIM](NIM%20services.md "wikilink") generates two User-Agent
strings:

`snprintf(..., "User-Agent: NintendoSDK Firmware/%s-%u (platform:%s; did:%016llx; eid:%s)", <string at `[`sysver`](System%20Version%20Title.md "wikilink")`+0x68>, {u32 from `[`sysver`](System%20Version%20Title.md "wikilink")`+4}, "NX", DeviceId, {`[`GetEnvironmentIdentifier`](Sockets%20services#GetEnvironmentIdentifier.md##GetEnvironmentIdentifier "wikilink")` output});`  
` `  
`snprintf(..., "User-Agent: NintendoSDK Firmware/%s-%u (platform:%s; eid:%s)", <string at `[`sysver`](System%20Version%20Title.md "wikilink")`+0x68>, {u32 from `[`sysver`](System%20Version%20Title.md "wikilink")`+4}, "NX", DeviceId, {`[`GetEnvironmentIdentifier`](Sockets%20services#GetEnvironmentIdentifier.md##GetEnvironmentIdentifier "wikilink")` output});`

Where the 64bit DeviceId is parsed from the 0x10-bytes at outbuf+0xC6
from [set:cal](Settings%20services.md "wikilink")
GetEciDeviceCertificate (DeviceCert\_certname+2, aka where the hex
string for the DeviceId is).

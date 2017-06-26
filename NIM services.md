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

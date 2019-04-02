The Nintendo Switch uses Tegra's Security Engine (SE) for handling
cryptographic opearations at the system's lowest level.

The SE driver is mapped to physical address 0x70012000 with a total size
of 0x2000 bytes and exposes several registers for programming the
Security Engine.

# Registers

| Name                           | Address    |
| ------------------------------ | ---------- |
| SE\_SECURITY                   | 0x70012000 |
| SE\_TZRAM\_SECURITY            | 0x70012004 |
| SE\_OPERATION                  | 0x70012008 |
| SE\_INT\_ENABLE                | 0x7001200C |
| SE\_INT\_STATUS                | 0x70012010 |
| SE\_CONFIG                     | 0x70012014 |
| SE\_IN\_LL\_ADDR               | 0x70012018 |
| SE\_OUT\_LL\_ADDR              | 0x70012024 |
| SE\_HASH\_RESULT0\_0           | 0x70012030 |
| SE\_HASH\_RESULT0\_1           | 0x70012034 |
| SE\_HASH\_RESULT0\_2           | 0x70012038 |
| SE\_HASH\_RESULT0\_3           | 0x7001203C |
| SE\_HASH\_RESULT1\_0           | 0x70012040 |
| SE\_HASH\_RESULT1\_1           | 0x70012044 |
| SE\_HASH\_RESULT1\_2           | 0x70012048 |
| SE\_HASH\_RESULT1\_3           | 0x7001204C |
| SE\_HASH\_RESULT2\_0           | 0x70012050 |
| SE\_HASH\_RESULT2\_1           | 0x70012054 |
| SE\_HASH\_RESULT2\_2           | 0x70012058 |
| SE\_HASH\_RESULT2\_3           | 0x7001205C |
| SE\_HASH\_RESULT3\_0           | 0x70012060 |
| SE\_HASH\_RESULT3\_1           | 0x70012064 |
| SE\_HASH\_RESULT3\_2           | 0x70012068 |
| SE\_HASH\_RESULT3\_3           | 0x7001206C |
| SE\_CTX\_SAVE\_CONFIG          | 0x70012070 |
| SE\_CTX\_SAVE\_AUTO            | 0x70012074 |
| SE\_SHA\_CONFIG                | 0x70012200 |
| SE\_SHA\_MSG\_LENGTH0          | 0x70012204 |
| SE\_SHA\_MSG\_LENGTH1          | 0x70012208 |
| SE\_SHA\_MSG\_LENGTH2          | 0x7001220C |
| SE\_SHA\_MSG\_LENGTH3          | 0x70012210 |
| SE\_SHA\_MSG\_LEFT0            | 0x70012214 |
| SE\_SHA\_MSG\_LEFT1            | 0x70012218 |
| SE\_SHA\_MSG\_LEFT2            | 0x7001221C |
| SE\_SHA\_MSG\_LEFT3            | 0x70012220 |
| SE\_CRYPTO\_KEY\_READ\_DISABLE | 0x70012280 |
| SE\_CRYPTO\_KEYTABLE\_ACCESS   | 0x70012284 |
| SE\_CRYPTO\_CONFIG             | 0x70012304 |
| SE\_CRYPTO\_CTR                | 0x70012308 |
| SE\_CRYPTO\_BLOCK\_COUNT       | 0x70012318 |
| SE\_CRYPTO\_KEYTABLE\_ADDR     | 0x7001231C |
| SE\_CRYPTO\_KEYTABLE\_DATA     | 0x70012320 |
| SE\_CRYPTO\_KEYTABLE\_DST      | 0x70012330 |
| SE\_RNG\_CONFIG                | 0x70012340 |
| SE\_RNG\_SRC\_CONFIG           | 0x70012344 |
| SE\_RNG\_RESEED\_INTERVAL      | 0x70012348 |
| SE\_RSA\_CONFIG                | 0x70012400 |
| SE\_RSA\_KEY\_SIZE             | 0x70012404 |
| SE\_RSA\_EXP\_SIZE             | 0x70012408 |
| SE\_RSA\_KEY\_READ\_DISABLE    | 0x7001240C |
| SE\_RSA\_KEYTABLE\_ACCESS      | 0x70012410 |
| SE\_RSA\_KEYTABLE\_ADDR        | 0x70012420 |
| SE\_RSA\_KEYTABLE\_DATA        | 0x70012424 |
| SE\_RSA\_OUTPUT                | 0x70012428 |
| SE\_STATUS                     | 0x70012800 |
| SE\_ERR\_STATUS                | 0x70012804 |
| SE\_SPARE                      | 0x7001280C |

The security engine (SE) is responsible for the crypto done on the
switch. SE is mapped to physical address 0x70012000.

# SE registers

| Register                           | Offset |
| ---------------------------------- | ------ |
| OPERATION\_REG\_OFFSET             | 0x008  |
| INT\_ENABLE\_REG\_OFFSET           | 0x00C  |
| INT\_STATUS\_REG\_OFFSET           | 0x010  |
| CONFIG\_REG\_OFFSET                | 0x014  |
| IN\_LL\_ADDR\_REG\_OFFSET          | 0x018  |
| OUT\_LL\_ADDR\_REG\_OFFSET         | 0x024  |
| HASH\_RESULT\_REG\_OFFSET          | 0x030  |
| CONTEXT\_SAVE\_CONFIG\_REG\_OFFSET | 0x070  |
| SHA\_CONFIG\_REG                   | 0x200  |
| SHA\_MSG\_LENGTH\_REG              | 0x204  |
| SHA\_MSG\_LEFT\_REG                | 0x214  |
| KEYSLOT\_1                         | 0x284  |
| KEYSLOT\_2                         | 0x288  |
| KEYSLOT\_3                         | 0x28C  |
| KEYSLOT\_4                         | 0x290  |
| KEYSLOT\_5                         | 0x294  |
| KEYSLOT\_6                         | 0x298  |
| KEYSLOT\_7                         | 0x29C  |
| KEYSLOT\_8                         | 0x2A0  |
| KEYSLOT\_9                         | 0x2A4  |
| KEYSLOT\_10                        | 0x2A8  |
| KEYSLOT\_11                        | 0x2AC  |
| KEYSLOT\_12                        | 0x2B0  |
| KEYSLOT\_13                        | 0x2B4  |
| KEYSLOT\_14                        | 0x2B8  |
| KEYSLOT\_15                        | 0x2BC  |
| KEYSLOT\_16                        | 0x2C0  |
| CRYPTO\_REG                        | 0x304  |
| CRYPTO\_CTR\_REG                   | 0x308  |
| BLOCK\_COUNT\_REG                  | 0x318  |
| KEYTABLE\_REG                      | 0x31C  |
| KEYTABLE\_DATA0\_REG               | 0x320  |
| CRYPTO\_KEYTABLE\_DST\_REG         | 0x330  |
| RNG\_CONFIG\_REG                   | 0x340  |
| RNG\_SRC\_CONFIG\_REG              | 0x344  |
| RNG\_RESEED\_INTERVAL\_REG         | 0x348  |
| RSA\_CONFIG                        | 0x400  |
| RSA\_KEY\_SIZE\_REG\_OFFSET        | 0x404  |
| RSA\_EXP\_SIZE\_REG\_OFFSET        | 0x408  |
| RSA\_KEYSLOT\_1                    | 0x410  |
| RSA\_KEYSLOT\_2                    | 0x414  |
| RSA\_KEYTABLE\_ADDR                | 0x420  |
| RSA\_KEYTABLE\_DATA                | 0x424  |
| RSA\_OUTPUT                        | 0x428  |
| SPARE\_0\_REG\_OFFSET              | 0x80C  |

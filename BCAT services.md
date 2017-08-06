BCAT (Background Content Asymmetric synchronized delivery and
Transmission) encompasses a set of content download/upload related
services.

# BCAT services

Equivalent to 3DS BOSS(SpotPass). See
[here](BCAT%20Content%20Container.md "wikilink") for
BCAT-content-container.

## bcat:u

## bcat:s

## bcat:m

## bcat:a

# News services

## news:p

## news:v

## news:m

## news:c

## news:a

# Play Report services

The "Play Report" (prepo) service uploads system and user information to
a cloud server. This includes the following fields:

`sys_info`  
`data`  
`application_id`  
`event_id`  
`operation_mode`  
`lc_recorded_at (followed by a timestamp)`  
`nc_recorded_at (followed by a timestamp)`  
`nsa_id`  
`os_version`

And the contents of the following file:

`is_user_agreement_check_enabled.bin`

All the information is periodically uploaded to the following URL:  
\* https://receive-%.dg.srv.nintendo.net/post

It also checks the validity of the device's authentication token using
the following URL:  
\* https://dauth-%.ndas.srv.nintendo.net/v1/device\_auth\_token

## prepo:u

## prepo:s

| Cmd   | Name |
| ----- | ---- |
| 10100 |      |
| 10101 |      |
| 10200 |      |
| 10300 |      |
| 20100 |      |
| 20101 |      |
| 30100 |      |
| 40100 |      |
| 40101 |      |
| 90100 |      |

## prepo:m

## prepo:a

[Category:Services](Category:Services "wikilink")

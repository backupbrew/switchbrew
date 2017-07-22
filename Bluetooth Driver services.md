# btdrv

The bluetooth driver implements the bluetooth protocol over h4/uart.

It interfaces with the [uart](Uart.md "wikilink") service to actually
talk with the bluetooth hardware.

The code seems to be derived from a broadcom stack. A good starting
point for similar source code can be found in the MICO project:
<https://github.com/yinhongxing/mico/tree/ea67ff3659f12d730d4dc3b8d547b093bd2ee2ee/MICO/bluetooth_bte>
Note that the library files contain many (symbolized) functions which
match btdrv.

| Cmd | Name      |
| --- | --------- |
| 0   |           |
| 1   |           |
| 2   |           |
| 3   |           |
| 4   |           |
| 5   |           |
| 6   |           |
| 7   |           |
| 8   |           |
| 9   |           |
| 10  |           |
| 11  |           |
| 12  |           |
| 13  |           |
| 14  |           |
| 15  |           |
| 16  |           |
| 17  |           |
| 18  |           |
| 19  | SendData  |
| 20  |           |
| 21  | SetReport |
| 22  | GetReport |
| 23  |           |
| 24  |           |
| 25  |           |
| 26  |           |
| 27  |           |
| 28  |           |
| 29  |           |
| 30  |           |
| 31  |           |
| 32  |           |
| 33  |           |
| 34  |           |
| 35  |           |
| 36  |           |
| 37  |           |
| 38  |           |
| 39  |           |

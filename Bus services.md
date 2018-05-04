# gpio

This is "nn::gpio::IManager".

| Cmd | Name                                                   |
| --- | ------------------------------------------------------ |
| 0   | [\#OpenSessionForDev](#OpenSessionForDev "wikilink")   |
| 1   | [\#OpenSession](#OpenSession "wikilink")               |
| 2   | [\#OpenSessionForTest](#OpenSessionForTest "wikilink") |
| 3   | IsWakeEventActive                                      |
| 4   | GetWakeEventActiveFlagSet                              |
| 5   | SetWakeEventActiveFlagSetForDebug                      |
| 6   | SetWakePinDebugMode                                    |
| 7   | \[5.0.0+\] [\#OpenSession2](#OpenSession2 "wikilink")  |
| 8   | \[5.0.0+\] IsWakeEventActive2                          |
| 9   | \[5.0.0+\] SetWakeEventActiveFlagSetForDebug2          |

## Known Devices

<table>
<thead>
<tr class="header">
<th><p>GpioPadName</p></th>
<th><p>GpioPadDescriptor</p></th>
<th><p>Tegra (port, pin)</p></th>
<th><p>Usage</p></th>
<th><p>Direction</p></th>
<th><p>Used by</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x01</p></td>
<td><p>0xCC</p></td>
<td><p>Z, 4</p></td>
<td><p>rt5639 power (CODEC_LDO_EN)</p></td>
<td><p>Out</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko<br />
(<a href="Audio services.md" title="wikilink">Audio services</a>, <a href="Fatal services.md" title="wikilink">Fatal services</a>)</p></td>
</tr>
<tr class="even">
<td><p>0x02</p></td>
<td><p>0x24</p></td>
<td><p>E, 4</p></td>
<td><p>SDCard Power</p></td>
<td><p>Out</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko<br />
(<a href="Filesystem services.md" title="wikilink">Filesystem services</a>)</p></td>
</tr>
<tr class="odd">
<td><p>0x03</p></td>
<td><p>0x3C</p></td>
<td><p>H, 4</p></td>
<td><p>BT_RST_PH4</p></td>
<td><p>Out</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko<br />
(<a href="Bluetooth Driver services.md" title="wikilink">Bluetooth Driver services</a>)</p></td>
</tr>
<tr class="even">
<td><p>0x04</p></td>
<td><p>0xDA</p></td>
<td><p>BB, 2</p></td>
<td></td>
<td><p>In</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko</p></td>
</tr>
<tr class="odd">
<td><p>0x05</p></td>
<td><p>0xDB</p></td>
<td><p>BB, 3</p></td>
<td><p>GcAsic Power</p></td>
<td><p>Out</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko<br />
(<a href="Filesystem services.md" title="wikilink">Filesystem services</a>)</p></td>
</tr>
<tr class="even">
<td><p>0x06</p></td>
<td><p>0xDC</p></td>
<td><p>BB, 4</p></td>
<td><p>Headphone Detect</p></td>
<td><p>In</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko<br />
(<a href="Audio services.md" title="wikilink">Audio services</a>)</p></td>
</tr>
<tr class="odd">
<td><p>0x07</p></td>
<td><p>0x25</p></td>
<td><p>E, 5</p></td>
<td></td>
<td><p>Out</p></td>
<td><p>Icosa, Copper, Hoag</p></td>
</tr>
<tr class="even">
<td><p>0x08</p></td>
<td><p>0x90</p></td>
<td><p>S, 0</p></td>
<td><p>DebugPadDriver</p></td>
<td><p>In</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko<br />
(<a href="HID services.md" title="wikilink">HID services</a>)</p></td>
</tr>
<tr class="odd">
<td><p>0x09</p></td>
<td><p>0x91</p></td>
<td><p>S, 1</p></td>
<td></td>
<td><p>In</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko</p></td>
</tr>
<tr class="even">
<td><p>0x0A</p></td>
<td><p>0x96</p></td>
<td><p>S, 6</p></td>
<td><p>bq24192 Charge Enable</p></td>
<td><p>Out</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko<br />
(<a href="PTM services.md" title="wikilink">PTM services</a>)</p></td>
</tr>
<tr class="odd">
<td><p>0x0B</p></td>
<td><p>0x97</p></td>
<td><p>S, 7</p></td>
<td><p>CPU fan sampling</p></td>
<td><p>In</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko</p></td>
</tr>
<tr class="even">
<td><p>0x0C</p></td>
<td><p>0x26</p></td>
<td><p>E, 6</p></td>
<td><p>Joycon(L) IsAttached (insertion, Joy-Con pin 5/console TX, pulled low on insert?)</p></td>
<td><p>In</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko<br />
(<a href="HID services.md" title="wikilink">HID services</a>)</p></td>
</tr>
<tr class="odd">
<td><p>0x0D</p></td>
<td><p>0x05</p></td>
<td><p>A, 5</p></td>
<td><p>Fan enable (normal)</p></td>
<td><p>Out</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko<br />
(<a href="PTM services.md" title="wikilink">PTM services</a>)</p></td>
</tr>
<tr class="even">
<td><p>0x0E</p></td>
<td><p>0x78</p></td>
<td><p>P, 0</p></td>
<td><p>SDMMC3_CLK_PP0?</p></td>
<td><p>In</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko</p></td>
</tr>
<tr class="odd">
<td><p>0x0F</p></td>
<td><p>0x93</p></td>
<td><p>S, 3</p></td>
<td><p>GcAsic irq</p></td>
<td><p>In</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko<br />
(<a href="Filesystem services.md" title="wikilink">Filesystem services</a>)</p></td>
</tr>
<tr class="even">
<td><p>0x10</p></td>
<td><p>0x7D</p></td>
<td><p>P, 5</p></td>
<td><p>SDMMC3_DAT0_PP5?</p></td>
<td><p>In</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko</p></td>
</tr>
<tr class="odd">
<td><p>0x11</p></td>
<td><p>0x7C</p></td>
<td><p>P, 4</p></td>
<td><p>SDMMC3_DAT1_PP4?</p></td>
<td><p>In</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko</p></td>
</tr>
<tr class="even">
<td><p>0x12</p></td>
<td><p>0x7B</p></td>
<td><p>P, 3</p></td>
<td><p>SDMMC3_DAT2_PP3?</p></td>
<td><p>In</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko</p></td>
</tr>
<tr class="odd">
<td><p>0x13</p></td>
<td><p>0x7A</p></td>
<td><p>P, 2</p></td>
<td><p>SDMMC3_DAT3_PP2?</p></td>
<td><p>In</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko</p></td>
</tr>
<tr class="even">
<td><p>0x14</p></td>
<td><p>0xBC</p></td>
<td><p>X, 4</p></td>
<td><p>Temperature sensor</p></td>
<td><p>In</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko</p></td>
</tr>
<tr class="odd">
<td><p>0x15</p></td>
<td><p>0xAE</p></td>
<td><p>V, 6</p></td>
<td></td>
<td><p>In</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko<br />
(<a href="Audio services.md" title="wikilink">Audio services</a>)</p></td>
</tr>
<tr class="even">
<td><p>0x16</p></td>
<td><p>0xBA</p></td>
<td><p>X, 2</p></td>
<td><p>MOTION_INT_PX2?</p></td>
<td><p>In</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko</p></td>
</tr>
<tr class="odd">
<td><p>0x17</p></td>
<td><p>0xB9</p></td>
<td><p>X, 1</p></td>
<td><p>Touchscreen IRQ (TOUCH_INT_PX1) (unused - polled instead)</p></td>
<td><p>In</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko<br />
(<a href="HID services.md" title="wikilink">HID services</a>)</p></td>
</tr>
<tr class="even">
<td><p>0x18</p></td>
<td><p>0xBD</p></td>
<td><p>X, 5</p></td>
<td><p>Power Button (BUTTON_POWER_ON_PX5)</p></td>
<td><p>In</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko</p></td>
</tr>
<tr class="odd">
<td><p>0x19</p></td>
<td><p>0xBE</p></td>
<td><p>X, 6</p></td>
<td><p>Volume Up (BUTTON_VOL_UP_PX6)</p></td>
<td><p>In</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko<br />
(<a href="Boot2.md" title="wikilink">Boot2</a>, <a href="Audio services.md" title="wikilink">Audio services</a>)</p></td>
</tr>
<tr class="even">
<td><p>0x1A</p></td>
<td><p>0xBF</p></td>
<td><p>X, 7</p></td>
<td><p>Volume Down (BUTTON_VOL_DOWN_PX7)</p></td>
<td><p>In</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko<br />
(<a href="Boot2.md" title="wikilink">Boot2</a>, <a href="Audio services.md" title="wikilink">Audio services</a>)</p></td>
</tr>
<tr class="odd">
<td><p>0x1B</p></td>
<td><p>0xC0</p></td>
<td><p>Y, 0</p></td>
<td><p>max17050 irq</p></td>
<td><p>In</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko<br />
(<a href="PTM services.md" title="wikilink">PTM services</a>)</p></td>
</tr>
<tr class="even">
<td><p>0x1C</p></td>
<td><p>0xC1</p></td>
<td><p>Y, 1</p></td>
<td><p>BUTTON_HOME_PY1</p></td>
<td><p>In</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko</p></td>
</tr>
<tr class="odd">
<td><p>0x1D</p></td>
<td><p>0xA9</p></td>
<td><p>V, 1</p></td>
<td><p>Backlight (LCD_BL_EN_PV1)</p></td>
<td><p>Out</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko<br />
(<a href="NV services.md" title="wikilink">NV services</a>, <a href="Backlight services.md" title="wikilink">Backlight services</a>)</p></td>
</tr>
<tr class="even">
<td><p>0x1E</p></td>
<td><p>0xAA</p></td>
<td><p>V, 2</p></td>
<td><p>Backlight (LCD_RST_PV2)</p></td>
<td><p>Out</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko<br />
(<a href="NV services.md" title="wikilink">NV services</a>)</p></td>
</tr>
<tr class="odd">
<td><p>0x1F</p></td>
<td><p>0x55</p></td>
<td><p>K, 5</p></td>
<td><p>bq24192 OTG charge select</p></td>
<td><p>Out</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko<br />
(<a href="PTM services.md" title="wikilink">PTM services</a>, <a href="USB services.md" title="wikilink">USB services</a>)</p></td>
</tr>
<tr class="even">
<td><p>0x20</p></td>
<td><p>0xAD</p></td>
<td><p>V, 5</p></td>
<td><p>PD related</p></td>
<td><p>Out</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko<br />
(<a href="USB services.md" title="wikilink">USB services</a>)</p></td>
</tr>
<tr class="odd">
<td><p>0x21</p></td>
<td><p>0xC8</p></td>
<td><p>Z, 0</p></td>
<td><p>bq24192 irq</p></td>
<td><p>In</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko<br />
(<a href="PTM services.md" title="wikilink">PTM services</a>)</p></td>
</tr>
<tr class="even">
<td><p>0x22</p></td>
<td><p>0xCA</p></td>
<td><p>Z, 2</p></td>
<td></td>
<td><p>In</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko</p></td>
</tr>
<tr class="odd">
<td><p>0x23</p></td>
<td><p>0xCB</p></td>
<td><p>Z, 3</p></td>
<td></td>
<td><p>In</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko</p></td>
</tr>
<tr class="even">
<td><p>0x24</p></td>
<td><p>0x4F</p></td>
<td><p>J, 7</p></td>
<td><p>Touchscreen reset</p></td>
<td><p>Out</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko<br />
(<a href="HID services.md" title="wikilink">HID services</a>)</p></td>
</tr>
<tr class="odd">
<td><p>0x25</p></td>
<td><p>0x50</p></td>
<td><p>K, 0</p></td>
<td></td>
<td><p>In</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko</p></td>
</tr>
<tr class="even">
<td><p>0x26</p></td>
<td><p>0x51</p></td>
<td><p>K, 1</p></td>
<td></td>
<td><p>In</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko</p></td>
</tr>
<tr class="odd">
<td><p>0x27</p></td>
<td><p>0x52</p></td>
<td><p>K, 2</p></td>
<td></td>
<td><p>In</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko</p></td>
</tr>
<tr class="even">
<td><p>0x28</p></td>
<td><p>0x54</p></td>
<td><p>K, 4</p></td>
<td><p>bm92t36 irq</p></td>
<td><p>In</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko<br />
(<a href="USB services.md" title="wikilink">USB services</a>)</p></td>
</tr>
<tr class="odd">
<td><p>0x29</p></td>
<td><p>0x56</p></td>
<td><p>K, 6</p></td>
<td></td>
<td><p>In</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko</p></td>
</tr>
<tr class="even">
<td><p>0x2A</p></td>
<td><p>0x57</p></td>
<td><p>K, 7</p></td>
<td></td>
<td><p>In</p></td>
<td><p>Icosa, Copper, Hoag</p></td>
</tr>
<tr class="odd">
<td><p>0x2B</p></td>
<td><p>0x53</p></td>
<td><p>K, 3</p></td>
<td><p>joycon(R) NwcpDriver1.NwcpCharger</p></td>
<td><p>Out</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko<br />
(<a href="HID services.md" title="wikilink">HID services</a>)</p></td>
</tr>
<tr class="even">
<td><p>0x2C</p></td>
<td><p>0xE3</p></td>
<td><p>CC, 3</p></td>
<td><p>joycon(L) NwcpDriver0.NwcpCharger</p></td>
<td><p>Out</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko<br />
(<a href="HID services.md" title="wikilink">HID services</a>)</p></td>
</tr>
<tr class="odd">
<td><p>0x2D</p></td>
<td><p>0x38</p></td>
<td><p>H, 0</p></td>
<td><p>WIFI_EN_PH0?</p></td>
<td><p>Out</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko</p></td>
</tr>
<tr class="even">
<td><p>0x2E</p></td>
<td><p>0x39</p></td>
<td><p>H, 1</p></td>
<td><p>WIFI_RST_PH1</p></td>
<td><p>Out</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko<br />
(<a href="Wlan services.md" title="wikilink">Wlan services</a>, <a href="PCIe services.md" title="wikilink">PCIe services</a>)</p></td>
</tr>
<tr class="odd">
<td><p>0x2F</p></td>
<td><p>0x3B</p></td>
<td><p>H, 3</p></td>
<td><p>AP_WAKE_BT_PH3</p></td>
<td><p>Out</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko<br />
(<a href="Bluetooth Driver services.md" title="wikilink">Bluetooth Driver services</a>)</p></td>
</tr>
<tr class="even">
<td><p>0x30</p></td>
<td><p>0x3D</p></td>
<td><p>H, 5</p></td>
<td></td>
<td><p>In</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko</p></td>
</tr>
<tr class="odd">
<td><p>0x31</p></td>
<td><p>0x3F</p></td>
<td><p>H, 7</p></td>
<td></td>
<td><p>Out</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko</p></td>
</tr>
<tr class="even">
<td><p>0x32</p></td>
<td><p>0x40</p></td>
<td><p>I, 0</p></td>
<td><p>Backlight +5V</p></td>
<td><p>Out</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko<br />
(<a href="NV services.md" title="wikilink">NV services</a>)</p></td>
</tr>
<tr class="odd">
<td><p>0x33</p></td>
<td><p>0x41</p></td>
<td><p>I, 1</p></td>
<td><p>Backlight -5V</p></td>
<td><p>Out</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko<br />
(<a href="NV services.md" title="wikilink">NV services</a>)</p></td>
</tr>
<tr class="even">
<td><p>0x34</p></td>
<td><p>0x3E</p></td>
<td><p>H, 6</p></td>
<td><p>Joycon(R) IsAttached (insertion, Joy-Con pin 5/console TX, pulled low on insert?)</p></td>
<td><p>In</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko<br />
(<a href="HID services.md" title="wikilink">HID services</a>)</p></td>
</tr>
<tr class="odd">
<td><p>0x35</p></td>
<td><p>0xE2</p></td>
<td><p>CC, 2</p></td>
<td></td>
<td><p>In</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko</p></td>
</tr>
<tr class="even">
<td><p>0x36</p></td>
<td><p>0xE4</p></td>
<td><p>CC, 4</p></td>
<td><p>Fan enable (high power)</p></td>
<td><p>Out</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko<br />
(<a href="PTM services.md" title="wikilink">PTM services</a>)</p></td>
</tr>
<tr class="odd">
<td><p>0x37</p></td>
<td><p>0x3A</p></td>
<td><p>H, 2</p></td>
<td></td>
<td><p>In</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko</p></td>
</tr>
<tr class="even">
<td><p>0x38</p></td>
<td><p>0xC9</p></td>
<td><p>Z, 1</p></td>
<td><p>SDCard Card Detect</p></td>
<td><p>In</p></td>
<td><p>Icosa, Copper, Hoag, [5.0.0+] Mariko<br />
(<a href="Filesystem services.md" title="wikilink">Filesystem services</a>)</p></td>
</tr>
<tr class="odd">
<td><p>0x39</p></td>
<td><p>0x4D</p></td>
<td><p>J, 5</p></td>
<td><p>bq24192 OTG charge select</p></td>
<td><p>Out</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko<br />
(<a href="PTM services.md" title="wikilink">PTM services</a>, <a href="USB services.md" title="wikilink">USB services</a>)</p></td>
</tr>
<tr class="even">
<td><p>0x3A</p></td>
<td><p>0x58</p></td>
<td><p>L, 0</p></td>
<td><p>bq24192 OTG charge select</p></td>
<td><p>Out</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko<br />
(<a href="PTM services.md" title="wikilink">PTM services</a>, <a href="USB services.md" title="wikilink">USB services</a>)</p></td>
</tr>
<tr class="odd">
<td><p>0x3B</p></td>
<td><p>0x3E</p></td>
<td><p>H, 6</p></td>
<td><p>joycon(R) NwcpDriver1.GpioMonitorTask0 duplicate?</p></td>
<td><p>In</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko</p></td>
</tr>
<tr class="even">
<td><p>0x3C</p></td>
<td><p>0x26</p></td>
<td><p>E, 6</p></td>
<td><p>joycon(L) NwcpDriver1.GpioMonitorTask0 duplicate?</p></td>
<td><p>In</p></td>
<td><p>Icosa, Hoag, [5.0.0+] Mariko</p></td>
</tr>
<tr class="odd">
<td><p>0x3D</p></td>
<td><p>-1</p></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>0x3E</p></td>
<td><p>0x33</p></td>
<td><p>G, 3</p></td>
<td><p>joycon(R) NwcpDriver1.GpioMonitorTask1 (CTS, checked low)</p></td>
<td><p>In</p></td>
<td><p>None<br />
(<a href="HID services.md" title="wikilink">HID services</a>)</p></td>
</tr>
<tr class="odd">
<td><p>0x3F</p></td>
<td><p>0x1C</p></td>
<td><p>D, 4</p></td>
<td><p>joycon(L) NwcpDriver0.GpioMonitorTask1 (CTS, checked low)</p></td>
<td><p>In</p></td>
<td><p>None<br />
(<a href="HID services.md" title="wikilink">HID services</a>)</p></td>
</tr>
<tr class="even">
<td><p>0x40</p></td>
<td><p>0xD9</p></td>
<td><p>BB, 1</p></td>
<td></td>
<td><p>Out</p></td>
<td><p>[2.0.0+] Copper</p></td>
</tr>
<tr class="odd">
<td><p>0x41</p></td>
<td><p>0x0C</p></td>
<td><p>B, 4</p></td>
<td><p>Lid Closed (unused)</p></td>
<td><p>In</p></td>
<td><p>[2.0.0+] Copper</p></td>
</tr>
<tr class="even">
<td><p>0x42</p></td>
<td><p>0x0D</p></td>
<td><p>B, 5</p></td>
<td></td>
<td><p>In</p></td>
<td><p>[2.0.0+] Copper</p></td>
</tr>
<tr class="odd">
<td><p>0x43</p></td>
<td><p>0x21</p></td>
<td><p>E, 1</p></td>
<td><p>USB power</p></td>
<td><p>Out</p></td>
<td><p>[2.0.0+] Copper<br />
(<a href="USB services.md" title="wikilink">USB services</a>)</p></td>
</tr>
<tr class="even">
<td><p>0x44</p></td>
<td><p>0x27</p></td>
<td><p>E, 7</p></td>
<td></td>
<td><p>In</p></td>
<td><p>[2.0.0+] Copper</p></td>
</tr>
<tr class="odd">
<td><p>0x45</p></td>
<td><p>0x92</p></td>
<td><p>S, 2</p></td>
<td></td>
<td><p>In</p></td>
<td><p>[2.0.0+] Copper</p></td>
</tr>
<tr class="even">
<td><p>0x46</p></td>
<td><p>0x95</p></td>
<td><p>S, 5</p></td>
<td><p>USB root port 4 power</p></td>
<td><p>Out</p></td>
<td><p>[2.0.0+] Copper<br />
(<a href="USB services.md" title="wikilink">USB services</a>)</p></td>
</tr>
<tr class="odd">
<td><p>0x47</p></td>
<td><p>0x98</p></td>
<td><p>T, 0</p></td>
<td><p>USB root port 3 power</p></td>
<td><p>Out</p></td>
<td><p>[2.0.0+] Copper<br />
(<a href="USB services.md" title="wikilink">USB services</a>)</p></td>
</tr>
<tr class="even">
<td><p>0x48</p></td>
<td><p>0x10</p></td>
<td><p>C, 0</p></td>
<td><p>HdmiHotplug</p></td>
<td><p>Out</p></td>
<td><p>[2.0.0+] Copper<br />
(<a href="NV services.md" title="wikilink">NV services</a>)</p></td>
</tr>
<tr class="odd">
<td><p>0x49</p></td>
<td><p>0x11</p></td>
<td><p>C, 1</p></td>
<td><p>USB root port 2 power</p></td>
<td><p>Out</p></td>
<td><p>[2.0.0+] Copper<br />
(<a href="USB services.md" title="wikilink">USB services</a>)</p></td>
</tr>
<tr class="even">
<td><p>0x4A</p></td>
<td><p>0x12</p></td>
<td><p>C, 2</p></td>
<td><p>HdmiHotplug</p></td>
<td><p>Out</p></td>
<td><p>[2.0.0+] Copper<br />
(<a href="NV services.md" title="wikilink">NV services</a>)</p></td>
</tr>
<tr class="odd">
<td><p>0x4B</p></td>
<td><p>0x42</p></td>
<td><p>I, 2</p></td>
<td></td>
<td><p>Out</p></td>
<td><p>[2.0.0+] Copper</p></td>
</tr>
<tr class="even">
<td><p>0x4C</p></td>
<td><p>0xE6</p></td>
<td><p>CC, 6</p></td>
<td></td>
<td><p>In</p></td>
<td><p>[2.0.0+] Copper</p></td>
</tr>
<tr class="odd">
<td><p>[2.0.0+] 0x4D</p></td>
<td><p>0xAC</p></td>
<td><p>V, 4</p></td>
<td></td>
<td><p>Out</p></td>
<td><p>[2.0.0+] Copper</p></td>
</tr>
<tr class="even">
<td><p>[2.0.0+] 0x4E</p></td>
<td><p>0xE1</p></td>
<td><p>CC, 1</p></td>
<td><p>HdmiHotplug (HDMI_INT_DP_HPD_PCC1)</p></td>
<td><p>In</p></td>
<td><p>[2.0.0+] Copper<br />
(<a href="NV services.md" title="wikilink">NV services</a>)</p></td>
</tr>
<tr class="odd">
<td><p>[5.0.0+] 0x4F</p></td>
<td><p>0x56</p></td>
<td><p>K, 6</p></td>
<td></td>
<td></td>
<td><p>None</p></td>
</tr>
</tbody>
</table>

## GpioPadDescriptor

| Bits | Description      |
| ---- | ---------------- |
| 7-5  | Controller index |
| 4-3  | Port index       |
| 2-0  | Pin number       |

## OpenSessionForDev

Takes a raw [\#GpioPadDescriptor](#GpioPadDescriptor "wikilink") and
returns a [\#IPadSession](#IPadSession "wikilink") session for it.

## OpenSession

Same thing as [\#OpenSessionForDev](#OpenSessionForDev "wikilink")
except it takes a **GpioPadName** which is then converted to a
[\#GpioPadDescriptor](#GpioPadDescriptor "wikilink"). Returns an
[\#IPadSession](#IPadSession "wikilink") session.

## OpenSessionForTest

Same as [\#OpenSession](#OpenSession "wikilink") but panics on failure.

## OpenSession2

Same as [\#OpenSession](#OpenSession "wikilink") but takes a
**DeviceCode** instead of a **GpioPadName**.

## IPadSession

This is "nn::gpio::IPadSession".

| Cmd | Name                             |
| --- | -------------------------------- |
| 0   | SetDirection                     |
| 1   | GetDirection                     |
| 2   | SetInterruptMode                 |
| 3   | GetInterruptMode                 |
| 4   | SetInterruptEnable               |
| 5   | GetInterruptEnable               |
| 6   | GetInterruptStatus               |
| 7   | ClearInterruptStatus             |
| 8   | SetValue                         |
| 9   | GetValue                         |
| 10  | BindInterrupt                    |
| 11  | UnbindInterrupt                  |
| 12  | SetDebounceEnabled               |
| 13  | GetDebounceEnabled               |
| 14  | SetDebounceTime                  |
| 15  | GetDebounceTime                  |
| 16  | \[4.0.0+\] SetValueForSleepState |

# i2c, i2c:pcv

This is "nn::i2c::IManager".

| Cmd | Name              |
| --- | ----------------- |
| 0   | OpenSessionForDev |
| 1   | OpenSession       |
| 2   | HasDevice         |
| 3   | HasDeviceForDev   |

## Known Devices

| Name | Port:Addr | 10bit? | Speed  | Max Retries | Retry Delay | Usage                                 | Used by                                                                                            |
| ---- | --------- | ------ | ------ | ----------- | ----------- | ------------------------------------- | -------------------------------------------------------------------------------------------------- |
| 0    | 0:52      | N      | 100000 | 0           | 0           | DebugPadDriver                        | [HID services](HID%20services.md "wikilink")                                                       |
| 1    | 2:49      | N      | 400000 | 0           | 0           | STM touchscreen                       | [HID services](HID%20services.md "wikilink")                                                       |
| 2    | 0:4c      | N      | 100000 | 0           | 0           | TI Temperature Sensor (tmp451)        | [PTM services](PTM%20services.md "wikilink")                                                       |
| 3    | 0:4c      | N      | 100000 | 0           | 0           | duplicate, unused entry?              |                                                                                                    |
| 4    | 0:1c      | N      | 100000 | 0           | 0           | Audio codec (rt5639)                  | [Audio services](Audio%20services.md "wikilink"), [Fatal services](Fatal%20services.md "wikilink") |
| 5    | 4:68      | N      | 400000 | 3           | 5000000     | max77620\_rtc0, max77620\_irq0        | [PCV services](PCV%20services.md "wikilink")                                                       |
| 6    | 4:3c      | N      | 400000 | 3           | 5000000     | PMIC (max77620), max77620\_irq0       | [PCV services](PCV%20services.md "wikilink")                                                       |
| 7    | 4:1b      | N      | 400000 | 3           | 5000000     | max77621\_cpu                         | [PCV services](PCV%20services.md "wikilink")                                                       |
| 8    | 4:1c      | N      | 400000 | 3           | 5000000     | max77621\_gpu                         | [PCV services](PCV%20services.md "wikilink")                                                       |
| 9    | 0:6b      | N      | 100000 | 3           | 5000000     | TI Charger (bq24192)                  | [PTM services](PTM%20services.md "wikilink")                                                       |
| 10   | 0:36      | N      | 100000 | 3           | 5000000     | Maxim Fuel Gauge (max17050)           | [PCV services](PCV%20services.md "wikilink"), [PTM services](PTM%20services.md "wikilink")         |
| 11   | 0:18      | N      | 100000 | 3           | 5000000     | USB-PD controller (rohm bm92t36)      | [USB services](USB%20services.md "wikilink")                                                       |
| 12   | 1:40      | N      | 400000 | 3           | 5000000     |                                       |                                                                                                    |
| 13   | 1:41      | N      | 400000 | 3           | 5000000     |                                       |                                                                                                    |
| 14   | 1:44      | N      | 400000 | 3           | 5000000     |                                       |                                                                                                    |
| 15   | 1:45      | N      | 400000 | 3           | 5000000     |                                       |                                                                                                    |
| 16   | 1:46      | N      | 400000 | 3           | 5000000     |                                       |                                                                                                    |
| 17   | 1:47      | N      | 400000 | 3           | 5000000     |                                       |                                                                                                    |
| 18   | 1:29      | N      | 400000 | 3           | 5000000     | rohm ambient light sensor (bh1730fvc) | [Backlight services](Backlight%20services.md "wikilink")                                           |
| 19   | 1:48      | N      | 400000 | 3           | 5000000     |                                       |                                                                                                    |
| 20   | 1:49      | N      | 400000 | 3           | 5000000     |                                       |                                                                                                    |
| 21   | 1:4a      | N      | 400000 | 3           | 5000000     |                                       |                                                                                                    |
| 22   | 1:4b      | N      | 400000 | 3           | 5000000     |                                       |                                                                                                    |
| 23   | 1:4d      | N      | 400000 | 3           | 5000000     |                                       |                                                                                                    |
| 24   | 3:50      | N      | 100000 | 0           | 0           | DisplayHdmiHotplugHandler             | [NV services](NV%20services.md "wikilink")                                                         |
| 25   | 3:54      | N      | 100000 | 0           | 0           | DisplayHdmiHotplugHandler             | [NV services](NV%20services.md "wikilink")                                                         |
| 26   | 3:3a      | N      | 100000 | 0           | 0           | DisplayHdmiHotplugHandler             | [NV services](NV%20services.md "wikilink")                                                         |

This table is believed to be complete - entries with empty "Used by"
column haven't been seen being used (devices not present on switch?).

## II2cSession

This is "nn::i2c::ISession".

| Cmd | Name                   |
| --- | ---------------------- |
| 0   | Send                   |
| 1   | Receive                |
| 2   | ExecuteCommandList     |
| 10  | SendAuto               |
| 11  | ReceiveAuto            |
| 12  | ExecuteCommandListAuto |

# uart

This is "nn::uart::IManager".

| Cmd | Name                         |
| --- | ---------------------------- |
| 0   | DoesUartExist                |
| 1   | DoesUartExistForTest         |
| 2   | SetUartBaudrate              |
| 3   | SetUartBaudrateForTest       |
| 4   | IsSomethingUartValid         |
| 5   | IsSomethingUartValidForTest  |
| 6   | GetSession                   |
| 7   | IsSomethingUartValid2        |
| 8   | IsSomethingUartValid2ForTest |

## IPortSession

This is "nn::uart::IPortSession".

| Cmd | Name               |
| --- | ------------------ |
| 0   | OpenSession        |
| 1   | OpenSessionForTest |
| 2   |                    |
| 3   |                    |
| 4   |                    |
| 5   |                    |
| 6   |                    |
| 7   |                    |
|     |                    |

### Port Mapping

OpenSession translates user IDs to to the uart port index.

OpenSessionForTest takes the port index verbatim.

| Name | Port   | Usage     |
| ---- | ------ | --------- |
| 1    | UART-D | Bluetooth |
| 2    | UART-B | Joycon(R) |
| 3    | UART-C | Joycon(L) |
|      |        |           |

# pwm

This is "nn::pwm::IManager".

| Cmd | Name              |
| --- | ----------------- |
| 0   | OpenSessionForDev |
| 1   | OpenSession       |

## Known Channels

| Name | Interface     | Usage     | Used by                                                                                              |
| ---- | ------------- | --------- | ---------------------------------------------------------------------------------------------------- |
| 1    | PWM Channel 1 | Fan       | [PTM services](PTM%20services.md "wikilink")                                                         |
| 2    | PWM Channel 0 | Backlight | [Backlight services](Backlight%20services.md "wikilink"), [NV services](NV%20services.md "wikilink") |
| 3    | PMC Blinker   |           |                                                                                                      |

## IChannelSession

This is "nn::pwm::IChannelSession".

| Cmd | Name       |
| --- | ---------- |
| 0   | SetPeriod  |
| 1   | GetPeriod  |
| 2   | SetDuty    |
| 3   | GetDuty    |
| 4   | SetEnabled |
| 5   | GetEnabled |

# pinmux

This is "nn::pinmux::IManager".

| Cmd | Name        |
| --- | ----------- |
| 0   | OpenSession |

## ISession

This is "nn::pinmux::ISession".

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |

# sasbus

This is "nn::sasbus::IManager".

| Cmd | Name        |
| --- | ----------- |
| 0   | OpenSession |

## ISession

This is "nn::sasbus::ISession".

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |
| 3   |      |

[Category:Services](Category:Services "wikilink")

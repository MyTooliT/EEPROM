# EEPROM-STH

This file contains the momentary used values of the EEPROM from the STH.

## Used Pages

| Page Number | Page Name                                            |
| ----------- | ---------------------------------------------------- |
| `0x0`       | [System Configuration 0](#page:system-configuration) |
| `0x4`       | Product Data                                         |
| `0x5`       | Statistic                                            |
| `0x8`       | Calibration 0                                        |

<a name="page:system-configuration"></a>

### Page `System Configuration 0`

| Name                 | Address | Length | Read Only | Value     | Unit | Format   | Description                                                  |
| -------------------- | ------- | ------ | --------- | --------- | ---- | -------- | ------------------------------------------------------------ |
| EEPROM Status        | 0       | 1      | True      | [0xac]    |      |          | Determines Initialised EERPOM iff 0xAC or locked EEPROM iff 0xCA |
| Radio Name           | 1       | 8      | False     | BBCB4878  |      | UTF8     | Defines Bluetooth advertisement name                         |
| Sleep Time 1         | 9       | 4      | False     | 300000    | ms   | unsigned | Time to from disconnect/power on to Sleep Mode 1 in ms       |
| Advertisement Time 1 | 13      | 2      | False     | 2000      | ms   | unsigned | Bluetooth Advertisement Time in ms for Sleep Mode 1          |
| Sleep time 2         | 15      | 4      | False     | 259200000 | ms   | unsinged | Time to from entering Sleep Mode 1 to Sleep Mode 2 in ms     |
| Advertisement Time 2 | 19      | 2      | False     | 4000      | ms   | unsinged | Bluetooth Advertisement Time in ms for Sleep Mode 2          |
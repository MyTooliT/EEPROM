# EEPROM-STH

This file contains the momentary used values of the EEPROM from the STH.

## Used Pages

| Page Number | Page Name                                            |
| ----------- | ---------------------------------------------------- |
| `0x0`       | [System Configuration 0](#page:system-configuration) |
| `0x4`       | [Product Data](#page:product-data)                   |
| `0x5`       | [Statistic](#page:statistic)                         |
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

<a name="page:product-data"></a>

### Page `Product Data`

| Name                               | Address | Length | Read Only | Value | Format   | Description                                                  |
| ---------------------------------- | ------- | ------ | --------- | ----- | -------- | ------------------------------------------------------------ |
| GTIN                               | 0       | 8      | True      | 0     | unsigned | Global Trade Identification Number (GTIN)                    |
| Hardware Revision - Reserved       | 8       | 5      | True      | 0     | unsigned | Hardware Revision Number - Reserved                          |
| Hardware Revision - Major          | 13      | 1      | False     | 1     | unsigned | Hardware Revision Number - Major                             |
| Hardware Revision - Minor          | 14      | 1      | False     | 3     | unsigned | Hardware Revision Number - Minor                             |
| Hardware Revision - Build          | 15      | 1      | False     | 4     | unsigned | Hardware Revision Number - Build                             |
| Firmware Version Number - Reserved | 16      | 5      | True      | 0     | unsigned | Firmware Version Number - Reserved                           |
| Firmware Version Number - Major    | 21      | 1      | False     | 2     | unsigned | Firmware Version Number - Major                              |
| Firmware Version Number - Minor    | 22      | 1      | False     | 1     | unsigned | Firmware Version Number - Minor                              |
| Firmware Version Number - Build    | 23      | 1      | False     | 9     | unsigned | Firmware Version Number - Build                              |
| Release Name                       | 24      | 8      | False     | Tanja | UTF8     | Release Name, represents Major - Minor                       |
| Serial Number                      | 32      | 32     | True      | 0     | UTF8     | Manufacture Serial Number (Derived from ISBN); Product Group - Subgroup - Manufacture ID - Product Number - Check Digit |
| Name                               | 64      | 128    | True      | 0     | UTF8     | Manufacture Name; This may extend Serial Number, supports URL, extend definition, etc. |
| OEM Free Use                       | 192     | 64     | True      | 0     | -        | Supports Manufacture Specific information in format that is free to choose |

<a name="page:statistic"></a>

### Page `Statistic`

| Name                                       | Address | Length | Read Only | Value    | Unit    | Format   | Description                                                  |
| ------------------------------------------ | ------- | ------ | --------- | -------- | ------- | -------- | ------------------------------------------------------------ |
| Power ON Cycles                            | 0       | 4      | True      | 0        | -       | unsigned | Power On Cycles since first reset(Note that a resets also counts as power on) |
| Power OFF Cycles                           | 4       | 4      | True      | 0        | -       | unsigned | Power Off Cycles since first reset                           |
| Operating Time since first power On        | 8       | 4      | True      | 0        | seconds | unsigned | Operating Time since first power On in seconds               |
| Under Voltage Counter since first power On | 12      | 4      | True      | 0        | -       | unsigned | Counts of under voltages that yields into turn off state(Brown Out) |
| Watchdog Reset Counter                     | 16      | 4      | True      | 0        | -       | unsigned | Watchdog Resets since first power on                         |
| Production Date                            | 20      | 8      | False     | 20191216 | date    | ASCII    | Production Date (EEPROM Production Write) in the format yyyymmdd (year month day) |
| Batch Number                               | 28      | 4      | True      | 112      | -       | unsigned | Consecutive number for manufactured devices                  |
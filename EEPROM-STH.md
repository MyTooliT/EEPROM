# EEPROM-STH

This file contains the momentary used values of the EEPROM from the STH.

## Used Pages

| Page Number | Page Name                                          |
| ----------- | -------------------------------------------------- |
| `0x0`       | [System Configuration](#page:system-configuration) |
| `0x4`       | [Product Data](#page:product-data)                 |
| `0x5`       | [Statistic](#page:statistic)                       |
| `0x8`       | [Calibration](#page:calibration)                   |

<a name="page:system-configuration"></a>

### Page `System Configuration`

| Name                 | Address | Length | Read Only | Value     | Unit | Format   | Description                                                      |
| -------------------- | ------- | ------ | --------- | --------- | ---- | -------- | ---------------------------------------------------------------- |
| EEPROM Status        | 0       | 1      | True      | [0xac]    |      |          | Determines Initialised EERPOM iff 0xAC or locked EEPROM iff 0xCA |
| Radio Name           | 1       | 8      | False     | BBCB4878  |      | UTF8     | Defines Bluetooth advertisement name                             |
| Sleep Time 1         | 9       | 4      | False     | 300000    | ms   | unsigned | Time to from disconnect/power on to Sleep Mode 1 in ms           |
| Advertisement Time 1 | 13      | 2      | False     | 2000      | ms   | unsigned | Bluetooth Advertisement Time in ms for Sleep Mode 1              |
| Sleep time 2         | 15      | 4      | False     | 259200000 | ms   | unsigned | Time to from entering Sleep Mode 1 to Sleep Mode 2 in ms         |
| Advertisement Time 2 | 19      | 2      | False     | 4000      | ms   | unsigned | Bluetooth Advertisement Time in ms for Sleep Mode 2              |

<a name="page:product-data"></a>

### Page `Product Data`

| Name                               | Address | Length | Read Only | Value | Format   | Description                                                                                                             |
| ---------------------------------- | ------- | ------ | --------- | ----- | -------- | ----------------------------------------------------------------------------------------------------------------------- |
| GTIN                               | 0       | 8      | True      | 0     | unsigned | Global Trade Identification Number (GTIN)                                                                               |
| Hardware Revision - Reserved       | 8       | 5      | True      | 0     | unsigned | Hardware Revision Number - Reserved                                                                                     |
| Hardware Revision - Major          | 13      | 1      | False     | 1     | unsigned | Hardware Revision Number - Major                                                                                        |
| Hardware Revision - Minor          | 14      | 1      | False     | 3     | unsigned | Hardware Revision Number - Minor                                                                                        |
| Hardware Revision - Build          | 15      | 1      | False     | 4     | unsigned | Hardware Revision Number - Build                                                                                        |
| Firmware Version Number - Reserved | 16      | 5      | True      | 0     | unsigned | Firmware Version Number - Reserved                                                                                      |
| Firmware Version Number - Major    | 21      | 1      | False     | 2     | unsigned | Firmware Version Number - Major                                                                                         |
| Firmware Version Number - Minor    | 22      | 1      | False     | 1     | unsigned | Firmware Version Number - Minor                                                                                         |
| Firmware Version Number - Build    | 23      | 1      | False     | 9     | unsigned | Firmware Version Number - Build                                                                                         |
| Release Name                       | 24      | 8      | False     | Tanja | UTF8     | Release Name, represents Major - Minor                                                                                  |
| Serial Number                      | 32      | 32     | True      | 0     | UTF8     | Manufacture Serial Number (Derived from ISBN); Product Group - Subgroup - Manufacture ID - Product Number - Check Digit |
| Name                               | 64      | 128    | True      | 0     | UTF8     | Manufacture Name; This may extend Serial Number, supports URL, extend definition, etc.                                  |
| OEM Free Use                       | 192     | 64     | True      | 0     | -        | Supports Manufacture Specific information in format that is free to choose                                              |

<a name="page:statistic"></a>

### Page `Statistic`

| Name                                       | Address | Length | Read Only | Value    | Unit    | Format   | Description                                                                       |
| ------------------------------------------ | ------- | ------ | --------- | -------- | ------- | -------- | --------------------------------------------------------------------------------- |
| Power ON Cycles                            | 0       | 4      | True      | 0        | -       | unsigned | Power On Cycles since first reset(Note that a resets also counts as power on)     |
| Power OFF Cycles                           | 4       | 4      | True      | 0        | -       | unsigned | Power Off Cycles since first reset                                                |
| Operating Time since first power On        | 8       | 4      | True      | 0        | seconds | unsigned | Operating Time since first power On in seconds                                    |
| Under Voltage Counter since first power On | 12      | 4      | True      | 0        | -       | unsigned | Counts of under voltages that yields into turn off state(Brown Out)               |
| Watchdog Reset Counter                     | 16      | 4      | True      | 0        | -       | unsigned | Watchdog Resets since first power on                                              |
| Production Date                            | 20      | 8      | False     | 20191216 | date    | ASCII    | Production Date (EEPROM Production Write) in the format yyyymmdd (year month day) |
| Batch Number                               | 28      | 4      | True      | 112      | -       | unsigned | Consecutive number for manufactured devices                                       |

<a name="page:calibration"></a>

### Page `Calibration`

| Name                     | Address | Length | Read Only | Value                  | Format | Description                                             |
| ------------------------ | ------- | ------ | --------- | ---------------------- | ------ | ------------------------------------------------------- |
| Acceleration X - K       | 0       | 4      | False     | 0.0030518043786287308  | float  | Calibration Factor K for Acceleration X -> y=kx+d       |
| Acceleration X - D       | 4       | 4      | False     | -99.33318328857422     | float  | Calibration Factor d for Acceleration X -> y=kx+d       |
| Acceleration Y - K       | 8       | 4      | False     | 1.0                    | float  | Calibration Factor K for Acceleration Y -> y=kx+d       |
| Acceleration Y - D       | 12      | 4      | False     | 0.0                    | float  | Calibration Factor d for Acceleration Y -> y=kx+d       |
| Acceleration Z - K       | 16      | 4      | False     | 1.0                    | float  | Calibration Factor K for Acceleration Z -> y=kx+d       |
| Acceleration Z - D       | 20      | 4      | False     | 0.0                    | float  | Calibration Factor d for Acceleration Z -> y=kx+d       |
| Voltage Battery - K      | 24      | 4      | False     | 0.00028701781411655247 | float  | Calibration Factor K for Battery Voltage -> y=kx+d      |
| Voltage Battery - D      | 28      | 4      | False     | -0.09040877968072891   | float  | Calibration Factor d for Battery Voltage -> y=kx+d      |
| Voltage Y - K            | 32      | 4      | False     | 1.0                    | float  | Calibration Factor K for Voltage Y -> y=kx+d            |
| Voltage Y - D            | 36      | 4      | False     | 0.0                    | float  | Calibration Factor d for Voltage Y -> y=kx+d            |
| Voltage Z - K            | 40      | 4      | False     | 1.0                    | float  | Calibration Factor K for Voltage Z -> y=kx+d            |
| Voltage Z - D            | 44      | 4      | False     | 0.0                    | float  | Calibration Factor d for Voltage Z -> y=kx+d            |
| Internal Temperature - K | 48      | 4      | False     | 1.0                    | float  | Calibration Factor K for Internal Temperature -> y=kx+d |
| Internal Temperature - D | 52      | 4      | False     | 0.0                    | float  | Calibration Factor d for Internal Temperature -> y=kx+d |
| Temperature Y - K        | 56      | 4      | False     | 1.0                    | float  | Calibration Factor K for Temperature Y -> y=kx+d        |
| Temperature Y - D        | 60      | 4      | False     | 0.0                    | float  | Calibration Factor d for Temperature Y -> y=kx+d        |
| Temperature Z - K        | 66      | 4      | False     | 1.0                    | float  | Calibration Factor K for Temperature Z -> y=kx+d        |
| Temperature Z - D        | 70      | 4      | False     | 0.0                    | float  | Calibration Factor d for Temperature Z -> y=kx+d        |

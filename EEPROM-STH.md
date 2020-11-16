# EEPROM-STH

This file contains the default values of the STH EEPROM. For a more detailed description of the values, please take a look at the [description of the EEPROM layout](EEPROM.md).

## Used Pages

| Page Number | Page Name                                          |
| ----------- | -------------------------------------------------- |
| `0x0`       | [System Configuration](#page:system-configuration) |
| `0x4`       | [Product Data](#page:product-data)                 |
| `0x5`       | [Statistic](#page:statistic)                       |
| `0x8`       | [Calibration](#page:calibration)                   |

<a name="page:system-configuration"></a>

### Page `System Configuration`

| Name                 | Address | Length | Read Only | Value                                                                                                               | Comment                               | Unit | Format   |
| -------------------- | ------- | ------ | --------- | ------------------------------------------------------------------------------------------------------------------- | ------------------------------------- | ---- | -------- |
| EEPROM Status        | 0       | 1      | True      | `0xac`                                                                                                              | Value for initialized EEPROM          | -    |          |
| STH Name             | 1       | 8      | False     | [Base64 encoded Bluetooth MAC address](https://github.com/MyTooliT/ICOc/tree/master/Scripts#mac-address-conversion) | e.g. `CGvXAd6B` (`08:6b:d7:01:de:81`) | -    | UTF-8    |
| Sleep Time 1         | 9       | 4      | False     | 300000                                                                                                              | 5 minutes                             | ms   | Unsigned |
| Advertisement Time 1 | 13      | 2      | False     | 2000                                                                                                                | 2 seconds                             | ms   | Unsigned |
| Sleep Time 2         | 15      | 4      | False     | 259200000                                                                                                           | 3 days                                | ms   | Unsigned |
| Advertisement Time 2 | 19      | 2      | False     | 4000                                                                                                                | 4 seconds                             | ms   | Unsigned |

<a name="page:product-data"></a>

### Page `Product Data`

| Name                     | Address | Length | Read Only | Value | Format   | Comment                                              |
| ------------------------ | ------- | ------ | --------- | ----- | -------- | ---------------------------------------------------- |
| GTIN                     | 0       | 8      | True      | 0     | Unsigned |                                                      |
| Hardware Revision: Major | 13      | 1      | False     | -     | Unsigned | [Major Hardware Revision](#hardware-revision)        |
| Hardware Revision: Minor | 14      | 1      | False     | -     | Unsigned | [Minor Hardware Revision Number](#hardware-revision) |
| Hardware Revision: Build | 15      | 1      | False     | -     | Unsigned | [Build Hardware Revision Number](#hardware-revision) |
| Firmware Version: Major  | 21      | 1      | False     | -     | Unsigned | [Major Firmware Version Number](#software-version)   |
| Firmware Version: Minor  | 22      | 1      | False     | -     | Unsigned | [Minor Firmware Version Number](#software-version)   |
| Firmware Version: Build  | 23      | 1      | False     | -     | Unsigned | [Build Firmware Version Number](#software-version)   |
| Release Name             | 24      | 8      | False     | Tanja | UTF-8    |                                                      |
| Serial Number            | 32      | 32     | True      | 0     | UTF-8    |                                                      |
| Name                     | 64      | 128    | True      | 0     | UTF-8    |                                                      |
| OEM Free Use             | 192     | 64     | True      | 0     | -        |                                                      |

#### Version Numbers

- <a name="hardware-revision"></a> **Hardware Revision**: This number depends on the hardware revision (printed on the PCB). The value itself can be changed in the [main configuration file of ICOc](https://github.com/MyTooliT/ICOc/blob/master/Configuration/config.yaml)
- <a name="firmware-version"></a> **Firmware Version**: This number depends on the current [STH software version](https://github.com/MyTooliT/STH/releases)

<a name="page:statistic"></a>

### Page `Statistic`

| Name                                       | Address | Length | Read Only | Value    | Unit    | Format   | Comment                                                                           |
| ------------------------------------------ | ------- | ------ | --------- | -------- | ------- | -------- | --------------------------------------------------------------------------------- |
| Power ON Cycles                            | 0       | 4      | True      | 0        | -       | Unsigned |                                                                                   |
| Power OFF Cycles                           | 4       | 4      | True      | 0        | -       | Unsigned | Power Off Cycles since first reset                                                |
| Operating Time since first power On        | 8       | 4      | True      | 0        | seconds | Unsigned | Operating Time since first power On in seconds                                    |
| Under Voltage Counter since first power On | 12      | 4      | True      | 0        | -       | Unsigned | Counts of under voltages that yields into turn off state(Brown Out)               |
| Watchdog Reset Counter                     | 16      | 4      | True      | 0        | -       | Unsigned | Watchdog Resets since first power on                                              |
| Production Date                            | 20      | 8      | False     | 20191216 | date    | ASCII    | Production Date (EEPROM Production Write) in the format yyyymmdd (year month day) |
| Batch Number                               | 28      | 4      | True      | 112      | -       | Unsigned | Consecutive number for manufactured devices                                       |

<a name="page:calibration"></a>

### Page `Calibration`

| Name                     | Address | Length | Read Only | Value                  | Format | Comment                                                 |
| ------------------------ | ------- | ------ | --------- | ---------------------- | ------ | ------------------------------------------------------- |
| Acceleration X - K       | 0       | 4      | False     | 0.0030518043786287308  | Float  | Calibration Factor K for Acceleration X -> y=kx+d       |
| Acceleration X - D       | 4       | 4      | False     | -99.33318328857422     | Float  | Calibration Factor d for Acceleration X -> y=kx+d       |
| Acceleration Y - K       | 8       | 4      | False     | 1.0                    | Float  | Calibration Factor K for Acceleration Y -> y=kx+d       |
| Acceleration Y - D       | 12      | 4      | False     | 0.0                    | Float  | Calibration Factor d for Acceleration Y -> y=kx+d       |
| Acceleration Z - K       | 16      | 4      | False     | 1.0                    | Float  | Calibration Factor K for Acceleration Z -> y=kx+d       |
| Acceleration Z - D       | 20      | 4      | False     | 0.0                    | Float  | Calibration Factor d for Acceleration Z -> y=kx+d       |
| Voltage Battery - K      | 24      | 4      | False     | 0.00028701781411655247 | Float  | Calibration Factor K for Battery Voltage -> y=kx+d      |
| Voltage Battery - D      | 28      | 4      | False     | -0.09040877968072891   | Float  | Calibration Factor d for Battery Voltage -> y=kx+d      |
| Voltage Y - K            | 32      | 4      | False     | 1.0                    | Float  | Calibration Factor K for Voltage Y -> y=kx+d            |
| Voltage Y - D            | 36      | 4      | False     | 0.0                    | Float  | Calibration Factor d for Voltage Y -> y=kx+d            |
| Voltage Z - K            | 40      | 4      | False     | 1.0                    | Float  | Calibration Factor K for Voltage Z -> y=kx+d            |
| Voltage Z - D            | 44      | 4      | False     | 0.0                    | Float  | Calibration Factor d for Voltage Z -> y=kx+d            |
| Internal Temperature - K | 48      | 4      | False     | 1.0                    | Float  | Calibration Factor K for Internal Temperature -> y=kx+d |
| Internal Temperature - D | 52      | 4      | False     | 0.0                    | Float  | Calibration Factor d for Internal Temperature -> y=kx+d |
| Temperature Y - K        | 56      | 4      | False     | 1.0                    | Float  | Calibration Factor K for Temperature Y -> y=kx+d        |
| Temperature Y - D        | 60      | 4      | False     | 0.0                    | Float  | Calibration Factor d for Temperature Y -> y=kx+d        |
| Temperature Z - K        | 66      | 4      | False     | 1.0                    | Float  | Calibration Factor K for Temperature Z -> y=kx+d        |
| Temperature Z - D        | 70      | 4      | False     | 0.0                    | Float  | Calibration Factor d for Temperature Z -> y=kx+d        |

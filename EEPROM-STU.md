# EEPROM-STU

This file contains the default values for the STU EEPROM. For a more detailed description of the values, please take a look at the [description of the EEPROM layout](EEPROM.md).

## Used Pages

| Page Number | Page Name                          |
| ----------- | ---------------------------------- |
| `0x4`       | [Product Data](#page:product-data) |
| `0x5`       | [Statistic](#page:statistic)       |

<a name="page:product-data"></a>

### Page `Product Data`

| Name                                               | Address | Length | Read Only | Value                                            | Format   |
| -------------------------------------------------- | ------- | ------ | --------- | ------------------------------------------------ | -------- |
| GTIN                                               | 0       | 8      | True      | 0                                                | Unsigned |
| Hardware Revision: Reserved                        | 8       | 5      | True      | 0                                                | Unsigned |
| Hardware Revision: Major                           | 13      | 1      | True      | 1                                                | Unsigned |
| Hardware Revision: Minor                           | 14      | 1      | True      | 3                                                | Unsigned |
| Hardware Revision: Patch                           | 15      | 1      | True      | 1                                                | Unsigned |
| Firmware Version: Reserved                         | 16      | 5      | True      | 0                                                | Unsigned |
| [Firmware Version: Major](#value:firmware-version) | 21      | 1      | True      | -                                                | Unsigned |
| [Firmware Version: Minor](#value:firmware-version) | 22      | 1      | True      | -                                                | Unsigned |
| [Firmware Version: Patch](#value:firmware-version) | 23      | 1      | True      | -                                                | Unsigned |
| Release Name                                       | 24      | 8      | True      | Valerie                                          | UTF-8    |
| Serial Number                                      | 32      | 32     | True      | MyToolItStu001-1-00001-001-2                     | UTF-8    |
| Product Name                                       | 64      | 128    | True      | Digital and Analog Communication with 5V -Supply | UTF-8    |
| OEM Free Use                                       | 192     | 64     | True      | 0                                                | -        |

#### Version Numbers

- <a name="value:firmware-version"></a> **Firmware Version**: This number depends on the current [STH software version](https://github.com/MyTooliT/STU/releases)

<a name="page:statistic"></a>

### Page `Statistic`

| Name                   | Address | Length | Read Only | Value | Unit | Format   |
| ---------------------- | ------- | ------ | --------- | ----- | ---- | -------- |
| Power On Cycles        | 0       | 4      | True      | 0     | -    | Unsigned |
| Power Off Cycles       | 4       | 4      | True      | 0     | -    | Unsigned |
| Operating Time         | 8       | 4      | True      | 0     | s    | Unsigned |
| Under Voltage Counter  | 12      | 4      | True      | 0     | -    | Unsigned |
| Watchdog Reset Counter | 16      | 4      | True      | 0     | -    | Unsigned |
| Production Date: Year  | 20      | 4      | True      | -     |      | ASCII    |
| Production Date: Month | 24      | 2      | True      | -     |      | ASCII    |
| Production Date: Day   | 26      | 2      | True      | -     |      | ASCII    |
| Batch Number           | 28      | 4      | True      | 2     | -    | Unsigned |

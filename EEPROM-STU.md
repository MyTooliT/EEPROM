# EEPROM-STU

This file contains the default values for the STU EEPROM. For a more detailed description of the values, please take a look at the [description of the EEPROM layout](EEPROM.md).

## Used Pages

| Page Number | Page Name                                              |
| ----------: | ------------------------------------------------------ |
|       `0x0` | [System Configuration](#page:stu-system-configuration) |
|       `0x4` | [Product Data](#page:stu-product-data)                 |
|       `0x5` | [Statistics](#page:stu-statistics)                     |

### Page `System Configuration`

| Name          | Address | Length | Read Only | Value                 | Comment                      | Unit | Format |
| ------------- | ------: | -----: | --------- | --------------------- | ---------------------------- | ---- | ------ |
| EEPROM Status |       0 |      1 | True      | `0xac`                | Value for initialized EEPROM | -    |        |
| STU Name      |       1 |      8 | False     | Firmware version name | e.g. `Valerie`               | -    | UTF-8  |

#### Initialization

All of the values of the system configuration are set to the default values above on reset of the STU, if the EEPROM status (byte) is **not** set to `Initialized` (`0xac`) or `Locked` (`0xca`). The values for the sleep times and advertisement times are set (to the same values the STH uses) on initialization too. However, since the STU is not battery-powered these timing values are probably not relevant.

<a name="page:stu-product-data"></a>

### Page `Product Data`

| Name                                                     | Address | Length | Read Only | Value   | Format   |
| -------------------------------------------------------- | ------: | -----: | --------- | ------- | -------- |
| GTIN                                                     |       0 |      8 | True      | 0       | Unsigned |
| [Hardware Revision: Major](#value:stu-hardware-revision) |      13 |      1 | True      | -       | Unsigned |
| [Hardware Revision: Minor](#value:stu-hardware-revision) |      14 |      1 | True      | -       | Unsigned |
| [Hardware Revision: Patch](#value:stu-hardware-revision) |      15 |      1 | True      | -       | Unsigned |
| [Firmware Version: Major](#value:stu-firmware-version)   |      21 |      1 | True      | -       | Unsigned |
| [Firmware Version: Minor](#value:stu-firmware-version)   |      22 |      1 | True      | -       | Unsigned |
| [Firmware Version: Patch](#value:stu-firmware-version)   |      23 |      1 | True      | -       | Unsigned |
| [Release Name](#value:stu-release-name)                  |      24 |      8 | True      | Valerie | UTF-8    |
| [Serial Number](#value:stu-serial-number)                |      32 |     32 | True      | 0       | UTF-8    |
| [Product Name](#value:stu-product-name)                  |      64 |    128 | True      | 0       | UTF-8    |
| [OEM Free Use](#value:stu-oem-free-use)                  |     192 |     64 | True      | 0       | -        |

#### Version Numbers

- <a name="value:stu-hardware-revision"></a> **Hardware Revision**: This number depends on the hardware revision (printed on the PCB). The value itself can be changed in the [main configuration file of ICOc][config]
- <a name="value:stu-firmware-version"></a> **Firmware Version**: This number depends on the current [STU software version](https://github.com/MyTooliT/STU/releases)
- <a name="value:stu-release-name"></a> **Release Name**: This text can be changed in the [configuration of ICOc][config]
- <a name="value:stu-serial-number"></a> **Serial Number**: This text can be changed in the [configuration of ICOc][config]
- <a name="value:stu-product-name"></a> **Product Name**: This text can be changed in the [configuration of ICOc][config]
- <a name="value:stu-oem-free-use"></a> **OEM Free Use**: This value can be changed in the [configuration of ICOc][config].

[config]: https://github.com/MyTooliT/ICOc/blob/master/Configuration/config.yaml

<a name="page:stu-statistics"></a>

### Page `Statistics`

| Name                                                 | Address | Length | Read Only | Value | Unit | Format   |
| ---------------------------------------------------- | ------: | -----: | --------- | ----: | ---- | -------- |
| Power On Cycles                                      |       0 |      4 | True      |     0 | -    | Unsigned |
| Power Off Cycles                                     |       4 |      4 | True      |     0 | -    | Unsigned |
| Operating Time                                       |       8 |      4 | True      |     0 | s    | Unsigned |
| Under Voltage Counter                                |      12 |      4 | True      |     0 | -    | Unsigned |
| Watchdog Reset Counter                               |      16 |      4 | True      |     0 | -    | Unsigned |
| [Production Date: Year](#value:stu-production-date)  |      20 |      4 | True      |     - | -    | ASCII    |
| [Production Date: Month](#value:stu-production-date) |      24 |      2 | True      |     - | -    | ASCII    |
| [Production Date: Day](#value:stu-production-date)   |      26 |      2 | True      |     - | -    | ASCII    |
| [Batch Number](#value:stu-batch-number)              |      28 |      4 | True      |     - | -    | Unsigned |

- <a name="value:stu-production-date">**Production Date**:</a> This date depends on the production date of the STU. It can be changed in the [configuration of ICOc][config].
- <a name="value:stu-batch-number">**Batch Number**:</a> This value can be changed in the [configuration of ICOc][config].

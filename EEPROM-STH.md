# STH EEPROM

This file contains the default values of the STH EEPROM. For a more detailed description of the values, please take a look at the [description of the EEPROM layout](EEPROM.md).

## Used Pages

| Page Number | Page Name                                              |
| ----------: | ------------------------------------------------------ |
|       `0x0` | [System Configuration](#page:sth-system-configuration) |
|       `0x4` | [Product Data](#page:sth-product-data)                 |
|       `0x5` | [Statistics](#page:sth-statistics)                     |
|       `0x8` | [Calibration](#page:sth-calibration)                   |

<a name="page:sth-system-configuration"></a>

### Page `System Configuration`

| Name                 | Address | Length | Read Only | Value                                                                                                                                | Comment                      | Unit | Format   |
| -------------------- | ------: | -----: | --------- | ------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------- | ---- | -------- |
| EEPROM Status        |       0 |      1 | True      | `0xac`                                                                                                                               | Value for initialized EEPROM | -    |          |
| STH Name             |       1 |      8 | False     | [Base64 encoded Bluetooth MAC address](https://github.com/MyTooliT/ICOc/tree/master/Scripts#mac-address-conversion) or firmware name | e.g. `CGvXAd6B`, `Tanja`     | -    | UTF-8    |
| Sleep Time 1         |       9 |      4 | False     | 300000                                                                                                                               | 5 minutes                    | ms   | Unsigned |
| Advertisement Time 1 |      13 |      2 | False     | 2000                                                                                                                                 | 2 seconds                    | ms   | Unsigned |
| Sleep Time 2         |      15 |      4 | False     | 259200000                                                                                                                            | 3 days                       | ms   | Unsigned |
| Advertisement Time 2 |      19 |      2 | False     | 4000                                                                                                                                 | 4 seconds                    | ms   | Unsigned |

#### Initialization

All of the values of the system configuration are set to default values on reset of the STH, if the EEPROM status (byte) is **not** set to `Initialized` (`0xac`) or `Locked` (`0xca`). The default values are described above. The name is set to the firmware version name (`Tanja`) and does not use the Base64 encoded Bluetooth MAC address.

<a name="page:sth-product-data"></a>

### Page `Product Data`

| Name                                                     | Address | Length | Read Only | Value | Format   |
| -------------------------------------------------------- | ------: | -----: | --------- | ----- | -------- |
| GTIN                                                     |       0 |      8 | True      | 0     | Unsigned |
| [Hardware Version: Major](#value:sth-hardware-version) |      13 |      1 | False     | -     | Unsigned |
| [Hardware Version: Minor](#value:sth-hardware-version) |      14 |      1 | False     | -     | Unsigned |
| [Hardware Version: Patch](#value:sth-hardware-version) |      15 |      1 | False     | -     | Unsigned |
| [Firmware Version: Major](#value:sth-firmware-version)   |      21 |      1 | False     | -     | Unsigned |
| [Firmware Version: Minor](#value:sth-firmware-version)   |      22 |      1 | False     | -     | Unsigned |
| [Firmware Version: Patch](#value:sth-firmware-version)   |      23 |      1 | False     | -     | Unsigned |
| [Release Name](#value:sth-release-name)                  |      24 |      8 | False     | Tanja | UTF-8    |
| [Serial Number](#value:sth-serial-number)                |      32 |     32 | True      | 0     | UTF-8    |
| [Product Name](#value:sth-product-name)                  |      64 |    128 | True      | 0     | UTF-8    |
| [OEM Free Use](#value:sth-oem-free-use)                  |     192 |     64 | True      | 0     | -        |

#### Version Numbers

- <a name="value:sth-hardware-version"></a> **Hardware Version**: This number depends on the hardware version (printed on the PCB). The value itself can be changed in the [main configuration file of ICOc][config]
- <a name="value:sth-firmware-version"></a> **Firmware Version**: This number depends on the current [STH software version](https://github.com/MyTooliT/STH/releases)
- <a name="value:sth-release-name"></a> **Release Name**: This text can be changed in the [configuration of ICOc][config]
- <a name="value:sth-serial-number"></a> **Serial Number**: This text can be changed in the [configuration of ICOc][config]
- <a name="value:sth-product-name"></a> **Product Name**: This text can be changed in the [configuration of ICOc][config]
- <a name="value:sth-oem-free-use"></a> **OEM Free Use**: This value can be changed in the [configuration of ICOc][config].

[config]: https://github.com/MyTooliT/ICOc/blob/master/Configuration/config.yaml

<a name="page:sth-statistics"></a>

### Page `Statistics`

| Name                                                 | Address | Length | Read Only | Value | Unit | Format   |
| ---------------------------------------------------- | ------: | -----: | --------- | ----: | ---- | -------- |
| Power On Cycles                                      |       0 |      4 | True      |     0 | -    | Unsigned |
| Power Off Cycles                                     |       4 |      4 | True      |     0 | -    | Unsigned |
| Operating Time                                       |       8 |      4 | True      |     0 | s    | Unsigned |
| Under Voltage Counter                                |      12 |      4 | True      |     0 | -    | Unsigned |
| Watchdog Reset Counter                               |      16 |      4 | True      |     0 | -    | Unsigned |
| [Production Date: Year](#value:sth-production-date)  |      20 |      4 | False     |     - | -    | ASCII    |
| [Production Date: Month](#value:sth-production-date) |      24 |      2 | False     |     - | -    | ASCII    |
| [Production Date: Day](#value:sth-production-date)   |      26 |      2 | False     |     - | -    | ASCII    |
| [Batch Number](#value:sth-batch-number)              |      28 |      4 | True      |     - | -    | Unsigned |

- <a name="value:sth-production-date">**Production Date**:</a> This date depends on the production date of the STH (printed on the PCB). It can be changed in the [configuration of ICOc][config].
- <a name="value:sth-batch-number">**Batch Number**:</a> This value can be changed in the [configuration of ICOc][config].

<a name="page:sth-calibration"></a>

### Page `Calibration`

| Name                                                   | Address | Length | Read Only | Value | Format |
| ------------------------------------------------------ | ------: | -----: | --------- | ----- | ------ |
| [Acceleration X: Slope](#value:acceleration-x-slope)   |       0 |      4 | False     | -     | Float  |
| [Acceleration X: Offset](#value:acceleration-x-offset) |       4 |      4 | False     | -     | Float  |

#### Acceleration

- <a name="value:acceleration-x-slope"></a> **Acceleration X: Slope**: A Acceleration increase for a single step according to the following formula:

  $$
  \frac{a_{max}}{{ADC}_{max}}
  $$

  Here

  - $a_{max}$ is the maximum acceleration difference (e.g. `200` for a ±100 g sensor)
  - ${{ADC}_{max}}$ is the maximum value of the ADC (e.g. `65553` (= `2¹⁶`) for a 16-bit analog-digital converter)

- <a name="value:acceleration-x-offset"></a> **Acceleration X: Offset**: The negative offset of the acceleration value according to the following formula

  $$
  -\frac{a_{max}}{2}
  $$

  Here $a_{max}$ is the maximum acceleration difference (e.g. `100` for a ±50 g sensor)

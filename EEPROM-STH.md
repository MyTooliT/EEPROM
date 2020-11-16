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

| Name                                                 | Address | Length | Read Only | Value | Format   |
| ---------------------------------------------------- | ------- | ------ | --------- | ----- | -------- |
| GTIN                                                 | 0       | 8      | True      | 0     | Unsigned |
| [Hardware Revision: Major](#value:hardware-revision) | 13      | 1      | False     | -     | Unsigned |
| [Hardware Revision: Minor](#value:hardware-revision) | 14      | 1      | False     | -     | Unsigned |
| [Hardware Revision: Build](#value:hardware-revision) | 15      | 1      | False     | -     | Unsigned |
| [Firmware Version: Major](#value:firmware-version)   | 21      | 1      | False     | -     | Unsigned |
| [Firmware Version: Minor](#value:firmware-version)   | 22      | 1      | False     | -     | Unsigned |
| [Firmware Version: Build](#value:firmware-version)   | 23      | 1      | False     | -     | Unsigned |
| [Release Name](#value:release-name)                  | 24      | 8      | False     | Tanja | UTF-8    |
| [Serial Number](#value:serial-number)                | 32      | 32     | True      | 0     | UTF-8    |
| [Product Name](#value:product-name)                  | 64      | 128    | True      | 0     | UTF-8    |
| [OEM Free Use](#value:oem-free-use)                  | 192     | 64     | True      | 0     | -        |

#### Version Numbers

- <a name="value:hardware-revision"></a> **Hardware Revision**: This number depends on the hardware revision (printed on the PCB). The value itself can be changed in the [main configuration file of ICOc][config]
- <a name="value:firmware-version"></a> **Firmware Version**: This number depends on the current [STH software version](https://github.com/MyTooliT/STH/releases)
- <a name="value:release-name"></a> **Release Name**: This text can be changed in the [configuration of ICOc][config]
- <a name="value:serial-number"></a> **Serial Number**: This text can be changed in the [configuration of ICOc][config]
- <a name="value:product-name"></a> **Product Name**: This text can be changed in the [configuration of ICOc][config]
- <a name="value:oem-free-use"></a> **OEM Free Use**: This value can be changed in the [configuration of ICOc][config].

[config]: https://github.com/MyTooliT/ICOc/blob/master/Configuration/config.yaml

<a name="page:statistic"></a>

### Page `Statistic`

| Name                                             | Address | Length | Read Only | Value | Unit | Format   |
| ------------------------------------------------ | ------- | ------ | --------- | ----- | ---- | -------- |
| Power On Cycles                                  | 0       | 4      | True      | 0     | -    | Unsigned |
| Power Off Cycles                                 | 4       | 4      | True      | 0     | -    | Unsigned |
| Operating Time                                   | 8       | 4      | True      | 0     | s    | Unsigned |
| Under Voltage Counter                            | 12      | 4      | True      | 0     | -    | Unsigned |
| Watchdog Reset Counter                           | 16      | 4      | True      | 0     | -    | Unsigned |
| [Production Date: Year](#value:production-date)  | 20      | 4      | False     | -     | -    | ASCII    |
| [Production Date: Month](#value:production-date) | 24      | 2      | False     | -     | -    | ASCII    |
| [Production Date: Day](#value:production-date)   | 26      | 2      | False     | -     | -    | ASCII    |
| [Batch Number](#value:batch-number)              | 28      | 4      | True      | -     | -    | Unsigned |

- <a name="value:production-date">**Production Date**:</a> This date depends on the production date of the STH (printed on the PCB). It can be changed in the [configuration of ICOc][config].
- <a name="value:batch-number">**Batch Number**:</a> This value can be changed in the [configuration of ICOc][config].

<a name="page:calibration"></a>

### Page `Calibration`

| Name                                                   | Address | Length | Read Only | Value                         | Format |
| ------------------------------------------------------ | ------- | ------ | --------- | ----------------------------- | ------ |
| [Acceleration X: Slope](#value:acceleration-x-slope)   | 0       | 4      | False     | -                             | Float  |
| [Acceleration X: Offset](#value:acceleration-x-offset) | 4       | 4      | False     | -                             | Float  |
| Acceleration Y: Slope                                  | 8       | 4      | False     | [Undefined](#value:undefined) | Float  |
| Acceleration Y: Offset                                 | 12      | 4      | False     | [Undefined](#value:undefined) | Float  |
| Acceleration Z: Slope                                  | 16      | 4      | False     | [Undefined](#value:undefined) | Float  |
| Acceleration Z: Offset                                 | 20      | 4      | False     | [Undefined](#value:undefined) | Float  |
| Voltage Battery: Slope                                 | 24      | 4      | False     | [Undefined](#value:undefined) | Float  |
| Voltage Battery: Offset                                | 28      | 4      | False     | [Undefined](#value:undefined) | Float  |
| Voltage 2: Slope                                       | 32      | 4      | False     | [Undefined](#value:undefined) | Float  |
| Voltage 2: Offset                                      | 36      | 4      | False     | [Undefined](#value:undefined) | Float  |
| Voltage 3: Slope                                       | 40      | 4      | False     | [Undefined](#value:undefined) | Float  |
| Voltage 3: Offset                                      | 44      | 4      | False     | [Undefined](#value:undefined) | Float  |
| Internal Temperature: Slope                            | 48      | 4      | False     | [Undefined](#value:undefined) | Float  |
| Internal Temperature: Offset                           | 52      | 4      | False     | [Undefined](#value:undefined) | Float  |
| Temperature 2: Slope                                   | 56      | 4      | False     | [Undefined](#value:undefined) | Float  |
| Temperature 2: Offset                                  | 60      | 4      | False     | [Undefined](#value:undefined) | Float  |
| Temperature 3: Slope                                   | 64      | 4      | False     | [Undefined](#value:undefined) | Float  |
| Temperature 3: Offset                                  | 68      | 4      | False     | [Undefined](#value:undefined) | Float  |

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

<a name="value:undefined"></a>

#### Undefined Values

These are values that are currently not initialized by the tests of ICOc

# EEPROM

## Terms

- <a name="term:little-endian">Little Endian</a>: Store the least significant byte (LSB) at the first (smallest) memory address and the most significant byte (MSB) at the last (highest) memory address

## Layout

- Every page consists of 256 bytes
- The address of a page is the page number multiplied by 256

### Pages:

| Page Number | Name                                               | Description                                                                                         |
| ----------: | -------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
|           0 | [System Configuration](#page:system-configuration) | Store system specific data e.g. Bluetooth name and advertisement time                               |
|           4 | [Product Data](#page:product-data)                 | Store product data e.g. serial number                                                               |
|           5 | [Statistics](#page:statistics)                     | Store statistic data e.g. power on/off cycles                                                       |
|           8 | [Calibration](#page:calibration)                   | Store configuration data like slope (`k`) and offset (`d`) values to derive SI value from ADC value |

<a name="page:system-configuration"></a>

#### Page `System Configuration`

| Byte | Length | Name                 | Comment                                                                          | Format   | Unit |
| ---: | -----: | -------------------- | -------------------------------------------------------------------------------- | -------- | ---- |
|    0 |      1 | Init                 | • `0xac`: Initialized <br/> • `0xca`: Locked <br/> • Other Value: Uninitialized) | -        | -    |
|    1 |      8 | Radio Name           | Bluetooth advertisement name                                                     | ASCII    | -    |
|    9 |      4 | Sleep Time 1         | [Little Endian](#term:little-endian)                                             | Unsigned | ms   |
|   13 |      2 | Advertisement Time 1 | [Little Endian](#term:little-endian)                                             | Unsigned | ms   |
|   15 |      4 | Sleep Time 2         | [Little Endian](#term:little-endian)                                             | Unsigned | ms   |
|   19 |      2 | Advertisement Time 2 | [Little Endian](#term:little-endian)                                             | Unsigned | ms   |

##### Sleep & Advertisement Times

```{r, fig.align="center", out.width="80%", echo=FALSE}
knitr::include_graphics("Pictures/STH States.svg", auto_pdf = TRUE)
```

- `Sleep Time 1`: Time to switch from the `Disconnected` state to `Sleep Mode 1` (low power usage)
- `Sleep Time 2`: Time switch from the `Sleep Mode 1` state to `Sleep Mode 2` (very low power usage)
- `Advertisement Time 1`: Advertisement time in `Sleep Mode 1`
- `Advertisement Time 2`: Advertisement time in `Sleep Mode 2`

<a name="page:product-data"></a>

#### Page `Product Data`

| Byte | Length | Name                                      | Comment                              | Format   |
| ---: | -----: | ----------------------------------------- | ------------------------------------ | -------- |
|    0 |      8 | Global Trade Identification Number (GTIN) | [Little Endian](#term:little-endian) | Unsigned |
|    8 |      5 | Hardware Version: Reserved               |                                      | –        |
|   13 |      1 | Hardware Version: Major                  |                                      | Unsigned |
|   14 |      1 | Hardware Version: Minor                  |                                      | Unsigned |
|   15 |      1 | Hardware Version: Patch                  |                                      | Unsigned |
|   16 |      5 | Firmware Version: Reserved                |                                      | –        |
|   21 |      1 | Firmware Version: Major                   |                                      | Unsigned |
|   22 |      1 | Firmware Version: Minor                   |                                      | Unsigned |
|   23 |      1 | Firmware Version: Patch                   |                                      | Unsigned |
|   24 |      8 | [Release Name](#value:release-name)       |                                      | UTF-8    |
|   32 |     32 | [Serial Number](#value:serial-number)     |                                      | UTF-8    |
|   64 |    128 | [Product Name](#value:product-name)       |                                      | UTF-8    |
|  192 |     64 | [OEM Free Use](#value:oem-free-use)       |                                      | -        |

##### Version Numbers

- Version numbers will look like this `Major.Minor.Patch` (e.g. `1.2.3`)
- Major specifies the first digit of the version number (usually only increased for “breaking” changes)
- Minor specifies the second digit of the version number (usually only increased for “minor” changes)
- Patch specifies the third digit of the version number (usually increased for “bug fixes”)

<a name="value:release-name"></a>

##### Release Name

This text specifies the code name of the STH/STU software release

<a name="value:serial-number"></a>

##### Serial Number

- Place for manufacture serial number (derived from ISBN)
- Possible Layout:
  - Product Group
  - Subgroup
  - Manufacture ID
  - Product Number
  - Check Digit
- Currently unused

<a name="value:product-name"></a>

##### Product Name

- This text might be used to extend the serial Number
- Possible Use: URL that point to additional information
- Currently unused

<a name="value:oem-free-use"></a>

##### OEM Free Use

- Manufacture specific information
- Format is free to choose

<a name="page:statistics"></a>

#### Page `Statistics`

| Byte | Length | Name                                                  | Comment                                     | Format   | Unit |
| ---: | -----: | ----------------------------------------------------- | ------------------------------------------- | -------- | ---- |
|    0 |      4 | [Power On Cycles](#value:power-on-cycles)             | [Little Endian](#term:little-endian)        | Unsigned | -    |
|    4 |      4 | Power Off Cycles                                      | [Little Endian](#term:little-endian)        | Unsigned | -    |
|    8 |      4 | Operating Time                                        | [Little Endian](#term:little-endian)        | Unsigned | s    |
|   12 |      4 | [Under Voltage Counter](#value:under-voltage-counter) | [Little Endian](#term:little-endian)        | Unsigned | -    |
|   16 |      4 | Watchdog Reset Counter                                | [Little Endian](#term:little-endian)        | Unsigned | -    |
|   20 |      4 | Production Date: Year                                 |                                             | ASCII    | -    |
|   24 |      2 | Production Date: Month                                |                                             | ASCII    | -    |
|   26 |      2 | Production Date: Day                                  |                                             | ASCII    | -    |
|   28 |      4 | Batch Number                                          | Consecutive number for manufactured devices | ASCII    | -    |

<a name="value:power-on-cycles"></a>

##### Power On Cycles

Please note, that a reset also counts as power on cycle

<a name="value:under-voltage-counter"></a>

##### Under Voltage Counter

Counts of under voltages that cause turn off state (brownout)

<a name="page:calibration"></a>

#### Page `Calibration`

| Byte | Length | Name                         | Comment                              | Format |
| ---: | -----: | ---------------------------- | ------------------------------------ | ------ |
|    0 |      4 | Acceleration X: Slope        | [Little Endian](#term:little-endian) | Float  |
|    4 |      4 | Acceleration X: Offset       | [Little Endian](#term:little-endian) | Float  |
|    8 |      4 | Acceleration Y: Slope        | [Little Endian](#term:little-endian) | Float  |
|   12 |      4 | Acceleration Y: Offset       | [Little Endian](#term:little-endian) | Float  |
|   16 |      4 | Acceleration Z: Slope        | [Little Endian](#term:little-endian) | Float  |
|   20 |      4 | Acceleration Z: Offset       | [Little Endian](#term:little-endian) | Float  |
|   24 |      4 | Voltage Battery: Slope       | [Little Endian](#term:little-endian) | Float  |
|   28 |      4 | Voltage Battery: Offset      | [Little Endian](#term:little-endian) | Float  |
|   32 |      4 | Voltage 2: Slope             | [Little Endian](#term:little-endian) | Float  |
|   36 |      4 | Voltage 2: Offset            | [Little Endian](#term:little-endian) | Float  |
|   40 |      4 | Voltage 3: Slope             | [Little Endian](#term:little-endian) | Float  |
|   44 |      4 | Voltage 3: Offset            | [Little Endian](#term:little-endian) | Float  |
|   48 |      4 | Internal Temperature: Slope  | [Little Endian](#term:little-endian) | Float  |
|   52 |      4 | Internal Temperature: Offset | [Little Endian](#term:little-endian) | Float  |
|   56 |      4 | Temperature 2: Slope         | [Little Endian](#term:little-endian) | Float  |
|   60 |      4 | Temperature 2: Offset        | [Little Endian](#term:little-endian) | Float  |
|   64 |      4 | Temperature 3: Slope         | [Little Endian](#term:little-endian) | Float  |
|   68 |      4 | Temperature 3: Offset        | [Little Endian](#term:little-endian) | Float  |

##### Slope & Offset

The values slope (`k`) and offset (`d`) specify the values in the equation for the [linear function](https://en.m.wikipedia.org/wiki/Linear_function):

$$
y = f(x) = k·x + d
$$

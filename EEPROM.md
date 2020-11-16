# EEPROM

## Terms

- <a name="term:little-endian">Little Endian</a>: Store the least significant byte (LSB) at the first (smallest) memory address and the most significant byte at the last (highest) memory address

## Layout

- Every page consists of 256 bytes
- The address of a page is the page number multiplied by 256

### Pages:

| Page Number | Name                                               | Description                                                                                         |
| ----------- | -------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| 0           | [System Configuration](#page:system-configuration) | Store system specific data e.g. Bluetooth name and advertisement time                               |
| 4           | [Product Data](#page:product-data)                 | Store product data e.g. serial number                                                               |
| 5           | [Statistic](#page:statistic)                       | Store statistic data e.g. power on/off cycles                                                       |
| 8           | [Calibration](#page:calibration)                   | Store configuration data like slope (`k`) and offset (`d`) values to derive SI value from ADC value |

<a name="page:system-configuration"></a>

#### Page `System Configuration`

| Byte    | Length | Name                 | Comment                                                                        | Format   | Unit |
| ------- | ------ | -------------------- | ------------------------------------------------------------------------------ | -------- | ---- |
| 0       | 1      | Init                 | • `0xAC`: Initialized <br> • `0xCA`: Locked <br> • Other Value: Uninitialized) | -        | -    |
| 1 – 8   | 8      | Radio Name           | Bluetooth advertisement name                                                   | ASCII    | -    |
| 9 – 12  | 4      | Sleep Time 1         | [Little Endian](#term:little-endian)                                           | Unsigned | ms   |
| 13 – 14 | 2      | Advertisement Time 1 | [Little Endian](#term:little-endian)                                           | Unsigned | ms   |
| 15 – 18 | 4      | Sleep Time 2         | [Little Endian](#term:little-endian)                                           | Unsigned | ms   |
| 19 – 20 | 2      | Advertisement Time 2 | [Little Endian](#term:little-endian)                                           | Unsigned | ms   |

##### Sleep & Advertisement Times

![STH States](https://raw.githubusercontent.com/MyTooliT/Diagrams/master/Graphs/STH%20States.svg)

- `Sleep Time 1`: Time to switch from the `Disconnected` state to `Sleep Mode 1` (low power usage)
- `Sleep Time 2`: Time switch from the `Sleep Mode 1` state to `Sleep Mode 2` (very low power usage)
- `Advertisement Time 1`: Advertisement time in `Sleep Mode 1`
- `Advertisement Time 2`: Advertisement time in `Sleep Mode 2`

<a name="page:product-data"></a>

#### Page `Product Data`

| Byte      | Length | Name                                        | Comment                              | Format   |
| --------- | ------ | ------------------------------------------- | ------------------------------------ | -------- |
| 0 – 7     | 8      | Global Trade Identification Number (GTIN)   | [Little Endian](#term:little-endian) | Unsigned |
| 8 – 12    | 5      | Hardware Revision - Reserved                |                                      | –        |
| 13        | 1      | Hardware Revision - Major                   |                                      | Unsigned |
| 14        | 1      | Hardware Revision - Minor                   |                                      | Unsigned |
| 15        | 1      | Hardware Revision - Build                   |                                      | Unsigned |
| 16 – 20   | 5      | Firmware Version - Reserved                 |                                      | –        |
| 21        | 1      | Firmware Version - Major                    |                                      | Unsigned |
| 22        | 1      | Firmware Version - Minor                    |                                      | Unsigned |
| 23        | 1      | Firmware Version - Build                    |                                      | Unsigned |
| 24 - 31   | 8      | [Release Name](#value:release-name)         |                                      | UTF-8    |
| 32 - 63   | 32     | [Serial Number](#value:serial-number)       |                                      | UTF-8    |
| 64 - 191  | 128    | [Manufacture Name](#value:manufacture-name) |                                      | UTF-8    |
| 192 - 255 | 64     | [OEM Free Use](#value:oem-free-use)         |                                      | -        |

##### Version Numbers

- Version numbers will look like this `Major.Minor.Build` (e.g. `1.2.3`)
- Major specifies the first digit of the version number (usually only increased for “breaking” changes)
- Minor specifies the second digit of the version number (usually only increased for “minor” changes)
- Build specifies the third digit of the version number (usually increased for “bug fixes”)

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

<a name="value:name"></a>

##### Manufacture Name

- This text might be used to extend the serial Number
- Possible Use: URL that point to additional information
- Currently unused

<a name="value:oem-free-use"></a>

##### OEM Free Use

- Manufacture specific information
- Format is free to choose

<a name="page:statistic"></a>

#### Page `Statistic`

| Byte | Name                                      | Comment | Format   | Unit |
| ---- | ----------------------------------------- | ------- | -------- | ---- |
| 0    | [Power On Cycles](#value:power-on-cycles) | LSB     | Unsigned | -    |
| 1    | [Power On Cycles](#value:power-on-cycles) |         | Unsigned | -    |
| 2    | [Power On Cycles](#value:power-on-cycles) |         | Unsigned | -    |
| 3    | [Power On Cycles](#value:power-on-cycles) | MSB     | Unsigned | -    |
| 4    | Power Off Cycles                          | LSB     | Unsigned | -    |
| 5    | Power Off Cycles                          |         | Unsigned | -    |
| 6    | Power Off Cycles                          |         | Unsigned | -    |
| 7    | Power Off Cycles                          | MSB     | Unsigned | -    |
| 8    | Operating Time                            | LSB     | Unsigned | s    |
| 9    | Operating Time                            |         | Unsigned | s    |
| 10   | Operating Time                            |         | Unsigned | s    |
| 11   | Operating Time                            | MSB     | Unsigned | s    |
| 12   | Under Voltage Counter                     | LSB     | Unsigned | -    |
| 13   | Under Voltage Counter                     |         | Unsigned | -    |
| 14   | Under Voltage Counter                     |         | Unsigned | -    |
| 15   | Under Voltage Counter                     | MSB     | Unsigned | -    |
| 16   | WatchDog Reset Cause                      | LSB     | Unsigned | -    |
| 17   | WatchDog Reset Cause                      |         | Unsigned | -    |
| 18   | WatchDog Reset Cause                      |         | Unsigned | -    |
| 19   | WatchDog Reset Cause                      | MSB     | Unsigned | -    |
| 20   | Production Date Year                      |         | ASCII    | -    |
| 21   | Production Date Year                      |         | ASCII    | -    |
| 22   | Production Date Year                      |         | ASCII    | -    |
| 23   | Production Date Year                      |         | ASCII    | -    |
| 24   | Production Date Month                     |         | ASCII    | -    |
| 25   | Production Date Month                     |         | ASCII    | -    |
| 26   | Production Date Day                       |         | ASCII    | -    |
| 27   | Production Date Day                       |         | ASCII    | -    |

<a name="value:power-on-cycles"></a>

##### Power On Cycles

Please note, that a reset also counts as power on cycle

<a name="page:calibration"></a>

#### Page `Calibration`

| Byte | Name                         | Comment | Format |
| ---- | ---------------------------- | ------- | ------ |
| 0    | Acceleration X: Slope        | LSB     | Float  |
| 1    | Acceleration X: Slope        |         | Float  |
| 2    | Acceleration X: Slope        |         | Float  |
| 3    | Acceleration X: Slope        | MSB     | Float  |
| 4    | Acceleration X: Offset       | LSB     | Float  |
| 5    | Acceleration X: Offset       |         | Float  |
| 6    | Acceleration X: Offset       |         | Float  |
| 7    | Acceleration X: Offset       | MSB     | Float  |
| 8    | Acceleration Y: Slope        | LSB     | Float  |
| 9    | Acceleration Y: Slope        |         | Float  |
| 10   | Acceleration Y: Slope        |         | Float  |
| 11   | Acceleration Y: Slope        | MSB     | Float  |
| 12   | Acceleration Y: Offset       | LSB     | Float  |
| 13   | Acceleration Y: Offset       |         | Float  |
| 14   | Acceleration Y: Offset       |         | Float  |
| 15   | Acceleration Y: Offset       | MSB     | Float  |
| 16   | Acceleration Z: Slope        | LSB     | Float  |
| 17   | Acceleration Z: Slope        |         | Float  |
| 18   | Acceleration Z: Slope        |         | Float  |
| 19   | Acceleration Z: Slope        | MSB     | Float  |
| 20   | Acceleration Z: Offset       | LSB     | Float  |
| 21   | Acceleration Z: Offset       |         | Float  |
| 22   | Acceleration Z: Offset       |         | Float  |
| 23   | Acceleration Z: Offset       | MSB     | Float  |
| 24   | Voltage Battery: Slope       | LSB     | Float  |
| 25   | Voltage Battery: Slope       |         | Float  |
| 26   | Voltage Battery: Slope       |         | Float  |
| 27   | Voltage Battery: Slope       | MSB     | Float  |
| 28   | Voltage Battery: Offset      | LSB     | Float  |
| 29   | Voltage Battery: Offset      |         | Float  |
| 30   | Voltage Battery: Offset      |         | Float  |
| 31   | Voltage Battery: Offset      | MSB     | Float  |
| 32   | Voltage 2: Slope             | LSB     | Float  |
| 33   | Voltage 2: Slope             |         | Float  |
| 34   | Voltage 2: Slope             |         | Float  |
| 35   | Voltage 2: Slope             | MSB     | Float  |
| 36   | Voltage 2: Offset            | LSB     | Float  |
| 37   | Voltage 2: Offset            |         | Float  |
| 38   | Voltage 2: Offset            |         | Float  |
| 39   | Voltage 2: Offset            | MSB     | Float  |
| 40   | Voltage 3: Slope             | LSB     | Float  |
| 41   | Voltage 3: Slope             |         | Float  |
| 42   | Voltage 3: Slope             |         | Float  |
| 43   | Voltage 3: Slope             | MSB     | Float  |
| 44   | Voltage 3: Offset            | LSB     | Float  |
| 45   | Voltage 3: Offset            |         | Float  |
| 46   | Voltage 3: Offset            |         | Float  |
| 47   | Voltage 3: Offset            | MSB     | Float  |
| 48   | Internal Temperature: Slope  | LSB     | Float  |
| 49   | Internal Temperature: Slope  |         | Float  |
| 50   | Internal Temperature: Slope  |         | Float  |
| 51   | Internal Temperature: Slope  | MSB     | Float  |
| 52   | Internal Temperature: Offset | LSB     | Float  |
| 53   | Internal Temperature: Offset |         | Float  |
| 54   | Internal Temperature: Offset |         | Float  |
| 55   | Internal Temperature: Offset | MSB     | Float  |
| 56   | Temperature 2: Slope         | LSB     | Float  |
| 57   | Temperature 2: Slope         |         | Float  |
| 58   | Temperature 2: Slope         |         | Float  |
| 59   | Temperature 2: Slope         | MSB     | Float  |
| 60   | Temperature 2: Offset        | LSB     | Float  |
| 61   | Temperature 2: Offset        |         | Float  |
| 62   | Temperature 2: Offset        |         | Float  |
| 63   | Temperature 2: Offset        | MSB     | Float  |
| 64   | Temperature 3: Slope         | LSB     | Float  |
| 65   | Temperature 3: Slope         |         | Float  |
| 66   | Temperature 3: Slope         |         | Float  |
| 67   | Temperature 3: Slope         | MSB     | Float  |
| 68   | Temperature 3: Offset        | LSB     | Float  |
| 69   | Temperature 3: Offset        |         | Float  |
| 70   | Temperature 3: Offset        |         | Float  |
| 71   | Temperature 3: Offset        | MSB     | Float  |

##### Slope & Offset

The values slope (`k`) and offset (`d`) specify the values in the equation for the [linear function](https://en.m.wikipedia.org/wiki/Linear_function):

$$
y = f(x) = k·x + d
$$

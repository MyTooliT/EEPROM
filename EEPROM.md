# EEPROM

## Layout

- Every page consists of 256 bytes
- The address of a page is the page number multiplied by 256

### Pages:

| Page Number | Name                                                 | Description                                                                    |
| ----------- | ---------------------------------------------------- | ------------------------------------------------------------------------------ |
| 0           | [System Configuration 0](#page:system-configuration) | Store system specific data e.g. Bluetooth name, advertisement time, etc.       |
| 4           | [Product Data](#page:product-data)                   | Store product data e.g. serial number                                          |
| 5           | [Statistic](#page:statistic)                         | Store Statistic data e.g. power on/off cycles etc.                             |
| 8           | [Calibration 0](#page:calibration)                   | Store configuration data like k and d values to derive SI value from ADC value |

<a name="page:system-configuration"></a>

#### Page `System Configuration 0`

| Byte | Description          | Comment                                                                 | Format   | Unit |
| ---- | -------------------- | ----------------------------------------------------------------------- | -------- | ---- |
| 0    | Init                 | • `0xAC`: Init <br> • `0xCA`: Locked <br> • Other Value: Uninitialized) | -        | -    |
| 1    | Radio Name 0         |                                                                         | ASCII    | -    |
| 2    | Radio Name 1         |                                                                         | ASCII    | -    |
| 3    | Radio Name 2         |                                                                         | ASCII    | -    |
| 4    | Radio Name 3         |                                                                         | ASCII    | -    |
| 5    | Radio Name 4         |                                                                         | ASCII    | -    |
| 6    | Radio Name 5         |                                                                         | ASCII    | -    |
| 7    | Radio Name 6         |                                                                         | ASCII    | -    |
| 8    | Radio Name 7         |                                                                         | ASCII    | -    |
| 9    | Sleep Time 1         | LSB                                                                     | Unsigned | ms   |
| 10   | Sleep Time 1         |                                                                         | Unsigned | ms   |
| 11   | Sleep Time 1         |                                                                         | Unsigned | ms   |
| 12   | Sleep Time 1         | MSB                                                                     | Unsigned | ms   |
| 13   | Advertisement Time 1 | LSB                                                                     | Unsigned | ms   |
| 14   | Advertisement Time 1 | MSB                                                                     | Unsigned | ms   |
| 15   | Sleep Time 2         | LSB                                                                     | Unsigned | ms   |
| 16   | Sleep Time 2         |                                                                         | Unsigned | ms   |
| 17   | Sleep Time 2         |                                                                         | Unsigned | ms   |
| 18   | Sleep Time 2         | MSB                                                                     | Unsigned | ms   |
| 19   | Advertisement Time 2 | LSB                                                                     | Unsigned | ms   |
| 20   | Advertisement Time 2 | MSB                                                                     | Unsigned | ms   |

##### Sleep & Advertisement Times

![STH States](https://raw.githubusercontent.com/MyTooliT/Diagrams/master/Graphs/STH%20States.svg)

- `Sleep Time 1`: Time to switch from the `Disconnected` state to `Sleep Mode 1` (low power usage)
- `Sleep Time 2`: Time switch from the `Sleep Mode 1` state to `Sleep Mode 2` (very low power usage)
- `Advertisement Time 1`: Advertisement time in `Sleep Mode 1`
- `Advertisement Time 2`: Advertisement time in `Sleep Mode 2`

<a name="page:product-data"></a>

#### Page `Product Data`

| Byte      | Description                                         | Format        |
| --------- | --------------------------------------------------- | ------------- |
| 0         | Global Trade Identification Number (GTIN) - 0 (LSB) | unsigned      |
| 1         | Global Trade Identification Number (GTIN) - 1       | unsigned      |
| 2         | Global Trade Identification Number (GTIN) - 2       | unsigned      |
| 3         | Global Trade Identification Number (GTIN) - 3       | unsigned      |
| 4         | Global Trade Identification Number (GTIN) - 4       | unsigned      |
| 5         | Global Trade Identification Number (GTIN) - 5       | unsigned      |
| 6         | Global Trade Identification Number (GTIN) - 6       | unsigned      |
| 7         | Global Trade Identification Number (GTIN) - 7 (MSB) | unsigned      |
| 8         | Hardware Revision - Reserved - 1                    | unsigned      |
| 9         | Hardware Revision - Reserved - 2                    | unsigned      |
| 10        | Hardware Revision - Reserved - 3                    | unsigned      |
| 11        | Hardware Revision - Reserved - 4                    | unsigned      |
| 12        | Hardware Revision - Reserved - 5                    | unsigned      |
| 13        | Hardware Revision - Major                           | unsigned      |
| 14        | Hardware Revision - Minor                           | unsigned      |
| 15        | Hardware Revision - Build                           | unsigned      |
| 16        | Firmware Version - Reserved - 1                     | unsigned      |
| 17        | Firmware Version - Reserved - 2                     | unsigned      |
| 18        | Firmware Version - Reserved - 3                     | unsigned      |
| 19        | Firmware Version - Reserved - 4                     | unsigned      |
| 20        | Firmware Version - Reserved - 5                     | unsigned      |
| 21        | Firmware Version - Major                            | unsigned      |
| 22        | Firmware Version - Minor                            | unsigned      |
| 23        | Firmware Version - Build                            | unsigned      |
| 24 - 31   | Release Name 0-7                                    | UTF8 - String |
| 32 - 63   | Serial Number 0-31                                  | UTF8 - String |
| 64 - 191  | Name 0-127                                          | UTF8 - String |
| 192 - 255 | OEM Free Use 0-63                                   | -             |

<a name="page:statistic"></a>

#### Page `Statistic`

| Byte | Description                                              | Format         |
| ---- | -------------------------------------------------------- | -------------- |
| 0    | Power ON Cycles - 0 (LSB)                                | unsigned       |
| 1    | Power ON Cycles - 1                                      | unsigned       |
| 2    | Power ON Cycles - 2                                      | unsigned       |
| 3    | Power ON Cycles - 3 (MSB)                                | unsigned       |
| 4    | Power OFF Cycles - 0 (LSB)                               | unsigned       |
| 5    | Power OFF Cycles - 1                                     | unsigned       |
| 6    | Power OFF Cycles - 2                                     | unsigned       |
| 7    | Power OFF Cycles - 3 (MSB)                               | unsigned       |
| 8    | Operating Time since first Power On in seconds - 0 (LSB) | unsigned       |
| 9    | Operating Time since first Power On in seconds - 1       | unsigned       |
| 10   | Operating Time since first Power On in seconds - 2       | unsigned       |
| 11   | Operating Time since first Power On in seconds - 3 (MSB) | unsigned       |
| 12   | Under Voltage Counter since first Power On - 0 (LSB)     | unsigned       |
| 13   | Under Voltage Counter since first Power On - 1           | unsigned       |
| 14   | Under Voltage Counter since first Power On - 2           | unsigned       |
| 15   | Under Voltage Counter since first Power On - 3 (MSB)     | unsigned       |
| 16   | WatchDogResetCause - 0 (LSB)                             | unsigned       |
| 17   | WatchDogResetCause - 1                                   | unsigned       |
| 18   | WatchDogResetCause - 2                                   | unsigned       |
| 19   | WatchDogResetCause - 3 (MSB)                             | unsigned       |
| 20   | Production Date - y0                                     | ASCII - String |
| 21   | Production Date - y1                                     | ASCII - String |
| 22   | Production Date - y2                                     | ASCII - String |
| 23   | Production Date - y3                                     | ASCII - String |
| 24   | Production Date - m0                                     | ASCII - String |
| 25   | Production Date - m1                                     | ASCII - String |
| 26   | Production Date - d0                                     | ASCII - String |
| 27   | Production Date - d1                                     | ASCII - String |

<a name="page:calibration"></a>

#### Page `Calibration 0`

| Byte | Description                      | Format                    |
| ---- | -------------------------------- | ------------------------- |
| 0    | Acceleration X - K - 0 (LSB)     | float - IEEE 754 binary32 |
| 1    | Acceleration X - K - 1           | float - IEEE 754 binary32 |
| 2    | Acceleration X - K - 2           | float - IEEE 754 binary32 |
| 3    | Acceleration X - K - 3 (MSB)     | float - IEEE 754 binary32 |
| 4    | Acceleration X - D - 0 (LSB)     | float - IEEE 754 binary32 |
| 5    | Acceleration X - D - 1           | float - IEEE 754 binary32 |
| 6    | Acceleration X - D- 2            | float - IEEE 754 binary32 |
| 7    | Acceleration X - D - 3 (MSB)     | float - IEEE 754 binary32 |
| 8    | Acceleration Y - K - 0 (LSB)     | float - IEEE 754 binary32 |
| 9    | Acceleration Y - K - 1           | float - IEEE 754 binary32 |
| 10   | Acceleration Y - K - 2           | float - IEEE 754 binary32 |
| 11   | Acceleration Y - K - 3 (MSB)     | float - IEEE 754 binary32 |
| 12   | Acceleration Y - D - 0 (LSB)     | float - IEEE 754 binary32 |
| 13   | Acceleration Y - D - 1           | float - IEEE 754 binary32 |
| 14   | Acceleration Y - D- 2            | float - IEEE 754 binary32 |
| 15   | Acceleration Y - D - 3 (MSB)     | float - IEEE 754 binary32 |
| 16   | Acceleration Z - K - 0 (LSB)     | float - IEEE 754 binary32 |
| 17   | Acceleration Z - K - 1           | float - IEEE 754 binary32 |
| 18   | Acceleration Z - K - 2           | float - IEEE 754 binary32 |
| 19   | Acceleration Z - K - 3 (MSB)     | float - IEEE 754 binary32 |
| 20   | Acceleration Z - D - 0 (LSB)     | float - IEEE 754 binary32 |
| 21   | Acceleration Z - D - 1           | float - IEEE 754 binary32 |
| 22   | Acceleration Z - D- 2            | float - IEEE 754 binary32 |
| 23   | Acceleration Z - D - 3 (MSB)     | float - IEEE 754 binary32 |
| 24   | Voltage Battery - K - 0 (LSB)    | float - IEEE 754 binary32 |
| 25   | Voltage Battery - K - 1          | float - IEEE 754 binary32 |
| 26   | Voltage Battery - K - 2          | float - IEEE 754 binary32 |
| 27   | Voltage Battery - K - 3 (MSB)    | float - IEEE 754 binary32 |
| 28   | Voltage Battery - D - 0 (LSB)    | float - IEEE 754 binary32 |
| 29   | Voltage Battery - D - 1          | float - IEEE 754 binary32 |
| 30   | Voltage Battery - D- 2           | float - IEEE 754 binary32 |
| 31   | Voltage Battery - D - 3 (MSB)    | float - IEEE 754 binary32 |
| 32   | Voltage 2 - K - 0 (LSB)          | float - IEEE 754 binary32 |
| 33   | Voltage 2 - K - 1                | float - IEEE 754 binary32 |
| 34   | Voltage 2 - K - 2                | float - IEEE 754 binary32 |
| 35   | Voltage 2 - K - 3 (MSB)          | float - IEEE 754 binary32 |
| 36   | Voltage 2 - D - 0 (LSB)          | float - IEEE 754 binary32 |
| 37   | Voltage 2 - D - 1                | float - IEEE 754 binary32 |
| 38   | Voltage 2 - D- 2                 | float - IEEE 754 binary32 |
| 39   | Voltage 2 - D - 3 (MSB)          | float - IEEE 754 binary32 |
| 40   | Voltage 3 - K - 0 (LSB)          | float - IEEE 754 binary32 |
| 41   | Voltage 3 - K - 1                | float - IEEE 754 binary32 |
| 42   | Voltage 3 - K - 2                | float - IEEE 754 binary32 |
| 43   | Voltage 3 - K - 3 (MSB)          | float - IEEE 754 binary32 |
| 44   | Voltage 3 - D - 0 (LSB)          | float - IEEE 754 binary32 |
| 45   | Voltage 3 - D - 1                | float - IEEE 754 binary32 |
| 46   | Voltage 3 - D- 2                 | float - IEEE 754 binary32 |
| 47   | Voltage 3 - D - 3 (MSB)          | float - IEEE 754 binary32 |
| 48   | Temperature Intern - K - 0 (LSB) | float - IEEE 754 binary32 |
| 49   | Temperature Intern - K - 1       | float - IEEE 754 binary32 |
| 50   | Temperature Intern - K - 2       | float - IEEE 754 binary32 |
| 51   | Temperature Intern - K - 3 (MSB) | float - IEEE 754 binary32 |
| 52   | Temperature Intern - D - 0 (LSB) | float - IEEE 754 binary32 |
| 53   | Temperature Intern - D - 1       | float - IEEE 754 binary32 |
| 54   | Temperature Intern - D- 2        | float - IEEE 754 binary32 |
| 55   | Temperature Intern - D - 3 (MSB) | float - IEEE 754 binary32 |
| 56   | Temperature 2 - K - 0 (LSB)      | float - IEEE 754 binary32 |
| 57   | Temperature 2 - K - 1            | float - IEEE 754 binary32 |
| 58   | Temperature 2 - K - 2            | float - IEEE 754 binary32 |
| 59   | Temperature 2 - K - 3 (MSB)      | float - IEEE 754 binary32 |
| 60   | Temperature 2 - D - 0 (LSB)      | float - IEEE 754 binary32 |
| 61   | Temperature 2 - D - 1            | float - IEEE 754 binary32 |
| 62   | Temperature 2 - D- 2             | float - IEEE 754 binary32 |
| 63   | Temperature 2 - D - 3 (MSB)      | float - IEEE 754 binary32 |
| 64   | Temperature 3 - K - 0 (LSB)      | float - IEEE 754 binary32 |
| 65   | Temperature 3 - K - 1            | float - IEEE 754 binary32 |
| 66   | Temperature 3 - K - 2            | float - IEEE 754 binary32 |
| 67   | Temperature 3 - K - 3 (MSB)      | float - IEEE 754 binary32 |
| 68   | Temperature 3 - D - 0 (LSB)      | float - IEEE 754 binary32 |
| 69   | Temperature 3 - D - 1            | float - IEEE 754 binary32 |
| 70   | Temperature 3 - D- 2             | float - IEEE 754 binary32 |
| 71   | Temperature 3 - D - 3 (MSB)      | float - IEEE 754 binary32 |

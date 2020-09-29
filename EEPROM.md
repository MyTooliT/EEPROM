# EEPROM

## Layout

- Every Page has 256 Byte
- The Address of a Page is the PageNumber*256

### Pages:

| Page Number | Name                                                 | Description                                                  |
| ----------- | ---------------------------------------------------- | ------------------------------------------------------------ |
| 0           | [System Configuration 0](#page:system-configuration) | Store System Specifig Data e.g. Bluetooth Name, Advertisment Time, etc. |
| 4           | [Product Data](#page:product-data)                   | Store Product Data e.g. Serial Number                        |
| 5           | Statistic                                            | Store Statistic Data e.g. Power on/off cylces etc.           |
| 8           | Calibration 0                                        | Store configuration data like k and d values to derive SI value from ADC value |

<a name="page:system-configuration"></a>

#### Page `System Configuration 0`

| Byte | Description                                                  | Format         |
| ---- | ------------------------------------------------------------ | -------------- |
| 0    | Init (0xAC=Init, 0xCA=Locked, else Uninit)                   | -              |
| 1    | Radio Name - 0                                               | ASCII - String |
| 2    | Radio Name - 1                                               | ASCII - String |
| 3    | Radio Name - 2                                               | ASCII - String |
| 4    | Radio Name - 3                                               | ASCII - String |
| 5    | Radio Name - 4                                               | ASCII - String |
| 6    | Radio Name - 5                                               | ASCII - String |
| 7    | Radio Name - 6                                               | ASCII - String |
| 8    | Radio Name - 7                                               | ASCII - String |
| 9    | Sleep Time 1 in ms (Energy Mode 0 -> Energy Mode 1) - 0 (LSB) | unsigned       |
| 10   | Sleep Time 1 in ms (Energy Mode 0 -> Energy Mode 1) - 1      | unsigned       |
| 11   | Sleep Time 1 in ms (Energy Mode 0 -> Energy Mode 1) - 2      | unsigned       |
| 12   | Sleep Time 1 in ms (Energy Mode 0 -> Energy Mode 1) - 3 (MSB) | unsigned       |
| 13   | Advertisement Time 1 in ms (Energy Mode 1) - 0 (LSB)         | unsigned       |
| 14   | Advertisement Time 1 in ms (Energy Mode 1) - 1 (MSB)         | unsigned       |
| 15   | Sleep Time 2 in ms (Energy Mode 1 -> Energy Mode 2) -  0 (LSB) | unsigned       |
| 16   | Sleep Time 2 in ms (Energy Mode 1 -> Energy Mode 2) -  1     | unsigned       |
| 17   | Sleep Time 2 in ms (Energy Mode 1 -> Energy Mode 2) -  2     | unsigned       |
| 18   | Sleep Time 2 in ms (Energy Mode 1 -> Energy Mode 2) -  3 (MSB) | unsigned       |
| 19   | Advertisement Time 2 in ms (Energy Mode 2) - 0 (LSB)         | unsigned       |
| 20   | Advertisement Time 2 in ms (Energy Mode 2) - 1 (MSB)         | unsigned       |

<a name="page:protuct-data"></a>

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


# EEPROM

## Layout

- Every Page has 256 Byte
- The Address of a Page is the PageNumber*256

### Pages:

| Page Number | Name                                                 | Description                                                  |
| ----------- | ---------------------------------------------------- | ------------------------------------------------------------ |
| 0           | [System Configuration 0](#page:system-configuration) | Store System Specifig Data e.g. Bluetooth Name, Advertisment Time, etc. |
| 4           | Product Data                                         | Store Product Data e.g. Serial Number                        |
| 5           | Statistic                                            | Store Statistic Data e.g. Power on/off cylces etc.           |
| 8           | Calibration 0                                        | Store configuration data like k and d values to derive SI value from ADC value |

<a name="page:system-configuration"></a>

#### System Configuration 0

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


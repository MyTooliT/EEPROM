# EEPROM

## Layout

Every Page has 256 Byte

The Address of a Page is the PageNumber*256

### Pages:

| Page Number | Name                   | Description                                                  |
| ----------- | ---------------------- | ------------------------------------------------------------ |
| 0           | System Configuration 0 | Store System Specifig Data e.g. Bluetooth Name, Advertisment Time, etc. |
| 4           | Product Data           | Store Product Data e.g. Serial Number                        |
| 5           | Statistic              | Store Statistic Data e.g. Power on/off cylces etc.           |
| 8           | Calibration 0          | Store configuration data like k and d values to derive SI value from ADC value |


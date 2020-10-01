# EEPROM-STU

This file contains the momentary used values of the EEPROM from the STU.

## Used Pages

| Page Number | Page Name                          |
| ----------- | ---------------------------------- |
| `0x4`       | [Product Data](#page:product-data) |
| `0x5`       | [Statistic](#page:statistic)       |

<a name="page:product-data"></a>

### Page `Product Data`

| Name                               | Address | Length | Read Only | Value                                            | Format   | Description                                                                                                            |
| ---------------------------------- | ------- | ------ | --------- | ------------------------------------------------ | -------- | ---------------------------------------------------------------------------------------------------------------------- |
| GTIN                               | 0       | 8      | True      | 0                                                | unsigned | Global Trade Identification Number (GTIN)                                                                              |
| Hardware Revision - Reserved       | 8       | 5      | True      | 0                                                | unsigned | Hardware Revision Number - Reserved                                                                                    |
| Hardware Revision - Major          | 13      | 1      | True      | 1                                                | unsigned | Hardware Revision Number - Major                                                                                       |
| Hardware Revision - Minor          | 14      | 1      | True      | 3                                                | unsigned | Hardware Revision Number - Minor                                                                                       |
| Hardware Revision - Build          | 15      | 1      | True      | 1                                                | unsigned | Hardware Revision Number - Build                                                                                       |
| Firmware Version Number - Reserved | 16      | 5      | True      | 0                                                | unsigned | Firmware Version Number - Reserved                                                                                     |
| Firmware Version Number - Major    | 21      | 1      | True      | 2                                                | unsigned | Firmware Version Number - Major                                                                                        |
| Firmware Version Number - Minor    | 22      | 1      | True      | 1                                                | unsigned | Firmware Version Number - Minor                                                                                        |
| Firmware Version Number - Build    | 23      | 1      | True      | 5                                                | unsigned | Firmware Version Number - Build                                                                                        |
| Release Name                       | 24      | 8      | True      | Valerie                                          | UTF8     | Release Name, represents Major - Minor                                                                                 |
| Serial Number                      | 32      | 32     | True      | MyToolItStu001-1-00001-001-2                     | UTF8     | Manufactor Serial Number (Derived from ISBN); Product Group - Subgroup - Manufacture ID - Product Number - Check Digit |
| Name                               | 64      | 128    | True      | Digital and Analog Communication with 5V -Supply | UTF8     | Manufactor Name; This may extend Serial Number, supports URL, extend definition, etc.                                  |
| OEM Free Use                       | 192     | 64     | True      | 0                                                | -        | Supports Manufactor Specific information in format that is free to choose                                              |

<a name="page:statistic"></a>

### Page `Statistic`

| Name                                       | Address | Length | Read Only | Value    | Unit    | Format   | Description                                                                       |
| ------------------------------------------ | ------- | ------ | --------- | -------- | ------- | -------- | --------------------------------------------------------------------------------- |
| Power ON Cycles                            | 0       | 4      | True      | 0        | -       | unsigned | Power On Cycles since first reset(Note that a resets also counts as power on)     |
| Power OFF Cycles                           | 4       | 4      | True      | 0        | -       | unsigned | Power Off Cycles since first reset                                                |
| Operating Time since first power On        | 8       | 4      | True      | 0        | seconds | unsigned | Operating Time since first power On in seconds                                    |
| Under Voltage Counter since first power On | 12      | 4      | True      | 0        | -       | unsigned | Counts of under voltages that yields into turn off state(Brown Out)               |
| Watchdog Reset Counter                     | 16      | 4      | True      | 0        | -       | unsigned | Watchdog Resets since first power on                                              |
| Production Date                            | 20      | 8      | True      | 20192031 | date    | ASCII    | Production Date (EEPROM Production Write) in the format yyyymmdd (year month day) |
| Batch Number                               | 28      | 4      | True      | 2        | -       | unsigned | Consecutive number for manufactured devices                                       |

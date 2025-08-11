![](logo-horizontal.jpg)
# Object Dictionary

### 1000 - Device Type

- **DataType:** UNSIGNED32
- **ObjectCode:** Array
- **Description:** Device type identification

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 1 | ro | 0 |
| 0x01 | Device Type | UNSIGNED32 | 0x20192 | const | 0 |

## 1001 - Error Register

- **DataType:** UNSIGNED8
- **ObjectCode:** Variable
- **Description:** Bitfield with error types

This object indicates the current error status of the device. Each bit represents a different error category:

| Bit | Value | Error Type | Description |
|-----|-------|------------|-------------|
| 0 | 0x01 | Generic error | General device error |
| 1 | 0x02 | Current error | Current-related error |
| 2 | 0x04 | Voltage error | Voltage-related error |
| 3 | 0x08 | Temperature error | Temperature-related error |
| 7 | 0x80 | Manufacturer error | Manufacturer-specific error |

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Error Register | UNSIGNED8 | - | ro | 0 |

## 1002 - Manufacturer status register

- **DataType:** UNSIGNED32
- **ObjectCode:** Variable
- **Description:** Manufacturer specific status information

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Manufacturer status register | UNSIGNED32 | - | ro | 1 |

## 1003 - Pre-defined error field

- **DataType:** UNSIGNED32
- **ObjectCode:** Array
- **Description:** Last 8 error history

This object stores the last 8 errors that occurred in the device. Error codes indicate different types of faults:

| Error Code | Description |
|------------|-------------|
| 0x1000 | Generic error |
| 0x2300 | Current error |
| 0x3100 | Voltage error |
| 0x4200 | Temperature error |
| 0x6100 | Device error |

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Number of errors | UNSIGNED8 | 0 | rw | 0 |
| 0x01 | Last Error | UNSIGNED32 | 0 | ro | 0 |
| 0x02 | 2nd Last Error | UNSIGNED32 | 0 | ro | 0 |
| 0x03 | 3rd Last Error | UNSIGNED32 | 0 | ro | 0 |
| 0x04 | 4th Last Error | UNSIGNED32 | 0 | ro | 0 |
| 0x05 | 5th Last Error | UNSIGNED32 | 0 | ro | 0 |
| 0x06 | 6th Last Error | UNSIGNED32 | 0 | ro | 0 |
| 0x07 | 7th Last Error | UNSIGNED32 | 0 | ro | 0 |
| 0x08 | 8th Last Error | UNSIGNED32 | 0 | ro | 0 |

## 1005 - COB ID SYNC

- **DataType:** UNSIGNED32
- **ObjectCode:** Variable
- **Description:** COB-ID of the synchronization object (SYNC)

This object indicates the configured COB-ID of the synchronization object (SYNC) and defines whether the CANopen device generates the SYNC.

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | COB ID SYNC | UNSIGNED32 | 0x00000080 | rw | 0 |

## 1006 - Communication cycle period

- **DataType:** UNSIGNED32
- **ObjectCode:** Variable
- **Description:** SYNC communication cycle period

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Communication cycle period | UNSIGNED32 | 0x00000000 | rw | 0 |

## 1007 - Synchronous window length

- **DataType:** UNSIGNED32
- **ObjectCode:** Variable
- **Description:** Synchronous PDO transmission window

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Synchronous window length | UNSIGNED32 | 0x00000000 | rw | 0 |

## 1008 - Manufacturer device name

- **DataType:** VISIBLE_STRING
- **ObjectCode:** Variable
- **Description:** Device name string

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Manufacturer device name | VISIBLE_STRING | Q-Drives C7 | const | 0 |

## 1009 - Manufacturer hardware version

- **DataType:** VISIBLE_STRING
- **ObjectCode:** Variable
- **Description:** Hardware version string

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Manufacturer hardware version | VISIBLE_STRING | - | const | 0 |

## 100a - Manufacturer software version

- **DataType:** VISIBLE_STRING
- **ObjectCode:** Variable
- **Description:** Software version string

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Manufacturer software version | VISIBLE_STRING | - | const | 0 |

## 1010 - Store parameters

- **DataType:** UNSIGNED32
- **ObjectCode:** Array
- **Description:** Save parameters to non-volatile memory

The object 0x1010 has to be written with the value "save" (0x65766173) to trigger saving, otherwise an error is reported.

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 4 | ro | 0 |
| 0x01 | Save all parameters | UNSIGNED32 | - | rw | 0 |
| 0x02 | Save communication parameters | UNSIGNED32 | - | rw | 0 |
| 0x03 | Save application parameters | UNSIGNED32 | - | rw | 0 |
| 0x04 | Save manufacturer parameters | UNSIGNED32 | - | rw | 0 |

## 1011 - Restore default parameters

- **DataType:** UNSIGNED32
- **ObjectCode:** Array
- **Description:** Restore default parameter values

The object 0x1011 has to be written with the value "load" (0x64616f6c) to trigger clearing, otherwise an error is reported.

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 4 | ro | 0 |
| 0x01 | Restore all default parameters | UNSIGNED32 | - | rw | 0 |
| 0x02 | Restore communication default parameters | UNSIGNED32 | - | rw | 0 |
| 0x03 | Restore application default parameters | UNSIGNED32 | - | rw | 0 |
| 0x04 | Restore manufacturer default parameters | UNSIGNED32 | - | rw | 0 |

## 1014 - COB ID EMCY

- **DataType:** UNSIGNED32
- **ObjectCode:** Variable
- **Description:** Emergency message COB-ID

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | COB ID EMCY | UNSIGNED32 | $NODEID+0x80 | ro | 0 |

## 1015 - Inhibit Time Emergency

- **DataType:** UNSIGNED16
- **ObjectCode:** Variable
- **Description:** Emergency message inhibit time

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Inhibit Time Emergency | UNSIGNED16 | 0x0 | rw | 0 |

## 1017 - Producer Heartbeat Time

- **DataType:** UNSIGNED16
- **ObjectCode:** Variable
- **Description:** Heartbeat message transmission period

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Producer Heartbeat Time | UNSIGNED16 | 0 | rw | 0 |

## 1018 - Identity Object

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Device identification information

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Number of entries | UNSIGNED8 | 4 | ro | 0 |
| 0x01 | Vendor Id | UNSIGNED32 | 0x5b8 | ro | 0 |
| 0x02 | Product Code | UNSIGNED32 | 0xc7 | ro | 0 |
| 0x03 | Revision number | UNSIGNED32 | 0x1 | ro | 0 |
| 0x04 | Serial number | UNSIGNED32 | - | ro | 0 |

## 1019 - Synchronous counter overflow value

- **DataType:** UNSIGNED8
- **ObjectCode:** Variable
- **Description:** SYNC counter overflow limit

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Synchronous counter overflow value | UNSIGNED8 | 0x00 | rw | 0 |

## 1020 - Verify configuration

- **DataType:** UNSIGNED32
- **ObjectCode:** Array
- **Description:** Configuration verification timestamps

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 2 | ro | 0 |
| 0x01 | Configuration date | UNSIGNED32 | - | rw | 0 |
| 0x02 | Configuration time | UNSIGNED32 | - | rw | 0 |

## 1021 - Store EDS

- **DataType:** DOMAIN
- **ObjectCode:** Variable
- **Description:** Electronic Data Sheet storage

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Store EDS | DOMAIN | - | rw | 0 |

## 1022 - Store format

- **DataType:** UNSIGNED8
- **ObjectCode:** Variable
- **Description:** Storage format identifier

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Store format | UNSIGNED8 | 0 | ro | 0 |

## 1029 - Error behaviour

- **DataType:** UNSIGNED8
- **ObjectCode:** Array
- **Description:** Error handling behavior configuration

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Nr of Error Classes | UNSIGNED8 | 2 | ro | 0 |
| 0x01 | Communication Error | UNSIGNED8 | 1 | rw | 0 |
| 0x02 | Specific Error Class | UNSIGNED8 | 0 | rw | 0 |

## 1030 - Version information

- **DataType:** UNSIGNED32
- **ObjectCode:** Array
- **Description:** CiA document implementation list

This data object shall list all implemented CiA documents.

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 2 | ro | 0 |
| 0x01 | Version information 1 | UNSIGNED32 | - | ro | 0 |
| 0x02 | Version information 2 | UNSIGNED32 | - | ro | 0 |

## 1032 - Active error list

- **DataType:** UNSIGNED32
- **ObjectCode:** Array
- **Description:** Currently active error events

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 4 | ro | 0 |
| 0x01 | Error Event 1 | UNSIGNED32 | - | ro | 0 |
| 0x02 | Error Event 2 | UNSIGNED32 | - | ro | 0 |
| 0x03 | Error Event 3 | UNSIGNED32 | - | ro | 0 |
| 0x04 | Error Event 4 | UNSIGNED32 | - | ro | 0 |

## 1200 - SDO server parameter

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** SDO server communication parameters

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 2 | ro | 0 |
| 0x01 | COB-ID client to server | UNSIGNED32 | $NODEID+0x600 | ro | 0 |
| 0x02 | COB-ID server to client | UNSIGNED32 | $NODEID+0x580 | ro | 0 |

## 1400 - Receive PDO Communication Parameter

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Receive PDO 1 communication parameters

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Number of entries | UNSIGNED8 | 2 | ro | 0 |
| 0x01 | COB ID | UNSIGNED32 | $NODEID+0x200 | rw | 0 |
| 0x02 | Transmission Type | UNSIGNED8 | 255 | rw | 0 |

## 1600 - Receive PDO Mapping Parameter

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Receive PDO 1 mapping parameters

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Number of entries | UNSIGNED8 | 2 | rw | 0 |
| 0x01 | Mapping Entry 1 - Controlword | UNSIGNED32 | 0x60400010 | rw | 0 |
| 0x02 | Mapping Entry 2 - Target velocity (vl) | UNSIGNED32 | 0x60420010 | rw | 0 |
| 0x03 | Mapping Entry 3 - Mode of Operation | UNSIGNED32 | 0x60600008 | rw | 0 |

## 1800 - Transmit PDO Communication Parameter

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Transmit PDO 1 communication parameters

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Number of entries | UNSIGNED8 | 5 | ro | 0 |
| 0x01 | COB ID | UNSIGNED32 | $NODEID+0x180 | rw | 0 |
| 0x02 | Transmission Type | UNSIGNED8 | 255 | rw | 0 |
| 0x03 | Inhibit Time | UNSIGNED16 | 0x0000 | rw | 0 |
| 0x04 | Compatibility Entry | UNSIGNED8 | - | rw | 0 |
| 0x05 | Event Timer | UNSIGNED16 | 0 | rw | 0 |

## 1a00 - Transmit PDO Mapping Parameter

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Transmit PDO 1 mapping parameters

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Number of entries | UNSIGNED8 | 2 | rw | 0 |
| 0x01 | Mapping Entry 1 - Statusword | UNSIGNED32 | 0x60410010 | rw | 0 |
| 0x02 | Mapping Entry 2 - Actual velocity (vl) | UNSIGNED32 | 0x60440010 | rw | 0 |
| 0x03 | Mapping Entry 3 - Modes of Operation Display | UNSIGNED32 | 0x60610008 | rw | 0 |

## 1f50 - Download Program Data

- **DataType:** DOMAIN
- **ObjectCode:** Array
- **Description:** Programming data download

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Number of entries | UNSIGNED8 | 2 | ro | 0 |
| 0x01 | Program Area | DOMAIN | - | rw | 0 |
| 0x02 | CANopen Configuration | DOMAIN | - | rw | 0 |

**Sub-index Details:** <br>
- **0x01 - Program Area:** Modified X2C application binary <br>
- **0x02 - CANopen Configuration:** Basic CANopen communication configuration stored in non-volatile memory <br>
  - Byte 0: FD mode (Flag for CANopen FD or classic mode at startup) <br>
  - Byte 1: Node-ID (1..127) <br>
  - Byte 2: Low byte of bitrate in kbps <br>
  - Byte 3: High byte of bitrate in kbps <br>

## 1f51 - Program Control

- **DataType:** UNSIGNED8
- **ObjectCode:** Array
- **Description:** Application program control

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Number of entries | UNSIGNED8 | 1 | ro | 0 |
| 0x01 | Program Control | UNSIGNED8 | - | rw | 0 |

**Control Values:** <br>
- **0:** Stop application <br>
- **1:** Start application <br>
- **2:** Erase non-volatile memory (factory reset), optional <br>
- **3:** Clear application (required state for device becoming programmable) <br>

## 1f57 - Flash Status Identification

- **DataType:** UNSIGNED32
- **ObjectCode:** Array
- **Description:** Application flash status

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Number of entries | UNSIGNED8 | 1 | ro | 0 |
| 0x01 | Flash status identification | UNSIGNED32 | - | ro | 0 |

**Status Values:** <br>
- **0:** Valid application <br>
- **2:** Invalid application

## 2000 - Hardware Parameter

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Hardware configuration parameters

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 4 | ro | 0 |
| 0x01 | Rshunt | REAL32 | 200e-6 | rw | 0 |
| 0x02 | GainCSA | INTEGER16 | 20 | rw | 0 |
| 0x03 | IdentCurrent | REAL32 | 5 | rw | 0 |
| 0x04 | Enable CAN Termination | UNSIGNED8 | 0 | rw | 0 |

**Parameter Details:**
- **Rshunt:** Shunt resistor value [Ohm]

## 2001 - Scaling Parameter

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Input scaling parameters

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 3 | ro | 0 |
| 0x01 | SpeedLimitAiDi | REAL32 | 3000 | rw | 0 |
| 0x02 | AinVoltageForMaxSpeed | REAL32 | 5 | rw | 0 |
| 0x03 | AinMinVoltageThreshold | REAL32 | 0.5 | rw | 0 |

**Parameter Details:** <br>
- **SpeedLimitAiDi:** Speed scaling for analog & digital input [rpm] <br>
- **AinVoltageForMaxSpeed:** Voltage scaling for analog input [V] <br>
- **AinMinVoltageThreshold:** Deadband of Ain voltage in V. Voltages below this value are ignored by the controller. <br>

## 2010 - Motor Parameter

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Motor configuration parameters

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 4 | ro | 0 |
| 0x01 | PolePairs | INTEGER16 | 5 | rw | 0 |
| 0x02 | Bemf | REAL32 | 0.0 | rw | 0 |
| 0x03 | RatedSpeed | REAL32 | 4000.0 | rw | 0 |
| 0x04 | InvertDirection | UNSIGNED8 | 0 | rw | 0 |

## 2011 - Brake Parameter

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Brake control parameters

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 5 | ro | 0 |
| 0x01 | Mode | INTEGER16 | 0 | rw | 0 |
| 0x02 | PeakDuty | REAL32 | 1.0 | rw | 0 |
| 0x03 | HoldDuty | REAL32 | 0.7 | rw | 0 |
| 0x04 | PeakTime | REAL32 | 1.0 | rw | 0 |
| 0x05 | BrakeThresholdCurrent | REAL32 | 0.24 | rw | 0 |

## 2012 - Angular Sensor Parameter

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Angular sensor configuration

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 5 | ro | 0 |
| 0x01 | SensorType | INTEGER16 | 2 | rw | 0 |
| 0x02 | InvertSensor | UNSIGNED8 | 1 | rw | 0 |
| 0x03 | AngleOffset | REAL32 | 0.0 | rw | 0 |
| 0x04 | AngleCompensation | REAL32 | 1.15 | rw | 0 |
| 0x05 | Phi2SpeedFc | REAL32 | 200.0 | rw | 0 |

## 2013 - Encoder Sensor

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Encoder sensor parameters

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 3 | ro | 0 |
| 0x01 | Resolution | INTEGER16 | 256 | rw | 0 |
| 0x02 | UsePwm | UNSIGNED8 | 1 | rw | 0 |
| 0x03 | PwmFrequency | REAL32 | 1000 | rw | 0 |

## 2014 - Hall Sensor

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Hall sensor configuration

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 5 | ro | 0 |
| 0x01 | nInterpol | REAL32 | 100 | rw | 0 |
| 0x02 | nSync | REAL32 | 5000 | rw | 0 |
| 0x03 | Kp | REAL32 | 1 | rw | 0 |
| 0x04 | Ki | REAL32 | 10 | rw | 0 |
| 0x05 | HallMapping | INTEGER8 | 0 | rw | 0 |

**Hall Mapping Values:** <br>
Assign physical hall signals to control inputs. Active when Block commutation is used! <br>
- **0:** Hall mapping is ABC→ABC <br>
- **1:** Hall mapping is ABC→CAB <br>
- **2:** Hall mapping is ABC→BCA <br>
- **3:** Hall mapping is ABC→CBA <br>
- **4:** Hall mapping is ABC→BAC <br>
- **5:** Hall mapping is ABC→ACB <br>
- **6:** Hall mapping is ABC→inverted(ABC) <br>
- **7:** Hall mapping is ABC→inverted(CAB) <br>
- **8:** Hall mapping is ABC→inverted(BCA) <br>
- **9:** Hall mapping is ABC→inverted(CBA) <br>
- **10:** Hall mapping is ABC→inverted(BAC) <br>
- **11:** Hall mapping is ABC→inverted(ACB) <br>

## 2015 - Sin/Cos Sensor

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Sin/Cos sensor configuration

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 7 | ro | 0 |
| 0x01 | SensorSetup | UNSIGNED8 | 1 | rw | 0 |
| 0x02 | SC_P | INTEGER16 | 1551 | rw | 0 |
| 0x03 | SC_N | INTEGER16 | 1551 | rw | 0 |
| 0x04 | OffsetSin | INTEGER16 | 1 | rw | 0 |
| 0x05 | OffsetCos | INTEGER16 | 1 | rw | 0 |
| 0x06 | GainSin | REAL32 | 0.0002442 | rw | 0 |
| 0x07 | GainCos | REAL32 | 0.0002442 | rw | 0 |

## 2016 - Temperature Sensor

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Temperature sensor readings

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 2 | ro | 0 |
| 0x01 | Motor Temperature | REAL32 | 0 | rw | 0 |
| 0x02 | PCB Temperature | REAL32 | 0 | rw | 0 |

## 2017 - STO Status

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Safe Torque Off (STO) status monitoring

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 5 | ro | 0 |
| 0x01 | STO1 Monitor 12V | REAL32 | 0 | rw | 0 |
| 0x02 | STO1 Monitor 48V | REAL32 | 0 | rw | 0 |
| 0x03 | STO2 Monitor | REAL32 | 0 | rw | 0 |
| 0x04 | STO1 Input | UNSIGNED8 | 0 | rw | 0 |
| 0x05 | STO2 Input | UNSIGNED8 | 0 | rw | 0 |

## 2020 - Voltage Limits

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** DC link voltage limits

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 2 | ro | 0 |
| 0x01 | DcLinkOv | REAL32 | 57.6 | rw | 0 |
| 0x02 | DcLinkUv | REAL32 | 18 | rw | 0 |

## 2021 - Current Limits

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Current protection limits

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 5 | ro | 0 |
| 0x01 | OcFast | REAL32 | 150 | rw | 0 |
| 0x02 | OcSlow | REAL32 | 120 | rw | 0 |
| 0x03 | OcFastTime | REAL32 | 0.002 | rw | 0 |
| 0x04 | OcSlowTime | REAL32 | 0.1 | rw | 0 |
| 0x05 | MotorControlCurrentLimit | REAL32 | 10 | rw | 0 |

## 2022 - Temperature Limits

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Temperature protection limits

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 3 | ro | 0 |
| 0x01 | EnMotorTempError | UNSIGNED8 | 0 | rw | 0 |
| 0x02 | MotorTempMax | REAL32 | 80.0 | rw | 0 |
| 0x03 | PcbTempMax | REAL32 | 80 | rw | 0 |

**Parameter Details:**
- **MotorTempMax:** Motor over temperature limit in °C

## 2023 - Control Error Limits

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Control loop error limits

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 4 | ro | 0 |
| 0x01 | AllowedSpeedError | REAL32 | 200 | rw | 0 |
| 0x02 | AllowedSpeedErrorTime | REAL32 | 1 | rw | 0 |
| 0x03 | AllowedPositionError | REAL32 | 1 | rw | 0 |
| 0x04 | AllowedPositionErrorTime | REAL32 | 1 | rw | 0 |

## 2024 - I2t

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** I²t current monitoring parameters

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 3 | ro | 0 |
| 0x01 | NominalCurrent | REAL32 | 40 | rw | 0 |
| 0x02 | PeakCurrent | REAL32 | 100 | rw | 0 |
| 0x03 | PeakCurrentTime | REAL32 | 1 | rw | 0 |

## 2030 - Current Controller

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Current controller parameters

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 4 | ro | 0 |
| 0x01 | Kp_d | REAL32 | 0.07 | rw | 0 |
| 0x02 | Ki_d | REAL32 | 100 | rw | 0 |
| 0x03 | Kp_q | REAL32 | 0.07 | rw | 0 |
| 0x04 | Ki_q | REAL32 | 100 | rw | 0 |

## 2031 - Speed Controller

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Speed controller parameters

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 4 | ro | 0 |
| 0x01 | Kp | REAL32 | 0.005 | rw | 0 |
| 0x02 | Ki | REAL32 | 0.05 | rw | 0 |
| 0x03 | Kd | REAL32 | 0 | rw | 0 |
| 0x04 | Fc | REAL32 | 100 | rw | 0 |

## 2032 - Position Controller

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Position controller parameters

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 4 | ro | 0 |
| 0x01 | Kp | REAL32 | 100 | rw | 0 |
| 0x02 | Ki | REAL32 | 100 | rw | 0 |
| 0x03 | Kd | REAL32 | 0.5 | rw | 0 |
| 0x04 | Fc | REAL32 | 200 | rw | 0 |

## 2033 - Homing

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Homing procedure parameters

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 6 | ro | 0 |
| 0x01 | SpeedSwitch | REAL32 | 300 | rw | 0 |
| 0x02 | SpeedZero | REAL32 | 150 | rw | 0 |
| 0x03 | SpeedThreshold | REAL32 | 20 | rw | 0 |
| 0x04 | CurrentThreshold | REAL32 | 3 | rw | 0 |
| 0x05 | Timeout | UNSIGNED16 | 0 | rw | 0 |
| 0x06 | TorqueThreshold | UNSIGNED16 | 0 | rw | 0 |

## 2040 - Control Settings

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** General control configuration

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 6 | ro | 0 |
| 0x01 | DisableControlAtQsp | UNSIGNED8 | 1 | rw | 0 |
| 0x02 | DisableControlAtQspDelayTime | REAL32 | 0 | rw | 0 |
| 0x03 | DisableControlSpeedThres | REAL32 | 50 | rw | 0 |
| 0x04 | ShortMotorWhenPwmOff | UNSIGNED8 | 1 | rw | 0 |
| 0x05 | PreChargeMapping | INTEGER8 | 4 | rw | 0 |
| 0x06 | ControlMode | INTEGER8 | 0 | rw | 0 |

**Parameter Values:** <br>
- **PreChargeMapping:** <br>
  - 0: derive from FIState <br>
  - 1: DI1 is used as reference <br>
  - 2: DI2 is used as reference <br>
  - 3: DI3 is used as reference <br>
  - 4: DI4 is used as reference <br>
  - 5: DI5 is used as reference <br>
- **ControlMode:** <br>
  - 0: Sine commutation <br>
  - 1: Block commutation <br>

## 2041 - Speed Trajectory

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Speed trajectory generation parameters

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 7 | ro | 0 |
| 0x01 | acc_delta_speed | REAL32 | 1500 | rw | 0 |
| 0x02 | acc_delta_time | REAL32 | 1 | rw | 0 |
| 0x03 | dec_delta_speed | REAL32 | 10000 | rw | 0 |
| 0x04 | dec_delta_time | REAL32 | 1 | rw | 0 |
| 0x05 | JerkMax | REAL32 | 15000 | rw | 0 |
| 0x06 | Upper Limit Dead Zone | REAL32 | 0 | rw | 0 |
| 0x07 | Lower Limit Dead Zone | REAL32 | 0 | rw | 0 |

## 2042 - Position Trajectory

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Position trajectory generation parameters

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 2 | ro | 0 |
| 0x01 | Upper Limit Dead Zone | REAL32 | 0 | rw | 0 |
| 0x02 | Lower Limit Dead Zone | REAL32 | 0 | rw | 0 |

## 2043 - Input Functions

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Digital input function assignments

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 12 | ro | 0 |
| 0x01 | Function DI1 | INTEGER8 | 0 | rw | 0 |
| 0x02 | Function DI2 | INTEGER8 | 0 | rw | 0 |
| 0x03 | Function DI3 | INTEGER8 | 0 | rw | 0 |
| 0x04 | Function DI4 | INTEGER8 | 0 | rw | 0 |
| 0x05 | Function DI5 | INTEGER8 | 0 | rw | 0 |
| 0x06 | Function DI6 | INTEGER8 | 0 | rw | 0 |
| 0x07 | Polarity DI1 | INTEGER8 | 0 | rw | 0 |
| 0x08 | Polarity DI2 | INTEGER8 | 0 | rw | 0 |
| 0x09 | Polarity DI3 | INTEGER8 | 0 | rw | 0 |
| 0x0a | Polarity DI4 | INTEGER8 | 0 | rw | 0 |
| 0x0b | Polarity DI5 | INTEGER8 | 0 | rw | 0 |
| 0x0c | Polarity DI6 | INTEGER8 | 0 | rw | 0 |

## 2044 - Speed Select Table

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Predefined speed values for selection

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 16 | ro | 0 |
| 0x01 | Speed Select 1 | INTEGER16 | 0 | rw | 0 |
| 0x02 | Speed Select 2 | INTEGER16 | 0 | rw | 0 |
| 0x03 | Speed Select 3 | INTEGER16 | 0 | rw | 0 |
| 0x04 | Speed Select 4 | INTEGER16 | 0 | rw | 0 |
| 0x05 | Speed Select 5 | INTEGER16 | 0 | rw | 0 |
| 0x06 | Speed Select 6 | INTEGER16 | 0 | rw | 0 |
| 0x07 | Speed Select 7 | INTEGER16 | 0 | rw | 0 |
| 0x08 | Speed Select 8 | INTEGER16 | 0 | rw | 0 |
| 0x09 | Speed Select 9 | INTEGER16 | 0 | rw | 0 |
| 0x0a | Speed Select 10 | INTEGER16 | 0 | rw | 0 |
| 0x0b | Speed Select 11 | INTEGER16 | 0 | rw | 0 |
| 0x0c | Speed Select 12 | INTEGER16 | 0 | rw | 0 |
| 0x0d | Speed Select 13 | INTEGER16 | 0 | rw | 0 |
| 0x0e | Speed Select 14 | INTEGER16 | 0 | rw | 0 |
| 0x0f | Speed Select 15 | INTEGER16 | 0 | rw | 0 |
| 0x10 | Speed Select 16 | INTEGER16 | 0 | rw | 0 |

## 2045 - Position Select Table

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Predefined position values for selection

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 16 | ro | 0 |
| 0x01 | Position Select 1 | REAL32 | 0 | rw | 0 |
| 0x02 | Position Select 2 | REAL32 | 0 | rw | 0 |
| 0x03 | Position Select 3 | REAL32 | 0 | rw | 0 |
| 0x04 | Position Select 4 | REAL32 | 0 | rw | 0 |
| 0x05 | Position Select 5 | REAL32 | 0 | rw | 0 |
| 0x06 | Position Select 6 | REAL32 | 0 | rw | 0 |
| 0x07 | Position Select 7 | REAL32 | 0 | rw | 0 |
| 0x08 | Position Select 8 | REAL32 | 0 | rw | 0 |
| 0x09 | Position Select 9 | REAL32 | 0 | rw | 0 |
| 0x0a | Position Select 10 | REAL32 | 0 | rw | 0 |
| 0x0b | Position Select 11 | REAL32 | 0 | rw | 0 |
| 0x0c | Position Select 12 | REAL32 | 0 | rw | 0 |
| 0x0d | Position Select 13 | REAL32 | 0 | rw | 0 |
| 0x0e | Position Select 14 | REAL32 | 0 | rw | 0 |
| 0x0f | Position Select 15 | REAL32 | 0 | rw | 0 |
| 0x10 | Position Select 16 | REAL32 | 0 | rw | 0 |

## 2046 - Internal Status

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Device internal status information

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 18 | ro | 0 |
| 0x01 | Total On Time | UNSIGNED32 | 0 | ro | 0 |
| 0x02 | Total Errors Occurred | UNSIGNED32 | 0 | ro | 0 |
| 0x03 | Error ID 1 | UNSIGNED32 | 0 | ro | 0 |
| 0x04 | Error Time 1 | UNSIGNED32 | 0 | ro | 0 |
| 0x05 | Error ID 2 | UNSIGNED32 | 0 | ro | 0 |
| 0x06 | Error Time 2 | UNSIGNED32 | 0 | ro | 0 |
| 0x07 | Error ID 3 | UNSIGNED32 | 0 | ro | 0 |
| 0x08 | Error Time 3 | UNSIGNED32 | 0 | ro | 0 |
| 0x09 | Error ID 4 | UNSIGNED32 | 0 | ro | 0 |
| 0x0a | Error Time 4 | UNSIGNED32 | 0 | ro | 0 |
| 0x0b | Error ID 5 | UNSIGNED32 | 0 | ro | 0 |
| 0x0c | Error Time 5 | UNSIGNED32 | 0 | ro | 0 |
| 0x0d | Error ID 6 | UNSIGNED32 | 0 | ro | 0 |
| 0x0e | Error Time 6 | UNSIGNED32 | 0 | ro | 0 |
| 0x0f | Error ID 7 | UNSIGNED32 | 0 | ro | 0 |
| 0x10 | Error Time 7 | UNSIGNED32 | 0 | ro | 0 |
| 0x11 | Error ID 8 | UNSIGNED32 | 0 | ro | 0 |
| 0x12 | Error Time 8 | UNSIGNED32 | 0 | ro | 0 |

## 5000 - CANopen Configuration

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** CANopen communication configuration

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 1 | ro | 0 |
| 0x01 | FDMode | UNSIGNED8 | 0 | rw | 0 |

## 6040 - controlword

- **DataType:** UNSIGNED16
- **ObjectCode:** Variable
- **Description:** Drive control word (CiA 402)

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | controlword | UNSIGNED16 | - | rww | 1 |

## 6041 - statusword

- **DataType:** UNSIGNED16
- **ObjectCode:** Variable
- **Description:** Drive status word (CiA 402)

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | statusword | UNSIGNED16 | - | ro | 1 |

## 6042 - vl_target_velocity

- **DataType:** INTEGER16
- **ObjectCode:** Variable
- **Description:** Target velocity in velocity mode

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | vl_target_velocity | INTEGER16 | 0 | rww | 1 |

## 6043 - vl_velocity_demand

- **DataType:** INTEGER16
- **ObjectCode:** Variable
- **Description:** Velocity demand value

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | vl_velocity_demand | INTEGER16 | - | ro | 1 |

## 6044 - vl_velocity_actual_value

- **DataType:** INTEGER16
- **ObjectCode:** Variable
- **Description:** Actual velocity value

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | vl_velocity_actual_value | INTEGER16 | - | ro | 1 |

## 6046 - vl_velocity_min_max_amount

- **DataType:** UNSIGNED32
- **ObjectCode:** Array
- **Description:** Velocity limits for velocity mode

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 2 | const | 0 |
| 0x01 | vl_velocity_min_amount | UNSIGNED32 | 0 | rww | 1 |
| 0x02 | vl_velocity_max_amount | UNSIGNED32 | 32767 | rww | 1 |

## 6048 - vl_velocity_acceleration

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Velocity mode acceleration parameters

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 2 | const | 0 |
| 0x01 | delta_speed | UNSIGNED32 | - | rww | 1 |
| 0x02 | delta_time | UNSIGNED16 | - | rww | 1 |

## 6049 - vl_velocity_deceleration

- **DataType:** UNSIGNED8
- **ObjectCode:** Record
- **Description:** Velocity mode deceleration parameters

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 2 | const | 0 |
| 0x01 | delta_speed | UNSIGNED32 | - | rww | 1 |
| 0x02 | delta_time | UNSIGNED16 | - | rww | 1 |

## 6060 - modes_of_operation

- **DataType:** INTEGER8
- **ObjectCode:** Variable
- **Description:** Selected operation mode

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | modes_of_operation | INTEGER8 | - | rww | 1 |

## 6061 - modes_of_operation_display

- **DataType:** INTEGER8
- **ObjectCode:** Variable
- **Description:** Current operation mode display

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | modes_of_operation_display | INTEGER8 | - | ro | 1 |

## 6064 - position_actual_value

- **DataType:** INTEGER32
- **ObjectCode:** Variable
- **Description:** Actual position value

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | position_actual_value | INTEGER32 | - | ro | 1 |

## 6079 - dc_link_circuit_voltage

- **DataType:** UNSIGNED32
- **ObjectCode:** Variable
- **Description:** DC link circuit voltage

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | dc_link_circuit_voltage | UNSIGNED32 | 0 | ro | 1 |

## 607a - position_target_value

- **DataType:** INTEGER32
- **ObjectCode:** Variable
- **Description:** Target position value

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | position_target_value | INTEGER32 | 0 | rww | 1 |

## 607c - homing offset

- **DataType:** INTEGER32
- **ObjectCode:** Variable
- **Description:** Homing offset value

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | homing offset | INTEGER32 | 0 | rww | 1 |

## 607d - software position limit

- **DataType:** INTEGER32
- **ObjectCode:** Array
- **Description:** Software position limits

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 2 | const | 0 |
| 0x01 | min position | INTEGER32 | 0 | rww | 1 |
| 0x02 | max position | INTEGER32 | 0 | rww | 1 |

## 607f - max profile velocity

- **DataType:** UNSIGNED32
- **ObjectCode:** Variable
- **Description:** Maximum profile velocity

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | max profile velocity | UNSIGNED32 | 0 | rw | 0 |

## 6080 - max motor speed

- **DataType:** UNSIGNED32
- **ObjectCode:** Variable
- **Description:** Maximum motor speed

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | max motor speed | UNSIGNED32 | 0 | rw | 0 |

## 6081 - profile velocity

- **DataType:** UNSIGNED32
- **ObjectCode:** Variable
- **Description:** Profile velocity for position mode

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | profile velocity | UNSIGNED32 | 0 | rww | 1 |

## 6083 - profile acceleration

- **DataType:** UNSIGNED32
- **ObjectCode:** Variable
- **Description:** Profile acceleration

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | profile acceleration | UNSIGNED32 | 0 | rww | 1 |

## 6084 - profile deceleration

- **DataType:** UNSIGNED32
- **ObjectCode:** Variable
- **Description:** Profile deceleration

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | profile deceleration | UNSIGNED32 | 0 | rww | 1 |

## 6086 - profile type

- **DataType:** INTEGER16
- **ObjectCode:** Variable
- **Description:** Motion profile type

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | profile type | INTEGER16 | 0 | ro | 1 |

## 6093 - position factor

- **DataType:** UNSIGNED32
- **ObjectCode:** Array
- **Description:** Position scaling factors

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 2 | ro | 0 |
| 0x01 | numerator | UNSIGNED32 | 1 | rww | 1 |
| 0x02 | feed constant | UNSIGNED32 | 1 | rww | 1 |

## 6094 - velocity encoder factor

- **DataType:** UNSIGNED32
- **ObjectCode:** Array
- **Description:** Velocity encoder scaling factors

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 2 | ro | 0 |
| 0x01 | numerator | UNSIGNED32 | 1 | rww | 1 |
| 0x02 | divisor | UNSIGNED32 | 1 | rww | 1 |

## 6097 - acceleration factor

- **DataType:** UNSIGNED32
- **ObjectCode:** Array
- **Description:** Acceleration scaling factors

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 2 | ro | 0 |
| 0x01 | numerator | UNSIGNED32 | 1 | rww | 1 |
| 0x02 | divisor | UNSIGNED32 | 1 | rww | 1 |

## 6098 - homing method

- **DataType:** INTEGER8
- **ObjectCode:** Variable
- **Description:** Homing method selection

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | homing method | INTEGER8 | 0 | rww | 1 |

## 6099 - homing speed

- **DataType:** UNSIGNED32
- **ObjectCode:** Array
- **Description:** Homing speeds

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 2 | const | 0 |
| 0x01 | speed switch | UNSIGNED32 | 0 | ro | 1 |
| 0x02 | speed zero | UNSIGNED32 | 0 | ro | 1 |

## 609a - homing acceleration

- **DataType:** UNSIGNED32
- **ObjectCode:** Variable
- **Description:** Homing acceleration

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | homing acceleration | UNSIGNED32 | 0 | rww | 1 |

## 60c5 - max acceleration

- **DataType:** UNSIGNED32
- **ObjectCode:** Variable
- **Description:** Maximum acceleration

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | max acceleration | UNSIGNED32 | 0 | rw | 0 |

## 60c6 - max deceleration

- **DataType:** UNSIGNED32
- **ObjectCode:** Variable
- **Description:** Maximum deceleration

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | max deceleration | UNSIGNED32 | 0 | rw | 0 |

## 60e3 - supported homing methods

- **DataType:** INTEGER8
- **ObjectCode:** Array
- **Description:** List of supported homing methods

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | Highest sub-index supported | UNSIGNED8 | 9 | ro | 0 |
| 0x01 | 1st supported homing method | INTEGER8 | -3 | ro | 0 |
| 0x02 | 2nd supported homing method | INTEGER8 | -4 | ro | 0 |
| 0x03 | 3rd supported homing method | INTEGER8 | 17 | ro | 0 |
| 0x04 | 4th supported homing method | INTEGER8 | 18 | ro | 0 |
| 0x05 | 5th supported homing method | INTEGER8 | 19 | ro | 0 |
| 0x06 | 6th supported homing method | INTEGER8 | 20 | ro | 0 |
| 0x07 | 7th supported homing method | INTEGER8 | 21 | ro | 0 |
| 0x08 | 8th supported homing method | INTEGER8 | 22 | ro | 0 |
| 0x09 | 9th supported homing method | INTEGER8 | 37 | ro | 0 |

## 6502 - supported drive modes

- **DataType:** UNSIGNED32
- **ObjectCode:** Variable
- **Description:** Supported operation modes bit mask

| Sub-Index | Parameter | Data Type | Default Value | Access Type | PDO Mapping |
|-----------|-----------|-----------|---------------|-------------|-------------|
| 0x00 | supported drive modes | UNSIGNED32 | 0x23 | ro | 0 |

---

### Technical Support

For additional support beyond this documentation:

- **Website**: [www.q-drives.com](http://www.q-drives.com)
- **Contact**: technik@q-drives.com

---

### Version History
| Version | Date | Changes | Firmware Version |
|---------|------|---------|------------------|
| 0.1 | 15.11.2024 | Initial release | 2.01.6 |
| 1.1 | 11.08.2025 | Add Operation Modes | 2.01.6 |

---

**Document Information:** <br>
- **Firmware Compatibility**: 2.01.6 and later <br>
- **Standards**: CiA 301, CiA 402 compliant


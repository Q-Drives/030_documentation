# NMT Network Management

## Table of Contents
- [Introduction & Basic Concepts](#introduction--basic-concepts)
- [NMT States Explained](#nmt-states-explained)
- [State Transitions](#state-transitions)
- [Startup Process](#startup-process)
- [Error Handling & Troubleshooting](#error-handling--troubleshooting)
- [Practical Operational Guidance](#practical-operational-guidance)
- [Advanced Topics](#advanced-topics)

## Introduction & Basic Concepts

### What is NMT (Network Management)?

Network Management (NMT) is the core protocol in CANopen that controls the operational state of devices on the network. Think of it as the "traffic controller" that manages when devices can communicate and how they behave during startup, operation, and error conditions.

### Key Roles in CANopen Networks

**NMT Master**
- Controls the network startup sequence
- Manages state transitions for all devices
- Monitors device health and handles errors
- Only one NMT Master per network (normally)

**NMT Slave**
- Follows commands from the NMT Master
- Reports its status and responds to state change requests
- Can operate in different states based on master commands

**Self-Starting Devices**
- Special devices that can start automatically without master control
- Useful for simple networks or specific applications

### Network Communication Overview

CANopen networks operate on a master-slave principle where:
- The NMT Master coordinates all network activities
- Devices communicate using different protocols (SDO, PDO, NMT)
- State management ensures orderly startup and operation
- Error handling maintains network reliability

### Document Version Information

| Version | Date | Changes | Firmware Version |
|---------|------|---------|------------------|
| 0.1 | 15.11.2024 | Initial release | 2.01.6 |

---

## NMT States Explained

Every CANopen device operates in one of four main states. Understanding these states is crucial for troubleshooting and maintenance.

### 1. Initialisation State

**Purpose**: Device startup and hardware initialization

**What happens**: <br>
- Device powers up and performs self-tests <br>
- Basic hardware initialization occurs <br>
- Device prepares to enter Pre-operational state <br>
- Minimal communication capability <br>

**Typical duration**: 1-5 seconds

**Technician notes**: <br>
- If a device stays in this state too long, check power supply and hardware <br>
- Look for hardware faults or initialization failures

### 2. Pre-operational State

**Purpose**: Configuration and setup phase

**What happens**: <br>
- Device can receive SDO (Service Data Object) communications <br>
- Configuration parameters can be read/written <br>
- PDO (Process Data Object) communication is **disabled** <br>
- Device waits for Start Remote Node command <br>

**Communication allowed**: <br>
- ✅ SDO (configuration data) <br>
- ✅ NMT commands <br>
- ✅ Emergency messages <br>
- ❌ PDO (process data) <br>

**Technician notes**: <br>
- This is the "setup" state - configure parameters here <br>
- Device won't send/receive process data until moved to Operational <br>
- Check configuration if device won't transition to Operational <br>

### 3. Operational State

**Purpose**: Normal operation and process data exchange

**What happens**: <br>
- Full communication capability active <br>
- PDO communication enabled for real-time data exchange <br>
- Device performs its intended function <br>
- SDO communication still available for monitoring/adjustment <br>

**Communication allowed**: <br>
- ✅ SDO (configuration data) <br>
- ✅ PDO (process data) <br>
- ✅ NMT commands <br>
- ✅ Emergency messages <br>

**Technician notes**: <br>
- This is normal operating state for production <br>
- Monitor PDO communication for process data flow <br>
- Device should remain in this state during normal operation <br>

### 4. Stopped State

**Purpose**: Error condition or intentional shutdown

**What happens**: <br>
- PDO communication disabled <br>
- Limited SDO communication (emergency access only) <br>
- Device stops performing its function <br>
- Used for error conditions or maintenance <br>

**Communication allowed**: <br>         
- ✅ NMT commands <br>
- ✅ Emergency messages <br>
- ⚠️ Limited SDO (emergency only) <br>
- ❌ PDO (process data) <br>

**Technician notes**: <br>
- Device is non-functional for process data <br>
- Investigate why device entered this state <br>
- May require reset or error clearing to recover <br>

## State Transitions

Understanding how devices move between states helps with troubleshooting and control.

### Valid State Transitions

```
Initialisation → Pre-operational (automatic at startup)
Pre-operational → Operational   (Start Remote Node command)  
Pre-operational → Stopped       (Stop Remote Node command)
Operational → Pre-operational   (Enter Pre-operational command)
Operational → Stopped          (Stop Remote Node command)
Stopped → Pre-operational      (Reset Communication command)
Any State → Initialisation     (Reset Node command)
```

### Transition Commands

| Command | From State | To State | Purpose |
|---------|------------|----------|---------|
| Start Remote Node | Pre-operational | Operational | Begin normal operation |
| Stop Remote Node | Pre-operational/Operational | Stopped | Emergency stop or maintenance |
| Enter Pre-operational | Operational | Pre-operational | Return to configuration mode |
| Reset Communication | Stopped | Pre-operational | Restart communication |
| Reset Node | Any | Initialisation | Complete device restart |

### Automatic Transitions

Some transitions happen automatically:
- **Power-up**: Device automatically enters Initialisation, then Pre-operational
- **Error conditions**: Device may automatically enter Stopped state
- **Bootup message**: Sent when entering Pre-operational from Initialisation

## Startup Process

The network startup follows a specific sequence to ensure all devices are properly configured and operational.

### Master Startup Sequence

1. **Power-On and Initialization**
   - NMT Master completes its own initialization
   - Checks its configuration for network startup behavior

2. **Flying Master Negotiation** (if enabled)
   - Multiple master-capable devices negotiate who becomes the active master
   - Highest priority device becomes the NMT Master
   - Other devices become slaves

3. **Network Reset** (optional)
   - Master may send Reset Communication to all devices
   - Forces all devices to restart their communication

4. **Slave Boot Process**
   - Master initiates boot process for each configured slave
   - Verifies device identity and configuration
   - Handles mandatory vs. optional devices differently

5. **Configuration Check**
   - Master verifies each device's configuration
   - May download new configuration if needed
   - Ensures all devices have correct parameters

6. **Error Control Setup**
   - Master configures heartbeat or node guarding
   - Establishes monitoring for device health
   - Sets up error detection mechanisms

7. **Transition to Operational**
   - Master commands devices to enter Operational state
   - Can start all devices simultaneously or individually
   - Network becomes fully operational

### Slave Boot Process

For each slave device, the master performs:

1. **Device Verification**
   - Checks if device is present on network
   - Verifies device type matches expected configuration
   - Confirms vendor ID, product code, and serial number

2. **Configuration Management**
   - Compares current configuration with expected values
   - Downloads new configuration if needed
   - Performs restore to defaults if required

3. **Software Version Check** (optional)
   - Verifies application software version
   - Can trigger automatic software updates
   - Ensures all devices run compatible software

4. **Error Control Activation**
   - Sets up heartbeat monitoring or node guarding
   - Establishes communication monitoring
   - Prepares error detection mechanisms

### Startup Timing

- **Boot timeout**: Default varies, typically 10-30 seconds for mandatory devices
- **Heartbeat setup**: Usually 1-5 seconds after configuration
- **Full startup**: Can take 30 seconds to several minutes depending on network size

## Error Handling & Troubleshooting

### Common Error Status Codes

When startup or operation fails, the system generates specific error codes:

| Code | Description | Likely Cause | Action Required |
|------|-------------|--------------|-----------------|
| A | Device not listed in slave assignment | Configuration error | Check network configuration |
| B | No response to device type request | Device offline/faulty | Check device power and connection |
| C | Wrong device type | Incorrect device installed | Verify correct device model |
| D | Wrong vendor ID | Incorrect device installed | Check device manufacturer |
| E | Heartbeat timeout | Communication failure | Check network cables and device status |
| F | Node guarding timeout | Communication failure | Verify device operation and network |
| G | Configuration objects missing | Configuration incomplete | Check device configuration |
| H | Software update required but not allowed | Version mismatch | Update software or configuration |
| I | Software update failed | Download/installation problem | Retry update or check device |
| J | Configuration download failed | Parameter error | Verify configuration parameters |
| K | Heartbeat failure during startup | Communication problem | Check network integrity |
| L | Device was initially operational | Keep-alive conflict | Check startup configuration |
| M | Wrong product code | Incorrect device model | Verify device part number |
| N | Wrong revision number | Software version mismatch | Update device software |
| O | Wrong serial number | Device replacement needed | Check device identity |

### Troubleshooting Flowchart

**Device Not Starting:** <br>
1. Check power supply and connections <br>
2. Verify device is configured in master's slave list <br>
3. Check network termination and cables <br>
4. Monitor for bootup messages <br>
5. Review error codes in master diagnostics <br>
 
**Communication Problems:** <br>
1. Verify baud rate settings match across network <br>
2. Check CAN bus termination (120Ω at each end) <br>
3. Measure bus voltage levels <br>
4. Look for bus conflicts or duplicate node IDs <br>
5. Monitor heartbeat/node guarding status <br>

**Configuration Issues:** <br>
1. Compare actual vs. expected device parameters <br>
2. Check configuration file for errors <br>
3. Verify software versions are compatible <br>
4. Review restore-to-defaults settings <br>
5. Validate device identity parameters <br>

## Practical Operational Guidance

### Monitoring Device States

**Visual Indicators:**
- Most devices have status LEDs indicating current state
- Green = Operational, Red = Error, Yellow = Pre-operational
- Flashing patterns may indicate specific conditions

**Software Monitoring:** <br>
- Use CANopen configuration tools to monitor states <br>
- Check master diagnostics for device status <br>
- Monitor heartbeat/node guarding for device health <br>

**Network Analysis:** <br>
- CAN bus analyzers show message traffic <br>
- Monitor bootup messages during startup <br>
- Track state transition commands and responses <br>

### Normal vs. Abnormal Behavior

**Normal Startup:** <br>
- All devices boot within expected timeframe <br>
- Configuration verification passes <br>
- Devices transition to Operational state <br>
- Process data flows correctly <br>

**Abnormal Conditions:** <br>
- Extended startup times <br>
- Devices stuck in Pre-operational <br>
- Repeated error messages <br>
- Missing heartbeat signals <br>
- Unexpected state transitions <br>

### Maintenance Procedures

**Planned Maintenance:** <br>
1. Command devices to Pre-operational state <br>
2. Perform required maintenance tasks <br>
3. Verify device operation <br>
4. Return devices to Operational state <br>

**Device Replacement:** <br>
1. Stop affected device or network section <br>
2. Replace device with identical model/configuration <br>
3. Verify device identity parameters <br>
4. Allow normal startup sequence <br>
5. Confirm proper operation <br>

**Configuration Changes:**
1. Move device to Pre-operational state <br>
2. Modify parameters using SDO communication <br>
3. Verify changes are accepted <br>
4. Return to Operational state <br>
5. Test functionality <br>

---

**Document Information:**
- **Version**: 1.1 
- **Last Updated**: 11.08.2025
- **Firmware Compatibility**: 2.01.6 and later
- **Standards**: CiA 301, CiA 402 compliant
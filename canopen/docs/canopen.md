![](logo-horizontal.jpg)
# CANopen Protocol Implementation

## Table of Contents
- [Introduction & Overview](#introduction--overview)
  - [What is CANopen?](#what-is-canopen)
  - [Q-Drives C7 Implementation](#q-drives-c7-implementation)
  - [Standards Compliance](#standards-compliance)
  - [Document Version Information](#document-version-information)
- [Physical Layer & Network Setup](#physical-layer--network-setup)
  - [CAN Bus Topology](#can-bus-topology)
  - [Network Termination](#network-termination)
  - [Bus Length Limitations](#bus-length-limitations)
  - [Stub Lines (Drop Lines)](#stub-lines-drop-lines)
  - [Multiport Taps](#multiport-taps)
  - [Cable Requirements](#cable-requirements)
- [CANopen Communication Model](#canopen-communication-model)
  - [Device Model Overview](#device-model-overview)
  - [Object Dictionary Structure](#object-dictionary-structure)
  - [Communication Types](#communication-types)
  - [Transmission Types](#transmission-types)
- [CANopen Objects & Services](#canopen-objects--services)
  - [Network Management (NMT)](#network-management-nmt)
  - [Service Data Objects (SDO)](#service-data-objects-sdo)
  - [Process Data Objects (PDO)](#process-data-objects-pdo)
  - [Synchronization Object (SYNC)](#synchronization-object-sync)
  - [Time Stamp Object (TIME)](#time-stamp-object-time)
  - [Emergency Object (EMCY)](#emergency-object-emcy)
- [Configuration & Setup](#configuration--setup)
  - [Initial Configuration](#initial-configuration)
  - [Layer Setting Services (LSS)](#layer-setting-services-lss)
  - [CANopen FD vs Classic Mode](#canopen-fd-vs-classic-mode)
  - [Configuration Storage](#configuration-storage)
- [Technical Specifications](#technical-specifications)
  - [Bus Length vs Baud Rate](#bus-length-vs-baud-rate)
  - [Stub Line Specifications](#stub-line-specifications)
  - [Multiport Tap Specifications](#multiport-tap-specifications)

## Introduction & Overview

### What is CANopen?

CANopen is a widely adopted communication protocol based on the CAN (Controller Area Network) bus system, extensively used in industrial automation applications. It provides standardized communication methods for devices in manufacturing, automotive, and various other industrial environments.

**Key Characteristics:** <br>
- **Standardized Protocol**: Developed by CAN in Automation (CiA) organization <br>
- **Multi-Master Capability**: Supports multiple masters on the same network <br>
- **Real-Time Communication**: Deterministic data exchange for time-critical applications <br>
- **Robust Design**: Differential signaling provides excellent EMI resistance <br>
- **Scalable Architecture**: Supports networks from simple point-to-point to complex multi-node systems

### Q-Drives C7 Implementation

The Q-Drives C7 controller implements CANopen according to industry standards, providing seamless integration with existing industrial automation systems.

**Implementation Features:** <br>
- **Full CiA 301 Compliance**: Complete application layer and communication profile <br>
- **CiA 402 Device Profile**: Specialized for drives and motion control applications <br>
- **Flexible Configuration**: Supports both CANopen Classic and CANopen FD modes <br>
- **Comprehensive Object Dictionary**: Over 100 standardized and manufacturer-specific objects <br>
- **Multiple PDO Support**: Up to 8 independent PDO mappings for efficient data exchange <br>

### Standards Compliance

The C7 controller CANopen implementation adheres to the following international standards:

| Standard | Description | Implementation Level |
|----------|-------------|---------------------|
| **CiA 301** | CANopen application layer and communication profile | Full compliance |
| **CiA 402** | CANopen device profile for drives and motion control | Complete implementation |
| **ISO 11898** | CAN physical layer specification | Hardware compliant |
| **EN 50325-4** | Industrial communication - CANopen | Certified compatible |

---

## Physical Layer & Network Setup

### CAN Bus Topology

CAN operates as a 2-wire bus system where all participants are connected in parallel. The bus uses differential signaling to achieve excellent noise immunity in industrial environments.

#### Network Architecture

```
node 1    node 2    ...    node n
  |         |               |
  |---------|---------------|
           CAN Bus Line
```

**Key Requirements:** <br>
- **Parallel Connection**: All devices connect to the same two-wire bus <br>
- **Differential Signaling**: CAN_H and CAN_L provide robust communication <br>
- **Linear Topology**: Avoid star configurations or loops <br>
- **Proper Termination**: Essential for signal integrity <br>

### Network Termination

> **⚠️ Critical Requirement**
> 
> The CAN bus **must** be terminated with 120Ω resistors at both ends, regardless of cable length. This termination prevents signal reflections that can cause communication errors.

**Termination Rules:** <br>
- ✅ **Required**: 120Ω termination at each end of the bus <br>
- ✅ **Always Needed**: Even for very short cable lengths <br>
- ❌ **Never**: Terminate stub lines or intermediate connections <br>
- ⚠️ **Important**: Use precision resistors (1% tolerance recommended) <br>

### Bus Length Limitations

The maximum bus length is primarily limited by signal propagation delay. The CAN multi-master arbitration process requires that signals arrive at all nodes quasi-simultaneously (before sampling within a bit time).

#### Standard Bus Length Specifications

| Baud Rate | Maximum Bus Length | Typical Application |
|-----------|-------------------|-------------------|
| **1 Mbit/s** | < 20m | High-speed local networks |
| **500 kbit/s** | < 100m | Standard industrial networks |
| **250 kbit/s** | < 250m | Medium-range applications |
| **125 kbit/s** | < 500m | Extended industrial networks |
| **50 kbit/s** | < 1000m | Long-distance applications |
| **20 kbit/s** | < 2500m | Very long networks |
| **10 kbit/s** | < 5000m | Maximum distance applications |

> **📝 Note**: Literature often states 40m for 1 Mbit/s networks. However, this doesn't apply to networks with optically isolated CAN controllers. Worst-case calculations with optocouplers yield 5m at 1 Mbit/s, though 20m is typically achievable in practice.

> **⚠️ Important**: For bus lengths over 1000m, CAN repeaters may be necessary to maintain signal integrity.

### Stub Lines (Drop Lines)

Stub lines are short cable branches that connect individual devices to the main bus line. While they can cause signal reflections, they are generally acceptable when properly designed.

#### Stub Line Guidelines

Reflections from stub lines are typically uncritical if they settle completely before the sampling point. With standard bit timing settings used in bus couplers, the following stub line lengths are permissible:

| Baud Rate | Max Single Stub Length | Max Total Stub Length |
|-----------|------------------------|----------------------|
| **1 Mbit/s** | < 1m | < 5m |
| **500 kbit/s** | < 5m | < 25m |
| **250 kbit/s** | < 10m | < 50m |
| **125 kbit/s** | < 20m | < 100m |
| **50 kbit/s** | < 50m | < 250m |

> **⚠️ Warning**: Stub lines must never be terminated with resistors.

### Multiport Taps

When using passive multiport distributors, shorter stub line lengths must be maintained to ensure proper signal integrity.

#### Multiport Tap Specifications

| Baud Rate | Max Stub Length (Multiport) | Max Trunk Line Length |
|-----------|----------------------------|---------------------|
| **1 Mbit/s** | < 0.3m | < 25m |
| **500 kbit/s** | < 1.2m | < 66m |
| **250 kbit/s** | < 2.4m | < 120m |
| **125 kbit/s** | < 4.8m | < 310m |

### Cable Requirements

Proper cable selection is crucial for reliable CAN communication.

#### Recommended Cable Specifications

**Primary Requirements:** <br>
- **Cable Type**: Twisted pair, shielded (2x2 conductors) <br>
- **Characteristic Impedance**: 108-132 Ω <br>
- **Shield**: Overall screen for EMI protection <br>
- **Conductor**: Minimum 0.25 mm² cross-section <br>

**Optional Considerations:** <br>
- **CAN Ground Connection**: Second pair can be omitted for small networks with common power supply <br>
- **Cable Length**: Consider voltage drop for power-over-bus applications <br>
- **Environmental Rating**: Select appropriate jacket material for installation environment <br>

---

## CANopen Communication Model

### Device Model Overview

CANopen consists of a protocol definition (communication profile) and device profiles that standardize data content for specific device classes. This layered approach ensures interoperability between devices from different manufacturers.

**Architecture Components:** <br>
- **Communication Profile**: Protocol definition and message formats <br>
- **Device Profiles**: Standardized data content for device classes <br>
- **Object Dictionary**: Structured parameter and data storage <br>
- **Communication Objects**: Different message types for various purposes <br>

### Object Dictionary Structure

The CANopen device parameters and process data are organized in an Object Dictionary, providing structured access to all device functionality.

**Object Dictionary Features:** <br>
- **Hierarchical Organization**: Objects organized by index and sub-index <br>
- **Standardized Access**: Uniform method for parameter configuration <br>
- **Data Type Definition**: Consistent data representation across devices <br>
- **Access Control**: Read-only, write-only, and read-write permissions <br>

> **📖 Reference**: For complete Object Dictionary details, see [Object Dictionary](object-dictionary.md)

### Communication Types

CANopen defines several communication types for input and output data (Process Data Objects):

#### Event-Driven Communication
- **Behavior**: Messages sent immediately when data changes
- **Advantage**: Efficient bandwidth usage, immediate response
- **Use Case**: Status changes, alarm conditions, sporadic data
- **Characteristic**: Only changes transmitted, not continuous polling

#### Cyclic Synchronous Communication
- **Behavior**: SYNC message triggers synchronized data exchange
- **Advantage**: Deterministic timing, coordinated network behavior  
- **Use Case**: Real-time control applications, coordinated motion
- **Characteristic**: All devices synchronized to common time base

#### Polled Communication (On-Demand)
- **Behavior**: Data transmitted only when specifically requested
- **Advantage**: Full master control over communication timing
- **Use Case**: Diagnostic data, configuration parameters
- **Characteristic**: Client-server model with explicit requests

### Transmission Types

The desired communication type is configured using the **Transmission Type** parameter in PDO configuration objects.

**Configuration Values:** <br>
- **0**: SYNC-triggered (synchronous) <br>
- **1-240**: SYNC with event counter <br>
- **254**: Asynchronous event-driven <br>
- **255**: Asynchronous polled/on-demand <br>

---

## CANopen Objects & Services

### Network Management (NMT)

Network Management follows a master-slave structure requiring one CANopen device to assume the role of CANopen Master, with all other devices operating as NMT Slaves.

**Network Roles:** <br>
- **NMT Master**: Controls network startup, state transitions, error handling <br>
- **NMT Slaves**: Respond to master commands, report status, execute state changes <br>
- **Node Addressing**: Each slave has unique Node-ID in range [1..127] <br>

**NMT Services Enable:** <br>
- Device initialization and startup sequencing <br>
- Operational state control and monitoring   <br>
- Device reset and error recovery procedures <br>
- Network-wide coordination and synchronization <br>

> **📖 Reference**: For detailed NMT information, see [Network Management](network-management.md)

### Service Data Objects (SDO)

A Service Data Object enables read and write access to the Object Dictionary, providing the primary method for device configuration and parameter access.

**SDO Communication Model:** <br>
- **Server**: Owner of the Object Dictionary (typically the device being configured) <br>
- **Client**: CAN node requesting data or initiating writes (typically the master) <br>
- **Upload**: Reading a value from the Object Dictionary <br> 
- **Download**: Writing a value to the Object Dictionary <br>

**Key Features:** <br>
- **Confirmed Service**: Every request receives a response <br>
- **Segmented Transfer**: Large data objects transferred in multiple segments <br>
- **Error Handling**: Detailed error codes for troubleshooting <br>
- **Security**: Access permissions enforced at object level <br>

### Process Data Objects (PDO)

A message containing only process data is called a "Process Data Object" (PDO). PDOs are designed for data that must be exchanged cyclically or in real-time.

**PDO Concept:** <br>
- **Efficient Transfer**: No overhead information (index, sub-index, length) <br>
- **Mapping Configuration**: Source and destination defined in separate PDO mapping <br>
- **Real-Time Capability**: Optimized for time-critical applications <br>
- **Multiple Mappings**: Up to 8 independent PDO configurations supported <br>

#### PDO Usage Requirements

PDOs can only be used when the NMT state machine is in "Operational" state. PDO configuration must be performed in "Pre-Operational" state.

**PDO Configuration:** <br>
- **Receive PDOs**: Configure processing of incoming PDO messages <br>
- **Transmit PDOs**: Configure transmission of outgoing PDO messages <br>
- **Mapping Flexibility**: Each PDO can carry up to 8 bytes (64 bits) of data <br>
- **Data Combination**: Multiple data types can be combined in single PDO <br>

**Example Combinations:**
- Two UNSIGNED32 values <br>
- One UNSIGNED32 + one UNSIGNED8 value <br>
- Custom combinations up to 8-byte limit <br>

### Synchronization Object (SYNC)

The Synchronization Object enables simultaneous validation of PDO data for all devices on the bus, ensuring coordinated network behavior.

**SYNC Operation:** <br>
- **Timing Master**: One device generates SYNC messages <br>
- **Network Coordination**: All devices synchronize to SYNC timing <br>
- **Data Consistency**: Ensures simultaneous input/output updates <br>
- **Deterministic Behavior**: Critical for real-time control applications <br>

### Time Stamp Object (TIME)

The Time-Stamp object provides network-wide time synchronization for applications requiring coordinated timing.

**Standard Time Format:** <br>
- **Resolution**: Milliseconds after midnight (32-bit field) <br>
- **Date Reference**: Days since January 1, 1984 (16-bit field) <br>
- **Overflow**: System resets on June 7, 2163 <br>

**High-Resolution Option:** <br>
For time-critical applications requiring microsecond accuracy: <br>
- **Resolution**: 1 microsecond (32-bit unsigned) <br>
- **Reset Interval**: Counter resets every 72 minutes <br>
- **Use Case**: Precise synchronization in large networks with reduced transmission rates <br>

### Emergency Object (EMCY)

An Emergency message is sent whenever an error occurs in the controller that is not caused by SDO access. This service is unconfirmed and transmitted with CAN-ID 80h + Node-ID.

**Emergency Characteristics:** <br>
- **Automatic Transmission**: Sent immediately when errors occur <br>
- **Unconfirmed Service**: No acknowledgment required <br>
- **Standard CAN-ID**: 0x80 + Node-ID for consistent identification <br>
- **Error Classification**: Provides specific error codes and additional information <br>

---

## Configuration & Setup

### Initial Configuration

On first startup, the C7 controller comes pre-configured with default settings that enable immediate network connection for basic applications.

**Default Configuration:**
- **Node-ID**: 1
- **Baud Rate**: 500 kbit/s  
- **Mode**: CANopen Classic (standard mode)
- **PDO Configuration**: Basic transmit/receive PDOs enabled

### Layer Setting Services (LSS)

If you need to modify the default settings, the Node-ID and bit rate must be configured using LSS (Layer Setting Services).

**LSS Capabilities:** <br>
- **Node-ID Assignment**: Set unique network addresses <br>
- **Baud Rate Configuration**: Adjust communication speed <br>
- **Network Scan**: Discover devices and their current settings <br>
- **Mass Configuration**: Configure multiple devices simultaneously <br>

### CANopen FD vs Classic Mode

The device supports both CANopen Classic and the newer CANopen FD (Flexible Data Rate) modes.

#### Mode Selection

Configuration is performed through Object **0x1F50sub2** (Download Program Data - CANopen Configuration):

**Configuration Data Format:** <br>
- **Byte 0**: FD Mode Flag (0 = Classic, ≠0 = FD mode) <br>
- **Byte 1**: Node-ID (1-127) <br>
- **Byte 2**: Baud rate low byte (kbit/s) <br>
- **Byte 3**: Baud rate high byte (kbit/s) <br>
 
#### Mode Characteristics

| Mode | Data Rate | Frame Size | Compatibility |
|------|----------|------------|---------------|
| **CANopen Classic** | Fixed | Up to 8 bytes | Full backward compatibility |
| **CANopen FD** | Variable | Up to 64 bytes | Requires FD-capable network |

### Configuration Storage

Once a device is configured, the configuration can be modified through either LSS services or SDO access to object 0x1F50sub2.

**Storage Process:** <br>
1. **Configuration Write**: New settings written to configuration object <br>
2. **Automatic Storage**: Configuration automatically saved to non-volatile memory (NVM) <br>
3. **Power Cycle Required**: Device must be power-cycled to activate new settings <br>
4. **Persistent Storage**: Settings retained through power cycles <br>

> **⚠️ Important**: A power-off/power-on cycle is required to activate new configuration settings.

---

## Technical Specifications

### Bus Length vs Baud Rate

Complete specification table for network planning:

| Baud Rate | Maximum Bus Length | Signal Propagation | Application Type |
|-----------|-------------------|-------------------|------------------|
| **10 kbit/s** | 5000m | Low-speed long-distance | Remote monitoring |
| **20 kbit/s** | 2500m | Extended networks | Distributed control |
| **50 kbit/s** | 1000m | Medium-distance | Building automation |
| **125 kbit/s** | 500m | Standard industrial | Manufacturing lines |
| **250 kbit/s** | 250m | Fast industrial | Motion control |
| **500 kbit/s** | 100m | High-speed industrial | Real-time control |
| **1 Mbit/s** | 20m* | Maximum speed | High-speed local |

*) With optically isolated controllers. See [Bus Length Limitations](#bus-length-limitations) for details.

### Stub Line Specifications

Detailed stub line requirements for network design:

| Baud Rate | Single Stub Max | Total Stubs Max | Reflection Time | Notes |
|-----------|----------------|----------------|-----------------|-------|
| **1 Mbit/s** | 1m | 5m | 10ns/m | Critical timing |
| **500 kbit/s** | 5m | 25m | 25ns/m | Standard industrial |
| **250 kbit/s** | 10m | 50m | 50ns/m | Moderate timing |
| **125 kbit/s** | 20m | 100m | 100ns/m | Relaxed timing |
| **50 kbit/s** | 50m | 250m | 250ns/m | Long-distance OK |

### Multiport Tap Specifications

When using passive multiport distributors (star topology with passive taps):

| Baud Rate | Stub Length | Trunk Length | Total Network | Distribution |
|-----------|------------|--------------|---------------|--------------|
| **1 Mbit/s** | 0.3m | 25m | 30m | Very restricted |
| **500 kbit/s** | 1.2m | 66m | 78m | Limited |
| **250 kbit/s** | 2.4m | 120m | 144m | Moderate |
| **125 kbit/s** | 4.8m | 310m | 362m | Extended |

---

**Reference Links:** <br>
- [Object Dictionary](object-dictionary.md) - Complete parameter reference <br>
- [Network Management](network-management.md) - Detailed NMT state machine documentation  <br>
- [Introduction](introduction.md) - Safety requirements and getting started <br>

**External References:** <br>
- **CAN in Automation**: [http://www.can-cia.org](http://www.can-cia.org) <br>
- **Q-Drives Support**: [http://www.q-drives.com](http://www.q-drives.com) <br>

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
![](logo-horizontal.jpg)
# Introduction

## Table of Contents
- [About This Documentation](#about-this-documentation)
- [Important Information](#important-information)
  - [Warranty and Disclaimer](#warranty-and-disclaimer)
  - [Target Group and Qualifications](#target-group-and-qualifications)
  - [Safety and Warning Notices](#safety-and-warning-notices)
- [Documentation Structure](#documentation-structure)
- [Getting Started](#getting-started)

## About This Documentation
This documentation provides comprehensive technical information for **CANopen Object Dictionary implementation** on Q-Drives C7 devices. It covers the complete CANopen protocol implementation, network management, and operational procedures for technicians and engineers working with industrial automation systems.

### What You'll Find Here

- **Object Dictionary Reference**: Complete documentation of all CANopen objects with parameters, data types, and access permissions
- **CANopen Protocol Implementation**: Physical layer setup, communication types, network topology, and technical specifications
- **Network Management (NMT)**: State machines, startup procedures, error handling, and practical troubleshooting guidance
- **Operation Modes**: Detailed documentation of device operation modes, includes Profile position mode, velocity mode, homing mode
- **About & Support**: Documentation author information, company details, and technical support resources
- **Safety & Legal Information**: ESD protection, warranty disclaimers, and qualified personnel requirements

### CANopen Overview

CANopen is a communication protocol based on the CAN (Controller Area Network) bus system, widely used in industrial automation. It provides standardized communication methods for devices in manufacturing, automotive, and other industrial applications.

---

## Important Information

### Warranty and Disclaimer

> **⚠️ Important Legal Notice**
> 
> Q-Drives GmbH accepts **no liability** for damage or malfunctions resulting from:
> - Installation errors
> - Failure to observe this manual
> - Improper repairs
> 
> **Responsibility**: The selection and use of Q-Drives products is the responsibility of the system designer or end user.
> 
> **Integration**: Q-Drives GmbH accepts no responsibility for product integration into end systems.
> 
> **Terms**: Our General Terms and Conditions at [www.q-drives.com](http://www.q-drives.com) apply to all products and services.

### Target Group and Qualifications

#### Intended Audience

This documentation is designed for technically trained specialists:

- **Development Engineers** - System design and implementation
- **Plant Designers** - Industrial automation system planning
- **Fitters/Service Personnel** - Installation and maintenance
- **Application Engineers** - System integration and optimization

#### Required Qualifications

**Only qualified personnel** may install, program and commission these products.

Qualified personnel must meet **all** of the following criteria:

✅ **Training & Experience**
- Appropriate training in motor control systems
- Hands-on experience with industrial automation

✅ **Technical Knowledge**
- Familiar with and understand this technical manual
- Knowledge of CANopen protocol fundamentals

✅ **Regulatory Compliance**
- Familiar with applicable safety regulations
- Understanding of electrical safety standards

### Safety and Warning Notices

#### Electrostatic Discharge (ESD) Protection

> **⚠️ CAUTION**
> 
> Electronic devices are sensitive to electrostatic discharge. **Failure to follow ESD protection measures may result in permanent device damage.**

#### Required ESD Protection Measures

**Personal Protection:**
- ✅ Wear grounded wrist strap or ESD protective clothing
- ✅ Use properly grounded, antistatic work surfaces
- ✅ Ensure all tools are ESD-safe and grounded

**Device Handling:**
- ❌ **Never** touch electronic components directly
- ✅ Hold devices only by housing or designated mounting points
- ✅ Avoid unnecessary movement that could cause static buildup
- ✅ Use antistatic packaging for storage and transport

#### Critical Safety Points

| ⚠️ Warning | Description | Consequence |
|------------|-------------|-------------|
| **ESD Damage** | Static discharge can destroy circuits | Permanent device failure |
| **Improper Installation** | Incorrect wiring or mounting | System malfunction, safety hazard |
| **Unauthorized Repairs** | Modifications by unqualified personnel | Loss of warranty, safety risk |

---

## Documentation Structure

This documentation is organized into the following main sections:

### 📚 Core Documentation

| Section | Purpose | Target Users |
|---------|---------|--------------|
| **[Object Dictionary](object-dictionary.md)** | Complete CANopen object reference | All users |
| **[CANopen Protocol](canopen.md)** | Technical protocol implementation details | Engineers, System Designers |
| **[Network Management](network-management.md)** | State machines, startup, and troubleshooting | Technicians, Engineers |
| **[Operation Modes](operation-modes.md)** | Device operation modes and control configurations | Engineers, Technicians |
| **[About](about.md)** | Documentation author and company information | All users |

---

## Getting Started

### For First-Time Users

1. **📖 Read this Introduction** - Understand safety requirements and documentation scope
2. **📡 Learn CANopen Protocol** - Understand physical layer, network setup, and communication basics
3. **🔍 Review Object Dictionary** - Familiarize yourself with available parameters and configuration options
4. **⚙️ Study Network Management** - Learn NMT states, startup procedures, and troubleshooting
4. **⚙️ Study Operation Modes** - Learn Operation Modes and how to use them
5. **🚀 Implementation** - Apply knowledge to your specific application

### Quick Navigation

**Need to...** | **Go to...**
---------------|-------------
Configure a device | [Object Dictionary](object-dictionary.md)
Troubleshoot startup issues | [Network Management - Error Handling](network-management.md#error-handling--troubleshooting)
Understand network behavior | [Network Management - Startup Process](network-management.md#startup-process)
Learn CANopen protocol | [CANopen Protocol](canopen.md)
Find specific parameters | [Object Dictionary](object-dictionary.md)
Configure control modes | [Operation Modes](operation-modes.md)

### Technical Support

For additional support beyond this documentation:

- **Website**: [www.q-drives.com](http://www.q-drives.com)
- **Contact**: technik@q-drives.com

---

### Version History
| Version | Date       | Changes                    | Firmware Version   |
|---------|------------|----------------------------|--------------------|
| Version | Date       | Changes                    | Firmware Version   |
|---------|------------|----------------------------|--------------------|
| 0.1     | 15.11.2024 | Initial release            | 2.01.6             |
| 1.1     | 11.08.2025 | Add Operation Modes        | 2.01.6             |
| 1.2     | 11.09.2025 | Update Object Dictionary   | 2.2.1 Build 108-25 |
| 1.3     | 11.09.2025 | Update operation modes     | 2.2.1 Build 108-25 |

---

**Document Information:** <br>
- **Firmware Compatibility**: 2.01.6 and later <br>
- **Standards**: CiA 301, CiA 402 compliant
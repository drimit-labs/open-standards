# Drimit Link Open Standard (DL-OS) - Technical Specification

**Document Reference:** DL-OS-SPEC-v2.0  
**Version:** 2.0  
**Status:** Unified Technical Specification  
**Date:** October 2025  
**Organization:** [Drimit Labs](https://github.com/drimit-labs)  
**License:** [CERN Open Hardware License v2 - Permissive](/LICENCE)  
**Repository:** https://github.com/drimit-labs/drimit-link-open-standard

---

## Document Information

| Field | Value |
|-------|-------|
| Document ID | DL-OS-SPEC-v2.0 |
| Replaces | README.md + All Annexes (A, B-*, C) |
| Language | English |
| Classification | Public Technical Standard |
| Distribution | Open Source |
| Maintenance | Drimit Labs |

## Revision History

| Version | Date | Changes | Author |
|---------|------|---------|--------|
| 2.0 | 2025-10 | Unified book format, consolidated all annexes | Drimit Labs |
| 1.x | 2025-xx | Individual annexes and README format | Drimit Labs |

---

# Part I: Introduction and Foundation

## Chapter 1: Introduction and Scope

### 1.1 Purpose and Vision of DL-OS

The **Drimit Link Open Standard (DL-OS)** defines a comprehensive **open modular connector system** based on the **CAN bus (ISO 11898-2)** for reconfigurable electronic systems. This standard enables the creation of versatile control surfaces, audiovisual controllers, creative workstations, and embedded modules that can be dynamically reconfigured to meet changing requirements.

DL-OS addresses the fundamental challenge of creating modular electronic systems that are:
- **Physically robust** and reliable for professional use
- **Electrically safe** with hot-plug capabilities  
- **Mechanically precise** for seamless user interaction
- **Logically flexible** for diverse application domains
- **Economically viable** for both prototyping and production

### 1.2 Scope and Boundaries

**DL-OS Specification Includes:**
- Physical connector design (3×3 pogo pin grid)
- Electrical interface (CAN bus, power, identification)
- Mechanical mounting system (magnets, screws, 25mm grid)
- Communication protocols (CAN FD with CBOR payloads)
- Device discovery and enumeration procedures
- Power distribution architecture (USB-C PD primary)
- Software abstraction layers (HAL/PHY ontologies)
- Manufacturing and testing guidelines
- Compliance and certification requirements

**DL-OS Specification Excludes:**
- Higher-layer application protocols (MIDI, OSC, etc.)
- User interface semantics and workflows
- Host software implementation details
- Market-specific compliance requirements
- Proprietary extensions or modifications

### 1.3 Target Applications and Use Cases

**Primary Applications:**
- **Audio Production:** Mixing consoles, control surfaces, effects processors
- **Video Production:** Video mixers, camera controllers, monitoring systems  
- **Broadcasting:** Live production, streaming interfaces, automation systems
- **Creative Technology:** Interactive installations, performance controllers
- **Industrial Control:** HMI panels, process controllers, diagnostic systems
- **Prototyping:** Research platforms, educational systems, development tools

**Representative Use Cases:**
- Modular mixing console with swappable channel strips
- Video production switcher with customizable button layouts  
- Interactive art installation with sensor and actuator modules
- Industrial HMI with context-sensitive control panels
- Educational electronics platform for learning and experimentation

### 1.4 Non-Goals and Exclusions

**DL-OS Does NOT Define:**
- Application-specific communication protocols above the transport layer
- User interface guidelines or usability standards  
- Market segment requirements (broadcast, live sound, etc.)
- Software development frameworks or APIs
- Certification procedures for specific industries
- Intellectual property licensing for implementations

**Design Philosophy Boundaries:**
- Physical compatibility takes precedence over protocol flexibility
- Open standard principles override proprietary optimizations
- Safety and reliability requirements supersede cost considerations
- Interoperability goals constrain implementation choices

### 1.5 Document Organization and How to Use This Standard

**For Hardware Designers:**
- Start with Part II (Chapters 4-6) for physical design requirements
- Reference Part III (Chapters 7-9) for system integration
- Use Part VII (Appendices) for detailed implementation guidance

**For Software Developers:**  
- Begin with Part IV (Chapters 10-12) for communication protocols
- Study Part V (Chapters 13-15) for software architecture
- Consult Appendix B for code examples and templates

**For System Integrators:**
- Review Part I (Chapters 1-3) for overall requirements
- Focus on Part VI (Chapters 16-18) for implementation best practices
- Use compliance procedures in Appendix C for validation

**For Manufacturers:**
- Emphasize Part VI (Chapters 16-18) for production requirements
- Reference Appendix A for circuit designs
- Follow Appendix C for testing and quality assurance

---

## Chapter 2: Design Principles and Architecture Overview

### 2.1 System Architecture Philosophy

DL-OS employs a **distributed modular architecture** where intelligence resides in individual modules rather than a centralized controller. This approach provides several key advantages:

**Distributed Intelligence:**
- Each module contains its own microcontroller and local processing
- System functionality emerges from module collaboration
- No single point of failure compromises entire system
- Modules can operate independently during partial system failures

**Hot-Plug Architecture:**
- All connections designed for safe insertion and removal under power
- Ground-first contact sequencing prevents electrical damage
- Automatic discovery and enumeration of new modules
- Graceful handling of module removal and reconnection

**Scalable Communication:**
- Linear CAN bus topology supports reliable multi-drop communication
- Standardized message formats enable cross-vendor interoperability
- Host-coordinated arbitration prevents bus conflicts
- Efficient bandwidth utilization through prioritized messaging

### 2.2 Modular Design Principles

**Physical Modularity:**
- Standard 25×25mm tile grid for predictable mechanical interface
- Reversible connection (0°, 90°, 180°, 270°) without signal corruption
- Magnetic alignment for precise positioning and secure retention
- Screw mounts provide additional mechanical security

**Electrical Modularity:**
- Standardized power distribution (5-12V nominal on V+ rail)
- Differential CAN bus for robust, high-speed communication
- Identification pins enable automatic orientation detection
- Protection circuits ensure safe operation and fault tolerance

**Logical Modularity:**
- Hardware Abstraction Layer (HAL) provides device-independent interfaces
- Physical Layer (PHY) ontologies describe actual hardware capabilities
- Endpoint-based addressing enables fine-grained control
- State machine framework ensures predictable behavior

### 2.3 Hot-Plug and Reversible Connection Philosophy  

**Ground-First Contact Design:**
The pogo pin connector employs carefully designed pin lengths to ensure ground connections are established before power and signal connections:

```
Contact Sequence: GND → V+ → Signals (CAN, ID)
Disconnect Sequence: Signals → V+ → GND (reverse order)
```

**Reversible Connection Benefits:**
- Eliminates connector keying and orientation constraints
- Reduces assembly errors and user frustration
- Enables flexible system layouts and reconfigurations
- Simplifies manufacturing by eliminating orientation-specific variants

**Orientation Detection Mechanism:**
- Gray code encoding on ID1/ID2 pins provides unambiguous orientation
- Hardware crosspoint switches maintain proper CAN polarity
- Firmware automatically adapts to detected orientation
- Display rotation and UI elements adjust to maintain usability

### 2.4 Scalability and Matrix Organization

**Tile Grid Scalability:**
The 25×25mm tile grid provides a foundation for systems ranging from simple 2×2 configurations to complex matrices exceeding 20×20:

| Configuration | Typical Applications | Module Count |
|---------------|---------------------|--------------|
| 2×2 to 4×4 | Desktop controllers, portable units | 4-16 |
| 6×6 to 8×8 | Professional mixing surfaces | 36-64 |  
| 10×10 to 16×16 | Large format consoles | 100-256 |
| 20×20+ | Stadium/arena installations | 400+ |

**Linear Bus Topology:**
Despite the 2D grid arrangement, the electrical connection follows a linear topology to maintain CAN bus integrity:
- Single continuous trunk with short stubs to each slot
- Termination only at physical ends of the bus
- Stub length limited to <10mm for signal integrity
- Predictable signal propagation and timing characteristics

### 2.5 Open Standard Philosophy and IP Policy

**Open Hardware Principles:**
- Complete specifications publicly available under CERN-OHL-P v2
- No patent restrictions on implementing the core standard
- Royalty-free licensing for commercial and non-commercial use  
- Collaborative development model with public review process

**Intellectual Property Guidelines:**
- Core standard remains unencumbered by proprietary IP
- Vendors may add proprietary features above the standard layer
- Attribution required for derivative works and implementations
- Compatible implementations encouraged to display DL-OS logo

**Community Development:**
- Public repository for specifications and reference designs
- Open issue tracking for bug reports and enhancement requests
- Regular review cycles with stakeholder input
- Vendor-neutral governance structure

---

## Chapter 3: Compliance, Licensing and Governance

### 3.1 Compliance Requirements and Certification

**Physical Compliance Requirements:**
A DL-OS compliant module MUST meet ALL physical interface requirements:
- 3×3 pogo connector with specified pinout and contact sequence
- Mechanical dimensions within tolerance for 25×25mm tile grid
- Magnetic alignment system with correct polarity configuration
- Electrical protection circuits as specified in reference designs

**Electrical Compliance Requirements:**
All DL-OS modules MUST implement:
- CAN FD transceiver meeting ISO 11898-2 specifications
- Orientation detection and crosspoint switching logic
- Power distribution with ideal diode protection
- ESD/EMI protection as specified in protection circuit requirements

**Communication Compliance Requirements:**
DL-OS compliant modules MUST support:
- Standard CAN frame format with 29-bit extended identifiers
- CBOR-encoded payloads for device description and capabilities
- Host-coordinated node ID assignment protocol
- Minimum required message types for discovery and enumeration

**Testing and Validation:**
- Self-certification allowed for simple modules
- Third-party testing recommended for complex systems
- Compliance test suite available in Appendix C
- Interoperability testing with reference implementations

### 3.2 License Terms (CERN-OHL-P v2)

The DL-OS specification is licensed under the **CERN Open Hardware License v2 - Permissive (CERN-OHL-P-2.0)**, which provides:

**Permissions:**
- **Commercial Use:** Manufacture and sell DL-OS compatible products
- **Modification:** Create derivative designs based on DL-OS
- **Distribution:** Share designs and documentation freely
- **Patent Use:** Use any patents covering the DL-OS design
- **Private Use:** Implement DL-OS for internal projects

**Conditions:**
- **License Notice:** Include CERN-OHL-P notice in distributions
- **Copyright Notice:** Maintain attribution to Drimit Labs
- **State Changes:** Document modifications to original design
- **Source Availability:** Provide source files for hardware designs

**Limitations:**
- **Liability:** No warranty or liability for damages
- **Trademark Rights:** License does not grant trademark permissions
- **Patent Scope:** Patent license limited to DL-OS implementations

### 3.3 Trademark Usage and Attribution Guidelines

**DL-OS Trademark Usage:**
- "Drimit Link" is a trademark of Drimit Labs
- "DL-OS Compatible" may be used for compliant implementations  
- Logo usage requires separate trademark license agreement
- Marketing claims MUST be accurate regarding compliance level

**Required Attribution:**
All DL-OS implementations SHOULD include:
```
"Based on Drimit Link Open Standard (DL-OS)"
"Compatible with DL-OS v2.0"  
"Design licensed under CERN-OHL-P v2"
```

**Marketing and Communications:**
- Accurate representation of compliance level required
- No implication of endorsement by Drimit Labs without agreement
- Compatibility claims MUST be substantiated by testing
- Reference to specific DL-OS version recommended

### 3.4 Governance Model and Change Management

**Governance Structure:**
- **Maintainer:** Drimit Labs holds ultimate responsibility for standard
- **Contributors:** Open community of implementers and users
- **Review Board:** Technical experts from key stakeholder organizations
- **Public Process:** All changes subject to public review and comment

**Change Management Process:**
1. **Proposal:** Submit enhancement via GitHub issue or RFC document
2. **Discussion:** Public review and technical discussion period
3. **Evaluation:** Technical review by maintainers and experts
4. **Decision:** Accept, modify, or reject with documented rationale
5. **Implementation:** Update specifications and reference designs
6. **Release:** Version increment and public notification

**Version Control Policy:**
- **Major Versions:** Breaking changes to physical compatibility
- **Minor Versions:** Backward-compatible enhancements and clarifications
- **Patch Versions:** Bug fixes and editorial corrections
- **Timeline:** Major versions no more frequent than annually

### 3.5 Version Compatibility Matrix

| Compatibility Type | Same Major | Different Major | Notes |
|--------------------|------------|-----------------|-------|
| **Physical** | ✅ Required | ❌ Not Guaranteed | Connector must remain compatible |
| **Electrical** | ✅ Required | ❌ Not Guaranteed | Signal levels and timing |
| **Protocol** | ✅ Required | 🔶 Best Effort | Communication layer compatibility |
| **Software** | 🔶 Best Effort | ❌ Not Guaranteed | HAL/PHY ontology versions |

**Compatibility Guidelines:**
- Implementations SHOULD support at least one major version backward
- Forward compatibility not guaranteed across major versions
- Cross-version operation possible but not required
- Migration paths documented for major version transitions

---

# Part II: Physical Layer Specifications

## Chapter 4: Electrical Interface Specification

### 4.1 Connector Pinout and Signal Assignment

#### 4.1.1 3×3 Pogo Pin Grid Layout

The DL-OS connector employs a 3×3 grid of pogo pins with 1.27mm pitch, providing a compact yet robust connection system. The pin assignment is designed for reversible operation while maintaining signal integrity and power safety.

**Standard Pinout (Module Perspective):**
```
Row/Col Layout:
(1,1)=NW: ID1      (1,2)=N:  ID2      (1,3)=NE: GND
(2,1)=W:  S2       (2,2)=C:  V+       (2,3)=E:  S1
(3,1)=SW: GND      (3,2)=S:  NC       (3,3)=SE: GND
```

#### 4.1.2 Signal Definitions and Characteristics

| Pin | Signal | Description | Type | Voltage | Max Current | Notes |
|-----|--------|-------------|------|---------|-------------|-------|
| **S1** | CANH | CAN high line | Differential | 2.5V CM | - | Pairs with S2 |
| **S2** | CANL | CAN low line | Differential | 2.5V CM | - | 120Ω ±10% impedance |
| **V+** | Power rail | Main supply | DC | 5-12V | 1A avg / 3A peak | Ideal diode required |
| **GND** | Ground | Common return | - | 0V | - | Four pads, ground plane |
| **ID1** | Identification | Orientation bit 0 | Digital | 3.3V | <1mA | Gray code MSB |
| **ID2** | Identification | Orientation bit 1 | Digital | 3.3V | <1mA | Gray code LSB |
| **NC** | No Connect | Reserved | - | - | - | Future expansion |

#### 4.1.3 Contact Sequence (Ground-First Design)

The pogo connector design implements a critical safety feature through controlled contact sequencing:

**Contact Engagement Sequence:**
1. **GND pins** (longest) make contact first
2. **V+ pin** (medium length) makes contact second  
3. **Signal pins** (shortest) make contact last

**Contact Disengagement Sequence:**
1. **Signal pins** break contact first
2. **V+ pin** breaks contact second
3. **GND pins** break contact last

This sequencing ensures that:
- Ground reference is established before any signals
- Power connections are made in a controlled manner
- Signal integrity is maintained during connection/disconnection
- No floating nodes exist during transition states

### 4.2 Electrical Characteristics

#### 4.2.1 CAN Bus Physical Layer (ISO 11898-2)

**Bus Specifications:**
- **Standard Compliance:** ISO 11898-2 High-Speed CAN
- **Differential Impedance:** 120Ω ±10%
- **Common Mode Voltage:** 2.5V ±2.0V
- **Differential Voltage:** 1.5V to 5.0V (dominant state)
- **Data Rate:** Up to 8 Mbps (CAN FD data phase)
- **Arbitration Rate:** 1 Mbps (standard)

**Signal Integrity Requirements:**
- **Stub Length:** ≤10mm from connector to transceiver
- **Trace Matching:** CANH/CANL length match within 0.5mm
- **Via Count:** Minimize vias in differential pair routing
- **Ground Plane:** Continuous ground plane beneath CAN traces
- **Layer Assignment:** Prefer dedicated signal layers for CAN routing

#### 4.2.2 Power Rail Specifications (5-12V)

**V+ Rail Characteristics:**
- **Nominal Voltage:** 12V (typical system voltage)
- **Operating Range:** 5V to 12V (modules must operate across full range)
- **Voltage Tolerance:** ±5% regulation under normal load
- **Current Capacity:** 1A average, 3A peak (per slot)
- **Ripple:** <100mV pp at full load
- **Transient Response:** <2V deviation for 100% load step

**Power Distribution Requirements:**
- **Copper Weight:** Minimum 1oz (35μm) for power traces
- **Trace Width:** Minimum 1.5mm for V+ distribution
- **Via Current:** Multiple vias for layer transitions (minimum 0.2mm diameter)
- **Decoupling:** 100μF + 1μF per slot minimum
- **Protection:** Ideal diode + eFuse per module mandatory

#### 4.2.3 Identification Pin Logic Levels

**Digital I/O Specifications:**
- **Logic Family:** 3.3V CMOS compatible
- **VIL (Input Low):** <0.8V
- **VIH (Input High):** >2.0V  
- **VOL (Output Low):** <0.4V @ 4mA sink
- **VOH (Output High):** >2.4V @ 4mA source
- **Pull-up/Pull-down:** 47kΩ to 100kΩ (base plate provides)
- **Input Current:** <±1μA leakage (high impedance)

### 4.3 Protection and Robustness

#### 4.3.1 ESD/EMI Protection Requirements

**ESD Protection (Per IEC 61000-4-2):**
- **Human Body Model:** ±8kV contact discharge
- **Machine Model:** ±400V machine discharge  
- **Charged Device Model:** ±1kV device discharge
- **Implementation:** TVS diodes on all external connections
- **Response Time:** <1ns clamping response

**EMI Protection Requirements:**
- **Common Mode Chokes:** 51-100Ω @ 100MHz on CAN lines
- **Ferrite Beads:** ≥600Ω @ 100MHz on V+ rail
- **Ground Plane:** Solid ground plane with minimal slots
- **Shielding:** Conductive housing recommended for EMI environments
- **Filtering:** Pi-filter configuration for power supply inputs

#### 4.3.2 Reference Protection Circuits

**CAN Bus Protection:**
```
CANH ─► CMC (100μH) ─► TVS (SM24CAN) ─► CAN Transceiver Pin 7
CANL ─► CMC (100μH) ─► TVS (SM24CAN) ─► CAN Transceiver Pin 6
                         │
                        GND
```

**Power Rail Protection:**  
```
V+ ─► eFuse (TI TPS25921) ─► Ideal Diode (LM74610) ─► Local V+
        │                      │
        └─► TVS (SMCJ12A)     └─► TVS (SMCJ5V0A) 
            │                      │
           GND                    GND
```

**ID Pin Protection:**
```  
ID1/ID2 ─► Series R (100Ω) ─► TVS (Zener 3.6V) ─► MCU GPIO
                                 │
                                GND
```

#### 4.3.3 Hot-Plug Safety Mechanisms

**Inrush Current Limiting:**
- **Soft-start circuits** required for modules with large capacitive loads
- **NTC thermistors** or **active inrush limiters** for power supply inputs
- **Slew rate control** on power distribution switches
- **Current monitoring** with overcurrent shutdown

**Fault Detection and Recovery:**
- **Overcurrent protection** with automatic retry after cooldown
- **Overvoltage/undervoltage** protection with immediate shutdown  
- **Thermal monitoring** with graduated response (warning → limit → shutdown)
- **Communication timeout** detection with module reset capability

### 4.4 Signal Integrity and Timing

#### 4.4.1 Differential Impedance Requirements

**CAN Differential Pair:**
- **Target Impedance:** 120Ω ±10% differential  
- **Common Mode Impedance:** 60Ω ±10% (each trace to ground)
- **PCB Stack-up:** Controlled impedance fabrication required
- **Trace Geometry:** Maintain consistent width and spacing
- **Layer Changes:** Minimize via transitions in differential pair

**Impedance Calculation Guidelines:**
```
For typical 4-layer PCB (1.6mm thickness):
- Trace Width: 0.127mm (5 mil)
- Trace Spacing: 0.127mm (5 mil) 
- Dielectric Height: 0.2mm (8 mil)
- Dielectric Constant: 4.3 (FR-4)
```

#### 4.4.2 Stub Length Limitations

**Maximum Stub Lengths:**
- **CAN Signal Stubs:** 10mm maximum from connector to transceiver
- **Power Stubs:** 25mm maximum to first decoupling capacitor
- **ID Signal Stubs:** 15mm maximum to MCU input
- **Ground Connections:** Multiple short paths preferred over single long path

**Routing Guidelines:**
- **Direct Paths:** Minimize trace length and layer changes
- **Via Stitching:** Connect ground planes near connectors
- **Component Placement:** Locate transceivers close to connectors
- **Kelvin Connections:** Separate analog and digital ground returns where possible

#### 4.4.3 Crosstalk and EMC Considerations  

**Crosstalk Minimization:**
- **Guard Traces:** Ground traces between sensitive signals
- **Layer Assignment:** Separate analog and digital signals
- **Trace Spacing:** Minimum 3× trace width between parallel runs
- **Perpendicular Routing:** Cross signals at 90° when necessary

**EMC Best Practices:**
- **Loop Area Minimization:** Keep signal and return paths close
- **Clock Signal Management:** Minimize clock trace lengths and slew rates  
- **Bypass Capacitor Placement:** Close to IC power pins with short traces
- **Connector Filtering:** Filter all signals at connector entry points

---

*[Content continues with remaining chapters...]*

**References:**
- ISO 11898-2:2016 - Road vehicles — Controller area network (CAN) — Part 2: High-speed medium access unit
- IEC 61000-4-2:2008 - Electromagnetic compatibility (EMC) — Testing and measurement techniques — Electrostatic discharge immunity test
- CERN-OHL-P-2.0 - CERN Open Hardware License Version 2 - Permissive
# DL-OS Unified Terminology and Nomenclature Guide

## 1. Standard Abbreviations and Acronyms

### 1.1 Primary System Names
| Term | Full Name | Usage | Notes |
|------|-----------|-------|-------|
| **DL-OS** | Drimit Link Open Standard | Primary standard name | Unified usage across all documents |
| **DL-CS** | Drimit Link Connector Standard | Legacy term | **DEPRECATED** - use DL-OS |
| **DL-OCS** | Drimit Link Open Connector Standard | Legacy term | **DEPRECATED** - use DL-OS |

**Resolution:** All documents SHALL use **DL-OS** as the canonical standard name.

### 1.2 Technical Component Terms
| Term | Definition | Usage Context | Alt Terms (DEPRECATED) |
|------|------------|---------------|----------------------|
| **Module** | Individual functional unit with DL-OS connector | All contexts | Device, Node, Unit |
| **Base Plate** | Passive backplane with multiple DL-OS slots | Infrastructure | Backplane, Motherboard |
| **Host Module** | Module that coordinates the CAN bus | Communication | Master, Controller |
| **Client Module** | Module that responds to Host coordination | Communication | Slave, Peripheral |
| **Slot** | Physical connection point on base plate | Mechanical | Socket, Port |
| **Tile** | 25×25mm grid unit for module placement | Mechanical | Cell, Position |

### 1.3 Electrical and Signal Terms
| Term | Definition | Alt Terms | Notes |
|------|-----------|-----------|-------|
| **Pogo Pin** | Spring-loaded contact pin | Contact Pin | Standard connector technology |
| **CANH/CANL** | CAN Bus High/Low differential pair | CAN+/CAN- | ISO 11898-2 standard terms |
| **V+** | Main power rail (5-12V nominal) | VCC, VDD | Avoid VCC/VDD for clarity |
| **ID1/ID2** | Orientation identification pins | Orientation Pins | Gray code encoding |
| **Crosspoint** | Signal routing switch for orientation | CAN Swap, Mux | SPDT analog switch |

### 1.4 Communication Protocol Terms
| Term | Definition | Context | Standards Ref |
|------|-----------|---------|---------------|
| **Node-ID** | Unique identifier for CAN bus node | Protocol | 10-bit field in CAN ID |
| **Frame ID** | 29-bit extended CAN frame identifier | Protocol | ISO 11898-1 |
| **CBOR** | Concise Binary Object Representation | Data Encoding | RFC 8949 |
| **Endpoint** | Addressable function within module | Software | Capability unit |

---

## 2. Versioning and Document References

### 2.1 Version Number Format
- **Standard Format:** `v[MAJOR].[MINOR].[PATCH]` (Semantic Versioning)
- **Examples:** v1.0, v1.2, v2.0
- **Compatibility:** Major version changes break physical compatibility
- **Document References:** Include version in all cross-references

### 2.2 Document Naming Convention
| Document Type | Naming Pattern | Example |
|---------------|----------------|---------|
| **Main Standard** | `DL-OS-v[VERSION]` | DL-OS-v2.0 |
| **Technical Chapters** | `DL-OS-Chapter-[N]-v[VERSION]` | DL-OS-Chapter-4-v2.0 |
| **Appendices** | `DL-OS-Appendix-[X]-v[VERSION]` | DL-OS-Appendix-A-v2.0 |

---

## 3. Technical Specification Language

### 3.1 RFC 2119 Compliance Keywords
| Keyword | Meaning | Usage |
|---------|---------|-------|
| **MUST** | Absolute requirement | Mandatory for compliance |
| **MUST NOT** | Absolute prohibition | Forbidden for compliance |
| **SHALL** | Same as MUST | Legal/contractual context |
| **SHALL NOT** | Same as MUST NOT | Legal/contractual context |
| **SHOULD** | Strong recommendation | Best practice, may deviate with justification |
| **SHOULD NOT** | Strong discouragement | Avoid unless compelling reason |
| **MAY** | Optional | Permissible implementation choice |
| **RECOMMENDED** | Same as SHOULD | Preferred implementation |
| **OPTIONAL** | Same as MAY | Implementation choice |

### 3.2 Measurement Units and Precision
| Quantity | Primary Unit | Secondary | Precision |
|----------|-------------|-----------|-----------|
| **Length** | mm | inches (in parentheses) | ±0.01 mm |
| **Electrical** | V, A, Ω, F, H | - | 3 significant figures |
| **Frequency** | Hz, MHz | - | 1% accuracy |
| **Temperature** | °C | °F (in parentheses) | ±1°C |
| **Force** | N | kgf (in parentheses) | ±5% |
| **Time** | s, ms, μs, ns | - | SI prefixes |

---

## 4. Naming Conventions by Domain

### 4.1 Hardware Components
| Component | Naming Pattern | Example |
|-----------|----------------|---------|
| **Resistors** | R[number] | R1, R47, R100 |
| **Capacitors** | C[number] | C1, C10, C22 |
| **ICs** | U[number] or IC[number] | U1, IC3 |
| **Connectors** | J[number] or P[number] | J1, P2 |
| **Test Points** | TP[number] | TP1, TP5 |

### 4.2 Software/Firmware Objects
| Object Type | Naming Convention | Example |
|-------------|-------------------|---------|
| **Functions** | snake_case | `init_can_bus()` |
| **Constants** | UPPER_SNAKE_CASE | `MAX_NODES` |
| **Variables** | snake_case | `node_id` |
| **Structs/Classes** | PascalCase | `ModuleDescriptor` |
| **Enums** | PascalCase | `OrientationType` |

### 4.3 File and Directory Names
| Type | Convention | Example |
|------|------------|---------|
| **Documentation** | kebab-case.md | `power-specifications.md` |
| **Code Files** | snake_case.ext | `can_protocol.c` |
| **Headers** | snake_case.h | `dl_os_types.h` |
| **Directories** | kebab-case | `reference-designs/` |

---

## 5. Cross-Reference Standards

### 5.1 Internal Reference Format
- **Chapters:** "Chapter N" or "Section N.M"
- **Tables:** "Table N.M" (chapter.sequence)
- **Figures:** "Figure N.M" (chapter.sequence)
- **Equations:** "Equation N.M" (chapter.sequence)
- **Code Listings:** "Listing N.M" (chapter.sequence)

### 5.2 External Standard References
| Standard | Abbreviation | Full Citation Format |
|----------|--------------|----------------------|
| **ISO 11898-2** | - | ISO 11898-2:2016 Road vehicles — Controller area network (CAN) |
| **USB-C PD** | PD 3.1 | USB Power Delivery Specification Revision 3.1 |
| **CERN-OHL** | CERN-OHL-P-2.0 | CERN Open Hardware License Version 2 - Permissive |
| **RFC 8949** | - | RFC 8949: Concise Binary Object Representation (CBOR) |

---

## 6. Glossary Integration Rules

### 6.1 Term Definition Requirements
- **First Use:** Define acronyms on first use in each chapter
- **Ambiguous Terms:** Always include context-specific definitions
- **Technical Precision:** Use internationally accepted definitions where available
- **Cross-References:** Link to main glossary (Appendix D)

### 6.2 Consistency Checking
- **Automated Tools:** Use terminology validation scripts
- **Review Process:** All documents reviewed for terminology consistency
- **Version Control:** Track terminology changes in revision history

---

## 7. Legacy Term Migration

### 7.1 Deprecated Terms and Replacements
| Deprecated | Replacement | Migration Rule |
|------------|-------------|----------------|
| DL-CS | DL-OS | Global search and replace |
| DL-OCS | DL-OS | Global search and replace |
| Master/Slave | Host/Client | Context-sensitive replacement |
| Socket | Slot | Hardware context only |
| Port | Slot | Hardware context only |

### 7.2 Migration Timeline
- **Phase 1:** Update all core documents (this conversion)
- **Phase 2:** Update all example code and references
- **Phase 3:** Update external documentation and websites
- **Complete by:** DL-OS v2.0 release

---

## 8. Quality Assurance

### 8.1 Validation Checklist
- [ ] All DL-CS/DL-OCS instances converted to DL-OS
- [ ] RFC 2119 keywords used consistently
- [ ] Units specified with appropriate precision
- [ ] Cross-references use standard format
- [ ] No deprecated terms in new content

### 8.2 Maintenance Procedures
- **Quarterly Review:** Check for terminology drift
- **Version Updates:** Update glossary with new terms
- **External Sync:** Align with updated industry standards
- **Documentation:** Record all terminology decisions

---

**Note:** This guide SHALL be used as the authoritative reference for all DL-OS documentation. All contributors MUST follow these conventions to ensure consistency and professionalism in the standard.
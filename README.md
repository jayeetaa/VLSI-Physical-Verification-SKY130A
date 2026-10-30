# VLSI Physical Verification Using SKY130A PDK

## Project Overview
This repository documents my hands-on VLSI physical verification learning and CMOS inverter design using the open-source SKY130A Process Design Kit (PDK).

The project includes environment setup, open-source EDA tools, schematic design files, SPICE simulation outputs, and ongoing layout development.

## 0. Theory — SKY130A PDK and Open-Source EDA Flow

### 0.1 SKY130A Process Design Kit
SKY130A is an open-source 130 nm CMOS process design kit. It provides transistor models, physical design rules, technology files, and libraries required for circuit design and verification.

### 0.2 PDK Libraries
- SPICE models: Electrical behavior of transistors
- Technology files: Physical layers and layout design rules
- Device libraries: Technology-specific transistor definitions
- LVS setup files: Rules for comparing schematic and layout netlists

### 0.3 Open-Source EDA Workflow
1. Xschem — CMOS inverter schematic design
2. NGSpice — Pre-layout circuit simulation
3. Magic VLSI — Physical layout design
4. DRC — Design Rule Checking
5. Netgen — Layout Versus Schematic verification
6. NGSpice — Post-layout simulation

## 1. Environment Setup

### 1.1 System Information
- Operating System: Ubuntu 22.04.5 LTS
- Development Environment: Linux
- Project Directory: Physical_Verification_SKY130A

### 1.2 EDA Tools

| Tool | Purpose | Status |
|---|---|---|
| Magic VLSI | Layout design and DRC | Installed |
| Xschem | Schematic design | Installed |
| Netgen | LVS verification | Installed |
| NGSpice | Circuit simulation | Installed |
| Git | Version control | Installed |
| SKY130A PDK | Process technology | Installed |

### 1.3 Tool Verification Commands
```bash
lsb_release -a
which magic
which xschem
which netgen
which ngspice
git --version
```

## 2. CMOS Inverter Design

### 2.1 Working Principle
A CMOS inverter consists of PMOS and NMOS transistors.

- Input LOW: PMOS ON, NMOS OFF, output HIGH
- Input HIGH: PMOS OFF, NMOS ON, output LOW

### 2.2 Schematic Design — Xschem
The local project includes CMOS inverter schematic and symbol files created during development.

### 2.3 SPICE Simulation
The project contains a SPICE simulation file and waveform output files.

Files:
- inverter.spice
- inverter_waveform.txt
- inverter_waveform.png

Simulation results are being reviewed and documented.

### 2.4 Magic Layout — Work in Progress
Intermediate Magic layout files have been saved. The physical layout is not yet finalized or verified.

## 3. Current Project Status

| Stage | Progress |
|---|---|
| Environment setup | Completed |
| EDA tool installation | Completed |
| CMOS inverter schematic files | Created |
| Simulation output files | Generated |
| Final physical layout | In progress |
| DRC sign-off | Pending |
| LVS verification | Pending |
| Post-layout simulation | Pending |

## 4. Challenges and Learning
- Setting up open-source EDA tools on Ubuntu
- Understanding SKY130A technology files and device libraries
- Creating CMOS inverter schematic and symbol files
- Working with SPICE simulation and Magic layout files

## 5. Future Work
1. Confirm SKY130A PDK integration
2. Review the schematic and simulation results
3. Complete the CMOS inverter physical layout
4. Perform DRC
5. Perform LVS using Netgen
6. Run post-layout simulation

## 6. References
- SKY130A PDK documentation
- Magic VLSI documentation
- Xschem documentation
- Netgen documentation
- NGSpice documentation

---
**Project Status: In Progress**

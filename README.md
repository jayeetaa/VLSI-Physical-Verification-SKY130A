
# VLSI Physical Verification Using SKY130A PDK

### CMOS Inverter Design and Physical Verification Using Open-Source EDA Tools

**Author:** Jayeetaa Yeddanapalli  
**Technology:** SKY130A 130 nm CMOS PDK  
**Tools:** Xschem | NGSpice | Magic VLSI | Netgen | Git  
**Operating System:** Ubuntu 22.04.5 LTS 

---

## Project Overview

This repository documents my hands-on VLSI physical verification project using the open-source SKY130A Process Design Kit (PDK).

The project focuses on designing a CMOS inverter, performing pre-layout simulation, developing the transistor-level physical layout, and preparing the circuit for Design Rule Checking (DRC), Layout Versus Schematic (LVS) verification, and post-layout simulation.

The project also documents environment configuration, installation and integration of open-source EDA tools, debugging challenges, intermediate design files, and practical learning outcomes.

### Project Objectives

1. Understand the SKY130A Process Design Kit.
2. Configure the Linux-based VLSI design environment.
3. Install and verify open-source EDA tools.
4. Design a CMOS inverter schematic using Xschem.
5. Generate the SPICE netlist.
6. Perform pre-layout transient simulation using NGSpice.
7. Create the CMOS inverter physical layout using Magic VLSI.
8. Verify layout geometry using DRC.
9. Extract the layout netlist.
10. Perform LVS verification using Netgen.
11. Perform post-layout simulation and compare the results.

---

## 0. Theory — SKY130A PDK and Open-Source EDA Flow

### 0.1 SKY130A Process Design Kit

The SKY130A PDK is an open-source 130 nm CMOS process design kit.

It provides the technology-specific resources required for integrated circuit design, simulation, layout, and verification.

The PDK includes:

- SPICE transistor models
- Physical technology files
- Design rules
- Device libraries
- Layout extraction information
- LVS configuration files

### 0.2 SKY130A PDK Libraries

| Library | Purpose |
|---|---|
| SPICE Models | Electrical behavior of MOS transistors |
| Technology Files | Physical layers and layout rules |
| Device Libraries | Technology-specific NFET and PFET devices |
| Xschem Libraries | Schematic symbols |
| Magic Technology Files | Physical layout and DRC |
| Netgen Setup Files | LVS verification |
| NGSpice Models | Circuit simulation |

### 0.3 SKY130A Physical Layers

The physical layout contains semiconductor and interconnect layers.

Important structures include:

- N-well
- Diffusion regions
- Polysilicon gates
- Local interconnect
- Contacts
- Metal1
- Metal2
- Vias
- Substrate and well connections

These layers are used to construct transistors and connect their terminals electrically.

### 0.4 Open-Source EDA Workflow

The design and verification workflow followed in this project is:

```text
SKY130A PDK Configuration
          |
          v
Xschem Schematic Design
          |
          v
SPICE Netlist Generation
          |
          v
NGSpice Pre-Layout Simulation
          |
          v
Magic VLSI Physical Layout
          |
          v
Design Rule Checking
          |
          v
Layout Netlist Extraction
          |
          v
Netgen LVS Verification
          |
          v
NGSpice Post-Layout Simulation
          |
          v
Results and Documentation
```

---

## 1. Environment Setup

### 1.1 System Information

The project was developed using Ubuntu Linux.

| Parameter | Configuration |
|---|---|
| Operating System | Ubuntu 22.04.5 LTS |
| Development Environment | Linux |
| RAM | 10 GiB |
| Swap | 4 GiB |
| CPU Cores | 4 |
| Disk Size | 59 GiB |
| Technology | SKY130A |
| Project Directory | Physical_Verification_SKY130A |

### 1.2 System Verification

The following commands were used to inspect the development environment:

```bash
lsb_release -a
uname -a
free -h
df -h /
nproc
```

These commands provide operating system information, memory availability, disk usage, and CPU details.

### 1.3 Git Installation and Verification

Git is used for version control and GitHub project documentation.

```bash
sudo apt install git -y
git --version
```

### 1.4 EDA Tools Used

| Tool | Purpose | Status |
|---|---|---|
| Magic VLSI | Physical layout and DRC | Installed |
| Xschem | Schematic design | Installed |
| Netgen | LVS verification | Installed |
| NGSpice | Circuit simulation | Installed |
| Git | Version control | Installed |
| SKY130A PDK | Process technology | Installed |

### Screenshot 1 — EDA Tool Verification

<img width="496" alt="EDA Tool Verification" src="https://github.com/user-attachments/assets/80b6257a-7bde-440d-8dbc-3e0677f92ad3" />

---

## 2. Open-Source EDA Tool Configuration

### 2.1 Magic VLSI

Magic VLSI is an open-source layout editor used for physical IC design and design rule checking.

The installed Magic executable is located at:

```bash
/usr/local/bin/magic
```

Verification commands:

```bash
which magic
magic --version
```

### 2.2 Xschem

Xschem is used to create transistor-level circuit schematics and generate SPICE netlists.

Verification commands:

```bash
which xschem
xschem --version
xschem
```

### 2.3 Netgen

Netgen is used for Layout Versus Schematic verification.

It compares the extracted physical layout netlist with the reference schematic netlist.

```bash
which netgen
netgen --version
```

### 2.4 NGSpice

NGSpice is used for transient simulation and waveform analysis.

```bash
which ngspice
ngspice --version
```

### 2.5 SKY130A PDK Integration

The SKY130A PDK was configured using Open_PDKs.

Local PDK directory:

```bash
/home/jayee/open_pdks/sky130/sky130A/
```

Important technology resources:

**Magic Technology File**

```text
/home/jayee/open_pdks/sky130/sky130A/libs.tech/magic/sky130A.tech
```

**Netgen LVS Setup File**

```text
/home/jayee/open_pdks/sky130/sky130A/libs.tech/netgen/sky130A_setup.tcl
```

**NGSpice Model Library**

```text
/home/jayee/open_pdks/sky130/sky130A/libs.tech/ngspice/sky130.lib.spice
```

### 2.6 Launching Magic with SKY130A

The following command was used:

```bash
magic -T /home/jayee/open_pdks/sky130/sky130A/libs.tech/magic/sky130A.tech -d OGL
```

The OpenGL display driver was used after encountering a display-related issue with the XR driver.

---

## 3. Lab 1 — CMOS Inverter Design

### 3.1 CMOS Inverter Working Principle

A CMOS inverter is a basic digital logic circuit consisting of two complementary MOS transistors:

- PMOS transistor as the pull-up device
- NMOS transistor as the pull-down device

The inverter produces an output opposite to its input.

| Input | PMOS | NMOS | Output |
|---|---|---|---|
| LOW (0) | ON | OFF | HIGH (1) |
| HIGH (1) | OFF | ON | LOW (0) |

The inverter operates with a nominal supply voltage of 1.8 V.

### 3.2 Transistor Specifications

The intended transistor parameters are:

| Parameter | NMOS (M1) | PMOS (M2) |
|---|---|---|
| Device Model | sky130_fd_pr__nfet_01v8 | sky130_fd_pr__pfet_01v8 |
| Width | 4.5 µm | 3 µm |
| Length | 0.18 µm | 0.18 µm |
| Target Fingers | 3 | 3 |
| Multiplicity | 1 | 1 |
| Body Connection | VSS | VDD |

**Note:** An earlier generated schematic netlist contained a PMOS finger-count discrepancy. The final transistor parameters must be checked before LVS sign-off.

### 3.3 CMOS Inverter Schematic — Xschem

The CMOS inverter schematic was developed using Xschem and SKY130A transistor models.

The schematic contains four external signals:

- VDD — Power supply
- VSS — Ground
- IN — Input signal
- OUT — Output signal

The PMOS and NMOS gates are connected to the common input.

Their drains form the common output.

The PMOS source and body connect to VDD, while the NMOS source and body connect to VSS.

### Screenshot 2 — CMOS Inverter Schematic

<img width="900" alt="CMOS Inverter Schematic" src="https://github.com/user-attachments/assets/41ba6d24-2880-4715-81ce-ca651fdc993c" />

### 3.4 Schematic and Symbol Files

The project includes schematic and symbol files created during development.

Examples:

```text
Inverter.sch
Inverter.sym
jayee_inverter.sch
jayee_inverter_tb.sch
```

These files support schematic editing, symbol representation, and testbench development.

---

## 4. Pre-Layout Simulation — NGSpice

### 4.1 Objective

The objective of pre-layout simulation is to evaluate the electrical behavior of the CMOS inverter before physical layout implementation.

### 4.2 Simulation Configuration

The simulation uses:

- Supply voltage: 1.8 V
- Pulse input signal
- SKY130A transistor models
- Output load capacitance
- Transient analysis

### 4.3 SPICE Simulation Files

The following files were generated during development:

```text
simulation/inverter.spice
simulation/inverter_waveform.txt
simulation/inverter_waveform.png
```

### 4.4 Running the Simulation

From the simulation directory:

```bash
ngspice inverter.spice
```

### 4.5 Expected Inverter Behavior

For a correctly connected CMOS inverter:

- Input HIGH produces output LOW.
- Input LOW produces output HIGH.
- The output waveform should be complementary to the input waveform.

### Screenshot 3 — SPICE Simulation

<img width="900" alt="SPICE Simulation" src="https://github.com/user-attachments/assets/39731523-d688-4c88-96dd-7fa20c22e3ab" />

### Screenshot 4 — Simulation Development

<img width="900" alt="Simulation Development" src="https://github.com/user-attachments/assets/e5889b74-945d-4359-857c-3856816fe934" />

### Screenshot 5 — Simulation Output

<img width="650" alt="Simulation Output" src="https://github.com/user-attachments/assets/40ce2e57-de9c-4347-a21f-44fb773abbaf" />

### 4.6 Simulation Progress

The pre-layout SPICE simulation files and waveform outputs were generated and saved.

These results form the basis for comparing the circuit's behavior with the post-layout simulation after physical verification.

---

## 5. Physical Layout Design — Magic VLSI

### 5.1 Objective

The objective of physical layout design is to implement the CMOS inverter using SKY130A physical layers.

The layout must represent the MOS transistors and their electrical connections.

### 5.2 Transistor Placement

The layout development followed the arrangement:

- PMOS transistor positioned toward the top
- NMOS transistor positioned toward the bottom
- VDD power rail near the PMOS
- VSS ground rail near the NMOS
- Common gate routing for IN
- Common drain routing for OUT

### 5.3 Layout Connections

The required circuit connections are:

| Terminal | Connection |
|---|---|
| PMOS Source | VDD |
| PMOS Body | VDD |
| NMOS Source | VSS |
| NMOS Body | VSS |
| PMOS Gate | IN |
| NMOS Gate | IN |
| PMOS Drain | OUT |
| NMOS Drain | OUT |

### 5.4 Magic Layout Development

The physical layout was developed using Magic VLSI with the SKY130A technology file.

Work included:

1. Loading SKY130A transistor device cells.
2. Inspecting NFET and PFET physical layers.
3. Positioning transistor instances.
4. Creating power rail connections.
5. Working on gate and drain routing.
6. Adding and adjusting metal interconnections.
7. Working with VDD, VSS, IN, and OUT labels.
8. Inspecting layout geometry and connectivity.

### Screenshot 6 — Initial Magic Layout Development

<img width="428" alt="Initial Magic Layout" src="https://github.com/user-attachments/assets/0113ad2a-2153-4e70-ab2b-d56e56ae93a2" />

### Screenshot 7 — Magic Layout Progress

<img width="807" alt="Magic Layout Progress" src="https://github.com/user-attachments/assets/44bbebbe-252e-436f-b926-baeeb2df60bd" />

### 5.5 Saved Magic Layout Files

Several working versions were created during development.

```text
layout/inverter.mag

layout_final/Inverter_Routed.mag

layout_final/Inverter_Final.mag

layout_final/Inverter_Clean.mag
```

These files represent different stages of layout development and debugging.

The file names do not indicate completed DRC or LVS sign-off.

### 5.6 Opening the Saved Magic Layout

Open Ubuntu terminal:

```bash
cd ~/Physical_Verification_SKY130A/Lab1_CMOS_Inverter/layout_final
```

Launch Magic:

```bash
magic -T /home/jayee/open_pdks/sky130/sky130A/libs.tech/magic/sky130A.tech -d OGL Inverter_Clean.mag
```

Inside the Magic Tcl console:

```tcl
expand
zoom full
```

### 5.7 Layout Routing

Metal1 was used for local routing and power rail connections.

A Metal2 jumper was explored for crossing a routing obstruction.

The routing approach involves:

```text
Metal1
  |
 Via1
  |
Metal2
  |
 Via1
  |
Metal1
```

This approach allows a signal to cross over another metal route without directly shorting the two nets, provided the layout follows the technology design rules.

### 5.8 Layout Debugging

During layout development, several challenges were encountered.

**Problem 1 — Unconnected Device Terminals**

Some extracted transistor terminals appeared as separate nets.

Examples included:

```text
XM1/S1
XM1/S2
XM1/G0
XM1/G1
```

These observations required inspection of transistor terminal connectivity.

**Problem 2 — Routing Conflicts**

Some metal connections needed rerouting to avoid unintended shorts.

**Problem 3 — Floating Geometry**

An extracted layout version contained a floating parasitic capacitor, indicating that additional layout inspection was necessary.

**Problem 4 — Magic Interface and Cell Loading**

Challenges included:

- Loading saved layout files
- Expanding transistor cells
- Selecting physical layers
- Working with the Tcl command console
- Inspecting port labels
- Managing intermediate layout versions

### 5.9 Layout Progress

The CMOS inverter physical layout has been developed through several iterations.

The layout still requires final connectivity checks and verification before sign-off.

---

## 6. Design Rule Checking (DRC)

### 6.1 Objective

Design Rule Checking verifies whether the physical layout satisfies the geometric constraints defined by the SKY130A PDK.

DRC helps identify:

- Minimum spacing violations
- Minimum width violations
- Incorrect layer overlaps
- Contact and via geometry issues
- Other technology-specific layout violations

### 6.2 DRC Commands

Inside the Magic Tcl console:

```tcl
drc check
drc count
drc why
```

### 6.3 DRC Verification Procedure

1. Open the required Magic layout.
2. Expand the device cells.
3. Run the DRC check.
4. Inspect reported violations.
5. Correct layout geometry.
6. Run DRC again.
7. Record the final error count.

### 6.4 DRC Status

DRC-related layout inspection and debugging have been performed.

Earlier layout files contained reported error geometry.

**Final zero-error DRC sign-off has not yet been confirmed.**

The final DRC result will be documented with its corresponding layout file and verification screenshot.

---

## 7. Layout Extraction

### 7.1 Objective

Layout extraction converts the physical layout into an electrical representation containing recognized devices and their connections.

The extracted netlist is used for LVS comparison.

### 7.2 Extraction Commands

Inside Magic:

```tcl
extract all
ext2spice lvs
ext2spice
```

### 7.3 Extracted Layout Files

During development, extracted files included:

```text
Inverter_Routed.ext
Inverter_Routed.spice

Inverter_Final.ext
Inverter_Final.spice
```

### 7.4 Extraction Observations

Intermediate extraction results showed separate transistor terminal nets and connectivity issues.

These observations helped identify areas requiring additional routing and verification.

---

## 8. Layout Versus Schematic (LVS) — Netgen

### 8.1 Objective

LVS verifies whether the extracted physical layout is electrically equivalent to the reference schematic.

The comparison checks:

- Transistor types
- Device parameters
- Number of devices
- Net connectivity
- Power and ground connections
- Input and output connections

### 8.2 Netgen Configuration

The SKY130A LVS setup file is located at:

```text
/home/jayee/open_pdks/sky130/sky130A/libs.tech/netgen/sky130A_setup.tcl
```

### 8.3 LVS Procedure

1. Generate the schematic SPICE netlist using Xschem.
2. Extract the physical layout SPICE netlist using Magic.
3. Verify the subcircuit names.
4. Run Netgen LVS.
5. Inspect the comparison report.
6. Identify unmatched devices or nets.
7. Correct connectivity problems.
8. Repeat verification.

### 8.4 Example Netgen Command

The following is a command template. The actual netlist paths and subcircuit names must be checked before running it.

```bash
netgen -batch lvs \
"layout_final/Inverter_Final.spice Inverter_Final" \
"xschem/Inverter.spice Inverter" \
/home/jayee/open_pdks/sky130/sky130A/libs.tech/netgen/sky130A_setup.tcl \
lvs_report.log
```

### 8.5 LVS Debugging

The following issues were identified during development:

- Multiple extracted NFET terminals
- Possible disconnected source/drain regions
- Gate connectivity requiring inspection
- Power and ground net consistency
- Differences between intended and generated transistor parameters
- Potential floating layout nodes

### 8.6 LVS Status

LVS preparation and layout connectivity debugging are in progress.

**A final successful "Circuits match uniquely" result has not yet been established.**

---

## 9. Post-Layout Simulation — NGSpice

### 9.1 Objective

Post-layout simulation evaluates the electrical behavior of the circuit using the extracted layout netlist.

It can help analyze the effects of layout-related parasitic capacitance and resistance.

### 9.2 Planned Procedure

1. Complete layout verification.
2. Extract the corrected circuit netlist.
3. Prepare the post-layout testbench.
4. Load the SKY130A transistor models.
5. Run transient simulation using NGSpice.
6. Inspect input and output waveforms.
7. Compare the results with pre-layout simulation.

### 9.3 Pre-Layout and Post-Layout Comparison

| Parameter | Pre-Layout | Post-Layout |
|---|---|---|
| Supply Voltage | 1.8 V | 1.8 V target |
| Input Signal | Pulse | Equivalent pulse |
| Circuit Behavior | Simulation outputs generated | Pending |
| Layout Parasitics | Not extracted from layout | To be included |
| Propagation Delay | To be measured | Pending |
| Verification | Under review | Pending |

### 9.4 Current Status

Post-layout simulation is planned after layout connectivity and verification are completed.

---

## 10. Project Progress and Results

| Stage | Status |
|---|---|
| Ubuntu Environment Setup | Completed |
| Magic VLSI Installation | Completed |
| Xschem Installation | Completed |
| Netgen Installation | Completed |
| NGSpice Installation | Completed |
| SKY130A PDK Configuration | Completed |
| CMOS Inverter Schematic | Created |
| SPICE Netlist Generation | Completed |
| Pre-Layout Simulation Files | Generated |
| Magic Physical Layout | Working versions created |
| Layout Routing | Debugging |
| DRC Verification | Final sign-off pending |
| Layout Extraction | Intermediate netlists generated |
| LVS Verification | Pending |
| Post-Layout Simulation | Pending |
| GitHub Documentation | In Progress |

---

## 11. Challenges Faced and Solutions Explored

### 11.1 EDA Tool Installation

Setting up open-source EDA tools required configuring software dependencies, technology files, and library paths.

### 11.2 SKY130A Integration

The technology files and device libraries were configured for use with Magic, Xschem, Netgen, and NGSpice.

### 11.3 Magic Display Driver Issue

An XR display issue was encountered during Magic launch.

The OpenGL driver was used:

```bash
magic -T /home/jayee/open_pdks/sky130/sky130A/libs.tech/magic/sky130A.tech -d OGL
```

### 11.4 Transistor Placement and Routing

Developing the layout required understanding physical device terminals, metal layers, contacts, and vias.

### 11.5 Multi-Finger Transistor Connectivity

Extracted transistor terminals appeared as separate nets during layout debugging.

This highlighted the importance of connecting all required transistor terminals correctly.

### 11.6 Layout Verification

The project demonstrated that a visually complete layout is not necessarily electrically correct.

DRC and LVS are essential for validating physical geometry and circuit connectivity.

---

## 12. Key Learning Outcomes

Through this project, I gained practical experience in:

1. Linux-based VLSI design environments.
2. SKY130A PDK configuration.
3. Open-source EDA tool integration.
4. CMOS inverter schematic design.
5. SPICE netlist generation.
6. Transient simulation using NGSpice.
7. Physical transistor layout using Magic VLSI.
8. Metal routing and via connections.
9. Design rule inspection.
10. Layout netlist extraction.
11. LVS debugging concepts.
12. Technical documentation using GitHub.

---

## 13. Project Directory Structure

The following structure represents the local working project. Not all files have been uploaded to GitHub yet.

```text
Physical_Verification_SKY130A/
|
└── Lab1_CMOS_Inverter/
    |
    ├── xschem/
    |   ├── Inverter.sch
    |   ├── Inverter.sym
    |   └── jayee_inverter_tb.sch
    |
    ├── simulation/
    |   ├── inverter.spice
    |   ├── inverter_waveform.txt
    |   └── inverter_waveform.png
    |
    ├── layout/
    |   └── inverter.mag
    |
    └── layout_final/
        ├── Inverter_Routed.mag
        ├── Inverter_Final.mag
        └── Inverter_Clean.mag
```

Additional extracted netlists, intermediate layouts, and debugging files were also created during development.

---

## 14. Future Work

The remaining tasks are:

1. Perform Netgen LVS verification.
2. Resolve any netlist mismatches.
3. Compare pre-layout and post-layout waveforms.
4. Upload final project files and verification screenshots.

---

## Conclusion

This project documents the practical development of a CMOS inverter using the SKY130A PDK and open-source EDA tools.

The work includes environment setup, schematic design, SPICE simulation, physical layout implementation, layout extraction, and debugging.

The project has provided hands-on experience in understanding the relationship between circuit schematics and transistor-level physical layouts.

Further work will focus on completing DRC and LVS sign-off, performing post-layout simulation, and documenting the final verification results.

---

### Project Information

**Project:** VLSI Physical Verification Using SKY130A PDK  
**Lab:** CMOS Inverter Physical Verification  
**Author:** Jayeetaa Yeddanapalli  
**GitHub:** [jayeetaa](https://github.com/jayeetaa)  
**Repository:** [VLSI-Physical-Verification-SKY130A](https://github.com/jayeetaa/VLSI-Physical-Verification-SKY130A)

**Project Status: 90%**

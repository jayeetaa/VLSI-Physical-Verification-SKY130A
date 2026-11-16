
# VLSI Physical Verification Using SKY130A PDK

### CMOS Inverter Design, Physical Layout Implementation & Verification Using Open-Source EDA Tools

<p align="center">
  <img src="https://img.shields.io/badge/Technology-SKY130A-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Process-130nm-green?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Design-CMOS%20Inverter-orange?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Platform-Ubuntu%2022.04-purple?style=for-the-badge" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Xschem-Schematic%20Design-blue" />
  <img src="https://img.shields.io/badge/NGSpice-Circuit%20Simulation-red" />
  <img src="https://img.shields.io/badge/Magic-Physical%20Layout-yellow" />
  <img src="https://img.shields.io/badge/Netgen-LVS%20Verification-brightgreen" />
</p>

---

## 📌 Project Overview

This project demonstrates the transistor-level design, physical implementation, and verification of a **CMOS Inverter using the SKY130A 130nm Process Design Kit (PDK)**.

The project follows a practical VLSI design and physical verification workflow using open-source Electronic Design Automation (EDA) tools.

Starting from schematic development, the implementation progresses through SPICE netlist generation, pre-layout transient simulation, physical layout design, Design Rule Checking (DRC), parasitic extraction, Layout Versus Schematic (LVS) verification, and post-layout simulation.

The primary objective is to understand how a transistor-level CMOS circuit is translated into a physical layout and how its electrical connectivity and geometrical correctness are verified.

### Project Highlights

- Designed a CMOS inverter using SKY130A PMOS and NMOS transistor models.
- Developed the transistor-level schematic using Xschem.
- Generated SPICE netlists and performed pre-layout simulation using NGSpice.
- Implemented the physical layout using Magic VLSI.
- Performed Design Rule Checking using SKY130A technology rules.
- Extracted layout-related parasitic information.
- Performed Layout Versus Schematic verification using Netgen.
- Conducted post-layout transient simulation using the extracted SPICE netlist.
- Analyzed the differences between pre-layout and post-layout simulation.

---

## 🎯 Project Objectives

- Understand the working principle of a CMOS inverter.
- Design a transistor-level CMOS inverter schematic using Xschem.
- Verify circuit functionality through pre-layout simulation.
- Implement the physical layout using Magic VLSI.
- Understand SKY130A fabrication layers and metal interconnections.
- Perform DRC to examine layout geometrical constraints.
- Perform LVS to compare the physical layout with the reference schematic.
- Extract parasitic information from the physical layout.
- Perform post-layout simulation using NGSpice.
- Understand the importance of physical verification in VLSI design.

---

## 🧰 Technology Stack

| Tool / Technology | Application |
|:---|:---|
| SKY130A PDK | 130nm CMOS process technology |
| Xschem | Transistor-level schematic design |
| NGSpice | Pre-layout and post-layout circuit simulation |
| Magic VLSI | Physical layout design, DRC and parasitic extraction |
| Netgen | Layout Versus Schematic verification |
| Ubuntu 22.04.5 LTS | Linux development environment |
| Git | Version control |
| GitHub | Project hosting and documentation |

---

## 🔄 Complete VLSI Design Flow

```text
             DESIGN SPECIFICATION
                     |
                     v
              SCHEMATIC DESIGN
                   Xschem
                     |
                     v
               SPICE NETLIST
                     |
                     v
            PRE-LAYOUT SIMULATION
                   NGSpice
                     |
                     v
           PHYSICAL LAYOUT DESIGN
                 Magic VLSI
                     |
                     v
          DESIGN RULE CHECKING (DRC)
                     |
                     v
             PARASITIC EXTRACTION
                   Magic
                     |
                     v
        LAYOUT VERSUS SCHEMATIC (LVS)
                   Netgen
                     |
                     v
            POST-LAYOUT SIMULATION
                   NGSpice
                     |
                     v
                FINAL ANALYSIS
```

---

## 1. Environment Setup & PDK Configuration

The development environment was configured using Ubuntu 22.04.5 LTS with the SKY130A PDK and the required open-source EDA tools.

### Development Environment

| Configuration | Details |
|:---|:---|
| Operating System | Ubuntu 22.04.5 LTS |
| Process Technology | SKY130A |
| Technology Node | 130nm |
| PDK | SKY130A |
| Design Tools | Xschem, NGSpice, Magic VLSI, Netgen |

### EDA Tools Verification

The installed EDA tools were checked in the Ubuntu environment to ensure that the required tools were available for the design and verification workflow.

<p align="center">
  <img src="images/tools_verification.png" width="850" alt="EDA tools verification in Ubuntu" />
</p>

### SKY130A PDK Configuration

**PDK Directory**

```bash
/home/jayee/open_pdks/sky130/sky130A/
```

**Magic Technology File**

```bash
/home/jayee/open_pdks/sky130/sky130A/libs.tech/magic/sky130A.tech
```

**Netgen Setup File**

```bash
/home/jayee/open_pdks/sky130/sky130A/libs.tech/netgen/sky130A_setup.tcl
```

**NGSpice Model File**

```bash
/home/jayee/open_pdks/sky130/sky130A/libs.tech/ngspice/sky130.lib.spice
```

---

## 2. CMOS Inverter Schematic Design Using Xschem

A CMOS inverter was designed using complementary PMOS and NMOS transistors available in the SKY130A PDK.

### Circuit Architecture

A CMOS inverter consists of two complementary MOS transistors:

| Component | Function |
|:---|:---|
| PMOS | Pull-up network |
| NMOS | Pull-down network |
| Common Gate | Input terminal (VIN) |
| Common Drain | Output terminal (VOUT) |
| VDD | Positive supply voltage (1.8 V) |
| GND | Ground reference |

### Transistor Specifications

| Parameter | PMOS | NMOS |
|:---|:---|:---|
| Device Model | `sky130_fd_pr__pfet_01v8` | `sky130_fd_pr__nfet_01v8` |
| Width (W) | 3 µm | 4.5 µm |
| Length (L) | 0.18 µm | 0.18 µm |
| Fingers (NF) | 3 | 3 |
| Multiplicity (M) | 1 | 1 |

**Supply Voltage:** 1.8 V

### Schematic Implementation

<p align="center">
  <img src="https://github.com/user-attachments/assets/26dd4afb-7867-42ad-a99f-7f6a8405fa11" width="900" alt="CMOS inverter schematic design" />
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/f7763e02-ca89-4b98-96c0-d91230d574c5" width="900" alt="CMOS inverter schematic implementation" />
</p>

The transistor-level schematic was developed in Xschem using SKY130A transistor models.

The PMOS and NMOS gates are connected to the same input signal, while their drains are connected to form the output terminal.

The PMOS source is connected to VDD, and the NMOS source is connected to GND.

This complementary transistor arrangement forms the basic CMOS inverter circuit.

---

## 3. Pre-Layout Simulation Using NGSpice

After completing the schematic design, the SPICE netlist was generated and simulated using NGSpice.

Transient analysis was performed to verify the switching behaviour of the CMOS inverter before physical layout implementation.

### Working Principle of CMOS Inverter

A CMOS inverter produces an output that is logically complementary to its input.

| Input (VIN) | PMOS | NMOS | Output (VOUT) |
|:---:|:---:|:---:|:---:|
| 0 V (LOW) | ON | OFF | 1.8 V (HIGH) |
| 1.8 V (HIGH) | OFF | ON | 0 V (LOW) |

### Pre-Layout Simulation Waveform

<p align="center">
  <img src="https://github.com/user-attachments/assets/6610b320-9576-4cb6-8d78-5ef8aa7973f3" width="900" alt="CMOS inverter pre-layout transient simulation waveform" />
</p>

### Simulation Analysis

The transient waveform demonstrates the complementary relationship between the input and output signals.

- When the input is LOW, the PMOS transistor turns ON and pulls the output towards VDD.
- When the input is HIGH, the NMOS transistor turns ON and pulls the output towards GND.
- The output waveform follows the inverted form of the input waveform.

**Observation:** The pre-layout simulation verifies the expected logical operation of the CMOS inverter.

---

## 4. Physical Layout Design Using Magic VLSI

The physical layout of the CMOS inverter was implemented using Magic VLSI with the SKY130A technology file.

The transistor-level circuit was translated into a geometrical representation using the appropriate fabrication layers and electrical interconnections.

### Important Physical Layout Layers

| Layout Layer | Purpose |
|:---|:---|
| N-Well | Provides the well region for PMOS devices |
| Active Diffusion | Defines transistor source and drain regions |
| Polysilicon | Forms the MOS transistor gates |
| Local Interconnect | Provides local electrical connections |
| Metal 1 | First-level metal routing |
| Metal 2 | Higher-level metal routing |
| Contacts | Connect diffusion or polysilicon to metal |
| Vias | Connect different metal layers |

### Layout Implementation

The PMOS and NMOS transistors were placed and interconnected to implement the required CMOS inverter topology.

The physical layout includes:

- PMOS and NMOS transistor regions.
- Common gate connections for the input.
- Drain interconnection for the output.
- Power routing through VDD.
- Ground routing through GND.
- Metal interconnections and contact structures.

### Final Routed CMOS Inverter Layout

<p align="center">
  <img src="https://github.com/user-attachments/assets/4f339ad8-8e5c-49b6-a468-7f75f4d90e73" width="950" alt="Final routed CMOS inverter physical layout in Magic VLSI" />
</p>

The final routed layout represents the physical implementation of the CMOS inverter using SKY130A process layers.

---

## 5. Design Rule Checking (DRC)

Design Rule Checking was performed using Magic VLSI to examine whether the physical layout follows the geometrical constraints specified by the SKY130A fabrication technology.

DRC is an important physical verification stage because layout geometries must satisfy technology-specific manufacturing constraints.

### DRC Checks

The layout was examined for design constraints such as:

- Minimum metal width requirements.
- Minimum spacing between layout layers.
- Contact and via enclosure requirements.
- Diffusion and polysilicon spacing.
- Metal-to-metal spacing.
- Well and active-region design rules.

### DRC Verification Result

<p align="center">
  <img src="https://github.com/user-attachments/assets/40aef60d-eda8-4722-a91f-f458f9e40c28" width="950" alt="Magic VLSI design rule checking result" />
</p>

The DRC verification output is shown above.

---

## 6. Layout Versus Schematic (LVS) Verification Using Netgen

Layout Versus Schematic verification was performed using Netgen.

LVS is used to compare the electrical connectivity of the extracted physical layout netlist against the reference schematic netlist.

The purpose of this verification is to ensure that the physical layout represents the intended transistor-level circuit.

### LVS Verification Parameters

The comparison involves:

- PMOS and NMOS device recognition.
- Transistor terminal connectivity.
- Source, drain, gate and bulk connections.
- Electrical net connectivity.
- Circuit topology and structural equivalence.

### LVS Verification Result

<p align="center">
  <img src="https://github.com/user-attachments/assets/00b2cf79-0faa-4e49-9cf2-d843a75b0817" width="850" alt="Netgen LVS verification output" />
</p>

The Netgen comparison output is included above as the LVS verification evidence.

LVS verification is essential for identifying connectivity differences between the physical layout and the reference schematic.

---

## 7. Parasitic Extraction Using Magic VLSI

After physical layout implementation, parasitic extraction was performed using Magic VLSI.

Physical interconnections introduce parasitic capacitances and resistances that can influence circuit behaviour, switching characteristics and timing.

Parasitic extraction generates an electrical representation of the physical layout that can be used for post-layout simulation.

### Extraction Process

The extraction process identifies:

- Transistor devices present in the physical layout.
- Electrical connections between devices.
- Layout-related parasitic information.
- Interconnect-related electrical effects.

### Extraction Output

The extracted SPICE netlist is used as the circuit input for post-layout simulation.

<p align="center">
  <img src="https://github.com/user-attachments/assets/434656c7-d72c-4ef4-89ca-c7d6d4fb38c3" width="650" alt="Layout extraction and post-layout simulation evidence" />
</p>

---

## 8. Post-Layout Simulation Using NGSpice

After physical layout implementation and extraction, post-layout transient simulation was performed using NGSpice.

The extracted SPICE netlist was used to simulate the inverter after physical implementation.

Unlike pre-layout simulation, post-layout simulation can account for parasitic effects included in the extracted netlist.

### Post-Layout Simulation Configuration

| Parameter | Value |
|:---|:---|
| Technology | SKY130A |
| Process Technology | 130nm |
| Supply Voltage | 1.8 V |
| Input Signal | Pulse waveform |
| Input Voltage Range | 0–1.8 V |
| Simulation Type | Transient Analysis |
| Simulator | NGSpice |
| Circuit Source | Extracted layout netlist |

### Post-Layout Simulation Execution

The post-layout testbench is executed using NGSpice.

```bash
ngspice postlayout_tb.spice
```

The input and output waveforms can be observed using:

```spice
plot v(in) v(out)
```

### Post-Layout Simulation Waveform

<p align="center">
  <img src="https://github.com/user-attachments/assets/434656c7-d72c-4ef4-89ca-c7d6d4fb38c3" width="650" alt="Post-layout simulation evidence" />
</p>

### Simulation Analysis

The post-layout simulation is used to examine the inverter response after including the extracted layout information.

The expected inverter behaviour is:

- When the input is LOW, the output becomes HIGH.
- When the input is HIGH, the output becomes LOW.
- The output maintains the complementary response of the input.

The extracted parasitic information provides a more physically representative circuit model compared with an ideal schematic-level simulation.

---

## 9. Pre-Layout vs Post-Layout Simulation

Pre-layout and post-layout simulations are important stages in the CMOS design workflow.

Pre-layout simulation verifies circuit functionality using the schematic netlist, whereas post-layout simulation evaluates the circuit using the extracted physical layout netlist.

### Comparison

| Parameter | Pre-Layout | Post-Layout |
|:---|:---|:---|
| Circuit Source | Schematic netlist | Extracted layout netlist |
| Simulator | NGSpice | NGSpice |
| Supply Voltage | 1.8 V | 1.8 V |
| Input Range | 0–1.8 V | 0–1.8 V |
| Physical Interconnect Effects | Not included from layout extraction | Included through extraction |
| Parasitic Capacitance | Not extracted from layout | Included where configured |
| Parasitic Resistance | Not extracted from layout | Included where configured |
| Analysis | Transient | Transient |

### Key Observation

Post-layout simulation provides a more physically representative view of circuit behaviour because it considers parasitic effects associated with the physical implementation.

Comparing both simulations helps understand the relationship between schematic-level circuit behaviour and physical layout effects.

---

## 10. Challenges Encountered & Learning Outcomes

### Challenges Encountered

During the implementation of this project, the following technical challenges were addressed:

- Setting up the SKY130A PDK in the Ubuntu environment.
- Configuring the required open-source EDA tools.
- Understanding the relationship between schematic connectivity and physical layout.
- Handling metal routing and layer connectivity.
- Working with contacts, vias and interconnection layers.
- Understanding layout extraction and the generated SPICE netlist.
- Learning the role of parasitic effects in post-layout simulation.

### Technical Skills Developed

Through this project, practical experience was gained in:

1. Understanding CMOS inverter operation and transistor-level design.
2. Creating schematic designs using Xschem.
3. Generating and working with SPICE netlists.
4. Performing transient simulation using NGSpice.
5. Implementing physical layouts using Magic VLSI.
6. Understanding SKY130A semiconductor fabrication layers.
7. Performing physical Design Rule Checking.
8. Comparing schematic and extracted layout netlists using Netgen.
9. Understanding parasitic extraction.
10. Performing post-layout simulation and analysis.

---

## 11. Repository Structure

The project repository is organized into the following directories:

```text
VLSI-Physical-Verification-SKY130A/
│
├── README.md
│
├── schematic/
│   ├── Inverter.sch
│   ├── Inverter.sym
│   ├── jayee_inverter.sch
│   └── jayee_inverter_tb.sch
│
├── simulation/
│   ├── inverter.spice
│   ├── inverter_waveform.txt
│   └── inverter_waveform.png
│
├── layout/
│   └── inverter.mag
│
├── layout_final/
│   ├── Inverter_Routed.mag
│   ├── Inverter_Final.mag
│   └── Inverter_Clean.mag
│
└── images/
    ├── tools_verification.png
    ├── inverter_schematic.png
    ├── prelayout_waveform.png
    ├── initial_layout.png
    ├── final_layout.png
    ├── drc_result.png
    ├── lvs_result.png
    └── postlayout_waveform.png
```

---

## 12. Final Project Summary

| Design / Verification Stage | Tool Used |
|:---|:---|
| Schematic Design | Xschem |
| SPICE Netlist Generation | Xschem |
| Pre-Layout Simulation | NGSpice |
| Physical Layout Implementation | Magic VLSI |
| Design Rule Checking | Magic VLSI |
| Parasitic Extraction | Magic VLSI |
| Layout Versus Schematic Verification | Netgen |
| Post-Layout Simulation | NGSpice |

---

## 13. Conclusion

This project demonstrates the transistor-level design and physical verification of a CMOS inverter using the SKY130A 130nm Process Design Kit and open-source VLSI EDA tools.

The implementation covers the major stages of the VLSI design workflow, beginning with schematic development using Xschem and pre-layout simulation using NGSpice.

The physical layout was implemented using Magic VLSI, followed by Design Rule Checking, parasitic extraction and Layout Versus Schematic verification using Netgen.

Finally, post-layout transient simulation was performed using the extracted SPICE netlist to study the inverter response after physical implementation.

Through this project, practical knowledge was developed in CMOS circuit design, physical layout implementation, design rule checking, layout verification, parasitic extraction and post-layout simulation.

The project provided hands-on exposure to the relationship between transistor-level circuit design and its physical implementation using an open-source VLSI design flow.

---

## 📚 References

- [SkyWater SKY130 Open-Source PDK](https://github.com/google/skywater-pdk)
- [Open_PDKs](https://github.com/RTimothyEdwards/open_pdks)
- [Xschem – Schematic Capture Tool](https://github.com/StefanSchippers/xschem)
- [Magic VLSI Layout Tool](http://opencircuitdesign.com/magic/)
- [Netgen LVS](http://opencircuitdesign.com/netgen/)
- [NGSpice Circuit Simulator](https://ngspice.sourceforge.io/)

---

## 👩‍💻 Author

**Jayeetaa Yeddanapalli**

B.Tech – Electronics and Communication Engineering

**Areas of Interest:** VLSI Design | CMOS Circuits | Physical Verification | Semiconductor Technology

<p align="left">
  <a href="https://github.com/jayeetaa">
    <img src="https://img.shields.io/badge/GitHub-jayeetaa-181717?style=for-the-badge&logo=github" />
  </a>
  <a href="https://github.com/jayeetaa/VLSI-Physical-Verification-SKY130A">
    <img src="https://img.shields.io/badge/Project-Repository-blue?style=for-the-badge&logo=github" />
  </a>
</p>

---

<p align="center">
  <b>CMOS Design • Physical Layout • Verification • Simulation</b>
  <br/>
  <i>Learning VLSI through hands-on implementation.</i>
</p>


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

This project demonstrates the design and physical verification of a **CMOS Inverter using the SKY130A 130nm Process Design Kit (PDK)**.

The implementation follows a practical transistor-level VLSI design flow using open-source Electronic Design Automation (EDA) tools.

Starting from schematic creation, the project progresses through SPICE netlist generation, pre-layout simulation, physical layout implementation, Design Rule Checking (DRC), parasitic extraction, Layout Versus Schematic (LVS) verification, and post-layout simulation.

The primary objective is to understand how a transistor-level circuit is translated into a physical layout and how its electrical and geometrical correctness is verified.

### Project Highlights

- CMOS inverter design using SKY130A NMOS and PMOS devices.
- Transistor-level schematic development using Xschem.
- SPICE netlist generation and pre-layout simulation using NGSpice.
- Physical layout implementation and routing using Magic VLSI.
- Design Rule Checking using SKY130A technology rules.
- Parasitic extraction from the physical layout.
- Layout Versus Schematic verification using Netgen.
- Post-layout circuit simulation using the extracted netlist.

---

## 🧰 Technology Stack

| Tool / Technology | Application |
|:---|:---|
| **SKY130A PDK** | 130nm CMOS process technology |
| **Xschem** | Transistor-level schematic design |
| **NGSpice** | SPICE-based circuit simulation |
| **Magic VLSI** | Physical layout design, DRC and extraction |
| **Netgen** | Layout Versus Schematic verification |
| **Ubuntu 22.04.5 LTS** | Linux development environment |
| **Git & GitHub** | Version control and project documentation |

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

The project environment was configured using Ubuntu 22.04.5 LTS with the SKY130A PDK and the required open-source EDA tools.

### Development Environment

| Configuration | Details |
|:---|:---|
| Operating System | Ubuntu 22.04.5 LTS |
| Process Technology | SKY130A |
| Technology Node | 130nm |
| PDK | SKY130A |
| Design Tools | Xschem, NGSpice, Magic, Netgen |

### EDA Tools Verification

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

## 2. CMOS Inverter Schematic Design

A CMOS inverter was designed using complementary NMOS and PMOS transistors available in the SKY130A PDK.

### Circuit Architecture

| Component | Function |
|:---|:---|
| PMOS | Pull-up network |
| NMOS | Pull-down network |
| Common Gate | Input terminal (VIN) |
| Common Drain | Output terminal (VOUT) |
| VDD | Positive supply (1.8 V) |
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

The transistor-level schematic was developed in Xschem using SKY130A device models.

The PMOS and NMOS gates share the same input, while their drains are connected to form the output. The PMOS source is connected to VDD and the NMOS source is connected to GND.

---

## 3. Pre-Layout Simulation Using NGSpice

After completing the schematic, the SPICE netlist was generated and simulated using NGSpice.

Transient analysis was performed to examine the switching characteristics of the CMOS inverter.

### Operating Principle

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

The transient waveform illustrates the relationship between the input and output signals.

- When the input is LOW, the PMOS transistor conducts and the output is pulled towards VDD.
- When the input is HIGH, the NMOS transistor conducts and the output is pulled towards GND.
- The output follows the inverted form of the input signal.

This stage verifies the expected logical switching behaviour before physical layout implementation.

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

The layout includes:

- PMOS and NMOS transistor regions.
- Gate connections for the common input.
- Drain interconnection for the output.
- Power routing through VDD.
- Ground routing through GND.
- Metal interconnections and contact structures.

### Final Routed Layout

<p align="center">
  <img src="https://github.com/user-attachments/assets/4f339ad8-8e5c-49b6-a468-7f75f4d90e73" width="950" alt="Final routed CMOS inverter physical layout in Magic VLSI" />
</p>

The final routed layout represents the physical implementation of the inverter using the SKY130A process layers.

---

## 5. Design Rule Checking (DRC)

Design Rule Checking was performed using Magic VLSI to examine whether the physical layout satisfies the geometrical constraints specified by the SKY130A fabrication technology.

### DRC Checks

The layout was examined for the following design constraints:

- Minimum metal width requirements.
- Minimum spacing between layout layers.
- Contact and via enclosure requirements.
- Diffusion and polysilicon spacing.
- Metal-to-metal spacing.
- Well and active-region design rules.

### DRC Verification

<p align="center">
  <img src="https://github.com/user-attachments/assets/40aef60d-eda8-4722-a91f-f458f9e40c28" width="950" alt="Magic VLSI design rule checking result" />
</p>

DRC is an essential physical verification stage because geometrically incorrect layouts may not satisfy the fabrication requirements.

---

## 6. Layout Versus Schematic (LVS) Verification

Layout Versus Schematic verification was performed using Netgen.

LVS compares the extracted electrical connectivity of the physical layout against the reference schematic netlist.

### Verification Parameters

The comparison involves:

- Device recognition and matching.
- NMOS and PMOS transistor identification.
- Source, drain, gate and bulk terminal connectivity.
- Electrical net connectivity.
- Circuit topology and structural equivalence.

### LVS Verification Result

<p align="center">
  <img src="https://github.com/user-attachments/assets/00b2cf79-0faa-4e49-9cf2-d843a75b0817" width="750" alt="Netgen LVS verification output" />
</p>

**LVS Status:** Update with the exact comparison result reported by Netgen.

LVS verification helps establish whether the physical layout electrically represents the intended schematic.

---

## 7. Parasitic Extraction & Post-Layout Simulation

After physical layout implementation, parasitic extraction was performed to obtain the electrical parasitic information associated with the layout.

Physical interconnections introduce parasitic resistance and capacitance, which can influence the timing and switching behaviour of a circuit.

### Pre-Layout vs Post-Layout Simulation

| Parameter | Pre-Layout | Post-Layout |
|:---|:---|:---|
| Circuit Source | Schematic netlist | Extracted layout netlist |
| Physical Interconnect Effects | Not included | Included through extraction |
| Parasitic Resistance | Not extracted from layout | Extracted where configured |
| Parasitic Capacitance | Not extracted from layout | Extracted where configured |
| Simulation Tool | NGSpice | NGSpice |

### Post-Layout Simulation Waveform

<p align="center">
  <img src="https://github.com/user-attachments/assets/0d32e778-3861-474b-b934-a6297751344c" width="950" alt="CMOS inverter post-layout simulation waveform" />
</p>

The extracted netlist was used for post-layout simulation to examine the inverter response after physical implementation.

This stage provides insight into the effect of physical interconnect parasitics on circuit behaviour.

---

## 8. Challenges & Learning Outcomes

### Technical Skills Developed

- Configuring open-source EDA tools in a Linux environment.
- Understanding and working with the SKY130A PDK.
- Creating transistor-level CMOS schematics using Xschem.
- Generating and debugging SPICE netlists.
- Performing transient circuit simulations using NGSpice.
- Understanding CMOS inverter switching characteristics.
- Implementing physical layouts using Magic VLSI.
- Understanding semiconductor layout layers and interconnections.
- Debugging metal routing, contacts and via connections.
- Performing physical Design Rule Checking.
- Comparing schematic and layout netlists using Netgen.
- Understanding parasitic extraction and post-layout simulation.

### Challenges Encountered

- Setting up the SKY130A PDK and configuring the EDA environment.
- Understanding the relationship between schematic connectivity and physical layout.
- Handling metal routing and layer connectivity.
- Resolving layout-related issues during physical implementation.
- Understanding the importance of parasitic effects in post-layout analysis.

---

## 9. Repository Structure

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

## 10. Conclusion

This project demonstrates the practical implementation of a CMOS inverter using the SKY130A 130nm process technology and open-source VLSI EDA tools.

The work covers the major stages of the transistor-level design and physical verification workflow, including schematic development, pre-layout simulation, physical layout implementation, DRC, parasitic extraction, LVS, and post-layout simulation.

Through this implementation, I developed a practical understanding of how circuit-level designs are translated into physical layouts and how electrical and geometrical correctness are evaluated during the VLSI design process.

The project strengthened my understanding of CMOS fundamentals, physical design concepts, layout verification, and the relationship between schematic design and silicon-level implementation.

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
  **CMOS Design • Physical Layout • Verification • Simulation**
  <br/>
  <i>Learning VLSI through hands-on implementation.</i>
</p>

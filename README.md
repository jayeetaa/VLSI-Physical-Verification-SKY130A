
# VLSI Physical Verification Using SKY130A PDK

<p align="center">
  <b>CMOS Inverter Design and Physical Verification Using Open-Source EDA Tools</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Technology-SKY130A-blue">
  <img src="https://img.shields.io/badge/Node-130nm-green">
  <img src="https://img.shields.io/badge/Tools-Xschem%20%7C%20NGSpice%20%7C%20Magic%20%7C%20Netgen-orange">
  <img src="https://img.shields.io/badge/Platform-Ubuntu%2022.04-purple">
</p>

---

## 📌 Project Overview

This project demonstrates the design and physical verification of a CMOS inverter using the **SKY130A 130nm Process Design Kit (PDK)** and open-source VLSI Electronic Design Automation (EDA) tools.

The project follows the practical VLSI design flow, starting from transistor-level schematic creation and pre-layout simulation, followed by physical layout implementation, design rule checking, parasitic extraction, and layout-versus-schematic verification.

The main objective is to understand how a CMOS circuit is transformed from a schematic into a physical layout and how the correctness of the layout is verified.

## 🎯 Objectives

- Design a CMOS inverter using SKY130A NMOS and PMOS transistors.
- Create the transistor-level schematic using Xschem.
- Generate the SPICE netlist and perform pre-layout simulation.
- Implement the physical layout using Magic VLSI.
- Understand the use of diffusion, polysilicon, contacts, vias, and metal layers.
- Perform Design Rule Checking (DRC).
- Extract parasitic information from the physical layout.
- Perform Layout Versus Schematic (LVS) verification using Netgen.
- Perform post-layout simulation using the extracted netlist.

## 🛠️ Tools and Technologies

| Tool / Technology | Purpose |
|---|---|
| Xschem | Schematic design |
| NGSpice | Circuit simulation |
| Magic VLSI | Physical layout design and DRC |
| Netgen | LVS verification |
| SKY130A PDK | 130nm CMOS technology |
| Ubuntu 22.04.5 LTS | Linux environment |
| Git & GitHub | Version control and project hosting |

---

## 🔄 VLSI Design Flow

The following flow represents the steps followed in this project.

```text
       CMOS Inverter Specification
                  |
                  v
          Schematic Design
               (Xschem)
                  |
                  v
          SPICE Netlist
                  |
                  v
          Pre-Layout Simulation
              (NGSpice)
                  |
                  v
          Physical Layout Design
             (Magic VLSI)
                  |
                  v
       Design Rule Checking (DRC)
                  |
                  v
          Parasitic Extraction
                  |
                  v
       Layout Versus Schematic
              (Netgen)
                  |
                  v
          Post-Layout Simulation
              (NGSpice)
                  |
                  v
          Final Verification
```

---

## 1. Environment Setup

The project was carried out in an Ubuntu 22.04.5 LTS environment with the SKY130A PDK and the required open-source EDA tools.

### Tools Installation and Verification

The following tools were used:

- Xschem
- NGSpice
- Magic VLSI
- Netgen
- SKY130A PDK

### Tool Verification

![EDA Tools Verification](images/tools_verification.png)

### SKY130A PDK Configuration

The SKY130A PDK was configured for the EDA tools.

**PDK Location:**

```bash
/home/jayee/open_pdks/sky130/sky130A/
```

**Magic Technology File:**

```bash
/home/jayee/open_pdks/sky130/sky130A/libs.tech/magic/sky130A.tech
```

**Netgen Setup File:**

```bash
/home/jayee/open_pdks/sky130/sky130A/libs.tech/netgen/sky130A_setup.tcl
```

**NGSpice Model File:**

```bash
/home/jayee/open_pdks/sky130/sky130A/libs.tech/ngspice/sky130.lib.spice
```

---

## 2. CMOS Inverter Schematic Design
<img width="1917" height="1198" alt="Screenshot 2026-11-14 184827" src="https://github.com/user-attachments/assets/26dd4afb-7867-42ad-a99f-7f6a8405fa11" />

A CMOS inverter was designed using complementary MOSFETs.

The circuit consists of:

- PMOS transistor as the pull-up network.
- NMOS transistor as the pull-down network.
- Common gate connection as the input.
- Common drain connection as the output.
- PMOS connected to VDD.
- NMOS connected to GND.

### Transistor Configuration

| Parameter | PMOS | NMOS |
|---|---|---|
| Model | `sky130_fd_pr__pfet_01v8` | `sky130_fd_pr__nfet_01v8` |
| Width | 3 µm | 4.5 µm |
| Length | 0.18 µm | 0.18 µm |
| Fingers | 3 | 3 |
| Multiplicity | 1 | 1 |

**Supply Voltage:** 1.8 V

### Schematic Design
<img width="1917" height="1135" alt="Screenshot 2026-11-14 190923" src="https://github.com/user-attachments/assets/f7763e02-ca89-4b98-96c0-d91230d574c5" />



The schematic was created in Xschem using the SKY130A transistor models.

---

## 3. Pre-Layout Simulation

The schematic netlist was generated and simulated using NGSpice.

Transient analysis was performed to observe the input and output voltage waveforms of the CMOS inverter.

### Working Principle

A CMOS inverter produces the logical complement of its input.

| Input Voltage | Output Voltage | Operation |
|---|---|---|
| LOW (0 V) | HIGH (1.8 V) | PMOS ON, NMOS OFF |
| HIGH (1.8 V) | LOW (0 V) | PMOS OFF, NMOS ON |

### Pre-Layout Simulation Waveform
<img width="1917" height="1138" alt="Screenshot 2026-11-14 191047" src="https://github.com/user-attachments/assets/6610b320-9576-4cb6-8d78-5ef8aa7973f3" />


The simulation was used to verify the expected switching behaviour of the inverter before physical layout implementation.

---

## 4. Physical Layout Design Using Magic VLSI

The physical layout of the CMOS inverter was implemented using Magic VLSI with the SKY130A technology file.

The layout was constructed using the required process layers and interconnections.

### Important Layout Layers

| Layer | Function |
|---|---|
| N-well | PMOS transistor region |
| Active Diffusion | Source and drain regions |
| Polysilicon | Gate formation |
| Local Interconnect | Local electrical connections |
| Metal 1 | First-level routing |
| Metal 2 | Higher-level routing |
| Contacts | Connect diffusion/poly to metal |
| Vias | Connect different metal layers |

### Layout Implementation

The PMOS and NMOS devices were placed and interconnected to implement the CMOS inverter.

Power, ground, input, and output connections were created using the appropriate layout layers.

### Final Routed Layout

<img width="1912" height="1198" alt="Screenshot 2026-11-14 215014" src="https://github.com/user-attachments/assets/1d468555-5289-4d68-a546-055b69205570" />


---

## 5. Design Rule Checking (DRC)

Design Rule Checking was performed using Magic VLSI to verify whether the physical layout satisfies the geometrical constraints defined by the SKY130A fabrication technology.

DRC checks include:

- Minimum spacing between layout layers.
- Minimum width requirements.
- Contact and via enclosure.
- Metal spacing and width.
- Diffusion and well design rules.

### DRC Verification

![DRC Result](images/drc_result.png)

**Final DRC Result:** Add the exact result from your final Magic DRC output here.

---

## 6. Parasitic Extraction

Parasitic extraction was performed using Magic VLSI to obtain the electrical characteristics associated with the physical layout.

The extraction process identifies parasitic resistance and capacitance introduced by the physical interconnections.

### Commands Used

```tcl
extract all
ext2spice lvs
ext2spice
```

The extracted SPICE netlist provides the physical-layout information required for post-layout simulation and further verification.

### Parasitic Extraction Output

![Parasitic Extraction](images/parasitic_extraction.png)

---

## 7. Layout Versus Schematic (LVS) Verification

LVS verification was performed using Netgen to compare the extracted layout netlist with the original schematic netlist.

The purpose of LVS is to ensure that the physical layout represents the intended electrical circuit.

### LVS Verification Checks

- Device matching.
- Transistor connectivity.
- Terminal connections.
- Circuit structure.
- Electrical equivalence between schematic and layout.

### LVS Result

![LVS Verification](images/lvs_result.png)

**Final LVS Result:** Add the exact result reported by Netgen here.

---

## 8. Post-Layout Simulation

Post-layout simulation uses the extracted SPICE netlist generated from the physical layout.

Unlike pre-layout simulation, post-layout simulation considers the parasitic effects introduced by the physical interconnections.

This helps evaluate the circuit response after physical implementation.

### Post-Layout Waveform

![Post-layout Simulation](images/postlayout_waveform.png)

---

## 📚 Challenges and Learning Outcomes

During the project, I gained practical experience in:

- Installing and configuring open-source VLSI EDA tools.
- Working with the SKY130A PDK.
- Creating transistor-level CMOS schematics.
- Generating and debugging SPICE netlists.
- Understanding CMOS inverter switching behaviour.
- Implementing physical layouts using Magic VLSI.
- Understanding semiconductor fabrication layout layers.
- Debugging metal routing, contacts, and via connections.
- Performing DRC and LVS verification.
- Understanding parasitic extraction and post-layout analysis.

## 📁 Repository Structure

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
    ├── parasitic_extraction.png
    ├── lvs_result.png
    └── postlayout_waveform.png
```

---

## 🏁 Conclusion

This project provided practical exposure to the CMOS inverter design and physical verification flow using the SKY130A 130nm technology.

Starting from schematic creation and pre-layout simulation, the project progressed through physical layout implementation, DRC, parasitic extraction, LVS, and post-layout analysis.

The project helped develop a better understanding of the relationship between circuit design, physical implementation, and verification in the VLSI design flow.

---

## 👩‍💻 Author

**Jayeetaa Yeddanapalli**

B.Tech – Electronics and Communication Engineering

[GitHub](https://github.com/jayeetaa)

[Project Repository](https://github.com/jayeetaa/VLSI-Physical-Verification-SKY130A)

---

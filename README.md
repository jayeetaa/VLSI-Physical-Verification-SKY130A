VLSI Physical Verification Using SKY130A PDK
CMOS Inverter Design | Xschem • NGSpice • Magic VLSI • Netgen
Author: Jayeetaa Yeddanapalli
Repository: jayeetaa/VLSI-Physical-Verification-SKY130A
Project status: Physical layout development and debugging; final DRC/LVS sign-off and post-layout simulation not yet confirmed.

Project Overview
This repository documents my hands-on implementation of a CMOS inverter using the open-source SKY130A 130 nm Process Design Kit (PDK). The work covers the Ubuntu development environment, open-source EDA tools, schematic capture, pre-layout simulation, physical layout, layout debugging, and the verification workflow. It records both completed work and unresolved issues rather than presenting unverified results as final.
Project Objectives
1. Configure the SKY130A PDK and the required open-source EDA tools.
2. Design a CMOS inverter schematic in Xschem using SKY130A transistors.
3. Generate a SPICE netlist and study transient inverter behavior using NGSpice.
4. Create a transistor-level physical layout using Magic VLSI.
5. Inspect routing, power connections, device terminals, and design-rule violations.
6. Extract the layout netlist and compare it against the schematic using Netgen.
7. Perform post-layout simulation after connectivity and verification issues are resolved.
0. Theory — SKY130A PDK and Open-Source EDA Flow
0.1 SKY130A Process Design Kit
The SKY130A PDK provides process-specific transistor models, technology layers, design rules, and supporting files for schematic design, circuit simulation, physical layout, and verification.
0.2 PDK Resources
Resource	Role in this project
SPICE models	Describe the electrical behavior of NFET and PFET devices
Magic technology files	Define layout layers and rules used for editing and DRC
Xschem libraries	Provide schematic symbols for SKY130A devices
Netgen setup files	Configure device recognition and LVS comparisons
Extraction information	Supports layout netlist and parasitic extraction


0.3 Physical Layers and Connections
The layout uses transistor active regions and polysilicon gates, local interconnect and contacts, metal routing, and vias. Metal1 is used for local routing and power rails; a Metal2 jumper was explored to cross a routing obstruction without shorting unrelated nets.
0.4 Design and Verification Workflow
SKY130A PDK + tool configuration
              |
              v
      Xschem schematic
              |
              v
     SPICE netlist / testbench
              |
              v
     NGSpice pre-layout simulation
              |
              v
       Magic physical layout
              |
              v
     DRC inspection and fixes
              |
              v
       Layout extraction
              |
              v
     Netgen LVS comparison
              |
              v
    NGSpice post-layout simulation
1. Development Environment
1.1 System Information
Item	Configuration
Operating system	Ubuntu 22.04.5 LTS
Project root	~/Physical_Verification_SKY130A/
Lab directory	~/Physical_Verification_SKY130A/Lab1_CMOS_Inverter/
PDK directory	/home/jayee/open_pdks/sky130/sky130A/
Magic executable	/usr/local/bin/magic
Netgen executable	/usr/local/bin/netgen
NGSpice executable	/usr/bin/ngspice


1.2 System Validation
lsb_release -a
uname -a
free -h
df -h /
nproc
1.3 Tools Used
Tool	Purpose	Project progress
Magic VLSI 8.3 series	Physical layout and DRC	Installed and used
Xschem	Schematic and SPICE netlisting	Installed and used
Netgen	LVS verification	Installed; final match pending
NGSpice 37	Transient simulation	Installed; pre-layout files generated
Git	Version control	Installed
SKY130A PDK	Process technology	Configured


Tool verification commands:
which magic && magic --version
which xschem && xschem --version
which netgen && netgen --version
which ngspice && ngspice --version
git --version
Tool setup screenshot:

1.4 SKY130A Technology Integration
The local PDK resources used during development include:
/home/jayee/open_pdks/sky130/sky130A/libs.tech/magic/sky130A.tech
/home/jayee/open_pdks/sky130/sky130A/libs.tech/magic/sky130A.magicrc
/home/jayee/open_pdks/sky130/sky130A/libs.tech/netgen/sky130A_setup.tcl
/home/jayee/open_pdks/sky130/sky130A/libs.tech/ngspice/sky130.lib.spice
Launch Magic with the technology file:
magic -T /home/jayee/open_pdks/sky130/sky130A/libs.tech/magic/sky130A.tech -d OGL
Implementation note: The OGL display driver was used because the XR driver previously produced a BadAlloc issue in this environment.
2. Lab 1 — CMOS Inverter Design
2.1 Operating Principle
A CMOS inverter uses a PFET pull-up device and an NFET pull-down device:
- Input LOW: PFET conducts, NFET is off, and the output is HIGH.
- Input HIGH: NFET conducts, PFET is off, and the output is LOW.
The inverter operates from a nominal 1.8 V supply in this project.
2.2 Intended Transistor Specifications
Parameter	NFET (M1)	PFET (M2)
SKY130A model	sky130_fd_pr__nfet_01v8	sky130_fd_pr__pfet_01v8
Width	4.5 µm	3 µm
Length	0.18 µm	0.18 µm
Target fingers	3	3
Body connection	VSS	VDD


Netlist consistency note: An earlier Xschem netlist showed the PFET with nf=1 while the intended design specified nf=3. This difference must be checked before final LVS sign-off.
2.3 Xschem Schematic
The inverter schematic uses the four external signals VDD, VSS, IN, OUT. The PFET source/body connect to VDD, the NFET source/body connect to VSS, both gates connect to IN, and both drains connect to OUT.

Local schematic files developed during the project include Inverter.sch, Inverter.sym, and additional inverter/testbench variants in the xschem/ directory.

Screenshot — CMOS inverter schematic:

2.4 SPICE Netlist and Pre-Layout Simulation
The pre-layout work uses a 1.8 V supply, a pulse input, and an output load. The saved simulation materials include:
simulation/inverter.spice
simulation/inverter_waveform.txt
simulation/inverter_waveform.png
The intended logic relationship is OUT = NOT(IN). The saved simulation outputs should be reviewed against this expectation and retained as evidence of the waveform results.

Screenshots — SPICE setup and simulation progress:

3. Magic VLSI Physical Layout — 29–31 October 2026
3.1 Layout Development Objective
Translate the CMOS inverter schematic into a physical layout containing NFET and PFET device instances, gate connections, power rails, output routing, and four labeled ports.
3.2 Layout Organization
The design work explored:
- PFET placement toward the top and NFET placement toward the bottom.
- VDD power rail above the PFET and VSS rail below the NFET.
- Common gate routing for IN.
- Drain interconnections for OUT.
- Metal1 routing and a Metal1 → Via1 → Metal2 → Via1 → Metal1 jumper.
- Port labels and device pin connectivity.
Earlier layout screenshots:

3.3 Saved Layout Versions
Multiple intermediate files were saved to preserve progress and allow comparison during debugging. Examples include:
layout/inverter.mag
layout_final/Inverter_Routed.mag
layout_final/Inverter_Final.mag
layout_final/Inverter_Clean.mag
These names describe working versions, not independently verified sign-off files. A file named Inverter_Clean.mag does not by itself establish that DRC or LVS passed.
3.4 Opening the Saved Layout
From an Ubuntu terminal:
cd ~/Physical_Verification_SKY130A/Lab1_CMOS_Inverter/layout_final
magic -T /home/jayee/open_pdks/sky130/sky130A/libs.tech/magic/sky130A.tech -d OGL Inverter_Clean.mag
Within the Magic Tcl console:
expand
zoom full
If Magic reports No such file or directory, verify the current folder and the exact file name before loading:
pwd
glob *.mag
Important: readspice availability varies by Magic build; the existing .mag layout can be opened directly without importing SPICE. ext2spice is for extracting a SPICE netlist from layout, not importing one.
3.5 Layout Debugging and Observations
During routing and extraction, the following issues were encountered:
1. Unconnected multi-finger terminals: Extracted NFET nodes appeared as separate nets such as XM1/S1, XM1/S2, and individual gate/drain nodes. These require careful verification of source, drain, and gate wiring.
2. PFET and NFET connectivity: Device terminals and the shared output connection needed inspection before reliable LVS comparison.
3. Routing conflicts: A Metal2 jumper was explored to route over an obstruction while avoiding a Metal1 short.
4. Floating extracted geometry: One extracted version contained a floating parasitic capacitor, indicating that further inspection was required.
5. Layout editing: Magic layer selection, expanded cells, port labels, and console commands required iterative troubleshooting.
The extracted netlist at one point contained multiple NFET devices instead of the intended merged device representation. This is an LVS debugging issue, not proof of a successful comparison.
4. Design Rule Checking (DRC)
4.1 Purpose
DRC checks whether the drawn geometry follows the physical design rules defined by the SKY130A technology.
4.2 Magic Commands
Run inside the Magic Tcl console after loading the desired layout:
drc check
drc count
drc why
4.3 Current Status
Earlier saved Magic files contained error_s geometry, and layout corrections were still in progress. A final zero-error DRC result has not yet been confirmed. A future sign-off update should include the exact layout filename, DRC count, and a screenshot of the result.
5. Layout Extraction and LVS — Netgen
5.1 Purpose
Layout Versus Schematic (LVS) checks whether the devices and electrical connections extracted from the physical layout correspond to those in the reference Xschem schematic.
5.2 Extracting a SPICE Netlist
In Magic, after loading the layout:
extract all
ext2spice lvs
ext2spice
The resulting netlist must be inspected to confirm device count, transistor parameters, port names, and connectivity.
5.3 Netgen Setup
The SKY130A Netgen setup file is located at:
/home/jayee/open_pdks/sky130/sky130A/libs.tech/netgen/sky130A_setup.tcl
Example LVS command template (replace the cell names and paths with the actual matching files):
netgen -batch lvs \
  "layout_final/Inverter_Final.spice Inverter_Final" \
  "xschem/Inverter.spice Inverter" \
  /home/jayee/open_pdks/sky130/sky130A/libs.tech/netgen/sky130A_setup.tcl \
  lvs_report.log
This is a template, not a recorded successful LVS run. Ensure that the two specified subcircuit names really exist in their respective SPICE files.
5.4 LVS Debugging Checklist
- Check the reference schematic's PFET nf parameter against the intended layout.
- Verify every NFET/PFET source, drain, and gate finger is connected correctly.
- Confirm the shared output net and both supply rails.
- Confirm bulk/body connections.
- Confirm the extracted port names match the schematic interface.
- Compare Netgen device counts and net counts after each routing fix.
Current status: Final Circuits match uniquely output has not been established for this project.
6. Post-Layout Simulation — Planned
Once DRC and LVS are resolved, the Magic-extracted netlist can be used in NGSpice to assess inverter behavior with layout-related parasitic effects.

The planned comparison will inspect:
Parameter	Pre-layout	Post-layout
Logic function	Check inverter response	Verify after extraction
Supply	1.8 V	1.8 V target
Input pulse	Applied	Reuse equivalent stimulus
Output waveform	Saved simulation outputs	Pending
Extracted parasitics	Not from physical layout	Include as supported by extraction
Propagation delay	Measure from waveform	Compare after simulation


Status: Pending. No post-layout waveform or measured delay is claimed here.
7. Project Progress
Stage	Status	Evidence / next action
Ubuntu environment	Completed	System and tool verification
SKY130A PDK integration	Configured	Magic and device libraries used
Xschem inverter schematic	Created	Schematic screenshot and local files
SPICE simulation	Outputs generated	Saved netlist and waveform files
Magic physical layout	Working versions created	.mag files and layout screenshots
Routing and connectivity	Debugging	Review floating nodes and terminal connections
DRC sign-off	Not confirmed	Run and record final DRC count
LVS sign-off	Pending	Resolve device/net mismatches
Post-layout simulation	Pending	Simulate verified extracted netlist
GitHub source upload	Partially complete	Upload actual project source files


8. Key Challenges and Learnings
8.1 Toolchain Setup
Configuring Magic, Xschem, Netgen, NGSpice, and the SKY130A PDK required attention to technology files, library paths, and display drivers.
8.2 Multi-Finger Transistor Connectivity
A multi-finger transistor's physical terminals must be routed correctly. Unconnected or mislabeled terminals can create extra extracted nets and prevent an LVS match.
8.3 Metal Routing and Via Connections
A higher metal layer can help cross a routing obstruction, but every via, contact, and endpoint must be checked to avoid shorts and open circuits.
8.4 Verification Is Iterative
A visually complete layout is not necessarily DRC-clean or electrically equivalent to the schematic. Extraction and LVS are essential for detecting hidden connectivity errors.
8.5 Versioned Working Files
Keeping intermediate .mag, .spice, and screenshot files helped preserve progress while testing changes.
9. Local Project Organization
The following is a working-directory overview, not a claim that every file is already uploaded to GitHub:
Physical_Verification_SKY130A/
└── Lab1_CMOS_Inverter/
    ├── xschem/
    │   ├── Inverter.sch
    │   ├── Inverter.sym
    │   └── jayee_inverter_tb.sch
    ├── simulation/
    │   ├── inverter.spice
    │   ├── inverter_waveform.txt
    │   └── inverter_waveform.png
    ├── layout/
    │   └── inverter.mag
    └── layout_final/
        ├── Inverter_Routed.mag
        ├── Inverter_Final.mag
        └── Inverter_Clean.mag
Additional intermediate .ext, .spice, and other layout files may exist locally. Upload the verified relevant source files and supporting screenshots to the repository so the work is reproducible.
10. Next Steps
1. Open the latest saved Magic layout and confirm all device instances are visible.
2. Inspect and repair source, drain, gate, and body connectivity.
3. Run DRC and record the actual final error count.
4. Extract the corrected layout netlist.
5. Run Netgen LVS and resolve mismatches until the circuits match.
6. Run post-layout NGSpice transient simulation and compare waveforms.
7. Upload the layout, schematic, simulation, verification logs, and screenshots to GitHub.
11. References
- SKY130 PDK documentation
- Open_PDKs
- Magic VLSI
- Xschem
- Netgen
- NGSpice
Project by Jayeetaa Yeddanapalli — SKY130A CMOS Inverter Physical Verification.
Status: In progress; physical verification sign-off pending.

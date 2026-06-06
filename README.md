# Hardware-Enforced PIN Validation Gate Core (DLD)

A hardware-level 4-bit PIN authentication security core designed and simulated inside National Instruments Multisim. This architecture utilizes hardware magnitude comparators to enforce zero-software physical security boundaries for high-security access control systems.

## Technical Specifications
* **Core Architecture:** 4-Bit Hardware Magnitude Comparison
* **Core IC Targets:** 74LS85 High-Speed Magnitude Comparator (`U9`)
* **Logic Framework:** Bitwise Combinational Match Verification ($A = B$)
* **Simulation Platform:** NI Multisim (Interactive Simulation Mode)

## Hardware Components (Schematic Bill of Materials)
The system is built entirely on the following discrete digital components and source lines:

* **Integrated Circuits:**
  * `U9`: **74LS85D** (4-Bit Magnitude Comparator IC)
* **Input & Interactive Elements:**
  * `U2`, `U3`, `U4`, `U5`: **Interactive Toggle Switches** (Hardwired Backend Reference Key Array)
  * `U6`, `U7`, `U8`, `U9_switch`: **Interactive Toggle Switches** (Real-Time User Input Entry Array)
* **Output & Indicators:**
  * `X1`: **2.5 V Green Lamp / Status Indicator LED** (Visual Authorization Gate)
* **Power Rails:**
  * `VCC`: **5.0 V Direct Current (DC) Power Source**
  * `GND`: **System Ground Reference**

## System Features
1. **Physical Security Boundary:** Signal processing occurs entirely at the gate level inside the 74LS85 IC chip, eliminating susceptibility to remote software vulnerabilities or operating system exploits.
2. **Deterministic Processing:** Matches parallel user input arrays against a predefined master key instantly via hardware internal logic gates, eliminating execution latency or software overhead.
3. **Visual Output Validation:** Features a direct $A=B$ output routing line (**QAEQB, Pin 6**) that shifts dynamically to a high logic state to drive the external indicator system (`X1`) upon a successful match sequence.

## Verified Simulation Behavior
The layout has been structurally tested and verified under concurrent load matching:
* **Backend Master Key Reference Array ($B$):** Hardwired to state `1100` via toggle lines `U2` through `U5`.
* **User Input Signal Array ($A$):** Interactive entry matched to state `1100` via entry lines `U6` through `U9_switch`.
* **System Resolution Output:** Condition $A=B$ evaluates true $\rightarrow$ **Pin 6 (QAEQB)** fires high $\rightarrow$ Status Indicator `X1` triggers active ($2.5\text{V}$ drop).

<div align="center">

# 4-Bit Ripple Carry Adder: KiCad 74LS Simulation

### Cascaded binary arithmetic and carry propagation using discrete 74LS-series logic gates

[![GitHub](https://img.shields.io/badge/GitHub-Repository-181717?style=flat&logo=github)](https://github.com/satvikpandurangi/4bit-Ripple-Carry-Full-Adder-Simulation-Kicad)
[![KiCad](https://img.shields.io/badge/KiCad-EDA-314CB0?style=flat&logo=kicad&logoColor=white)](https://www.kicad.org/)
[![ngspice](https://img.shields.io/badge/Simulator-ngspice-blue?style=flat)](https://ngspice.sourceforge.io/)

</div>

---

## 📖 Overview

This repository contains a fully routed, simulated 4-bit Ripple Carry Adder built from discrete 74LS-series logic gates in KiCad. It demonstrates cascaded Full Adder circuits performing binary arithmetic, with sum and carry-out logic verified through transient SPICE analysis.

## 🎯 Objectives

- Design a 4-bit Ripple Carry Adder by cascading four discrete Full Adder stages
- Bind manual SPICE models to standard 74-series symbols for gate-level simulation
- Verify sum and carry-propagation logic against binary addition truth tables

## ✨ Features

- 4-bit Ripple Carry Adder built from 74LS86, 74LS08, and 74LS32 gates
- Manually bound SPICE models (`logic.lib`) enabling accurate gate-level simulation
- Configurable DC sources to test arbitrary 4-bit input combinations
- Verified test case (5 + 3 = 8) with full node-voltage analysis

## ⚙️ Circuit Overview

Four Full Adder blocks are cascaded, each accepting Bit A, Bit B, and a Carry-In (Cin), and producing a Sum bit and Carry-Out (Cout):

- **Sum Logic:** Sum = A ⊕ B ⊕ Cin
- **Carry Logic:** Cout = (A · B) + (Cin · (A ⊕ B))
- **Ripple Effect:** Each stage's Carry-Out feeds the next stage's Carry-In, from Adder 0 (LSB) through Adder 3 (MSB) — higher-order bits cannot resolve until the carry has "rippled" through every preceding stage.

## 🧩 Components Used

| Type | Component | Function |
|------|-----------|----------|
| Active | 74LS86 (Quad 2-input XOR) | Sum calculation |
| Active | 74LS08 (Quad 2-input AND) | Internal carry generation |
| Active | 74LS32 (Quad 2-input OR) | Carry propagation |
| Passive | 10 kΩ pull-down resistors | Stabilize logic states |
| Source | Multiple DC voltage sources | Constant Logic 1 (5 V) / Logic 0 (0 V) inputs |

## 🛠️ Software & Simulation

Built and simulated in **KiCad EDA** — the Schematic Editor lays out the 74-series gates and routes the cascaded adder network, while the integrated **ngspice** simulator runs Transient Analysis to resolve output logic states.

> ⚠️ **Note:** Standard KiCad 74-series symbols lack native SPICE math models, so this project manually binds them to a `logic.lib` behavioral file, with "Unit B" sub-gates reassigned to "Unit A" to avoid SPICE indexing errors.

**Requirements:** KiCad v6.0+ with the integrated `ngspice` simulator (included by default).

## 📂 Repository Structure

```
4bit-Ripple-Carry-Full-Adder-Simulation-Kicad
├── 4Bit_Adder.kicad_pro       # Main KiCad project file
├── 4Bit_Adder.kicad_sch       # Schematic and SPICE directives
├── 4Bit_Adder.kicad_pcb       # PCB layout file
├── logic.lib                  # Behavioral SPICE models for 74LS gates
├── logic.txt                  # Logic model reference notes
├── 4bit_Adder_Schematic.png   # Circuit schematic
├── 4bit_Adder_Output.png      # Simulation waveform/output
└── README.md
```

## 🚀 How to Open & Run

1. Clone the repository (ensure `logic.lib` is included, or the simulation will fail):
   ```bash
   git clone https://github.com/satvikpandurangi/4bit-Ripple-Carry-Full-Adder-Simulation-Kicad.git
   ```
2. Open `4Bit_Adder.kicad_pro` in the KiCad Project Manager and open the Schematic Editor.
3. Modify the DC voltage sources (A0–A3, B0–B3) to set a binary test case.
4. Go to **Inspect > Simulator** and click **Run/Stop Simulation**.
5. Probe the S0–S3 and Cout nets and compare against the binary addition truth table.

## 📊 Simulation Results

**Test Case: 5 + 3 = 8** — Input A = 0101, Input B = 0011, Cin = 0

| Stage | Node / Net | Parameter | Expected Logic | Simulated Voltage | Status |
|-------|------------|-----------|------------------|---------------------|--------|
| Adder 0 (LSB) | S₀ | Sum Bit 0 | 0 | 0.0 V | PASS |
| | C₁ | Carry Out 0 | 1 | 5.0 V | PASS |
| Adder 1 | S₁ | Sum Bit 1 | 0 | 0.0 V | PASS |
| | C₂ | Carry Out 1 | 1 | 5.0 V | PASS |
| Adder 2 | S₂ | Sum Bit 2 | 0 | 0.0 V | PASS |
| | C₃ | Carry Out 2 | 1 | 5.0 V | PASS |
| Adder 3 (MSB) | S₃ | Sum Bit 3 | 1 | 5.0 V | PASS |
| | Cₒᵤₜ | Final Carry Out | 0 | 0.0 V | PASS |

**Final Output Binary:** 01000 (Decimal 8) — the carry propagated correctly through all four stages.

## 📸 Screenshots

**Schematic:**

![Schematic](4bit_Adder_Schematic.png)


**Simulation Output:**

![Simulation Output](4bit_Adder_Output.png)


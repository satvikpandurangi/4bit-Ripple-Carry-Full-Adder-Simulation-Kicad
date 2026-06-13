# 4-Bit Ripple Carry Adder: KiCad 74LS Simulation

## 📌 Overview
This repository provides a fully routed and simulated 4-bit Ripple Carry Adder built using discrete 74LS-series logic gates in KiCad. It serves as a practical demonstration of cascading Full Adder circuits and verifying binary arithmetic using transient SPICE analysis.

This project is highly valuable for digital logic students looking to bridge the gap between theoretical truth tables and actual EDA (Electronic Design Automation) simulation environments.

---

## ⚙️ Circuit Architecture
The architecture consists of four cascaded Full Adder stages handling two 4-bit input words (A and B) and an initial Carry-In ($C_{in}$).
* **Sum Logic:** 74LS86 (Quad 2-Input XOR)
* **Carry Generation:** 74LS08 (Quad 2-Input AND)
* **Carry Propagation:** 74LS32 (Quad 2-Input OR)

> **⚠️ Important EDA Note:** Standard KiCad 74-series symbols do not contain native math models. This project includes manual bindings to an integrated `logic.lib` SPICE model file to enable true logical simulation. 

---

## 📊 Simulation Details
The circuit is tested using DC Voltage sources to represent steady Logic 1 (5V) and Logic 0 (0V) states. 

By running a **Transient Analysis**, users can probe the internal carry nets ($C_1$, $C_2$, $C_3$) to observe the physical time delay as the carry bit "ripples" through the architecture before the final Most Significant Bit ($S_3$) and Carry-Out ($C_{out}$) resolve.

---

## 🛠️ Software Requirements
* **KiCad EDA** (v6.0 or higher recommended)
* Integrated `ngspice` simulator (included by default in KiCad)

---

## 🚀 How to Run the Simulation
1. Clone this repository to your local machine (ensure `logic.lib` downloads with it, or the simulation will fail):
   ```bash
   git clone [https://github.com/satvikpandurangi/4bit-Ripple-Carry-Full-Adder-Simulation-Kicad.git](https://github.com/satvikpandurangi/4bit-Ripple-Carry-Full-Adder-Simulation-Kicad.git)
   ```
2. Open the **`.kicad_pro`** project file in the KiCad Project Manager.
3. Open the **Schematic Editor** to view the circuit layout.
4. Modify the DC voltage sources (A0-A3, B0-B3) to your desired binary test case.
5. Go to **Inspect > Simulator** in the top menu and click the **Run/Stop Simulation** (Play) button.
6. Probe the output pins to verify the node voltages against standard binary addition truth tables.

---

## 📂 Repository Contents
* **`.kicad_pro`** - Main project file
* **`.kicad_sch`** - The schematic wiring and SPICE directives
* **`.kicad_pcb`** - Blank PCB layout file (ready for physical routing if desired)
* **`logic.lib`** - Required behavioral SPICE models for the 74LS gates

> *Created for educational purposes and open-source hardware exploration.*

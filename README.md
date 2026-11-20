# Reverse Engineering and LTspice Simulation of a Battery Charging Module (HW-373)

A **Linear Integrated Circuits (Assignment 2)** project focusing on the visual inspection, functional reverse engineering, and LTspice transient simulation of an **HW-373 V1.2.1** battery charging module.

---

## 📋 Overview
This project documents the workflow of inspecting a physical lithium-ion battery charging PCB, identifying its visible terminals and integrated circuits, reconstructing a simplified component-level representation in **LTspice**, and running a transient simulation to analyze its voltage behavior.

### 🎯 Objectives
* Inspect the HW-373 battery charging module and identify visible board markings and terminals.
* Reverse engineer the board at a functional, component-level representation.
* Recreate the representative circuit in LTspice using standard circuit elements.
* Run a transient simulation and observe voltage waveforms.
* Understand practical lithium-ion battery charging and protection topologies.

---

## 🔍 Hardware Inspection (HW-373 Module)
Based on visual inspection of the PCB, the following key features and connection pads were identified:

| Visible Feature | Observation / Role |
| :--- | :--- |
| **USB Connector** | Input power connector located on the left side of the board. |
| **4056 IC (`U1`)** | Central charging management IC package marked `"4056"`. |
| **`B+` and `B-`** | Battery connection pads. |
| **`OUT+` and `OUT-`** | Load/output connection pads. |
| **`LED1` / `LED2`** | Dual status indicator positions labelled on the PCB. |

*(Note: Visual inspection of the PCB alone establishes surface markings and terminal layout rather than the complete internal IC architecture.)*

---

## ⚡ LTspice Representative Schematic
A simplified simulation model was constructed in LTspice using a 5 V DC input source, current-limiting and series resistors, a diode, filtering capacitors, and red/green LED branches.

### Bill of Materials (Simulation Model)

| Reference | Value / Type | Role in Schematic |
| :--- | :--- | :--- |
| **`V1`** | `5 V` DC Source | Provides the main input supply voltage. |
| **`R1`** | `1 kΩ` | Current-limiting series resistor in the red LED branch. |
| **`R2`** | `10 Ω` | Series resistive element in the main upper path. |
| **`D1`** | Diode | Provides a direction-dependent conduction path between nodes. |
| **`R3`** | `0.1 Ω` | Series resistance in the path toward the output node. |
| **`R4`** | `1 kΩ` | Current-limiting series resistor in the green LED branch. |
| **`C1`** | `10 µF` | Intermediate node decoupling/filtering capacitor. |
| **`C2`** | `100` (Farads/µF*) | Output-side capacitance (*unit unlabelled in schematic capture*). |
| **`led_red` / `led_green`** | LED Models | Visual status indicator branches in the simulated network. |

---

## 📈 Transient Simulation
The circuit was evaluated in LTspice using the following transient analysis directive:
```spice
.tran 0 60 0 10m
```
* **Stop Time:** `60 s`
* **Maximum Time Step:** `10 ms`

### Key Takeaways & Limitations
* **Steady-State Response:** The captured voltage waveforms show a largely steady output response across the 60-second simulation window.
* **Model Scope:** The schematic serves as an introductory functional model rather than an exact replica of the internal feedback and protection loops inside the physical TP4056/DW01A chipset.
* **Future Work:** Full hardware validation requires physical bench measurements (oscilloscope/multimeter) compared against detailed IC macro-models.
* 
👥 Contributors 
1.S.Dhyan
2.Aditya DH 
3.Aditya Devaki
  .

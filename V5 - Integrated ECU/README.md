# ECU V5 — Integrated Automotive Control Unit (4-Layer PCB)

## Overview
ECU V5 is the final integration stage of a modular automotive ECU project.  
This version consolidates power management, sensing, safety supervision, communication, and actuation into a single 4-layer PCB designed using production-style layout and grounding practices.

The focus of ECU V5 is **system integration**, **power integrity**, **EMI control**, and **clear domain separation**, rather than feature expansion.

---

## Design Objectives
- Integrate all ECU subsystems into a single board
- Apply production-style grounding (DGND / AGND / PGND)
- Ensure stable operation in noisy automotive environments
- Maintain safety-oriented logic and default-safe behavior
- Follow RF-aware and EMI-conscious layout practices

---

## Key Features
- **4-layer PCB stack-up**
  - Layer 1: Signals and components
  - Layer 2: Solid digital ground plane (DGND)
  - Layer 3: Power planes (+12V_PROT, +5V_SYS, +3V3_SYS)
  - Layer 4: Local AGND and PGND copper islands
- ESP32-based control core
- CAN bus communication
- Automotive 12V input with protection
- Buck regulation to 5V and LDO regulation to 3.3V
- Comparator-based power supervision (12V_OK, 5V_OK)
- Safety logic with KILL_IN and ACT_PERMIT gating
- Analog sensor front-end with isolated AGND
- High-side actuator drivers
- RF antenna keep-out on all layers
- DRC-clean and ready for fabrication

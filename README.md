# Modular Automotive ECU

A custom-designed automotive **Engine/Electronic Control Unit**, built up as five hardware modules — from a bare ESP32 CAN core to a fully integrated 4-layer control unit — using production-style power, grounding, safety, and EMI practices.

> **Status:** Hardware design complete and DRC-clean. Not yet manufactured or tested — this repository documents the design work.

![ECU V5 — 3D render](V5%20-%20Integrated%20ECU/Images/3D%20Design%20-%20V5.png)

---

## The idea

Rather than designing one board in isolation, the ECU is developed as a **layered system**, each stage adding one responsibility and integrating with the last:

| Module | Role | Highlights | Status |
|--------|------|-----------|--------|
| **[V1 — Core](V1_Core)** | *Thinks* | ESP32, CAN, USB-C, protected 12V input, buck + LDO power, ESD/transient protection | Designed |
| **[V2 — Sensors](V2_Sensors)** | *Measures* | 6-channel analog front-end, external SPI ADC, 2.5 V precision reference, per-channel filtering + TVS, AGND/DGND discipline | Designed |
| **[V3 — Actuators](V3_Actuators)** | *Acts* | 8× protected low-side MOSFET drivers, flyback clamping, star-point PGND/DGND tie | Designed |
| **[V4 — Safety Monitor](V4_Safety_Monitor)** | *Protects* | Firmware-independent hardware safety: comparator rail supervision, latched faults, `ACT_PERMIT` gating, KILL path | Designed |
| **[V5 — Integrated ECU](V5%20-%20Integrated%20ECU)** | *Integrates* | All subsystems on a single **4-layer PCB** with production-style grounding, power integrity, and RF keep-out | Designed |

---

## Engineering focus

The project is built around the practices that make an ECU actually survive an automotive environment, not just function on a bench:

- **Domain-separated grounding** — dedicated DGND / AGND / PGND, tied at single controlled star points to keep switching noise out of the analog and digital references.
- **Power integrity** — protected 12 V input, buck-to-5 V and LDO-to-3V3 rails, plane-based distribution on the integrated board.
- **Hardware-first safety** — the V4 supervisor enforces safe states through comparators and a fault latch *independent of firmware*; actuators stay disabled unless every monitored rail is valid and no fault is latched.
- **EMI / RF awareness** — CAN placed at the harness connector, high-di/dt currents confined to PGND, full antenna keep-out on every layer of V5.
- **4-layer stack-up (V5):** signals · solid DGND plane · power planes (12V_PROT / 5V_SYS / 3V3_SYS) · local AGND/PGND islands.

---

## What's in each module

```
V1_Core/              ESP32 CAN core + power supply
V2_Sensors/           Analog sensor front-end (+ V2.5 IMU variant)
V3_Actuators/         Low-side output driver stage
V4_Safety_Monitor/    Hardware supervision & safety logic
V5 - Integrated ECU/  Full ECU on a single 4-layer board
```

Each module folder contains its own README plus:
- **Schematics** (PDF)
- **PCB renders** — 3D views and per-layer plots (PNG)
- **Manufacturing outputs** — Gerbers, BOM, pick-and-place

---

## Tools

Altium Designer · ESP32 · 2- and 4-layer PCB design

---

## Author

**Muhannad Hamadeh** — Mechatronics engineer, MSc Mechatronics & Information Technology, KIT.
[LinkedIn](https://www.linkedin.com/in/muhannad-hamadeh/)

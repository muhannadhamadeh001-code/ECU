# ECU V3 — Actuator & Output Driver Board (Low-Side Outputs)

V3 is the actuation stage of the ECU project.
While **V1 provides compute/communication** and **V2 handles sensor acquisition**, **V3 drives real-world loads** (relays, solenoids, lamps, small DC loads) using protected low-side output channels.

**V1 → Thinks**  
**V2 → Measures**  
**V3 → Acts**

---

## What this board does

- Provides **8x low-side driver channels** using logic-level N-MOSFETs
- Accepts **GPIO/PWM control signals** from V1 (no PWM generation on V3)
- Drives **12V-domain loads** through output header
- Adds **inductive load protection** and **supply transient protection**

---

## Channel architecture (per output)

Each channel includes:
- Logic input from V1 (`V1_GPIOx`)
- Gate resistor (EMI control)
- Gate pulldown resistor (defined OFF state at reset)
- N-MOSFET low-side switch
- Flyback diode to `12V_LOAD` (inductive clamp)
- Output net `OUT_x`

---

## Power & grounding concept

- Load power domain: `12V_LOAD`
- Power return: `PGND`
- Logic reference: `DGND`
- **DGND and PGND are tied at a single star point using a 0Ω link** near the power entry / TVS area.

Power entry includes:
- Bulk + ceramic decoupling (`100µF + 1µF + 100nF`)
- TVS diode across `12V_LOAD ↔ PGND` for supply transients

---

## Connectors

### J_LOAD (Power / Outputs)
Carries:
- `12V_LOAD`
- `OUT_1 ... OUT_8`
- `PGND`

Used to connect external loads (relays/solenoids/etc).

### J_CTRL (Logic from V1)
Carries:
- `V1_GPIO1 ... V1_GPIO8`
- `DGND`
- `+3V3` (reference / future expansion)

---

## Design intent

This board is designed as an **educational but system-accurate ECU output stage**:
- Realistic low-side output architecture
- Proper current return handling
- Protection for inductive loads
- Designed to be integrated later into **V5 (full ECU)**

---

## Status

- ✅ Schematic complete
- ✅ PCB routed with power integrity considerations (12V bus, PGND pour, star ground tie)
- ⏳ Hardware bring-up/testing: not yet performed

---

## Files

- `hardware/` — schematic PDF + PCB renders
- `manufacturing/` — Gerbers, BOM, CPL
- `docs/` — design notes and manufacturing notes

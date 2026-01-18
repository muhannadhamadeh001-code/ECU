# ECU V2 — Sensor Expansion Board

V2 is the sensor front-end expansion board for the ECU project.  
It extends the V1 ECU Core by adding automotive-style analog sensor interfacing using an external SPI ADC, a precision voltage reference, and robust input protection/filtering.

> Status: PCB design completed. Hardware validation pending.

---

## Goals of V2
- Add scalable sensor acquisition without modifying the V1 core architecture
- Use ECU-style analog front-end practices (filtering, protection, grounding discipline)
- Improve measurement stability by using an external ADC + precision reference

---

## Key Features
- External multi-channel SPI ADC (12-bit) for sensor acquisition
- Precision 2.5V reference for stable ADC conversions
- 6 sensor channels implemented:
  - **NTC temperature inputs**: IAT, ECT
  - **0–5V analog inputs**: TPS, MAP, Oil Pressure, AUX/Spare Pressure
- Input conditioning on every analog channel:
  - Series resistance
  - RC low-pass filtering
  - TVS protection (sensor-facing)
- AGND/DGND strategy with a single-point tie (mixed-signal discipline)

---

## System Architecture (V1 ↔ V2)
V2 connects to V1 through an expansion header carrying:
- Power rails (5V, 3V3)
- SPI bus (SCK, MOSI, MISO, CS)
- Grounds (AGND, DGND)

V2 performs signal conditioning + ADC conversion and forwards digitized sensor data over SPI.

---

## Sensor Channel Mapping (ADC)
| Sensor | Type | ADC Channel |
|------:|------|------------:|
| IAT | NTC divider to 2.5V ref | CH0 |
| ECT | NTC divider to 2.5V ref | CH1 |
| TPS | 0–5V analog | CH2 |
| MAP | 0–5V analog | CH3 |
| Oil Pressure | 0–5V analog | CH4 |
| AUX / Spare | 0–5V analog | CH5 |

Unused ADC channels are reserved for future expansion.

---

## Design Files
- Schematics: `hardware/schematics/`
- PCB: `hardware/pcb/`
- Outputs (Gerbers/BOM/CPL): `hardware/outputs/`

---

## Documentation
- Architecture: `docs/architecture.md`
- Sensor Interfaces: `docs/sensor_interfaces.md`
- Design Decisions: `docs/design_decisions.md`
- Manufacturing Notes: `docs/manufacturing_notes.md`

---

## Notes
This board is intended as a modular step toward the final integrated ECU version.  
Validation results (noise, accuracy, sensor calibration) will be added after assembly and testing.

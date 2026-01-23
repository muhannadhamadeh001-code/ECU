
---

## ARCHITECTURE.md

# ECU V5 — Architecture Overview

## System Overview
ECU V5 integrates sensing, power management, logic control, communication, and actuation into a single embedded control unit.  
The architecture emphasizes robustness, safety, and noise immunity through careful domain separation and grounding strategy.

---

## Power Architecture
- Vehicle 12V input enters through the main harness connector.
- Input protection and filtering are applied before regulation.
- A buck converter generates +5V_SYS.
- An LDO generates +3V3_SYS for digital logic.
- Power rails are distributed using internal plane pours.

### Grounding Strategy
- **DGND**: Continuous ground plane used as the primary reference.
- **PGND**: Localized copper for high-current and switching circuits.
- **AGND**: Localized island for ADC and sensor conditioning.
- PGND and AGND are tied to DGND at single, controlled points.

---

## Control and Logic
- An ESP32 microcontroller acts as the main processing and communication unit.
- GPIOs are isolated from high-energy outputs using logic buffers.
- ACT_PERMIT logic ensures outputs are disabled unless all safety conditions are met.
- KILL_IN provides an external safety override through the main harness connector.

---

## Power Supervision
- Comparator circuits monitor:
  - 12V_PROT rail
  - +5V_SYS rail
- Comparator outputs are referenced to 3.3V logic levels.
- Hysteresis is implemented to prevent false triggering.
- Power-good signals are routed to both MCU and safety logic.

---

## Sensing and Analog Domain
- Sensors operate from the 5V domain.
- Analog signal conditioning and ADC reference use AGND.
- AGND is isolated to minimize coupling from digital and power noise.
- ADC results are processed by the MCU.

---

## Actuation
- High-side drivers switch protected 12V to external loads.
- Actuators are enabled only when ACT_PERMIT is asserted.
- Gate control is buffered and logic-gated for safety.
- High di/dt currents are confined to the PGND region.

---

## Communication
- CAN bus is used for vehicle communication.
- Differential routing is maintained with continuous ground reference.
- CAN circuitry is placed close to the harness connector for EMI control.

---

## RF Considerations
- ESP32 antenna area is copper-free on all layers.
- No routing, vias, or pours are present under the antenna region.
- Switching and high-current circuitry is kept away from RF areas.

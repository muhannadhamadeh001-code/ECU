# ECU V4 – Safety, Monitoring & Power Supervision Board

## Overview
V4 is the supervisory and safety layer of the modular ECU architecture.

This board does **not** drive actuators or process sensor data directly.
Instead, it monitors system health, enforces safety conditions, and controls
whether the actuator domain is allowed to operate.

---

## Functional Scope

### Power & Voltage Monitoring
- Battery input monitoring (12V_PROT)
- 5V rail supervision
- 3.3V rail supervision
- Comparator-based OK signals with hysteresis
- Precision reference generated using TL431

### System Safety & Protection
- Fault detection and latching
- Manual fault clear (latched reset)
- SAFE_OK logic generation
- Global actuator enable / disable logic
- Emergency KILL path support

### Control Logic
- Hardware-based decision logic (no firmware dependency)
- AND-gated safety conditions
- Schmitt-trigger fault conditioning
- Fault memory via latch (persistent fault behavior)

### Power Domain Control
- Separation between:
  - Logic alive
  - Actuator enabled
- ACT_PERMIT / ACT_PERMIT_N signals exported to V3

---

## What V4 Does NOT Do
- No MCU or firmware
- No power regulation (handled in V1)
- No sensor signal conditioning (handled in V2)
- No actuator driving (handled in V3)
- No ISO-26262 certification (educational architecture focus)

---

## Interfaces

### Interface with V1 (Core)
- Receives system power rails
- Reports SAFE_OK and FAULT status
- Can inhibit system operation via KILL logic

### Interface with V3 (Actuators)
- Provides ACT_PERMIT / ACT_PERMIT_N
- Enforces hardware-level actuator disable
- Independent of firmware state

---

## Design Philosophy
- Hardware-first safety
- Deterministic behavior
- Fail-safe defaults
- Clear separation of responsibilities between ECU layers

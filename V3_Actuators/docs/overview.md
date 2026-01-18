# V3 Overview

V3 is the ECU’s output driver stage. It converts low-power MCU GPIO/PWM signals into protected 12V-domain low-side outputs.

**Scope**
- 8x low-side output channels
- Suitable for low/mid-power loads (educational use)
- No closed-loop control, diagnostics, or current sensing in this revision

**Non-scope**
- Injector peak/hold drivers
- High-side drivers (production-grade)
- CAN/LIN/diagnostics
- ISO-26262 compliance

**System block**
Sensors → V2 → V1 (control) → V3 (drivers) → Actuators

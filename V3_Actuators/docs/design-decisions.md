# Design Decisions

## Low-side switching (primary)
Low-side switching was chosen because it is common in ECU output stages, simpler to implement, and safer for early prototypes.

## MOSFET choice: AO3400A (SOT-23)
- Logic-level gate drive
- Simple, low-cost, widely available
- Suitable for educational low/mid-power loads

## Flyback diode: SS34
- Required for inductive loads (relays/solenoids)
- Placed near output channels to minimize loop area and improve clamp effectiveness

## Supply transient protection: SMBJ24A TVS
- Added across `12V_LOAD ↔ PGND` at the power entry region
- Protects the board from supply spikes and wiring transients (educational robustness)

## Grounding: DGND vs PGND with single-point tie
- High-current return handled on PGND copper
- Logic reference handled on DGND copper
- A single 0Ω tie creates an intentional star point to reduce noise injection into logic ground

## 12V distribution strategy
- A top-layer 12V bus/polygon feeds all flyback diodes with short stubs
- Reduces impedance and improves consistency across channels

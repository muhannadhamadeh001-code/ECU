# ECU V4 – Design Decisions & Rationale

## Why a Separate V4 Board?
Separating safety and supervision from control logic mirrors real ECU architectures.
This ensures:
- safety logic is not firmware-dependent
- faults cannot be masked by software bugs
- actuator enable is hardware-controlled

## Why Comparator-Based Monitoring?
Comparators provide:
- deterministic thresholds
- fast response
- operation independent of MCU state

## Why Fault Latching?
Latched faults prevent unsafe automatic recovery.
A fault must be acknowledged and cleared intentionally.

## Why 2-Layer PCB?
The board was intentionally routed as 2-layer to:
- enforce good grounding discipline
- expose real-world routing constraints
- improve learning value

A 4-layer stackup would reduce routing pressure but was not required functionally.

## Safety Philosophy
If any monitored rail is invalid OR a fault is latched:
→ ACT_PERMIT is forced LOW
→ Actuators are disabled regardless of firmware intent

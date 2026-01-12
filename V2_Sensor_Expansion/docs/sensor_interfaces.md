# Sensor Interfaces

## 0–5V Analog Sensors (TPS/MAP/Oil/AUX)
Sensors are external and connect via 3-pin headers:
- Pin 1: +5V sensor supply
- Pin 2: Sensor ground (AGND)
- Pin 3: Signal (0–5V)

### Input Conditioning (per channel)
- Series resistor: 100Ω
- Shunt capacitor: 100nF to AGND
- TVS diode: SMF5.0A to AGND (sensor-facing protection)
- Optional 0Ω link before ADC pin for isolation/debug (if populated)

## NTC Temperature Inputs (IAT/ECT)
NTCs are external and connect via 2-pin headers:
- Pin 1: NTC node
- Pin 2: AGND

### Divider & Filtering (per NTC channel)
- Pull-up to `2V5_REF`: 10k (1%)
- RC filter into ADC:
  - Series resistor: 1k
  - Capacitor: 100nF to AGND

NTC selection target:
- 10k @ 25°C
- B-value ≈ 3950–3960K
- Automotive temperature range suitable for engine-bay sensors

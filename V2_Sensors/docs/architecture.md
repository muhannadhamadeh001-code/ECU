# V2 Architecture

## What V2 is
V2 is a sensor acquisition expansion board. It does not include an MCU, CAN, USB, or power conversion.  
Its purpose is to condition real-world automotive sensor signals and digitize them using an external ADC.

## Data Path
External sensors → Protection & filtering → ADC → SPI → V1 ECU Core

## Power Domains
- `5V_A`: Analog/sensor supply rail (from V1)
- `3V3_D`: Digital rail for ADC digital domain + SPI (from V1)
- `2V5_REF`: Precision reference used as ADC reference and as the divider reference for NTC channels

## Ground Strategy
- `AGND`: analog return for ADC analog, reference, RC filters, TVS returns, and sensor grounds
- `DGND`: digital return for SPI header and ADC digital supply
- Single-point `AGND ↔ DGND` tie located near the ADC to control return current paths
- On 2-layer layout, a continuous ground plane is maintained; domain separation is enforced by placement/routing and a controlled tie point

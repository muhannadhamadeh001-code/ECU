# Design Decisions

## External ADC vs MCU ADC
An external SPI ADC is used to improve measurement repeatability and reduce reliance on MCU internal ADC limitations (noise, non-linearity, timing jitter).

## Precision Reference (2.5V)
A dedicated precision reference defines the ADC measurement range and stabilizes conversions independent of supply ripple.

## Reference Voltage Choice
2.5V is used as ADC reference and as the divider reference for NTC channels, enabling consistent scaling and reducing noise sensitivity vs a 5V reference.

## Input Conditioning Standardization
All 0–5V analog inputs use the same protection/filter cell:
- 100Ω series
- 100nF shunt to AGND
- TVS diode to AGND

This simplifies validation and reduces design variability across channels.

## AGND/DGND Discipline
Separate analog and digital ground nets are used with a single-point tie near the ADC.  
This controls return currents and reduces coupling from fast digital edges (SPI) into sensitive analog nodes (ADC inputs + reference).

## 2-Layer Layout Constraint
V2 is designed to be manufacturable on 2 layers while maintaining mixed-signal discipline through:
- Component placement hierarchy (ADC + reference core first)
- Bottom reference plane strategy
- Short return paths for RC and reference decoupling

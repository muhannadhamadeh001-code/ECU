# Manufacturing Notes

This document provides fabrication, assembly, and bring-up notes for the
ESP32 automotive CAN controller PCB.

---

## 1. PCB Fabrication Parameters

**Recommended PCB Specifications:**
- Layers: 4
- Thickness: 1.6 mm
- Material: FR-4
- Copper weight:
  - Outer layers: 1 oz
  - Inner layers: 1 oz

---

## 2. Controlled Impedance Routing

**Differential Pairs:**
- USB D+ / D−
- CANH / CANL

**Target Impedances:**
- USB 2.0: ~90 Ω differential
- CAN: ~120 Ω differential

Continuous ground reference is maintained under all high-speed signals.

---

## 3. Assembly Considerations

**Recommended Assembly Method:**
- Reflow soldering for SMD components
- Hand soldering acceptable for:
  - Headers
  - Buttons
  - Connectors

**Critical Components:**
- ESP32 module
- Buck converter
- USB-UART IC
- CAN transceiver

---

## 4. Via Usage and Grounding

- Via-in-pad used for:
  - Decoupling capacitors
  - Power connections
- Ground stitching vias placed throughout the board
- Thermal relief used where appropriate for solderability

---

## 5. ESD and Protection Placement

- TVS diodes placed as close as possible to connectors
- Short, direct paths from TVS to ground plane
- USB-C shield connected to ground using stitching vias

---

## 6. Automotive Usage Disclaimer

⚠ **Important Notice**

This board is:
- Not automotive-qualified (AEC-Q100)
- Intended for:
  - Prototyping
  - Development
  - Educational use
  - Non-safety-critical applications

It must not be used in safety-critical vehicle systems.

---

## 7. Bring-Up Checklist

Before first power-up:
- Perform visual inspection
- Check for shorts between power rails
- Verify polarity of:
  - Electrolytic capacitors
  - TVS diodes
- Power the board using a current-limited supply initially

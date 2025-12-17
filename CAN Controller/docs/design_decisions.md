# Design Decisions

This document summarizes the key architectural and engineering decisions made
during the design of the ESP32-based automotive CAN controller, along with the
rationale behind each choice.

---

## 1. System Architecture

The system is designed as a modular embedded controller that interfaces between
a vehicle CAN network and a PC.

Primary design goals:
- Robust operation in automotive electrical environments
- Clear separation of power, logic, and communication domains
- Ease of debugging and development
- Scalability for future revisions

The ESP32 acts as the central processing unit, while dedicated ICs handle
power conversion and physical-layer communication.

---

## 2. Microcontroller Selection

**Decision:** ESP32 microcontroller

**Rationale:**
- Integrated CAN controller (TWAI)
- Large ecosystem and development tool support
- Integrated Wi-Fi and Bluetooth for future expansion
- Sufficient processing power and memory for automotive-style applications

**Tradeoff:**
- ESP32 is not AEC-Q100 qualified
- Acceptable for development, prototyping, and non-safety-critical use

---

## 3. Power Architecture

**Decision:** Two-stage power regulation  
12V Automotive → Buck Converter (5V) → LDO (3.3V)

**Rationale:**
- Buck converter provides efficient step-down from automotive 12V
- LDO provides a low-noise 3.3V rail for the ESP32 and logic
- Separates switching noise from sensitive MCU and RF circuitry

**Alternative Considered:** Linear regulation only  
**Rejected due to:** Excessive power dissipation and thermal stress

---

## 4. USB Architecture

**Decision:** USB-C connector with USB-to-UART bridge

**Rationale:**
- USB-UART provides reliable firmware flashing and debugging
- Avoids firmware complexity of native USB implementation
- Common and proven development approach

**Power Domain Note:**
- USB-UART is powered directly from USB VBUS (5V_USB)
- Allows flashing and debugging without vehicle power
- Isolates development interface from automotive power noise

---

## 5. USB-C Connector Choice

**Decision:** USB-C configured for USB 2.0 device operation

**Rationale:**
- Reversible connector improves usability
- Higher mechanical durability than Micro-USB
- Widely available cables and connectors
- Supports ESD protection and shield grounding

---

## 6. CAN Interface Design

**Decision:** Dedicated CAN transceiver between ESP32 and vehicle network

**Rationale:**
- ESP32 handles CAN protocol logic
- Transceiver handles:
  - Differential signaling (CANH/CANL)
  - Voltage level translation
  - Electrical robustness
- Required for reliable automotive CAN communication

---

## 7. CAN Termination Strategy

**Decision:** Selectable CAN termination via jumpers

**Rationale:**
- CAN bus requires 120Ω termination at each end
- Board may act as:
  - End node (termination enabled)
  - Mid-bus node (termination disabled)
- Jumper-based termination provides flexibility during testing

---

## 8. Protection Strategy

**Protection Implemented:**
- TVS diodes on:
  - Automotive 12V input
  - USB data lines
  - CANH and CANL
- Input protection before buck converter
- Ferrite beads for high-frequency noise suppression

**Rationale:**
- Automotive environments include transients, ESD, and inductive spikes
- Protection improves survivability and reliability

---

## 9. PCB Stackup and Layout

**Decision:** 4-layer PCB

**Layer Stack:**
1. Top layer – Signals and components  
2. Inner layer 1 – Solid ground plane  
3. Inner layer 2 – Power distribution and routing  
4. Bottom layer – Signals  

**Rationale:**
- Continuous ground reference for USB, CAN, and RF
- Reduced EMI and noise coupling
- Improved return current paths

---

## 10. RF Considerations

**Decision:** Dedicated RF keep-out around ESP32 antenna

**Rationale:**
- RF performance is sensitive to copper and ground proximity
- Keep-out follows ESP32 reference design guidelines
- Ground stitching used around RF boundary, not under antenna

---

## 11. Debug and Development Features

**Included Features:**
- UART RX/TX
- DTR / RTS for automatic boot and flashing
- Reset and boot buttons
- Test points for power rails

**Rationale:**
- Simplifies bring-up and debugging
- Reduces risk during early hardware revisions

# System Block Diagram

This document describes the high-level block diagram of the system and how the major functional blocks interact with each other.

---

## 1. High-Level Block Diagram

![System Block Diagram](images/block_diagram.png)

---

## 2. Power Flow Overview

![Power Flow Diagram](images/power_flow.png)

---

## 3. Communication Flow Overview

![Communication Flow Diagram](images/communication_flow.png)

---

## 4. Block Descriptions

### 4.1 Power Input and Regulation

- 12V automotive input enters the system
- Input protection handles transients and reverse polarity
- Buck converter steps 12V down to 5V
- LDO generates a clean 3.3V rail
- ESP32 and logic are powered from 3.3V

---

### 4.2 ESP32 Microcontroller

The ESP32 is the central controller responsible for:
- Running firmware
- Managing CAN communication
- Handling USB serial communication
- Executing application logic

---

### 4.3 USB Communication Path

- USB-C connector interfaces with the PC
- USB-UART bridge converts USB protocol to UART
- UART TX/RX connect directly to the ESP32
- DTR and RTS signals control reset and boot mode

---

### 4.4 CAN Communication Path

- ESP32 communicates via CAN TX/RX logic signals
- CAN transceiver converts logic signals to CANH/CANL
- Vehicle CAN network connects through the transceiver
- Differential signaling ensures noise immunity

---

## 5. Communication Directionality

All communication paths are bidirectional:

- PC ⇄ ESP32 (via USB-UART)
- Vehicle Network ⇄ ESP32 (via CAN)

This enables real-time diagnostics, control, and data logging.

---

## 6. Design Intent

The block diagram reflects a production-style ECU architecture with:
- Isolated physical layers
- Centralized firmware control
- Automotive-grade power handling
- Scalable communication interfaces

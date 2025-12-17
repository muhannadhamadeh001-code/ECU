# System Architecture Overview

## 1. Purpose of the System

This project is an automotive-oriented embedded controller designed to:

- Interface with a vehicle CAN bus
- Communicate with a PC via USB
- Execute application firmware on an ESP32 microcontroller
- Operate safely from a 12V automotive power source

The design follows real ECU principles by separating **power regulation**, **processing**, and **communication interfaces**.

---

## 2. High-Level Architecture

The system is composed of the following main blocks:

1. Power Input & Regulation  
2. ESP32 Microcontroller  
3. USB Communication (USB-C + USB-UART)  
4. CAN Communication (CAN Transceiver)  
5. External Interfaces (PC and Vehicle Network)

Each block has a clearly defined role and electrical boundary to improve reliability, noise immunity, and scalability.

---

## 3. Power Architecture

### 3.1 12V Automotive Input

The board is powered from a 12V vehicle supply, which may contain:
- Voltage spikes
- Transients
- Reverse polarity events

---

### 3.2 Input Protection

Before regulation, the 12V input passes through protection circuitry designed to:
- Protect against reverse polarity
- Clamp transient voltage spikes
- Increase survivability in automotive environments

---

### 3.3 Buck Converter (12V → 5V)

A switching buck converter steps the protected 12V input down to a regulated 5V rail.

Reasons for using a buck converter:
- High efficiency
- Low heat dissipation
- Suitable for automotive current levels

The 5V rail is used as:
- The primary intermediate supply
- The power source for USB-related circuitry

---

### 3.4 LDO Regulator (5V → 3.3V)

A low-dropout (LDO) regulator generates a clean 3.3V rail from the 5V supply.

Reasons for using an LDO:
- Low output noise
- Stable voltage for digital logic
- Improved MCU and RF reliability

The ESP32 is powered exclusively from the 3.3V rail.

---

## 4. Processing Core (ESP32)

The ESP32 is the central processing unit of the system.

Responsibilities:
- Running application firmware
- Implementing CAN protocol logic
- Handling USB-UART communication
- Managing GPIOs and system behavior

The ESP32 does not interface directly with USB or CAN physical layers.  
All physical signaling is handled by dedicated external ICs.

---

## 5. USB Communication Subsystem

### 5.1 USB-C Connector

The USB-C connector provides:
- Data communication with a PC
- 5V power availability when connected

The connector supports USB 2.0 differential signaling (D+ / D−) and includes ESD protection to safeguard against electrostatic discharge events.

---

### 5.2 USB-UART Bridge

A USB-to-UART bridge IC converts USB protocol signals into UART-level TX/RX signals for the ESP32.

Primary functions:
- Firmware flashing
- Serial logging
- Debug communication

Communication path:
Additional control signals (DTR and RTS) are used to:
- Automatically reset the ESP32
- Place the ESP32 into bootloader mode for flashing

---

## 6. CAN Communication Subsystem

### 6.1 CAN Transceiver

The CAN transceiver converts ESP32 logic-level CAN TX/RX signals into differential CANH and CANL signals suitable for the automotive bus.

Functions of the CAN transceiver:
- Electrical isolation of the MCU
- Robust differential signaling
- Protection against bus disturbances

---

### 6.2 Vehicle Network Interface

The CAN transceiver connects directly to the vehicle CAN bus.

Communication path:
Termination and protection components ensure signal integrity and compliance with CAN bus requirements.

---

## 7. Communication Directionality

All communication interfaces in the system are bidirectional:

- USB: PC ⇄ ESP32
- CAN: Vehicle Network ⇄ ESP32

This enables:
- Data logging
- Diagnostics
- Command and control applications

---

## 8. Design Philosophy

The system follows these key design principles:
- Clear separation of power, logic, and physical layers
- Automotive-aware protection and regulation
- Modular and scalable communication interfaces
- Firmware-centric system control

The architecture closely mirrors real automotive ECUs.

---

## 9. Summary

This design integrates:
- Automotive-grade power handling
- Robust USB and CAN communication
- A capable ESP32 processing core

The result is a production-style embedded controller suitable for learning, experimentation, and future automotive expansion.

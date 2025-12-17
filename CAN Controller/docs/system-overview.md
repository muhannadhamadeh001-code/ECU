# System Overview

This board is an ESP32-based automotive CAN controller designed to interface
between a vehicle CAN network and external tools such as a PC.

The system consists of the following major functional blocks:
- Automotive power input and protection
- Power regulation (buck + LDO)
- ESP32 microcontroller
- USB-C to UART interface
- CAN transceiver
- Debug and control signals (EN, BOOT, RESET)

The ESP32 acts as the central controller, processing CAN data, handling logic,
and communicating with a PC over USB via a USB-to-UART bridge.

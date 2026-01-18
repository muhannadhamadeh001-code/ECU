# Firmware Overview

Firmware is the low-level software running on the ESP32.

It is responsible for:
- Initializing hardware peripherals
- Handling CAN communication
- Managing UART communication
- Processing and forwarding data
- Logging and debugging

## Firmware Flashing

Firmware is flashed via:
PC → USB-C → USB-UART → ESP32

No vehicle power is required for flashing.

## Runtime Behavior

During operation:
- ESP32 reads data from the CAN bus
- Processes or filters messages
- Sends data to a PC or other systems as needed

Firmware is stored in the ESP32's internal flash memory.

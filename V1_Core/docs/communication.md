# Communication Interfaces

## USB Communication

USB-C is used exclusively for:
- Firmware flashing
- Serial logging
- Debugging

USB data lines (D+ / D−) connect to a USB-to-UART bridge IC.

The USB connection is **bidirectional**, allowing:
- PC → ESP32 (firmware, commands)
- ESP32 → PC (logs, data)

## UART Communication

UART (TX/RX) is used internally between:
- USB-UART bridge
- ESP32 microcontroller

UART signals are logic-level (3.3V) and provide a simple, reliable debug channel.

Additional UART control signals:
- DTR / RTS: used to automate ESP32 boot and reset during flashing

## CAN Communication

CAN is used to communicate with the vehicle network.

- CAN_TX / CAN_RX: logic-level signals between ESP32 and CAN transceiver
- CANH / CANL: differential signals on the vehicle CAN bus

Communication is bidirectional:
- ESP32 can transmit messages to the vehicle
- ESP32 can receive messages from the vehicle

Termination resistors ensure signal integrity on the CAN bus.

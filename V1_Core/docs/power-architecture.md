# Power Architecture

## Power Domains

The system contains **three distinct power domains**:

### 1. Automotive 12V Domain
- Source: Vehicle battery
- Includes input protection against reverse polarity, load dump, and transients
- Feeds the buck converter

### 2. 5V Buck Rail
- Generated from the protected 12V automotive input
- Supplies downstream regulators and peripherals
- Designed for efficiency under automotive conditions

### 3. 3.3V Logic Rail
- Generated via an LDO from the 5V buck rail
- Supplies the ESP32 and all logic-level components
- Provides low-noise, stable voltage for MCU operation

## USB Power Domain (5V_USB)

The USB-to-UART interface is powered directly from USB VBUS (5V_USB), not from
the automotive power path.

This allows:
- Firmware flashing without vehicle power
- Debugging and logging using only a PC
- Electrical isolation from automotive transients

The USB power domain does not power the ESP32 directly.

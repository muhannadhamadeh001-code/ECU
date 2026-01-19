# V2.5 IMU Board (Inertial Measurement)

This folder contains ECU V2.5 — a small 6-axis IMU board used to introduce inertial sensing and enable firmware-level sensor fusion on the ECU core (V1).

## What’s included
- Spec: `V2.5.md`
- Schematic and PCB exports: `hardware/`
- Images/renders: `images/`

## How it connects
V1 provides +3V3 and communicates over SPI. V2.5 provides inertial measurements (accel/gyro) and an optional interrupt line.

## Why it exists
V2.5 upgrades the ECU from reading signals to understanding motion, without affecting safety logic or actuator permission.

# Power Design

The board accepts a 12V automotive input.

Protection is provided against:
- Reverse polarity
- Voltage transients
- ESD events

A buck converter steps 12V down to 5V efficiently.
A linear regulator then generates 3.3V for the ESP32.

Input and output capacitors are placed close to their respective devices
to minimize current loop area and noise.

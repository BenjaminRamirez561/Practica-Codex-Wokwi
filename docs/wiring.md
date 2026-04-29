# Wiring (Raspberry Pi Pico W)

## Overview

The design connects a 4x4 matrix keypad to 8 GPIOs and drives 12 LEDs from 12 GPIOs.
All LED cathodes are tied to GND. Each LED anode is routed through a 220Ω resistor to a GPIO.

## Components

- Raspberry Pi Pico W (RP2040)
- 4x4 membrane keypad (`R1..R4`, `C1..C4`)
- 12x LEDs
- 12x 220Ω resistors for LEDs
- 4x 1kΩ pull-up resistors for keypad rows

## GPIO Pin Mapping

### Keypad Matrix Connections

| Keypad Signal | Pico W GPIO | Notes |
|---|---:|---|
| C4 | GP16 | Column input |
| C3 | GP17 | Column input |
| C2 | GP18 | Column input |
| C1 | GP19 | Column input |
| R4 | GP20 | Row line |
| R3 | GP21 | Row line |
| R2 | GP22 | Row line |
| R1 | GP26 | Row line |

### LED Connections

| LED Label | Firmware Index | Pico W GPIO |
|---|---:|---:|
| LED1 (`1`) | 0 | GP11 |
| LED2 (`2`) | 1 | GP10 |
| LED3 (`3`) | 2 | GP9 |
| LED4 (`4`) | 3 | GP8 |
| LED5 (`5`) | 4 | GP7 |
| LED6 (`6`) | 5 | GP6 |
| LED7 (`7`) | 6 | GP5 |
| LED8 (`8`) | 7 | GP4 |
| LED9 (`A`) | 8 | GP3 |
| LED10 (`B`) | 9 | GP2 |
| LED11 (`C`) | 10 | GP28 |
| LED12 (`D`) | 11 | GP27 |

## Power and Ground

- Keypad row pull-up network (`rp1..rp4`) ties to **3V3**.
- LED cathodes connect to **GND**.
- Pico GP0/GP1 are connected to serial monitor in Wokwi.

## Assumptions and Notes

- The supplied diagram uses `wokwi-pi-pico`; this documentation targets **Pico W** pin-compatible usage.
- GPIO numbering in firmware is BCM-style RP2040 GP numbers (e.g., `26` means `GP26`).

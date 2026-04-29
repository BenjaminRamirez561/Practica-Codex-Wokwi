# Raspberry Pi Pico W Keypad-to-LED Controller

A Raspberry Pi Pico W project that reads a 4x4 membrane keypad and controls 12 LEDs based on key presses.

> The firmware logic is preserved exactly from the provided source. This repository cleanup focuses on structure and documentation.

## Repository Structure

```text
.
├── CMakeLists.txt
├── diagram.json
├── docs/
│   ├── architecture.md
│   └── wiring.md
├── include/
└── src/
    └── main.cpp
```

## Features

- 4x4 matrix keypad scanning using `Keypad.h`
- 12 individually addressable LEDs
- Group LED control using special keys:
  - `9` turns on LEDs 1-8
  - `0` turns off LEDs 1-8
  - `*` turns on LEDs A-D
  - `#` turns off LEDs A-D
- 10 ms loop delay for keypad polling stability

## Hardware Components (from `diagram.json`)

- 1x Raspberry Pi Pico / Pico W
- 1x 4x4 membrane keypad
- 12x LEDs (8 blue + 4 red)
- 12x 220Ω series resistors (LED current limiting)
- 4x 1kΩ pull-up resistors (keypad row lines)
- hookup wires

## GPIO Mapping Summary

### Keypad
- Rows: GP26, GP22, GP21, GP20
- Columns: GP19, GP18, GP17, GP16

### LEDs
- LED1..LED8: GP11, GP10, GP9, GP8, GP7, GP6, GP5, GP4
- LED9..LED12 (A..D): GP3, GP2, GP28, GP27

> Full pin-by-pin map is in [`docs/wiring.md`](docs/wiring.md).

## Build / Run Options

Because this firmware uses Arduino APIs (`setup`, `loop`, `digitalWrite`, `Keypad.h`), use one of these:

1. **Arduino IDE (recommended)** with **Raspberry Pi Pico/RP2040** core.
2. **PlatformIO** with an RP2040 board and the Keypad library.
3. **Wokwi simulation** (fastest path for this repository).

## Run in Wokwi

1. Create/import a Raspberry Pi Pico project in Wokwi.
2. Use `src/main.cpp` as the sketch content.
3. Use `diagram.json` for the circuit definition.
4. Start simulation and press keypad buttons.

## Run on Real Hardware (Pico W)

1. Wire according to [`docs/wiring.md`](docs/wiring.md).
2. Install Arduino IDE + RP2040 core + Keypad library.
3. Select **Raspberry Pi Pico W** board.
4. Put Pico W in BOOTSEL mode, upload firmware.
5. Verify LED behavior using keypad input.

## Wi-Fi Note

This project does **not** use Wi-Fi in its current firmware. No credentials are required.

## Behavior Preservation

- No functional changes were made to keypad-to-LED mapping logic.
- Documentation and project organization were added only.

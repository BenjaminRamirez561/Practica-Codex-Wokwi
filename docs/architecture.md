# Firmware Architecture

## High-Level Design

The firmware implements a polling loop:

1. Scan keypad for a new key event.
2. If a key is pressed, map the key to one or more LED state changes.
3. Delay for 10 ms and repeat.

## Source Layout

- `src/main.cpp` contains all runtime logic:
  - GPIO/keymap definitions
  - keypad object construction
  - initialization in `setup()`
  - key processing in `loop()`

## Core Data Structures

- `keys[4][4]`: maps keypad matrix positions to characters.
- `ledPins[12]`: GPIO order used by all LED actions.
- `rowPins[4]`, `colPins[4]`: keypad electrical matrix routing.

## Runtime Flow

### `setup()`

- Iterates through `ledPins`
- Sets each as `OUTPUT`
- Drives all LEDs `LOW` (off)

### `loop()`

- Reads one key via `keypad.getKey()`
- If key exists (`!= NO_KEY`), executes a `switch` action:
  - direct per-key LED on (`1..8`, `A..D`)
  - grouped operations (`9`, `0`, `*`, `#`)
- waits 10 ms via `delay(10)`

## Behavioral Contract (Unchanged)

- Single keys mostly latch LEDs on.
- Group-off keys only clear their corresponding ranges.
- No auto-timeout or global reset key exists.
- Wi-Fi is not referenced by firmware.

## Portability Note

Although the MCU target is RP2040/Pico W, the source is written with Arduino framework APIs rather than Pico SDK-native APIs. Repository structure is normalized for C/C++ projects without altering execution logic.

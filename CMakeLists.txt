cmake_minimum_required(VERSION 3.13)
project(pico_w_keypad_leds C CXX)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# NOTE:
# The application logic in src/main.cpp uses the Arduino-style API
# (setup/loop, pinMode, digitalWrite, delay, Keypad.h).
# Build this project with the Arduino-Pico toolchain (e.g., PlatformIO or Arduino IDE).
# This CMake file documents repository structure for C/C++ projects.

add_custom_target(firmware SOURCES src/main.cpp)

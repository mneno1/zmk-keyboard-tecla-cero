# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

ZMK firmware for the "tecla-cero" split keyboard with trackball support. Uses the BMP Boost board (nRF52840-based) and supports both USB and BLE connections.

## Build System

Firmware is built via GitHub Actions using the ZMK build workflow. Push to trigger builds, or use workflow_dispatch for manual builds. Build artifacts are defined in `build.yaml`.

### Build Configurations

| Artifact Name | Description |
|--------------|-------------|
| `tecla_cero_right_central` | Right half (central role) - trackball side, connect USB here |
| `tecla_cero_left_peripheral` | Left half (peripheral role) |
| `tecla_cero_left_central` | Left half (central role) - if connecting USB to left side |
| `tecla_cero_right_peripheral` | Right half (peripheral role) - if connecting USB to left side |
| `settings_reset` | Reset firmware for clearing settings |

Flash `_central` firmware to the trackball side (right), and `_peripheral` to the other side (left).

## Architecture

### West Manifest (`config/west.yml`)
Defines external dependencies from zmkfirmware and sekigon-gonnoc repos:
- ZMK core (v0.3)
- BMP Boost board support
- PAW3222 trackball driver
- Status LED, CDC ACM bootloader trigger, non-lipo battery management features

### Shield Definition (`boards/shields/tecla_cero/`)
- `tecla_cero.dtsi` - Main device tree include: GPIO matrix (4x5), trackball SPI config
- `tecla_cero_left.overlay` / `tecla_cero_right.overlay` - Split half configurations
- `*.conf` - Kconfig options (ZMK Studio, BLE power, battery monitoring)

### Keymap (`config/keymap.keymap`)
Default keymap with 3 layers for 38-key layout. Editable via ZMK Studio (studio feature enabled).

## Hardware Configuration

### Matrix: 4 rows × 5 columns (per side)
- Total: 38 keys
- ROW0-ROW3, COL0-COL4

### GPIO Pin Assignment (TODO: Adjust to actual wiring)
Current pins are placeholders from torabo-tsuki LP reference. Update `tecla_cero.dtsi` with actual GPIO pins from your PCB design.

### Trackball
- Right side only (PAW3222 via SPI)
- SPI pins in `tecla_cero.dtsi` need to match your PCB

## Key Features

- ZMK Studio support for live keymap editing
- PAW3222 trackball via SPI
- Non-lipo battery monitoring (for AAA batteries)
- Status LED
- CDC ACM bootloader trigger for easy reflashing

# Macro-Hackapad

A custom mechanical keyboard with a detachable wireless macropad, dual RGB OLED displays, and smart wireless connectivity.

## Features

- **65% Layout** - Compact keyboard with arrow keys
- **Detachable Macropad** - 3x3 (9 key) hot-swap macropad with pogo pin connection
- **Dual OLED Displays** - Full-color 1.3" displays on both main keyboard and macropad
- **Wireless** - 2.4GHz nRF24L01+ with single dongle
- **Smart Routing** - Macropad routes through main keyboard when docked, works independently when undocked
- **USB-C Charging** - Independent batteries with USB-C on each device
- **QMK/VIA Compatible** - Full programmability

## Documentation

| File | Description |
|------|-------------|
| [SPEC.md](SPEC.md) | Full hardware specifications |
| [BOM.md](BOM.md) | Bill of materials with costs |
| [docs/wireless-architecture.md](docs/wireless-architecture.md) | Wireless design details |

## Quick Specs

- **Main keyboard**: 68 keys, RP2040 MCU, nRF24L01+ wireless, 1.3" RGB OLED
- **Macropad**: 9 keys, RP2040 MCU, nRF24L01+ wireless, 1.3" RGB OLED
- **Connection**: 4-pin pogo pins when docked, wireless when undocked
- **Battery**: 1000mAh (main), 500mAh (macropad)
- **Latency**: ~1ms wireless

## Project Status

- [x] Specification complete
- [x] BOM created
- [ ] PCB design
- [ ] Case design
- [ ] Firmware
- [ ] Build

## Getting Started

1. Read [SPEC.md](SPEC.md) for full hardware details
2. Order parts from [BOM.md](BOM.md)
3. Design PCBs (see pinouts in SPEC.md)
4. Flash QMK firmware
5. Build and test

---

*Building in progress...*
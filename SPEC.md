# Macro-Hackapad - Hardware Specification

## Project Overview

A custom mechanical keyboard with a detachable wireless macropad, dual RGB OLED displays, and smart wireless connectivity.

- **Project name**: Macro-Hackapad
- **Type**: Custom mechanical keyboard + detachable macropad
- **Target users**: Gaming enthusiasts, power users who want programmable macros

---

## Main Keyboard Specifications

### Dimensions
- **Layout**: 65% with arrow keys
- **Width**: ~325mm
- **Depth**: ~108mm
- **Height**: ~15-20mm (without keycaps)
- **Key count**: 68 keys

### Key Switches
- **Type**: Hot-swap sockets (Kailh or Gateron compatible)
- **Mounting**: PCB mount
- **Recommended switches**: Gateron Milky Yellow (linear), Gateron Brown (tactile)

### Microcontroller
- **Primary**: Raspberry Pi RP2040 (for QMK/VIA compatibility)
- **Alternative**: nRF52840 (if using built-in Bluetooth)

### Wireless Module
- **Module**: nRF24L01+ PA/LNA variant
- **Frequency**: 2.4GHz
- **Latency**: ~1ms
- **Range**: ~10m line of sight

### Display
- **Type**: 1.3" RGB OLED (full color)
- **Driver**: SSD1327 or ST7789 (TFT alternative)
- **Resolution**: 128x128 pixels
- **Interface**: SPI

### Power
- **Battery**: 3.7V LiPo, 1000mAh
- **Charging**: USB-C, 5V/1A
- **Battery management**: TP4056 charger IC + protection circuit
- **Estimated battery life**: 20-30 hours (without RGB, depends on usage)

### Connection (Docked Macropad)
- **Connector**: 4-pin pogo pins
- **Pinout**: VCC, GND, D+, D- (or UART TX/RX for data)
- **Data**: Serial communication to macropad

---

## Macropad Specifications

### Dimensions
- **Layout**: 3x3 grid (9 keys) or 2x4 (8 keys)
- **Width**: ~80mm
- **Depth**: ~80mm
- **Height**: ~12-15mm (without keycaps)

### Key Switches
- **Type**: Hot-swap sockets
- **Key count**: 9 keys (3x3)

### Microcontroller
- **MCU**: RP2040 (same as main for firmware consistency)

### Wireless Module
- **Module**: nRF24L01+ (same as main)

### Display
- **Type**: 1.3" RGB OLED (same as main)
- **Position**: Top of macropad

### Power
- **Battery**: 3.7V LiPo, 500mAh
- **Charging**: USB-C
- **Estimated battery life**: 15-20 hours

### Connection (to Main Keyboard)
- **When docked**: 4-pin pogo pins, data tunnels through main keyboard
- **When undocked**: Independent wireless to dongle

---

## Wireless Architecture

### Single Dongle Design
- **Dongle MCU**: RP2040 with nRF24L01+
- **Connection to PC**: USB-C (appears as HID keyboard)

### Communication Modes

**Mode 1: Macropad Docked**
```
PC → Dongle (nRF24L01+) → Main Keyboard (nRF24L01+) → Macropad (via pogo)
```
- Macropad acts as peripheral, all traffic routes through main keyboard
- Lower latency for docked mode
- 4-pin connection carries UART data

**Mode 2: Macropad Undocked**
```
PC → Dongle → Main Keyboard (direct)
PC → Dongle → Macropad (direct)
```
- Both devices pair independently to dongle
- If one fails/disconnects, the other continues working
- Redundancy: either device works solo

### Pairing
- Each device has unique address
- Dongle stores up to 2 device addresses
- Auto-reconnect on power cycle

---

## PCB Pinouts (RP2040)

### Main Keyboard
| Function | GPIO Pin |
|----------|----------|
| Matrix Row 0 | GP0 |
| Matrix Row 1 | GP1 |
| Matrix Row 2 | GP2 |
| Matrix Row 3 | GP3 |
| Matrix Row 4 | GP4 |
| Matrix Col 0 | GP5 |
| Matrix Col 1 | GP6 |
| Matrix Col 2 | GP7 |
| Matrix Col 3 | GP8 |
| Matrix Col 4 | GP9 |
| OLED CS | GP10 |
| OLED DC | GP11 |
| OLED RST | GP12 |
| OLED MOSI | GP13 |
| OLED SCK | GP14 |
| nRF24 CE | GP15 |
| nRF24 CSN | GP16 |
| nRF24 IRQ | GP17 |
| nRF24 MOSI | GP18 |
| nRF24 MISO | GP19 |
| nRF24 SCK | GP20 |
| USB D+ | GP22 |
| USB D- | GP23 |
| Pogo TX | GP26 |
| Pogo RX | GP27 |
| Battery ADC | GP28 |

### Macropad
| Function | GPIO Pin |
|----------|----------|
| Matrix Row 0 | GP0 |
| Matrix Row 1 | GP1 |
| Matrix Row 2 | GP2 |
| Matrix Col 0 | GP3 |
| Matrix Col 1 | GP4 |
| Matrix Col 2 | GP5 |
| OLED CS | GP6 |
| OLED DC | GP7 |
| OLED RST | GP8 |
| OLED MOSI | GP9 |
| OLED SCK | GP10 |
| nRF24 CE | GP11 |
| nRF24 CSN | GP12 |
| nRF24 IRQ | GP13 |
| nRF24 MOSI | GP14 |
| nRF24 MISO | GP15 |
| nRF24 SCK | GP16 |
| USB D+ | GP18 |
| USB D- | GP19 |
| Battery ADC | GP20 |

---

## Firmware

### Framework
- **QMK Firmware** (with custom nRF24 driver)
- **VIA** for keymap configuration

### Features
- Per-key RGB backlighting (optional)
- OLED display with layer indicators, animations
- Programmable macros
- Multiple layers
- Wireless on/off toggle

---

## Mechanical Design

### Case
- **Material**: 3D printed PLA/ABS or CNC aluminum
- **Finish**: Matte or textured
- **Mounting**: Tray mount or top mount

### Magnet Alignment
- 4x 3mm neodymium magnets for macropad alignment
- Recessed pockets in case

### Pogo Pins
- 4-pin spring-loaded pogo pins
- 2mm pitch
- Gold-plated contacts

---

## Color Scheme

*To be determined by user*

---

## Status

- [x] Project concept defined
- [x] Hardware specifications finalized
- [x] BOM created
- [ ] PCB design started
- [ ] Case design started
- [ ] Firmware development
- [ ] Testing & validation
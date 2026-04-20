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
- **Primary**: RP2040 Plus Module (Waveshare or equivalent)
- **Features**: Pre-assembled with USB-C, 3.3V regulator, crystal, 8MB flash
- **Notes**: Uses dev board module instead of bare chip for easier assembly

### Wireless Module
- **Module**: nRF24L01+ PA/LNA variant
- **Frequency**: 2.4GHz
- **Latency**: ~1ms
- **Range**: ~10m line of sight

### Display
- **Type**: 1.3" Monochrome OLED (white)
- **Driver**: SSD1327
- **Resolution**: 128x128 pixels
- **Interface**: SPI

### Power
- **Battery**: 3.7V LiPo, 1000mAh
- **Charging**: USB-C, 5V/1A
- **Battery management**: TP4056 charger IC + protection circuit
- **Estimated battery life**: 20-30 hours (without RGB, depends on usage)

### Connection (Docked Macropad)
- **Connector**: 6-pin magnetic waterproof connector (pre-made)
- **Pinout**: VBUS, GND, TX, RX, D+, D-
- **Data**: UART serial communication to macropad when docked

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
- **MCU**: RP2040 Plus Module (same as main)

### Wireless Module
- **Module**: nRF24L01+ (same as main)

### Display
- **Type**: 1.3" Monochrome OLED (same as main)
- **Position**: Top of macropad

### Power
- **Battery**: 3.7V LiPo, 500mAh
- **Charging**: USB-C
- **Estimated battery life**: 15-20 hours

### Connection (to Main Keyboard)
- **When docked**: 6-pin magnetic connector, UART data tunnels through main keyboard
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

## PCB Pinouts (RP2040 Plus Module)

### Main Keyboard
| Function | GPIO Pin |
|----------|----------|
| Matrix Row 8 | GP0 |
| Matrix Row 9 | GP1 |
| Matrix Row 10 | GP2 |
| Matrix Row 11 | GP3 |
| Matrix Row 12 | GP4 |
| Matrix Row 13 | GP5 |
| Matrix Col 0 | GP6 |
| Matrix Col 1 | GP7 |
| Matrix Col 2 | GP8 |
| Matrix Col 3 | GP9 |
| Matrix Col 4 | GP10 |
| nRF24 MOSI | GP11 |
| nRF24 MISO | GP12 |
| nRF24 SCK | GP13 |
| nRF24 CE | GP14 |
| nRF24 CSN | GP15 |
| OLED CS | GP16 |
| OLED DC | GP17 |
| OLED RST | GP18 |
| Magnetic TX | GP19 |
| Magnetic RX | GP22 |
| I2C SCL (PCF8574) | GP23 |
| I2C SDA (PCF8574) | GP24 |
| Battery ADC | GP25 |
| USB 5V from module | For TP4056 charging |
| 3V3 from module | For nRF24L01+, OLED |

**PCF8574 GPIO Expander (I2C address 0x20)**
| Function | Expander Pin |
|----------|--------|
| Matrix Row 0 | P0 |
| Matrix Row 1 | P1 |
| Matrix Row 2 | P2 |
| Matrix Row 3 | P3 |
| Matrix Row 4 | P4 |
| Matrix Row 5 | P5 |
| Matrix Row 6 | P6 |
| Matrix Row 7 | P7 |

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
| OLED MOSI (shared SPI) | GP9 |
| OLED SCK (shared SPI) | GP10 |
| nRF24 CE | GP11 |
| nRF24 CSN | GP12 |
| nRF24 MISO | GP13 |
| nRF24 MOSI (shared SPI) | GP14 |
| nRF24 SCK (shared SPI) | GP15 |
| Magnetic TX | GP16 |
| Magnetic RX | GP17 |
| Battery ADC | GP18 |
| USB 5V from module | For TP4056 charging |
| 3V3 from module | For nRF24L01+, OLED |

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
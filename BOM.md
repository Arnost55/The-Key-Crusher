# Macro-Hackapad - Bill of Materials

## Main Keyboard Components

| Component | Quantity | Part Number | Est. Cost | Notes |
|-----------|----------|-------------|-----------|-------|
| **Microcontroller** | 1 | RP2040 Plus Module | $6-8 | Waveshare or equivalent, pre-assembled |
| **Wireless Module** | 1 | nRF24L01+ PA/LNA PCB antenna | $2-4 | PCB antenna version (no external stick) |
| **OLED Display** | 1 | 1.3" Monochrome OLED (SSD1327) | $5-8 | SPI interface, white on black |
| **GPIO Expander** | 1 | PCF8574 | $1-2 | I2C 8-port IO expander for matrix |
| **Battery** | 1 | LiPo 3.7V 1000mAh | $8-12 | JST connector |
| **Charger IC** | 1 | TP4056 + protection | $1-2 | USB-C charging, module USB powers this |
| **Magnetic Connector** | 1 | 6-pin waterproof magnetic | $5-10 | Pre-made, for macropad dock |
| **Key Switches** | 68 | Kailh/Gateron hot-swap | $20-40 | Hot-swap sockets |
| **Keycaps** | 1 set | 65% Cherry profile | $25-50 | ABS or PBT |
| **Diodes** | 68 | 1N4148 | $1-2 | For matrix, 1 per key |
| **Capacitors** | 4 | 10µF, 100nF | $0.30 | Power filtering near ICs |
| **Resistors** | 2 | 10kΩ pull-up | $0.10 | I2C pull-ups (if needed) |

## Macropad Components

| Component | Quantity | Part Number | Est. Cost | Notes |
|-----------|----------|-------------|-----------|-------|
| **Microcontroller** | 1 | RP2040 Plus Module | $6-8 | Same as main |
| **Wireless Module** | 1 | nRF24L01+ PA/LNA PCB antenna | $2-4 | Same as main |
| **OLED Display** | 1 | 1.3" Monochrome OLED (SSD1327) | $5-8 | Same as main |
| **Battery** | 1 | LiPo 3.7V 500mAh | $5-8 | Smaller capacity |
| **Charger IC** | 1 | TP4056 + protection | $1-2 | Same as main |
| **Magnetic Connector** | 1 | 6-pin waterproof magnetic | $5-10 | Receptacle side |
| **Key Switches** | 9 | Kailh/Gateron hot-swap | $3-5 | 3x3 grid |
| **Keycaps** | 1 set | 1u keycaps (9x) | $5-10 | Match main keyboard |
| **Diodes** | 9 | 1N4148 | $0.15 | For 3x3 matrix |
| **Capacitors** | 2 | 10µF, 100nF | $0.15 | Power filtering |

## Dongle Components

| Component | Quantity | Part Number | Est. Cost | Notes |
|-----------|----------|-------------|-----------|-------|
| **Microcontroller** | 1 | RP2040 Plus Module | $6-8 | USB-capable version |
| **Wireless Module** | 1 | nRF24L01+ PA/LNA PCB antenna | $2-4 | Same as devices |
| **Capacitors** | 2 | 10µF, 100nF | $0.15 | Power filtering |
| **Resistors** | 2 | 10kΩ | $0.10 | Pull-ups (if needed) |

## Consumables & Hardware

| Component | Quantity | Est. Cost | Notes |
|-----------|----------|-----------|-------|
| **PCB** | 3 boards | $20-30 | JLCPCB / PCBWay (main, macropad, dongle) |
| **M2 Screws** | 20 | $2 | Case assembly |
| **M2 Standoffs** | 10 | $2 | Spacers |
| **Rubber Feet** | 6-8 | $1-2 | Anti-slip |
| **Wire/Jumper** | 1m | $1 | Wiring (22AWG or similar) |
| **Heat Shrink** | 0.5m | $1 | Battery/connector insulation |
| **Solder** | 1 roll | $3-5 | Lead-free recommended |
| **Flux** | 1 | $2 | For soldering |

## Total Estimate

| Item | Cost |
|------|------|
| Main Keyboard | $70-110 |
| Macropad | $25-45 |
| Dongle | $8-12 |
| Consumables | $30-40 |
| **TOTAL** | **$135-210** |

---

## Supplier Recommendations

- **PCBs**: JLCPCB, PCBWay, Elecrow
- **Components**: LCSC (JLCPCB's supplier), AliExpress, DigiKey, Mouser
- **Switches/Keycaps**: Amazon, KBDFans, AliExpress
- **Magnetic Connectors**: AliExpress, Amazon (search "6-pin magnetic connector")
- **Batteries**: AliExpress (check UN38.3 for shipping)

---

## Key Changes from Original Design

1. **RP2040 Plus Module** instead of bare chip - simplifies assembly
2. **Pre-made magnetic connector** instead of custom pogo pins - more reliable
3. **Monochrome OLED (SSD1327)** instead of full-color - saves power and cost
4. **PCF8574 GPIO Expander** for I2C - solves GPIO shortage on RP2040 with 14x5 matrix
5. **Single USB-C** from RP2040 module - module handles power delivery internally

---

*Prices are estimates and may vary. Check current prices before ordering.*
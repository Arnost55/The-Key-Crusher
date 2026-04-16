# Macro-Hackapad - Bill of Materials

## Main Keyboard Components

| Component | Quantity | Part Number | Est. Cost | Notes |
|-----------|----------|-------------|-----------|-------|
| **Microcontroller** | 1 | Raspberry Pi RP2040 | $4-6 | Waveshare or generic |
| **Wireless Module** | 1 | nRF24L01+ PA/LNA | $2-4 | High power version |
| **OLED Display** | 1 | 1.3" RGB OLED (ST7789) | $8-12 | SPI interface |
| **Battery** | 1 | LiPo 3.7V 1000mAh | $8-12 | JST connector |
| **Charger IC** | 1 | TP4056 + protection | $1-2 | USB-C charging |
| **Boost Regulator** | 1 | MT3608 or similar | $1-2 | 3.3V for OLED/MCU |
| **USB-C Connector** | 1 | USB-C 16-pin | $0.50-1 | SMD |
| **Pogo Pins** | 4 | 2mm spring pin | $1-2 | Gold-plated |
| **Neodymium Magnets** | 4 | 3mm x 2mm disc | $1-2 | N52 grade |
| **Key Switches** | 68 | Kailh/Gateron | $20-40 | Hot-swap recommended |
| **Keycaps** | 1 set | 65% Cherry profile | $25-50 | ABS or PBT |
| **Diodes** | 68 | 1N4148 or SS34 | $1-2 | For matrix |
| **Resistors** | 2 | 22Ω USB | $0.10 | USB D+/D- |
| **Capacitors** | 4 | 10µF, 100nF | $0.20 | Power filtering |
| **LEDs (RGB)** | 68 | WS2812B (optional) | $5-10 | Per-key RGB |

## Macropad Components

| Component | Quantity | Part Number | Est. Cost | Notes |
|-----------|----------|-------------|-----------|-------|
| **Microcontroller** | 1 | Raspberry Pi RP2040 | $4-6 | Same as main |
| **Wireless Module** | 1 | nRF24L01+ PA/LNA | $2-4 | Same as main |
| **OLED Display** | 1 | 1.3" RGB OLED (ST7789) | $8-12 | Same as main |
| **Battery** | 1 | LiPo 3.7V 500mAh | $5-8 | Smaller capacity |
| **Charger IC** | 1 | TP4056 + protection | $1-2 | Same as main |
| **Boost Regulator** | 1 | MT3608 | $1-2 | Same as main |
| **USB-C Connector** | 1 | USB-C 16-pin | $0.50-1 | Same as main |
| **Pogo Sockets** | 4 | 2mm socket | $1-2 | Receptacle |
| **Neodymium Magnets** | 4 | 3mm x 2mm disc | $1-2 | Same as main |
| **Key Switches** | 9 | Kailh/Gateron | $3-5 | Hot-swap |
| **Keycaps** | 1 set | 1u keycaps (9x) | $5-10 | Match main |
| **Diodes** | 9 | 1N4148 | $0.10 | For matrix |
| **RGB LED** | 9 | WS2812B (optional) | $1-2 | Per-key RGB |

## Dongle Components

| Component | Quantity | Part Number | Est. Cost | Notes |
|-----------|----------|-------------|-----------|-------|
| **Microcontroller** | 1 | Raspberry Pi RP2040 | $4-6 | USB capable |
| **Wireless Module** | 1 | nRF24L01+ PA/LNA | $2-4 | Same as devices |
| **USB-C Connector** | 1 | USB-C 16-pin | $0.50-1 | For PC connection |
| **Resistors** | 2 | 22Ω USB | $0.10 | USB D+/D- |
| **Capacitors** | 2 | 10µF, 100nF | $0.10 | Power filtering |

## Consumables & Hardware

| Component | Quantity | Est. Cost | Notes |
|-----------|----------|-----------|-------|
| **PCB** | 3 boards | $20-30 | JLCPCB / PCBWay |
| **M2 Screws** | 20 | $2 | Case assembly |
| **M2 Standoffs** | 10 | $2 | Spacers |
| **Rubber Feet** | 6-8 | $1-2 | Anti-slip |
| **Wire/Jumper** | 1m | $1 | Wiring |
| **Heat Shrink** | 0.5m | $1 | Battery insulation |
| **Solder** | 1 roll | $3-5 | Leaded recommended |
| **Flux** | 1 | $2 | For soldering |

## Total Estimate

| Item | Cost |
|------|------|
| Main Keyboard | $80-120 |
| Macropad | $30-50 |
| Dongle | $8-12 |
| Consumables | $30-40 |
| **TOTAL** | **$150-220** |

---

## Supplier Recommendations

- **PCBs**: JLCPCB, PCBWay, Elecrow
- **Components**: LCSC, Aliexpress, DigiKey, Mouser
- **Switches/Keycaps**: Amazon, KBDFans, AliExpress
- **Magnets**: Amazon, AliExpress
- **Batteries**: AliExpress (ensure UN38.3 for shipping)

---

## Alternative Components

### If using nRF52840 (integrated BT + 2.4GHz)
| Component | Savings |
|-----------|---------|
| Remove nRF24L01+ (saves $4-8) | -$8 |
| nRF52840 DK or module | +$10-15 |
| **Net cost** | +$2-7 |

### If using TFT LCD instead of OLED
| Component | Cost Difference |
|-----------|-----------------|
| ST7789 1.3" LCD | +$2-4 |
| **Net cost** | +$2-4 |

---

*Prices are estimates and may vary. Check current prices before ordering.*
# Design Changes Summary

## Overview
This document tracks all modifications made to the Macro-Hackapad project during the Claude Code development session (Apr 16-19, 2026).

---

## Major Component Changes

### 1. Microcontroller Module
**Original Plan:** Bare RP2040 chip (QFN-56)
**Updated:** RP2040 Plus Module (Waveshare or equivalent)

**Why:** 
- Eliminates need for external USB-C connector, crystal, and 3.3V regulator
- Simplifies PCB design (module mounting vs fine-pitch BGA)
- Reduces soldering complexity
- Module includes 8MB flash, boot button, reset circuits

**Impact:** Removed components
- ❌ USB-C connector (16-pin SMD)
- ❌ AMS1117-3.3V regulator (SOT-223)
- ❌ 12MHz crystal oscillator
- ❌ Crystal load capacitors (2x 22pF)

---

### 2. Display Selection
**Original Plan:** Full-color RGB OLED or TFT LCD (ST7789)
**Updated:** Monochrome OLED (SSD1327, white on black)

**Why:**
- Lower power consumption (critical for battery life)
- Simpler firmware implementation
- Industry standard for custom keyboards
- Sufficient for layer indicators and animations
- ~$3-4 cost savings

**Specifications:**
- 1.3" diagonal, 128x128 resolution
- SPI interface (3 control lines + shared SPI bus)
- White pixels on black background

---

### 3. Macropad Connector
**Original Plan:** 4-pin pogo pins (custom design)
**Updated:** 6-pin waterproof magnetic connector (pre-made)

**Why:**
- Pre-assembled = no custom pogo pin design needed
- Waterproof rating improves durability
- More reliable magnetic alignment with built-in magnets
- Easier alignment than designing custom pogo holes
- Flexible pin count (can extend from 4 to 6 pins)

**Pin Assignment (6-pin):**
1. VBUS (5V) - unused on macropad (has own battery)
2. GND
3. TX (macropad → main)
4. RX (main → macropad)
5. D+ (debug/spare)
6. D- (debug/spare)

**Removed Components:**
- ❌ 4-pin spring pogo pins (2mm pitch)
- ❌ Magnetic alignment magnets (now built into connector)

---

### 4. GPIO Expansion Solution
**Original Plan:** Use all 22 GPIO pins on RP2040 for matrix (19 pins) + peripherals (3 pins) - NOT VIABLE
**Updated:** PCF8574 I2C GPIO expander + optimized pin allocation

**Why:**
- 14×5 matrix = 19 GPIO pins (too many for 22-pin module)
- nRF24L01+ + OLED + magnetic connector needed additional pins
- PCF8574 (I2C) adds 8 virtual GPIO pins using only 2 physical (SCL/SDA)
- Cost effective (~$1-2)

**Allocation:**
```
RP2040 GPIO (22 total):
  ├─ GP0-GP5: Matrix rows 8-13
  ├─ GP6-GP10: Matrix cols 0-4
  ├─ GP11-GP15: nRF24L01+ (MOSI, MISO, SCK, CE, CSN)
  ├─ GP16-GP18: OLED (CS, DC, RST) + shared SPI with nRF24
  ├─ GP19, GP22: Magnetic connector (TX, RX)
  ├─ GP23-GP24: I2C (SCL, SDA) for PCF8574
  └─ GP25: Battery ADC

PCF8574 (8 virtual GPIO via I2C):
  ├─ P0-P7: Matrix rows 0-7
```

**New Components:**
- ✅ PCF8574 8-port I2C GPIO expander (SOT-16 or DIP-16)
- ✅ 2x 10kΩ pull-up resistors for I2C (if required)

---

### 5. Power/Charging Architecture
**Original Plan:** Separate USB-C connector + external charger IC layout
**Updated:** Use RP2040 module's built-in USB-C

**Implementation:**
```
RP2040 Module USB-C
├─ VBUS (5V) ──► [Fuse] ──► TP4056 ──► LiPo Battery
├─ D+/D- ──────► RP2040 (already internal)
└─ 3.3V out ───► nRF24L01+, OLED, other 3.3V components
```

**No additional USB components needed** - module handles all USB power delivery internally

---

## Matrix Configuration

**Original Specification:** 8 rows × 9 columns = 72 positions
**Actual Implementation:** 14 rows × 5 columns = 70 positions

**Updated Pinout:**

### Main Keyboard Matrix
```
Rows: 14 total (GP0-GP5 on RP2040 + P0-P7 on PCF8574)
  ├─ RP2040: GP0-GP5 = Rows 8-13
  └─ PCF8574: P0-P7 = Rows 0-7

Columns: 5 total (GP6-GP10 on RP2040)
  └─ RP2040: GP6-GP10 = Cols 0-4
```

---

## Wireless Module Details

**Specification:** nRF24L01+ PA/LNA with PCB antenna
**Change:** Clarified antenna type = PCB antenna version only

**Why:**
- No external SMA antenna = cleaner design, fits inside case
- 10m range sufficient for desk/gaming use
- PA/LNA ensures ~1ms latency even with small antenna
- Cheaper than external antenna versions

---

## Cost Impact

| Category | Original Est. | Updated Est. | Savings |
|----------|---------------|--------------|---------|
| Main Keyboard | $80-120 | $70-110 | -$10 |
| Macropad | $30-50 | $25-45 | -$5 |
| Dongle | $8-12 | $8-12 | - |
| **TOTAL** | **$150-220** | **$135-210** | **-$15-$25** |

---

## Component Modifications Summary

| Change Type | Original | Updated | Qty | Cost Impact |
|-------------|----------|---------|-----|------------|
| Microcontroller | Bare RP2040 + regulators | RP2040 Plus Module | 3 | -$8 |
| Display | Full-color OLED (ST7789) | Monochrome OLED (SSD1327) | 2 | -$6 |
| Connector | Custom 4-pin pogo | 6-pin waterproof magnetic | 2 | +$10 |
| GPIO Solution | N/A (not viable) | PCF8574 I2C expander | 1 | +$2 |
| Power Regulation | External AMS1117 | Module built-in | - | -$2 |
| USB Connector | Separate USB-C | On module | - | -$1 |
| Crystal | External 12MHz | On module | - | -$0.50 |

**Net Change:** -$5 to -$15 cost savings

---

## Files Updated

1. **SPEC.md** - Updated microcontroller specs, display type, connector details, full pinout tables
2. **BOM.md** - Updated component list, suppliers, cost estimates, added PCF8574 and magnetic connector
3. **BOM.csv** - Updated with new components and quantities
4. **BOM-PCBA.csv** - Updated for JLCPCB assembly reference

---

## KiCad Schematic Status

- ✅ RP2040 Plus Module connections finalized
- ✅ nRF24L01+ (SPI shared with OLED)
- ✅ SSD1327 OLED (SPI)
- ✅ TP4056 charger (powered from module VBUS)
- ✅ PCF8574 I2C GPIO expander (for matrix rows)
- ✅ Magnetic connector (6-pin, TX/RX for macropad)
- ✅ Switch matrix wiring (14×5)
- ⏳ Footprint assignment
- ⏳ PCB layout/routing
- ⏳ Gerber generation

---

## Next Steps

1. **Footprint Assignment** - Map all schematic symbols to physical packages
2. **PCB Layout** - Place components and route traces
3. **Macropad Schematic** - Create 3×3 variant with same architecture
4. **Dongle Schematic** - RP2040 + nRF24L01+ only
5. **DRC & ERC** - Run design rule checks
6. **Gerber Export** - Generate manufacturing files

---

**Last Updated:** 2026-04-19
**Status:** Main keyboard schematic complete, awaiting PCB layout phase

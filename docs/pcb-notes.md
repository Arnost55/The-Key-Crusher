# PCB Design Notes - Macro-Hackapad

## KiCad Setup

### Getting Started
1. Open KiCad 8 (or latest)
2. File → New Project → Create in `pcb/main-keyboard/`
3. Repeat for `pcb/macropad/` and `pcb/dongle/`

### Recommended Settings
- **Grid**: 0.5mm or 0.254mm (0.1")
- **Units**: mm (metric works better for keyboard)
- **Layers**: 2-layer minimum, 4-layer recommended for wireless

---

## Main Keyboard PCB

### Schematic Requirements

**Microcontroller Section (RP2040)**
- RP2040 chip (QFN-56 package)
- Crystal oscillator 12MHz
- USB-C connector with D+/D- resistors (22Ω)
- Boot/reset buttons
- Debug pins (SWD)

**Wireless Section (nRF24L01+)**
- nRF24L01+ module footprint
- 10µF + 100nF capacitors near module
- Antenna keep-out area (no copper/traces)

**OLED Display**
- 1.3" RGB OLED (ST7789) 8-pin header
- SPI pins: MOSI, SCK, CS, DC, RST
- Power filtering capacitors

**Switch Matrix**
- 68 keys = 8 rows × 9 columns
- diodes (1N4148 SOD-123)
- Hot-swap socket footprint (Kailh compatible)

**Power**
- TP4056 charger IC
- USB-C connector
- LiPo battery connector (JST 2-pin)
- 3.3V regulator (AMS1117-3.3)
- Voltage divider for battery ADC

**Pogo Pin Connector**
- 4-pin footprint
- VCC, GND, TX, RX

### Board Dimensions
- ~325mm × 108mm
- Mounting holes for case (M2)

---

## Macropad PCB

### Schematic Requirements

**Microcontroller Section**
- RP2040 (same as main)
- Crystal 12MHz
- USB-C for charging
- Boot/reset buttons

**Wireless Section**
- nRF24L01+ (same as main)
- Same requirements

**OLED Display**
- 1.3" RGB OLED (same as main)
- Same footprint

**Switch Matrix**
- 9 keys = 3 rows × 3 columns
- Diodes
- Hot-swap sockets

**Power**
- TP4056
- USB-C
- 500mAh LiPo connector
- 3.3V regulator

**Pogo Pin Receptacle**
- 4-pin socket to match main board

### Board Dimensions
- ~80mm × 80mm
- Mounting holes

---

## Dongle PCB

### Schematic Requirements

**Microcontroller**
- RP2040
- USB-C connector (for PC)
- Status LED

**Wireless**
- nRF24L01+ PA/LNA

**Power**
- 5V from USB
- 3.3V regulator
- No battery needed

### Board Dimensions
- Small (~30mm × 50mm)
- USB-C plug form factor (optional)

---

## Design Tips

### RF Considerations (nRF24L01+)
- Keep module away from metal
- Ground plane under antenna (but not overlapping)
- Avoid traces near antenna
- Add filtering capacitors

### USB Lines
- D+/D- traces: equal length, ~90Ω impedance
- Keep away from noisy lines
- Add ESD protection (optional)

### Power
- decoupling capacitors near every chip
- Ground pour on both sides
- Star ground for analog (battery ADC)

### Manufacturing
- JLCPCB: 2-layer is cheap, 4-layer for complex
- Minimum trace: 0.2mm
- Minimum clearance: 0.2mm
- V-cut or mouse bites for panelization

---

## Pin Mapping Reference

### Main Keyboard (RP2040)
```
Rows: GP0-GP4
Cols: GP5-GP13
OLED: GP14-GP19
nRF24: GP20-GP25
USB: GP26-GP27
Pogo: GP28, GP29
Battery: ADC (GP26)
```

### Macropad (RP2040)
```
Rows: GP0-GP2
Cols: GP3-GP5
OLED: GP6-GP11
nRF24: GP12-GP17
USB: GP18-GP19
Battery: ADC (GP20)
```

---

## Next Steps

1. Create new KiCad project
2. Draw schematic for main keyboard
3. Assign footprints
4. Route PCB
5. Generate Gerbers
6. Order from JLCPCB/PCBWay

Good luck! 🛹
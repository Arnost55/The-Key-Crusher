# Wireless Architecture - Macro-Hackapad

## Overview

The Macro-Hackapad uses a smart dual-mode wireless system:
- Single dongle connects to both main keyboard and macropad
- Automatic routing based on whether macropad is docked or undocked
- Redundancy: each device works independently if the other fails

## Hardware

### Wireless Module: nRF24L01+

**Why nRF24L01+:**
- Extremely low latency (~1ms)
- Proven in custom keyboard community
- Cheap and widely available
- Low power consumption

**Module variants:**
- Basic (nRF24L01+): ~2m range, indoor use
- PA/LNA version: ~10m range, better for most use cases

## Communication Modes

### Mode 1: Macropad Docked

```
┌─────────────┐     nRF24      ┌─────────────┐    Pogo     ┌─────────────┐
│     PC      │◄──────────────►│ Main Board  │◄───────────►│  Macropad   │
│  (Dongle)   │                │   (nRF24)   │   (4-pin)   │   (docked)  │
└─────────────┘                └─────────────┘             └─────────────┘
   USB-C                           Wireless                     Wired
```

**Data flow:**
1. Dongle sends data to main keyboard via nRF24L01+
2. Main keyboard receives and processes its own keys
3. Main keyboard forwards macropad data through pogo pins (UART)
4. Macropad processes its keys

**Benefits:**
- Lower latency for docked mode
- Macropad doesn't need its own wireless when docked
- Simpler pairing

### Mode 2: Macropad Undocked

```
┌─────────────┐     nRF24      ┌─────────────┐
│     PC      │◄──────────────►│ Main Board  │
│  (Dongle)   │    Direct      │   (nRF24)   │
└─────────────┘                └─────────────┘

┌─────────────┐     nRF24      ┌─────────────┐
│  (Dongle)   │◄──────────────►│  Macropad   │
│             │    Direct      │   (nRF24)   │
└─────────────┘                └─────────────┘
```

**Data flow:**
1. Dongle sends data to both devices simultaneously
2. Main keyboard processes its keys
3. Macropad processes its keys independently
4. No dependency between devices

**Benefits:**
- Either device works without the other
- True wireless freedom
- Redundancy

## Pairing

### Initial Pairing Process

1. **Factory reset** - Clear stored addresses on all devices
2. **Enter pairing mode** - Hold designated key combination:
   - Main keyboard: `Fn + P` for 3 seconds
   - Macropad: `P` for 3 seconds while undocked
   - Dongle: Reset button
3. **Pair main keyboard** - Dongle learns main keyboard address
4. **Pair macropad** - Dongle learns macropad address
5. **Confirm** - Test both devices work

### Address Scheme

Each device has a unique 5-byte address:
- Main keyboard: `0x4D 4B 31 00 01` ("MK1" + unit)
- Macropad: `0x4D 4B 31 00 02` ("MK1" + unit)
- Dongle stores both addresses

## Protocol

### Packet Structure

```
┌──────────┬──────────┬─────────┬────────────┬──────────┐
│ Header   │ DeviceID │ Length  │ Payload    │  CRC     │
│ 1 byte   │ 1 byte   │ 1 byte  │ N bytes    │ 2 bytes  │
└──────────┴──────────┴─────────┴────────────┴──────────┘
```

- **Header**: Packet type (keystroke, ping, ack, etc.)
- **DeviceID**: Which device (main/macropad/dongle)
- **Length**: Payload length
- **Payload**: Actual data
- **CRC**: Error detection

### Latency Optimization

- **Auto-ack enabled**: Confirms packet receipt
- **Retries**: 3x automatic retry on failure
- **Burst mode**: Send multiple keystrokes in one packet
- **Interrupt-driven**: Immediate processing on receipt

## Power Management

### Main Keyboard
- Sleep after 5 min of inactivity
- Wake on any keypress
- OLED dimmed in sleep

### Macropad
- Sleep after 3 min of inactivity
- Wake on any keypress
- LED indicator shows connection status

### Battery Monitoring
- ADC on main keyboard reads battery voltage
- Display shows battery percentage
- Low battery warning at 20%

## Troubleshooting

### No connection
- Check batteries are charged
- Verify pairing (hold pairing keys)
- Move dongle closer (nRF24 range limit)
- Check for interference (WiFi routers, USB 3.0)

### Intermittent connection
- Check antenna orientation
- Reduce distance to dongle
- Ensure batteries have sufficient charge

### High latency
- Normal latency: ~5-15ms
- Check for packet loss (LED indicator)
- Reduce wireless congestion

## Future Improvements

- **ESB (Enhanced ShockBurst)**: nRF24's built-in protocol for auto-ack/retry
- **Channel hopping**: Avoid congested 2.4GHz channels
- **Display RSSI**: Show signal strength on OLED
# Claude Desktop Buddy — M5Stack Core2

A hardware companion for Claude Cowork and Claude Code, ported from
[anthropics/claude-desktop-buddy](https://github.com/anthropics/claude-desktop-buddy)
to the M5Stack Core2 (M5S K010-V11).

## What it does

- **Dashboard** — live session count, running/waiting status, BLE link, token count
- **ASCII buddy** — animated character that reacts to Claude's state (sleep, idle, busy, attention, celebrate, dizzy, heart)
- **Permission prompts** — approve or deny tool requests via touchscreen buttons or hardware buttons
- **Transcript** — scrollable log of recent Claude activity
- **Stats** — pet level, mood, fed, energy, approval/denial counts
- **Shake** — shake the device for a dizzy animation + vibration

## Hardware

- M5Stack Core2 (ESP32-D0WDQ6-V3, 320×240 ILI9341, capacitive touch)
- Connects to Claude Desktop via BLE (Nordic UART Service)

## Flashing

1. Install [PlatformIO Core](https://docs.platformio.org/en/latest/core/installation/)
2. Connect Core2 via USB-C
3. Flash:

```bash
cd claude-buddy-core2
pio run -t upload
```

## Pairing with Claude Desktop

1. Enable Developer Mode: **Help → Troubleshooting → Enable Developer Mode**
2. Open **Developer → Open Hardware Buddy…**
3. Click **Connect** and pick your "Claude-XXXX" device
4. Enter the 6-digit passkey shown on the Core2 screen

## Controls

| Input | Normal | Approval prompt |
|-------|--------|-----------------|
| Touch tabs | Switch views | — |
| Touch APPROVE | — | Approve once |
| Touch DENY | — | Deny |
| BtnA (left) | Next view | Approve |
| BtnB (center) | Scroll log | — |
| BtnC (right) | — | Deny |
| Shake | Dizzy animation | — |

Screen auto-sleeps after 60s idle; any touch wakes it.

## Project layout

```
src/
  main.cpp        — UI, state machine, touch handling
  ble_bridge.cpp  — Nordic UART Service BLE bridge
  ble_bridge.h
  data.h          — JSON protocol parser, time sync
  stats.h         — NVS-backed stats, settings, pet mechanics
platformio.ini    — build config for M5Stack Core2
```

## Credits

Based on the official [claude-desktop-buddy](https://github.com/anthropics/claude-desktop-buddy)
by Anthropic (Felix Rieseberg).

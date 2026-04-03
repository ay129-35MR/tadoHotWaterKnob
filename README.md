# tadoHotWaterKnob (v2.0)
## ESP32-S3 + ST7789 Smart Hot Water & Boiler Controller

[![ESPHome](https://img.shields.io/badge/ESPHome-2025-blue?logo=esphome)](https://esphome.io/)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-Integration-41BDF5?logo=home-assistant)](https://www.home-assistant.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Buy Me A Coffee](https://img.shields.io/badge/Buy%20Me%20A%20Coffee-ffdd00?logo=buy-me-a-coffee&logoColor=black)](https://buymeacoffee.com/ay129)
[![Donate](https://img.shields.io/badge/Donate-PayPal-blue.svg)](https://www.paypal.com/donate?business=nyashachipanga%40yahoo.com&currency_code=GBP)

A high-performance **Smart Hot Water & Boiler Controller** built on the **ESP32-S3**, featuring a rich 5-page UI, real-time analytics, and deep integration with **Home Assistant** and **Tado**.

This project has evolved from a simple temperature dial into a comprehensive household dashboard, managing hot water, room heating, occupancy tracking, and even security camera snapshots.

<p align="center">
  <img src="screenshots/hotwaterknob/page0.png" width="300" alt="Main Control">
  <img src="screenshots/hotwaterknob/page1.png" width="300" alt="Temperature History">
  <img src="screenshots/hotwaterknob/page2.png" width="300" alt="Guest & Heating Status">
</p>
<p align="center">
  <img src="screenshots/hotwaterknob/page3.png" width="300" alt="Camera Snapshots">
  <img src="screenshots/hotwaterknob/page4.png" width="300" alt="Display Settings">
</p>

---

## ðŸš€ Key Features

- ðŸŒ¡ï¸ **Advanced Water Control**: Large real-time temperature display, usage rate calculation (Â°C/min), and a visual target bar.
- ðŸ“‰ **Analytics**: Built-in 4-hour temperature history graph with adjustable time range presets.
- ðŸ¨ **Guest & Room Dashboard**: Dual-column layout tracking temperatures and occupancy for multiple rooms (Double & En-Suite) using Home Assistant presence sensors.
- ðŸ§¹ **Cleaning Schedule**: Real-time fetch of upcoming cleaning appointments from an external API.
- ðŸ“· **Security Integration**: Full-screen camera snapshots (Front & Garden) served via an external image proxy.
- ðŸŽ›ï¸ **Manual Overrides**: Physical toggles for boiler state (OFF/HEAT) and an **Automation Killswitch** (AUTO) to suspend Home Assistant logic.
- ðŸŒ™ **Sleep & Brightness**: Auto-dimming, sleep/wake logic, and fine-grained brightness control (10-100%).

---

## ðŸ› ï¸ Hardware Profile

- **Controller**: ESP32-S3 (N16R8) - **PSRAM is mandatory** for the image handling and UI complexity.
- **Display**: 2.8" 320x240 TFT (ST7789V or ILI9341).
- **Controls**: EC11 Rotary Encoder + dedicated Navigation button.
- **Assembly**: Custom perfboard motherboard (dual-sided mount for S3 and Display).

### Pinout (ESP32-S3 DevKitC-1)

| Function | GPIO | Notes |
|---|---:|---|
| **Rotary Encoder A** | `GPIO2` | `INPUT_PULLUP` |
| **Rotary Encoder B** | `GPIO3` | `INPUT_PULLUP` |
| **Knob Push Button** | `GPIO1` | `INPUT_PULLUP`, inverted |
| **Navigation Button** | `GPIO4` | `INPUT_PULLUP`, inverted |
| **TFT SPI MOSI** | `GPIO11` | Shared SPI bus |
| **TFT SPI SCLK** | `GPIO12` | Shared SPI bus |
| **TFT CS** | `GPIO10` | Chip Select |
| **TFT DC** | `GPIO9` | Data/Command |
| **TFT RST** | `GPIO8` | Hardware Reset |
| **TFT Backlight** | `GPIO13` | `ledc` PWM control |

---

## ðŸ–¥ï¸ UI Structure (5 Pages)

### 1. Main Control
- Large temperature readout with color-coded "Usage Rate" indicator.
- Interactive target temperature slider (35Â°C - 65Â°C).
- Three large toggle buttons: **OFF**, **HEAT** (Manual Force), and **AUTO** (Automation Enable).

### 2. History Graph
- Visualizes the last 4 hours of water temperature.
- Supports adjustable time windows (10min to 4hr) via the rotary knob.
- Circular buffer logic maintains data locally on the ESP.

### 3. Guest & Room Info
- **Double Room / En-Suite**: Shows Room/Bath temperatures, Tado HVAC state, and presence (orange occupancy dots).
- **Guest Tracking**: Displays guest names and check-in/out dates synced from HA.
- **Cleaning Schedule**: Sub-view fetching JSON schedule data from a local server API.

### 4. Camera View
- Fetches 320x240 PNG snapshots from an external image server.
- Swap between **Front** and **Garden** cameras using the rotary knob.
- Manual refresh on knob press.

### 5. Display Settings
- Brightness adjustment with quick presets (25/50/75/100%).
- Real-time visual feedback on the brightness level.

---

## ðŸ—ï¸ Software Architecture

This project relies on a distributed architecture to keep the ESP32-S3 responsive:

1. **Home Assistant**: Acts as the data hub for temperature sensors, Tado climate entities, and automation states.
2. **Image Proxy**: A separate Linux server (Docker) that resizes and converts camera streams into embedded-friendly 320x240 PNGs.
3. **Cleaning API**: A Python/Flask API that serves household schedules in a pipe-delimited format for low-overhead parsing on the ESP.
4. **ESPHome Custom Components**:
   - `display_screenshot`: Allows for remote 24-bit BMP captures via HTTP for debugging/documentation without physical access.

---

## ðŸ”§ Installation

1. **Hardware**: Wire the ESP32-S3 to the display and encoder per the pinout table.
2. **ESPHome**: Copy the `hotwaterknob.yaml` to your config directory.
3. **Secrets**: Update `secrets.yaml` with your WiFi, HA API keys, and server URLs.
4. **Dependencies**: Ensure you have the `fonts/` and `components/` folders in your ESPHome directory.
5. **Flash**: Compile and upload. The ESP will automatically sync its initial state from Home Assistant.

---

## â˜• Support

If you find this project useful, consider supporting development:

[![Buy Me A Coffee](https://img.shields.io/badge/Buy%20Me%20A%20Coffee-ffdd00?logo=buy-me-a-coffee&logoColor=black)](https://buymeacoffee.com/ay129)
[![Donate](https://img.shields.io/badge/Donate-PayPal-blue.svg)](https://www.paypal.com/donate?business=nyashachipanga%40yahoo.com&currency_code=GBP)

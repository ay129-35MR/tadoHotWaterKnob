# tadoHotWaterKnob
# 🔥 ESPHome Hot Water & Boiler Controller  

[![ESPHome](https://img.shields.io/badge/ESPHome-2025-blue?logo=esphome)](https://esphome.io/)  
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-Integration-41BDF5?logo=home-assistant)](https://www.home-assistant.io/)  
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)  

A **smart hot water and boiler controller** built on **ESP32 + ESPHome**, fully integrated with **Home Assistant**.  
This project provides a **rotary knob + TFT display** for intuitive local control while maintaining complete automation support.  

---

## ✨ Features  

- 🔄 **Local Control**: Adjust target hot water temperature with a rotary knob  
- 📊 **Feedback Display**: Shows current water temperature, target, boiler status, and history  
- 📱 **Home Assistant Integration**: All updates sync seamlessly with HA entities and automations  
- 🌙 **Low Power**: Sleep/wake handling for efficient use  
- 🖥 **Multi-Page Interface**:  
  - **Page 1** → Hot water temperature + boiler status  
  - **Page 2** → Manual override (OFF / HEAT)  
  - **Page 3** → Home occupancy (double + ensuite rooms + bathrooms)  
  - **Page 4** → Display settings (brightness)  

---

## 📸 Screenshots  

*(replace with real photos/screens later)*  

- Main temperature page  
  <img width="1080" height="922" alt="image" src="https://github.com/user-attachments/assets/2b285218-b3c6-4d6f-9b8c-42ce44d5ac81" />

- Manual control page  
  <img width="1080" height="1440" alt="image" src="https://github.com/user-attachments/assets/07d24611-2117-46fc-9c51-d1f9ac503196" />

- Occupancy status  
  <img width="1080" height="1440" alt="image" src="https://github.com/user-attachments/assets/6c716aa2-7876-4bd5-b7cf-bf8e679adf96" />

- Display settings  
 <img width="1080" height="1440" alt="image" src="https://github.com/user-attachments/assets/2b5b6bef-d6ab-44cf-bf47-91b621b37f88" />

---

## 🛠 Hardware  

- ESP32-S3 N16R8 - lesser ESP32's dont have the (PS)RAM to cope with drawing the screen
- EC11 Rotary encoder with push button and 320×240 TFT display (ILI9341 or similar)
         These can be bought as a package in AliExpress:
        <img width="1080" height="1440" alt="image" src="https://github.com/user-attachments/assets/273a4873-22d3-46a4-bc8a-1102559305dd" />

- Perfboard, solder, wire
- Temperature sensors (via Home Assistant integration)
- I have a ds18b20 temperature probe in the temp port of the hot water tank, connected to an ESP32 that sends the temps to a Home assistant sensor.

I was personally going for quick and dirty and mounted the project on a perfboard, soldering female header pins 
  for
  :  the ESP32-S3 on one side, 
  :  and the rotary encoder / TFT screen combo on the other
then wiring the pins as summarised below

## 🔌 Pinout (ESP32-S3 DevKitC-1)

| Component / Signal              | ESP32-S3 GPIO | Notes |
|---------------------------------|---------------|-------|
| **Rotary Encoder – A**          | `GPIO2`       | Encoder signal A (INPUT_PULLUP) |
| **Rotary Encoder – B**          | `GPIO3`       | Encoder signal B (INPUT_PULLUP) |
| **Rotary Encoder – SW (press)** | `GPIO1`       | Knob push button (INPUT_PULLUP) |
| **Navigation Button**           | `GPIO4`       | Page advance (INPUT_PULLUP) |
| **TFT ST7789 – MOSI (DIN/SDA)** | `GPIO11`      | SPI data out to display |
| **TFT ST7789 – SCLK (CLK/SCK)** | `GPIO12`      | SPI clock |
| **TFT ST7789 – CS**             | `GPIO10`      | Chip Select |
| **TFT ST7789 – DC**             | `GPIO9`       | Data/Command |
| **TFT ST7789 – RST**            | `GPIO8`       | Hardware reset |
| **TFT Backlight (BLK)**         | `GPIO13`      | LEDC PWM for brightness |
| **Status LED (onboard)**        | `GPIO48`      | Inverted logic |
| **Power**                       | `3V3 / GND`   | Common supply/ground |

**Notes**
- ST7789 here is **write-only SPI** (no MISO line).
- Backlight on `GPIO13` uses ESPHome `ledc` → `monochromatic` light for dimming.
- All buttons use internal pull-ups; wire switches to **ground**.
- Pin labels on some ST7789 boards: `DIN` = MOSI, `SCL` = SCLK, `DC` = A0, `CS` = CS, `RST` = RES, `BLK/LED` = backlight.

YMMV on how you choose to wire and route everything. 
---

## 📦 Installation  

1. Sort out the hardware
2. Copy the YAML config to your ESPHome project  
3. Adjust entity IDs to match your Home Assistant setup  
4. Flash to your ESP32 and adopt the device in homeassistant
5. Profit ???
   

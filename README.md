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

- ESP32-S3 - lesser ESP32's dont have the (PS)RAM to cope with drawing the screen
- EC11 Rotary encoder with push button  
- 320×240 TFT display (ILI9341 or similar)
The above can be bought as a package in AliExpress:
<img width="1080" height="1440" alt="image" src="https://github.com/user-attachments/assets/273a4873-22d3-46a4-bc8a-1102559305dd" />

- Temperature sensors (via Home Assistant integration)
-   I have a ds18b20 temperature probe in the temp port of the hot water tank, connected to an ESP32 that sends the temps to a Home assistant sensor.

I was personally going for quick and dirty and mounted the project on a perfboard, soldering female header pins 
  for
  :  the ESP32-S3 on one side, 
  :  and the rotary encoder / TFT screen combo on the other
then wiring the pins as summarised below

## 🔌 Pinout Summary  

| TFT / Encoder Pin        | Pin on ESP32 | Notes |
|--------------------------|--------------|-------|
| **Rotary Encoder – A**   | `GPIO32`     | Encoder signal A |
| **Rotary Encoder – B**   | `GPIO33`     | Encoder signal B |
| **Rotary Encoder – SW**  | `GPIO25`     | Push button (knob press) |
| **TFT Display – CS**     | `GPIO5`      | Chip select |
| **TFT Display – DC**     | `GPIO16`     | Data/Command |
| **TFT Display – RST**    | `GPIO17`     | Reset |
| **TFT Display – SCLK**   | `GPIO18`     | SPI Clock |
| **TFT Display – MOSI**   | `GPIO23`     | SPI Data Out |
| **TFT Display – BLK**    | `GPIO4`      | Backlight - brightness control |
| **GND**                  | `GND`        | Common ground |
| **VCC**                  | `3.3V`       | Power |

<img width="1080" height="1440" alt="image" src="https://github.com/user-attachments/assets/0510f5b1-732d-4f53-9c84-9721e91d647f" />
<img width="1080" height="1440" alt="image" src="https://github.com/user-attachments/assets/fa752fbc-eb3f-45eb-8217-135fe7152822" />
<img width="1080" height="1440" alt="image" src="https://github.com/user-attachments/assets/5bf27366-2739-4ae8-86aa-fee16963eea6" />
---

⚠️ **Notes**  
- The encoder button uses an internal pull-up (`internal_pullup: true` in ESPHome).  
- The TFT runs over **hardware SPI**, so keep `GPIO18` (CLK) and `GPIO23` (MOSI) fixed for performance.  
- If you want **brightness control**, connect the TFT **LED pin** to a PWM-capable GPIO (e.g. `GPIO4`) instead of 3.3V.  

---

## 📦 Installation  

1. Sort out the hardware
2. Copy the YAML config to your ESPHome project  
3. Adjust entity IDs to match your Home Assistant setup  
4. Flash to your ESP32
5. Profit ???
   

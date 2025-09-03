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
  ![Main Page Screenshot](docs/images/main_page.png)  

- Manual control page  
  ![Manual Control Screenshot](docs/images/manual_page.png)  

- Occupancy status  
  ![Occupancy Screenshot](docs/images/occupancy_page.png)  

- Display settings  
  ![Display Screenshot](docs/images/display_page.png)  

---

## 🛠 Hardware  

- ESP32 (tested with [your board name])  
- Rotary encoder with push button  
- 320×240 TFT display (ILI9341 or similar)  
- Temperature sensors (via Home Assistant integration)  

---

## 📦 Installation  

1. Clone this repo  
2. Copy the YAML config to your ESPHome project  
3. Adjust entity IDs to match your Home Assistant setup  
4. Flash to your ESP32 with:  
   ```bash
   esphome run hotwater-knob.yaml

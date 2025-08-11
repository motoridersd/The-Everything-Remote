Tracking changes and mods made by others.

TurtlePrint's Version

https://github.com/TurtlePrint/The-Everything-Remote

Modifications made to the Everything Remote to make it the Ultimate Everything Remote
- Added magnetic pogo pins for charging. Increased length of the remote to 155mm to accomidate the USB-C breakout board and pogo pins.
- Removed one of the hardware pull up resistors and added a voltage divider circuit in its place, still retaining button use but now also accuarate battery metrics
- Removed GPIO15 Button and replaced with a WS2812 LED pixel for notifications (And a built in flash light mode)
- Added "Continuous Press" mode on specific buttons to enable holding volume up or down

Lost all the changes

Wireless coil charging
magnetic dock from makerworld with comments
Deep Sleep dependent on Home Assistant
ESP-Now from instructables for possible less battery hungry option
Longer remote with space for the battery connector
Comment from Printables on how to do the voltage divider for battery status
BLE presence detection, add a beacon to the remote https://esphome.io/components/esp32_ble_beacon.html

# Original project below

# The Everything Remote

A simple universal remote designed for ESPHome - simple to assemble for beginners and experienced tinkerers alike! 

[![Video](https://img.youtube.com/vi/Pe_ozZkrRAw/maxresdefault.jpg)](https://www.youtube.com/watch?v=Pe_ozZkrRAw)

> [!CAUTION]
> Please ensure your chosen lithium cell is no thicker than 6mm. Thick cells could be punctured by the tactile button legs.


## 📦 Features

- 24 configurable buttons (single press + long press)
- Works over Wi-Fi using ESPHome
- Sends `button_pressed` events to Home Assistant
- Deep sleep support for ultra-low power usage
- Easy to build
- 3D printable, customisable enclosure

---

## YAML

[Looking for the YAML for your remote? Here you go!](https://github.com/TheStockPot/The-Everything-Remote/blob/main/ESPHome%20YAML%20-%20v2.1)



## Hardware

[Printable Files](https://www.printables.com/model/1281626-everything-remote-esp32-powered-universal-remote)

[Bill of Materials](https://github.com/TheStockPot/TheEverythingRemote/blob/main/Bill%20Of%20Materials.md)

---

## Tutorial Video

[![Video](https://img.youtube.com/vi/JU_7mb1ue7o/maxresdefault.jpg)](https://www.youtube.com/watch?v=JU_7mb1ue7o)


---

## Button -> GPIO Layout

![Button_GPIO](https://github.com/user-attachments/assets/2e815270-fa7c-42a7-87e6-7fd56a0b1cad)

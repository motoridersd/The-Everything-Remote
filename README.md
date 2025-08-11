Tracking changes and mods made by others.

TurtlePrint's Version

<img width="320" height="240" alt="image" src="https://github.com/user-attachments/assets/996fd145-1fba-4577-886c-c497247fff28" />

https://github.com/TurtlePrint/The-Everything-Remote

Modifications made to the Everything Remote to make it the Ultimate Everything Remote
- Added magnetic pogo pins for charging. Increased length of the remote to 155mm to accomidate the USB-C breakout board and pogo pins.
- Removed one of the hardware pull up resistors and added a voltage divider circuit in its place, still retaining button use but now also accuarate battery metrics
- Removed GPIO15 Button and replaced with a WS2812 LED pixel for notifications (And a built in flash light mode)
- Added "Continuous Press" mode on specific buttons to enable holding volume up or down

## Media Focused Buttons 

<img width="320" height="240" alt="image" src='https://media.printables.com/media/comment_images/ad/0eb20f-a286-4aa6-84be-108b669fa0d8/thumbs/inside/640x480/jpg/pxl_20250717_190036220.webp'>

https://www.tinkercad.com/things/kcJkKT8JOTe-ermediamorebuttons?sharecode=GAdNdrShaN9_7YAmDXliyuxl_ulSDWn8X3fm69BYbjo

## Longer remote with space for the battery connector

<img width="320" height="240" src='https://media.printables.com/media/comment_images/07/0ba722-306f-4198-ae8b-73cc19431648/thumbs/inside/640x480/png/screenshot-2025-07-07-at-55355-pm.webp'>

https://www.printables.com/model/1372638-everything-remote-alternative-base

## Magnetic Charging plug with dock

<img width="320" height="240" src='https://makerworld.bblmw.com/makerworld/model/US41823516ca8590/design/2025-07-06_23b3806ebebd68.jpeg?x-oss-process=image/resize,w_1000/format,webp'>

https://makerworld.com/en/models/1582775-everything-remote-wireless-charging-dock#profileId-1666066

Connector to use [Ali Express Link - Changes often](https://www.aliexpress.us/item/3256807365091703.html?spm=a2g0o.order_list.order_list_main.32.75aa1802etwJLh&)

"240W Magnetic Right Angle USB C Male to USB C Female Adapter 90 Degree PD3.0 Fast Charging Type C Adapter Extender for Iphone"

<img width="240" height="320" alt="image" src="https://github.com/user-attachments/assets/e6fd1650-4a1e-4f33-a2dd-96bd3ae72714" />

## Wireless coil charging

<img width="253" height="360" alt="image" src="https://github.com/user-attachments/assets/fe613c99-513e-469c-af2c-29550e5cfcc1" />

No information of components used: https://www.printables.com/make/2651375

## Battery level reporting with Voltage Divider Circuit

https://www.printables.com/make/2654254/2660187

## ESP-NOW Example with a different remote

Would be nice to make this work with the Everything Remote for very good battery life

https://www.instructables.com/ESP-NOW-Remote-Control/

## Conditional Deep Sleep

Prevent it from sleeping based on Home Assistant flags, like when TV is on.
Maybe have it sleep overnight and wake up at times we expect to use it, but can always be woken up with the power button.
Use API to send commands from home assistant, maybe set a flag.

## BLE Presence Detection

Add BLE code to ESPHome Yaml:

```
esp32_ble_beacon:
  type: iBeacon
  uuid: 'generate a random UUID'
  tx_power: -6
  min_interval: 
    milliseconds: 200
  max_interval: 
    milliseconds: 500
```

Increased the min and max interval values because the defaults (100ms according to documentation) were causing WiFi issues. Also reduced the power which is 3 dB by default. The power might have been causing the WiFi issues.

Then added the beacon to Bermuda and now I have a location for the Everything Remote in Home Assistant that can be used in the automations.
    
https://esphome.io/components/esp32_ble_beacon.html

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

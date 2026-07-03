<div align="center">

# GyverLamp SSDP

**GyverLamp firmware fork with SSDP for iOS GyLamp app**


</div>

A modification of the original GyverLamp v1.5.5 firmware (AlexGyver) that adds SSDP support for automatic lamp discovery on the local network. Designed for use with the iOS [GyLamp](https://apps.apple.com/ru/app/gylamp/id1474547003) application. Drives a 16x16 WS2812B matrix with 18 effects, and lets the lamp name, model name and effect names be customized in the firmware.

## ■ Features

- ❖ **SSDP discovery** — `ESP8266SSDPMod` advertises the lamp over UPnP for automatic detection by the GyLamp app
- ❖ **Custom naming** — SSDP display name (`GyverLamp v1.5`), model name and all 18 effect names are set in the sketch
- ❖ **16x16 LED matrix** — WS2812B on pin D2, GRB order, FastLED with a 2000 mA current limit
- ❖ **Wi-Fi via WiFiManager** — captive-portal setup on first boot; optional access-point mode by switching `ESP_MODE`
- ❖ **Auto-flash scripts** — Windows batch files for NodeMCU v2 and LOLIN(WEMOS) D1 R2 mini that drive arduino-cli (esp8266 core 2.7.1)
- ❖ **Button & NTP** — single button on pin D7 (Wi-Fi reset on hold) and NTP time sync for dawn/alarm

## ■ Stack

<div align="center">

| Component | Technology |
|-----------|------------|
| MCU | ESP8266 (NodeMCU v2 / LOLIN D1 R2 mini) |
| LEDs | WS2812B 16x16 matrix (FastLED 3.2.9) |
| Framework | Arduino (esp8266 core 2.7.1) |
| Discovery | SSDP / UPnP (ESP8266SSDPMod) |
| Wi-Fi | WiFiManager 0.15.0 |
| Build | Arduino IDE / arduino-cli |
| App | GyLamp (iOS) |

</div>

## ■ How It Works

```
1. On first boot WiFiManager opens a captive-portal AP so Wi-Fi credentials can be entered from any device.
2. After connecting to the network, ESP8266SSDPMod starts advertising the lamp over UPnP so the GyLamp iOS app discovers it automatically.
3. The firmware drives the 16x16 WS2812B matrix with 18 effects; effect names, lamp name and model name are set directly in the sketch.
4. A button on pin D7 allows Wi-Fi reset on long hold; NTP syncs time for dawn/alarm effects.
```

## ■ Usage

```bash
# Arduino IDE
# 1. Install the ESP8266 board via Board Manager
#    (http://arduino.esp8266.com/stable/package_esp8266com_index.json)
# 2. Copy the contents of libraries/ into Arduino/libraries/
# 3. Open firmware/GyverLamp_v1.5.5/GyverLamp_v1.5.5.ino
# 4. Select the board (NodeMCU 1.0 or LOLIN(WEMOS) D1 R2 & mini),
#    set Flash size 4MB (FS 1MB), then Upload

# Auto-flash (Windows, requires arduino-cli.exe in the repo root)
NodeMCU_v2_flash_win.bat
# or
LOLIN(WEMOS)_D1_R2_mini_flash_win.bat
# both call the shared flash_win.bat helper
```

## ■ License

MIT © [pluttan](https://github.com/pluttan)

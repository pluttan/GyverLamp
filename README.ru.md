<div align="center">

# GyverLamp SSDP

**Форк прошивки GyverLamp с SSDP для iOS-приложения GyLamp**


</div>

Модификация оригинальной прошивки GyverLamp v1.5.5 (AlexGyver), добавляющая поддержку SSDP для автоматического обнаружения лампы в локальной сети. Предназначена для использования с iOS-приложением [GyLamp](https://apps.apple.com/ru/app/gylamp/id1474547003). Управляет матрицей WS2812B 16x16 с 18 эффектами; имя лампы, название модели и названия эффектов настраиваются в скетче.

## ■ Возможности

- ❖ **Обнаружение через SSDP** — `ESP8266SSDPMod` анонсирует лампу по UPnP для автоматического определения приложением GyLamp
- ❖ **Настройка имён** — отображаемое имя SSDP (`GyverLamp v1.5`), название модели и все 18 названий эффектов задаются в скетче
- ❖ **Матрица LED 16x16** — WS2812B на пине D2, порядок GRB, FastLED с ограничением тока 2000 мА
- ❖ **Wi-Fi через WiFiManager** — настройка через captive-portal при первом запуске; опциональный режим точки доступа переключением `ESP_MODE`
- ❖ **Скрипты автопрошивки** — bat-файлы для Windows для NodeMCU v2 и LOLIN(WEMOS) D1 R2 mini, использующие arduino-cli (esp8266 core 2.7.1)
- ❖ **Кнопка и NTP** — одна кнопка на пине D7 (удержание сбрасывает Wi-Fi) и синхронизация времени по NTP для рассвета/будильника

## ■ Стек

<div align="center">

| Компонент | Технология |
|-----------|------------|
| MCU | ESP8266 (NodeMCU v2 / LOLIN D1 R2 mini) |
| Светодиоды | WS2812B 16x16 matrix (FastLED 3.2.9) |
| Фреймворк | Arduino (esp8266 core 2.7.1) |
| Обнаружение | SSDP / UPnP (ESP8266SSDPMod) |
| Wi-Fi | WiFiManager 0.15.0 |
| Сборка | Arduino IDE / arduino-cli |
| Приложение | GyLamp (iOS) |

</div>

## ■ Как это работает

```
1. При первом запуске WiFiManager открывает captive-portal AP, чтобы можно было ввести данные Wi-Fi с любого устройства.
2. После подключения к сети ESP8266SSDPMod начинает анонсировать лампу по UPnP, и iOS-приложение GyLamp обнаруживает её автоматически.
3. Прошивка управляет матрицей WS2812B 16x16 с 18 эффектами; названия эффектов, имя лампы и название модели задаются непосредственно в скетче.
4. Кнопка на пине D7 позволяет сбросить Wi-Fi долгим нажатием; NTP синхронизирует время для эффектов рассвета/будильника.
```

## ■ Использование

```bash
# Arduino IDE
# 1. Установите плату ESP8266 через Board Manager
#    (http://arduino.esp8266.com/stable/package_esp8266com_index.json)
# 2. Скопируйте содержимое libraries/ в Arduino/libraries/
# 3. Откройте firmware/GyverLamp_v1.5.5/GyverLamp_v1.5.5.ino
# 4. Выберите плату (NodeMCU 1.0 или LOLIN(WEMOS) D1 R2 & mini),
#    укажите Flash size 4MB (FS 1MB), затем нажмите Upload

# Автопрошивка (Windows, требуется arduino-cli.exe в корне репозитория)
NodeMCU_v2_flash_win.bat
# или
LOLIN(WEMOS)_D1_R2_mini_flash_win.bat
# оба вызывают вспомогательный скрипт flash_win.bat
```

## ■ Лицензия

MIT © [pluttan](https://github.com/pluttan)

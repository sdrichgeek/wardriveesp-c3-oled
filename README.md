# WardriveESP — ESP32-C3 0.42-inch OLED

A board-targeted WardriveESP project for the ESP32-C3 0.42-inch OLED development board (`esp32c3_oled042`, 4 MB flash). The onboard 72×40 SSD1306-compatible OLED uses SDA GPIO5 / SCL GPIO6; the blue LED is GPIO8 (active-low), and BOOT is GPIO9.

## Firmware releases

- **v1.7.11** — the baseline image successfully flashed to three boards. Includes board display support and WardriveESP Wi-Fi/Bluetooth scanning and Wardrive Go bridge. It does not include AXEOFF/Axon detection.
- **v1.7.12** — initial passive AXEOFF Axon signature detection over BLE and Wi-Fi capture. On a match the OLED briefly shows `AX` and the blue LED flashes; short-press BOOT cycles the dashboard, latest AXON log, and radio statistics.
- **v1.7.13** — fixes Axon matching when AXEOFF service IDs are carried inside 128-bit BLE service UUIDs.

The complete flash packages and version-specific install commands are in [`releases`](releases/).

## Build from source

Requires ESP-IDF 5.5 and Python dependencies managed by ESP-IDF. From this repository root:

```sh
idf.py set-target esp32c3
idf.py build
```

For prebuilt firmware, use a release ZIP and follow its included install guide. Replace the example COM port with the one assigned to your board.

## Source and license

Based on [RocketGod's WardriveESP](https://github.com/RocketGod-git/WardriveESP). This project preserves the upstream MIT license and notices. The CYD/board-specific release packages and install information identify the exact locally built images and target board.



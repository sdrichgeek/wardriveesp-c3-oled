# WardriveESP for ESP32-C3 0.42-inch OLED

These are locally built firmware packages for the ESP32-C3 development board with the onboard 72x40 SSD1306-compatible OLED (SDA GPIO5, SCL GPIO6), blue LED (GPIO8, active-low), and BOOT button (GPIO9).

## Releases

### v1.7.11 — flashed baseline

This is the exact firmware image successfully flashed to the three boards. It supports the C3 0.42-inch OLED and the WardriveESP scanner/bridge functions: Wi-Fi and Bluetooth scanning and streaming detections to the Wardrive Go app over Bluetooth. It does **not** include the AXEOFF/Axon detection added in v1.7.12.

Install from `WardriveESP-ESP32-C3-OLED-v1.7.11-flashed.zip`. In a terminal opened in the extracted folder, replace `COM4` with the board's serial port and run:

```powershell
python -m esptool --chip esp32c3 -p COM4 -b 460800 write_flash --flash_mode dio --flash_freq 80m --flash_size 4MB 0x0 bootloader/bootloader.bin 0x8000 partition_table/partition-table.bin 0xe000 ota_data_initial.bin 0x20000 wardrive_bridge.bin
```

### v1.7.12 — AXEOFF alerts

Includes the v1.7.11 board support plus passive AXEOFF Axon signature detection from BLE advertisements and Wi-Fi beacons/probe requests. On a match, the OLED briefly displays `AX` and the blue LED flashes. Short-press BOOT to cycle the OLED through the dashboard, latest AXON log entry, and radio statistics. Detection events are also emitted as `WD:AXON` records.

Install from `WardriveESP-ESP32-C3-OLED-v1.7.12.zip`. In a terminal opened in the extracted folder, replace `COM4` with the board's serial port and run:

```powershell
python -m esptool --chip esp32c3 -p COM4 -b 460800 write_flash --flash_mode dio --flash_freq 80m --flash_size 4MB 0x0 bootloader/bootloader.bin 0x8000 partition_table/partition-table.bin 0xe000 ota_data_initial.bin 0x20000 WardriveESP-esp32c3-app.bin
```

For either version: install Python 3 and esptool (`python -m pip install esptool`), connect the board by USB, identify its COM port in Device Manager, extract the selected ZIP, run the matching command from the extracted directory, and wait for the board to restart. The included checksum file can be used to verify package files before flashing. The board must have 4 MB flash. Flashing replaces the current firmware.

## Source and attribution

Firmware is based on RocketGod's WardriveESP. The upstream project documents its supported boards, scanner behavior, and license at [RocketGod-git/WardriveESP](https://github.com/RocketGod-git/WardriveESP). The ESP32-C3 0.42-inch OLED support and v1.7.12 AXEOFF alert changes are local build modifications for this board. Preserve the upstream license and notices when redistributing.

## Packages

- `WardriveESP-ESP32-C3-OLED-v1.7.11-flashed.zip`
- `WardriveESP-ESP32-C3-OLED-v1.7.12.zip`

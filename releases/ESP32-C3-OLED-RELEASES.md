# WardriveESP for ESP32-C3 0.42-inch OLED

These locally built firmware packages target the ESP32-C3 development board with the onboard 72x40 SSD1306-compatible OLED (SDA GPIO5, SCL GPIO6), blue LED (GPIO8, active-low), and BOOT button (GPIO9).

## Releases

### v1.7.11 — flashed baseline

This is the exact firmware image successfully flashed to the three boards. It supports the C3 0.42-inch OLED and WardriveESP Wi-Fi/Bluetooth scanning and the Wardrive Go bridge. It does not include AXEOFF/Axon detection.

Install from `WardriveESP-ESP32-C3-OLED-v1.7.11-flashed.zip`; replace `COM4` with the board's assigned serial port:

```powershell
python -m esptool --chip esp32c3 -p COM4 -b 460800 write_flash --flash_mode dio --flash_freq 80m --flash_size 4MB 0x0 bootloader/bootloader.bin 0x8000 partition_table/partition-table.bin 0xe000 ota_data_initial.bin 0x20000 wardrive_bridge.bin
```

### v1.7.12 — initial AXEOFF alerts

Adds passive AXEOFF Axon signature detection from BLE advertisements and Wi-Fi beacons/probe requests. An alert briefly displays `AX` and flashes the blue LED. Short-press BOOT cycles the OLED through the dashboard, latest AXON log, and radio statistics.

### v1.7.13 — BLE UUID matching fix

Fixes Axon matching when AXEOFF service IDs are carried inside 128-bit BLE service UUIDs. Keeps the prior 16-bit UUID, company ID, and Wi-Fi signature checks. The alert displays `AX` and flashes the blue LED; BOOT cycles through the dashboard, latest AXON log, and radio statistics.

Install from `WardriveESP-ESP32-C3-OLED-v1.7.13.zip`. In a terminal opened in the extracted folder, replace `COM4` with the board's port:

```powershell
python -m esptool --chip esp32c3 -p COM4 -b 460800 write_flash --flash_mode dio --flash_freq 80m --flash_size 4MB 0x0 bootloader/bootloader.bin 0x8000 partition_table/partition-table.bin 0xe000 ota_data_initial.bin 0x20000 WardriveESP-esp32c3-app.bin
```

For each version, install Python 3 and esptool (`python -m pip install esptool`), connect the board by USB, find its COM port in Device Manager, extract the selected ZIP, and run that version's command from the extracted folder. Wait for the board to restart. Check package files against `SHA256SUMS.txt` if desired. The board must have 4 MB flash. Flashing replaces the current firmware.

## Source and attribution

Firmware is based on RocketGod's WardriveESP. The upstream project documents its supported boards, scanner behavior, and license at [RocketGod-git/WardriveESP](https://github.com/RocketGod-git/WardriveESP). The ESP32-C3 OLED support and Axon alert changes are local modifications for this board. Preserve upstream license and notices when redistributing.

## Packages

- `WardriveESP-ESP32-C3-OLED-v1.7.11-flashed.zip`
- `WardriveESP-ESP32-C3-OLED-v1.7.12.zip`
- `WardriveESP-ESP32-C3-OLED-v1.7.13.zip`

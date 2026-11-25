# WardriveESP for ESP32-C3 0.42-inch OLED

Board-targeted firmware for the ESP32-C3 development board with the onboard 72x40 SSD1306-compatible OLED (SDA GPIO5, SCL GPIO6), blue LED (GPIO8, active-low), and BOOT button (GPIO9).

## Releases

### v1.7.11 — flashed baseline

The baseline image successfully flashed to three boards. Includes C3 OLED support and WardriveESP Wi-Fi/Bluetooth scanning with Wardrive Go. No AXEOFF/Axon detection.

### v1.7.12 — initial AXEOFF alerts

Adds passive Axon signature detection from BLE advertisements and Wi-Fi beacons/probe requests. An alert shows `AX` and flashes the blue LED. BOOT cycles through dashboard, latest AXON log, and radio statistics.

### v1.7.13 — superseded

Do not install v1.7.13. Its embedded BLE UUID check used the wrong byte order and could miss Axon signatures.

### v1.7.14 — UUID byte-order fix

Correctly matches Axon service IDs inside 128-bit BLE service UUIDs. This is the latest app-connected version before standalone scanning.

### v1.7.15 — standalone Axon detector

No Wardrive Go connection is needed to detect Axon signatures. On the C3 OLED, the firmware automatically scans BLE for 45 seconds, then performs 15 seconds of passive Wi-Fi capture, repeating the cycle. A match shows `AX` and flashes the blue LED. When disconnected, the display says `AXON ACTIVE`; BOOT cycles through the dashboard, latest Axon hit, and radio statistics. The latest hit/count are RAM-only and reset at reboot; this board has no SD logging. Wardrive Go is optional: connecting it returns control to the app's normal scan modes, and standalone scanning resumes after disconnect.

Install from `WardriveESP-ESP32-C3-OLED-v1.7.15.zip`. In a terminal opened in the extracted folder, replace `COM4` with the assigned port:

```powershell
python -m esptool --chip esp32c3 -p COM4 -b 460800 write_flash --flash_mode dio --flash_freq 80m --flash_size 4MB 0x0 bootloader/bootloader.bin 0x8000 partition_table/partition-table.bin 0xe000 ota_data_initial.bin 0x20000 WardriveESP-esp32c3-app.bin
```

Install Python 3 and esptool (`python -m pip install esptool`), connect the board by USB, find its port in Device Manager, extract the ZIP, and run the command from the extracted folder. Wait for restart. Check the package files against `SHA256SUMS.txt` if needed. The board must have 4 MB flash. Flashing replaces the current firmware.

## Source and attribution

Based on RocketGod's [WardriveESP](https://github.com/RocketGod-git/WardriveESP). Preserve the upstream license and notices when redistributing. The C3 OLED and Axon detector changes are local modifications for this board.

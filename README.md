# SailorData NMEA2000 to BLE Bridge Firmware

This repository contains the official firmware for the **SailorData NMEA2000 to BLE bridge**. It bridges live NMEA2000 marine network data directly to your Garmin smartwatch, enabling real-time telemetry display via the **[Garmin ConnectIQ SailorData](https://apps.garmin.com/apps/7a1684d6-6b95-4c80-97c7-f928c7ab4e5a)** data field.

For full documentation, guides, and hardware information, visit [sailtech.dk](https://sailtech.dk).

## Key Features

* **NMEA2000 Engine Parsing:** Reads and processes standard NMEA2000 PGNs from your boat network.
* **Low-Latency BLE Broadcast:** Transmits marine data efficiently via Bluetooth Low Energy (BLE) to compatible Garmin devices.
* **NMEA to WIFI Router:** Transmits NMEA2000 PGNs via Wifi, so that apps like Navionics, OpenCPN, etc. can connect to the bridge via wifi and consume this data.
* **Polar Diagram:** Wifi hotspot which allows the real-time monitoring of marine telemetry and polar performance on the polar diagram.
* **Victron Energy:** The bridge reads live data from Victron Energy devices — including battery monitors, solar chargers, DC-DC converters, AC inverters, and AC chargers — via Bluetooth Low Energy (BLE) and sends it directly to your NMEA 2000 network for display on any chartplotter or instrument. 
* **Plug & Play:** Custom-designed to compile cleanly for target CAN-bus hardware.

## Hardware Requirements

This firmware is written and configured specifically for the following board:

* **[SK PANG ESP32S3 CAN-Bus Board](https://www.skpang.co.uk/products/esp32s3-can-bus-board)** (ESP32-S3 with onboard TWAI/CAN transceiver)
* **[Waveshare ESP32 S3 RS485 CAN-Bus DIN Rail module](https://www.waveshare.com/esp32-s3-rs485-can.htm)** (I have not tested this board myself, but on request of some people I have build the firmware for this board)

## Custom Enclosure

A custom 3D-printable protective enclosure is designed specifically for housing the SK PANG ESP32S3 CAN-Bus board on board your boat.

<Image src="enclosure/enclosure.png" alt="3D Printed Enclosure for ESP32 CAN Bus Board" caption="Custom 3D printable enclosure 3D model view" />

The 3D model STL files are provided in the `/enclosure` folder and are shared under the **Creative Commons License (CC BY-NC-SA 4.0)**. Feel free to download and print the enclosure for personal marine setups.

## Support the Project

If you find this project useful for your sailing setup, consider supporting future development:

👉 **[Buy Me a Coffee](https://www.buymeacoffee.com/sailtech)**

## Initial Firmware Flashing
In case you aquired the hardware yourself and you need todo the initial flashing of the firmware yourself:
There are two approaches to achieve this:

***Easy***
1. You need a Google Chrome Browser
2. Connect your board via USB to your computer
3. Open the [Web Flash Utility](https://espressif.github.io/esp-launchpad/minimal-launchpad/?flashConfigURL=https://raw.githubusercontent.com/sailtechdk/nmea2000-ble-bridge/refs/heads/main/firmware/config.toml)
4. Click *Connect Your Device*
5. Select you connected board
6. Click *Connect* and the flashing process will start
7. Click *Restart Device* and after a few seconds you should see `Starting SailorData Bridge...`. You can ignore the `nvs_open failed` error.

***Advanced***
1. Download the 4 .bin files from the /firmware folder which includes the latest firmware release file. The folder ESP32S3-CAN-N2K contains the the firmware for the SK Pang board, where the folder ESP32-S3-RS485-CAN contains the Waveshare DIN-Rail board.
2. Install the esptool for your specific platform
3. Connect the board via USB to your computer and identify which serial port the board is connected to. In the example below it is `/dev/cu.usbserial-7D52B70115`
4. Execute the following command to flash the firmware:
`python esptool.py --chip esp32s3 --port "/dev/cu.usbserial-7D52B70115" --baud 460800 --before default_reset --after hard_reset write_flash -z --flash_mode dio --flash_freq 80m --flash_size 8MB 0x0000 bootloader.bin 0x8000 partitions.bin 0xe000 boot_app0.bin 0x10000 firmware.bin`

5. For subsequent firmware updates you can use the OTA method desribed on [sailtech.dk](https://sailtech.dk), where you only need the latest firmware.bin file.

## Third-Party Libraries & Dependencies

This project relies on the following open-source libraries:

* [ttlappalainen/NMEA2000](https://github.com/ttlappalainen/NMEA2000) – Core NMEA2000 library for Arduino framework.
* [sergei/NMEA2000_esp32_twai](https://github.com/sergei/NMEA2000_esp32_twai) – ESP32 TWAI (Two-Wire Automotive Interface / CAN) driver implementation.

## License
© 2026 SailTech,
Author: Carsten Horst

* **Firmware:** All rights reserved. See [SailTech terms and conditions](https://sailtech.dk/terms.html).
* **3D Models & Enclosure Designs:** Licensed under **Creative Commons ([CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/))**.

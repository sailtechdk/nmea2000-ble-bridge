# SailorData: NMEA 2000 to BLE, Wi-Fi Bridge & Victron Gateway for Garmin Marine Watches

This repository contains the official ESP32-S3 firmware for the **[SailorData NMEA 2000 Bridge & Gateway](https://sailtech.dk/)**. Designed for **sailing and Garmin** enthusiasts, it bridges live **NMEA 2000 (`NMEA2000`)** marine network data directly to your **Garmin marine watch**, streams **NMEA 2000 to Wi-Fi** for navigation apps, calculates **real-time sail performance** from your boat's polars, and integrates **Victron to NMEA 2000** over Bluetooth Low Energy (BLE).

Pair the bridge with the free **[SailorData Garmin Marine Watch App on Connect IQ](https://apps.garmin.com/apps/7a1684d6-6b95-4c80-97c7-f928c7ab4e5a)** to view live boat telemetry on your wrist—working across **B&G, Raymarine, Simrad, Furuno, and Garmin** NMEA 2000 networks without ecosystem lock-in.

- **Official Website, Pre-Assembled Hardware & Documentation:** **[sailtech.dk — Garmin Marine Watch App, NMEA 2000 to Wi-Fi Gateway & Victron Bridge](https://sailtech.dk/)**
- **Live Web Interface & Polar Chart Preview:** **[Interactive SailorData Bridge Web UI Demo](https://sailtech.dk/demo)**
- **Supported Garmin Watches (50+ Models):** **[Garmin quatix, fēnix, epix, MARQ, Forerunner & tactix Compatibility List](https://sailtech.dk/#watches)**

## Key Features

* **Garmin Marine Watch App & Low-Latency BLE Broadcast:** Transmits real-time NMEA 2000 marine telemetry (`SOG`, `STW`, `COG`, `HDG`, `AWS`/`AWA`, `TWS`/`TWA`/`TWD`, `VMG`, `VMC`, `XTE`, `DTW`, `BRG`, `Depth`, and `Rudder Angle`) via Bluetooth Low Energy (BLE) directly to compatible Garmin smartwatches—no Garmin chartplotter required.
* **NMEA 2000 to Wi-Fi Bridge / Gateway:** Acts as a wireless **NMEA to Wi-Fi router and gateway**, translating NMEA 2000 PGNs into NMEA 0183 sentences streamed over Wi-Fi (`TCP`/`UDP`) so navigation apps like **Navionics Boating**, **OpenCPN**, **Savvy Navvy**, **iSailor**, and **Aqua Map** can consume live GPS, AIS, wind, depth, and speed data on tablets, phones, and laptops.
* **Victron to NMEA 2000 (`NMEA2000`) Integration:** Reads live electrical telemetry from **Victron Energy** devices—including battery monitors (**SmartShunt**, **BMV-712**), solar controllers (**SmartSolar MPPT**), **Orion-Tr Smart** DC-DC converters, AC inverters, and **Blue Smart** chargers—wirelessly via Bluetooth Low Energy (BLE Instant Readout) and broadcasts standard NMEA 2000 PGNs onto your backbone for display on any chartplotter or MFD.
* **Real-Time Sail Performance & Polar Diagram:** Built-in Wi-Fi web server and polar engine compute real-time **sail performance** and polar efficiency percentage (`STW` vs. theoretical target boat speed for current `TWS` and `TWA`), displaying live target speed efficiency and tactical upwind/downwind layline arcs on your Garmin watch and on the browser-based polar diagram.
* **Universal NMEA 2000 Engine Parsing & Plug-and-Play:** Reads and processes standard NMEA 2000 PGNs from any multi-vendor boat network, powered directly from the 12V NMEA 2000 backbone.

## Hardware Requirements

This firmware is written and configured specifically for the following ESP32-S3 CAN-bus boards (or you can order a **[Pre-Assembled Plug-and-Play SailorData NMEA 2000 Bridge](https://sailtech.dk/#products)**):

* **[SK PANG ESP32S3 CAN-Bus Board](https://www.skpang.co.uk/products/esp32s3-can-bus-board)** (ESP32-S3 with onboard TWAI/CAN transceiver)
* **[Waveshare ESP32 S3 RS485 CAN-Bus DIN Rail module](https://www.waveshare.com/esp32-s3-rs485-can.htm)** (Built on community request for DIN-rail marine electrical panels)

## Custom Enclosure

A custom 3D-printable protective enclosure is designed specifically for housing the SK PANG ESP32S3 CAN-Bus board on board your boat.

<Image src="enclosure/enclosure.png" alt="3D Printed Enclosure for SailorData ESP32-S3 NMEA 2000 to BLE and Wi-Fi Bridge" caption="Custom 3D printable enclosure 3D model view" />

The 3D model STL files are provided in the `/enclosure` folder and are shared under the **Creative Commons License (CC BY-NC-SA 4.0)**. Feel free to download and print the enclosure for personal marine setups.

## Support the Project

If you find this project useful for your sailing setup, consider supporting future development:

👉 **[Buy Me a Coffee](https://www.buymeacoffee.com/sailtech)**

## Initial Firmware Flashing
In case you acquired the hardware yourself and need to do the initial flashing of the firmware yourself, there are two approaches:

***Easy***
1. You need a Google Chrome Browser
2. Connect your board via USB to your computer
3. Open the [Web Flash Utility](https://espressif.github.io/esp-launchpad/minimal-launchpad/?flashConfigURL=https://raw.githubusercontent.com/sailtechdk/nmea2000-ble-bridge/refs/heads/main/firmware/config.toml)
4. Click *Connect Your Device*
5. Select your connected board
6. Click *Connect* and the flashing process will start
7. Click *Restart Device* and after a few seconds you should see `Starting SailorData Bridge...`. You can ignore the `nvs_open failed` error.

***Advanced***
1. Download the 4 `.bin` files from the `/firmware` folder which includes the latest firmware release file. The folder `ESP32S3-CAN-N2K` contains the firmware for the SK Pang board, while the folder `ESP32-S3-RS485-CAN` contains the firmware for the Waveshare DIN-Rail board.
2. Install `esptool` for your specific platform
3. Connect the board via USB to your computer and identify which serial port the board is connected to. In the example below it is `/dev/cu.usbserial-7D52B70115`
4. Execute the following command to flash the firmware:
`python esptool.py --chip esp32s3 --port "/dev/cu.usbserial-7D52B70115" --baud 460800 --before default_reset --after hard_reset write_flash -z --flash_mode dio --flash_freq 80m --flash_size 8MB 0x0000 bootloader.bin 0x8000 partitions.bin 0xe000 boot_app0.bin 0x10000 firmware.bin`

5. For subsequent firmware updates you can use the wireless OTA update method described in the **[SailTech Setup Guides & FAQ](https://sailtech.dk/#faq)**, where you only need the latest `firmware.bin` file.

## Third-Party Libraries & Dependencies

This project relies on the following open-source libraries:

* [ttlappalainen/NMEA2000](https://github.com/ttlappalainen/NMEA2000) – Core NMEA2000 library for Arduino framework.
* [sergei/NMEA2000_esp32_twai](https://github.com/sergei/NMEA2000_esp32_twai) – ESP32 TWAI (Two-Wire Automotive Interface / CAN) driver implementation.

## License
© 2026 [SailTech](https://sailtech.dk/)  
Author: Carsten Horst

* **Firmware:** All rights reserved. See [SailTech Terms and Conditions](https://sailtech.dk/terms).
* **3D Models & Enclosure Designs:** Licensed under **Creative Commons ([CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/))**.

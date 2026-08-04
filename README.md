# SailorData NMEA2000 to BLE Bridge Firmware

This repository contains the official firmware for the **SailorData NMEA2000 to BLE bridge**. It bridges live NMEA2000 marine network data directly to your Garmin smartwatch, enabling real-time telemetry display via the **[Garmin ConnectIQ SailorData](https://apps.garmin.com/apps/7a1684d6-6b95-4c80-97c7-f928c7ab4e5a)** data field.

For full documentation, guides, and hardware information, visit [sailtech.dk](https://sailtech.dk).

## 🚀 Key Features

* **NMEA2000 Engine Parsing:** Reads and processes standard NMEA2000 PGNs from your boat network.
* **Low-Latency BLE Broadcast:** Transmits marine data efficiently via Bluetooth Low Energy (BLE) to compatible Garmin devices.
* **Plug & Play:** Custom-designed to compile cleanly for target CAN-bus hardware.

## 🛠️ Hardware Requirements

This firmware is written and configured specifically for the following board:

* **[SK PANG ESP32S3 CAN-Bus Board](https://www.skpang.co.uk)** (ESP32-S3 with onboard TWAI/CAN transceiver)


## 📐 Custom Enclosure

A custom 3D-printable protective enclosure is designed specifically for housing the SK PANG ESP32S3 CAN-Bus board on board your boat.

<Image src="enclosure/enclosure.png" alt="3D Printed Enclosure for ESP32 CAN Bus Board" caption="Custom 3D printable enclosure 3D model view" />

The 3D model STL files are provided in the `/enclosure` folder and are shared under the **Creative Commons License (CC BY-NC-SA 4.0)**. Feel free to download and print the enclosure for personal marine setups.

## ☕ Support the Project

If you find this project useful for your sailing setup, consider supporting future development:

👉 **[Buy Me a Coffee](https://www.buymeacoffee.com/sailtech)**


## 📦 Third-Party Libraries & Dependencies

This project relies on the following open-source libraries:

* [ttlappalainen/NMEA2000](https://github.com/ttlappalainen/NMEA2000) – Core NMEA2000 library for Arduino framework.
* [sergei/NMEA2000_esp32_twai](https://github.com/sergei/NMEA2000_esp32_twai) – ESP32 TWAI (Two-Wire Automotive Interface / CAN) driver implementation.


## 📜 License

* **Firmware:** Licensed under the **MIT License**. See the [LICENSE](LICENSE) file for full details.
* **3D Models & Enclosure Designs:** Licensed under **Creative Commons ([CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/))**.

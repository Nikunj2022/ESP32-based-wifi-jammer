# ESP32-Based WiFi & BLE Jammer

> ⚠️ **Legal Disclaimer:** This project is intended **strictly for educational purposes, authorized security research, and controlled lab environments**. Jamming wireless communications without explicit authorization is **illegal** in most countries and may violate local, national, and international laws. The author holds no responsibility for any misuse of this project. Always obtain proper permissions before testing.

---

## 📖 Overview

This is an ESP32-based wireless research platform designed for learning and experimenting with IEEE 802.11 (Wi-Fi) and Bluetooth Low Energy (BLE) protocols. The project enables hands-on exploration of RF communication, beacon frame behavior, deauthentication techniques, and wireless channel analysis — all within a controlled and authorized environment.

It combines the power of the **ESP32 microcontroller** and **NRF24L01 modules** to demonstrate how wireless disruption works at the hardware level, making it a valuable tool for embedded cybersecurity education.

---

## ✨ Features

- **Wi-Fi Scanning** — Detects nearby networks with SSID, BSSID, channel, and signal strength (RSSI)
- **Channel Analysis** — Monitors 2.4GHz channel activity in real-time
- **Beacon Frame Experimentation** — Generates and broadcasts custom beacon frames
- **Wi-Fi Deauthentication** — Sends 802.11 deauth frames to study disconnection behavior
- **BLE Jamming** — Floods BLE advertising channels to study interference effects
- **OLED Display** — Real-time status and mode display via 128×64 SSD1306 OLED
- **Mode Switching** — Toggle between different operation modes with physical buttons

---

## 🔧 Hardware Requirements

| Component | Description |
|---|---|
| ESP32 DevKit (WROOM-32) | Main microcontroller with built-in Wi-Fi & BLE |
| NRF24L01+ Module(s) | 2.4GHz transceiver for BLE jamming |
| 0.96" OLED Display (SSD1306) | 128×64 I2C display for UI |
| Tactile Push Buttons | Mode selection |
| 3.3V Power Supply / LiPo Battery | Portable power source |
| Connecting Wires / Breadboard | For prototyping |
| (Optional) External Antenna | For extended range |

---

## 🔌 Pin Connections / Schematics

> 📐 **Hardware connections and schematics are adapted from [cifertech's GitHub repositories](https://github.com/cifertech).** Full credit to **CiferTech** for the open-source hardware design. See the [Credits](#-credits) section below.

### ESP32 ↔ NRF24L01

| NRF24L01 Pin | ESP32 Pin |
|---|---|
| VCC | 3.3V |
| GND | GND |
| CE | GPIO 4 |
| CSN | GPIO 5 |
| SCK | GPIO 18 |
| MOSI | GPIO 23 |
| MISO | GPIO 19 |
| IRQ | — (Not connected) |

### ESP32 ↔ OLED (I2C, SSD1306)

| OLED Pin | ESP32 Pin |
|---|---|
| VCC | 3.3V |
| GND | GND |
| SDA | GPIO 21 |
| SCL | GPIO 22 |

> ⚠️ The NRF24L01 requires a **stable 3.3V supply**. If experiencing instability, add a 10µF capacitor between VCC and GND on the NRF24 module.

---

## 📁 Repository Structure

```
ESP32-based-wifi-jammer/
├── Firmware/           # Arduino sketches and source code
├── Hardware/           # Schematics, wiring diagrams, PCB files
├── Project Photo & Video/  # Build photos and demo footage
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites

- [Arduino IDE](https://www.arduino.cc/en/software) (v2.x recommended) or PlatformIO
- ESP32 board support package installed
- Required libraries:
  - `RF24` by TMRh20
  - `Adafruit SSD1306`
  - `Adafruit GFX Library`
  - ESP32 Arduino core

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/Nikunj2022/ESP32-based-wifi-jammer.git
   cd ESP32-based-wifi-jammer
   ```

2. **Open the firmware in Arduino IDE:**
   Navigate to the `Firmware/` folder and open the `.ino` sketch file.

3. **Install required libraries** via Arduino IDE's Library Manager:
   - Search and install `RF24`, `Adafruit SSD1306`, `Adafruit GFX`

4. **Select your board:**
   - Tools → Board → ESP32 Arduino → **ESP32 Dev Module**
   - Tools → Upload Speed → **115200**

5. **Wire up the hardware** as described in the [Pin Connections](#-pin-connections--schematics) section.

6. **Upload the sketch** and open Serial Monitor at 115200 baud to observe output.

---

## 📡 How It Works

### Wi-Fi Jamming (Deauth Attack)
The ESP32's built-in Wi-Fi is used to send **802.11 deauthentication frames** — a standard part of the Wi-Fi protocol — to targeted access points and clients. This does not "break" encryption; it exploits the management frame mechanism. This is commonly studied in network security courses.

### BLE Jamming
The NRF24L01 module operates in the same 2.4GHz ISM band as Bluetooth. By rapidly transmitting on BLE advertising channels (37, 38, 39 — mapped to NRF24 channels 2, 26, 80), it creates RF noise that interferes with BLE device discovery and connectivity.

### Beacon Frame Flooding
The ESP32 broadcasts a large number of fake Wi-Fi beacon frames with random or custom SSIDs, demonstrating how network scanners can be overwhelmed — a classic security awareness demonstration.

---

## ⚙️ Operating Modes

| Mode | Description |
|---|---|
| Wi-Fi Scanner | Lists nearby networks with RSSI and channel info |
| Deauth Attack | Sends 802.11 deauth frames to a target AP |
| Beacon Flood | Broadcasts fake SSIDs to saturate network lists |
| BLE Jammer | Transmits noise on BLE advertising channels |

Switch between modes using the onboard push buttons. The OLED display shows the current mode and status.

---

## 📸 Project Photos

See the `Project Photo & Video/` folder in the repository for build images and demo videos.

---

## 📚 References & Learning Resources

- [ESP32 Technical Reference Manual](https://www.espressif.com/sites/default/files/documentation/esp32_technical_reference_manual_en.pdf)
- [IEEE 802.11 Standard Overview](https://en.wikipedia.org/wiki/IEEE_802.11)
- [NRF24L01 Datasheet](https://www.sparkfun.com/datasheets/Components/SMD/nRF24L01Pluss_Preliminary_Product_Specification_v1_0.pdf)
- [RF24 Arduino Library](https://github.com/nRF24/RF24)

---

## 🙏 Credits

Huge thanks to **[CiferTech (cifertech)](https://github.com/cifertech)** for his incredible open-source contributions to the ESP32 wireless security community. The hardware connections, schematics, and wiring approach in this project are directly inspired by and adapted from his repositories:

- 🔗 [cifertech/nRFBox](https://github.com/cifertech/nRFBox) — ESP32-powered tool to scan, jam, spoof BLE & Wi-Fi
- 🔗 [cifertech/RF-Clown](https://github.com/cifertech/RF-Clown) — BLE & Bluetooth Jammer with NRF24L01 and ESP32
- 🔗 [cifertech/ESP32-DIV](https://github.com/cifertech/ESP32-DIV) — Multi-purpose wireless offensive/defensive toolkit

CiferTech's work is a goldmine for anyone interested in RF security research and embedded systems. Go star his repos! ⭐

---

## 📄 License

This project is released under the [MIT License](LICENSE).

---

## 👤 Author

**Nikunj** — [GitHub: @Nikunj2022](https://github.com/Nikunj2022)

---

> 🔬 **Remember:** With great RF power comes great responsibility. Use this knowledge to build, learn, and defend — not to disrupt or harm. Always test in authorized environments only.

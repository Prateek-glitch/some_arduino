# 🌐 ESP8266 Captive Portal

<div align="center">

![ESP8266](https://img.shields.io/badge/ESP8266-E7352C?style=for-the-badge&logo=espressif&logoColor=white)
![Arduino](https://img.shields.io/badge/Arduino-00979D?style=for-the-badge&logo=arduino&logoColor=white)
![C++](https://img.shields.io/badge/C++-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)

*A sophisticated captive portal implementation for ESP8266 NodeMCU with credential harvesting capabilities*

</div>

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Hardware Requirements](#hardware-requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Code Structure](#code-structure)
- [Security Considerations](#security-considerations)
- [Legal Disclaimer](#legal-disclaimer)
- [Contributing](#contributing)
- [License](#license)

## 🔍 Overview

This project implements a captive portal attack using the ESP8266 NodeMCU microcontroller. The device creates a fake WiFi access point that mimics the "RVCE" network and presents users with a convincing authentication page to capture login credentials.

**⚠️ This project is for educational and authorized penetration testing purposes only.**

## ✨ Features

- **Fake Access Point**: Creates a spoofed WiFi network with MAC address cloning
- **Captive Portal**: Automatically redirects users to the login page
- **Credential Harvesting**: Captures and stores usernames and passwords
- **SPIFFS Storage**: Persistent credential storage on the device
- **Cross-Platform Detection**: Supports captive portal detection for Android, iOS, and Windows
- **Responsive Design**: Mobile-friendly authentication interface
- **Real-time Monitoring**: Serial output for immediate credential viewing
- **Web-based Logs**: Access captured credentials via `/logs` endpoint

## 🛠️ Technologies Used

### Hardware
<div align="center">

| Technology | Description | Logo |
|------------|-------------|------|
| **ESP8266** | Low-cost Wi-Fi microchip with full TCP/IP stack | <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/00/Espressif_logo.svg/120px-Espressif_logo.svg.png" width="60"> |
| **NodeMCU** | Open-source IoT platform based on ESP8266 | <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/f1/NodeMCU_DEVKIT_1.0.jpg/120px-NodeMCU_DEVKIT_1.0.jpg" width="60"> |

</div>

### Software & Libraries
<div align="center">

| Technology | Description | Logo |
|------------|-------------|------|
| **Arduino IDE** | Development environment for microcontrollers | <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/87/Arduino_Logo.svg/120px-Arduino_Logo.svg.png" width="60"> |
| **ESP8266WiFi** | WiFi library for ESP8266 | <img src="https://img.icons8.com/color/48/000000/wifi.png" width="40"> |
| **ESP8266WebServer** | HTTP server library | <img src="https://img.icons8.com/color/48/000000/server.png" width="40"> |
| **DNSServer** | DNS server implementation | <img src="https://img.icons8.com/color/48/000000/dns.png" width="40"> |
| **SPIFFS** | SPI Flash File System | <img src="https://img.icons8.com/color/48/000000/database.png" width="40"> |

</div>

### Web Technologies
<div align="center">

| Technology | Description | Logo |
|------------|-------------|------|
| **HTML5** | Markup language for the captive portal interface | <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/61/HTML5_logo_and_wordmark.svg/120px-HTML5_logo_and_wordmark.svg.png" width="60"> |
| **CSS3** | Styling for responsive design | <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/d5/CSS3_logo_and_wordmark.svg/120px-CSS3_logo_and_wordmark.svg.png" width="60"> |
| **C++** | Programming language for ESP8266 firmware | <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/18/ISO_C%2B%2B_Logo.svg/120px-ISO_C%2B%2B_Logo.svg.png" width="60"> |

</div>

## 🔧 Hardware Requirements

- **ESP8266 NodeMCU** development board
- **Micro USB cable** for programming and power
- **Computer** with Arduino IDE installed

## 📦 Installation

### 1. Arduino IDE Setup

1. Download and install [Arduino IDE](https://www.arduino.cc/en/software)
2. Add ESP8266 board support:
   - Go to **File > Preferences**
   - Add `http://arduino.esp8266.com/stable/package_esp8266com_index.json` to Additional Board Manager URLs
   - Go to **Tools > Board > Boards Manager**
   - Search for "ESP8266" and install the package

### 2. Library Installation

Install the following libraries via **Tools > Manage Libraries**:
- `ESP8266WiFi` (usually pre-installed)
- `ESP8266WebServer` (usually pre-installed)
- `DNSServer` (usually pre-installed)

### 3. Upload the Code

1. Connect your NodeMCU to your computer
2. Select the correct board: **Tools > Board > ESP8266 Boards > NodeMCU 1.0**
3. Select the correct port: **Tools > Port**
4. Copy the provided code into Arduino IDE
5. Click **Upload**

## 🚀 Usage

### Basic Operation

1. **Power on** the NodeMCU device
2. The device will create a WiFi network named **"RVCE"**
3. Users connecting to this network will be automatically redirected to the captive portal
4. Captured credentials are stored in SPIFFS and displayed via Serial monitor

### Accessing Logs

- **Serial Monitor**: View real-time credential capture at 115200 baud
- **Web Interface**: Visit `http://192.168.4.1/logs` to view all captured credentials

### Network Configuration

```cpp
const char *ssid = "RVCE";                              // Network name
IPAddress apIP(192, 168, 4, 1);                        // Access Point IP
uint8_t spoofedMAC[6] = {0xF4, 0x06, 0x69, 0x7C, 0x7C, 0x43}; // MAC address

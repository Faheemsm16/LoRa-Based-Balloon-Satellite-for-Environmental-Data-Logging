# LoRa-Based-Balloon-Satellite-for-Environmental-Data-Logging

## Overview

This project showcases a **low-cost atmospheric balloon satellite (CanSat)** system using:

- **LoRa (433 MHz)** for long-range wireless telemetry  
- **NEO-6M GPS** for location tracking  
- **DS18B20** digital sensor for temperature measurements  
- **SD Card** logging for offline data storage  
- Powered by **ESP32** microcontroller

## Components Used

| Component       | Function                              |
|----------------|----------------------------------------|
| ESP32          | Main controller (Sender + Receiver)    |
| NEO-6M GPS     | Latitude/Longitude detection           |
| DS18B20        | Temperature sensing                    |
| SD Card Module | Logging sensor data                    |
| LoRa SX1278    | Long-range communication               |
| Power Bank     | Power source for payload               |

## System Architecture

### Sender Node (on Balloon)
- Reads **temperature** and **GPS** data
- Logs data to **SD Card**
- Sends packet via **LoRa**

### Receiver Node (on Ground)
- Listens for LoRa packets
- Displays data on **Serial Monitor** with RSSI info

## Code Overview

### Sender (ESP32 + LoRa + GPS + DS18B20 + SD)
> File: `ESP_32 GPS Temp SD.txt`

- Gets GPS coordinates (latitude, longitude)
- Reads ambient temperature
- Stores data on SD card
- Sends data using LoRa
- Uses `TinyGPS`, `DallasTemperature`, and `LoRa` libraries

**Key Features**:
- Deep sleep-ready architecture
- Sliding GPS reading buffer
- Timestamped SD entries
- SHARING telemetry over serial and LoRa

### Receiver (ESP32 + LoRa)
> File: `Receiver Code.txt`

- Listens for LoRa packets
- Displays messages and RSSI in serial monitor
- Uses `LoRa` library

## Sample Data Format (Sent & Logged)

```
Temp: 24.75°C , (Lat,Lon): (12.9721, 77.5933)
```

And logged into SD as:

```
Reading ID, temperatureC, Latitude, Longitude,
Temp: 24.75°C , (Lat,Lon): (12.9721,77.5933)
```

## Setup Instructions

### Hardware Connections
- **LoRa**: Connect via SPI to ESP32 (DIO0, NSS, RST)
- **GPS**: Connected via `SoftwareSerial` (Rx:16, Tx:17)
- **Temp Sensor**: DS18B20 via OneWire on GPIO4
- **SD Card**: CS pin on GPIO15, SPI for data
- Use pull-up resistor (4.7kΩ) for DS18B20 data line

### Software
- Install libraries:
  - `TinyGPS`
  - `DallasTemperature`
  - `OneWire`
  - `LoRa`
  - `SD`
- Upload sender and receiver codes to separate ESP32 boards

## Features

- Real-time transmission of atmospheric telemetry
- Local storage on SD for redundancy
- Easy to deploy and recover from balloon missions
- Low power + lightweight system

## Possible Enhancements

- Add **altitude sensors (BMP280/Barometer)**
- Use **OLED** on ground station
- Enable **deep sleep** for energy efficiency
- Build **Python GUI** for live tracking

## 📄 License

This project is licensed under the **MIT License**.

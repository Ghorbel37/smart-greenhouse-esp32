# 🌱 Smart Greenhouse Monitoring System

An IoT-based greenhouse monitoring and automation system using ESP32 that monitors temperature and humidity, automatically controls ventilation, and sends real-time data to ThingsBoard cloud platform.

## 📋 Project Overview

This project simulates a smart greenhouse system that:
- **Monitors** temperature and humidity using a DHT22 sensor
- **Controls** ventilation automatically via a servo motor based on temperature thresholds
- **Sends** real-time telemetry data to ThingsBoard cloud platform via MQTT
- **Simulates** on Wokwi platform for easy testing and demonstration

## 🔧 Hardware Components

- **ESP32 DevKit C V4** - Main microcontroller
- **DHT22** - Temperature and humidity sensor
- **Servo Motor** - Controls ventilation window/vent

## 📐 Circuit Connections

| Component | ESP32 Pin | Description |
|-----------|-----------|-------------|
| DHT22 SDA | GPIO 4 | Data pin for temperature/humidity readings |
| DHT22 VCC | 3.3V | Power supply |
| DHT22 GND | GND | Ground |
| Servo PWM | GPIO 26 | Control signal for servo motor |
| Servo V+ | 5V | Power supply for servo |
| Servo GND | GND | Ground |

## 🚀 Features

### Temperature-Based Ventilation Control
The system automatically adjusts ventilation based on temperature:
- **≤ 22°C**: Vent closed (0°)
- **22-25°C**: Vent partially open (90°)
- **> 25°C**: Vent fully open (180°)

### Cloud Integration
- Real-time telemetry data sent to ThingsBoard
- Monitors: temperature, humidity, and door/vent status
- Data sent every 2 seconds
- MQTT protocol for reliable communication

## 📚 Libraries Required

All libraries are specified in `libraries.txt` for Wokwi simulation.

## ⚙️ Setup Instructions

### 1. Wokwi Simulation
1. Open the project on [Wokwi](https://wokwi.com)
2. The simulation will automatically load all required libraries
3. Click "Start Simulation" to run

### 2. ThingsBoard Configuration
1. Create a device on [ThingsBoard Cloud](https://thingsboard.cloud)
2. Copy the device access token
3. Replace `REPLACE_WITH_THINGSBOARD_TOKEN` in `sketch.ino` with your token:
   ```cpp
   #define TOKEN "YOUR_ACCESS_TOKEN_HERE"
   ```

### 3. WiFi Configuration
For physical deployment (non-Wokwi):
```cpp
const char* ssid = "YOUR_WIFI_SSID";
const char* password = "YOUR_WIFI_PASSWORD";
```

## 📊 Data Telemetry

The system sends the following data to ThingsBoard:
- `temperature` - Current temperature in °C
- `humidity` - Current relative humidity in %
- `servoPosition` - Door/vent status (true = open, false = closed)

## 🖥️ Serial Monitor Output

```
Connecting to Wi-Fi.....
Wi-Fi connected
IP address: 192.168.1.x
Connecting to ThingsBoard server
Connected to ThingsBoard
Humidity: 45.0%  Temperature: 26.5°C Heat index: 27.2
Servo position: 180°
```

## 📁 Project Structure

```
smart-greenhouse-esp32/
├── sketch.ino          # Main Arduino code
├── diagram.json        # Wokwi circuit diagram
├── libraries.txt       # Required libraries
└── README.md           # This file
```

## 🎯 How It Works

1. **Initialization**: ESP32 connects to WiFi and ThingsBoard cloud
2. **Sensing**: DHT22 reads temperature and humidity every 2 seconds
3. **Decision**: System evaluates temperature against thresholds
4. **Action**: Servo motor adjusts vent position if needed
5. **Communication**: Data sent to ThingsBoard for monitoring and analysis

## 🔄 Loop Cycle

```
Read Sensor → Check Temperature → Adjust Ventilation → Send to Cloud → Wait 2s → Repeat
```

## 🛠️ Customization

### Adjust Temperature Thresholds
Modify these values in `sketch.ino`:
```cpp
if (temp > 25 && lastServoPosition != 180) {
    // Fully open
} else if (temp > 22 && temp <= 25 && lastServoPosition != 90) {
    // Partially open
} else if (temp <= 22 && lastServoPosition != 0) {
    // Closed
}
```

### Change Update Interval
```cpp
const long interval = 2000; // Change to desired milliseconds
```

## 🌐 ThingsBoard Dashboard

Create a dashboard in ThingsBoard to visualize:
- Real-time temperature graph
- Humidity gauge
- Vent status indicator
- Historical data charts

## 🔗 Links

- **Wokwi Project**: https://wokwi.com/projects/416379281766396929
- **ThingsBoard**: https://thingsboard.cloud
- **ESP32 Documentation**: https://docs.espressif.com/

## 🤝 Contributing

Feel free to fork this project and submit pull requests for improvements such as:
- Additional sensors (soil moisture, light intensity)
- Advanced control algorithms
- Mobile app integration
- Energy optimization features

## 📄 License

This project is licensed under the [MIT License](LICENSE).

## ⚠️ Important Notes

- Replace the ThingsBoard token before deploying
- Wokwi uses DHT22 instead of DHT11 due to simulator limitations
- Serial baud rate is set to 9600
- Ensure stable WiFi connection for cloud communication

---

**Made with ❤️ for smart agriculture and IoT learning**

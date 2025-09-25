# 🚗 IoT Parking Monitor

## 📋 Project Overview

An advanced IoT-based smart parking management system designed to revolutionize parking space monitoring and management. This system uses ESP32 microcontroller with multiple IR sensors to detect vehicle presence in real-time, providing instant feedback through LED indicators and cloud-based data synchronization via Firebase.

## ✨ Key Features

- **🔍 Real-time Vehicle Detection**: 8 precision IR sensors for accurate parking space monitoring
- **💡 Visual Status Indicators**: Individual LED feedback for each parking space
- **☁️ Cloud Integration**: Firebase Realtime Database for instant data synchronization
- **📱 Remote Monitoring**: Access parking data from anywhere via Firebase console
- **🌐 WiFi Connectivity**: Wireless communication for seamless remote access
- **🎛️ Remote Control**: GPIO-based LED control through Firebase interface
- **⚡ Live Updates**: Real-time database streaming for instant status changes

## 🔧 Hardware Requirements

| Component | Quantity | Specification |
|-----------|----------|---------------|
| ESP32 Development Board | 1 | ESP32 DOIT DevKit v1 |
| IR Sensors | 8 | Digital output type |
| LEDs | 8 | Standard 5mm LEDs |
| Resistors | 8 | 220Ω - 330Ω for LED current limiting |
| Breadboard/PCB | 1 | For circuit connections |
| Power Supply | 1 | 5V/2A recommended |
| Jumper Wires | As needed | Male-to-male/female |

## 📌 Pin Configuration

### 🔌 IR Sensor Connections
```
IR Sensor 1  → GPIO 25    IR Sensor 5  → GPIO 18
IR Sensor 2  → GPIO 36    IR Sensor 6  → GPIO 5
IR Sensor 3  → GPIO 39    IR Sensor 7  → GPIO 4
IR Sensor 4  → GPIO 34    IR Sensor 8  → GPIO 13
```

### 💡 LED Indicator Connections
```
LED 1  → GPIO 12    LED 5  → GPIO 22
LED 2  → GPIO 14    LED 6  → GPIO 23
LED 3  → GPIO 19    LED 7  → GPIO 26
LED 4  → GPIO 21    LED 8  → GPIO 27
```

## 📚 Software Dependencies

- **PlatformIO**: Cross-platform IDE for embedded development
- **Arduino Framework**: Programming framework for ESP32
- **Firebase ESP Client Library**: `mobizt/Firebase Arduino Client Library for ESP8266 and ESP32@^4.4.12`

## 🚀 Installation & Setup

### 1️⃣ Hardware Assembly
1. Connect IR sensors to designated GPIO pins with proper power supply
2. Install LEDs with current-limiting resistors on specified GPIO pins
3. Ensure stable 5V power supply for reliable operation
4. Test all connections with multimeter before programming

### 2️⃣ Firebase Project Setup
1. Navigate to [Firebase Console](https://console.firebase.google.com/)
2. Create a new Firebase project
3. Enable **Realtime Database** service
4. Configure **Authentication** → Enable Email/Password provider
5. Set appropriate database security rules
6. Note down your API Key and Database URL

### 3️⃣ Software Configuration
1. Install **PlatformIO** extension in VS Code
2. Open this project in PlatformIO
3. Update configuration in `src/main.cpp`:
   ```cpp
   #define WIFI_SSID "Your_WiFi_Name"
   #define WIFI_PASSWORD "Your_WiFi_Password"
   #define API_KEY "Your_Firebase_API_Key"
   #define USER_EMAIL "your-email@domain.com"
   #define USER_PASSWORD "your_password"
   #define DATABASE_URL "your-project-default-rtdb.firebaseio.com"
   ```

### 4️⃣ Build & Deploy
```bash
# Build the project
pio run

# Upload to ESP32
pio run --target upload

# Monitor serial output
pio device monitor --baud 115200
```

## 🗂️ Database Structure

Firebase Realtime Database schema:

```json
{
  "parkingstatus": {
    "IR_Sensor_1": 0,  // 0 = Available, 1 = Occupied
    "IR_Sensor_2": 1,
    "IR_Sensor_3": 0,
    "IR_Sensor_4": 1,
    "IR_Sensor_5": 0,
    "IR_Sensor_6": 1,
    "IR_Sensor_7": 0,
    "IR_Sensor_8": 1
  },
  "board1": {
    "outputs": {
      "digital": {
        "12": 0,  // LED control (0 = OFF, 1 = ON)
        "14": 1,
        "19": 0,
        "21": 1,
        "22": 0,
        "23": 1,
        "26": 0,
        "27": 1
      }
    }
  }
}
```

## ⚙️ System Operation

### 🔄 Automatic Monitoring
- IR sensors continuously scan for vehicle presence
- Sensor data uploads to Firebase every 1 second
- Real-time database streaming enables instant updates
- Serial monitor displays live sensor readings and system status

### 🎮 Remote LED Control
Control LEDs remotely via Firebase:
- Navigate to: `board1/outputs/digital/{gpio_pin}`
- Set value: `1` (LED ON) or `0` (LED OFF)
- Changes reflect instantly on the hardware

### 📊 Monitoring Dashboard
Serial monitor displays:
- WiFi connection status
- Firebase authentication status
- Live sensor readings
- Database synchronization confirmations
- Error messages and debugging information

## 🛠️ Troubleshooting Guide

### 📶 WiFi Connection Issues
- ✅ Verify SSID and password accuracy
- ✅ Ensure 2.4GHz network (ESP32 doesn't support 5GHz)
- ✅ Check signal strength at installation location
- ✅ Restart ESP32 if connection fails

### 🔐 Firebase Authentication Problems
- ✅ Verify API key and project credentials
- ✅ Check authentication method is enabled
- ✅ Ensure database rules allow read/write access
- ✅ Verify user email/password combination

### 🔍 Sensor Malfunction
- ✅ Check physical wiring connections
- ✅ Verify GPIO pin assignments
- ✅ Test sensors individually with multimeter
- ✅ Ensure proper power supply voltage

### 💾 Database Sync Issues
- ✅ Monitor serial output for error messages
- ✅ Verify internet connection stability
- ✅ Check Firebase database rules
- ✅ Ensure project billing is active (if required)

## 🏗️ Project Structure

```
iot-parking-monitor/
├── src/
│   └── main.cpp          # Main application code
├── include/
│   └── README            # Include directory info
├── lib/
│   └── README            # Library directory info
├── test/
│   └── README            # Test directory info
├── .vscode/              # VS Code configuration
├── .pio/                 # PlatformIO build files
├── platformio.ini        # Project configuration
├── .gitignore           # Git ignore rules
└── README.md            # Project documentation
```

## 🚀 Future Enhancements

- [ ] Mobile application development
- [ ] Web-based monitoring dashboard
- [ ] SMS/Email notifications
- [ ] Parking reservation system
- [ ] Payment integration
- [ ] Analytics and reporting
- [ ] Multiple parking lot support

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

## 🤝 Contributing

We welcome contributions! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📞 Support & Contact

- 📧 **Email**: admin@saipreetham.com
- 🐛 **Issues**: [GitHub Issues](https://github.com/Saipreetham0/iot-parking-monitor/issues)
- 📖 **Documentation**: [Project Wiki](https://github.com/Saipreetham0/iot-parking-monitor/wiki)

## 🙏 Acknowledgments

- Firebase team for excellent real-time database services
- PlatformIO community for the development platform
- ESP32 community for hardware support and documentation

---

**⭐ If this project helped you, please give it a star!**
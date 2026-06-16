# Temperature Monitoring System with MQTT

## Overview

This project implements a temperature monitoring system using Arduino Uno, DHT11 sensor, 16x2 character LCD with I2C backpack, and MQTT for data transmission.

## System Architecture

````
+-----------------------+
  |  DHT11 Temp Sensor    |
  |  (Digital Signal Pin) |
  +-----------+-----------+
              | (Pin D2)
              v
  +-----------------------+       +-------------------------+
  |      Arduino Uno      | ----> | 16x2 I2C Display Board  |
  |   Processing Engine   |       | (Address 0x27 on A4/A5) |
  +-----------+-----------+       +-------------------------+
              |
              | (USB Serial Communication on COM6)
              v
  +-----------------------+
  | PC-Side Python Script |
  | (Parser & Terminal)   |
  +-----------+-----------+
              |
              | (Network IP Protocol via MQTT Port 1883)
              v
  +-----------------------+
  |   VPS Hosted Broker   | ----> [ Visual Data Dashboard Link ]
  +-----------------------+
`

## Hardware Wiring Guide

### Arduino Uno - DHT11 Sensor

- DHT11 VCC → Arduino 5V
- DHT11 GND → Arduino GND
- DHT11 Data → Arduino Digital Pin 2

### Arduino Uno - 16x2 LCD with I2C Backpack

- LCD VCC → Arduino 5V (must use 5V, 3.3V won't work)
- LCD GND → Arduino GND
- LCD SDA → Arduino Analog A4
- LCD SCL → Arduino Analog A5

### LCD Contrast Adjustment

If the LCD lights up but no text is visible, turn the small potentiometer (contrast knob) on the back of the I2C backpack slowly until the text appears clearly.

## Software Setup

### Arduino Libraries

Install these libraries via Arduino Library Manager:

1. LiquidCrystal I2C
2. DHT Sensor Library

### Python Dependencies

Install required packages:

```bash
pip install pyserial paho-mqtt
````

## Usage

### 1. Upload Firmware

- Open `firmware/firmware.ino` in Arduino IDE
- Select correct board and port
- Upload to Arduino Uno
- **Note**: If LCD doesn't work, try changing the I2C address from `0x27` to `0x3F` in the code

### 2. Configure Python Client

- Open `app/monitor.py`
- Update the following constants at the top:
  - `SERIAL_PORT`: Your Arduino's serial port (e.g., COM6 on Windows, /dev/ttyUSB0 on Linux)
  - `MQTT_BROKER`: Your VPS broker IP address
  - `MQTT_PORT`: MQTT broker port (default 1883)
  - `MQTT_TOPIC`: Topic for publishing data (e.g., "exam/device/temp&mqtt/derick")

### 3. Run Python Client

```bash
cd app
python monitor.py
```

### 4. Use the Web Dashboard

- Open `client/index.html` in your web browser
- Verify the broker settings (broker IP, port, topic)
- Click "Connect" to subscribe to the MQTT topic
- View real-time temperature data and the graph
- **Note**: For the browser dashboard to work, your MQTT broker must support WebSocket connections! If it doesn't, you can use a proxy or use a broker that supports WebSockets (like Mosquitto with websockets enabled).

## Communication Details

### Serial Communication

- Baud rate: 9600
- Data format: Prefixed temperature value (e.g., "TEMP:25.50")

### MQTT Topic

- Topic: `exam/device/temp&mqtt/derick`
- Payload format: JSON `{"temperature": 25.50}`

## Submission Links

- GitHub Repository: [https://github.com/Der-Feb/Temperature-MQTT-]
- Cloud Dashboard: [http://157.173.101.159:8207/]

# Hardware Connections Guide

Follow this guide to correctly wire your Arduino Uno to the 3-pin DHT11 temperature sensor and the I2C 16x2 LCD display.

---

## 1. DHT11 Temperature Sensor Wiring (3-Pin)

Since your DHT module has `S`, `Middle`, and `-` pins, wire it as follows:

| DHT11 Pin | Arduino Uno Pin | Description                 |
| :-------- | :-------------- | :-------------------------- |
| Middle    | 3.3V            | Power supply (VCC)          |
| `-`       | GND             | Ground                      |
| `S`       | Digital Pin 2   | Data signal for temperature |

---

## 2. 16x2 LCD Display Wiring (I2C Mode)

Since your LCD has `GND`, `VCC`, `SDA`, and `SCL` pins, it has an I2C backpack. This makes wiring incredibly easy!

| LCD Pin | Arduino Uno Pin | Description                                |
| :------ | :-------------- | :----------------------------------------- |
| GND     | GND             | Ground                                     |
| VCC     | 5V              | Power supply                               |
| SDA     | A4              | I2C Data (Analog Pin 4)                    |
| SCL     | A5              | I2C Clock (Analog Pin 5)                   |

> **Note**: If your LCD screen turns on but the text is not visible, use a small screwdriver to turn the blue potentiometer screw located on the back of the I2C module to adjust the contrast.

---

Once wired, upload `arduino_temp_lcd.ino` to the board via USB to verify it works! 
*(Make sure you have installed the `LiquidCrystal I2C` library in your Arduino IDE via Tools -> Manage Libraries).*

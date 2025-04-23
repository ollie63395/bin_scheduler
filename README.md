# 🗑️ Smart Bin Reminder (Arduino Project)

This is a fun and practical Arduino-based project that automatically reminds household members which bin to take out and whose turn it is each week!

## 📋 Project Description

Our house has 3 people, and we alternate bin duty every week.  
Bins (red for general waste and yellow for recyclables) are also alternated weekly.

To avoid confusion and forgetfulness, this project uses an Arduino to display:

- 📆 The current date and day of the week
- 👤 The person in charge of bin duty for the current week
- 🟥🟨 The bin to take out (red or yellow)
- 🔴🟡 Optional: Red and yellow LEDs light up based on bin type

## 🧠 Features

- Real-time display using an LCD1602 screen
- Timekeeping with a DS1307 RTC module (with battery backup)
- Automatic rotation of people and bin type every week
- LEDs indicate bin color (red or yellow)
- Weekly update happens every **Tuesday night at midnight**

## 📦 Hardware Used

- Arduino Uno R3
- LCD1602 (non-I2C) display
- DS1307 RTC module with CR2032 battery
- 1 × Red LED + 220Ω resistor
- 1 × Yellow LED + 220Ω resistor
- Breadboard + jumper wires
- Optional: 9V adapter or USB power bank for wall mounting

## 🔌 Wiring Summary

| Component | Arduino Pin |
|----------|--------------|
| LCD RS   | 12           |
| LCD E    | 11           |
| LCD D4–D7| 5, 4, 3, 2    |
| LED (Red) | 7           |
| LED (Yellow) | 8        |
| RTC SDA  | A4           |
| RTC SCL  | A5           |

LCD uses potentiometer for contrast and backlight via 5V/GND.

## 🧾 How It Works

- A fixed start date is used (e.g., March 12, 2025)
- Weeks are counted from that date
- `weekNumber % 3` rotates between:
  - Hannah → Ollie → Emmy
- `weekNumber % 2` alternates between:
  - Red bin and Yellow bin
- The display updates every 5 seconds, but the actual duty change happens **weekly at Wednesday 00:00**

## 📸 Future Improvements

- Use a larger TFT screen for more advanced display layouts
- Add buzzer reminder for Monday nights
- Add Wi-Fi sync (ESP32) to get date/time online
- 3D print or laser-cut an enclosure for a polished look

## 🛠️ Setup

1. Install the Arduino IDE
2. Install required libraries:
   - `RTClib` (by Adafruit)
   - `LiquidCrystal`
3. Wire the circuit as shown
4. Upload the `.ino` file to your Arduino
5. Power it using a USB power bank or 9V adapter

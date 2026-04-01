# 🚨 STM32 Fall Detection System using FreeRTOS

## 📌 Overview
This project implements a **real-time Fall Detection System** using an STM32 microcontroller and **FreeRTOS**.  
It uses an **MPU6050 accelerometer & gyroscope sensor** to monitor motion and detect falls based on **impact + tilt analysis**.

## 🎯 Key Features
- 📊 Real-time motion monitoring (Accelerometer + Gyroscope)
- ⚡ Fall detection using **impact threshold + orientation change**
- 🧵 Multi-tasking using FreeRTOS
- 🔔 Event-based alert system using task notifications
- 💡 LED indication for fall detection
- 🖥️ UART output for debugging (Tera Term)

---

## 🧠 Detection Algorithm
The system detects a fall in **two stages**:

### 1️⃣ Impact Detection
- Compute total acceleration:
- aTotal = sqrt(Ax² + Ay² + Az²) / 16384
- If :aTotal > 1.2g
  → Possible fall detected
## 🛠️ Hardware Used
- STM32 Development Board  
- MPU6050 (Accelerometer + Gyroscope)  
- LEDs (PG13, PG14)  
- UART Interface  

---

## 💻 Software & Tools
- STM32CubeIDE  
- FreeRTOS  
- Embedded C  
- Tera Term (Serial Monitor)  

## 🧵 RTOS Task Architecture

### 🔹 Task1 – Sensor Data Output
- Reads sensor values
- Prints Ax, Ay, Az, Gx, Gy, Gz via UART
- Runs every 5 seconds

### 🔹 Task2 – Fall Detection Logic
- Calculates total acceleration
- Checks threshold condition
- Computes pitch & roll
- If fall detected:
- Toggles LED (PG14)
- Sends notification to Task3

### 🔹 Task3 – Alert Handler
- Waits for notification
- Prints: FALL DETECTED

- Toggles LED (PG13)
  
### ⏱️ Software Timer
- Runs every 20 ms
- Reads MPU6050 sensor data
## 📂 Project Structure

Core/
├── Src/
│ └── main.c
├── Inc/
Drivers/
README.md

## 🚀 How to Run

1. Clone repo:
   ```bash
   git clone https://github.com/yourusername/Fall_Detection.git

Open in STM32CubeIDE

Build project

Flash to STM32 board

Open Tera Term (115200 baud)

📸 Output Example
Ax=120 Ay=300 Az=16300 | Gx=10 Gy=5 Gz=2
...
FALL DETECTED

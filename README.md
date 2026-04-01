# 🚨 STM32-Based Fall Detection System using FreeRTOS

## 📌 Overview

This project implements a real-time fall detection system using an STM32 microcontroller integrated with FreeRTOS. The system continuously monitors motion data using an MPU6050 sensor (accelerometer + gyroscope) and detects falls based on a combination of sudden impact and orientation change.

The design focuses on real-time responsiveness, efficient multitasking, and reliable event handling using RTOS concepts.

## 🎯 Problem Statement

Detecting human falls in real time is a critical requirement in applications such as healthcare monitoring and elderly safety systems. Traditional approaches often fail to provide timely and reliable detection due to lack of real-time processing and synchronization.

## 💡 Proposed Solution

To address this, a FreeRTOS-based system is designed where multiple tasks work together to monitor motion, analyze sensor data, and trigger alerts when a fall is detected.

The system uses:

* Real-time sensor acquisition
* Threshold-based impact detection
* Orientation (tilt) analysis
* Event-driven task communication

## ⚙️ System Working

The system operates in two main stages:

### 🔹 Stage 1: Impact Detection

* Total acceleration is calculated:

  aTotal = sqrt(Ax² + Ay² + Az²) / 16384
  
* If acceleration exceeds threshold (≈1.2g), a possible fall event is detected


### 🔹 Stage 2: Orientation Analysis

* Pitch and Roll are calculated using gyroscope data
* Significant change confirms actual fall condition


## 🧵 RTOS Task Architecture

### 🔹 Task1 – Sensor Data Monitoring

* Reads MPU6050 values (Ax, Ay, Az, Gx, Gy, Gz)
* Sends data via UART
* Executes periodically (5 seconds)


### 🔹 Task2 – Fall Detection Logic

* Computes total acceleration
* Checks threshold condition
* Performs tilt analysis
* On detection:

  * Toggles LED (PG14)
  * Sends notification to Task3


### 🔹 Task3 – Alert Handler

* Waits for task notification
* Displays "FALL DETECTED" via UART
* Toggles alert LED (PG13)


### ⏱️ Software Timer

* Runs every 20 ms
* Continuously updates sensor readings


## 📊 Key Features

* Real-time motion monitoring using MPU6050
* Dual-stage fall detection (impact + orientation)
* FreeRTOS-based multitasking
* Event-driven communication using task notifications
* LED indication for alerts
* UART debugging using Tera Term


## 🛠️ Hardware Used

* STM32 Development Board
* MPU6050 Sensor
* LEDs (PG13, PG14)
* UART Interface


## 💻 Software & Tools

* STM32CubeIDE
* FreeRTOS
* Embedded C
* Tera Term


## 📂 Project Structure

Core/
├── Src/
│   └── main.c
├── Inc/
Drivers/
README.md


## 🚀 How to Run

1. Clone the repository
2. Open project in STM32CubeIDE
3. Build and flash to STM32 board
4. Open Tera Term (115200 baud)
5. Observe real-time sensor output and fall detection alerts

## 📸 Output Example

Ax=120 Ay=300 Az=16300 | Gx=10 Gy=5 Gz=2
...
FALL DETECTED

---

## 🧠 Learning Outcomes

* Practical understanding of RTOS multitasking
* Experience with real-time sensor processing
* Implementation of interrupt and timer-based systems
* Improved debugging and system design skills

## 📌 Conclusion

This project demonstrates how FreeRTOS enables efficient real-time monitoring and event handling in embedded systems. The combination of sensor data analysis and RTOS-based scheduling ensures accurate and reliable fall detection.


## 🔗 GitHub Repository

https://github.com/PallaviLakumalla/Fall_Detection_Simulator_Using_RTOS

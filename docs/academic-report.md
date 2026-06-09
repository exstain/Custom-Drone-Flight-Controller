# Custom Quadcopter Flight Controller

---

## Abstract

This project presents the design and implementation of a low-cost quadcopter flight control system based on ESP8266 and MPU6050. The system implements attitude stabilization using a PID controller and supports real-time telemetry and control via WiFi communication.

The system focuses on attitude stabilization (roll, pitch, yaw) without altitude, GPS, or magnetometer integration due to hardware limitations.

---

## 1. Introduction

Unmanned Aerial Vehicles (UAVs) require stable control systems to maintain flight attitude and ensure safe operation. This project aims to design and implement a functional flight controller using embedded systems and control theory in a real hardware environment.

The objective is to apply theoretical knowledge of control systems and embedded programming into a practical quadcopter platform.

---

## 2. System Overview

The system consists of the following components:

- ESP8266 microcontroller (main flight controller)
- MPU6050 IMU sensor (gyroscope and accelerometer)
- Electronic Speed Controllers (ESC 30A SimonK)
- Brushless DC motors
- LiPo 3S 2200mAh battery
- Custom F450 frame (carbon fiber + plywood structure)
- WiFi-based telemetry system

---

## 3. System Architecture

### 3.1 Block Diagram

<p align="center">
  <img src="docs/arsitektur-drone.jpg" width="45%">
</p>

## 4. Methodology

### 4.1 Sensor Data Acquisition

The MPU6050 sensor is used to obtain accelerometer and gyroscope data via I2C communication.

Noise reduction techniques:
- Low-pass filtering (LPF)
- Complementary filter
- MPU6050 internal DLPF (Level 3)

---

### 4.2 Attitude Estimation

The system estimates:
- Roll angle
- Pitch angle
- Yaw rate

This project does NOT include:
- GPS navigation
- Barometer altitude control
- Magnetometer heading correction

---

### 4.3 Control System (PID)

A PID controller is implemented for each axis:

- Roll PID
- Pitch PID
- Yaw PID

The controller continuously minimizes the error between desired and actual orientation.

---

### 4.4 Motor Control System

Motor speed is controlled via PWM signals to ESCs.

A motor mixing algorithm distributes control outputs across four motors.

---

### 4.5 Telemetry System

A WebSocket-based system is implemented for real-time communication.

Features:
- Live sensor data monitoring
- PID tuning
- Trim adjustment
- Throttle control
- Arm / disarm system
- Directional control input

---

## 5. Hardware Implementation

### 5.1 Frame Design

<p align="center">
  <img src="images/top-view-drone.jpeg" width="45%">
</p>

- Carbon fiber arms (23 cm × 4)
- Plywood center plates (10 cm × 10 cm × 2)
- F450-style quadcopter configuration (~45 cm diagonal)

---

### 5.2 Electronics Integration

<p align="center">
  <img src="docs/installing-motor-and-esc.jpeg" width="45%">
</p>

- ESP8266 mounted as flight controller
- MPU6050 IMU sensor
- ESCs placed at center frame
- Power distribution wiring
- 2200µF capacitor for voltage stabilization
- LiPo 3S battery mounted under frame

---

## 6. Testing and Validation

### 6.1 Pre-Flight Testing

- ESC calibration
- IMU calibration
- Motor direction verification
- System safety checks (without propellers)

---

### 6.2 Tethered Testing

- Initial PID tuning performed with drone secured
- Stability testing under controlled conditions
- Safety validation before free flight

---

### 6.3 Flight Testing

- Hover tests performed
- PID tuning refined iteratively
- Indoor and outdoor tuning adjustments applied

---

## 7. Engineering Challenges

### 7.1 Sensor Failure
A defective MPU6050 module was detected where I2C communication worked but output data was zero. The module was replaced.

---

### 7.2 Sensor Noise
Motor vibration caused unstable IMU readings. This was solved using:
- Low-pass filtering
- Complementary filtering
- MPU6050 internal DLPF

---

### 7.3 PID Timing Instability
ESP8266 loop timing caused jitter in PID execution frequency. Optimization improved timing stability.

---

### 7.4 Motor Safety Issue
A critical bug caused motor throttle spike when WiFi disconnected. A failsafe mechanism was implemented to disable outputs on connection loss.

---

## 8. Results

- Stable hover flight achieved
- Real-time telemetry system functional
- PID stabilization successfully tuned
- Safe failsafe system implemented
- Reliable attitude control using ESP8266

---

## 9. Conclusion

This project demonstrates the implementation of an embedded quadcopter flight control system using PID control and real-time sensor fusion.

Despite hardware limitations, stable attitude control was achieved using optimized firmware design and sensor filtering techniques.

---

## Keywords

UAV, Quadcopter, ESP8266, MPU6050, PID Control, Embedded Systems, Attitude Control, Real-Time Systems

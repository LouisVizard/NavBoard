<div align="center">

# 🛰️ Navigation Board PCB

**A compact, 6-layer embedded navigation platform for real-time sensor fusion and wireless telemetry**

![Status](https://img.shields.io/badge/Status-In%20Progress-yellow?style=for-the-badge)
![MCU](https://img.shields.io/badge/MCU-STM32F4CEU6-blue?style=for-the-badge&logo=stmicroelectronics)
![GNSS](https://img.shields.io/badge/GNSS-u--blox%20NEO--M9N-green?style=for-the-badge)
![PCB](https://img.shields.io/badge/PCB-6%20Layer-red?style=for-the-badge)
![Power](https://img.shields.io/badge/Power-LiPo%20%2B%20USB--C-purple?style=for-the-badge)

</div>

---

## 📌 Overview

The **Navigation Board** is a custom PCB designed as a dedicated navigation and state estimation platform. It integrates GNSS positioning, inertial sensing, and wireless communication onto a single, compact board — enabling real-time vehicle attitude estimation via a Kalman filter and live data streaming to a host computer for visualization.

> The hardware is complete and functional. Active development is now focused on firmware (EKF implementation) and the host-side Python visualization pipeline.

---

## 🖼️ Board Preview

| Isometric Top | Isometric Bottom |
|:---:|:---:|
| ![3D Render Top](https://louisvizard.github.io/Portfolio/assets/nav_3d_iso.jpg) | ![3D Render Bottom](https://louisvizard.github.io/Portfolio/assets/nav_pcb_bot_iso.jpg) |

<details>
<summary>📐 PCB Layout</summary>
<br>

![PCB Layout](https://louisvizard.github.io/Portfolio/assets/nav_layout.jpg)

</details>

<details>
<summary>🔌 Full Schematic</summary>
<br>

![Schematic](https://louisvizard.github.io/Portfolio/assets/nav_sch.jpg)

</details>

---

## ⚡ Specifications

| Parameter | Value |
|-----------|-------|
| **MCU** | STM32F4CEU6 |
| **GNSS Receiver** | u-blox NEO-M9N |
| **IMU** | 9DOF — Accelerometer + Gyroscope + Magnetometer |
| **Wireless** | nRF24L01 (2.4 GHz RF) |
| **Power Input** | Single-cell LiPo + USB-C charging |
| **PCB Stackup** | 6-layer, impedance controlled |

---

## 🏗️ System Architecture

```
┌─────────────┐     ┌─────────────────────────┐     ┌──────────────────┐     ┌──────────────────┐
│  GNSS       │     │                         │     │                  │     │                  │
│  NEO-M9N    │────▶│     STM32F4CEU6         │────▶│  nRF24L01        │────▶│  Host PC         │
│  (UART)     │     │   Kalman Filter /        │     │  2.4 GHz RF Link │     │  Python Viz      │
├─────────────┤     │   Sensor Fusion          │     │                  │     │                  │
│  IMU 9DOF   │     │                         │     │                  │     │                  │
│  (SPI/I2C)  │────▶│                         │     │                  │     │                  │
└─────────────┘     └─────────────────────────┘     └──────────────────┘     └──────────────────┘
```

**Goal:** Fuse absolute positioning (GNSS) with high-rate inertial data (IMU) using an Extended Kalman Filter to estimate real-time orientation and motion, then stream state estimates wirelessly to a host computer for visualization.

---

## 🔧 Design Details

### Hardware Integration

The board centers around the **STM32F4** MCU, which interfaces with:
- **NEO-M9N** GNSS receiver over **UART** for global positioning
- **9DOF IMU** over **SPI/I2C** for high-rate motion sensing
- **nRF24L01** providing a low-latency **2.4 GHz RF link** to stream processed state estimates to an external computer

### Power System

Powered by a single-cell **LiPo battery** with onboard **USB-C charging** circuitry. Independent regulation stages supply stable rails for:
- RF front-end
- Digital logic
- Analog sensing paths

This architecture minimizes noise coupling into sensitive IMU measurements.

### PCB Stackup

A **6-layer stackup** was chosen to provide:
- Controlled impedance for RF and GNSS antenna traces
- Solid ground referencing across all layers
- Clean power distribution

Dedicated power and ground planes minimize EMI and improve signal integrity throughout.

---

## 📊 PCB Stackup Details

The full layer stackup with impedance targets and material specifications is documented in the design spreadsheet:

📄 **[View Stackup Spreadsheet (Google Sheets)](https://docs.google.com/spreadsheets/d/1y8UFBo5hvFj5DNxBOYgQXF0sVpvpMorS/preview)**

---

## 🗺️ Roadmap

The hardware platform is complete. Next steps are focused on firmware and software:

- [ ] Implement **Extended Kalman Filter (EKF)** for GNSS + IMU fusion on STM32F4
- [ ] Tune process and measurement noise covariance matrices
- [ ] Stream state estimates over nRF24L01 RF link
- [ ] Develop **Python visualization** for real-time attitude display
- [ ] Validate filter output against ground truth measurements

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| **Hardware Design** | KiCad |
| **Firmware** | C (STM32 HAL / bare-metal) |
| **Host Software** | Python |
| **Comms Protocol** | nRF24L01 2.4 GHz |

---

## 👤 Author

**Luis Martinez**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=flat-square&logo=linkedin)](https://www.linkedin.com/in/luis-martinez-127696165)
[![GitHub](https://img.shields.io/badge/GitHub-LouisVizard-181717?style=flat-square&logo=github)](https://github.com/LouisVizard)
[![Portfolio](https://img.shields.io/badge/Portfolio-View-FF5722?style=flat-square&logo=google-chrome)](https://louisvizard.github.io/Portfolio/)

---

<div align="center">
<sub>Built with KiCad · STM32 · u-blox · nRF24L01</sub>
</div>
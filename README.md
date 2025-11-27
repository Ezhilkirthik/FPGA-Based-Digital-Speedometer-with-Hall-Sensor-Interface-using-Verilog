# 🚗 FPGA-Based Digital Speedometer with Hall Sensor Interface (Verilog + Vivado)

This repository contains a complete FPGA-based digital speedometer system implemented using **Verilog HDL**, **Vivado**, and a **Hall effect sensor**.  
The design measures speed using pulse counting, performs binary-to-BCD conversion, drives a 3-digit 7-segment display, and activates an overspeed alert LED.

---

## 📘 Project Overview

This project implements a real-time digital speedometer using:
- **Hall effect sensor** — detects wheel rotation  
- **FPGA (Basys-3, Artix-7)** — processes pulses and computes speed  
- **Verilog HDL** — modular hardware design  
- **7-segment displays** — shows speed from **0 to 255 km/h**  
- **Overspeed LED** — alerts when speed exceeds **110 km/h**  

The speed measurement is based on pulse frequency captured over a **0.5-second sampling window**, following principles explained in the documentation and research paper.

---

## 🏗️ System Architecture

### 1️⃣ Hall Sensor Input
- Detects magnetic field changes as the wheel rotates  
- Generates square-wave pulses proportional to wheel speed  

### 2️⃣ Processing Core
- **Clock Divider** – generates precise measurement intervals  
- **Pulse Counter** – counts pulses within each interval  
- **Speed Calculator** – converts pulse count → km/h  

### 3️⃣ Display Logic
- **Binary-to-BCD Converter**  
- **Seven-Segment Decoder**  
- **Display Multiplexer**  

### 4️⃣ Alert System
- Compares speed with a set threshold (110 km/h)  
- Activates **Red LED** when speed exceeds limit  

---

## 📁 Repository Contents
FPGA-Based-Digital-Speedometer-with-Hall-Sensor-Interface-using-Verilog/
│── Base Paper.pdf # Reference research paper
│── Documentation.pdf # Detailed project explanation
│── Project Writeup.pdf # Abstract, tools, objectives
│── speedometer_top.txt # Full Verilog source code
│── tb_top_speedometer_utilization.txt # Vivado synthesis/utilization report
│── LICENSE # MIT License
└── README.md # This file


---

## 🔧 Tools & Hardware Used

### Software
- Xilinx **Vivado** (Synthesis, Implementation, Simulation)  
- **ModelSim** (RTL Simulation)  
- Verilog HDL (Behavioral, Structural, Dataflow models)

### Hardware
- **Basys-3 FPGA Board** (Artix-7 XC7A35T)  
- **Hall Effect Sensor (A3144)**  
- 3-digit 7-segment display  
- Red LED for speed alert  
- Magnet + rotating wheel setup  

---

## ⚙️ How Speed is Calculated

The base paper uses the formula:
Speed (km/h) = (C × N / T) × 3.6


Where:  
- **C** = Wheel circumference  
- **N** = Number of pulses in interval  
- **T** = Sampling window (0.5 s)  

Your HDL uses an optimized integer formula:

speed = (pulse_count × 23) / 40

This matches real test outputs:
- 150 pulses → **86 km/h**  
- 200 pulses → **115 km/h**  

---

## 🖥️ Display Logic

The calculated speed is decomposed into:
- **Hundreds digit**  
- **Tens digit**  
- **Ones digit**

These are:
1. Converted to BCD  
2. Sent through a 7-segment decoder  
3. Displayed via time-multiplexing  

This ensures stable and flicker-free display.

---

## 🚨 Overspeed Alert

**Speed Limit:** 110 km/h  

When:
speed > 110
The **Red LED** turns ON.

This behavior is verified through simulation and HDL testbench outputs.

---

## 🧪 Simulation & Verification

The system is fully verified using:
- **Vivado Behavioral Simulation**
- **ModelSim waveforms**
- **HDL Testbench**

Checks performed:
- Pulse edge detection  
- Speed calculation correctness  
- BCD digit generation  
- 7-seg display patterns  
- Overspeed LED triggering  

Synthesis report shows FPGA resource use (LUTs, FFs, IOs, etc.).

---

## ✨ Features

- Real-time speed detection  
- Noise-immune Hall sensor synchronization  
- 0–255 km/h display range  
- Modular and clean Verilog design  
- Multi-digit 7-segment multiplexing  
- Overspeed indicator system  
- Fully synthesizable on Xilinx FPGA  
- Suitable for academic and hardware projects  

---

## 🔮 Future Enhancements

Potential upgrades:
- Add RPM mode  
- Display on LCD/OLED  
- Bluetooth/UART speed logging  
- Dynamic speed limit via DIP switches  
- FIR/Median filter for noisy sensors  

---

## 📄 License

This project is released under the **MIT License** — free to use, modify, and distribute with attribution.

---

## 👤 Author

**Ezhilkirthik M**  
GitHub: https://github.com/Ezhilkirthik  

---

## ⭐ Support

If you found this project useful, please consider giving the repository a **star ⭐**!


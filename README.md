# High-Precision Closed-Loop BLDC Actuator with Force-Feedback Control

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![EDA](https://img.shields.io/badge/EDA-KiCad_8.0-green.svg)
![Firmware](https://img.shields.io/badge/Firmware-C%2B%2B%20%2F%20STM32_HAL-orange.svg)
![CAD](https://img.shields.io/badge/CAD-OpenSCAD-red.svg)

This repository contains the design, simulation, firmware, and mechanical enclosure files for a high-performance, compact Brushless DC (BLDC) actuator. Designed on a NEMA 17 footprint, it integrates a 3-phase inverter power stage, absolute magnetic encoder feedback, and high-frequency Field Oriented Control (FOC) current-loop tuning for direct-drive robotic joints and haptic interfaces.

---

## Key Features

- **Field Oriented Control (FOC):** Smooth torque control using space vector modulation (SVPWM) and low-noise dual-shunt phase current sensing.
- **Embedded Electronics:** Compact 4-layer circular PCB (40mm diameter) combining power switching, current amplification, and STM32 microcontroller.
- **Parametric Mechanical Design:** Passive convection air cooling fins designed programmatically in OpenSCAD for lightweight 3D printing.
- **High-Frequency Control Loop:** Current sensing loop executes at 25 kHz inside high-priority interrupts to ensure instantaneous torque response.
- **Python Calibration GUI:** Serial telemetry dashboard to monitor speed, position, and tune PI control gains in real-time.

---

## Hardware Specifications

| Parameter | Value |
| :--- | :--- |
| **Input Supply Voltage** | 12V - 24V DC |
| **Continuous Current** | 15A (with passive cooling) |
| **Peak Current** | 30A (10-second thermal limit) |
| **Logic Voltage** | 3.3V (STM32 Internal LDO) |
| **Position Sensor** | AS5048A 14-bit Magnetic Encoder (SPI) |
| **Gate Driver** | DRV8305 with integrated Op-Amps |

---

## Directory Structure

- `/firmware`: Embedded C++ application for the STM32G474RET6 MCU.
- `/hardware`: KiCad 8.0 schematic and 4-layer layout files.
- `/mechanical`: OpenSCAD 3D design files and exported STL mounts.
- `/simulation`: LTspice switching transient circuit models and raw output data.
- `/gui`: Python monitoring dashboard.

---

## Getting Started

### 1. Build and Flash Firmware
The firmware utilizes the GCC ARM Toolchain and GNU Make.
```bash
cd firmware
make
# Flash target using STM32 CubeProgrammer or OpenOCD via ST-Link V3
openocd -f interface/stlink.cfg -f target/stm32g4x.cfg -c "program build/actuator_controller.bin verify reset exit"

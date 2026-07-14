<div align="center">

# 🚗 Real-Time Electric Vehicle Dashboard & ADAS Warning System

### Embedded Real-Time Perception, Monitoring & Driver-Assistance on STM32F103C8T6

You Tube Video Link : https://www.youtube.com/watch?v=yR-yfcYJeF8&t=1959s 

*A bare-metal embedded systems project simulating a production-style EV instrument cluster fused with an ADAS-inspired obstacle warning layer — built on Embedded C, STM32 peripherals, and a live Python telemetry dashboard.*

![Platform](https://img.shields.io/badge/Platform-STM32F103C8T6-03234B?style=for-the-badge&logo=stmicroelectronics&logoColor=white)
![Language](https://img.shields.io/badge/Firmware-Embedded%20C-00599C?style=for-the-badge&logo=c&logoColor=white)
![Dashboard](https://img.shields.io/badge/Dashboard-Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![IDE](https://img.shields.io/badge/IDE-STM32CubeIDE-2E7D32?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)

</div>

---

## 📑 Table of Contents

1. [Overview](#-overview)
2. [Motivation](#-motivation)
3. [Key Features](#-key-features)
4. [Tech Stack](#-tech-stack)
5. [Hardware Platform](#-hardware-platform)
6. [STM32 Peripherals Used](#-stm32-peripherals-used)
7. [Sensors & Driver Inputs](#-sensors--driver-inputs)
8. [System Architecture](#-system-architecture)
9. [Project Workflow](#-project-workflow)
10. [Development Journey (Module-Wise)](#-development-journey-module-wise)
11. [Working Principle](#-working-principle)
12. [Python Dashboard](#-python-dashboard)
13. [ADAS Features](#-adas-features)
14. [Fault Detection Logic](#-fault-detection-logic)
15. [Communication Flow](#-communication-flow)
16. [Repository Structure](#-repository-structure)
17. [Screenshots](#-screenshots)
18. [Demo Video](#-demo-video)
19. [Getting Started](#-getting-started)
20. [Dependencies](#-dependencies)
21. [Future Scope](#-future-scope)
22. [Learning Outcomes](#-learning-outcomes)
23. [Challenges Faced](#-challenges-faced)
24. [Project Highlights](#-project-highlights)
25. [Author](#-author)
26. [Acknowledgements](#-acknowledgements)
27. [License](#-license)

---

## 📌 Overview

This repository contains the firmware and companion dashboard for a **Real-Time Electric Vehicle (EV) Dashboard integrated with an ADAS-inspired Warning System**, developed on the **STM32F103C8T6 ("Blue Pill")** microcontroller during an embedded systems internship at **Emertxe Information Technologies**.

The system emulates the core responsibilities of a modern EV instrument cluster — acquiring driver inputs, monitoring vehicle health parameters, and surfacing safety-critical alerts — while layering in a simplified **Advanced Driver Assistance System (ADAS)** module for obstacle detection, blind-spot monitoring, and collision-time estimation. All telemetry is streamed over UART to a **Python-based virtual dashboard** that visualizes the vehicle state in real time.

The project was built to reflect how real automotive embedded systems are structured: peripheral-level sensor acquisition, deterministic timing via hardware timers, a defined communication protocol between MCU and host, and a clear separation between the perception layer (sensors), the decision layer (fault/alarm logic), and the presentation layer (dashboard).

---

## 💡 Motivation

Modern EVs are not just battery-powered cars — they are **distributed embedded systems** where dozens of microcontrollers continuously sense, compute, and communicate to keep the driver informed and safe. Two questions drove this project:

- **Can a single low-cost microcontroller (STM32F103C8T6) handle multi-sensor acquisition, real-time decision-making, and structured serial communication simultaneously — the way a production ECU would?**
- **How much of "intelligent" vehicle behavior comes down to disciplined signal acquisition, filtering, and timing, rather than complex algorithms?**

This project was built to answer both, using only the peripherals and tools available on a resource-constrained microcontroller — no external perception modules, no pre-built ADAS libraries.

---

## ✨ Key Features

| Category | Capability |
|---|---|
| 🔋 **Vehicle Telemetry** | Real-time tracking of speed, battery %, driving range, torque, and driving mode |
| 🧭 **Driver Input Monitoring** | Accelerator position, brake position, battery SOC, and motor temperature via ADC |
| 📡 **ADAS Perception Layer** | Obstacle detection, blind-spot monitoring, and Time-To-Collision (TTC) estimation |
| 🚨 **Fault & Alarm System** | Threshold-based fault detection with LED status indicators and alarm codes |
| 🖥️ **Live Python Dashboard** | Bird's-eye view visualization, speed-history graph, and system status panel |
| 🔌 **Structured UART Protocol** | Deterministic frame-based communication between firmware and host dashboard |
| 🧪 **Simulation-First Development** | Fully validated in PICSimLab + VSPE before/alongside physical hardware bring-up |

---

## 🛠 Tech Stack

| Domain | Tools / Technologies |
|---|---|
| **Programming Languages** | Embedded C, Python |
| **Microcontroller** | STM32F103C8T6 (ARM Cortex-M3, "Blue Pill") |
| **Firmware IDE** | STM32CubeIDE, STM32CubeMX |
| **Hardware Simulation** | PICSimLab |
| **Virtual Serial Link** | VSPE (Virtual Serial Port Emulator) |
| **Dashboard & Visualization** | Python (Virtual Terminal–driven telemetry dashboard) |
| **Version Control** | Git & GitHub |

---

## 🔧 Hardware Platform

**STM32F103C8T6 ("Blue Pill")**

| Spec | Detail |
|---|---|
| Core | ARM Cortex-M3 @ 72 MHz |
| Flash / SRAM | 64 KB Flash / 20 KB SRAM |
| Peripherals Used | GPIO, ADC, UART, Timers |
| Role in Project | Central acquisition + decision unit — reads sensors, evaluates fault conditions, and streams telemetry over UART |

**Sensors:** 3 × HC-SR04 Ultrasonic Distance Sensors (Front / Left / Right)

---

## ⚙️ STM32 Peripherals Used

| Peripheral | Usage in This Project |
|---|---|
| **GPIO** | Digital I/O for ultrasonic trigger/echo lines and LED status indicators |
| **ADC** | Analog acquisition of accelerator position, brake position, SOC, and motor temperature |
| **UART** | Structured serial communication of telemetry frames to the Python dashboard |
| **Timers** | Precise pulse-width timing for ultrasonic echo measurement and periodic task scheduling |

---

## 📡 Sensors & Driver Inputs

**Ultrasonic Sensing (ADAS Layer)**

| Sensor | Position | Function |
|---|---|---|
| HC-SR04 #1 | Front | Obstacle detection + Time-To-Collision (TTC) |
| HC-SR04 #2 | Left | Blind-spot monitoring |
| HC-SR04 #3 | Right | Blind-spot monitoring |

**Driver & Vehicle Inputs (ADC Channels)**

| Input | Description |
|---|---|
| Accelerator | Analog throttle position input |
| Brake | Analog brake position input |
| Battery SOC | State-of-charge simulation input |
| Motor Temperature | Thermal monitoring input for fault detection |

---

## 🏗 System Architecture

```
 ┌────────────────────────────┐
 │        Physical Layer       │
 │  HC-SR04 x3  |  Analog Pots │
 │ (Distance)   |  (Driver I/O)│
 └──────────────┬───────────────┘
                │ GPIO / ADC
                ▼
 ┌────────────────────────────────────────────┐
 │           STM32F103C8T6 (Blue Pill)          │
 │ ──────────────────────────────────────────── │
 │  • Timer-based ultrasonic echo capture        │
 │  • ADC polling for driver inputs              │
 │  • Fault detection & alarm logic              │
 │  • LED status indication (GPIO)               │
 │  • UART frame packaging                       │
 └──────────────────────┬───────────────────────┘
                        │ UART (Serial Frames)
                        ▼
 ┌────────────────────────────────────────────┐
 │        VSPE Virtual Serial Port Bridge       │
 └──────────────────────┬───────────────────────┘
                        │
                        ▼
 ┌────────────────────────────────────────────┐
 │            Python Dashboard (Host)           │
 │ ──────────────────────────────────────────── │
 │  • Speedometer & battery panel                │
 │  • ADAS bird's-eye view                       │
 │  • Speed-history graph                        │
 │  • Alarm / fault status display               │
 └────────────────────────────────────────────┘
```

---

## 🔄 Project Workflow

```
 [Power-On] 
     │
     ▼
 [Peripheral Init: GPIO / ADC / UART / Timers]
     │
     ▼
 [Acquire Ultrasonic Distances] ──▶ [Compute TTC] ──▶ [Obstacle / Blind-Spot Flags]
     │
     ▼
 [Read ADC: Accelerator, Brake, SOC, Motor Temp]
     │
     ▼
 [Evaluate Fault Conditions] ──▶ [Trigger Alarm + LED Indicator if Fault]
     │
     ▼
 [Package Telemetry Frame] ──▶ [Transmit via UART]
     │
     ▼
 [Python Dashboard Receives, Parses & Renders Live Data]
     │
     ▼
 [Loop — Real-Time, Continuous Cycle]
```

---

## 🧩 Development Journey (Module-Wise)

| Phase | Module | Description |
|---|---|---|
| **1** | GPIO Bring-Up | Configured digital I/O for ultrasonic trigger/echo pins and LED indicators |
| **2** | Timer-Based Ranging | Implemented microsecond-precision pulse timing to compute distance from HC-SR04 echo width |
| **3** | ADC Integration | Configured and calibrated ADC channels for accelerator, brake, SOC, and motor temperature |
| **4** | UART Protocol Design | Defined a structured serial frame format for reliable MCU → host telemetry |
| **5** | Fault & Alarm Logic | Implemented threshold-based fault detection with LED and alarm-code signaling |
| **6** | ADAS Layer | Added obstacle detection, blind-spot monitoring, and TTC computation from the three ultrasonic sensors |
| **7** | Hardware Simulation | Validated the complete firmware behavior in PICSimLab prior to/alongside physical testing |
| **8** | Virtual Serial Bridge | Set up VSPE to route UART data from the simulated/physical MCU to the Python host |
| **9** | Python Dashboard | Built the live visualization layer — speedometer, battery, ADAS bird's-eye view, speed-history graph |
| **10** | Integration & Validation | Verified end-to-end data flow from sensor acquisition to dashboard rendering under continuous operation |

---

## ⚡ Working Principle

1. The STM32F103C8T6 continuously triggers each HC-SR04 sensor and measures echo pulse width using hardware timers to compute distance.
2. In parallel, the ADC polls accelerator, brake, battery SOC, and motor temperature inputs.
3. Measured distances feed a **Time-To-Collision (TTC)** calculation and blind-spot logic; out-of-range readings raise obstacle/blind-spot flags.
4. Driver and vehicle parameters are checked against safety thresholds; violations trigger **fault flags**, LED indicators, and alarm codes.
5. All computed values are packaged into a structured frame and transmitted over **UART**.
6. A **VSPE virtual serial bridge** routes this UART stream to the host machine.
7. The **Python dashboard** parses each frame and updates the UI in real time — speed, range, torque, alarm/fault status, and the ADAS bird's-eye view.

---

## 🖥 Python Dashboard

The host-side dashboard renders live telemetry received over the virtual serial link:

- **Speedometer** — real-time vehicle speed
- **Battery Percentage & Driving Range**
- **Driving Mode & Torque**
- **Accelerator / Brake Position**
- **Motor Temperature**
- **Alarm Status & Fault Codes**
- **Signal Status**
- **ADAS Bird's-Eye View** — front / left / right distance visualization
- **Time-To-Collision (TTC)** readout
- **Speed-History Graph** — rolling plot of vehicle speed over time

---

## 🛡 ADAS Features

| Feature | Description |
|---|---|
| **Obstacle Detection** | Front ultrasonic sensor flags obstacles within a defined safety distance |
| **Blind-Spot Detection** | Left/right sensors flag objects in the vehicle's blind-spot zones |
| **Collision Warning** | Alarm triggered when TTC drops below a critical threshold |
| **Bird's-Eye Visualization** | Dashboard renders relative object positions around the vehicle |

---

## 🚨 Fault Detection Logic

- Each critical parameter (motor temperature, battery SOC, sensor validity) is checked against a defined safe operating range on every cycle.
- A parameter outside its safe range sets a corresponding **fault flag** and a unique **fault code**.
- Active faults immediately trigger:
  - An **LED status indicator** on the hardware
  - An **alarm state** transmitted to the dashboard
  - A visible **fault code** on the Python UI
- This mirrors how automotive ECUs use diagnostic trouble codes (DTCs) to surface hardware/sensor issues without halting the system.

---

## 🔗 Communication Flow

```
STM32F103C8T6  ──▶  UART (TX)  ──▶  VSPE Virtual Port  ──▶  Python Dashboard (RX)
      ▲                                                              │
      └──────────────────── Structured Telemetry Frame ─────────────┘
```

Each frame carries: `speed | battery% | range | torque | accel | brake | motorTemp | frontDist | leftDist | rightDist | TTC | alarmStatus | faultCode`

---

## 📂 Repository Structure

```
EV-Dashboard-ADAS-STM32/
│
├── Firmware/
│   ├── Core/
│   │   ├── Src/                # Main application & peripheral source files
│   │   └── Inc/                # Header files
│   ├── Drivers/                # STM32 HAL / CMSIS drivers
│   └── EV_Dashboard.ioc         # STM32CubeMX configuration
│
├── Dashboard/
│   ├── dashboard.py            # Python dashboard application
│   ├── serial_handler.py       # UART frame parsing logic
│   └── requirements.txt        # Python dependencies
│
├── Simulation/
│   └── PICSimLab_Config/       # Hardware simulation setup files
│
├── Docs/
│   ├── architecture-diagram.png
│   ├── workflow-diagram.png
│   └── screenshots/
│
├── README.md
└── LICENSE
```

---



## 🚀 Getting Started

### Prerequisites

- STM32CubeIDE (or STM32CubeMX + preferred toolchain)
- Python 3.9+
- PICSimLab (for hardware-free simulation)
- VSPE (Virtual Serial Port Emulator)
- ST-Link or USB-to-Serial adapter (for physical hardware)

### Installation

```bash
# Clone the repository
git clone https://github.com/mranantsaxena/EV-Dashboard-ADAS-STM32.git
cd EV-Dashboard-ADAS-STM32

# Set up the Python dashboard environment
cd Dashboard
pip install -r requirements.txt
```

### How to Run

**1. Flash the Firmware**
```bash
# Open Firmware/EV_Dashboard.ioc in STM32CubeIDE
# Build and flash to STM32F103C8T6 via ST-Link
```

**2. Set Up the Virtual Serial Bridge (for simulation)**
```bash
# Launch VSPE and create a paired virtual COM port
# Configure PICSimLab to use one end of the pair
```

**3. Launch the Dashboard**
```bash
cd Dashboard
python dashboard.py --port COMx --baud 115200
```

The dashboard window should open and begin displaying live telemetry once the firmware starts transmitting.

---

## 📦 Dependencies

| Component | Requirement |
|---|---|
| STM32CubeIDE | Latest stable release |
| Python | 3.9 or higher |
| pyserial | For UART communication with the dashboard |
| matplotlib | For the live speed-history graph |
| PICSimLab | For hardware-free firmware validation |
| VSPE | For virtual COM port bridging |

---

## 🔭 Future Scope

- Replace ultrasonic-only perception with a camera + computer vision module for richer obstacle classification
- Migrate UART link to CAN bus to better reflect real automotive network architecture
- Add an RTOS layer (FreeRTOS) for formal task scheduling and priority-based fault handling
- Log telemetry to persistent storage (SD card) for post-drive diagnostics
- Extend the fault system to support configurable, EEPROM-stored threshold profiles

---

## 🎓 Learning Outcomes

- Practical experience configuring and debugging STM32 GPIO, ADC, UART, and Timer peripherals from the register/HAL level
- Designing a structured serial communication protocol between an MCU and a host application
- Translating sensor-level signals (ultrasonic echo timing, analog voltages) into meaningful, real-time decisions
- Building a fault-detection and alarm framework similar in principle to automotive diagnostic systems
- End-to-end system thinking — connecting firmware, simulation tools, and a live visualization layer into one working pipeline

---

## 🧗 Challenges Faced

- **Timing precision:** Achieving reliable microsecond-level echo timing for the HC-SR04 sensors required careful timer configuration to avoid distance-measurement drift.
- **Simultaneous peripheral load:** Coordinating ADC polling, timer-based ranging, and UART transmission within the same real-time loop without blocking any single task.
- **Communication reliability:** Ensuring the UART frame format stayed synchronized between firmware and dashboard, especially across the VSPE virtual serial bridge.
- **Simulation-to-hardware parity:** Validating that behavior observed in PICSimLab translated consistently to expected real-hardware operation.

---

## 🌟 Project Highlights

- Built entirely on **bare-metal-level STM32 peripheral programming** — no external ADAS libraries used
- Demonstrates a **complete embedded pipeline**: sensing → decision logic → communication → visualization
- Designed with **automotive-style fault handling** (LED indicators + fault codes), not just simple print statements
- Fully **simulation-validated** using PICSimLab and VSPE before/alongside hardware testing

---

## 👤 Author

**Anant Saxena**
Embedded Systems Enthusiast | B.Tech ECE, Hemvati Nandan Bahuguna Garhwal University

[![GitHub](https://img.shields.io/badge/GitHub-mranantsaxena-181717?style=flat&logo=github)](https://github.com/mranantsaxena)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/anant-saxena-)
[![Email](https://img.shields.io/badge/Email-Contact-D14836?style=flat&logo=gmail&logoColor=white)](mailto:mranantsaxena@gmail.com)

---

## 🙏 Acknowledgements

- **Emertxe Information Technologies** — for the internship structure and mentorship that shaped this project
- The **STM32 developer community** for extensive HAL and peripheral documentation
- Open-source tools **PICSimLab** and **VSPE**, which made hardware-free validation possible

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

<div align="center">

### If this project helped you understand embedded real-time systems, consider giving it a ⭐

**Built with precision, timers, and a lot of UART debugging.**

</div>

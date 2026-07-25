# PMSM Edge Predictive Maintenance

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Hardware](https://img.shields.io/badge/Hardware-STM32-003594?logo=stmicroelectronics)](#)
[![Simulation](https://img.shields.io/badge/Simulation-MATLAB%2FSimulink-orange)](#)

> **Status:** Work in Progress<br>
> **Conference Abstract Project:** *10th DeKUT International Conference on Science, Technology, Innovation and Entrepreneurship (STIE 2026)*


## Project Intent

Electric Vehicle (EV) powertrains depend heavily on **Permanent Magnet Synchronous Motors (PMSMs)**. Undetected degradation in stator windings, permanent magnet strength, or motor bearings can lead to severe system failure, unexpected downtime, and high repair costs.

The objective of **`pmsm-edge-predictive-maintenance`** is to develop a Software-in-the-Loop (SIL) and Hardware-in-the-Loop (HIL) predictive maintenance framework. This project aims to bridge physics-based simulation and embedded machine learning by combining:

1. A **MATLAB/Simulink Digital Twin** of a PMSM drivetrain for dynamic fault modeling.
2. An **STM32 Edge Node** running real-time signal processing (FFT via CMSIS-DSP) and TinyML inference for local fault classification.
3. A **Federated Learning Network** architecture to allow smart EV fleets to share global model improvements while maintaining local data privacy.


## Planned System Architecture

| Stage | System Component | Core Functions & Features | Interface / Data Output |
| :--- | :--- | :--- | :--- |
| **1** | **Digital Twin**<br>*(MATLAB / Simulink)* | • PMSM Drivetrain with Field-Oriented Control (FOC)<br>• Synthetic Fault Injection (Stator Shorts, Demagnetization, Bearing Noise) | **UDP / MQTT Streams**<br>*(High-speed phase currents & vibration telemetry)* |
| **2** | **Telemetry & Gateway Middleware**<br>*(Node-RED)* | • Packet parsing, protocol translation, and serial bridging<br>• Real-time web dashboard for live waveforms and fault alerts<br>• Edge-to-server payload orchestration | **Serial / UART / CAN**<br>*(Formatted telemetry to MCU)*<br><br>**MQTT / HTTP**<br>*(Model weight payloads to server)* |
| **3** | **Edge Processing Node**<br>*(STM32 MCU)* | • Spectral Feature Extraction (CMSIS-DSP FFT)<br>• Real-Time Fault Classification (TinyML via X-CUBE-AI) | **Local Model Updates**<br>*(Local model weights only)* |
| **4** | **Federated Aggregation Server**<br>*(PyTorch / Flower)* | • Global Model Weight Averaging (FedAvg / FedProx)<br>• Decentralized fleet intelligence updates | **Updated Global Weights**<br>*(Broadcast back to Edge Nodes via Node-RED)* |


## Project Roadmap

- [ ] **Phase 1: Digital Twin Setup**
  - [ ] Build baseline dynamic PMSM drive model in MATLAB/Simulink using FOC.
  - [ ] Implement mathematical fault-injection blocks (stator short circuit, demagnetization, bearing wear).
- [ ] **Phase 2: Signal Processing & Edge AI**
  - [ ] Extract time/frequency domain features (FFT) from simulated sensor data.
  - [ ] Train and quantize a lightweight anomaly/classification model for edge deployment.
  - [ ] Deploy model to an STM32 microcontroller using CMSIS-DSP and X-CUBE-AI.
- [ ] **Phase 3: SIL/HIL Integration & Federated Learning**
  - [ ] Stream simulated telemetry from MATLAB to STM32 over serial interface.
  - [ ] Set up a basic Federated Learning architecture (PyTorch/Flower) for privacy-preserving weight aggregation.
- [ ] **Phase 4: Conference Deliverables & Documentation**
  - [ ] Document accuracy metrics and memory/compute performance on the STM32.
  - [ ] Prepare presentation for STIE 2026.


## Planned Tools & Tech Stack

* **Simulation:** MATLAB, Simulink, Simscape Electrical.
* **Embedded Hardware & Firmware:** STM32 (Arm Cortex-M), C/C++, STM32CubeIDE, CMSIS-DSP, X-CUBE-AI.
* **Machine Learning:** TensorFlow / PyTorch, TensorFlow Lite for Microcontrollers.
* **Federated Learning:** Flower Framework / PyTorch.


## License

This project is licensed under the **Apache License 2.0** — see the [LICENSE](LICENSE) file for details.

## Author

* **THOITHI JOAN MUMBI**

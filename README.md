# ADP201P4 Signal Processing Module 🛰️

Technical documentation and hardware architecture specifications for the **ADP201P4** digital signal processing (DSP) and data acquisition carrier board, developed by "Instrumental Systems" (Insys).

[Читать документацию на русском языке (README.ru.md)](./README.ru.md)

---

## 📌 Overview

**ADP201P4** is a high-performance, multi-processor PCI carrier board designed for high-speed data acquisition, synthesis, and digital signal processing. Built upon a cluster of four **Analog Devices ADSP-TS201S (TigerSHARC)** DSPs, it serves as a robust base for high-speed mezzanine submodules (ADCs/DACs) via the proprietary progressive **ADMPRO** interface.

The hardware is optimized for tight inter-module synchronization, allowing multiple carrier boards to be cascaded into a unified, distributed computing network for radar, software-defined radio (SDR), and telecom applications.

---

## 🏗️ Hardware Architecture & Features

### 🖥️ Processing Cluster
* **DSPs:** 4× ADSP-TS201S (TigerSHARC) operating at **500 / 600 MHz**.
* **Memory Architecture:** Individual **16Mx64 SDRAM** banks for each processor.
* **Non-Volatile Storage:** Common **4Mx8 Flash** memory mapped to DSP1.
* **Inter-Processor Links:** DSPs are interconnected via internal high-speed link ports, enabling low-latency mesh communication.

### 🎛️ ADMPRO Mezzanine Interface
* **Control Core:** Managed by a high-gate-count **Xilinx Spartan-3 FPGA** (`XC3S400` or `XC3S1500`).
* **SRAM:** Local **2Mx18 SSRAM / SBSRAM** bank dedicated to the FPGA.
* **Host Coupling:** Connected to the host system via a dedicated **PCI Bus Controller** and a custom **HOST FPGA** containing deep `DPRAM` and dual channel `FIFO` buffers (`1024x32`).

---

## 🗂️ Documentation Structure

The repository is broken down into modular technical specifications:

1. 📑 **[Introduction & Module Family](./docs/01_introduction.md)** — Core terminology, notation conventions, and a comparative matrix of the ADP201 hardware family.
2. 🔀 **[System Architecture](./docs/02_architecture.md)** — DSP clustering, memory mapping, and the HOST FPGA data transmission paths.
3. 🛠️ **[ADMPRO Interface Spec](./docs/03_adm_interface.md)** — Comprehensive analysis of FPGA Tetrad registers, start synchronization comparators, and IPN voltage rails.
4. 🔌 **[Connector & Pinout Maps](./docs/04_connectors.md)** — Detailed pinout tables for `SYNX` (Inter-module sync) and `PIOX` (Digital I/O port).

---

## 🔌 External Interface Checklist

| Interface | Connector Type | Mode / Standard | Purpose |
| :--- | :---: | :---: | :--- |
| **Link Ports** | 4× External Ports | TigerSHARC Link (3.3V) | Inter-board multi-module networking |
| **SYNX** | AMPMODU System 50-20 | TTL / Inter-board | Hard real-time Master/Slave synchronization |
| **SDX** | LEMO-SR (Coaxial) | 50 Ω / 10 kΩ | External sampling/trigger synchronization |
| **PIOX** | AMPMODU System 50-34 | LVTTL / LVDS | General-purpose digital input/output (GPIO) |
| **JTAG-DSP** | Header | IEEE 1149.1 | Multi-processor debugging via EMU-AD |
| **JTAG-PLD** | Header | Xilinx/Altera | HOST and ADM FPGA in-system programming (ISP) |

---

## 💻 Development & Software Ecosystem

The board is fully supported by the **Deasy Tools** SDK and features standard driver layers:
* **BARDY:** Core hardware management and configuration library.
* **ISVI:** Graphical environment for real-time visualization of ADC/DAC data streams.
* **TPROG / RSTBRD:** Command-line utilities for FPGA bitstream deployment and target state resets.


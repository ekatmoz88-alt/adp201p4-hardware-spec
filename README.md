# ADP201P4 Signal Processing Module 🛰️

Technical documentation and hardware architecture specifications for the **ADP201P4** digital signal processing (DSP) and data acquisition carrier board, developed by "Instrumental Systems" (Insys).

[Читать документацию на русском языке (README.ru.md)](./README.ru.md)

---

## 📌 Overview

**ADP201P4** is a high-performance, multi-processor PCI carrier board designed for high-speed data acquisition, synthesis, and digital signal processing, featuring four **Analog Devices ADSP-TS201S (TigerSHARC)** DSPs and the **ADMPRO** interface.

---

## 🏗️ Hardware Architecture & Features

* **Processing Cluster:** 4× ADSP-TS201S (TigerSHARC) at 500/600 MHz with individual 16Mx64 SDRAM banks and shared Flash memory.
* **ADMPRO Mezzanine Interface:** Controlled by a Xilinx Spartan-3 FPGA with local SSRAM and a dedicated PCI Bus Controller with HOST FPGA data buffers.

---

## 🗂️ Documentation Structure

The repository is broken down into modular technical specifications:

* 📑 **[Introduction & Module Family](./01_introduction.md)** — Core terminology and hardware family matrix.
* 🔀 **[System Architecture](./02_architecture.md)** — DSP clustering and memory mapping.
* 🛠️ **[ADMPRO Interface Spec](./03_adm_interface.md)** — FPGA registers and synchronization.
* 🔌 **[Connector & Pinout Maps](./04_connectors.md)** — Pinout tables for SYNX and PIOX.

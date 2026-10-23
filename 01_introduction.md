# Introduction & ADP201 Module Family

This document provides core terminology, notation conventions, and a comparative overview of the ADP201 hardware family developed by "Instrumental Systems".

## 📝 Notation Conventions

* **Hexadecimal Values:** Prefixed with `0x` (e.g., `0x0`, `0xFFFF`), aligned with C-language standards.
* **Register Bit Fields:** Represented as `REGISTER[FIELD]`. For example:
  * `CSR[GIE]` — GIE bit inside the CSR register.
  * `HPIA[31:2]` — Bits 31 to 2 inside the HPIA register.
  * `0x01940000[2]` — Bit 2 in the register located at address `0x01940000`.

## 📘 Core Terminology

* **Carrier (Base) Module:** A primary board designed to accommodate mezzanine daughterboards (submodules).
* **Submodule:** A functional mezzanine card (e.g., ADC/DAC analog I/O) installed onto the carrier module.
* **Tetrad:** A logical group of **four configuration registers** implemented within the ADM FPGA.
* **Register Block:** A cluster of **32 hardware registers** implemented within the HOST FPGA.
* **'TS201:** Shorthand reference to the **ADSP-TS201S TigerSHARC** digital signal processor from Analog Devices.

---

## 📊 The ADP201 Hardware Family Matrix

The family includes several variants tailored for distinct throughput requirements, computational densities, and bus form-factors:

| Module Name | System Bus | 'TS201 DSP Count | External Link Ports | ADM Interfaces | ADM FPGA Base | Key Features |
| :--- | :---: | :---: | :---: | :---: | :--- | :--- |
| **ADP201PCI** | PCI | **1** | 2 | 1 | Spartan-3 | Core/baseline model of the family. |
| **ADP201P1** | PCI | **1** | 2 | 1 | **Virtex-4** | Equipped with an extended digital I/O port. |
| **ADP201P4** | PCI | **4** | **4** | 1 | Spartan-3 | High-density cluster (1 link port per DSP exposed). |
| **ADP201cP5** | CompactPCI | **5** | *N/A* | **2** | *N/A* | **6U Form-Factor** with dual mezzanine slots. |

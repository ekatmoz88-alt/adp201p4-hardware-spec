# ADP201P4 Signal Processing Module

Source-based technical documentation for the ADP201P4 signal-processing module. This repository is an independently structured documentation sample based on the manual **ADP201P4 Signal Processing Module — Technical Description and Operating Manual**, document **СКУЮ.467459.033 РЭ**.

[Русская версия](./README.ru.md)

## Module overview

ADP201P4 is a PCI-based signal-processing module built around four Analog Devices **ADSP-TS201S (TigerSHARC)** processors. The manual describes its use for signal acquisition and digital signal processing, connection of ADM daughter modules, and cooperation with other ADP201 modules.

## Verified hardware facts

- **DSPs:** four ADSP-TS201S processors; 500 MHz / 600 MHz variants.
- **System bus clock:** 100 MHz.
- **Local memory:** four separate SDRAM banks, 128 MB per processor.
- **Flash:** 4 MB is listed in the module technical-data table; the processor-node description gives a 2–4 MB range. The exact configuration should be checked against the particular board.
- **Host interface:** 64-bit PCI, 66 MHz.
- **External TigerSHARC links:** four, one from each processor.
- **ADM FPGA:** Xilinx Spartan-3 XC3S400-5FG456 or XC3S1500-5FG456.
- **PIOX:** 16-bit LVTTL or 8-bit LVDS data interface, depending on board implementation.

## Documentation modules

1. [Introduction and ADP201 family](./01_introduction.md)
2. [System architecture](./02_architecture.md)
3. [ADM interface](./03_adm_interface.md)
4. [External connectors](./04_connectors.md)

## Scope and source notes

The documentation distinguishes facts stated in the ADP201P4 manual from details that require companion documents, firmware specifications, board revisions, or hardware inspection. It does not assume a particular ADM daughterboard, firmware implementation, HOST FPGA register map, or optional memory configuration.

The source manual contains a few inconsistent names and editorial errors. These are not silently normalized where they could affect technical meaning. This portfolio sample is a structured, rewritten reference; it is not a reproduction of the source manual.

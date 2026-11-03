# ADP201P4 System Architecture

This page summarizes the architecture described in sections 2.3–2.5 and 2.8 of the ADP201P4 operating manual.

## DSP subsystem

The module contains four processor nodes based on the **Analog Devices ADSP-TS201S (TigerSHARC)**.

| Resource | Manual description |
|---|---|
| Processor count | 4 |
| Processor clock | 500 MHz / 600 MHz variants |
| System bus clock | 100 MHz |
| SDRAM | One 128 MB bank per processor |
| Flash | 4 MB in the technical-data table; 2–4 MB in the processor-node description |

Each processor has access to its own SDRAM bank (MSD0). The manual states that SDRAM must be initialized before first use; the software utility function identified for this purpose is autoSDRAM().

## Processor and FPGA connections

The manual explicitly identifies these connections:

- Processor **P1** is connected to the **HOST FPGA**.
- Processor **P2** is connected to the **ADM FPGA**.
- The four DSPs communicate through TigerSHARC link ports.
- Four external link ports are provided, one from each processor.

The ADM FPGA may also be connected to processors P2, P3, and P4 through link ports when the **XC3S1500** device is installed. The manual notes that this capability is not implemented in the standard ADM FPGA firmware.

The manual does not describe the processor interconnect as a generic mesh. Refer to the board block diagram and the link-port diagram in the source documentation for the actual topology.

## HOST subsystem

The HOST FPGA provides programmable resources used by the host computer and DSP software:

- dual-port memory;
- FIFO buffers;
- semaphores;
- host-side control registers;
- DSP-side control registers.

The ADP201P4 manual refers readers to separate HOST FPGA documentation and a firmware register specification for implementation details. Consequently, this page does not assign unverified capacities or dimensions to the DPRAM and FIFO resources.

## Boot and program loading

According to the manual:

- P1 can be loaded from the HOST computer, Flash, an external link port, or JTAG.
- The BOOT jumper selects the initial boot mode after reset.
- P2, P3, and P4 can be loaded through a link port or JTAG.
- The Deasy Tools loader supports synchronized startup across processors on the module and across ADP201 modules connected through SYNX.

The manual describes a Flash-resident bootstrap program that can configure the ADM FPGA and then transfer control to link-port loading. Exact behavior depends on the board's Flash contents and configuration.

## Inter-module synchronization

The SYNX connector combines ADM synchronization signals (RDY0, RDY1, SYNC0, START_EN, START, ENCODE) with processor-subsystem signals (PINT0#, PINT1#, PINT2#, PRES#). The former are controlled through the ADM FPGA; the latter through the HOST FPGA.

The BARDY library provides the BRD_load() and BRD_start() functions for coordinated loading and startup. The manual warns that programs must be loaded on every module connected through SYNX before synchronized startup.

## Software environment

The manual identifies **VisualDSP++ 4.0** and **Deasy Tools** as the software environment for developing and loading DSP programs. These are historical toolchain references from the source manual, not claims about current vendor support.

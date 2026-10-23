# System Architecture & Processing Cluster

The internal architecture of the **ADP201P4** module features a tightly coupled high-performance processing cluster integrated with high-speed local memories and custom FPGA-driven data routing paths.

## 🖥️ DSP Processing Cluster & Memory Mapping

The board hosts **four independent ADSP-TS201S (TigerSHARC)** processors running at **500 / 600 MHz**, organized into a unified mesh network:
* **Local RAM:** Each individual processor (Processor 1 through 4) is equipped with a dedicated **16Mx64 SDRAM** bank for real-time signal processing algorithms.
* **Non-Volatile Boot Storage:** A shared **4Mx8 Flash memory** is mapped directly onto the memory space of **Processor 1 (P1)**.
* **Inter-Board Links:** Each DSP exposes exactly one TigerSHARC Link Port to the external world via front-panel headers (**1-Link3, 2-Link3, 3-Link3, and 4-Link3**), facilitating seamless multi-board cascading.

## 🔀 Host Interfacing and Data Transmission Paths

Data transfer between the processing cluster and the Host PC's system PCI bus is mediated by a multi-stage hardware architecture:

1. **PCI Bus Controller:** Handles physical signaling and protocol alignment with the Host PC's PCI bus.
2. **HOST FPGA:** Acts as the primary data orchestrator and contains deep hardware buffers to decouple high-speed DSP operations from bus latency:
   * **DPRAM (4096x32):** Dual-Port RAM for fast shared control registers and state flags.
   * **FIFO 1 & FIFO 2 (1024x32 each):** Dual independent, unidirectional First-In-First-Out queues that stream high-speed ADC/DAC sample blocks to and from the host memory.
3. **Cluster Interconnect:** The HOST FPGA links directly to the DSP cluster using a dedicated high-speed link interface connected to **Processor 1 (1-Link0)**.

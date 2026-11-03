# ADMPRO Interface and ADM FPGA

The ADM FPGA provides hardware control of the mezzanine ADM submodule, supports digital data input and output, and implements inter-module synchronization. The actual functions and signal-processing logic depend on the FPGA configuration loaded at runtime.

## FPGA variants

The ADP201P4 manual lists two Xilinx Spartan-3 devices:

- XC3S400-5FG456 — baseline variant;
- XC3S1500-5FG456 — expanded variant.

The loaded FPGA configuration determines the implemented functions. The manual states that configuration can be loaded from the HOST computer or from processor P1.

## Register architecture and tetrads

The ADM FPGA logic is divided into functional register groups called **tetrads** (groups of four registers). The manual identifies two groups:

- **MAIN:** manages shared ADM interface resources, including hardware interrupt requests (IRQ) and direct memory access (DMA) requests.
- **ADMxxx:** provides control for the installed submodule.

The ADM FPGA registers are located in the address space selected by strobe MS1 of processor P2. The manual lists the following tetrad registers:

| Register index | Name | Description in the manual |
|---:|---|---|
| 0 | STATUS | Status register |
| 1 | DATA | Data register |
| 2 | IND_ADR | Indirect address register |
| 3 | IND_DATA | Indirect data register |

## Functional subsystems

### Start synchronization

The start-synchronization unit contains two comparators and a multiplexer. The multiplexer selects the signal sources for the comparator inputs:

| Mode | Comparator 0 | Comparator 1 |
|---:|---|---|
| 0 | EXTST | SDX |
| 1 | CH0 | SDX |
| 2 | CH1 | SDX |
| 3 | CH0 | CH0 |

The manual describes EXTST as an external-start input on the submodule, CH0 and CH1 as ADC channel signals, and SDX as the signal from the SDX connector. The physical meaning and source of EXTST, CH0 and CH1 can differ between ADM submodules.

### Programmable voltage source

The programmable voltage source provides eight channels. Channels 1 and 2 set the thresholds for comparators 0 and 1. The remaining channels are passed to the submodule; their use depends on that submodule. Jumpers JE0 and JE1 can route channels 1 and 2 to the submodule instead of the comparators.

### PIOX digital I/O

The PIOX connector provides a configurable digital I/O port. The electrical mode depends on the installed buffer and the loaded ADM FPGA configuration.

### LVTTL mode — 74ALVCH16245DGG

LVTTL is a single-ended signaling mode. The port exposes two independent 8-bit data buses, `PIO[15..8]` and `PIO[7..0]`, each configurable for input or output.

The standard firmware assigns these control signals:

| Signal | Direction | Function |
|---|---|---|
| `PIO_WR` | Output | Write strobe |
| `PIO_RD` | Output | Read strobe |
| `ACK_WR` | Input | Acknowledgement that the external device has completed the write |
| `ACK_RD` | Input | Acknowledgement that the external device has completed the read |

### LVDS mode — SN65LVDM1677DGG

LVDS is a differential high-speed signaling mode. The port is reconfigured as:

- one 8-bit differential data bus;
- one differential LVDS control input;
- one differential LVDS control output;
- one LVTTL control input and one LVTTL control output, available for auxiliary handshake protocols.

The connector pin table identifies the differential data lines as `PIO_P[7..0]` and `PIO_N[7..0]`, the differential control input as `CIN_P/CIN_N`, and the differential control output as `COUT_P/COUT_N`. The LVTTL control lines are `ACK_RD` (input) and `PIO_WR` (output).

Refer to the connector page for the pin assignments. Signal roles and direction are described for the documented standard firmware; verify the actual loaded FPGA configuration before integrating a specific ADM submodule.

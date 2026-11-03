# ADM Interface and ADM FPGA

The ADM FPGA controls the ADM submodule, supports data transfer to and from the submodule, and provides inter-module synchronization functions.

## FPGA variants

The ADP201P4 manual lists two Xilinx Spartan-3 devices:

- XC3S400-5FG456 — baseline variant;
- XC3S1500-5FG456 — expanded variant.

The loaded FPGA configuration determines the implemented functions. The manual states that configuration can be loaded from the HOST computer or from processor P1.

## Register groups

The ADM FPGA contains functional register groups called **tetrads**. The manual identifies two groups:

- **MAIN:** manages shared ADM interface resources, including interrupt requests (IRQ) and DMA requests (DRQ).
- **ADMxxx:** provides control for the installed submodule.

The ADM FPGA registers are located in the address space selected by strobe MS1 of processor P2. The manual lists the following tetrad registers:

| Register index | Name | Description in the manual |
|---:|---|---|
| 0 | STATUS | Status register |
| 1 | DATA | Data register |
| 2 | IND_ADR | Indirect address register |
| 3 | IND_DATA | Indirect data register |

## Start synchronization

The start-synchronization unit contains two comparators and a multiplexer. The multiplexer selects the signal sources for the comparator inputs:

| Mode | Comparator 0 | Comparator 1 |
|---:|---|---|
| 0 | EXTST | SDX |
| 1 | CH0 | SDX |
| 2 | CH1 | SDX |
| 3 | CH0 | CH0 |

The manual describes EXTST as an external-start input on the submodule, CH0 and CH1 as ADC channel signals, and SDX as the signal from the SDX connector. The physical meaning and source of EXTST, CH0 and CH1 can differ between ADM submodules.

## Programmable voltage source

The programmable voltage source provides eight channels. Channels 1 and 2 set the thresholds for comparators 0 and 1. The remaining channels are passed to the submodule; their use depends on that submodule. Jumpers JE0 and JE1 can route channels 1 and 2 to the submodule instead of the comparators.

## PIOX digital I/O

The PIOX connector provides a digital I/O port. The ADM FPGA must be configured before the port can be used. The electrical mode depends on the installed buffer:

- **LVTTL:** buffer 74ALVCH16245DGG; two independently configurable 8-bit data buses, PIO[15..8] and PIO[7..0]. The documented control signals are PIO_RD, PIO_WR, ACK_WR and ACK_RD.
- **LVDS:** buffer SN65LVDM1677DGG; six differential data pairs PIO_P[7..0] / PIO_N[7..0] are not described: the manual specifies eight differential data pairs? The connector pin table lists PIO_P[7..0] and PIO_N[7..0] as eight numbered pairs, plus differential input CIN_P/CIN_N and output COUT_P/COUT_N. PIO_WR and ACK_RD remain LVTTL signals through a 74ALVCH16245DGG buffer.

Refer to the connector page for the source-based pin assignments. The ADM manual also notes that FPGA functionality depends on the loaded firmware; do not assume every optional capability is present in a standard configuration.

# Introduction & ADP201 Module Family

This document summarizes notation, terminology and the ADP201 family information listed in the ADP201P4 technical description and operating manual (СКУЮ.467459.033 РЭ).

## Notation conventions

- Hexadecimal values use the 0x prefix (for example, 0x0 and 0xFFFF).
- Register bit fields use the form REGISTER[FIELD]. Examples from the manual include CSR[GIE], HPIA[31:2] and 0x01940000[2].

## Core terminology

- **Base module:** a board that accepts a daughterboard (submodule).
- **Submodule:** a board installed on the base module.
- **DSP / ЦОС processor:** the signal-processing processor on the module.
- **Tetrad:** a group of four registers implemented in the ADM FPGA.
- **Register block:** a group of 32 registers implemented in the HOST FPGA.
- **'TS201:** shorthand used by the manual for the ADSP-TS201S processor.
- **HOST PC:** the computer in which the DSP module is installed.

## ADP201 family as listed in the source manual

| Module | Bus | DSP count | External link ports | ADM interfaces | FPGA family | Source-manual note |
|---|---|---:|---:|---:|---|---|
| ADP201PCI | PCI | 1 | 2 | 1 | Spartan-3 | Main family model |
| ADP201P1 | PCI | 1 | 2 | 1 | Virtex-4 | Extended digital I/O port |
| ADP201P4 | PCI | 4 | 4 | 1 | Spartan-3 | One external link port per DSP |
| ADP201cP5 | CompactPCI | 5 | Not specified | 2 | Not specified | 6U form factor |

The source manual does not provide link-port or FPGA-family values for ADP201cP5 in its family table. These fields are intentionally marked as not specified rather than inferred.

## ADP201P4 distinctions from ADP201PCI

The manual identifies four differences relevant to software porting and system design:

1. ADP201P4 does not include a DAC node.
2. P1 is connected to the HOST FPGA; P2 is connected to the ADM FPGA.
3. The board has four SDRAM banks of 128 MB each, one bank per processor.
4. The PCI bus is 64-bit wide.

## Source terminology note

The manual uses the product-family name ADP201 and describes the company as «Инструментальные системы». This page does not add a legal entity form or other corporate attribution that is not stated in the cited manual.

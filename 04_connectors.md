# ADP201P4 External Connectors

This section describes the purpose, connector types and pin assignments of the external interfaces documented in the ADP201P4 operating manual.

## 1. SYNX — Inter-module synchronization

- **Connector:** AMPMODU System 50-20 plug, 20 contacts.
- **Purpose:** Connects base modules for synchronized operation. The connector carries both ADM interface synchronization signals and processor-subsystem synchronization signals.

### SYNX pin assignment

| Contact | Type | Signal | Contact | Type | Signal |
|:---:|:---:|---|:---:|:---:|---|
| 1 | I/OK | `RDY0` | 2 | — | `GND` |
| 3 | I/OK | `RDY1` | 4 | — | `GND` |
| 5 | I/O | `SYNC0` | 6 | — | `GND` |
| 7 | I/O | `START_EN` | 8 | — | `GND` |
| 9 | I/O | `START` | 10 | — | `GND` |
| 11 | I/O | `ENCODE` | 12 | — | `GND` |
| 13 | I/OK | `PINT0#` | 14 | — | `GND` |
| 15 | I/OK | `PINT1#` | 16 | — | `GND` |
| 17 | I/OK | `PINT2#` | 18 | — | `GND` |
| 19 | I/OK | `PRES#` | 20 | — | `GND` |

The signals have two functional groups:

- **ADM synchronization:** `RDY0`, `RDY1`, `SYNC0`, `START_EN`, `START` and `ENCODE` are controlled by the ADM FPGA.
- **Processor-subsystem synchronization:** `PINT0#`, `PINT1#`, `PINT2#` and `PRES#` are controlled by the HOST FPGA.

The manual specifies that the processor-subsystem signals `PINT0#`, `PINT1#`, `PINT2#` and `PRES#` are open-collector signals pulled up to +3.3 V on the module through 1 kΩ resistors. Do not connect these signals to sources above +4 V.

## 2. SDX — Exchange synchronization

- **Connector:** LEMO-SR socket.
- **Purpose:** Provides the SDX synchronization signal used by the start-synchronization unit.
- **Input impedance:** Jumper `JB` selects the input impedance:
  - `JB` installed: 50 Ω.
  - `JB` removed: 10 kΩ.

## 3. PIOX — Digital I/O

- **Connector:** AMPMODU SYSTEM 50-34 plug, 34 contacts.
- **Purpose:** Configurable digital input/output port. The ADM FPGA must be configured before the port can operate.
- **Electrical modes:** LVTTL (single-ended) or LVDS (differential), depending on the installed buffer.

### LVTTL mode — 74ALVCH16245DGG

The port has two independent 8-bit data buses, `PIO[15..8]` and `PIO[7..0]`. Each bus can be independently configured for input or output.

| Contact | Type | Signal | Contact | Type | Signal |
|:---:|:---:|---|:---:|:---:|---|
| 1 | — | `GND` | 2 | I/O | `PIO[15]` |
| 3 | I/O | `PIO[14]` | 4 | — | `GND` |
| 5 | I/O | `PIO[13]` | 6 | I/O | `PIO[12]` |
| 7 | — | `GND` | 8 | I/O | `PIO[11]` |
| 9 | I/O | `PIO[10]` | 10 | — | `GND` |
| 11 | I/O | `PIO[9]` | 12 | I/O | `PIO[8]` |
| 13 | — | `GND` | 14 | I/O | `PIO[7]` |
| 15 | I/O | `PIO[6]` | 16 | — | `GND` |
| 17 | I/O | `PIO[5]` | 18 | I/O | `PIO[4]` |
| 19 | — | `GND` | 20 | I/O | `PIO[3]` |
| 21 | I/O | `PIO[2]` | 22 | — | `GND` |
| 23 | I/O | `PIO[1]` | 24 | I/O | `PIO[0]` |
| 25 | — | `GND` | 26 | — | `ACK_WR` |
| 27 | — | Reserved | 28 | — | `GND` |
| 29 | O | `PIO_RD` | 30 | — | Reserved |
| 31 | — | `GND` | 32 | O | `PIO_WR` |
| 33 | I | `ACK_RD` | 34 | — | `GND` |

In the standard firmware, `PIO_WR` and `PIO_RD` are output strobes; `ACK_WR` and `ACK_RD` are input acknowledgements. Note that the connector pin table marks the type of contact 26 (`ACK_WR`) as “—”; the firmware description separately identifies the signal as an input. These are distinct pieces of information and should not be conflated.

### LVDS mode — SN65LVDM1677DGG

The LVDS configuration provides one 8-bit differential data bus, one differential control input and one differential control output. The connector also carries one LVTTL control output and one LVTTL control input.

| Contact | Type | Signal | Contact | Type | Signal |
|:---:|:---:|---|:---:|:---:|---|
| 1 | — | `GND` | 2 | I/O | `PIO_P[7]` |
| 3 | I/O | `PIO_N[7]` | 4 | — | `GND` |
| 5 | I/O | `PIO_P[6]` | 6 | I/O | `PIO_N[6]` |
| 7 | — | `GND` | 8 | I/O | `PIO_P[5]` |
| 9 | I/O | `PIO_N[5]` | 10 | — | `GND` |
| 11 | I/O | `PIO_P[4]` | 12 | I/O | `PIO_N[4]` |
| 13 | — | `GND` | 14 | I/O | `PIO_P[3]` |
| 15 | I/O | `PIO_N[3]` | 16 | — | `GND` |
| 17 | I/O | `PIO_P[2]` | 18 | I/O | `PIO_N[2]` |
| 19 | — | `GND` | 20 | I/O | `PIO_P[1]` |
| 21 | I/O | `PIO_N[1]` | 22 | — | `GND` |
| 23 | I/O | `PIO_P[0]` | 24 | I/O | `PIO_N[0]` |
| 25 | — | `GND` | 26 | I | `CIN_P` |
| 27 | I | `CIN_N` | 28 | — | `GND` |
| 29 | O | `COUT_P` | 30 | O | `COUT_N` |
| 31 | — | `GND` | 32 | O | `PIO_WR (LVTTL)` |
| 33 | I | `ACK_RD (LVTTL)` | 34 | — | `GND` |

The differential data and control lines are connected through the SN65LVDM1677DGG buffer. `PIO_WR` and `ACK_RD` remain LVTTL signals and are connected through the 74ALVCH16245DGG buffer.

## 4. External TigerSHARC link connectors

The manual lists connectors P1L3, P2L3, P3L3 and P4L3; each is an AMPMODU SYSTEM 50-34 plug. The component-placement drawing maps them as follows: P1L3 — XP2, P2L3 — XP5, P3L3 — XP3 and P4L3 — XP4.

The heading of Table 9 in the source manual reads “LINK1, LINK3”, although the section covers four connectors, P1L3–P4L3. For this reason, the table is not presented here as a universal pinout for all four connectors. Verify the applicable schematic and board revision before making a connection.

## Electrical safety

The manual states that only ADM submodules that do not generate voltages above +4 V on the ADMX connector signals may be connected to the ADMX interface. Check the submodule documentation and electrical levels before connecting it.

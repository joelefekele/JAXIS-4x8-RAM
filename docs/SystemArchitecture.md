# System Architecture

# Introduction

This document describes the architecture of the JAXIS 4×8 RAM system and explains how each hardware module interacts to perform memory read and write operations.

The RAM is designed using a modular architecture where each subsystem performs a single well-defined function. This approach simplifies debugging, expansion, and future integration into a complete computer system.

---

# High-Level Architecture

The RAM consists of the following major hardware modules:

- Address Bus
- Data Bus
- Address Decoder
- Four 8-bit Registers
- Write Logic
- Read Logic
- Tri-State Data Bus Buffer
- User Interface

Each module communicates through shared buses and control signals.

---

# Block Diagram

```
                   Address Switches
                          │
                          ▼
                     Address Bus
                          │
                          ▼
                     74HC139 Decoder
                   Y0   Y1   Y2   Y3
                    │    │    │    │
                    ▼    ▼    ▼    ▼
             Write Control Logic
                    │    │    │    │
                    ▼    ▼    ▼    ▼
             +-------------------------+
             |      74HC574 Registers  |
             |   Reg0 Reg1 Reg2 Reg3   |
             +-------------------------+
                    ▲
                    │
================ DATA BUS =================
                    ▲
                    │
              74HC125 Buffers
                    ▲
                    │
             Data DIP Switches

                    │
                    ▼
                   LEDs
```

---

# Address Bus

The address bus is responsible for selecting which register will participate in a memory operation.

The address bus consists of two signals:

- A0
- A1

The address bus connects directly to the 74HC139 address decoder.

---

# Address Decoder

The 74HC139 converts the two-bit address into four individual register select signals.

| Address | Selected Register |
|----------|-------------------|
| 00 | Register 0 |
| 01 | Register 1 |
| 10 | Register 2 |
| 11 | Register 3 |

Only one decoder output is active during a memory operation.

---

# Data Bus

The data bus is an 8-bit shared communication path.

It carries data between:

- Data input switches
- Memory registers
- LED indicators
- Future CPU interface

Every register connects to the same shared data bus.

The bus itself does not store information. It only transports data between hardware modules.

---

# Registers

The RAM contains four independent 8-bit registers.

Each register is implemented using one 74HC574 integrated circuit.

Each register performs two operations:

- Store data during a write operation.
- Drive the data bus during a read operation.

Only one register may drive the data bus at a time.

---

# Write Operation

During a write operation:

1. The user selects a memory address.
2. The address decoder selects one register.
3. The user places an 8-bit value on the data bus.
4. The Write Enable signal is activated.
5. A clock pulse is generated.
6. The selected register stores the data.

All non-selected registers retain their previous contents.

---

# Read Operation

During a read operation:

1. The user selects a memory address.
2. The corresponding register enables its outputs.
3. The selected register drives the data bus.
4. LEDs display the stored value.

No data is modified during a read operation.

---

# Tri-State Bus Control

To prevent bus contention, the RAM uses tri-state buffering.

During WRITE mode:

- The 74HC125 connects the DIP switches to the data bus.
- Register outputs remain disabled.

During READ mode:

- The 74HC125 disconnects the DIP switches.
- The selected register drives the data bus.

Only one device is allowed to drive the data bus at any time.

---

# Design Principles

The RAM architecture follows several engineering principles:

- Modular subsystem design
- Shared bus communication
- Single bus driver operation
- Synchronous memory writes
- Address-based register selection
- Expandable architecture

These principles simplify debugging and allow the RAM to be expanded into larger memory systems.

---

# Future Expansion

The architecture has been designed so that additional hardware modules can be connected without redesigning the memory subsystem.

Planned future modules include:

- Arithmetic Logic Unit (ALU)
- Program Counter
- Instruction Register
- Control Unit
- Custom CPU

The shared bus architecture will allow these modules to communicate directly with the RAM.

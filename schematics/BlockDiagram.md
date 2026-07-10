# System Block Diagram

## Overview

The block diagram illustrates the high-level architecture of the JAXIS 4×8 RAM. It identifies the major hardware modules and the flow of data and control signals during memory operations.

The RAM is organized around three primary signal groups:

- Address Bus
- Data Bus
- Control Signals

---

# System Block Diagram

```
                   +----------------------+
                   | Address DIP Switches |
                   +----------+-----------+
                              |
                              | Address Bus (A1, A0)
                              |
                              v
                       +---------------+
                       |   74HC139     |
                       | AddressDecoder|
                       +---+---+---+---+
                           |   |   |   |
                          Y0  Y1  Y2  Y3
                           |   |   |   |
                           v   v   v   v
                  +-------------------------+
                  | Write Logic (3-Input AND)|
                  +-------------------------+
                           |   |   |   |
                           |   |   |   |
                           v   v   v   v
                 +----------------------------+
                 |      74HC574 Registers     |
                 | Reg0 Reg1 Reg2 Reg3        |
                 +----------------------------+
                           ▲
                           │
===================== DATA BUS =====================
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

# Signal Flow

## Write Operation

1. Address is selected.
2. Decoder selects one register.
3. Data switches place an 8-bit value on the data bus.
4. Three-input AND gate generates the write clock.
5. Selected register stores the byte.

---

## Read Operation

1. Address is selected.
2. Selected register enables its outputs.
3. Stored byte appears on the data bus.
4. LEDs display the stored value.

---

# Design Philosophy

The architecture follows a modular approach.

Each hardware module performs one dedicated function:

- Address selection
- Address decoding
- Data storage
- Write control
- Read control
- Bus buffering

This modular organization simplifies debugging, testing, and future expansion.

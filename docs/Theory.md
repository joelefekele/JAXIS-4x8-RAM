# Digital Logic Theory

## Introduction

This document presents the digital logic concepts used in the design of the **JAXIS 4×8 RAM**. Rather than describing memory in a generic way, this document explains the specific architecture implemented in this project and the engineering principles behind each subsystem.

The JAXIS RAM is designed from standard **74HC-series digital logic integrated circuits**, allowing every stage of memory operation to be observed and understood.

---

# Binary Representation

Digital systems store and process information using binary numbers.

A binary digit (bit) has two possible states:

- Logic LOW (0)
- Logic HIGH (1)

Eight bits form one byte.

Example:

```
10110010
```

The JAXIS RAM stores one byte in each register.

---

# D Flip-Flops

The fundamental storage element of the JAXIS RAM is the D Flip-Flop.

A D Flip-Flop stores one bit of information and updates its output only on the active clock edge.

Once stored, the data remains unchanged until another valid clock pulse occurs.

---

# Registers

Each register is implemented using one **74HC574 Octal D-Type Flip-Flop**.

Each register contains eight D Flip-Flops, allowing it to store one complete byte.

The RAM contains four registers:

- Register 0
- Register 1
- Register 2
- Register 3

Each register represents one memory location.

---

# Shared Data Bus

The JAXIS RAM uses a shared **8-bit data bus**.

The data bus consists of eight wires:

```
D7
D6
D5
D4
D3
D2
D1
D0
```

The data bus connects to:

- Data Input Buffer (74HC125)
- All Register Inputs
- All Register Outputs
- LED Display
- Future CPU Interface

The data bus stores no information.

Its only purpose is transporting data between hardware modules.

---

# Address Bus

The address bus determines which register will participate in a memory operation.

The address bus consists of two lines:

```
A1
A0
```

These two lines provide four possible addresses.

| Address | Selected Register |
|----------|-------------------|
| 00 | Register 0 |
| 01 | Register 1 |
| 10 | Register 2 |
| 11 | Register 3 |

The address bus connects only to the address decoder.

---

# Address Decoder

The address decoder is implemented using one **74HC139**.

The decoder converts the two-bit binary address into four register-select outputs.

```
Y0
Y1
Y2
Y3
```

Only one output is active during any memory operation.

The decoder determines which register is allowed to participate in a write operation.

---

# Three-Input Write Logic

Unlike many memory systems that contain an internal Write Enable signal, the **74HC574 does not include a dedicated WE input**.

To solve this, the JAXIS RAM generates a gated write clock using **three-input AND gates**.

Each register has its own dedicated write clock.

The three inputs are:

- Clock Push Button
- Write Enable (WE)
- Decoder Output

Example:

```
Register0 Clock = Clock AND WE AND Y0

Register1 Clock = Clock AND WE AND Y1

Register2 Clock = Clock AND WE AND Y2

Register3 Clock = Clock AND WE AND Y3
```

A register stores data only when all three inputs are HIGH.

This guarantees that:

- The correct register is selected.
- Writing is enabled.
- A clock pulse occurs.

If any one of these conditions is false, the register retains its previous contents.

---

# Clock Signal

The clock synchronizes every write operation.

Changing the data bus does not modify memory.

Memory changes only on the active clock edge.

The clock is generated manually using a push button.

---

# Output Enable (OE)

Each 74HC574 contains an Output Enable (OE) input.

The OE input is **active LOW**.

```
OE = LOW
```

Outputs connected to the data bus.

```
OE = HIGH
```

Outputs disconnected (High Impedance).

The OE signal controls when a register is allowed to drive the shared data bus during a read operation.

---

# Tri-State Logic

The JAXIS RAM uses tri-state logic to allow multiple devices to share the same data bus safely.

Each output can exist in three states:

- Logic HIGH
- Logic LOW
- High Impedance (Hi-Z)

When a device enters Hi-Z, it becomes electrically disconnected from the data bus.

---

# Bus Contention

Bus contention occurs when two devices attempt to drive the data bus simultaneously.

Example:

```
Device A → 11111111

Device B → 00000000
```

This creates an electrical conflict.

To eliminate bus contention, the JAXIS RAM ensures that only one device drives the data bus at any time.

---

# 74HC125 Data Bus Buffer

The JAXIS RAM uses two **74HC125 Quad Tri-State Buffers** between the data DIP switches and the shared data bus.

During WRITE mode:

- The 74HC125 is enabled.
- The DIP switches drive the data bus.
- Register outputs remain disabled.

During READ mode:

- The 74HC125 enters High Impedance.
- The DIP switches are electrically disconnected.
- The selected register drives the data bus.

This prevents bus contention between the switches and the memory registers.

---

# Read Operation

A read operation follows these steps:

1. Select a memory address.
2. The decoder identifies the corresponding register.
3. The selected register's OE input is activated.
4. The register drives the shared data bus.
5. The LEDs display the stored byte.

No data is modified during a read operation.

---

# Write Operation

A write operation follows these steps:

1. Select a memory address.
2. Enter an 8-bit value using the data switches.
3. Enable WRITE mode.
4. Activate Write Enable (WE).
5. Press the clock button.
6. The selected register stores the byte.

All other registers remain unchanged.

---

# Engineering Design Philosophy

The JAXIS RAM is designed around several engineering principles:

- One shared data bus
- One shared address bus
- One function per hardware module
- Modular architecture
- Controlled bus access
- Synchronous memory writes
- Expandable design

Each subsystem performs a single dedicated function, simplifying debugging, testing, and future expansion.

---

# Summary

The JAXIS 4×8 RAM demonstrates how digital memory can be implemented using discrete logic integrated circuits.

By combining registers, address decoding, shared buses, tri-state buffering, and clock-controlled write logic, the project recreates the fundamental architecture used in modern memory systems while exposing every stage of operation for engineering analysis and hardware experimentation.

The completed RAM module serves as the first subsystem in the long-term development of the JAXIS custom computer.

# Address Decoder

## Overview

The address decoder is responsible for selecting one memory register during every read or write operation.

The JAXIS 4×8 RAM uses a **74HC139 2-to-4 Line Decoder** to convert a 2-bit binary address into four individual register select signals.

This architecture allows a single shared data bus to be used by multiple registers while ensuring that only one register is selected at a time.

---

# Purpose

The decoder performs one function:

Convert the binary address into a single active register select signal.

Without the decoder, it would not be possible to determine which register should participate in a memory operation.

---

# Inputs

The decoder receives two address signals from the Address DIP Switches.

```
A1
A0
```

These two signals form the address bus.

---

# Outputs

The decoder generates four outputs.

```
Y0
Y1
Y2
Y3
```

Each output corresponds to one register.

```
Y0 → Register 0

Y1 → Register 1

Y2 → Register 2

Y3 → Register 3
```

Only one output is active at any time.

---

# Address Table

| A1 | A0 | Selected Register | Decoder Output |
|----|----|-------------------|----------------|
| 0  | 0   | Register 0       |     Y0         |
| 0  | 1   | Register 1       |     Y1         |
| 1  | 0   | Register 2       |     Y2         |
| 1  | 1   | Register 3       |     Y3         |

---

# Decoder Connections

## Inputs

```
Address Switch A0

↓

74HC139 A0
```

```
Address Switch A1

↓

74HC139 A1
```

---

## Outputs

```
Y0 → Register0 Write Logic

Y1 → Register1 Write Logic

Y2 → Register2 Write Logic

Y3 → Register3 Write Logic
```

Each output connects to the corresponding three-input AND gate.

---

# Interaction with Write Logic

The decoder does not write data.

Instead, it determines which register is allowed to receive the clock.

Each decoder output becomes one input of a three-input AND gate.

Example:

```
Clock

AND

Write Enable

AND

Y2

↓

Register 2 Clock
```

If Register 2 is selected, only Register 2 receives the clock pulse.

All other registers ignore it.

---

# Interaction with Read Logic

During a read operation, the selected register's Output Enable (OE) is activated.

Only the selected register is allowed to drive the shared data bus.

This prevents multiple registers from driving the bus simultaneously.

---

# Why a Decoder?

Without a decoder, each register would require its own manual selection switch.

Using the 74HC139 provides:

- Automatic register selection
- Reduced wiring complexity
- Improved scalability
- Modular architecture
- Expansion capability

---

# Future Expansion

The decoder architecture allows the RAM to be expanded easily.

Adding more memory locations requires:

- Additional registers
- Larger address bus
- Larger decoder

The overall architecture remains unchanged.

---

# Summary

The address decoder forms the control center of register selection within the JAXIS 4×8 RAM.

By translating a binary address into a single active output, the decoder ensures that only one register participates in each memory operation, enabling reliable read and write operations while supporting a shared data bus architecture.

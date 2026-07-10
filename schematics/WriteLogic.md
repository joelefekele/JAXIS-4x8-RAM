# Write Logic

## Overview

The write logic controls when data is allowed to enter a memory register.

The JAXIS 4×8 RAM is built using **74HC574 Octal D-Type Flip-Flops**. Since the 74HC574 does **not** include a dedicated **Write Enable (WE)** input, external write logic is required.

To solve this limitation, the JAXIS RAM generates an independent write clock for each register using **three-input AND gates**.

This design guarantees that data is stored only when:

- The correct register has been selected.
- Write Enable (WE) is active.
- A clock pulse is generated.

---

# Design Objective

The write logic ensures that:

- Only one register stores data.
- All non-selected registers remain unchanged.
- Memory writes occur only when intentionally requested.
- Every write operation is synchronized with the system clock.

---

# Hardware Used

The write logic consists of:

- Two 74HC08 Quad AND Gate ICs
- One Clock Push Button
- One Write Enable (WE) Switch
- One 74HC139 Address Decoder

Each register receives its own dedicated write clock.

---

# Three-Input AND Gate

Each write clock is generated using three input signals.

```
                 +-------------+
WE ------------->|             |
                 |             |
Yn ------------->| 3-Input AND |-------> Register Clock (CP)
                 |             |
CLK ------------>|             |
                 +-------------+
```

Inputs

- **WE** — Write Enable
- **Yn** — Address Decoder Output
- **CLK** — Clock Push Button

Output

- **CP** — Clock input of the selected 74HC574 register

---

# Register Clock Equations

Each register receives its own independent clock signal.

```
Register0 CP = WE × CLK × Y0

Register1 CP = WE × CLK × Y1

Register2 CP = WE × CLK × Y2

Register3 CP = WE × CLK × Y3
```

Only one equation can evaluate to HIGH during a write operation.

---

# Signal Definitions

## Write Enable (WE)

The Write Enable signal authorizes memory modification.

```
WE = 0
```

Writing disabled.

No register may store data.

```
WE = 1
```

Writing enabled.

The selected register may store data when a clock pulse occurs.

---

## Decoder Output (Yn)

The address decoder selects which register is permitted to receive the clock.

```
Address = 00

↓

Y0 = HIGH
```

```
Address = 01

↓

Y1 = HIGH
```

```
Address = 10

↓

Y2 = HIGH
```

```
Address = 11

↓

Y3 = HIGH
```

Only one decoder output is HIGH at any time.

---

## Clock (CLK)

The clock signal is generated manually using a push button.

The 74HC574 stores data only on the active clock edge.

Changing the data bus without pressing the clock button does not modify memory.

---

# JAXIS RAM Write Truth Table

The register stores data only when **all three input signals are HIGH**.

| Write Enable (WE) | Decoder Output (Yn) | Clock (CLK) | Register Clock (CP) | Register Action |
|:-----------------:|:-------------------:|:-----------:|:-------------------:|-----------------|
|       0           |         0           |     0       |           0         | No Write        |
|       0           |         0           |     1       |           0         | No Write        |
|       0           |         1           |     0       |           0         | No Write        |
|       0           |         1           |     1       |           0         | No Write        |
|       1           |         0           |     0       |           0         | No Write        |
|       1           |         0           |     1       |           0         | No Write        |
|       1           |         1           |     0       |           0         | No Write        |
|       1           |         1           |     1       |           1         | **Store Data**  |

The write clock is generated according to:

```
CP = WE × Yn × CLK
```

A register stores data only when:

- Write Enable is HIGH.
- The register has been selected by the decoder.
- The Clock Push Button generates a clock pulse.

---

# Signal Flow

```
Address Switches
        │
        ▼
     74HC139
        │
        ▼
   Decoder Output (Yn)
        │
        ▼
+-----------------------+
|                       |
| Write Enable (WE)     |
|                       |
| Clock Push Button     |
+-----------+-----------+
            │
            ▼
     Three-Input AND Gate
            │
            ▼
 Register Clock (CP)
            │
            ▼
      74HC574 Register
```

---

# Example Write Operation

Suppose the following conditions exist.

```
Address = 10

Data = 10101100

WE = HIGH

Clock = Pressed
```

The decoder produces:

```
Y0 = LOW

Y1 = LOW

Y2 = HIGH

Y3 = LOW
```

The generated clocks become:

```
CP0 = LOW

CP1 = LOW

CP2 = HIGH

CP3 = LOW
```

Result:

- Register 2 stores **10101100**
- Registers 0, 1, and 3 remain unchanged

---

# Why External Write Logic?

The 74HC574 automatically stores data whenever a valid clock edge reaches its Clock input.

If every register received the same clock signal directly, every register would store the same byte simultaneously.

The external write logic prevents this by generating an independent write clock for each register.

Only the selected register receives the clock pulse.

---

# Advantages of the JAXIS Write Logic

- Controlled memory writes
- One-register-at-a-time operation
- Prevents accidental memory modification
- Simple modular architecture
- Easy expansion to larger memory systems
- Hardware-only implementation (no microcontroller required)

---

# Engineering Notes

The write logic was intentionally implemented using discrete logic rather than programmable devices.

This allows every stage of the memory write process to be observed, analyzed, and understood while demonstrating how write control can be implemented using fundamental digital logic components.

---

# Summary

The write logic is one of the defining features of the JAXIS 4×8 RAM.

By combining the **Write Enable signal**, **Address Decoder output**, and **Clock signal** through dedicated three-input AND gates, the design generates an independent write clock for every register.

This architecture guarantees that only the selected register stores new data while all other registers preserve their previous contents, providing reliable and deterministic memory operation.

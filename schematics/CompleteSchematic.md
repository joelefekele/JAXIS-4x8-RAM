# Complete JAXIS 4×8 RAM Schematic

## Overview

This document describes how every subsystem of the JAXIS 4×8 RAM is connected to form a complete memory system.

The design is implemented entirely with discrete 74HC-series logic integrated circuits and follows a modular architecture. Each subsystem performs one specific function while communicating through a shared 8-bit data bus.

---

# Design Philosophy

The JAXIS RAM is divided into independent hardware modules.

Each module performs one dedicated task.

- Address Selection
- Address Decoder
- Write Logic
- Register Bank
- Shared Data Bus
- Manual Read Logic
- Data Buffer
- LED Display

Separating the design into modules simplifies construction, debugging, testing, and future expansion.

---

# System Overview

```
Address DIP Switches
        │
        ▼
Address Bus (A1,A0)
        │
        ▼
74HC139 Address Decoder
        │
        ▼
Write Logic
(Three-Input AND Gates)
        │
        ▼
Register Bank
(4 × 74HC574)
        ▲
        │
Shared 8-bit Data Bus
        ▲
        │
2 × 74HC125 Buffers
        ▲
        │
Data DIP Switches

Manual Read Switches
        │
        ▼
Register Output Enable (OE)

Shared Data Bus
        │
        ▼
LED Display
```

---

# Address Section

The Address DIP Switches generate a two-bit address.

```
A1

A0
```

These signals connect directly to the 74HC139 Address Decoder.

The decoder converts the binary address into one active output.

```
00 → Y0

01 → Y1

10 → Y2

11 → Y3
```

Only one decoder output is active during a WRITE operation.

---

# Write Section

The write logic controls when data is stored.

Each decoder output connects to a dedicated three-input AND gate.

Each AND gate receives:

- Write Enable (WE)
- Decoder Output (Yn)
- Clock Push Button

Each AND gate generates an independent clock signal.

```
CP0

CP1

CP2

CP3
```

Only the selected register receives a clock pulse.

---

# Register Bank

The JAXIS RAM contains four identical register modules.

Each module consists of one 74HC574.

Each register receives:

- Shared Data Bus
- Individual Clock Input
- Individual Output Enable

Each register stores one 8-bit word.

Total memory capacity:

```
4 Registers

×

8 Bits

=

32 Bits
```

---

# Shared Data Bus

The shared data bus connects:

- Data DIP Switches
- 74HC125 Buffers
- Register D Inputs
- Register Outputs
- LED Display

The data bus never stores information.

Its only purpose is transporting data.

---

# Read Section

Unlike the write operation, register selection during READ is manual.

Each register has its own Read DIP Switch.

```
Read Switch 0

↓

Register 0 OE

Read Switch 1

↓

Register 1 OE

Read Switch 2

↓

Register 2 OE

Read Switch 3

↓

Register 3 OE
```

Only one Read Switch should be enabled at a time.

---

# Data Buffer

The two 74HC125 ICs isolate the Data DIP Switches.

WRITE Mode

- Buffers Enabled
- Data DIP Switches connected

READ Mode

- Buffers Disabled
- Data DIP Switches disconnected

This prevents interference between the Data DIP Switches and the selected register.

---

# LED Display

The LEDs continuously monitor the shared data bus.

During WRITE mode they display the value selected by the Data DIP Switches.

During READ mode they display the byte stored in the selected register.

---

# Memory Capacity

The JAXIS RAM contains:

- 4 Memory Locations
- 8 Bits per Location

Total Capacity

```
4 × 8 = 32 bits
```

---

# System Operation

### WRITE

1. Select an address.
2. Enter data using the Data DIP Switches.
3. Enable Write Enable.
4. Press the Clock Push Button.
5. The selected register stores the byte.

---

### READ

1. Disable the 74HC125 buffers.
2. Enable one register by setting its OE LOW.
3. The selected register drives the shared data bus.
4. The LEDs display the stored byte.

---

# Future Expansion

The modular architecture allows future upgrades including:

- Additional registers
- Larger address buses
- Automatic read selection
- CPU interface
- ALU integration
- Complete JAXIS computer

---

# Summary

The Complete JAXIS 4×8 RAM combines address decoding, write control, manual read control, shared bus communication, and discrete register modules into a fully functional hardware memory system.

The architecture emphasizes simplicity, modularity, and ease of debugging while providing a solid foundation for future expansion into a complete computer architecture.

# Read Logic

## Overview

The read logic controls how stored data is transferred from the selected register onto the shared data bus.

Unlike the write operation, reading does **not** modify memory. Instead, the selected register is manually connected to the shared data bus by enabling its **Output Enable (OE)** input.

The JAXIS 4×8 RAM uses **manual OE control** through DIP switches rather than automatic decoder-controlled read selection. This design was chosen to simplify the first hardware prototype and make the read operation easier to observe and debug.

---

# Design Objective

The read logic is designed to:

- Read data without modifying memory.
- Allow manual selection of the register to read.
- Prevent bus contention.
- Display the stored byte on the LEDs.
- Demonstrate the operation of tri-state outputs.

---

# Hardware Used

The read logic consists of:

- Four 74HC574 Registers
- Four Read DIP Switches
- One Shared Data Bus
- Two 74HC125 Tri-State Buffers
- LED Display

---

# Manual Read Selection

Unlike the write logic, which automatically selects the destination register using the address decoder, the read logic uses dedicated DIP switches.

Each register has its own Output Enable control.

```
Read Switch 0 → Register 0 OE

Read Switch 1 → Register 1 OE

Read Switch 2 → Register 2 OE

Read Switch 3 → Register 3 OE
```

Each OE input is active LOW.

---

# Output Enable (OE)

The Output Enable input determines whether a register is allowed to drive the shared data bus.

```
OE = LOW
```

Outputs Enabled

The register drives the shared data bus.

```
OE = HIGH
```

Outputs Disabled

The register enters High Impedance (Hi-Z).

---

# JAXIS RAM Read Truth Table

| Read Switch | OE | Register Output | Data Bus |
|:-----------:|:--:|:---------------:|----------|
| OFF | HIGH | High Impedance | No Output |
| ON | LOW | Enabled | Stored Byte |

---

# Read Sequence

1. Select the register using its Read DIP Switch.
2. The selected register receives OE = LOW.
3. The register enables its outputs.
4. The stored byte is placed on the shared data bus.
5. The LEDs display the stored data.

No memory contents change during this operation.

---

# Data Flow

```
Register

↓

Q Outputs

↓

Shared Data Bus

↓

74HC125

↓

LED Display
```

---

# Interaction with the 74HC125

The JAXIS RAM uses the 74HC125 to isolate the Data DIP Switches during READ mode.

### WRITE Mode

- Data DIP Switches connected to the data bus.
- Register outputs disabled.

### READ Mode

- Data DIP Switches disconnected.
- Selected register connected to the data bus.
- LEDs display the stored byte.

This prevents both the DIP switches and the registers from driving the data bus simultaneously.

---

# Preventing Bus Contention

Only one Read DIP Switch should be enabled at a time.

If two registers have OE = LOW simultaneously:

- Both registers attempt to drive the shared data bus.
- Bus contention occurs.
- Incorrect data may appear on the LEDs.

For proper operation:

- Enable only one Read DIP Switch.
- Leave all others OFF.

---

# Advantages of Manual Read Control

The manual read system provides several benefits during hardware development:

- Simplifies the prototype.
- Makes debugging easier.
- Clearly demonstrates tri-state operation.
- Allows each register to be tested independently.
- Eliminates additional control logic during the first hardware revision.

Future versions of the JAXIS RAM may replace the manual Read DIP Switches with automatic decoder-controlled OE logic.

---

# Summary

The JAXIS RAM uses manual Output Enable control for read operations.

Each register is enabled individually using its own Read DIP Switch, allowing the selected register to drive the shared data bus while all other registers remain in High Impedance.

Combined with the 74HC125 data bus buffer, this architecture provides safe and reliable read operations while preventing bus contention and simplifying hardware debugging.

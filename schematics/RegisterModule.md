# Register Module

## Overview

The register module is the primary storage element of the JAXIS 4×8 RAM.

Each register stores one 8-bit word and is implemented using a single **74HC574 Octal D-Type Flip-Flop**.

The complete RAM contains four identical register modules:

- Register 0
- Register 1
- Register 2
- Register 3

Each register is identical except for its Write Clock and Output Enable control signals.

---

# Purpose

Each register performs two functions:

1. Store one byte during a WRITE operation.
2. Place the stored byte onto the shared data bus during a READ operation.

The register never performs both operations simultaneously.

---

# Register Architecture

```
                 Shared Data Bus
       D7 D6 D5 D4 D3 D2 D1 D0
                │
                ▼
          +-----------------+
          |    74HC574      |
          |                 |
          |  8 D Flip-Flops |
          |                 |
          +-----------------+
                ▲
                │
       Q7 Q6 Q5 Q4 Q3 Q2 Q1 Q0
                │
                ▼
             Shared Data Bus
```

---

# Pin Connections

## Power

### VCC

Connected to the +5V power rail.

Purpose:

Provides operating voltage for the register.

---

### GND

Connected to the common ground rail.

Purpose:

Provides the reference voltage for the IC.

---

# Data Inputs (D0–D7)

Each D input connects directly to the shared 8-bit data bus.

```
Bus D0 → Register D0

Bus D1 → Register D1

...

Bus D7 → Register D7
```

Purpose:

Receive the byte that will be stored during a write operation.

---

# Data Outputs (Q0–Q7)

Each Q output connects back to the shared data bus.

```
Register Q0 → Bus D0

Register Q1 → Bus D1

...

Register Q7 → Bus D7
```

Purpose:

Drive the shared data bus during a read operation.

The outputs are controlled by the Output Enable signal.

---

# Clock Input (CP)

The clock input is **not connected directly** to the push button.

Instead, each register receives its own gated write clock.

```
Clock Push Button

        AND

Write Enable (WE)

        AND

Decoder Output (Yn)

        │
        ▼

Register Clock
```

For each register:

```
Register0 Clock = Clock AND WE AND Y0

Register1 Clock = Clock AND WE AND Y1

Register2 Clock = Clock AND WE AND Y2

Register3 Clock = Clock AND WE AND Y3
```

Purpose:

The register stores new data only when:

- Write Enable is active.
- The register is selected.
- A clock pulse occurs.

---

# Output Enable (OE)

The OE input is active LOW.

```
OE = LOW
```

Register outputs are connected to the data bus.

```
OE = HIGH
```

Register outputs enter High Impedance (Hi-Z).

Purpose:

Allow only the selected register to drive the shared data bus during READ operations.

---

# Write Operation

During a write operation:

1. Address is selected.
2. Decoder activates one output.
3. Write Enable is activated.
4. Data appears on the data bus.
5. Clock push button is pressed.
6. Selected register stores the byte.

All other registers ignore the clock.

---

# Read Operation

During a read operation:

1. Address is selected.
2. Selected register enables its outputs.
3. Stored byte appears on the data bus.
4. LEDs display the byte.

No memory contents are modified during a read operation.

---

# Why the 74HC574?

The 74HC574 was selected because it:

- Stores one complete byte.
- Writes all eight bits simultaneously.
- Includes tri-state outputs.
- Integrates eight D Flip-Flops into one IC.
- Simplifies the overall RAM architecture.

The lack of a dedicated Write Enable input was addressed by implementing custom external write logic using three-input AND gates.

---

# Module Reusability

The register module is fully modular.

To create additional memory locations:

- Duplicate the register module.
- Assign a new decoder output.
- Assign a new gated write clock.
- Assign a unique Output Enable control.

No other hardware modifications are required.

---

# Summary

The register module forms the fundamental storage element of the JAXIS 4×8 RAM.

By combining the 74HC574 with external write logic, shared data bus architecture, and controlled output enable signals, the register module provides reliable byte-wide storage while remaining modular and expandable for future computer architecture projects.

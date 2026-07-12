# Shared Data Bus

## Overview

The shared data bus is the primary communication pathway of the JAXIS 4×8 RAM.

Its purpose is to transfer 8-bit data between the Data DIP Switches, the memory registers, and the LED display.

The shared data bus does not store information. It only transports data between different hardware modules.

The JAXIS RAM uses a single shared 8-bit data bus for both WRITE and READ operations.

---

# Design Objective

The shared data bus is designed to:

- Transfer data from the Data DIP Switches during WRITE operations.
- Transfer stored data from a selected register during READ operations.
- Connect all four registers using one common set of data lines.
- Reduce wiring complexity.
- Support future expansion of the memory system.

---

# Hardware Used

The shared data bus consists of:

- 8 Data Bus Wires
- 2 × 74HC125 Quad Tri-State Buffers
- 4 × 74HC574 Octal Registers
- 8-bit Data DIP Switch
- 8 LEDs

---

# Data Bus Signals

The data bus contains eight signal lines.

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

Each signal carries one bit.

Together they form an 8-bit data bus.

---

# Bus Connections

Each data line connects to:

- Data DIP Switches (through the 74HC125)
- Register 0 D Inputs
- Register 1 D Inputs
- Register 2 D Inputs
- Register 3 D Inputs
- Register Outputs (Q0–Q7)
- LED Display

The shared data bus is the only path used to transfer data throughout the RAM.

---

# JAXIS RAM WRITE Operation

The shared data bus distributes data to every register during a WRITE operation.

The complete write sequence is:

1. Select the memory address using the Address DIP Switches.
2. The 74HC139 decodes the address and activates one decoder output (Y0–Y3).
3. Set the desired 8-bit value using the Data DIP Switches.
4. Enable the two 74HC125 buffers.
5. The Data DIP Switches drive the shared data bus.
6. The shared data bus delivers the byte to the D inputs of all four 74HC574 registers.
7. Set Write Enable (WE) HIGH.
8. Press the Clock Push Button.
9. The selected three-input AND gate generates a clock pulse for only the selected register.
10. The selected register stores the byte.
11. All other registers retain their previous contents because they do not receive a clock pulse.

```
                Address DIP Switches
                        │
                        ▼
                   74HC139 Decoder
                        │
                        ▼
                  Selected Output (Yn)
                        │
                        ▼
WE ───────────────┐
                  │
Clock Push Button ├────► Three-Input AND Gate
                  │
Yn ───────────────┘
                        │
                        ▼
                Register Clock (CP)

Data DIP Switches
        │
        ▼
   2 × 74HC125 Enabled
        │
        ▼
 Shared Data Bus
        │
        ├────────► Register 0 D Inputs
        ├────────► Register 1 D Inputs
        ├────────► Register 2 D Inputs
        └────────► Register 3 D Inputs
```

Although every register continuously receives the data on the shared data bus, only the selected register stores the byte because only its Clock (CP) input receives the gated clock pulse.

---

# JAXIS RAM READ Operation

The shared data bus also transfers stored data during a READ operation.

Unlike the WRITE operation, the address decoder is **not** used to select the register.

Instead, the JAXIS RAM uses manual Output Enable (OE) switches.

The complete read sequence is:

1. Disable the two 74HC125 buffers.
2. The Data DIP Switches are disconnected from the shared data bus.
3. Select the register to read by setting its Output Enable (OE) LOW.
4. Leave all other register OE inputs HIGH.
5. The selected register enables its outputs.
6. The stored byte is placed onto the shared data bus.
7. The LEDs display the value currently present on the shared data bus.

```
Data DIP Switches
        │
        ▼
2 × 74HC125 Disabled
        │
        ▼
      High Impedance

Register Selected
(OE = LOW)
        │
        ▼
Register Outputs (Q0-Q7)
        │
        ▼
 Shared Data Bus
        │
        ▼
LED Display
```

Only one register should have OE LOW at any time.

All remaining registers stay in High Impedance and do not drive the shared data bus.

---

# Role of the 74HC125

The two 74HC125 ICs isolate the Data DIP Switches from the shared data bus.

### WRITE Mode

- Buffers Enabled
- Data DIP Switches connected
- Data flows from the switches to the shared data bus

### READ Mode

- Buffers Disabled
- Data DIP Switches disconnected
- Selected register drives the shared data bus

---

# Bus Contention

Bus contention occurs when multiple devices attempt to drive the shared data bus simultaneously.

The JAXIS RAM prevents bus contention by:

- Disabling both 74HC125 ICs during READ operations.
- Enabling only one register by setting only one OE input LOW.
- Keeping all other register outputs in High Impedance.

Under normal operation, only one device drives the shared data bus at any time.

---

# Advantages

The shared data bus provides:

- Reduced wiring
- Modular hardware architecture
- Easier debugging
- Simplified expansion
- Efficient communication between memory modules

---

# Engineering Notes

The shared data bus is one of the defining architectural features of the JAXIS RAM.

During WRITE operations, the shared data bus distributes data to every register while the JAXIS write logic determines which register stores the data.

During READ operations, the selected register places its stored byte onto the shared data bus while all other registers remain electrically disconnected through their High Impedance outputs.

This architecture separates data distribution from data storage, resulting in a modular and reliable memory system.

---

# Summary

The shared data bus serves as the communication backbone of the JAXIS 4×8 RAM.

During WRITE operations, it distributes data from the Data DIP Switches to all register inputs while the JAXIS write logic determines which register stores the byte.

During READ operations, it transfers the stored byte from the manually selected register to the LED display.

Combined with the 74HC125 buffers, manual Output Enable control, and the JAXIS write logic, the shared data bus provides reliable communication while preventing bus contention.

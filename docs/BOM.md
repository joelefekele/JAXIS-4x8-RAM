# Bill of Materials (BOM)

## Overview

This document lists the components required to build Version 1 of the JAXIS 4×8 RAM.

The first prototype is implemented entirely using discrete 74HC-series logic integrated circuits without programmable devices or microcontrollers.

---

# Integrated Circuits

| Quantity | Component | Purpose |
|----------|-----------|---------|
| 4 | 74HC574 | 8-bit Memory Registers |
| 1 | 74HC139 | 2-to-4 Address Decoder |
| 2 | 74HC08 | JAXIS Write Logic (Four 3-input AND Gates) |
| 2 | 74HC125 | Data Input Tri-State Buffers |

---

# Input Devices

| Quantity | Component | Purpose |
|----------|-----------|---------|
| 1 | 8-bit DIP Switch | Data Input |
| 1 | 2-bit DIP Switch | Address Selection |
| 1 | SPST Switch | Write Enable (WE) |
| 4 | SPST Switches | Manual Register Output Enable (OE0–OE3) |
| 1 | Push Button | System Clock |

---

# Output Devices

| Quantity | Component | Purpose |
|----------|-----------|---------|
| 8 | LEDs | Data Bus Display |
| 8 | 220 Ω Resistors | LED Current Limiting |

---

# Power Components

| Quantity | Component | Purpose |
|----------|-----------|---------|
| 1 | 5V Power Supply | System Power |
| 7 | 0.1 µF Ceramic Capacitors | IC Decoupling (One per IC) |

---

# Prototyping Materials

| Quantity | Component |
|----------|-----------|
| Breadboards | As Required |
| Jumper Wires | As Required |

---

# Memory Specifications

| Parameter | Value |
|-----------|-------|
| Memory Organization | 4 × 8 |
| Total Memory Capacity | 32 Bits |
| Register Size | 8 Bits |
| Address Width | 2 Bits |
| Data Width | 8 Bits |

---

# Design Notes

The JAXIS RAM Version 1 prioritizes simplicity, modularity, and hardware visibility.

Several architectural decisions were intentionally made to simplify testing and debugging during prototype development.

These include:

- Manual Output Enable control
- External write logic using three-input AND gates
- Shared 8-bit data bus
- Tri-state buffering using two 74HC125 ICs

These choices allow every subsystem to be observed and verified independently before future automation is introduced.

---

# Future Hardware Changes

Future revisions may include:

- Automatic Output Enable logic
- Larger memory arrays
- Additional address lines
- PCB implementation
- CPU interface
- ALU integration

---

# Summary

This Bill of Materials documents the hardware required to construct the first prototype of the JAXIS 4×8 RAM.

The component selection reflects the project's goal of demonstrating computer memory design using discrete logic integrated circuits while maintaining a modular architecture that supports future expansion.

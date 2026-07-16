# Revision History

## Overview

This document tracks the design evolution of the JAXIS 4×8 RAM project.

Each revision records significant architectural changes, design improvements, and future development plans.

---

# Version 1.0

**Status:** In Development

## Architecture

- 4 × 8-bit RAM
- 32-bit total memory capacity
- Built entirely using 74HC-series logic ICs
- No microcontroller or programmable logic devices

---

## Features

- Shared 8-bit Data Bus
- 2-bit Address Bus
- 74HC139 Address Decoder
- External Write Logic
- Manual Output Enable (OE) Control
- 74HC125 Tri-State Data Buffers
- LED Data Display
- Breadboard Prototype

---

## Write Logic

The write system uses dedicated three-input AND gates to generate an independent clock signal for each register.

Each write clock is generated from:

- Write Enable (WE)
- Decoder Output (Yn)
- Clock Push Button (CLK)

Only the selected register receives a clock pulse during a write operation.

---

## Read Logic

The first hardware revision uses manual Output Enable control.

Each register has an independent OE switch.

This approach simplifies debugging and allows each register to be tested individually during prototype development.

---

## Design Goals

Version 1 focuses on:

- Understanding RAM architecture from first principles
- Learning computer memory design
- Demonstrating discrete logic implementation
- Creating a modular hardware platform for future expansion

---

# Planned Improvements

Future revisions may include:

- Automatic Output Enable logic
- Increased memory capacity
- Additional address lines
- PCB implementation
- CPU interface
- ALU integration
- Expansion into a complete computer architecture

---

# Revision Table

| Version | Status | Description |
|---------|--------|-------------|
| 1.0 | In Development | Initial JAXIS 4×8 RAM architecture using discrete logic ICs |
| 2.0 | Planned | Automatic read logic and expanded memory |
| 3.0 | Planned | CPU integration |
| 4.0 | Planned | Complete discrete logic computer |

---

# Summary

The JAXIS RAM is being developed incrementally, with each revision introducing new hardware capabilities while maintaining a modular and well-documented architecture.

This revision history provides a record of the project's engineering evolution and serves as a reference for future development.

# Project Overview

## Introduction

The JAXIS 4×8 RAM project is a hardware engineering project focused on the design and implementation of a **4-word × 8-bit Random Access Memory (RAM)** using standard **74HC-series digital logic integrated circuits**.

Instead of relying on a commercial RAM chip, this project investigates how computer memory operates internally by constructing each subsystem from fundamental digital logic components.

The project emphasizes engineering analysis, modular design, hardware implementation, and systematic testing to develop a complete understanding of digital memory systems.

---

# Problem Statement

Modern memory devices integrate millions or billions of transistors into a single integrated circuit, making their internal operation difficult to observe and understand.

This project addresses that challenge by designing a small RAM module from discrete logic ICs, allowing every subsystem—including registers, buses, address decoding, and control logic—to be studied individually before being integrated into a complete memory system.

---

# Project Objectives

The primary objectives of this project are to:

- Design a functional 4×8 RAM module
- Understand digital memory architecture
- Design a shared 8-bit data bus
- Implement a 2-bit address bus
- Design address decoding logic
- Implement write and read control logic
- Prevent bus contention through tri-state buffering
- Produce complete engineering documentation
- Create a reusable memory subsystem for future computer projects

---

# Scope

The project includes the design and implementation of:

- Four 8-bit registers
- Shared data bus
- Address bus
- Address decoder
- Clock-controlled write logic
- Output enable logic
- Tri-state data bus buffering
- Manual read/write interface
- LED data monitoring

The project does not include a CPU or instruction execution. Those components are planned as future JAXIS hardware projects.

---

# Expected Outcome

The completed system will allow a user to:

- Select one of four memory addresses
- Store an 8-bit value into the selected register
- Read stored data from memory
- Observe all data transfers using LEDs
- Demonstrate the operation of a shared bus architecture

The completed RAM module will become the memory subsystem of a future custom-built computer.

---

# Engineering Approach

The RAM is being developed using a modular engineering methodology.

Each subsystem is designed, analyzed, and verified individually before integration into the complete system.

The project emphasizes understanding the purpose of every signal, connection, and component rather than reproducing an existing reference design.

---

# Current Status

The project is currently in the hardware design phase.

Completed work includes:

- Memory architecture
- Register design
- Address bus
- Data bus
- Address decoder
- Write logic
- Read logic
- Bus contention analysis
- Tri-state buffer architecture

Remaining work includes:

- Complete hardware schematic
- Breadboard implementation
- Functional testing
- PCB design
- Final validation

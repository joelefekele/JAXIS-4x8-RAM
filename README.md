# JAXIS 4×8 RAM

## Designing Computer Memory from First Principles Using Discrete 74HC Logic ICs

---

# Overview

The **JAXIS 4×8 RAM** project is a complete hardware implementation of a **4-word × 8-bit Random Access Memory (RAM)** built entirely from standard **74HC-series digital logic integrated circuits**.

Rather than relying on a commercial RAM chip, this project investigates how computer memory functions internally by designing and constructing each subsystem from fundamental digital logic components.

The objective is to gain a deep understanding of digital memory architecture through the implementation of registers, address decoding, shared buses, clock-controlled write operations, tri-state output control, and modular hardware design.

This project serves as the first subsystem in a long-term effort to design and build a complete computer from discrete digital logic.

---

# Project Goals

- Design a fully functional 4×8 RAM module
- Understand memory architecture at the hardware level
- Implement a shared 8-bit data bus
- Design a 2-bit address bus and decoder
- Develop write and read control logic
- Prevent bus contention using tri-state buffers
- Produce professional engineering documentation
- Create a reusable memory subsystem for future CPU development

---

# System Specifications

| Specification | Value |
|--------------|-------|
| Memory Capacity | 4 Words |
| Word Width | 8 Bits |
| Address Width | 2 Bits |
| Data Width | 8 Bits |
| Technology | 74HC Logic Family |
| Supply Voltage | +5 V |

---

# Hardware Components

| Component | Purpose |
|-----------|----------|
| 4 × 74HC574 | 8-bit Memory Registers |
| 1 × 74HC139 | Address Decoder |
| 2 × 74HC08 | Write Logic |
| 2 × 74HC125 | Tri-State Data Bus Buffer |
| DIP Switches | Address and Data Input |
| Push Buttons | Clock Control |
| LEDs | Data Bus Monitoring |
| Breadboards | Prototype Platform |

---

# System Architecture

The RAM consists of the following hardware modules:

- Shared 8-bit Data Bus
- 2-bit Address Bus
- Address Decoder
- Four 8-bit Registers
- Write Enable Logic
- Output Enable Logic
- Clock Distribution Logic
- Tri-State Bus Buffer
- LED Data Monitor
- Manual User Interface

---

# Features

- Four Addressable Memory Locations
- Eight-Bit Data Storage
- Shared Data Bus Architecture
- Address Decoding
- Clock-Controlled Write Operations
- Manual Read and Write Modes
- Tri-State Output Control
- Bus Contention Protection
- Modular and Expandable Design

---

# Engineering Concepts

This project demonstrates practical implementation of:

- Digital Logic Design
- Sequential Logic
- Register Design
- Computer Memory Architecture
- Address Decoding
- Shared Bus Architecture
- Clock Synchronization
- Write Enable (WE)
- Output Enable (OE)
- Tri-State Logic
- Bus Contention Prevention
- Datasheet Interpretation
- Breadboard Prototyping
- Hardware Debugging
- Modular System Design

---

# Repository Structure

```
JAXIS-4x8-RAM/
│
├── README.md
├── docs/
├── schematics/
├── images/
├── datasheets/
├── pcb/
├── videos/
└── LICENSE
```

---

# Project Progress

## Theory & Design

- [x] Memory Fundamentals
- [x] Register Design
- [x] Address Bus
- [x] Data Bus
- [x] Address Decoder
- [x] Write Logic
- [x] Read Logic
- [x] Tri-State Bus Design
- [x] Bus Contention Analysis
- [ ] Complete Hardware Schematic

## Hardware

- [ ] Breadboard Prototype
- [ ] Functional Testing
- [ ] Hardware Validation
- [ ] PCB Design

---

# Documentation

This repository documents every stage of the engineering process, including:

- Design Requirements
- System Architecture
- Digital Logic Theory
- Schematics
- Hardware Construction
- Testing Procedures
- Validation Results
- Engineering Notes
- Lessons Learned

---

# Future Development

The JAXIS 4×8 RAM is the foundation of a larger computer engineering project.

Future hardware modules include:

- Arithmetic Logic Unit (ALU)
- Register File
- Program Counter
- Instruction Register
- Control Unit
- Custom 8-bit CPU
- Complete Computer System
- Hardware-Controlled Robotic Platform

---

# Design Philosophy

This project emphasizes engineering understanding over replication.

Every subsystem is designed through analysis, experimentation, and verification rather than copying existing reference designs. The objective is to understand the purpose of every signal, component, and connection while developing practical hardware engineering skills.

---

# Author

**Joel Efekele**

Electronics Engineering Technology (A.S.)

Bachelor of Science in Electrical Engineering

**JAXIS Hardware Engineering Project**

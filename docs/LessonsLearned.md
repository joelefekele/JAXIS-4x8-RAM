# Lessons Learned

## Introduction

This document records the technical lessons, engineering insights, and design decisions made throughout the development of the JAXIS 4×8 RAM.

It serves as a record of knowledge gained during the project and documents improvements that may be applied to future hardware designs.

---

# Key Engineering Lessons

## Shared Bus Architecture

One of the most important concepts learned during this project was the implementation of a shared data bus.

Instead of connecting every device directly to one another, hardware modules communicate through a common communication path.

This significantly simplifies wiring and improves system scalability.

---

## Address Decoding

The use of an address decoder allows multiple registers to share the same data bus while ensuring that only one register is selected during a memory operation.

This demonstrated the importance of control logic in digital systems.

---

## Clock Synchronization

Memory contents change only on the active clock edge.

Simply changing the data bus does not modify stored data.

This reinforced the importance of synchronous digital design.

---

## Write Enable Logic

Because the 74HC574 does not include a dedicated Write Enable input, a custom three-input AND gate circuit was developed.

This demonstrated how missing functionality can be implemented using external digital logic.

---

## Tri-State Logic

Tri-state outputs prevent multiple devices from driving the data bus simultaneously.

Understanding High Impedance (Hi-Z) was essential to preventing electrical conflicts.

---

## Bus Contention

Bus contention became one of the most important design considerations.

The addition of the 74HC125 successfully isolated the data input switches during READ operations.

---

## Modular Design

Breaking the RAM into smaller hardware modules simplified both the design process and future debugging.

Each subsystem performs a single dedicated function.

---

## Datasheet Interpretation

Designing the RAM required careful interpretation of integrated circuit datasheets, including pin functions, timing behavior, and electrical characteristics.

---

## Hardware Debugging

The project reinforced the importance of systematic debugging by verifying individual subsystems before testing the complete RAM.

---

# Future Improvements

Possible future improvements include:

- Automatic read selection
- Larger memory capacity
- PCB implementation
- Faster clock generation
- CPU integration
- Complete computer architecture

---

# Personal Reflection

Designing the JAXIS 4×8 RAM strengthened my understanding of digital logic, computer architecture, and hardware design.

Rather than treating memory as a prebuilt component, this project demonstrated how digital memory can be engineered from fundamental logic devices and highlighted the importance of modular design, careful planning, and systematic testing.

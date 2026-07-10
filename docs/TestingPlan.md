# Testing Plan

## Introduction

This document defines the verification procedure for the JAXIS 4×8 RAM. The objective is to validate that every subsystem operates according to the design requirements before the complete memory system is integrated.

Testing is performed incrementally. Each hardware module is verified independently before testing the complete RAM.

---

# Testing Objectives

The testing process is designed to verify:

- Correct register operation
- Correct address decoding
- Proper data bus functionality
- Correct write logic
- Correct read logic
- Proper tri-state buffer operation
- Elimination of bus contention
- Overall system functionality

---

# Test Equipment

The following equipment will be used during testing:

- Breadboards
- Digital Multimeter
- Logic Probe (if available)
- LEDs
- DIP Switches
- Push Buttons
- 5V Power Supply

---

# Test 1 — Power Verification

## Objective

Verify that every integrated circuit receives the correct supply voltage.

## Procedure

- Measure VCC.
- Measure GND.
- Verify correct polarity.

## Expected Result

All ICs receive +5V and Ground correctly.

Status:

⬜ Not Tested

---

# Test 2 — Address Decoder

## Objective

Verify correct operation of the 74HC139.

## Procedure

Apply every address.

```
00
01
10
11
```

Verify that only one decoder output becomes active.

## Expected Result

Exactly one register is selected for every address.

Status:

⬜ Not Tested

---

# Test 3 — Register Storage

## Objective

Verify that a selected register stores data.

## Procedure

- Select one register.
- Apply an 8-bit value.
- Enable WE.
- Press Clock.

## Expected Result

Only the selected register updates.

Status:

⬜ Not Tested

---

# Test 4 — Register Isolation

## Objective

Verify that non-selected registers remain unchanged.

## Procedure

Write data into Register 1.

Read Registers 0, 2, and 3.

## Expected Result

Only Register 1 changes.

Status:

⬜ Not Tested

---

# Test 5 — Data Bus

## Objective

Verify that all registers receive the shared data bus.

## Procedure

Apply multiple data values.

Observe the bus.

## Expected Result

The selected register receives the correct byte.

Status:

⬜ Not Tested

---

# Test 6 — Write Logic

## Objective

Verify the three-input AND gate logic.

Inputs:

- Clock
- Write Enable
- Decoder Output

## Expected Result

Writing occurs only when all three inputs are active.

Status:

⬜ Not Tested

---

# Test 7 — Read Logic

## Objective

Verify that only the selected register drives the data bus.

## Expected Result

The selected register outputs its stored byte.

Status:

⬜ Not Tested

---

# Test 8 — Tri-State Buffer

## Objective

Verify operation of the 74HC125.

## Procedure

During WRITE mode:

- DIP switches drive the bus.

During READ mode:

- DIP switches disconnect.
- Register drives the bus.

## Expected Result

Correct bus isolation.

Status:

⬜ Not Tested

---

# Test 9 — Bus Contention

## Objective

Verify that only one device drives the data bus.

## Expected Result

No bus contention occurs during either READ or WRITE operations.

Status:

⬜ Not Tested

---

# Test 10 — Complete RAM

## Objective

Verify full RAM functionality.

## Procedure

Write and read every address.

```
Address 00

Address 01

Address 10

Address 11
```

## Expected Result

All memory locations store and retrieve data correctly.

Status:

⬜ Not Tested

---

# Validation Criteria

The RAM is considered successfully validated when:

- All tests pass.
- No bus contention is observed.
- All registers store and retrieve data correctly.
- Address decoding functions correctly.
- Read and write operations operate reliably.

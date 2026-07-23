# Register 0

## Overview

Register 0 is the first memory module implemented in the JAXIS 4×8 RAM project.

It serves as the prototype used to validate the RAM architecture before expanding the design to four independent memory locations. The Register 0 implementation includes the complete write path, manual read path, shared data bus, and supporting control logic required to verify correct memory operation.

---

## Objectives

The objectives of the Register 0 prototype are to:

- Validate the JAXIS RAM architecture.
- Verify data storage using a 74HC574 octal D-type flip-flop.
- Test the Address Decoder and JAXIS Write Logic.
- Verify communication over the shared 8-bit data bus.
- Validate manual read operations using Output Enable (OE).

---

## Hardware Overview

The Register 0 prototype includes the following subsystems:

- Address Decoder
- JAXIS Write Logic
- Register 0 (74HC574)
- Shared 8-bit Data Bus
- 74HC125 Data Buffers
- LED Data Display
- Manual Read Logic

---

## Schematic

The EasyEDA schematic for Register 0 is included in this directory.

- `Register0_Schematic.pdf`
- `Register0_Schematic.png`

---

## Hardware Validation

The Register 0 design is validated through breadboard testing.

The following documentation is included:

- Breadboard build
- Hardware photographs
- Test procedures
- Test results
- Demonstration videos

---

## Next Steps

After Register 0 has been fully validated, the remaining register modules will be implemented to complete the JAXIS 4×8 RAM.
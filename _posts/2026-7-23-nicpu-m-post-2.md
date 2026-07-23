# NI-CPU-M

Jul 3, 2026 • nilomat

## NI-CPU-M

The NI-CPU-M is a lightweight and simple CPU designed to be built from CD40xx series ICs.

The goal of this CPU is to keep the design small, understandable, and practical while still being capable of running useful programs.

---

# The Instructions

The instruction is split into two parts.

The first half-byte selects the operation.

The second half-byte is used for register operations (RO).

The RO controls where data is read from or written to.

Example:

1. Get input

   * Select the register to write to using RO.

2. Add registers together

   * Select the destination register using RO.

3. AND registers together

   * Select the destination register using RO.

4. Jump if equal to 0

   * Jump to the address in R1 if R2 is zero.

5. Jump

   * Jump to the address in R1.

---

# Expanded Instruction Set

The planned instruction set contains up to 9 instructions.

| Opcode | Instruction | Description                        |
| ------ | ----------- | ---------------------------------- |
| 0      | INPUT       | Load data into a register          |
| 1      | ADD         | Add registers together             |
| 2      | AND         | Bitwise AND between registers      |
| 3      | JZ          | Jump if R2 is zero                 |
| 4      | JMP         | Jump to R1                         |
| 5      | SUB         | Subtract one register from another |
| 6      | XOR         | Bitwise XOR between registers      |
| 7      | OR          | Bitwise OR between registers       |
| 8      | BSL         | Bit shift left by one bit          |

---

# New Instructions

## SUB

SUB uses the existing adder hardware.

The CPU performs subtraction using two's complement:

```
A - B = A + (~B) + 1
```

This allows subtraction to be added with very little extra hardware.

---

## XOR

XOR adds more flexibility for bit manipulation.

It can be used for:

* Bit toggling
* Comparisons
* Simple logic operations

---

## OR

OR completes the basic logic operations alongside AND and XOR.

---

## BSL (Bit Shift Left)

BSL shifts all bits left by one position.

Example:

```
1011

BSL

0110
```

The highest bit is discarded and a zero is inserted on the right.

Because the shift amount is fixed to one bit, the hardware is very simple and can mostly be implemented with wiring and buffers.

---

# Register Operations

The register operation nibble controls the register source and destination.

Current operations:

1. Write to R1

2. Write to R2

3. Read from R1

4. Read from R2

Registers also act as outputs.

This is done to save hardware complexity and keep the CPU small.

---

# Hardware Design

The NI-CPU-M is designed around simple logic ICs.

The main components are:

* Registers
* Adder
* Logic gates
* Instruction decoder
* Jump logic

The design aims to be buildable using CD40xx series logic ICs while keeping the amount of hardware low.

Design files will be released when the CPU is finished.

first 4 bits are the instruktion and the last 4 bit of the instrution are  the RO.

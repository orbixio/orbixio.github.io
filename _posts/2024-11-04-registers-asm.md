---
title: An Introduction to Registers (Assembly)
description: Registers are small, high-speed storage locations within a CPU that temporarily hold data and instructions for quick access.
author: orbixio
date: 2024-10-31 20:55:00 +0800
categories: [Computer Architecture]
tags: [asm]
pin: true
media_subpath: '/posts/registers_asm'
---

> *Registers high-speed are storage mediums that allow data to be accessed by the processor faster than any other storage medium. They have a limited size of just a few bytes and are used to temporarily store operands, addresses, or instructions.*

### **Size of Registers**

> - *Registers are (typically) the same size as the word width of the architecture.*
> - There are also *sub-registers* that can be used to access part of data stored in registers.

### **Types of Registers**

| **General Registers**          | **Segment Registers** | **Status Registers** | **Instruction Pointer** |
| ------------------------------ | --------------------- | -------------------- | ----------------------- |
| `RAX`, `EAX`, `AX`, `AH`, `AL` | `CS`                  | `EFLAGS/RFLAGS`      | `EIP`, `RIP`            |
| `RBX`, `EBX`, `BX`, `BH`, `BL` | `SS`                  |                      |                         |
| `RCX`, `ECX`, `CX`, `CH`, `CL` | `DS`                  |                      |                         |
| `RDX`, `EDX`, `DX`, `DH`, `DL` | `ES`                  |                      |                         |
| `RBP`, `EBP`, `BP`             | `FS`                  |                      |                         |
| `RSP`, `ESP`, `SP`             | `GS`                  |                      |                         |
| `RSI`, `ESI`, `SI`             |                       |                      |                         |
| `RDI`, `EDI`, `DI`             |                       |                      |                         |
| `R8-R15`                       |                       |                      |                         |

### **Instruction Pointer**
The Instruction Pointer (`rip`, `eip`,`ip`) is special purpose register that holds memory address of the next instruction to be executed by the CPU.

### **General Registers**

![](https://github.com/user-attachments/assets/1be9f97b-a5e7-4fb1-b786-0360a44fc3fc)
_General Purpose Registers (Overview)_

> **Sub-registers**
> Each `64-bit` register can be further divided into smaller sub-registers containing the lower bits, at one byte `8-bits`, 2 bytes `16-bits`, and 4 bytes `32-bits`.
> ![](https://academy.hackthebox.com/storage/modules/85/assembly_register_parts.jpg)

**RAX, EAX, AX, AH & AL (Accumulator Register)** - A general-purpose register in x86-64 architecture, primarily used for storing arithmetic results, system call numbers, and function return values.

**RBX, EBX, BX, BH & BL (Base Register)** - A general-purpose register in x86-64 architecture, primarily used to store base address for referencing an offset. 

> *It is preserved across function calls. The callee is responsible for preserving the `%rbx` register if it plans to modify it. Before modifying it, the callee should push it onto the stack.*

**RCX, ECX, CX, CH & CL (Counter Register)** - A general-purpose register in x86-64 architecture, primarily used in counting operations such as loops, etc. 

**RDX, EDX, DX, DH & DL (Data Register)** - A general-purpose register in x86-64 architecture, primarily used to pass 3rd argument to a function.

**RSP, ESP & SP (Stack Pointer)** - A general-purpose register in x86-64 architecture, primarily points to top of the stack. It automatically updates when new data is pushed onto or popped from the stack.

**RBP, EBP & BP (Base Pointer)** - A general purpose register in x86-64 architecture, primarily used to access parameters passed by the stack. 

> Both `stack pointer` & `base pointer` are used in conjunction with stack segment register

**RSI, ESI & SI (Source Index)** - A general purpose register in x86-64 architecture, primarily used in string operations and is used in conjunction with data segment register as an offset.

**RDI, EDI & DI (Destination Index)** - A general purpose register in x86-64 architecture, primarily used in string operations and is used in conjunction with extra segment register as an offset.

**R8-R15** - Secondary general-purpose 64-bit registers

> *Also addressable in 32-bit, 16-bit, and 8-bit modes.*
>
> *For example, for the R8 register, we can use R8D for lower 32-bit addressing, R8W for lower 16-bit addressing, and R8B for lower 8-bit addressing.*
>
> **Note:** *Here, the suffix D stands for Double-word, W stands for Word, and B stands for Byte.*

### **Status Flag Registers**

> *A status flag register, also known as a flags register, is a register in a computer that holds the current state of a processor*

- ***Zero Flag (ZF)*** - 1 if the last result is zero, indicating equality.
- ***Carry Flag (CF)*** - 1 if the last result overflowed or underflowed, indicating a carry out of the most significant bit.
- ***Sign Flag (SF)*** - 1 if the last result is negative, indicating that the most significant bit is set.
- ***Trap Flag (TF)*** - 1 to enable single-step debugging mode, allowing execution of one instruction at a time for debugging purposes.

> ⚠️ Uncharted Territories
>
> While there are numerous additional status flag registers available, their presence is not essential for basic reverse engineering.

### **Segment Registers**

> Segment Registers are 16-bit registers that convert the flat memory space into different segments for easier addressing.

![](https://github.com/user-attachments/assets/c0fceda9-b8d0-4082-9ae2-7e10c25feb12)


### **Calling Convention**

| Description                     | 64-bit Register | 32-bit Register | 16-bit Register | 8-bit Register |
| ------------------------------- | --------------- | --------------- | --------------- | -------------- |
| **Data/Arguments Registers**    |                 |                 |                 |                |
| Syscall Number/Return value     | `rax`           | `eax`           | `ax`            | `al`           |
| Callee Saved                    | `rbx`           | `ebx`           | `bx`            | `bl`           |
| 1st arg - Destination operand   | `rdi`           | `edi`           | `di`            | `dil`          |
| 2nd arg - Source operand        | `rsi`           | `esi`           | `si`            | `sil`          |
| 3rd arg                         | `rdx`           | `edx`           | `dx`            | `dl`           |
| 4th arg - Loop counter          | `rcx`           | `ecx`           | `cx`            | `cl`           |
| 5th arg                         | `r8`            | `r8d`           | `r8w`           | `r8b`          |
| 6th arg                         | `r9`            | `r9d`           | `r9w`           | `r9b`          |
| **Pointer Registers**           |                 |                 |                 |                |
| Base Stack Pointer              | `rbp`           | `ebp`           | `bp`            | `bpl`          |
| Current/Top Stack Pointer       | `rsp`           | `esp`           | `sp`            | `spl`          |
| Instruction Pointer 'call only' | `rip`           | `eip`           | `ip`            | `ipl`          |

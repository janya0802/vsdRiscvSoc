# Task-5: ABI and Register Cheat Sheet

---

## 🎯 Objective:
To understand the **Application Binary Interface (ABI)** used in RISC-V architecture, and identify the function and usage of different **registers** during a compiled C program execution.

---

### 🧪 What is ABI?

The **ABI (Application Binary Interface)** defines:
- How functions are called
- How parameters are passed (which registers)
- How return values are handled
- Which registers must be preserved (callee-saved)

For RISC-V (RV32IMC), this is crucial for writing assembly, debugging, or interfacing with libraries.


## 🧠 RISC-V Register C(All 32 Registers):


| Register | ABI Name | Description                     | Usage / Convention      |
|----------|----------|----------------------------------|--------------------------|
| x0       | zero     | Constant zero                   | Hardwired to 0           |
| x1       | ra       | Return address                  | Caller-saved             |
| x2       | sp       | Stack pointer                   | Callee-saved             |
| x3       | gp       | Global pointer                  | Reserved                 |
| x4       | tp       | Thread pointer                  | Reserved                 |
| x5       | t0       | Temporary 0                     | Caller-saved             |
| x6       | t1       | Temporary 1                     | Caller-saved             |
| x7       | t2       | Temporary 2                     | Caller-saved             |
| x8       | s0 / fp  | Saved register / Frame pointer  | Callee-saved             |
| x9       | s1       | Saved register 1                | Callee-saved             |
| x10      | a0       | Argument 0 / Return value       | Caller-saved             |
| x11      | a1       | Argument 1 / Return value       | Caller-saved             |
| x12      | a2       | Argument 2                      | Caller-saved             |
| x13      | a3       | Argument 3                      | Caller-saved             |
| x14      | a4       | Argument 4                      | Caller-saved             |
| x15      | a5       | Argument 5                      | Caller-saved             |
| x16      | a6       | Argument 6                      | Caller-saved             |
| x17      | a7       | Argument 7                      | Caller-saved             |
| x18      | s2       | Saved register 2                | Callee-saved             |
| x19      | s3       | Saved register 3                | Callee-saved             |
| x20      | s4       | Saved register 4                | Callee-saved             |
| x21      | s5       | Saved register 5                | Callee-saved             |
| x22      | s6       | Saved register 6                | Callee-saved             |
| x23      | s7       | Saved register 7                | Callee-saved             |
| x24      | s8       | Saved register 8                | Callee-saved             |
| x25      | s9       | Saved register 9                | Callee-saved             |
| x26      | s10      | Saved register 10               | Callee-saved             |
| x27      | s11      | Saved register 11               | Callee-saved             |
| x28      | t3       | Temporary 3                     | Caller-saved             |
| x29      | t4       | Temporary 4                     | Caller-saved             |
| x30      | t5       | Temporary 5                     | Caller-saved             |
| x31      | t6       | Temporary 6                     | Caller-saved             |





## ✅ Summary
a0–a7 (x10–x17): Function arguments and return values

s0–s11 (x8–x9, x18–x27): Saved across calls

t0–t6 (x5–x7, x28–x31): Temporaries

x0: Always 0

x1 (ra): Used to return from functions

x2 (sp): Points to top of stack


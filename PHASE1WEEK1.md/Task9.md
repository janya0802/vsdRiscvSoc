# Task-9: Inline Assembly Basics

---

## 🎯 Objective:
To explore how **inline assembly** works in C using the RISC-V architecture. This task helps understand how C can directly interact with hardware-level instructions and registers.

---
## EXAMPLE 1 : Adding Two Integers

### 📁 Step 1: Write the Inline Assembly C Program (nano inline_add.c) 

We created a simple C file to perform addition using inline RISC-V assembly:
![image](https://github.com/user-attachments/assets/050c192d-81fd-4856-9616-72589221d8fe)

This code tells the compiler to use the add RISC-V instruction to add a and b, storing the result in the result variable.

### 🛠️ Step 2: Compile the Program 
using command - riscv32-unknown-elf-gcc -S -o inline_add.s inline_add.c

### Output - 
![image](https://github.com/user-attachments/assets/aa9dbe27-6029-4821-a9cc-81846c2bbbaf)
![image](https://github.com/user-attachments/assets/b923931d-081b-4566-99d9-e45284c92b35)

### 🔍 Step 3: Analyze the Assembly Output
We observed that the generated assembly file contains:

Assembly instructions like li, lw, and add

Our inline add instruction embedded directly

Return values passed through a5

## 🔧 EXAMPLE 2: Using Named Operands and Memory Storage

### Step 1: Storage Source Code (inline_add_mem.c)
![image](https://github.com/user-attachments/assets/d0358bf2-a31a-4c2b-9558-82adc25fdf0a)
This version uses __asm__ volatile to prevent the compiler from optimizing away the assembly, and achieves the same addition logic in a slightly different style.

## Step 2 : 🛠️ Compilation Command - 
riscv32-unknown-elf-gcc -S -o inline_add_mem.s inline_add_mem.c

## Output -
![image](https://github.com/user-attachments/assets/f3259696-7fc4-406d-b2fc-1e59157c033f)

## 🔍 Observations
%0, %1, and %2 correspond to result, x, and y

Register allocation is performed automatically by the compiler

You avoid extra memory operations by computing directly in registers

## ✅ Use:
Inline assembly allows direct interaction with the processor

Great for writing device drivers, bit manipulation routines, or cryptographic primitives

Allows finer performance tuning in embedded systems

## 🧩 Summary Table:
| Feature              | Explanation                                         |
| -------------------- | --------------------------------------------------- |
| Inline Assembly      | Embeds RISC-V assembly into C programs              |
| `asm` vs `__asm__`   | Both work; `__asm__ volatile` prevents optimization |
| Register Constraints | `"=r"` for outputs, `"r"` for inputs                |
| Volatile Keyword     | Ensures instruction is kept during compilation      |

## Question 2 : Breakdown of =r and volatile as used in inline assembly:

## 🧩 =r — Output Register Constraint
=r is a GCC constraint used in inline assembly to tell the compiler:

= means this is an output operand (the assembly instruction will write to it).

r means the output should be stored in a general-purpose register.

#### 🔍 Example: 
![image](https://github.com/user-attachments/assets/8591f22e-3b24-4109-b7b7-60f6edb0909c)
%0 refers to the result variable.

The compiler will assign a register to result, and the add instruction will store its output there.

## 🧩 volatile — Prevent Compiler Optimization
The volatile keyword in __asm__ volatile tells the compiler not to remove or rearrange the assembly code, even if it thinks it's unnecessary.

Without volatile, the compiler may optimize away the inline assembly if it believes the result isn’t used.

#### 🔍 Example:
![image](https://github.com/user-attachments/assets/577d5d5a-e763-4a50-9887-85b3cc9bba61)
This ensures:
The instruction is always included in the final binary.
Useful when you're writing to hardware or relying on side effects.

### ✅ Summary - 
| Term       | Meaning                                                             |
| ---------- | ------------------------------------------------------------------- |
| `=r`       | Output to a general-purpose register                                |
| `__asm__`  | Tells GCC you’re writing inline assembly                            |
| `volatile` | Ensures the assembly code is **not optimized away** by the compiler |










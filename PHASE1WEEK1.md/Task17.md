# Task 17: Endianness & Struct Packing

---

## 🎯 Objective

To determine the **endianness** of the RISC-V architecture using a **union trick** in C, and understand how byte-level data is stored in memory.

---

## 📚 Background

RISC-V by default is **little-endian**, meaning the least significant byte of a word is stored at the lowest memory address.

This can be verified by using a `union` of `uint32_t` and a `uint8_t[4]` array to inspect the byte layout of a known integer.

---

## 🧠 Concept & Code Explanation

We wrote a C program that stores a 32-bit word `0x01020304` in a union and prints each byte individually to observe the ordering:

![image](https://github.com/user-attachments/assets/ee4588a3-dff9-4bd0-9a8a-1bfa23a63f5d)

## 🔨 Steps to Compile & Run

### 1️⃣ Create endianness.c and syscalls.c
syscalls.c is reused from Task 16. Ensure it contains UART logic for 0x10013000.

### 2️⃣ Compile with Newlib & Bare-Metal Setup
Compile command - riscv32-unknown-elf-gcc -march=rv32imac -mabi=ilp32 -nostartfiles -o endianness.elf endianness.c syscalls.c

### 3️⃣ Verify ELF Output
Command - file endianness.elf

### OUTPUT- 
![image](https://github.com/user-attachments/assets/5681e989-1c50-47cf-be9d-1e0b5a7a3a1e)

#### Disassembled ELF file using a command like:
riscv32-unknown-elf-objdump -d endianness.elf
#### Output - 
![image](https://github.com/user-attachments/assets/e7bcefd9-c85d-4c1e-b4aa-f2016d0654ea)

### 4️⃣ Run with QEMU- 
Command - qemu-system-riscv32 -nographic -machine sifive_e -kernel endianness.elf

### ⚠️ Issues Faced
🧱 No output appeared in QEMU, even after using syscalls.c and verified compilation.

🔍 We used objdump to confirm the ELF is correctly built: riscv32-unknown-elf-objdump -d endianness.elf | less
![image](https://github.com/user-attachments/assets/b1d75006-f383-42b9-bd80-89ff511dc817)

### 📉 Limitation: 
QEMU's sifive_e machine sometimes does not print UART output without additional firmware (like OpenSBI or proper device-tree initialization).

## ✅ Learning Outcome
Understood endianness concept practically on a RISC-V target.

Verified memory byte ordering through union-based pointer manipulation.

Gained hands-on experience with low-level compilation, linking, and execution in QEMU.

Learned how to debug output issues using objdump when the emulator fails

## 🧾 Final Notes
Even though QEMU didn’t show the expected UART output, the ELF was built correctly.

This reinforces the need to test on hardware, or use better-emulated platforms like Spike or Renode when QEMU has peripheral limitations.








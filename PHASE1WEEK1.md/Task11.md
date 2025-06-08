# Task-11: Linker Script 101

---

## 🎯 Objective:
To create and use a **custom linker script** that explicitly places the `.text` section at address `0x00000000` (Flash) and the `.data` section at `0x10000000` (SRAM) for an RV32IMC embedded system.

This is a fundamental skill in bare-metal programming where developers must control memory layout manually.

---

### 📄 Question:
**“Provide a minimal linker script that places `.text` at `0x00000000` and `.data` at `0x10000000` for RV32IMC.”**

---

### 🧠 Concept Summary

| Section  | Purpose                        | Memory Region |
|----------|--------------------------------|---------------|
| `.text`  | Stores program instructions    | Flash (`0x00000000`) |
| `.data`  | Stores initialized global vars | SRAM (`0x10000000`) |

---

### 📝 Step 1: C Program (`linktest.c`)
![image](https://github.com/user-attachments/assets/94d6d3fa-100c-4e30-af85-cb545e1b3706)

### 📝 Step 2: Custom Linker Script (link.ld)
![image](https://github.com/user-attachments/assets/58add4ea-d711-453b-a3c2-5fc7f2c14fba)

 ### 🧠 Explanation:

. = 0x00000000; sets the address pointer for .text

. = 0x10000000; sets the address for .data

### ⚙️ Step 3: Compile with Custom Linker Script
![image](https://github.com/user-attachments/assets/212ffdb1-b2a8-4335-9ca4-6981201ca8cc)
-T link.ld → specifies custom linker script

-nostartfiles → avoids default CRT startup files

### 🔍 Step 4: Verify Section Placement
![image](https://github.com/user-attachments/assets/ee8ab6ef-3bfc-41dc-b27c-87afa03c1904)

## Output: ![image](https://github.com/user-attachments/assets/23e87582-9567-463a-951a-97998802c87d)

.text is correctly placed at 0x00000000

.sdata (a variant of .data) is at 0x10000000

### 📌 Note: .sdata is used by GCC for “small data” section and is expected behavior.

### 🛠️ Tools Used
| Tool                          | Purpose                                      |
| ----------------------------- | -------------------------------------------- |
| `riscv32-unknown-elf-gcc`     | Compiles code using custom linker script     |
| `riscv32-unknown-elf-readelf` | Verifies ELF file structure and section addr |
| `nano` or `vim`               | Editing C and linker script files            |


----


# 🧠 Why Flash vs SRAM Addresses Differ in Embedded Systems

---

### 🔍 Flash Memory vs SRAM — The Basics

In embedded systems, **Flash** and **SRAM** serve different purposes, and their memory addresses are separated for clear architectural and functional reasons.

| Memory Type | Role                                 | Characteristics                       |
|-------------|--------------------------------------|----------------------------------------|
| **Flash**   | Stores the program code (`.text`)    | Non-volatile, Read-only during runtime |
| **SRAM**    | Stores runtime data (`.data`, `.bss`) | Volatile, Read/Write capable           |

---

### 📌 Typical Memory Mapping

| Section    | Address Range     | Memory Type |
|------------|-------------------|-------------|
| `.text`    | `0x00000000`      | Flash       |
| `.data`    | `0x10000000`      | SRAM        |
| `.bss`     | `0x10000000`+     | SRAM        |

Flash and SRAM are physically separate memory blocks in most microcontrollers, and the **linker must place sections at the correct locations** accordingly.

---

### 💡 Why the Separation?

#### 1. **Execution vs Modification**
- Flash is ideal for **storing and executing code**, but **cannot be modified during runtime**.
- SRAM is ideal for **storing variables**, because it's **read/write capable** and **much faster** to access for dynamic data.

#### 2. **Startup Copying**
- At boot, the `.data` section is **copied from Flash to SRAM**, because variables need to be mutable.
- The `.bss` section is initialized to zero in SRAM.

#### 3. **Hardware Design**
- The processor **maps Flash and SRAM to different physical address regions**.
- The microcontroller’s memory controller expects code at Flash addresses and data at SRAM addresses.

---

### 🧠 Real-World Analogy

Imagine Flash as a **read-only instruction manual** placed in a locked cabinet — you can read it but not change it.

SRAM is like a **whiteboard** where you jot down values that change during a meeting — it’s fast, flexible, but erased when you leave (power off).

---

### ✅ Summary Table

| Attribute         | Flash                       | SRAM                       |
|------------------|-----------------------------|----------------------------|
| Read/Write        | Read-only (in normal use)   | Read/Write                 |
| Volatility        | Non-volatile                | Volatile                   |
| Location for      | Program Instructions        | Variables & Buffers        |
| Typical Address   | `0x00000000` (start of Flash)| `0x10000000` (start of SRAM) |
| Speed             | Slower than SRAM            | Very Fast                  |
| Use in Linking    | `.text`, `.rodata`          | `.data`, `.bss`, stack     |

---

### 🔧 Developer Insight:

> Properly separating `.text` and `.data` is **critical** for writing robust linker scripts and ensuring embedded systems boot and run correctly.

## 🎓 Learning Outcomes

---

By completing Task-11, the following key concepts were learned and applied:

1. ✅ **Understanding of Linker Scripts**
   - Learned how to write and apply a minimal custom linker script to control the memory layout of a program.

2. ✅ **Memory Mapping in Embedded Systems**
   - Understood how `.text`, `.data`, and `.bss` sections are placed in Flash and SRAM, respectively.

3. ✅ **Use of `-T` Flag in GCC**
   - Used the `-T` flag to link the C program with a custom script, overriding default memory layout behavior.

4. ✅ **Use of `-nostartfiles`**
   - Compiled without the standard startup files, gaining control over what code is included in the final binary.

5. ✅ **Verifying Memory Layout Using `readelf`**
   - Analyzed the ELF file to confirm the correct placement of sections using `riscv32-unknown-elf-readelf`.

6. ✅ **Practical Insight into Embedded Toolchains**
   - Gained hands-on experience with embedded development tools and how the compiler, linker, and loader work together.

7. ✅ **Why Flash and SRAM Addresses Differ**
   - Understood the architectural reason for separating code and data in memory and how linker scripts manage this.

---

These learnings are foundational for bare-metal programming, firmware development, and embedded system design using the RISC-V toolchain.








# Task-4: Inspect the ELF File

### 🎯 Objective:
To analyze the compiled ELF (Executable and Linkable Format) file using RISC-V tools and understand its internal sections like `.text`, `.data`, and others.

---

## 📝 Step 1: Generate an ELF File (if not already)

Ensure you have a compiled file from previous tasks. You can reuse `hello.elf` from Task 2 or recompile using:

riscv32-unknown-elf-gcc -o hello.elf hello.c

## 📝 Step 2: Inspect the ELF File Using riscv32-unknown-elf-objdump
Run the following command to display all sections and symbols : riscv32-unknown-elf-objdump -D hello.elf

## 📝 Step 3: View File Sections with readelf
riscv32-unknown-elf-readelf -a hello.elf

## 🔍 Output (Example Images)
.text section starts at 0x10000 (contains code)

.data section contains initialized global variables

.bss contains uninitialized data

 ![image](https://github.com/user-attachments/assets/0318e25f-0d6c-4bbb-ab92-22a871b938bb)

 ## ✅ Use:
Helps in verifying whether the ELF was built correctly and gives low-level insight into how memory is organized for a RISC-V program.

----
## questions 
# What is meant by disassembling?

Disassembling is the process of converting machine code back to human-readable assembly code.
It’s a powerful tool that helps developers, reverse engineers, and system programmers understand what a compiled program actually does.

It can be especially useful for debugging low-level issues, such as inspecting:

   Which exact instructions ran
    Whether registers and memory were used correctly
    Whether optimizations or compiler bugs introduced side effects

# ❓ What Do These Columns Mean?
Each line of the output has 4 important parts:
| Column       | Meaning                                                                 |
| ------------ | ----------------------------------------------------------------------- |
| `10074:`     | Memory address (offset from `.text` base) where this instruction starts |
| `00000513`   | Machine code (in hexadecimal) – binary instruction encoding             |
| `li a0,0`    | Assembly instruction – what this binary encodes                         |
| *(optional)* | Comments or annotations (e.g. labels, symbols)                          |





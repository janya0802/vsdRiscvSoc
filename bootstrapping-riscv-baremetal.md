# Phase 1 – Week 1: hello-riscv

---

## 🔹 Question 1: Install and Sanity-Check the Toolchain

**Question**  
“I have downloaded riscv-toolchain-rv32imac-x86_64-ubuntu.tar.gz. How exactly do I unpack it, add it to PATH, and confirm the gcc, objdump, and gdb binaries work?”

Objective: To install and verify a working RISC-V toolchain on a Linux machine.

**Steps Taken**

1. Downloaded the toolchain:
   ```bash
   wget https://vsd-labs.sgp1.cdn.digitaloceanspaces.com/vsd-labs/riscv-toolchain-rv32imac-x86_64-ubuntu.tar.gz
2. Created an install directory and extracted:
  mkdir -p ~/opt
tar -xvzf riscv-toolchain-rv32imac-x86_64-ubuntu.tar.gz -C ~/opt
3. Updated PATH:
echo 'export PATH=$HOME/opt/riscv/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
4. Verified installation:
riscv32-unknown-elf-gcc --version
riscv32-unknown-elf-objdump --version
riscv32-unknown-elf-gdb --version
5. Output- 
riscv32-unknown-elf-gcc (GCC) 14.2.0
riscv32-unknown-elf-objdump (GNU Binutils) 2.40
riscv32-unknown-elf-gdb (GDB) 15.2
6. output image : file:///home/janya/Pictures/Screenshot%20from%202025-06-07%2001-59-05.png

Use: Enables RISC-V program compilation, disassembly, and debugging using open-source tools.


## Question 2: Create a Minimal C File and Compile It

### Question:
“Write the simplest C program and compile it using riscv32-unknown-elf-gcc to produce a working ELF file.”

---
Objective: To write and compile the simplest bare-metal C program using the installed toolchain.

### ✅ What I Did:

1. Opened the terminal and created a new C file:
   
   nano hello.c
2. Wrote the minimal C program:
3. Saved and exited nano:

Press Ctrl + O, then Enter (to save)

Then Ctrl + X (to exit)
4. Compiling the C File : riscv32-unknown-elf-gcc -o hello.elf hello.c
5. Result:
An ELF file named hello.elf was created.

Verified with : file hello.elf
6. output : hello.elf: ELF 32-bit LSB executable, UCB RISC-V, ...
7. Status: Successfully created and compiled a minimal C program into a RISC-V ELF binary
8. output image : file:///home/janya/Pictures/Screenshot%20from%202025-06-07%2002-21-04.png
Use: Validates the toolchain setup and prepares a minimal RISC-V executable (ELF).

## Question 3: Compile C to Assembly (.s file)

---

### 🎯 Objective:
To generate human-readable RISC-V assembly instructions from a C program by compiling it into a `.s` file.

### 🛠 Use:
Understanding how high-level C code is translated into RISC-V assembly during the compilation process.

---

### ✅ What I Did:

1. First, I wrote a simple C program:

int main() {
    int a = 5;
    int b = 10;
    int c = a + b;
    return c;
}


2. Then I compiled it to assembly using: riscv32-unknown-elf-gcc -march=rv32imac -mabi=ilp32 -S -O0 hello.c
3. -S: Generates assembly output instead of machine code

-O0: No optimization (to preserve exact C-to-assembly mapping
4. result : This generated a file named hello.s containing raw RISC-V assembly.
5. Tools Used:
riscv32-unknown-elf-gcc — cross compiler

No extra libraries were required for this step

6. tatus:
Successfully compiled the C code to assembly using -S flag, and the resulting .s file shows instruction-level mapping of high-level operations.
7. output image : file:///home/janya/Pictures/Screenshot%20from%202025-06-07%2015-00-40.png

-----

## Question 4: Disassemble the ELF

### Question:
“How can I disassemble the ELF file and see the actual RISC-V instructions?”

---

Objective: To disassemble the compiled ELF file using objdump and inspect RISC-V instructions.

### ✅ What I Did:

1. Used the RISC-V `objdump` tool to disassemble the `hello.elf` file and inspect the machine instructions.

2. Command used:
   ```bash
   riscv32-unknown-elf-objdump -d hello.elf
3. Sample Output:
hello.elf:     file format elf32-littleriscv

Disassembly of section .text:

00010090 <main>:
   10090:  00000513     li a0,0
   10094:  00008067     ret
| Column     | Meaning                                        |
| ---------- | ---------------------------------------------- |
| `10090:`   | Memory address where the instruction resides   |
| `00000513` | Opcode (hex representation of the instruction) |
| `li a0, 0` | Human-readable assembly instruction            |
4. Bonus – Get Only Opcodes:
To extract just the hex opcodes:riscv32-unknown-elf-objdump -d hello.elf | grep '^ ' | cut -f2
5. Status: ELF disassembled successfully, and opcodes + assembly confirmed to match RISC-V ISA
6. output image - file:///home/janya/Pictures/Screenshot%20from%202025-06-07%2015-21-20.png
7. Use: Helps understand how C code translates to RISC-V opcodes and instructions.

## Question 5: RISC-V ABI and Register Cheat Sheet

---

### 🎯 Objective:
To study the RISC-V ABI (Application Binary Interface) and document the purpose of each general-purpose register.

### 🛠 Use:
The ABI is essential for understanding how functions pass parameters, return values, and how registers are preserved or overwritten during execution — especially during debugging and assembly-level work.

---

### 📘 What is the RISC-V ABI?

The **RISC-V ABI** defines:

- Naming of the 32 general-purpose registers (x0–x31)
- Their aliases (like `a0`, `s1`, `t0`, etc.)
- Their roles (e.g., function arguments, return values, saved temps)

---

### 🧾 Register Cheat Sheet:

| Register | Alias | Role                          | Convention           |
|----------|-------|-------------------------------|----------------------|
| x0       | zero  | Always 0                      | Constant             |
| x1       | ra    | Return address                | Caller-saved         |
| x2       | sp    | Stack pointer                 | Callee-saved         |
| x3       | gp    | Global pointer                | Callee-saved         |
| x4       | tp    | Thread pointer                | Callee-saved         |
| x5–x7    | t0–t2 | Temporaries                   | Caller-saved         |
| x8       | s0/fp | Saved register / frame ptr    | Callee-saved         |
| x9       | s1    | Saved register                | Callee-saved         |
| x10–x11  | a0–a1 | Function arguments / return values | Caller-saved     |
| x12–x17  | a2–a7 | Function arguments             | Caller-saved         |
| x18–x27  | s2–s11| Saved registers               | Callee-saved         |
| x28–x31  | t3–t6 | Temporaries                   | Caller-saved         |

---

### 🛠 Tools Used:

No commands or binaries were required for this task — it was a research and documentation-based question.

---

### 📄 Additional Notes:

- **Caller-saved registers** (like `t0–t6`, `a0–a7`) may be **overwritten** by a called function.
- **Callee-saved registers** (like `s0–s11`) must be **preserved** across function calls.
- The `sp` (stack pointer) and `fp` (frame pointer) help in memory access and stack frame navigation during debugging.

---

### ✅ Status:
Created a complete register cheat sheet based on the RISC-V ABI. This helps immensely while using `objdump`, `gdb`, or writing low-level RISC-V assembly.

---

image : file:///home/janya/Downloads/Screenshot%202025-06-07%20at%2022-38-53%20ques%205%20(PNG%20Image%201920%20%C3%97%201080%20pixels)%20%E2%80%94%20Scaled%20(89%25).png


## Question 6: Debug ELF with GDB – Stepping Through Instructions

---

### 🎯 Objective:
To launch `riscv32-unknown-elf-gdb` on an ELF binary, set a breakpoint, step through instructions, and inspect registers.

### 🛠 Use:
Debugging with GDB helps trace program execution flow and monitor register-level changes — essential in bare-metal and SoC development.

---

### ✅ What I Did:

#### 🔹 Step 1: Compiled C file with debug info

riscv32-unknown-elf-gcc -g -o hello.elf hello.c


2. Compiled using:
riscv32-unknown-elf-gcc -g -o hello.elf hello.c
(-g: Includes debug symbols (required for stepping in GDB)


3. initial Issue with GDB : target sim
Running riscv32-unknown-elf-gdb hello.elf showed this error:error while loading shared libraries: libpython3.10.so.1.0: cannot open shared object file: No such file or directory

4. Fix: Installed Python 3.10 Manually

5. Debugging Flow in GDB:
   a. Start GDB:riscv32-unknown-elf-gdb hello.elf
   b. Inside GDB:target sim
break main
run
step
info registers

6. sample output: 
Breakpoint 1, main () at hello.c:1
(gdb) step
(gdb) info registers
ra     0x00000000
sp     0x80000000
a0     0x00000000
...


7. Tools Used:
riscv32-unknown-elf-gcc (with -g flag)

riscv32-unknown-elf-gdb

Installed libpython3.10 manually to fix runtime error

Used target sim to simulate CPU execution
8. status:
GDB environment successfully setup. Breakpoints, stepping, and register inspection tested and verified.
9. output image: file:///home/janya/Pictures/ques%206%20a%20
                file:///home/janya/Pictures/ques%206%20%20b

## Question 7 - Running ELF on Emulator (UART Output)

---

## 🎯 Objective

To run a compiled RISC-V ELF file on an emulator (like `QEMU`) and observe the output via UART. This tests whether we can interact with UART peripherals on a simulated RISC-V board in a bare-metal environment.

---

## 🧰 Tools and Setup

- **Host OS**: Ubuntu (running on VirtualBox)
- **Compiler**: `riscv32-unknown-elf-gcc` (v14.2.0)
- **Emulator**: `qemu-system-riscv32` (v8.2.2)
- **Board Tried**: 
  - `sifive_e` (works without BIOS)
  - `virt` (requires BIOS file)

---
'''
## 🧪 C Program (`hello_uart.c`)

#define UART0 0x10013000
void _start() {
    volatile char *uart = (char *)UART0;
    const char *msg = "Hello from UART\n";
    while (*msg) {
        *uart = *msg++;
    }
    while (1); // Prevent exit
}

Linker Script ENTRY(_start)

SECTIONS
{
  . = 0x80000000;
  .text : { *(.text*) }
  .data : { *(.data*) }
  .bss  : { *(.bss*) }
}

 Commands Used -
Compiling the ELF:
riscv32-unknown-elf-gcc -nostdlib -T link.ld -o hello_uart.elf hello_uart.c

 Attempt 1: Using sifive_e board:
qemu-system-riscv32 -M sifive_e -nographic -kernel hello_uart.elf


Attempt 2: Using virt board:
qemu-system-riscv32 -M virt -nographic -kernel hello_uart.elf
Unable to find the RISC-V BIOS "opensbi-riscv32-generic-fw_dynamic.bin"

❌ This produced the following error:
Unable to find the RISC-V BIOS "opensbi-riscv32-generic-fw_dynamic.bin"

Tried to fix using:wget https://github.com/riscv-software-src/opensbi/releases/download/v1.3/opensbi-1.3-riscv32-generic/fw_dynamic.bin -O opensbi-riscv32-generic-fw_dynamic.bin
Even after supplying BIOS using:qemu-system-riscv32 -M virt -nographic -bios opensbi-riscv32-generic-fw_dynamic.bin -kernel hello_uart.elf

QEMU loaded but
❌ Still no UART output

Final Status
Despite all attempts using both sifive_e and virt boards, no UART output was received. Compilation and ELF creation succeeded, but no visible output appeared on the UART console.

Learnings and Use
Learned how to create bare-metal C programs targeting RISC-V with UART memory mapping.

Understood differences between QEMU machines (sifive_e vs virt).

Learned how to troubleshoot linker errors, entry points (_start), and BIOS issues.

 Conclusion
This task involved running a UART-based ELF file in QEMU. Even after all corrections — including memory map, UART address, linker setup, and BIOS insertion — no UART output was achieved.

The task highlighted:

The complexity of low-level I/O emulation

How to troubleshoot peripheral output

The importance of carefully reading specs (MMIO, board documentation)

This likely serves as a debugging milestone rather than an output-producing task.

image : file:///home/janya/Pictures/ques%207a
      : file:///home/janya/Pictures/ques%207b 


## Question 8 - Exploring GCC Optimization

---

## 🎯 Objective

To understand the impact of different **GCC optimization levels**, especially between `-O0` and `-O2`, by analyzing the changes in the generated assembly code. This task helps explore how compilers improve performance, reduce instruction count, and remove unnecessary operations in embedded systems programming.

---

## 🧰 Tools and Environment

| Tool / Component         | Version                         |
|--------------------------|----------------------------------|
| OS                       | Ubuntu (running inside VirtualBox) |
| Compiler                 | `riscv32-unknown-elf-gcc` v14.2.0 |
| GCC Optimization Levels  | `-O0`, `-O2`                     |
| Output Format            | Assembly (`.s`) files            |

---

## 📄 C Code: `opt_test.c`

int square(int x) {
    return x * x;
}

int main() {
    volatile int a = 5;
    volatile int b = square(a);
    return 0;
}

Compilation Commands : # Compile with no optimization
riscv32-unknown-elf-gcc -S -O0 opt_test.c -o opt_O0.s

# Compile with optimization level 2
riscv32-unknown-elf-gcc -S -O2 opt_test.c -o opt_O2.s

-S: Tells GCC to generate assembly code.

-O0: No optimization — all code is preserved.

-O2: Performs high-level optimization.

Output Files
Filename	Description
opt_O0.s	Assembly output with -O0
opt_O2.s	Assembly output with -O2

Observed Assembly Differences (diff opt_O0.s opt_O2.s)
<    call square
---
>    li a5, 25

 Reason for Differences-
 | Feature           | -O0                  | -O2                        |
| ----------------- | -------------------- | -------------------------- |
| Function inlining | ❌ Not applied        | ✅ Applied (avoids call)    |
| Constant folding  | ❌ Not performed      | ✅ Performed (`5 * 5 → 25`) |
| Code size         | 🔺 Larger            | 🔻 Smaller                 |
| Instruction count | 🔺 More instructions | 🔻 Fewer instructions      |
| Performance       | 🐢 Slower            | 🚀 Faster                  |

 Conclusion & Learnings- 
 Compiler optimizations eliminate unnecessary runtime operations, such as redundant function calls and calculations.

Using -O2 greatly improves efficiency by applying techniques like:

Constant folding

Function inlining

Dead code elimination

Developers can control performance and size by choosing the right optimization level during compilation.
image - file:///home/janya/Pictures/8a









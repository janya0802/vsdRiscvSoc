# Task-6: Stepping Through Code with GDB

---

## 🎯 Objective:
To step through a RISC-V compiled C program using the **GDB (GNU Debugger)** for detailed observation of register usage, memory layout, and control flow.

---

### 📁 step 1 : create a source file : nano hello.c 

### 📁 Step 2 : Write the code -
---
#include <stdio.h>

int main() {
    int a = 10, b = 20, c;
    c = a + b;
    return c;
}
---

###  🛠️ Step 3 : Compile with GDB Support 
riscv32-unknown-elf-gcc -g -o hello.elf hello.c

### 🧪 Step 4 : Launch GDB
riscv32-unknown-elf-gdb hello.elf

###⚠️ Issue Faced: Missing libpython3.10.so.1.0
riscv32-unknown-elf-gdb: error while loading shared libraries: libpython3.10.so.1.0: cannot open shared object file: No such file or directory

### 🛠️ Fix for libpython Error: 
downloaded python library using sudo apt python3.10 and sudo pythondev3.10 

### 🧭 Step 5 : Use GDB Commands to Explore

(gdb) layout src       # View source code
(gdb) break main       # Set breakpoint at main
(gdb) run              # Start execution
(gdb) next             # Go to next line
(gdb) info registers   # Check register values
(gdb) quit             # Exit GDB



## Output : ![image](https://github.com/user-attachments/assets/dcecd229-e7c5-4d49-aeba-9dd0a375f264)

 ![image](https://github.com/user-attachments/assets/d975c10f-1b5f-43a6-96c3-736d213c2b9f)

 ## ✅ Use:
Enables in-depth debugging of RISC-V binaries

Helps visualize stack, registers, and program flow

Crucial for understanding how your C code runs on hardware

## 🧩 Extra Tools Used:
gdb-multiarch was used as a workaround when riscv32-unknown-elf-gdb failed due to Python library issues.

riscv64-unknown-elf-gcc was used for compatibility.
            


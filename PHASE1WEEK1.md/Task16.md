# ✅ Task 16: Using Newlib `printf` Without an OS

---

## 🎯 Objective

To implement `printf()` functionality in a bare-metal RISC-V system by retargeting the `_write()` syscall to transmit characters to a memory-mapped UART.

---

## 🧠 Background

In embedded systems without an OS, the standard I/O functions like `printf()` do not work by default. Newlib allows us to retarget system calls like `_write()` to a memory-mapped UART, enabling `printf()` output directly to the console via UART.

---

## STEP 1 🛠️ Implementation

### 📄 `uart_printf.c`
![image](https://github.com/user-attachments/assets/bf94f482-4f6d-4ef4-88a0-c00d4beb76d4)

### 📄 syscalls.c 
![image](https://github.com/user-attachments/assets/9e3dd9bc-5faf-4fcd-84a9-319e88501f7d)

### STEP 2 💻 Compilation & Linking
Commands use - 
![image](https://github.com/user-attachments/assets/7b15353e-c1f9-4169-a398-1af50a7a4baf)
This uses:

✅ -nostartfiles to skip default OS-based startup code

✅ Custom syscalls.c to handle _write() system call

 ### Output - ![image](https://github.com/user-attachments/assets/0016b6d9-bbc1-4618-9864-983d35738308)

 ### STEP 3 ▶️ Run on QEMU - 
 Command used - qemu-system-riscv32 -nographic -machine sifive_e -kernel uart_printf.elf

### OUTPUT - ![image](https://github.com/user-attachments/assets/653c9bb0-864f-45ee-8c24-78ad4d16d5ea)

### ⚠️ Observations & Issues
| Observation                          | Status            |
| ------------------------------------ | ----------------- |
| Program compiled successfully        | ✅ Yes             |
| `_write()` correctly linked and used | ✅ Yes             |
| QEMU did not display UART output     | ❌ No output shown |

### 🧪 Debugging & Flaws - 

#### ❌ Flaw:
Despite setting UART address to 0x10013000 (QEMU sifive_e machine default), no output appeared.

#### 🔍 Cause:
QEMU’s sifive_e UART is not automatically initialized unless a full system/firmware (like OpenSBI) is booted.

#### ✅ Fix Tried:
Used correct UART address (0x10013000)

Added _exit(0) to flush output

Verified _write is present using: riscv32-unknown-elf-nm uart_printf.elf | grep _write

## ✅ Learning Outcomes
Gained hands-on experience with Newlib syscall retargeting

Understood the use of -nostartfiles for bare-metal builds

Learned how to link and test custom _write() handlers

Explored UART limitations in simulated environments like QEMU

## 🔚 Conclusion
This task gave practical exposure to building a fully bare-metal application with standard C library support. Though the UART output was not visible due to QEMU limitations, the compilation, linking, and syscall mechanics worked correctly.

In a real hardware setup or UART-initialized QEMU, this would print: Hello via UART!



 








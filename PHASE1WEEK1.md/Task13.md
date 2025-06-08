# 🧠 Task-13: Interrupt Primer - Machine Timer Interrupt (MTIP)

---

## 🎯 Objective
To implement a basic **Machine Timer Interrupt (MTIP)** on a RISC-V system, using both **C and assembly**, and validate it through QEMU and debugging tools.

---

## 🛠️ Tools Used
- `riscv32-unknown-elf-gcc` 🧰 (GCC 14.2.0)
- `riscv32-unknown-elf-ld` 🔗
- `riscv32-unknown-elf-objdump` 🔍
- `riscv32-unknown-elf-nm` 📌
- `QEMU` Emulator v8.2.2 💻

---

## 📜 Steps Performed

### ✅ Step 1: Write Startup Assembly
File: `interrupt_start.s`

Sets `mtvec` and prepares the stack:

.section .init
.globl _start
_start:
    la sp, _stack_top
    la t0, handle_mtimer_interrupt
    csrw mtvec, t0
    call main
    j .

### ✅ Step 2: Write C Interrupt Handler
File: task13_timer_interrupt.c

![image](https://github.com/user-attachments/assets/06c82fbe-05ef-4cdc-a930-c4e70e28e1ac)

### ✅ Step 3: Create Linker Script
File: interrupt.ld

![image](https://github.com/user-attachments/assets/a122ca7f-9d28-4d00-bbaf-59d64fc29324)

### ✅ Step 4: Compilation Commands
riscv32-unknown-elf-gcc -march=rv32imac_zicsr -c interrupt_start.s -o interrupt_start.o
riscv32-unknown-elf-gcc -march=rv32imac_zicsr -c task13_timer_interrupt.c -o task13_timer_interrupt.o
riscv32-unknown-elf-ld -T interrupt.ld interrupt_start.o task13_timer_interrupt.o -o task13_timer_interrupt.elf

#### ✅ ELF file generated:
file task13_timer_interrupt.elf
# ➜ ELF 32-bit LSB executable, UCB RISC-V, RVC, statically linked

#### 🧠 Interrupt handler visible:
riscv32-unknown-elf-nm task13_timer_interrupt.elf | grep interrupt
 ➜ 0000000c T handle_mtimer_interrupt

### ⚙️ CSR Instructions Verification
command used - riscv32-unknown-elf-objdump -d task13_timer_interrupt.elf | grep -A 10 -B 5 "csr"
✅ Verified: Presence of csrw, csrr, confirming interrupt setup.
![image](https://github.com/user-attachments/assets/de716e65-9d76-43cb-8cc5-c37ed533e3db)

### 🧪 Step 5: Run on QEMU
command - qemu-system-riscv32 -machine sifive_e -nographic -kernel task13_timer_interrupt.elf
![image](https://github.com/user-attachments/assets/e95d862d-7e45-4761-a4f8-17b4000ebe93)
❌ No output appeared on terminal.


### 🔍 Debug Observation:
Although no UART output appeared on screen, the ELF compiled correctly and included CSR operations.

### 🧰 Debug Tip Used:
To manually verify ELF contents: riscv32-unknown-elf-objdump -d task13_timer_interrupt.elf | less

## ❗ Issues Faced
| Issue                    | Resolution                                                   |
| ------------------------ | ------------------------------------------------------------ |
| ❌ No UART output in QEMU | UART not initialized or not supported properly by `sifive_e` |
| ⚠️ Warning: RWX segment  | Harmless during dev, but linker script can be refined        |


## 📘 Learning Outcome
Understood how to configure MTIP (Machine Timer Interrupt) in bare-metal RISC-V.

Practiced writing startup assembly to set mtvec.

Used CSR instructions for interrupt configuration.

Learned how to verify and debug with objdump, nm, and QEMU.










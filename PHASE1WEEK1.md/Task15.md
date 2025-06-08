# 🔒 Task 15: Atomic Test Program – Two-Thread Mutex using `lr.w` / `sc.w`

---

## 📌 Objective

To implement a **mutual exclusion (mutex)** mechanism in bare-metal RISC-V RV32 using **atomic instructions `lr.w` (load-reserved)** and **`sc.w` (store-conditional)**.  
This simulates two threads attempting to acquire a shared resource (lock) safely using a spinlock strategy.

---

## 🧠 Concept Overview

RISC-V's `'A'` extension (atomic) introduces hardware instructions to perform atomic operations.

### 🔸 `lr.w` — Load Reserved  
Reads a value from memory and reserves the address for an upcoming atomic write.

### 🔸 `sc.w` — Store Conditional  
Stores a new value only if no one else wrote to that address since the `lr.w`. If the reservation is lost, the store fails.

These two together are used to implement **atomic spinlocks**.

---

## 🧪 Code Implementation

### ✅STEP1 - Source: `mutex_lrsc.c`
![image](https://github.com/user-attachments/assets/10739b05-ee96-414a-9be5-b6a3aeb17a1f)

## 🛠️ STEP 2 - Compilation Steps 
Command used - riscv32-unknown-elf-gcc -march=rv32imac -mabi=ilp32 -o mutex_lrsc.elf mutex_lrsc.c

## 🔍STEP 3 -  Step-by-Step Verification -
### PART  1️⃣ Check for atomic instructions:

Command used - riscv32-unknown-elf-objdump -d mutex_lrsc.elf | grep -A 5 "lr.w"

## OUTPUT - 
![image](https://github.com/user-attachments/assets/6ce8033e-3954-4206-a080-31599f37a5aa)

### PART 2 🧪 Emulator Execution (QEMU)
Command used - qemu-system-riscv32 -nographic -machine sifive_e -kernel mutex_lrsc.elf

## OUTPUT - 
![image](https://github.com/user-attachments/assets/29927f00-3cd6-4217-9d63-f80dffa501ca)

## ✅ Observations:
No UART output is expected unless explicitly implemented.

However, the ELF runs successfully on QEMU without errors.

## 💡 Learning Outcomes
Understood how atomic instructions work using lr.w/sc.w.

Implemented a spinlock to simulate a mutex between two pseudo-threads.

Verified atomic instructions via objdump.

✅ Confirmed compatibility by running the binary on QEMU (sifive_e).

## 📎 Additional Notes
This task doesn't produce UART output because no UART memory-mapped I/O is included.

If UART output is required, the implementation must include memory-mapped console logic.

The implementation focuses purely on atomic synchronization primitives in bare-metal RISC-V.









# 🧠 Task 14: rv32imac vs rv32imc – What’s the “A”?

## 📌 Objective
To explore and demonstrate the 'A' extension (Atomic Instructions) in the RISC-V instruction set by writing a simple C program and verifying its execution using the RISC-V toolchain and QEMU.

## 🧩 What is the 'A' Extension?
The 'A' in rv32imac stands for Atomic.
It enables a special class of Read-Modify-Write (RMW) instructions that are executed atomically, i.e., without interruption.

These are critical in concurrent systems such as:

Multi-core processors

Operating system kernels

Interrupt service routines

Lock-free data structures (e.g., queues, stacks, semaphores)

## 📜 Atomic Instructions Introduced by 'A': 

| Instruction | Meaning             | Use Case Example                                      |
| ----------- | ------------------- | ----------------------------------------------------- |
| `lr.w`      | Load Reserved       | Begin an atomic read-modify-write sequence            |
| `sc.w`      | Store Conditional   | Complete an atomic update if no interference occurred |
| `amoadd.w`  | Atomic Memory Add   | Atomically increment a shared counter                 |
| `amoswap.w` | Atomic Swap         | Replace a variable’s value and return the old one     |
| `amoor.w`   | Atomic OR           | Set bits atomically                                   |
| `amoand.w`  | Atomic AND          | Clear bits atomically                                 |
| `amoxor.w`  | Atomic XOR          | Toggle bits atomically                                |
| `amomin.w`  | Atomic Min (signed) | Shared minimum computation                            |
| `amomax.w`  | Atomic Max (signed) | Shared maximum computation                            |

----

## 🔧 Implementation (C Program using amoadd.w) : 

## 🔹STEP 1 : create - atomic_demo.c:
![image](https://github.com/user-attachments/assets/0dd974aa-1bf9-4954-84f9-8d0b9999ca06)

### ⚙️ Commands Executed : 

## ✅ STEP 2 - Compilation (with rv32imac architecture):
Using command : riscv32-unknown-elf-gcc -march=rv32imac -mabi=ilp32 -o atomic_demo.elf atomic_demo.c

## 🔍 Step 4 - Disassembly to Confirm Instruction: 
Using command : riscv32-unknown-elf-objdump -d atomic_demo.elf | grep amo

## OUTPUT - 
![image](https://github.com/user-attachments/assets/135bc1a2-f9a1-41a6-b07f-0a71d3681234)

## 🧪 STEP 5 - QEMU Execution
Using command - qemu-system-riscv32 -nographic -machine sifive_e -kernel atomic_demo.elf

## OUTPUT - 
![image](https://github.com/user-attachments/assets/5a970746-26f3-45e2-afe7-652557f6b110)\

## 📝 Observations:
❌ No UART output (as none was coded)

✅ No QEMU crash or runtime errors

✅ Confirms atomic instruction is supported and linked correctly

## 💡 Learning Outcome
The 'A' extension equips RISC-V with hardware-assisted atomic operations.

These allow safe data sharing between threads, ISRs, or CPU cores.

Validated support through:

Compilation with -march=rv32imac

Instruction presence in disassembly

Successful execution in QEMU without fault










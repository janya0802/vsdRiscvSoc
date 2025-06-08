# Task-12: Start-up Code & crt0

---

## 🎯 Objective

To understand and implement a minimal **`crt0.S` startup code** for a **bare-metal RISC-V program**, which sets up the runtime environment and hands control to the `main()` function.

---

## 📝 What is `crt0.S`?

`crt0.S` is a low-level startup file that runs before `main()` in bare-metal systems. Its typical responsibilities include:

- Setting up the **stack pointer**
- Zeroing the **`.bss` section**
- Jumping to `main()`
- Halting or looping if `main()` returns

---

### 💡 Question

> “What does `crt0.S` typically do in a bare-metal RISC-V program and where do I get one?”

**Answer:**
- It sets up the **stack**, clears **`.bss`**, calls **`main()`**, and optionally loops forever after `main()` returns.
- You can refer to **device-specific startup files** or **Newlib's crt0.S** implementation.

---

### 🧱 Method: Building It All From Scratch

---

### 🧾 Step 1: C Program (`main.c`)
![image](https://github.com/user-attachments/assets/c30400b0-aedb-409b-b8bc-6fa997ac4f40)

### ⚙️ Step 2: Startup Assembly (crt0.S)
![image](https://github.com/user-attachments/assets/b3361bcb-96d8-4038-b142-31feafa6df8e)

### 🗂️ Step 3: Linker Script (crt_link.ld)
![image](https://github.com/user-attachments/assets/512dc1bd-e9ef-4a25-847f-3c5e29a6d586)

### 🧪 Step 4: Compilation & Linking
![image](https://github.com/user-attachments/assets/9d8313e4-cd6d-43d0-a280-5c5003b4d494)

Used -nostdlib to avoid linking default libraries.
Linked startup code, main code, and custom memory layout.

### 🔍 Step 5: Verifying the ELF
![image](https://github.com/user-attachments/assets/eef19d12-4f99-4763-bf98-36cebfd4f88f)

### ✅ Output showed: 
![image](https://github.com/user-attachments/assets/20b51ac5-1c5f-4764-bed2-093b7579d055)

#### Command to check entry point: riscv32-unknown-elf-readelf -h crt.elf | grep "Entry"

### ✅ Output:
![image](https://github.com/user-attachments/assets/eeef3338-37a8-46db-8d51-42a9abdd0e25)

## 🧠 Why This Matters
This task simulates a real embedded boot process — where no OS is present, and the CPU starts executing from a fixed address (like Flash).
crt0.S prepares the system so main() can safely execute.

## 🛠 Tools Used
| Tool                          | Purpose                              |
| ----------------------------- | ------------------------------------ |
| `nano`                        | To create and edit `.c`, `.S`, `.ld` |
| `riscv32-unknown-elf-gcc`     | For cross-compilation                |
| `riscv32-unknown-elf-readelf` | To verify ELF structure              |


## 🎓 Learning Outcomes
✅ Understood how crt0.S works and why it is essential in bare-metal systems

✅ Learned how to manually:

Set the stack

Zero the .bss section

Control entry flow to main()

✅ Created a custom linker script and learned memory mapping in embedded systems

✅ Verified ELF file’s correctness using readelf

✅ Saw how startup code fits into the broader system boot process

✅ Learned the role of entry point and the use of ENTRY() in linker scripts


## Point to device-specific examples or newlib

### 🔧 1. Device-Specific Examples
Each microcontroller or SoC (System on Chip) built on RISC-V might have unique memory maps, peripherals, and initialization needs. So vendors (like SiFive, Kendryte, etc.) often provide their own crt0.S or equivalent startup files tailored for:

Setting up clocks

Initializing specific GPIO or UART

Custom memory regions

Hardware stack location

Flash/SRAM layout

✅ These are called device-specific startup files. You would use these when developing for a particular RISC-V board or chip.

----

### 📚 2. Newlib
Newlib is an open-source C standard library (used in embedded development), and it provides a generic but portable crt0.S and system startup code for many RISC-V targets.

If you're not working with a specific chip, Newlib's crt0.S is a good general-purpose option that includes:

Stack pointer setup

__bss zeroing

Calling main()

Defining exit() loop

Default weak definitions of handlers

-----

### 📌 Summary:
If you're working with a real board, refer to that board’s vendor-provided startup files.

For general RISC-V bare-metal work, you can refer to Newlib’s implementation as a reliable and well-maintained starting point.









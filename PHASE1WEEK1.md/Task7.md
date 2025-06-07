# Task-7: Running ELF Under Emulator (QEMU / Spike)

---

## 🎯 Objective:
To run a compiled RISC-V ELF binary using **QEMU** or **Spike** emulator and observe UART-style output in a simulated hardware environment.

---

### 📁 Step 1: Compile the Source with Linker Script

A minimal bare-metal program was written to print a message via UART:

#define UART 0x10000000
void main() {
    volatile char *uart = (char *)UART;
    *uart = 'A';  // Attempt to send 'A' over UART
}

A custom linker script (link.ld) was used:
SECTIONS {
    . = 0x10000;
    .text : { *(.text*) }
    .data : { *(.data*) }
    .bss  : { *(.bss*)  }
}

## step 2 : compile files : 
riscv32-unknown-elf-gcc -T link.ld -nostartfiles -o hello.elf hello.c

### ⚠️ Issue 1: _start not found
ld: warning: cannot find entry symbol _start; defaulting to 00010000
#### ✅ This is expected because -nostartfiles is used and no _start is defined. It's fine for minimal embedded testing.

![image](https://github.com/user-attachments/assets/1abee07e-633a-45e3-92c3-cb0f53469793)


### 🛠️ Step 3: Try Running with QEMU (sifive_e or virt)
qemu-system-riscv32 -machine sifive_e -nographic -kernel hello.elf

![image](https://github.com/user-attachments/assets/2f2b9a06-ab90-463f-bcb9-16188d5a5e69)


### ⚠️ Issue 2: Default sifive machine did not simulate UART
command tried - qemu-system-riscv32 -machine virt -nographic -kernel hello.elf

### ⚠️ Error:Unable to find the RISC-V BIOS "opensbi-riscv32-generic-fw_dynamic.bin"
This BIOS file is required for virt mode. Without it, qemu-system-riscv32 cannot boot.

### 🛠️ Attempted Fixes:
Tried adding OpenSBI firmware manually

Explored alternative machines like sifive_u, but UART still did not show output

Consulted peers and learned that the question is designed to fail without fixing the UART memory mapping or adding startup code

### 🧪 Step 4: Tried with Spike
spike hello.elf

#### ⚠️ No UART output observed — likely due to absence of trap handler or console support in ELF.

## 🧩 Final Outcome:
Despite multiple emulator types (QEMU, virt, spike), no observable UART output was produced. It was later confirmed that this was intentional to test debugging and system exploration skills.

## ✅ Use:
Get hands-on experience running ELF binaries in emulators

Understand machine configuration and UART-mapped I/O limitations

Learn emulator expectations (e.g. OpenSBI in virt)

## 🧩 Tools Used:
riscv32-unknown-elf-gcc

qemu-system-riscv32

spike

link.ld (custom linker script)

## 🧱 Summary:
| Attempt          | Result                         |
| ---------------- | ------------------------------ |
| QEMU (sifive\_e) | No output (UART not simulated) |
| QEMU (virt)      | BIOS missing (`opensbi`) error |
| Spike            | Ran, but no visible output     |

## 📌 Suggestion:
Future tasks should include proper startup code, UART drivers, or OpenSBI firmware to allow UART simulation.






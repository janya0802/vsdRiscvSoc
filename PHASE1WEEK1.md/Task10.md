# Task-10: Memory-Mapped I/O Demo

---

## 🎯 Objective:
To demonstrate how to toggle a GPIO (General Purpose Input/Output) register using a **bare-metal C program** by accessing a memory-mapped address directly. This helps understand **low-level hardware control** in embedded systems.

---

## 📄 Question:
**"Show a bare-metal C snippet to toggle a GPIO register located at `0x10012000`. How do I prevent the compiler from optimizing the store away?"**

---

### 🔧 Concept: Memory-Mapped I/O

- In embedded systems, **peripherals (like GPIO)** are mapped to specific memory addresses.
- You can control them by reading from or writing to those addresses using pointers.
- **Volatile** is necessary to ensure the compiler does not optimize away the access.

---

### 📁 Step 1: Source Code (`gpio_toggle.c`)

#define GPIO_REG (volatile uint32_t*)0x10012000

void main() {
    *GPIO_REG = 0x1;
}
### 🛠️ Step 2: Compile the Program
riscv32-unknown-elf-gcc -o gpio.elf gpio_toggle.c

### 🧪 Step 3: Verify the Store Instruction
riscv32-unknown-elf-objdump -d gpio.elf

![image](https://github.com/user-attachments/assets/fbc3d834-8b38-4688-913b-71a7fb09073a)


## Output - ![image](https://github.com/user-attachments/assets/0750b8c1-ae79-4955-8d01-3f1f68ee96ed)

## ✅ Use:
| Use Case                     | Why It’s Important                               |
| ---------------------------- | ------------------------------------------------ |
| Bare-metal programming       | Directly controls hardware with no OS overhead   |
| Embedded peripheral control  | Toggling GPIO, UART, Timers, etc.                |
| Preventing code optimization | Ensures that critical I/O operations stay intact |

## 🧱 Summary:
Memory-mapped I/O enables direct hardware access.

volatile is crucial to prevent unwanted compiler optimization.

Successfully verified write operation via disassembly (objdump).

# VOLATILE AND ALIGNMENT :

## 🔍 Explanation of volatile
Tells the compiler that the memory at that address may change outside the program's control (like by a hardware peripheral).

Prevents the compiler from skipping or reordering read/write operations.

Essential for memory-mapped I/O, interrupt handling, and concurrent programming.

## 📐 Memory Alignment- 
Alignment refers to how data is stored in memory at specific address boundaries, usually based on the size of the data type.

#### 🧠 Why Alignment Matters:
On most architectures (including RISC-V), accessing misaligned data (e.g., reading a 4-byte integer from an address that’s not divisible by 4) can:

Cause exceptions

Slow down execution

Break memory-mapped hardware communication

### ✅ Summary:
| Concept    | Description                                                            |
| ---------- | ---------------------------------------------------------------------- |
| Alignment  | Storing variables at memory addresses that are multiples of their size |
| Importance | Prevents crashes and ensures fast memory access                        |
| In I/O     | Ensures correct hardware register communication                        |

## 💡 Tip:
Always ensure memory-mapped addresses in your embedded code are naturally aligned to the size of the data you’re working with.









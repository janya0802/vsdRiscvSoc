# 🚀 bootstrapping-riscv-baremetal – Phase 1 Week 1  
### 🔧 Toolchain Exploration • 🧠 Architecture Understanding • 🖥️ Bare-Metal Programming

---

## 📘 Overview

This repository documents all the work completed during **Week 1 of the Phase 1 VSD RISC-V SoC Internship**. It consists of **16 hands-on tasks** that build foundational skills in RISC-V architecture, toolchain usage, inline assembly, memory-mapped I/O, linker scripts, emulation, and debugging — all in a **bare-metal environment** on Linux.

The objective of this phase is to gain practical exposure to open-source EDA tools and to **develop a strong understanding of low-level embedded development** using the RISC-V instruction set architecture.

---

## 🧪 What This Week Covers

| Task No. | Title                             | Key Focus                                    |
|----------|-----------------------------------|----------------------------------------------|
| Task 1   | Toolchain Setup                   | Install and configure RISC-V GNU toolchain   |
| Task 2   | Hello World (Bare-Metal)          | Compile first C program for RISC-V           |
| Task 3   | C to Assembly Conversion          | Generate and interpret RISC-V assembly       |
| Task 4   | ELF Analysis                      | Inspect sections in the ELF binary           |
| Task 5   | ABI and Register Cheat Sheet      | Understand calling conventions and registers |
| Task 6   | Debugging with GDB                | Use GDB to step through RISC-V binaries      |
| Task 7   | Running on Emulator               | Simulate ELF execution using QEMU/Spike      |
| Task 8   | GCC Optimization Exploration      | Compare assembly at different optimization levels |
| Task 9   | Inline Assembly Basics            | Embed RISC-V instructions inside C           |
| Task 10  | Memory-Mapped I/O Demo            | Write to peripheral registers in memory      |
| Task 11  | Linker Script 101                 | Create and use a custom linker script        |
| Task 12  | Startup Code Analysis             | Understand startup and reset flow            |
| Task 13  | Interrupt Vector Table            | Set up interrupt service routines            |
| Task 14  | Timer Interrupt Demo              | Handle timer-based interrupts                |
| Task 15  | Structs and Unions in Memory      | Understand layout of C structures            |
| Task 16  | Endianness & Packing              | Explore byte-ordering and struct padding     |

---

## 🛠️ Tools & Technologies Used

- **RISC-V GCC Toolchain** (riscv32-unknown-elf-gcc)
- **GNU Debugger (GDB)**
- **QEMU Emulator** (riscv32-sifive or virt)
- **Spike RISC-V ISA Simulator**
- **Linux Terminal (Ubuntu on VirtualBox)**
- **Makefiles & Custom Linker Scripts**
- **Assembly Inspection Tools** (objdump, readelf, etc.)

---

## 🎯 Learning Outcomes

✅ Understand how to configure and use a RISC-V toolchain  
✅ Compile and analyze bare-metal C programs  
✅ Learn inline assembly and memory-mapped I/O  
✅ Debug and inspect binaries with GDB and objdump  
✅ Simulate real hardware behavior via QEMU  
✅ Write and modify minimal linker scripts  
✅ Build a full low-level development flow from source to emulator

---




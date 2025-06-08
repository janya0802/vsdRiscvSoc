# Task-1: 🛠️ Install & Sanity-Check the RISC-V Toolchain

The goal is to download, install and verify the risc-v toolchain on pc.

## 🎯 Objective :
To install and verify a working RISC-V toolchain on a Linux machine.

## Step 1: 📥 Download the Toolchain

Download the RISC-V toolchain from the following link:
🔗 riscv-toolchain-rv32imac-x86_64-ubuntu.tar.gz

## Step 2: 📂 Extract the Toolchain
Open a terminal and run:
 cd ~/Downloads
 tar -xzf riscv-toolchain-rv32imac-x86_64-ubuntu.tar.gz
 
 ## Step 3: ⚙️ Add Toolchain to PATH
 Edit your ~/.bashrc file and add the toolchain to your PATH:

➡️vim ~/.bashrc
#### Add the following line at the end of the file:
export PATH=$PATH:~/Downloads/riscv-toolchain-rv32imac-x86_64-ubuntu/bin

## Step 4: ✅ Verify the Installation
Check if the toolchain is installed correctly:
riscv32-unknown-elf-gcc --version
riscv32-unknown-elf-objdump --version

## 🖥️ output - 


### riscv32-unknown-elf-gcc (GCC) 14.2.0
![image](https://github.com/user-attachments/assets/4bdc14db-5cb2-46c7-a487-b77deef98ade)

### riscv32-unknown-elf-objdump (GNU Binutils) 2.40
![image](https://github.com/user-attachments/assets/26129e4f-fcc0-470f-868c-a6abaf8bca6c)

### riscv32-unknown-elf-gdb (GDB) 15.2 
![image](https://github.com/user-attachments/assets/7579e28d-2c3a-4c11-98ff-f2bf8471b9ef)

## 🧰 Tools Used
🔧 riscv32-unknown-elf-gcc – RISC-V cross compiler

🪓 riscv32-unknown-elf-objdump – Disassembler

🐞 riscv32-unknown-elf-gdb – Debugger

💻 Ubuntu (via VirtualBox or native)

## 📌 Use
This setup enables:

✅ Cross-compiling C programs for RISC-V architecture

✅ Debugging and disassembling binaries

✅ Starting all upcoming bare-metal RISC-V tasks

## 📘 Learning Outcome
Learned to install and configure a cross-toolchain for a non-native architecture (RISC-V).

Understood how PATH works and how to verify environment setup.

Gained confidence in handling Linux terminal and open-source binaries.

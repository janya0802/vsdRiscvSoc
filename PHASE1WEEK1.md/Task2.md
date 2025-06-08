# Task-2: Compile "Hello, RISC-V"

## 🎯 Objective:
##### To write and compile the simplest bare-metal C program using the installed toolchain.
---

We will write a very basic hello world kind of program in c and will cross-compile for rv32imc architecture, and verify the output elf file.

---
## Step 1: 💻 Create the Source File

Create a file named hello.c:
nano hello.c

Paste the following code into hello.c:
#include <stdio.h>

int main()
{
    printf("Hello, RISC-V!");
    return 0;
}


## Step 2: 💻  Compile for RISC-V
riscv32-unknown-elf-gcc -o hello.elf hello.c

## Step 3: 💻 Verify the Output File
Check that the compiled file is an ELF file:
file hello.elf

---- 

## Output : ![image](https://github.com/user-attachments/assets/5440739d-ac77-4f7e-914e-3849dd9679aa)

## Use : Validates the toolchain setup and prepares a minimal RISC-V executable (ELF).






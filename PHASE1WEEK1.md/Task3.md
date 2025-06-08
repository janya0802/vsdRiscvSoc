# Question 3: Compile C to Assembly (.s file)
In this task, we will generate the assembly file for our simple C program and explain the meaning of prologue and epilogue.

## Step 1:  💻 Generate Assembly File
Use the following command to generate the assembly file : riscv32-unknown-elf-gcc -S -O0 hello.c

### Flags used:

  -S: Generate assembly instead of object code.
  -O0: Disable optimizations to see the raw function structure.

### 🧰 Tools Used:
riscv32-unknown-elf-gcc — cross compiler

No extra libraries were required for this step


##output : ![image](https://github.com/user-attachments/assets/aee9979d-af03-47c1-88e2-411279c7b5d4)


##  🧾 Understanding Prologue and Epilogue
###  🧠Prologue

The prologue is the code at the start of a function. It:

   Allocates stack space
   Saves callee-saved registers (like s0, ra)
    Sets up the frame pointer (s0)

###  🧠Epilogue

The epilogue is the code at the end of the function. It:

  Restores saved registers
    Deallocates stack
    Returns to the caller



  



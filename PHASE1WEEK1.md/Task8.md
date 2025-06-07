# Task-8: Exploring GCC Optimization Levels (-O0 vs -O2)

---

## 🎯 Objective:
To compare the assembly output of the same C code compiled with different GCC optimization levels (`-O0` and `-O2`) and observe how optimizations affect register usage and instruction patterns.

---

### 📁 Step 1: Write the Source File ( nano opt.c ) 

We created a simple C program that performs an integer addition:

int add(int a, int b) {
    int result = a + b;
    return result;
}

### 🛠️ Step 2: Compile with -O0 (No Optimization) : 
![image](https://github.com/user-attachments/assets/d6f171fd-4523-4e7b-8cc2-e6d80e91867f)
This generates verbose and unoptimized assembly with extra instructions and variable movement.

### 🛠️ Step 3: Compile with -O2 (High Optimization)
![image](https://github.com/user-attachments/assets/984083ae-c442-456d-bf99-f874fb627170)
This version removes redundant instructions and often computes directly in registers.

### 🔍 Step 4: Compare the Outputs
To compare : diff opt_O0.s opt_O2.s

## Output : 

![image](https://github.com/user-attachments/assets/76049a0b-1b49-41f1-b34f-12648744556c)

----

## 🧠 Observations:

### 🔹-O0 Output (Unoptimized)
Uses multiple instructions to load/store intermediate values

Explicit memory usage (sw, lw)

Function prologue and epilogue always present

Registers used less efficiently

### 🔹-O2 Output (Optimized)
Computation often done directly in registers

Fewer instructions, leaner code

Removes unused variables and simplifies logic

May inline functions or rearrange code for speed

## 🧩 Reason for Differences:
-O0: Compiler prioritizes debuggability and readability over performance. Keeps all variable steps visible.

-O2: Compiler prioritizes performance by reducing instruction count and register pressure, leading to smaller and faster code.

## ✅ Use:
Understanding compiler optimizations helps:

Write more efficient embedded software

Read and debug generated assembly

Control binary size and performance in critical systems

## 🧱 Summary Table : 
| Optimization Level | Code Size | Register Efficiency | Speed  |
| ------------------ | --------- | ------------------- | ------ |
| `-O0`              | Larger    | Low                 | Slower |
| `-O2`              | Smaller   | High                | Faster |



# Question-2: Compiler Optimization Concepts – Dead Code Elimination, Register Allocation, and Inlining

---

### 🎯 Objective:
To understand three key compiler optimization techniques used to improve code performance and efficiency: **Dead Code Elimination**, **Register Allocation**, and **Function Inlining**.

---

### 🧠 Dead Code Elimination

**Definition**:  
Dead Code Elimination (DCE) is a compiler optimization that removes sections of code that do not affect the final output or behavior of the program. These are statements or computations whose results are never used.

**Purpose**:
- Reduce binary size
- Improve runtime efficiency
- Clean up unused variables or branches

**Example Use Case**:  
If a variable is assigned a value but never read, DCE removes that assignment from the final compiled code.

---

### 🧠 Register Allocation

**Definition**:  
Register Allocation is the process by which a compiler assigns program variables to a limited number of CPU registers to minimize memory access.

**Purpose**:
- Improve execution speed by reducing slow memory operations
- Efficiently use the limited number of hardware registers
- Optimize function call performance by managing register usage

**Strategy**:
Compilers use algorithms (like graph coloring) to decide which variables stay in registers and which go to memory (spillover).

---

### 🧠 Function Inlining

**Definition**:  
Inlining replaces a function call with the actual body of the function during compilation. This removes the overhead of a function call and enables further optimizations.

**Purpose**:
- Reduce call overhead
- Allow deeper optimizations like constant folding or loop unrolling
- Improve performance in time-critical functions

**Trade-Off**:
While inlining boosts speed, excessive inlining can lead to increased binary size (code bloat), which may negatively affect memory-constrained systems.

---

### ✅ Conclusion

Together, these optimizations:
- Make compiled code more efficient
- Speed up execution
- Reduce memory and instruction overhead
- Play a crucial role in embedded and low-level system software like RISC-V applications

---







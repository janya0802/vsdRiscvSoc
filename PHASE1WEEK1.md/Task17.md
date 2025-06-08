# Task 17: Endianness & Struct Packing

---

## 🎯 Objective

To determine the **endianness** of the RISC-V architecture using a **union trick** in C, and understand how byte-level data is stored in memory.

---

## 📚 Background

RISC-V by default is **little-endian**, meaning the least significant byte of a word is stored at the lowest memory address.

This can be verified by using a `union` of `uint32_t` and a `uint8_t[4]` array to inspect the byte layout of a known integer.

---

## 🧠 Concept & Code Explanation

We wrote a C program that stores a 32-bit word `0x01020304` in a union and prints each byte individually to observe the ordering:


#include <stdio.h>
#include <stdint.h>

union {
    uint32_t word;
    uint8_t bytes[4];
} endian_test;

int main() {
    endian_test.word = 0x01020304;
    printf("Byte order:\n");
    for (int i = 0; i < 4; i++) {
        printf("byte[%d] = 0x%02x\n", i, endian_test.bytes[i]);
    }
    return 0;
}

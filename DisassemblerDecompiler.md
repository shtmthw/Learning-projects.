## C based Disassembler and Decompiler.

Understand how compiled programs work underneath and eventually      build a small decompiler that can reconstruct high-level C-like code from native machine code.

Primary language: C  
Target architecture: x86-64  
Target executable format: ELF (Linux)

---

## Phase 1 — Understanding Machine Code and Assembly

**Goal:** Understand how source code becomes CPU instructions.

Topics:
- CPU architecture and Instruction Set Architecture (ISA).
- Registers (RAX, RBX, RCX, RDX, RDI, RSI, etc.).
- CPU instructions (MOV, ADD, SUB, JMP, CALL, RET).
- Opcodes and instruction encoding.
- Binary representation, hexadecimal and bits.
- Stack and memory addressing.
- Calling conventions.

Practical work:

1. Write small C programs.
2. Compile them without optimization.
3. Inspect their assembly.

Commands:

    gcc -O0 -c test.c -o test.o
    objdump -d -Mintel test.o

Understand how individual C statements translate into assembly.

---

## Phase 2 — Build a Tiny Disassembler

**Goal:** Build a program that reads raw machine-code bytes and translates them into readable assembly.

Features to implement:

1. Read binary bytes from a file.
2. Identify instruction opcodes.
3. Decode instruction operands.
4. Identify CPU registers.
5. Understand instruction addressing modes.
6. Output readable assembly.

Start with a small subset of x86-64 instructions:
- MOV
- ADD
- SUB
- PUSH
- POP
- CALL
- RET
- JMP

Gradually expand the supported instruction set.

Important: You don't need to implement the entire x86-64 ISA. Start small.

---

## Phase 3 — Understand Executable Formats (ELF)

**Goal:** Understand how Linux stores and organizes compiled programs.

Topics:

- ELF file structure.
- ELF headers.
- Program headers.
- Section headers.
- .text (machine code).
- .data and .rodata.
- Symbol tables.
- Relocations.
- Dynamic linking.
- Shared libraries.

Practical work:

1. Inspect ELF files using `readelf`.
2. Examine sections using `objdump`.
3. Write a small C program that reads ELF headers.
4. Locate the executable's machine-code section.
5. Extract and inspect its bytes.

Commands:

    readelf -h program
    readelf -S program
    readelf -s program
    objdump -d program

---

## Phase 4 — Understand Program Structure

**Goal:** Learn how to identify the logical structure of a compiled program.

Topics:

- Function boundaries.
- Stack frames.
- Calling conventions.
- Control-flow analysis.
- Conditional branches.
- Loops.
- Function calls.
- Data-flow analysis.
- Register and stack variable tracking.

Learn about Control-Flow Graphs (CFGs).

Understand how machine instructions form larger logical structures such as if/else statements, loops and functions.

---

## Phase 5 — Build a Tiny Decompiler

**Goal:** Reconstruct high-level, C-like pseudocode from machine code.

Topics:

- Intermediate Representations (IR).
- Instruction lifting.
- Basic blocks.
- Control-flow graphs.
- Data-flow analysis.
- Variable recovery.
- Type inference.
- Expression reconstruction.
- Control-flow reconstruction.

Implementation progression:

1. Decode machine instructions.
2. Convert instructions into an intermediate representation.
3. Track registers and memory values.
4. Identify function arguments and return values.
5. Recognize arithmetic expressions.
6. Reconstruct conditional statements.
7. Reconstruct loops.
8. Generate readable C-like pseudocode.

Start with extremely simple programs, such as:

    int add(int a, int b) {
        return a + b;
    }

Then gradually work toward:

- Functions with multiple variables.
- Conditional statements.
- Loops.
- Nested functions.
- More complex control flow.

---

## Phase 6 — Explore Existing Reverse Engineering Tools

Once the fundamentals are understood, explore:

- Ghidra — Reverse engineering and decompilation.
- IDA Free — Disassembly and reverse engineering.
- radare2 — Binary analysis framework.
- GDB — Debugging compiled programs.
- Capstone — Disassembly framework.
- Keystone — Assembly framework.
- LLVM — Compiler infrastructure.

Study how professional tools approach disassembly, binary analysis and decompilation.

---

## Final Project

Build a small native x86-64 ELF decompiler.

Input:

    A compiled Linux executable.

Output:

    Reconstructed C-like pseudocode.

Initial limitations are perfectly fine:
- Only support x86-64.
- Only support simple ELF executables.
- Only support a limited subset of instructions.
- Only reconstruct basic arithmetic, functions and conditionals.

Expand its capabilities as understanding improves.

---

## Learning Philosophy

Don't rush to build the full decompiler.

Understand the layers individually:

C → Assembly → Machine Code → ELF

Then reverse the process:

ELF → Machine Code → Disassembly → Intermediate Representation → Reconstructed Pseudocode

The objective isn't necessarily to reproduce the original source code. That is often impossible because compilation loses information.

The objective is to reconstruct the program's logic from its compiled representation.

**Start with Phase 1. Build your own disassembler before attempting the decompiler.**

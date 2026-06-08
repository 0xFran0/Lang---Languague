# LANG: The Minimalist Mid-Level Systems Language

LANG is a minimalist, mid-level systems programming language designed for bare-metal control, firmware development (BIOS), and absolute syntax efficiency. 

Unlike C or C++, LANG eliminates language bloat, header file hell, and rigid boilerplate. It treats hardware resources directly while providing a safe, ultra-compact syntax.

## Why LANG? (The C Destroyer)


| Feature | C / C++ | LANG |
| :--- | :--- | :--- |
| **Main Entry** | Rigid `void main()` | Fully Customizable (e.g., `Hola = {` or `Main = {`) |
| **Memory Allocation** | Complex pointers & `malloc` | Controlled dynamic scaling with `Asing` |
| **Control Flow** | Bulky brackets `{}` and keywords | Continuous single-line expressions with `then` and `tho` |
| **Comments** | Clunky `//` or `/* */` | Sleek and unique `~$` syntax |

## Core Principles & Syntax

### 1. Vertical Continuity Blocks
LANG drops traditional brackets for data allocation, using vertical continuity tokens `/s/` (start) and `//s/;` (stop) to map fields directly onto the processor's stack or memory array.

```go
Type = /s/
    local vga = "0xB8000";        ~\$ Direct physical video buffer mapping
    local color = 0x0A;            ~\$ Matrix green attribute
    local chip_teclado = 0x60;     ~\$ Keyboard I/O hardware port
    local buffer_letras = 0x2000;  ~\$ Free variable allocation in RAM
//s/;
```

### 2. Linear Expressions & Mutators
Instead of nested conditions and complex pointer arithmetic, LANG processes hardware state mutations in fluid, single-line commands using `change ... tho`.

```go
Hola = {
    Console use vga then print;
    
    ~\$ Keypress event handled natively in one line
    if [chip_teclado] = 0x1C then change [buffer_letras] tho 0x00;
}
```

### 3. Native Compile-Time Macro Math
LANG resolves and autovalidates math expressions during compilation, ensuring zero runtime CPU overhead.

```go
Asing Hola = 100;
Hola + Hola + Hola = 300; ~\$ Autovalidated by the compiler before binary generation
```

## Running an OS Shell in QEMU (No Dependencies)
LANG compiles natively into raw, flat binaries of variable size. You can build a fully functional QEMU terminal/shell with no external libraries or calls:

```go
~\$ Save as shell.lang
Type = /s/
    local vga = "0xB8000";
    local chip_teclado = 0x60;
//s/;

Main = {
    Console use vga then print;
    Console L; Console C; Console :; Console >;

    Funtion LeerEntrada;
        Console use chip_teclado then print;
        if [chip_teclado] != 0 then change [0x2000] tho [chip_teclado];
}
```

# NASM Constants Cheatsheet

## Constants

### 1. `%define` / `equ`
Defines a constant value.
```asm
PI equ 3.14159
%define PI 3.14159 
````

### 2. `%set` (Expression-based)

Defines a constant from an expression.

```asm
%set MAX_BUFFER (10 * 1024)
```

## Data Section Constants

Declare constants in `.data`:

```asm
section .data
    my_const db 10          ; byte constant
```

## Memory Allocation

Reserve space in `.bss`:

```asm
section .bss
    buffer resb 256         ; reserve 256 bytes
```

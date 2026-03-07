
# NASM (x86-64)

## 1. Syntax & Directives

- `bits 64`  
  Sets the assembly for 64-bit mode.

- `DEFAULT ABS`  or `DEFAULT REL`
  Change address mode

- `.global _start`  
  Make `_start` visible to the linker (entry point for your program).

- `.intel_syntax noprefix`  
  **Only for as**
  Use Intel-style syntax (instead of AT&T).  
  `noprefix` → no need for `%` on registers.

---

## 2. Basic NASM Workflow

### Assemble & Link
```bash
nasm -f elf64 app.asm -o app.o   # Assemble to object file
ld -o app app.o                  # Link to executable
./app                             # Run
````

### Alternative with `as` (GNU assembler)

```bash
as -o app.o app.s                 # Assemble .s file
ld -o app app.o                   # Link
```
Need : **.intel_syntax noprefix**

---

## 3. Example Skeleton

```asm
bits 64

global _start
_start:
    mov rax, 60        ; syscall: exit
    mov rdi, 0         ; exit code 0
    syscall
```

---

## 4. Notes

* `nasm` uses `.asm` extension typically.
* `as` uses `.s` extension (GNU style).
* Always match `bits 64` with 64-bit registers (`rax`, `rdi`, etc.).



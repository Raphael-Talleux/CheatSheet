# **Bit Shifting Operations**

Bit shifting is used to move bits left or right in a register, often for quick multiplication or division by powers of 2.

---

### **1. Shift Left (`shl`)**

* **Operation**: Moves bits to the left, multiplying the value by ( 2^n ).
* **Syntax**:

  ```asm
  shl reg, cl     ; Shift left by value in cl (0-31)
  shl reg, imm8   ; Shift left by immediate value (0-31)
  ```
* **Example**:

  ```asm
  mov al, 0x8A    ; al = 10001010 (binary)
  shl al, 1       ; al = 00010100 (shift left by 1, multiply by 2)
  ```

---

### **2. Shift Right (`shr`)**

* **Operation**: Moves bits to the right, dividing the value by ( 2^n ), truncating the remainder.
* **Syntax**:

  ```asm
  shr reg, cl     ; Shift right by value in cl (0-31)
  shr reg, imm8   ; Shift right by immediate value (0-31)
  ```
* **Example**:

  ```asm
  mov al, 0x8A    ; al = 10001010 (binary)
  shr al, 1       ; al = 01000101 (shift right by 1, divide by 2)
  ```

---

### **Quick Multiplication/Division**:

* **Shift left** = multiply by ( 2^n )

  ```asm
  mov eax, 3      ; eax = 3
  shl eax, 2      ; eax = 12 (3 * 4)
  ```
* **Shift right** = divide by ( 2^n )

  ```asm
  mov eax, 12     ; eax = 12
  shr eax, 2      ; eax = 3 (12 / 4)
  ```

---

### **Summary of Instructions**:

| Instruction   | Description                             | Example                      |
| ------------- | --------------------------------------- | ---------------------------- |
| `shl reg, cl` | Shift left by `cl`, multiply by ( 2^n ) | `shl eax, 2` (eax = eax * 4) |
| `shr reg, cl` | Shift right by `cl`, divide by ( 2^n )  | `shr eax, 2` (eax = eax / 4) |

---

### **Key Points**:

* **`shl`** = multiplication by powers of 2.
* **`shr`** = division by powers of 2 (with truncation).


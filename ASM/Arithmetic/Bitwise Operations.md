# Bitwise Operations Cheatsheet (x86_64 Assembly)

### 1. AND (`and`)
- **Description**: Performs bitwise AND operation.  
- **Syntax**: `and dest, src`
- **Operation**: Each bit of the destination register is ANDed with the corresponding bit of the source register.  
- **Result**: The result is stored in the destination register.
  
  **Truth Table**:
  | A  | B  | A AND B |
  |----|----|---------|
  |  0 |  0 |    0    |
  |  0 |  1 |    0    |
  |  1 |  0 |    0    |
  |  1 |  1 |    1    |

  **Example**:
  ```asm
  mov rax, 0xAA     ; rax = 10101010
  mov rbx, 0x33     ; rbx = 00110011
  and rax, rbx      ; rax = rax AND rbx -> 00100010
````

### 2. OR (`or`)

* **Description**: Performs bitwise OR operation.
* **Syntax**: `or dest, src`
* **Operation**: Each bit of the destination register is ORed with the corresponding bit of the source register.
* **Result**: The result is stored in the destination register.

  **Truth Table**:

  | A | B | A OR B |
  | - | - | ------ |
  | 0 | 0 | 0      |
  | 0 | 1 | 1      |
  | 1 | 0 | 1      |
  | 1 | 1 | 1      |

  **Example**:

  ```asm
  mov rax, 0xAA     ; rax = 10101010
  mov rbx, 0x33     ; rbx = 00110011
  or rax, rbx       ; rax = rax OR rbx -> 10111011
  ```

### 3. XOR (`xor`)

* **Description**: Performs bitwise XOR (exclusive OR) operation.
* **Syntax**: `xor dest, src`
* **Operation**: Each bit of the destination register is XORed with the corresponding bit of the source register.
* **Result**: The result is stored in the destination register.

  **Truth Table**:

  | A | B | A XOR B |
  | - | - | ------- |
  | 0 | 0 | 0       |
  | 0 | 1 | 1       |
  | 1 | 0 | 1       |
  | 1 | 1 | 0       |

  **Example**:

  ```asm
  mov rax, 0xAA     ; rax = 10101010
  mov rbx, 0x33     ; rbx = 00110011
  xor rax, rbx      ; rax = rax XOR rbx -> 10011001
  ```

### 4. NOT (`not`)

* **Description**: Performs bitwise NOT operation (inversion of all bits).
* **Syntax**: `not dest`
* **Operation**: Inverts all the bits of the destination register.
* **Result**: The result is stored in the destination register.

  **Truth Table**:

  | A | NOT A |
  | - | ----- |
  | 0 | 1     |
  | 1 | 0     |

  **Example**:

  ```asm
  mov rax, 0xAA     ; rax = 10101010
  not rax           ; rax = NOT rax -> 01010101
  ```

---

### Notes:

* All operations are **in-place**; they modify the destination register.
* These operations affect individual bits, useful for flag manipulations, masking, and bit-level calculations.
* For 64-bit registers (e.g., `rax`, `rbx`), the operations work on the full 64-bit width.

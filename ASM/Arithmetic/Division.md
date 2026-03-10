# x86-64 Division Cheatsheet

## 1. Overview

In x86-64, **division is special**:

* There are **unsigned (`DIV`)** and **signed (`IDIV`)** instructions.
* The **dividend must be in specific registers**, depending on the size.
* The **quotient and remainder** are always stored in fixed registers.
* Division by zero or overflow causes a **CPU exception**.

---

## 2. Which Registers Are Used

| Operand Size | Dividend Register(s) | Quotient | Remainder |
| ------------ | -------------------- | -------- | --------- |
| 8-bit        | `AL`                 | `AL`     | `AH`      |
| 16-bit       | `AX`                 | `AX`     | `DX`      |
| 32-bit       | `EDX:EAX`            | `EAX`    | `EDX`     |
| 64-bit       | `RDX:RAX`            | `RAX`    | `RDX`     |

> **Tip:** “High:Low” notation (`EDX:EAX`) means the **high part of the dividend goes in the extra register**, low part in EAX/RAX.

---

## 3. Unsigned Division (`DIV`)

### 3.1 Rules

1. `DIV r/m8` → `AL / operand` → quotient in `AL`, remainder in `AH`
2. `DIV r/m16` → `AX / operand` → quotient in `AX`, remainder in `DX`
3. `DIV r/m32` → `EDX:EAX / operand` → quotient in `EAX`, remainder in `EDX`
4. `DIV r/m64` → `RDX:RAX / operand` → quotient in `RAX`, remainder in `RDX`

### 3.2 Example (32-bit unsigned)

```asm
mov eax, 100        ; Dividend low
xor edx, edx        ; Clear high (EDX:EAX = 0:100)
mov ecx, 30         ; Divisor
div ecx             ; Quotient -> EAX=3, Remainder -> EDX=10
```

**Diagram for 32-bit DIV:**

```
EDX:EAX = 0:100  (dividend)
ECX       = 30   (divisor)
-----------------
Result: EAX = 3 (quotient)
        EDX = 10 (remainder)
```

---

## 4. Signed Division (`IDIV`)

### 4.1 Rules

* Same register conventions as `DIV`.
* **Must sign-extend the dividend** before division:

  * 8-bit → `CBW` (AL → AX)
  * 16-bit → `CWD` (AX → DX:AX)
  * 32-bit → `CDQ` (EAX → EDX:EAX)
  * 64-bit → `CQO` (RAX → RDX:RAX)

### 4.2 Example (32-bit signed)

```asm
mov eax, -20       ; Dividend
cdq                 ; Sign-extend into EDX:EAX
mov ecx, 6         ; Divisor
idiv ecx            ; Quotient -> EAX=-3, Remainder -> EDX=-2
```

**Diagram for 32-bit IDIV:**

```
EDX:EAX = -20
ECX       = 6
-----------------
Result: EAX = -3 (quotient)
        EDX = -2 (remainder)
```

> Notice: `CDQ` is crucial; without it, the CPU would divide the wrong 64-bit value and possibly cause an exception.

---

## 5. Quick Visual Guide

```
8-bit  : AL / operand  -> AL=quotient, AH=remainder
16-bit : AX / operand  -> AX=quotient, DX=remainder
32-bit : EDX:EAX / operand -> EAX=quotient, EDX=remainder
64-bit : RDX:RAX / operand -> RAX=quotient, RDX=remainder
```

**Sign-extension instructions for IDIV:**

| Size   | Instruction   |
| ------ | ------------- |
| 8-bit  | CBW → AX      |
| 16-bit | CWD → DX:AX   |
| 32-bit | CDQ → EDX:EAX |
| 64-bit | CQO → RDX:RAX |

---

## 6. Important Notes

1. **Overflow**: If quotient doesn’t fit → **#DE exception**.
2. **Division by zero** → **#DE exception**.
3. **Always clear high registers for unsigned division** if dividend fits in low register.
4. **Signed division requires sign-extension** (`CBW`, `CWD`, `CDQ`, `CQO`).


# x86-64 Assembly Arithmetic

## Registers

* **64-bit**: `rax`, `rbx`, `rcx`, `rdx`
* **32-bit**: `eax`
* **16-bit**: `ax`
* **8-bit**: `al`

---

## Addition

```asm
add rax, rbx        ; rax = rax + rbx
adc rax, rbx        ; add with carry
```

---

## Subtraction

```asm
sub rax, rbx        ; rax = rax - rbx
sbb rax, rbx        ; subtract with borrow
```

---

## Increment / Decrement

```asm
inc rax
dec rax
```

---

## Multiplication

| Instruction          | Signed | Uses RDX | Result location |
| -------------------- | ------ | -------- | --------------- |
| `mul rbx`            | No     | Yes      | `rdx:rax`       |
| `imul rbx`           | Yes    | Yes      | `rdx:rax`       |
| `imul rax, rbx`      | Yes    | No       | `rax`           |
| `imul rax, rbx, imm` | Yes    | No       | `rax`           |


---

## Division (x86-64, Intel syntax)

### Unsigned division

```asm
div rbx
```

* **Implicit registers (ALWAYS)**

  * Dividend (128-bit): `rdx:rax`
  * Divisor: `rbx`
* **Result**

  * Quotient  → `rax`
  * Remainder → `rdx`


### Signed division

```asm
idiv rbx
```

* **Implicit registers (ALWAYS)**

  * Dividend (128-bit, signed): `rdx:rax`
  * Divisor: `rbx`
* **Result**

  * Quotient  → `rax`
  * Remainder → `rdx`


### Required preparation

**Unsigned**

```asm
xor rdx, rdx
```

* Zero-extend `rax` into `rdx:rax`

**Signed**

```asm
cqo
```

* Sign-extend `rax` into `rdx:rax`


### Are these registers always used?

✅ **YES — ALWAYS**

* `rax` → quotient
* `rdx` → remainder
* Dividend is **always** `rdx:rax`
* You **cannot** choose other registers


### What happens on error?

* Division by zero → **#DE exception**
* Quotient too large → **#DE exception**


### Summary Table

| Instruction  | Signed | Dividend  | Quotient | Remainder | Forced |
| ------------ | ------ | --------- | -------- | --------- | ------ |
| `div r/m64`  | No     | `rdx:rax` | `rax`    | `rdx`     | YES    |
| `idiv r/m64` | Yes    | `rdx:rax` | `rax`    | `rdx`     | YES    |

---


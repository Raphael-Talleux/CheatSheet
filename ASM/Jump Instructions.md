# Jump Instructions Cheat Sheet

## Unconditional Jumps

Unconditional jumps always transfer execution to the target address, without evaluating any condition.

### `jmp` — Jump

Transfers control unconditionally to the specified label or address.

#### Syntax

```nasm
jmp label
jmp register
jmp [memory]
```

#### Examples

```nasm
jmp done            ; jump to a label

jmp rax             ; jump to address stored in rax

jmp [rip + target]  ; indirect jump using memory (RIP-relative)
```

#### Notes

* `jmp label` is encoded as a relative jump when possible.
* `jmp register` and `jmp [memory]` are indirect jumps.
* Commonly used for loops, state machines, and tail calls.

---

## Conditional Jumps

Conditional jumps transfer execution only if a specific condition is met.
They depend on the state of the FLAGS register, usually set by `cmp`, `test`, or arithmetic instructions.

### Common Comparison Setup

```nasm
cmp rax, rbx   ; sets flags based on (rax - rbx)
test rax, rax ; sets flags based on (rax & rax)
```

### Equality / Zero

| Instruction   | Meaning                      | Condition (FLAGS) |
| ------------- | ---------------------------- | ----------------- |
| `je` / `jz`   | jump if equal / zero         | ZF = 1            |
| `jne` / `jnz` | jump if not equal / not zero | ZF = 0            |

```nasm
cmp rax, 10
je equal_ten
```

### Signed Comparisons

| Instruction | Meaning                  | Condition          |
| ----------- | ------------------------ | ------------------ |
| `jl`        | jump if less             | SF ≠ OF            |
| `jle`       | jump if less or equal    | ZF = 1 or SF ≠ OF  |
| `jg`        | jump if greater          | ZF = 0 and SF = OF |
| `jge`       | jump if greater or equal | SF = OF            |

```nasm
cmp rax, rbx
jl less_signed
```

### Unsigned Comparisons

| Instruction | Meaning                | Condition         |
| ----------- | ---------------------- | ----------------- |
| `jb` / `jc` | jump if below / carry  | CF = 1            |
| `jbe`       | jump if below or equal | CF = 1 or ZF = 1  |
| `ja`        | jump if above          | CF = 0 and ZF = 0 |
| `jae`       | jump if above or equal | CF = 0            |

```nasm
cmp rax, rbx
ja above_unsigned
```

### Sign and Overflow

| Instruction | Meaning             | Condition |
| ----------- | ------------------- | --------- |
| `js`        | jump if sign        | SF = 1    |
| `jns`       | jump if not sign    | SF = 0    |
| `jo`        | jump if overflow    | OF = 1    |
| `jno`       | jump if no overflow | OF = 0    |

### Notes

* Conditional jumps are always relative.
* Use signed or unsigned jumps consistently with the data type.
* `cmp` does not store a result, it only updates FLAGS.


---

## Indirect Jumps and Jump Tables (Switch Statements)

Indirect jumps are commonly used to implement `switch` statements efficiently when branching on integer values with a known range.

### Concept

Instead of chaining many `cmp` + `jmp`, execution jumps to an address stored in memory.

A **jump table** is a contiguous array of addresses:

```
[rsi + 0x00] → case 0
[rsi + 0x08] → case 1
[rsi + 0x10] → case 2
[rsi + 0x18] → case 3
[rsi + 0x20] → default
```

* Each entry is **8 bytes** (64-bit address)
* Indexing uses: `base + index * 8`


### Example Logic

```text
if rdi == 0: jmp A
if rdi == 1: jmp B
if rdi == 2: jmp C
if rdi == 3: jmp D
else:        jmp E
```

Assumptions:

* `rdi` contains the switch value
* `rdi` is **not negative**
* `rsi` contains the jump table base address


### Minimal ASM Implementation

```nasm
cmp rdi, 3
ja  default_case     ; if rdi > 3 → default

jmp [rsi + rdi*8]    ; indirect jump via table

default_case:
jmp [rsi + 32]       ; 4 * 8 → default entry
```


### Key Notes

* This uses **one comparison** and **indirect jumps**
* `ja` is used for **unsigned** comparison
* `jmp [rsi + rdi*8]` is the core of a switch statement
* This pattern is common in compiler-generated code

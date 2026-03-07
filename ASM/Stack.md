# x86-64 Assembly Stack

---

## 1. What the Stack Is

* A **LIFO** (Last In, First Out) data structure
* Grows **downward** (toward lower memory addresses)
* Used for:

  * Function calls and returns
  * Temporary storage
  * Saving registers

---

## 2. Stack Registers

| Register | Description                            |
| -------- | -------------------------------------- |
| `rsp`    | Stack Pointer (points to top of stack) |
| `rbp`    | Base Pointer (optional frame pointer)  |

* `rsp` must be **16-byte aligned** before a `call` instruction.

---

## 3. Stack Growth Direction

```text
High memory addresses
────────────────────
| older data        |
|                   |
|                   |  ← stack grows downward
|                   |
| newer data        |
────────────────────
Low memory addresses
```

---

## 4. Basic Stack Instructions

### push

```asm
push rax        ; rsp -= 8, [rsp] = rax
```

### pop

```asm
pop rax         ; rax = [rsp], rsp += 8
```

Equivalent to:

```asm
sub rsp, 8
mov [rsp], rax
```

```asm
mov rax, [rsp]
add rsp, 8
```

---

## 5. Function Call Mechanics

### call

```asm
call my_func
```

* Pushes the **return address** onto the stack
* Jumps to the function

### ret

```asm
ret
```

* Pops the return address
* Jumps back to the caller



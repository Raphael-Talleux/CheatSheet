# Rust Ownership Cheat Sheet

## Core Concepts

### Ownership Rules
1. Each value in Rust has **one owner**.
2. There can only be **one owner at a time**.
3. When the owner goes **out of scope**, the value is **dropped**.

```rust
{
    let s = String::from("hello"); // s owns the String
} // s goes out of scope, memory is freed
````

---

## Move vs Copy

### Move (default for heap data)

Ownership is **moved**, not copied.

```rust
let s1 = String::from("hello");
let s2 = s1; // move
// s1 is no longer valid
```

### Copy (for simple stack data)

Types with the `Copy` trait are **copied**, not moved.

Common `Copy` types:

* integers (`i32`, `u64`, …)
* floats (`f64`)
* booleans (`bool`)
* chars (`char`)
* tuples of `Copy` types

```rust
let x = 5;
let y = x; // copy, x is still valid
```

---

## Ownership and Functions

### Passing ownership

```rust
fn takes_ownership(s: String) {
    println!("{}", s);
}

let s = String::from("hello");
takes_ownership(s);
// s is no longer valid
```

### Returning ownership

```rust
fn gives_ownership() -> String {
    String::from("hello")
}

let s = gives_ownership();
```

---

## Borrowing (References)

### Immutable Borrow (`&T`)

* Read-only
* Multiple immutable borrows allowed

```rust
let s = String::from("hello");
let r1 = &s;
let r2 = &s; // OK
```

### Mutable Borrow (`&mut T`)

* Read and write
* Only **one mutable borrow at a time**
* No immutable borrows while mutable borrow exists

```rust
let mut s = String::from("hello");
let r = &mut s;
r.push_str("!");
```

❌ Invalid:

```rust
let r1 = &s;
let r2 = &mut s; // error
```

### Mutable Borrow after Immutable Borrows

Rust allows creating a mutable reference **after** immutable references,
as long as the immutable references are **no longer used**.

```rust
let mut s = String::from("hello");

let r1 = &s;
let r2 = &s;

println!("{} and {}", r1, r2); // last use of r1 and r2

let r3 = &mut s; // ✅ OK: r1 and r2 are no longer used
r3.push_str("!");
````

This works because Rust uses **Non-Lexical Lifetimes (NLL)**:
the borrow ends at its **last usage**, not at the end of the scope.

---

## Borrowing Rules (Summary)

* Either:

  * **Any number of immutable references**, OR
  * **Exactly one mutable reference**
* References must always be **valid**

---

## Dangling References (Not Allowed)

Rust prevents references to data that goes out of scope.

```rust
fn dangle() -> &String {
    let s = String::from("hello");
    &s // ❌ invalid
}
```

Correct:

```rust
fn no_dangle() -> String {
    String::from("hello")
}
```

---

## Slices (Borrowed Views)

### String Slice (`&str`)

```rust
let s = String::from("hello");
let slice = &s[0..2]; // "he"
```

### Array Slice

```rust
let a = [1, 2, 3, 4];
let slice = &a[1..3]; // [2, 3]
```

Slices **do not own** the data.

---

## Ownership with Structs

Each field follows ownership rules.

```rust
struct User {
    name: String,
    age: u32,
}
```

Borrowing fields:

```rust
fn print_name(user: &User) {
    println!("{}", user.name);
}
```

---

## `Clone` vs `Copy`

### `Clone`

* Explicit deep copy
* Can be expensive

```rust
let s1 = String::from("hello");
let s2 = s1.clone();
```

### `Copy`

* Implicit, cheap
* Stack-only data


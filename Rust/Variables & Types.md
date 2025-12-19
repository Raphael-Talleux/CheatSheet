
# Rust Variables & Types Cheatsheet

## Variables

### Immutable Variables (Default)
In Rust, variables are immutable by default.

```rust
let x = 5; // Immutable variable
````

### Mutable Variables

To make a variable mutable, use the `mut` keyword.

```rust
let mut x = 5; // Mutable variable
x = 10; // Now you can change the value
```

### Constants

Constants are always immutable and must have an explicit type.

```rust
const MAX_POINTS: u32 = 100_000;
```

## Types

### Scalar Types

* **Integers**: Whole numbers

  * `i8`, `i16`, `i32`, `i64`, `i128` (signed)
  * `u8`, `u16`, `u32`, `u64`, `u128` (unsigned)
  * Example: `let x: i32 = 42;`
* **Floating Point Numbers**: Numbers with decimals

  * `f32`, `f64` (default is `f64`)
  * Example: `let pi: f64 = 3.1415;`
* **Booleans**: `true` or `false`

  * Example: `let is_active: bool = true;`
* **Characters**: A single Unicode character

  * Example: `let letter: char = 'A';`

### Compound Types

* **Tuples**: Group of different types

  * Can contain different data types.
  * Example: `let tuple: (i32, f64, char) = (42, 3.14, 'a');`

```rust
let (x, y, z) = tuple; // Destructuring
```

* **Arrays**: Collection of elements of the same type

  * Fixed size, all elements must be of the same type.
  * Example: `let arr: [i32; 3] = [1, 2, 3];`
  * Accessing elements: `arr[0]`

### Type Aliases

Rust allows you to create a type alias for any type.

```rust
type Kilometers = i32;
let distance: Kilometers = 100;
```

## Type Conversion

Rust does not perform implicit type conversion. You need to explicitly convert types using `as`.

```rust
let x: i32 = 10;
let y: u64 = x as u64;
```

## Common Data Structures

### Strings

* **String**: A growable, heap-allocated string type.

  ```rust
  let mut s = String::from("Hello");
  s.push_str(", world!");
  ```

* **&str**: A string slice, typically used for string literals.

  ```rust
  let greeting: &str = "Hello, world!";
  ```

### Vectors

A growable array, like an array, but can change in size.

```rust
let mut vec: Vec<i32> = Vec::new();
vec.push(1);
vec.push(2);
```

## Ownership and Borrowing

### Ownership

* Each value in Rust has a variable that is its *owner*.
* When ownership is transferred, the previous variable can no longer be used.

### Borrowing

* **References** allow you to borrow a value without taking ownership.

```rust
let x = 5;
let y = &x; // Borrowing
```

#### Mutable References

* Allows modifying the borrowed value, but only one mutable reference can exist at a time.

```rust
let mut x = 5;
let y = &mut x; // Mutable borrow
```
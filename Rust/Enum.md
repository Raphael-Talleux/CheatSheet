# Rust Cheatsheet: Enums

## Defining an Enum

Enums allow you to define a value as one of a set of possible values. For example, an IP address can be either IPv4 or IPv6, but not both.

### Example:

```rust
enum IpAddrKind {
    V4,
    V6,
}
````

Here, `IpAddrKind` is a custom type with two variants: `V4` and `V6`. This ensures an IP address is only one type at a time.



## Enum Values

### Creating Instances

Enum variants are accessed using `::`.

```rust
let four = IpAddrKind::V4;
let six = IpAddrKind::V6;
````

### Enums with Data

Data can be stored directly in enum variants:

```rust
enum IpAddr {
    V4(String),
    V6(String),
}

let home = IpAddr::V4("127.0.0.1".to_string());
```

### Different Data per Variant

Each variant can hold different types:

```rust
enum IpAddr {
    V4(u8, u8, u8, u8),
    V6(String),
}
```

### Complex Enums

Variants can mix types:

```rust
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
}
```

### Methods on Enums

You can define methods on enums:

```rust
impl Message {
    fn call(&self) {}
}
```

## The Option Enum

`Option` is a standard library enum that represents a value that could be something or nothing. It's Rust’s alternative to `null`.

```rust
enum Option<T> {
    None,
    Some(T),
}
````

### Example:

```rust
let some_number = Some(5);
let absent_number: Option<i32> = None;
```

`Option<T>` ensures safety by making you explicitly handle the case of a missing value (`None`).

### Handling `Option`

You can't use an `Option<T>` directly like a regular value. You must handle it first:

```rust
let x: i8 = 5;
let y: Option<i8> = Some(5);

let sum = x + y; // This will not compile
```

### Why Option?

Unlike `null`, `Option<T>` forces you to handle the absence of a value at compile time, preventing many bugs.

### Matching on Option

To use an `Option<T>`, you usually match on its variants:

```rust
match some_number {
    Some(n) => println!("We have a number: {}", n),
    None => println!("No number available"),
}
```

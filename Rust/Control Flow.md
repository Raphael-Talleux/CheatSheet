# Rust Control Flow

## Condition `if`
As a **condition**:
```rust
if x == 0 {
    println!("zero!");
} else if x < 100 {
    println!("biggish");
} else {
    println!("huge");
}
````

As an **expression**:

```rust
let size = if x < 20 { "small" } else { "large" };
```

## Loop `loop`

Infinite loop (can return a value with `break`):

```rust
let result = loop {
    break 42;
};
```

## Loop `while`

Loop while a condition is true:

```rust
while x < 10 {
    x += 1;
}
```

## Loop `for`

Iterate over a range or collection:

```rust
for i in 0..3 {
    println!("{}", i);
}
```

## `match`

Pattern matching (must be exhaustive):

```rust
match x {
    0 => println!("zero"),
    1..=9 => println!("small"),
    _ => println!("large"),
}
```

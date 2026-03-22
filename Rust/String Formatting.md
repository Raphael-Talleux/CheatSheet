# String Formatting

Rust uses `{}` placeholders with macros like `println!`, `format!`, etc.  
The colon `:` inside `{}` is used to specify **formatting options**.


## 1. Basic placeholders

```rust
let name = "Alice";
let age = 30;

println!("{} is {} years old.", name, age);      // positional
println!("{1} is {0} years old.", age, name);   // numbered
println!("{name} is {age} years old.", name=name, age=age); // named
````

## 2. Alignment and width

| Syntax      | Example  | Output       |
| ----------- | -------- | ------------ |
| `{:>width}` | `{:>10}` | Right-align  |
| `{:<width}` | `{:<10}` | Left-align   |
| `{:^width}` | `{:^10}` | Center-align |

```rust
println!("|{:>10}|", "rust");  // |      rust|
println!("|{:<10}|", "rust");  // |rust      |
println!("|{:^10}|", "rust");  // |   rust   |
```


## 3. Padding with characters

```rust
println!("|{:0>5}|", 42);     // |00042|
println!("|{:*^10}|", "rust"); // |***rust***|
```

* Syntax: `{:fill>width}`, `{:fill^width}`, `{:fill<width}`


## 4. Floating point precision

```rust
let pi = 3.14159;
println!("{:.2}", pi);   // 3.14
println!("{:8.2}", pi);  // '    3.14' (width 8, 2 decimals)
```

* `.precision` controls decimal places.
* `width.precision` sets total width + decimal precision.



## 5. Number formatting

| Specifier | Description   | Example           |
| --------- | ------------- | ----------------- |
| `b`       | binary        | `255 -> 11111111` |
| `o`       | octal         | `255 -> 377`      |
| `x`       | hex lowercase | `255 -> ff`       |
| `X`       | hex uppercase | `255 -> FF`       |

```rust
println!("{:08X}", 255); // 000000FF (width 8, padded with 0)
```

## 6. Signs

```rust
let n = 42;
println!("{:+}", n);  // +42
println!("{:-}", n);  // 42 (only negative shows -)
println!("{: }", n);  //  42 (space if positive)
println!("{:+08}", n); // +0000042 (width 8, padded with 0)
```


## 7. Combined example

```rust
let name = "Alice";
let score = 42;

println!("{name} scored {score:0>5}", name=name, score=score);
// Alice scored 00042
```
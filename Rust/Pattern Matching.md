# Rust Cheatsheet: Pattern Matching

## The match Control Flow Construct

Rust's `match` allows you to compare a value to multiple patterns and execute code based on the match. Patterns can be literals, variables, or wildcards. The power of `match` lies in exhaustiveness — Rust ensures all possible cases are covered.

### Example: Coin Matching

```rust
enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter,
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}
````

Each `match` arm has a pattern and code. If a pattern matches, the corresponding code runs.

### Patterns That Bind to Values

You can extract data from enum variants using match.

```rust
enum UsState {
    Alabama,
    Alaska,
}

enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter(UsState),
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Quarter(state) => {
            println!("State quarter from {:?}", state);
            25
        },
        _ => 0,
    }
}
```

### Handling Option with match

You can also use `match` with `Option<T>`:

```rust
fn plus_one(x: Option<i32>) -> Option<i32> {
    match x {
        None => None,
        Some(i) => Some(i + 1),
    }
}
```

### Exhaustiveness and Catch-All Patterns

`match` requires all cases to be handled. Use `_` to catch all other values.

```rust
let dice_roll = 9;
match dice_roll {
    3 => add_fancy_hat(),
    7 => remove_fancy_hat(),
    _ => reroll(),
}
```

If a pattern is omitted, Rust will give an error. The `_` wildcard matches any value, useful for cases where the value isn’t needed.

```rust
match dice_roll {
    3 => add_fancy_hat(),
    7 => remove_fancy_hat(),
    _ => (), // Do nothing
}
```

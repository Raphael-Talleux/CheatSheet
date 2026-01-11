# Rust Cheatsheet: IF LET and LET ELSE

## Concise Control Flow with `if let` and `let else`

The `if let` syntax allows you to combine `if` and `let` in a concise way to handle values that match a single pattern while ignoring the rest. It's especially useful when you only care about one pattern and want to avoid the verbosity of a full `match` expression.

### Example with `Option<u8>`

```rust
let config_max = Some(3u8);
match config_max {
    Some(max) => println!("The maximum is configured to be {max}"),
    _ => (),
}
````

In this case, we only care about when `config_max` is `Some`. Instead of using a full `match`, we can use `if let`:

```rust
let config_max = Some(3u8);
if let Some(max) = config_max {
    println!("The maximum is configured to be {max}");
}
```

This is more concise but doesn't offer the exhaustive checking that `match` does. `if let` is ideal when you care about a single pattern and want to ignore the rest.

### Adding an `else` Clause

You can combine `if let` with an `else` clause to handle the case where the pattern doesn't match:

```rust
let mut count = 0;
if let Coin::Quarter(state) = coin {
    println!("State quarter from {state:?}!");
} else {
    count += 1;
}
```

This pattern is useful for counting or performing a default action when the value doesn't match the pattern.

### Staying on the “Happy Path” with `let...else`

Rust's `let...else` allows you to express the common pattern of doing something when a value matches and returning early otherwise. It clarifies control flow by avoiding a nested `if let`.

```rust
fn describe_state_quarter(coin: Coin) -> Option<String> {
    let Coin::Quarter(state) = coin else {
        return None;
    };

    if state.existed_in(1900) {
        Some(format!("{state:?} is pretty old, for America!"))
    } else {
        Some(format!("{state:?} is relatively new."))
    }
}
```

The `let...else` construct ensures that the main body of the function remains on the "happy path" without any complex conditional logic.


# I/O Cheat Sheet

## stdin

```rust id="yq4l1u"
use std::io;

let mut input = String::new();
io::stdin().read_line(&mut input).expect("read error");

let input = input.trim(); // remove \n
```

```rust id="8yx0yj"
let n: i32 = input.parse().expect("parse error");
```

* `read_line` appends & keeps `\n`
* use `trim()` before parsing


## stdout

```rust id="mivm2z"
use std::io::{self, Write};

print!("Enter value: ");
io::stdout().flush().unwrap();

println!("Hello");
```

* `println!` → newline
* `print!` → needs `flush()`
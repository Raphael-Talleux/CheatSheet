# 🦀 Cargo — Essential Cheatsheet

A practical Cargo cheatsheet focused on **Rust CLI development**.  

## Create a Project
```bash
cargo new my_cli
cargo new my_cli --bin        # binary (default)
cargo new my_lib --lib        # library
```

## Build & Run
``` bash
cargo run                 # compile + run
cargo run -- arg1 arg2    # passer des arguments CLI
cargo build               # compile debug
cargo build --release     # compile optimisé
```

## Dev & Test workflow
``` bash
cargo check             # Check code (much faster without compilation)
cargo run -- args
cargo test              # Unit test
cargo clippy            # Help to produce better code
cargo fmt               # Format code to respect guidelines (indent, spaces, ...)
```


## Dependencies

Add a dependency:
``` bash
cargo add clap
cargo add serde --features derive
cargo add chrono
```
Update dependencies:
``` bash
cargo update
```

## Multiple Binaries

 ``` bash
[[bin]]
name = "taskr"
path = "src/main.rs"

[[bin]]
name = "taskr-admin"
path = "src/admin.rs"
```

## Utils

Generate documentation:
``` bash
cargo doc --open     # generate and open local docs
```

Cleanup project (exept code and toml)
``` bash
cargo clean
```
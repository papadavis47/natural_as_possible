# natural_as_possible

A Rust project scaffolded with Cargo.

## Requirements

- [Rust](https://www.rust-lang.org/tools/install) (stable toolchain) with `cargo`.
- This crate uses Rust **edition 2024**, which requires a recent toolchain (Rust 1.85 or newer). Update with `rustup update` if needed.

## Getting Started

Clone the repository and build the project:

```sh
cargo build
```

## Usage

Run the program:

```sh
cargo run
```

## Development

Common commands:

```sh
cargo check   # Type-check without producing a binary
cargo build   # Compile a debug build
cargo test    # Run the test suite
cargo fmt     # Format the code
cargo clippy  # Lint the code
```

To produce an optimized release build:

```sh
cargo build --release
```

## Project Structure

```
natural_as_possible/
├── Cargo.toml      # Package manifest and dependencies
├── Cargo.lock      # Locked dependency versions
└── src/
    └── main.rs     # Application entry point
```

## License

No license has been specified yet. Add a `LICENSE` file to declare how others may use this project.

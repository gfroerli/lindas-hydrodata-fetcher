# LINDAS Hydrodata Fetcher

This Rust application fetches open data from the [LINDAS
service](https://lindas.admin.ch/). Specifically, it fetches water temperature
data from the FOEN (BAFU) over a SPARQL endpoint.

Read `README.md` for a general overview.

## Build & Commands

- Run binary: `cargo run`
- Format code: `cargo fmt`
- Run linter: `cargo clippy`
- Run tests: `cargo test`

## Architecture

- Single binary

## Security

- Never commit secrets or API keys to repository
- Use environment variables or config files for sensitive data

## Configuration

When adding new configuration options, update all relevant places:

1. Example configuration in `config.example.toml`
2. Configuration schemas in `src/config.rs`
3. Documentation in README.md

All configuration keys use consistent naming and MUST be documented.

## Decisions

Whenever there is a situation where you need to choose between two approaches,
don't just pick one. Instead, ask.

This includes:

- Choosing between two possible architectural approaches
- Choosing between two libraries to use

...and similar situations.

## Conventions

### Rust

Imports:

- ALWAYS use merged imports: One `use` statement per crate
- Group imports using the "std / third party / first party (`super::` / `crate::`)" convention
- Don't use `std::*` directly, instead import the corresponding modules or types at the top level
- Don't use `super::*` imports (except in test modules), instead use `crate::` imports

Testing:

- Run tests with `cargo test`
- Add unit tests to the same module as the code being tested
- Add integration tests on top level
- When importing types that are only used for tests, import them inside the `tests` module and do not use `#[cfg(test)]` on top level
- When adding multiple unit tests for a function, struct or enum, wrap them in a dedicated module named after that unit. For example, when a function is called `check_foo`, the test path should be `tests::check_foo::a_test` and `tests::check_foo::another_test`.
- Never use `super::super::(...)` references or imports in tests, always use a `super::*` import in the module (and potentially parent modules).

Other:

- Sort dependencies (in `Cargo.toml`) and imports alphabetically
- Add rustdoc to all public symbols (structs, fields, enums, etc)
- Check if code compiles with `cargo check`
- Lint code with `cargo clippy`
- At the end, when everything else works fine, ALWAYS format code with rustfmt through `cargo fmt`
- NEVER use `unsafe` unless it is absolutely required to do so. If you think it is required, ALWAYS ask the developer for permission, along with a rationale.
- When crates provide RusTLS support, prefer that over OpenSSL
- Avoid deeply nested logic by using early returns for error cases

# Commands

These are the commands of this repository:

- Build: `cargo check --workspace --all-features`
- Test: `cargo test --workspace --all-features`
- Lint: `cargo clippy --workspace --all-targets --all-features -- -D warnings`
- Format: `cargo fmt --all`
- Start: `cargo run`

Copy each command as it stands. Do not remove a flag.

## When to run a check

Run a check only if the task changed a file that the check reads. If no such file
changed, do not run the check.

These files belong to each check:

- Lint: the path filter in `.github/workflows/clippy.yml` lists the files.
- Test: the path filter in `.github/workflows/test.yml` lists the files.
- Build and Format: the Rust files (`*.rs`) and the Cargo files (`Cargo.toml`, `Cargo.lock`).

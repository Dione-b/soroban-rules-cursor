# Master Rules for Soroban Contracts

You are an expert in Rust, the Soroban SDK, and smart contract development for the Stellar blockchain.

## Response Constraints
- Do not remove any existing code unless necessary.
- Do not remove my comments or commented-out code unless necessary.
- Do not change the formatting of my `use` declarations.
- Do not change the formatting of my code unless important for new functionality.

## Code Style and Structure
- Write concise and idiomatic Rust code, specific to the Soroban SDK.
- Use functional and declarative patterns common in Rust.
- Prefer iteration and modularization over code duplication.
- Use descriptive variable names (e.g., `is_initialized`, `has_balance`).
- Structure files as follows (based on best practices):
  - `src/lib.rs` (Contract entry point, `#[contract]` and `#[contractimpl]`)
  - `src/types.rs` (Custom types, `enum`s with `#[contracttype]`)
  - `src/error.rs` (The `enum Error` with `#[contracterror]`)
  - `src/storage.rs` (`DataKey` storage keys and helper functions)
  - `src/test.rs` (or `mod test` in `lib.rs` with `#[cfg(test)]`)

## Naming Conventions
- Use `snake_case` for functions, variables, and module names (Rust standard).
- Use `PascalCase` for `struct`s, `enum`s, and `trait`s (Rust standard).

## Rust and Soroban SDK Usage
- **Error Handling:**
  - **DON'T:** NEVER use `panic!`, `unwrap()`, or `expect()` in contract code.
  - **DON'T:** Use `assert!()` outside of tests.
  - **DO:** Always return `Result<T, Error>`, using the custom `enum Error` from `@src/error.rs`.
  - **DO:** Use `.ok_or(Error::...)` to convert `Option` to `Result`.
- **Storage:**
  - **DO:** Use `env.storage().instance()` for single, contract-wide data (e.g., Config, Admin).
  - **DO:** Use `env.storage().persistent()` for per-user data or collections (e.g., Balances).
  - **DO:** ALWAYS call `extend_ttl()` after setting or modifying data to prevent expiration.
  - **DO:** Define all storage keys in an `enum DataKey` (in `@src/storage.rs` or `@src/types.rs`).
- **Tokens (SAC):**
  - **DO:** Use `soroban_sdk::token::Client` for all SAC token interactions.
  - **DO:** Use `soroban_sdk::token::StellarAssetClient` for Stellar native assets.

## Syntax and Formatting
- Use standard Rust formatting (applied by `cargo fmt`).
- Use curly braces `{}` for all conditionals (`if`, `match`).
- Use `#[cfg(test)]` for test modules.
- **Test Boilerplate:**
  - **DO:** Use the standard test setup: `let env = Env::default();`, `let contract_id = env.register_contract(...)`, `let client = ContractClient::new(...)`.
  - **DO:** Use `env.mock_all_auths();` to simulate authentication in tests.
  - **DO:** Test failure paths using `#[should_panic(expected = "Error(...)")]`.

## Security and Authentication
- **DO:** ALWAYS authenticate *before* any state change.
- **DO:** Use `address.require_auth()` to verify the signer (e.g., `user.require_auth();` or `admin.require_auth();`).
- **DON'T:** NEVER allow state changes without a corresponding `.require_auth()` call.
- **DON'T:** Use predictable values (e.g., `env.ledger().timestamp()`) for security logic.

## Gas and Resource Optimization
- Be mindful of contract resource limits (CPU and memory).
- **DON'T:** Use `Vec` or `Map` in a *single* storage entry; this will hit size limits.
- **DON'T:** Use `env.storage().temporary()` for important data, as it expires quickly.
- Write deterministic and efficient code.

# Cursor Rules - Soroban/Rust

Rules repository for smart contract development in Soroban (Stellar) using Cursor IDE.

## What is it

This `.cursorrules` configures Cursor to assist in Soroban contract development in Rust, following SDK best practices and security standards.

## Features

- **Security first**: Never use `panic!`, `unwrap()` or `expect()` in contracts
- **Error handling**: Always return `Result<T, Error>` with custom errors
- **Storage patterns**: Correct usage of `instance()` vs `persistent()` with TTL
- **Authentication**: Mandatory validation via `require_auth()` before state changes
- **Optimization**: Practices to avoid CPU and memory limits
- **Structure**: Modular file organization (`lib.rs`, `types.rs`, `error.rs`, `storage.rs`, `test.rs`)

## How to use

Copy the `.cursorrules` file to the root of your Soroban project. Cursor will automatically apply the rules during development.

## Who is it for

Developers working with:
- Soroban contracts (Stellar blockchain)
- Rust + Soroban SDK
- SAC tokens (Stellar Asset Contract)
- Cursor IDE

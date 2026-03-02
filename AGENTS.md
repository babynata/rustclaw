# RustClaw — Agent Guidelines

This is a personal fork of OpenClaw with Rust native core via napi-rs.

- Repo: https://github.com/babynata/rustclaw
- Upstream: https://github.com/openclaw/openclaw
- In chat replies, file references must be repo-root relative only (e.g. `crates/binding-cache/src/lib.rs:42`).

## Project Focus

This fork's primary experiment: replacing performance-sensitive TypeScript hot paths with Rust via napi-rs.

- Core Rust work lives in `crates/` (napi-rs bindings)
- Active experiment branch: `feat/rust-phase0-workspace`
- TypeScript interface must remain compatible with upstream openclaw

## Project Structure

- `crates/` — Rust crates exposed via napi-rs
- `src/` — TypeScript core (CLI, gateway, commands, channels)
- `packages/` — Internal workspace packages
- `extensions/` — Channel plugins
- `apps/` — macOS / iOS / Android companion apps
- `docs/` — Documentation

## Build & Dev Commands

- Runtime: Node ≥22 + Rust stable ≥1.75
- Install deps: `pnpm install`
- Build Rust crates: `cargo build --release`
- Full build: `pnpm build`
- Type check: `pnpm tsgo`
- Lint/format: `pnpm check`
- Tests: `pnpm test`
- Dev loop: `pnpm gateway:watch`

## Rust / napi-rs Conventions

- Keep napi-rs bindings in `crates/<crate-name>/src/lib.rs`
- Expose only the minimal surface needed — don't pull TypeScript complexity into Rust
- Always benchmark before claiming a Rust replacement is faster
- Tag Rust-only commits with `[rust]` prefix (e.g. `[rust] add BindingCache LRU eviction`)

## Coding Style

- TypeScript: ESM, strict typing, no `any`
- Rust: idiomatic, safe code; avoid `unsafe` unless napi-rs requires it
- Keep files under ~500 LOC when feasible
- Add brief comments for tricky logic

## Syncing with Upstream

- `main` tracks upstream `openclaw/openclaw:main`
- Sync: `git pull upstream main --rebase`
- Do not force-push `main`

## Agent Notes

- Never edit `node_modules`
- Never commit real credentials or personal config values
- When working on Rust crates, verify `cargo test` passes before committing

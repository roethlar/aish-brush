# Repo-Specific Guidance
<!-- Extends AGENTS.md; never overrides it. Rules and pointers only — state
     lives in .agents/state.md. -->

## Mission Detail

This repo is **brush** (Bo(u)rn(e) RUsty SHell): a bash- and POSIX-compatible
shell written in Rust, plus an embeddable `brush_core::Shell` library. The
workspace is a multi-crate Rust project (edition 2024, MSRV 1.88.0 per
workspace `Cargo.toml`). Main crates: `brush-shell` (CLI entry),
`brush-interactive`, `brush-core`, `brush-builtins`, `brush-parser`, with
`xtask` for build/test automation.

This workspace is a fork of the public **brush** shell project. Workspace
`Cargo.toml` names the upstream product repository under the `reubeno`
GitHub account. Which GitHub remote this clone tracks is machine-local —
confirm with `git remote -v` (do not assume). Day-to-day agent work follows
whatever remotes and branch the owner is using unless they say otherwise.

## Reading Order

1. `AGENTS.md` — universal prime invariants and operators (toolkit-owned).
2. `.agents/repo-guidance.md` — this file (repo-specific rules).
3. `.agents/state.md` — what is true right now.
4. `.agents/decisions.md` — settled durable decisions still in force.
5. Project docs under `docs/` and `README.md` when the task needs product or
   how-to detail.

## Verification

Canonical local verification (pre-finish / before claiming work complete):

```bash
cargo xtask ci pre-commit
```

This runs the documented pre-commit workflow (quick checks plus deps,
schemas, and integration tests). Source of command: `xtask/src/ci.rs`
(`pre-commit` workflow) and the pre-migration agent guide.

Faster inner loop while iterating:

```bash
cargo xtask ci quick
```

Package-scoped checks when only one crate changed:

```bash
cargo check --package <crate>
cargo test --package <crate>
```

Compatibility-focused:

```bash
cargo test --test brush-compat-tests
# or a single case:
cargo test --test brush-compat-tests -- '<name of test case>'
```

Other useful xtask surfaces (not the default gate): `cargo xtask check fmt`,
`check lint`, `check deps`, `check build`, `check schemas`,
`cargo xtask test unit`, `cargo xtask test integration`.

**GitHub Actions (file-level evidence only):** workflow file
`.github/workflows/ci.yaml` sits on the path GitHub Actions executes and
declares triggers for `pull_request` and for `push` to branch `main` (with
path filters that skip pure markdown/docs-only pushes). Whether Actions is
enabled for the hosting remote, and whether recent runs passed, is
environment state — re-check with the host's Actions UI or `gh` if that
matters for the task; do not treat the workflow file alone as proof of live
gate history. Prefer the local `cargo xtask ci pre-commit` command above as
the verification default agents must actually run.

## Remotes & Sync

- Remotes are clone-local. Run `git remote -v` and `git branch -vv` rather
  than trusting chat or memory.
- Upstream product identity (for orientation): public `brush` under the
  `reubeno` GitHub account, as named in workspace `Cargo.toml`
  `repository`.
- Push policy: `.agents/push-policy.md` (not duplicated here).

## Earned Practices

Repo-specific working rules migrated from the former `AGENTS.md` agent guide
and verified against current tree layout:

- Prefer **`cargo xtask`** for validation over ad-hoc one-off cargo
  invocations when an xtask target exists.
- **Compatibility fixes** should add or update YAML cases under
  `brush-shell/tests/cases/` (see also `docs/how-to/run-tests.md`).
- **Public APIs** of published crates are public surface; non-backwards-
  compatible changes are breaking and need clear call-out. New optional
  fields on public structs that implement `Default` are generally fine when
  the default is sensible.
- When changing public APIs in `brush-core`, check call sites in
  `brush-shell/src/main.rs` and `brush-interactive/`.
- **Error handling:** `thiserror` for crate errors; `anyhow` only in tests.
- **Logging:** `tracing` with categories from `trace_categories` modules
  (e.g. `brush-core/src/trace_categories.rs`).
- Prefer references over cloning unless a separate owned copy is required
  (e.g. async capture).
- Platform-specific code belongs under `brush-core` `sys` modules
  (`brush-core/src/sys/`).
- Shell construction uses the builder pattern (`Shell::builder()` in
  `brush-core/src/shell.rs`).
- Exported items need rustdoc; workspace lints deny missing docs.
- **AI-assisted contributions:** when AI tools materially assist a change,
  include an `Assisted-by:` trailer (Linux-kernel-style), as also stated in
  `CONTRIBUTING.md` for human contributors. Format:
  `Assisted-by: AGENT_NAME:MODEL_VERSION [TOOL1] [TOOL2]`.
- Conventional commit style is expected for project commits (`feat:`,
  `fix:`, `docs:`, etc.) per contributor docs.
- Critical entry points for orientation: `brush-core/src/shell.rs`,
  `brush-core/src/lib.rs`, `brush-shell/src/main.rs`.

## Owner Communication

- Profile: default — owner chat: plain-English executive summary, no
  jargon; plans: token-dense, detailed, written for agents.

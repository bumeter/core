# Bumeter core

The shared engine of [Bumeter](https://bumeter.cc): reads the local logs of Claude Code, Kiro and OpenCode, keeps them in SQLite, and works out quota, context and effectiveness. Every Bumeter product uses it: [statusline](https://github.com/bumeter/statusline) (`bum`), [Desktop](https://github.com/bumeter/bumeter), [VS Code](https://github.com/bumeter/vscode).

This is a library, not something to install. Use it with a git tag:

```toml
bum-core = { git = "https://github.com/bumeter/core", tag = "v1.2.0" }
bum-service = { git = "https://github.com/bumeter/core", tag = "v1.2.0" }
```

| Crate | |
|---|---|
| `bum-core` | store, quota, effectiveness, config, paths |
| `bum-adapters` | log readers for Claude Code, Kiro, OpenCode |
| `bum-skills` | skill catalog, plan / apply / undo |
| `bum-service` | one host per machine: lock, socket, RPC, ops |

Working on core and a product together: in the product repo, add a `.cargo/config.toml` (not committed) that points the git dependency to your local clone:

```toml
[patch."https://github.com/bumeter/core"]
bum-core = { path = "../core/crates/bum-core" }
bum-adapters = { path = "../core/crates/bum-adapters" }
bum-skills = { path = "../core/crates/bum-skills" }
bum-service = { path = "../core/crates/bum-service" }
```

Release: bump `version` in `Cargo.toml`, tag `vX.Y.Z`, then raise the tag in each product repo.

License: GPL-3.0-or-later.

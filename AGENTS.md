# AGENTS.md

Single source of truth for AI coding agents working in this repo. `CLAUDE.md` only points here — put all agent guidance in this file.

## Project

`natural_as_possible` — Rust desktop GUI app built on GPUI (Zed's UI framework) via [GPUI Kit](https://github.com/longbridge/gpui-kit) (formerly `gpui-component`). Early stage: currently a single "Hello, World!" window with one button.

- Binary name: `nap` (`src/main.rs`)
- Rust edition 2024 (needs Rust 1.85+)
- Primary dev platform: Linux (Wayland + X11)

## Layout

```
Cargo.toml    # manifest; single UI dep: gpui-kit
Cargo.lock    # committed
src/main.rs   # entry point: app setup + HelloWorld view
learning/     # personal study notes — gitignored, local only
README.md
AGENTS.md     # this file
CLAUDE.md     # pointer to AGENTS.md
```

## Dependencies

- `gpui-kit = "0.7"` (0.7.1) — the only UI dependency. Re-exports everything:
  - `gpui_kit::*` — GPUI core (`div`, `Render`, `Window`, `Context`, `WindowOptions`, …)
  - `gpui_kit::component::*` — styled components (`Button`, `.v_flex()`, …)
  - `gpui_kit::assets::Assets` — bundled Lucide icons (default `assets` feature)
  - Platform backend (font-kit, wayland, x11) enabled by default
- GPUI comes from the crates.io `gpui-pre` snapshot, pinned exactly (`=0.3.8`) by gpui-kit. **Do not** add `gpui`, `gpui_platform`, or `gpui-component` directly, and do not add zed git deps — mixing sources produces duplicate `gpui` crates and type mismatches.
- Optional `gpui-fast` feature (Longbridge's experimental GPUI fork with retained-mode rendering) is **not** enabled. If ever enabled: views reading state outside entities/globals need `cx.notify()`; debug stale views with `GPUI_VIEW_RETENTION=0`.
- `anyhow` — error handling.

## App entry pattern

```rust
gpui_kit::application()
    .with_assets(gpui_kit::assets::Assets)
    .run(move |cx| {
        gpui_kit::init(cx); // required before using components
        gpui_kit::open_window(WindowOptions::default(), cx, |_, cx| cx.new(|_| MyView))
            .expect("Failed to open window");
    });
```

`gpui_kit::open_window` wraps the view in `Root` automatically — don't construct `Root` manually.

## Commands

```sh
cargo run            # build + launch the app (bin: nap)
cargo build
cargo check
cargo fmt            # must pass `cargo fmt --check`
cargo clippy         # currently warning-free; keep it that way
cargo test           # no tests yet
```

First build is slow (~2 min, large dep tree).

## Conventions

- Commit messages: concise, conventional prefix (`build:`, `feat:`, `fix:`, `docs:`, `chore:`).
- Keep `cargo fmt` and `cargo clippy` clean before committing.
- `learning/` is for the owner's notes; never commit it. Notes there may be stale (e.g. pre-gpui-kit dependency advice).

## Current state

- Migrated from `gpui-component` (git, pinned rev) + zed git `gpui` to `gpui-kit` 0.7.1 from crates.io.
- Builds, runs, fmt + clippy clean.
- No tests, no license yet.

<!--
SPDX-FileCopyrightText: 2026 tao3k team and Contributors

SPDX-License-Identifier: Apache-2.0 AND LGPL-2.1-or-later
-->

# Contributing to Marlin UI Official Marketplace

We welcome high-quality **Plugins**, **Themes**, and **Emacs Workspace Layouts** from both official maintainers and community authors!

## 1. Submitting a Plugin (e.g., Git UI, GitHub UI, AI Tools, Go WASI Docks)

1. Build and certify your plugin locally using `marlin-mygo`:
   ```sh
   just plugin new-react acme.git-ui ./my-git-ui
   CGO_ENABLED=0 go run ./cmd/marlin-app -dev-plugin ./my-git-ui
   CGO_ENABLED=0 go run ./cmd/marlin-mygo-tool doctor -dir ./my-git-ui -perf
   ```
2. Push your plugin source to a public HTTPS Git repository and note the exact 40-character release `commit_sha`.
3. Open a PR adding your entry to `plugins` in [`registry.json`](registry.json):
   ```json
   {
     "id": "acme.git-ui",
     "name": "Git Staging & Diff UI",
     "category": "developer-tools",
     "runtime": "webview-untrusted",
     "slot_id": "workbench.main",
     "trust_tier": "official",
     "publisher_id": "tao3k.official",
     "repository": "https://github.com/acme/marlin-git-ui",
     "commit_sha": "a1b2c3d4e5f60718293a4b5c6d7e8f9012345678",
     "subdir": ".",
     "summary": "Interactive Git staging, branch graph, and hunk diff panel."
   }
   ```

## 2. Submitting a Theme Pack (34-Token Semantic Palette)

Themes are declarative TOML packs (App Store 2.5.2 safe across Desktop, iOS, Android, and Web).
1. Add `themes/<name>.toml` defining the 8 base semantic RGB colors (`canvas`, `bar`, `ink`, `accent`, `info`, `success`, `warning`, `muted`) — Marlin's `DeriveTheme` automatically computes all 34 `--marlin-*` surfaces, borders, hover states, and WCAG-checked `ink_on_accent`.
2. Add your entry to `themes` in [`registry.json`](registry.json).

## 3. Submitting an Emacs Composable Workspace Layout

1. Export a layout from Marlin Studio (`SaveLayoutSpecFile`) or author a valid `layouts/<name>.json` with at most 8 leaf windows and split ratios within `[0.20, 0.80]`.
2. Add your entry to `layouts` in [`registry.json`](registry.json).

## Automated Admission Checks

Every PR automatically runs `.github/workflows/validate-registry.yml` verifying:
- `registry.json` schema v1, unique dot-namespaced IDs, and valid categories
- HTTPS-only repository URLs and 40-hex pinned `commit_sha`
- Zero restricted host slot violations (`approval.gate`, `host.auth`, `host.secrets`)
- Valid TOML themes and valid JSON layouts
- REUSE 3.3 SPDX licensing compliance

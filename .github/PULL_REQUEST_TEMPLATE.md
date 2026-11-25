<!--
SPDX-FileCopyrightText: 2026 tao3k team and Contributors

SPDX-License-Identifier: Apache-2.0 AND LGPL-2.1-or-later
-->

## Submission Type

- [ ] **UI Plugin** (e.g. Git UI, GitHub UI, AI Workflow, Productivity, Mobile Pack)
- [ ] **Curated Theme Pack** (`themes/<name>.toml` — 8-color semantic palette)
- [ ] **Emacs Composable Layout** (`layouts/<name>.json` — `LayoutSpec` binary split tree)

## Summary

- **Entry ID**: `<vendor>.<entry-name>`
- **Source Repository** (for plugins): `https://github.com/...`
- **Pinned 40-char Commit SHA** (for plugins): `<40-hex-sha>`
- **Target Slot / Runtime** (for plugins): e.g. `workbench.main` / `webview-untrusted`

## Official Marketplace Security & Quality Checklist

- [ ] `registry.json` entry passes CI schema & supply-chain validation (`Validate Official Marketplace Registry`)
- [ ] External plugin source uses `https://` with an immutable 40-character hex `commit_sha`
- [ ] Plugin does **not** target restricted Tier-0 host slots (`approval.gate`, `host.auth`, `host.secrets`)
- [ ] Plugin builds reproducibly without network access during packaging so Official CI can sign the `.marlinpkg` with Ed25519
- [ ] All new/modified files include REUSE 3.3 SPDX headers (or are covered by `REUSE.toml`)

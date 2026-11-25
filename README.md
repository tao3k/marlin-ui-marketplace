<!--
SPDX-FileCopyrightText: 2026 tao3k team and Contributors

SPDX-License-Identifier: Apache-2.0 AND LGPL-2.1-or-later
-->

# Marlin UI Official Marketplace (`tao3k/marlin-ui-marketplace`)

The official, community-open UI registry for **Marlin** UI plugins, curated 34-token themes, and shareable Emacs composable workspace layouts across Desktop (macOS / Linux / Windows), iOS, Android, and Web.

## What Lives Here

| Directory | Contents | Target Platforms |
| --- | --- | --- |
| [`registry.json`](registry.json) | Canonical machine-validated index of all admitted plugins, themes, and layouts | All |
| [`plugins/`](plugins/README.md) | Official & community plugin registry guidelines (Git UI, GitHub UI, AI workflows, Go WASI docks) | Desktop / Cross-Platform |
| [`themes/`](themes/) | Curated & community 8-color semantic theme packs (projected into 34 `--marlin-*` tokens) | Desktop + iOS + Android + Web |
| [`layouts/`](layouts/) | Shareable Emacs composable binary-split workspace perspectives (`LayoutSpec` JSON) | Desktop + Web |

## Security & Official Signing Model

1. **Zero Arbitrary Local Code in End-User UI**: Marlin clients verify every `.marlinpkg` and `catalog.json` strictly against Official Ed25519 release keys (`TrustRing.OfficialReleaseTrust()`).
2. **Community Submissions Welcome via PR**: Anyone can submit a Git UI, GitHub UI, AI panel, theme pack, or Emacs layout via Pull Request to [`registry.json`](registry.json).
3. **Immutable Source Pinning**: External plugin submissions must use `https://` and pin an exact 40-character Git `commit_sha`. Floating branch references are rejected automatically.
4. **Clean Official CI Build & Signing**: On merge, Official Marketplace CI builds from the pinned commit in an isolated runner, runs `marlin-mygo-tool doctor -perf`, signs the reproducible `.marlinpkg` with the official Ed25519 key, and publishes it to the signed catalog.
5. **Restricted Host Slots**: Plugins may never target `approval.gate`, `host.auth`, or `host.secrets`.

See [CONTRIBUTING.md](CONTRIBUTING.md) to publish your plugin, theme, or Emacs layout.

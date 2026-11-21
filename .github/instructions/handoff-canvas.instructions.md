---
applyTo: ".github/extensions/**"
description: Architecture, security, and verification rules for project-local Copilot handoff canvas panels.
---

- Load the `generate-handoff-canvas` skill before creating a new canvas panel
  from scratch.
- Keep `extension.mjs` directly in `.github/extensions/<canvas-id>/` (3 parent
  hops back to Git root; no `package.json` or VSIX). Keep `docs/ai/handoff.md`
  (and `docs/ai/todo.md`) as the sole source of truth — never a parallel record.
- Bind only `127.0.0.1:0` per `instanceId` and close all connections in
  `onClose`. Enforce `Host` validation (`403`), `timingSafeEqual` capability
  URL (`404`), and same-origin `x-handoff-token` + `Origin` + JSON
  `Content-Type` on all mutating routes (`403`).
- Build UI markup exclusively with DOM APIs and `textContent` (never `innerHTML`
  on repository/Git text), load zero remote fonts or scripts, and scrub
  credentials from Git remote URLs.
- Validate link opens with `realpath` containment and a non-executable binary
  allowlist, spawn with `shell: false`, and strip `ELECTRON_*` env vars before
  launching OS link handlers so `vscode://` opens properly.
- Verify security checks and dark/light/`380px` layout with an offline smoke
  test before claiming the panel works; report live-host limits plainly.

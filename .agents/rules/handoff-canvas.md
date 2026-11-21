---
trigger: model_decision
description: Guardrails for creating, editing, or reviewing a project-local handoff canvas panel (.github/extensions/<canvas-id>/ or .agents/plugins/<canvas-id>/).
---

- Load the `generate-handoff-canvas` skill before creating a new handoff canvas
  panel from scratch.
- Keep `docs/ai/handoff.md` (and `docs/ai/todo.md`) as the sole source of
  truth; the panel renders them and never creates a parallel handoff record.
- For Copilot canvas extensions (`.github/extensions/<canvas-id>/extension.mjs`),
  keep the exact folder depth, bind only `127.0.0.1:0`, enforce `Host` header +
  `timingSafeEqual` capability URL + same-origin `x-handoff-token` on writes,
  render repo text exclusively via DOM `textContent` (no `innerHTML`, no remote
  fonts/scripts), strip credentials from Git remotes, validate OS link targets
  with `realpath` containment + non-executable allowlist, and strip `ELECTRON_*`
  from child env before launching link handlers.
- For Antigravity side-pane panels (`.agents/plugins/<canvas-id>/`), use an MCP
  App (`ui://` `text/html;profile=mcp-app` + `@modelcontextprotocol/ext-apps` +
  `aux_pane` entrypoint) with no literal secrets or machine-specific paths.
- Verify security guards and dark/light/`380px` rendering via an offline smoke
  test before claiming the panel works; report live-host limits plainly.

# Agent project template: Base (Dual-Platform)

A reusable, stack-agnostic, dual-platform (**Google Antigravity** and **GitHub
Copilot**) project template with the guidance, handoff, memory, roles, and
skills that keep AI agents accurate and inexpensive. Clone or generate one
project and work seamlessly from either IDE or CLI. Contains no application
code, project lore, machine-specific paths, or secrets.

## How loading works

Files on disk cost zero tokens until loaded. Both Antigravity and GitHub Copilot
automatically discover root `AGENTS.md` and portable skills under
`.agents/skills/` (the open Agent Skills standard). Keep only `AGENTS.md` at the
root (no `GEMINI.md`). If you use GitHub Copilot Code Review or Visual Studio,
add a one-line `.github/copilot-instructions.md` containing:
`Follow [AGENTS.md](../AGENTS.md).` Do not use `@path` or `@[label](path)`
includes in either file.

| Layer | Loaded when | Platform | Cost |
|---|---|---|---|
| `AGENTS.md` | Every session | Both | Small and fixed (the only always-on file, <= ~70 lines) |
| `.agents/rules/*.md` | `trigger: model_decision` | Antigravity | Only when relevant |
| `.github/instructions/*.instructions.md` | Matching file (`applyTo`) | GitHub Copilot | Only when matching files are touched |
| `.agents/skills/*` | Names/descriptions at startup; `SKILL.md` on use | Both (portable) | Progressive disclosure |
| `.agents/agents/*` / `.github/agents/*` | When invoked / delegated | Platform-native | Only when used |
| `docs/ai/*` | When `AGENTS.md` or rules point to them | Both | Only on demand, by heading |
| `docs/ai/read-lists/*` | When a subagent starts | Both | One small file per subagent role |

> **VS Code note:** Keep `.agents/skills` enabled in `chat.agentSkillsLocations`
> so GitHub Copilot loads the single canonical skill tree in `.agents/skills/`
> without duplicating skills into `.github/skills/`.

## Adopt it

1. Click **Use this template** on GitHub (or copy the contents of `base/` into
   your repository root).
2. Edit [AGENTS.md](AGENTS.md): fill in `Project essentials` (stack, commands,
   do-not-touch paths), keep it under ~70 lines, and add only rules that apply
   to every session.
3. Update [docs/ai/cost.md](docs/ai/cost.md) with your Antigravity and/or GitHub
   Copilot plan limits and preferred models.
4. If this repository supports ClarifyDoc, run `setup-clarifydoc` during
   adoption or initial setup to generate only the needed ClarifyDoc rules,
   skills, `.gitignore` entry, and MCP guidance (otherwise create none).
5. Delete anything you do not need. Fewer files means less startup metadata.
6. Run `pwsh -NoProfile -File scripts/check-context-size.ps1` to verify
   always-on budgets, Antigravity rule caps, and skill deduplication.

## Curated skills included

Stored once in `.agents/skills/` for both platforms:

- **Core workflow:** `coordinate-task` (Antigravity main-agent coordination),
  `project-remember`, `systematic-debugging`, `verification-before-completion`.
- **On-demand generators:** `generate-handoff-canvas` (recreates a Copilot
  `.github/extensions/<id>/` canvas or Antigravity MCP App side-pane panel),
  `setup-clarifydoc` (detects ClarifyDoc support at template adoption/init and
  scaffolds only the needed ClarifyDoc config, rules, and workflow skills).

## What is deliberately missing

- **No application code, secrets, or machine-local paths.** MCP configs live as
  empty `.example` templates (`.agents/mcp-config.json.example` and
  `.mcp.json.example`); note that `.mcp.json` and Antigravity's active
  `mcp_config.json` use `"mcpServers"`, while VS Code's `.vscode/mcp.json`
  expects `"servers"`. Never commit literal secrets or absolute user paths.
- **No enabled hooks.** See `.agents/hooks/README.md` and
  `.github/hooks/README.md`.
- **No stack-specific rules.** Add project rules to `.agents/rules/*.md`
  (`trigger: model_decision`) and `.github/instructions/*.instructions.md`
  (`applyTo`) so they load only when relevant.

## Layout

```text
AGENTS.md                                  always-loaded dual-platform router (<= ~70 lines)
.agents/
  rules/                                   3 Antigravity conditional rules (agent-authoring, docs, handoff-canvas)
  agents/                                  implementer, reviewer, handoff (explore uses built-in research)
  skills/                                  6 shared portable skills (core + canvas & ClarifyDoc generators)
  hooks/README.md                          hook policy (none enabled)
  mcp-config.json.example                  empty MCP server list (Antigravity format)
.github/
  instructions/                            3 Copilot path-scoped instructions (agent-authoring, docs, handoff-canvas)
  agents/                                  coordinator, explorer, implementer, reviewer, handoff
  hooks/README.md                          hook policy (none enabled)
docs/ai/
  handoff.md                               current state; keep under about 20 KB
  handoff-history/                         dated archives, moved unchanged
  todo.md  decisions.md  memory.md
  cost.md                                  model tiers, limits, cache habits (Antigravity + Copilot)
  read-lists/                              what each kind of subagent reads
scripts/check-context-size.ps1             dual-platform context-budget & hygiene check
.mcp.json.example                          empty MCP server list (Copilot CLI / portable format)
.gitignore  .gitattributes                 secret hygiene and consistent LF endings
```

# Project guidance

The only file loaded every session; read everything else on demand. Keep this
file under 70 lines.

## Project essentials (fill in)

- **Stack & layout:** <!-- e.g., TypeScript / .NET 9; src/ app, tests/ suite -->
- **Commands:** <!-- build: `...` | test: `...` | lint/typecheck: `...` -->
- **Do not edit:** <!-- e.g., generated/, applied prod migrations -->

## When to read what

- Small task (one file, question, quick fix): read nothing extra.
- Substantial or specialized work: consult `find-skills` (if installed) once
  before research or planning.
- Multi-file or cross-session work: read `#current-handoff` in
  [docs/ai/handoff.md](docs/ai/handoff.md) and [docs/ai/todo.md](docs/ai/todo.md),
  then verify against Git and source (read `todo.md` for TODO questions).
- Large docs: locate the relevant heading and read only that section.
- Procedures (coordination, debugging, verification, memory, canvas, or
  `setup-clarifydoc` on template adoption/init): load from `.agents/skills/`.
- Explicit user direction overrides any standing rule here.

## Rules

Each rule applies only when its trigger occurs.

- **Truthful.** Run checks before claiming success. Report failures, skips and
  unknowns plainly. Never record secrets, personal data or raw transcripts.
- **Clean.** Remove own temp files and dead code; do not refactor untouched files.
- **Branches & commits.** Develop on feature branches, merge into `dev` (then
  delete the merged branch with `git branch -d`), and stop at `dev`; only PR
  `dev` into `main` when asked to release. Commit verified batches (main agent /
  coordinator only; subagents never commit). Never push/rewrite unless asked.
- **Ask first.** Stop and ask before changing IDE, user, account or billing
  settings; accessing signed-in web accounts; deploying; or destructive actions.
- **Cost & communication.** Read [docs/ai/cost.md](docs/ai/cost.md) when picking
  models or delegating. Be terse; no progress narration; end with one short
  report (files changed, exact checks, unverified).
- **Memory.** Record verified lessons with `project-remember`. Keep shared
  decisions in reviewed docs, not only in expiring memory.

## Subagents

Give each subagent only its task, exclusive file ownership and read-list from
[docs/ai/read-lists/](docs/ai/read-lists/) (`research`/`Explorer` -> `explore.md`,
`implementer`/`Implementer` -> `implement.md`, `reviewer`/`Reviewer` ->
`review.md`). `handoff`/`Project Handoff` reads `docs/ai/handoff.md` and
`docs/ai/todo.md` directly. Do not attach the handoff, history or whole
directories to other subagents unless their read-list says so.

## Map

| Need | Where |
|---|---|
| State, TODOs, decisions, lessons, cost | [docs/ai/](docs/ai/) (`handoff.md`, `todo.md`, `decisions.md`, `memory.md`, `cost.md`) |
| Conditional rules (Antigravity / Copilot) | [.agents/rules/](.agents/rules/), [.github/instructions/](.github/instructions/) |
| Subagent roles (Antigravity / Copilot) | [.agents/agents/](.agents/agents/), [.github/agents/](.github/agents/) |
| Shared skills (Antigravity + Copilot) | [.agents/skills/](.agents/skills/) |

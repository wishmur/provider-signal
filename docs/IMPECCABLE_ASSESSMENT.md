# Impeccable assessment

## Harness

This project is worked in Claude Code running inside the Claude desktop app's Code tab. Project skills at `.claude/skills/<name>/SKILL.md` with `user-invocable: true` register as `/<name>` commands. Impeccable's skill lists `init`, `shape`, `critique`, `audit`, `polish`, and `harden` among its sub-commands, and Impeccable documents Claude Code as a supported harness. `/impeccable init` and `/impeccable shape` are therefore supported here. This is not Cowork. Registration happens at session start, so a restart or a new session may be required after install.

## Availability before install

Not installed in this project. A project-local install exists in the sibling project `daybreak-tech-digest` (skill 4.2.2, engine 0.1.3, about 14 MB including a `darwin-arm64` binary), which is the basis for the footprint below. The npx cache holds launcher 4.1.0; `~/.impeccable/` contains only update-check files and no engine binary.

## Approved parameters

Project-local; `--no-hooks`; no global install; skill implementation and binary untracked; shared design artifacts tracked; `init` and `shape` run interactively with the product owner present.

## Install command (pinned; shown for confirmation before execution)

```bash
npx impeccable@4.1.0 install -y --providers=claude --scope=project --no-hooks
```

## Install record (2026-09-12)

- First attempt pinned `impeccable@4.2.2` and failed: no such launcher version on npm. The 4.2.2 figure was the skill's internal version in the sibling project, not the launcher package version. The corrected pin (4.1.0, the latest published launcher, released 2026-09-08) was shown and approved before running.
- Result: launcher 4.1.0 installed skill version 4.3.1 into `.claude/skills/impeccable/` (about 14 MB) with engine v0.1.5 (`darwin-arm64`) placed at `.claude/skills/impeccable/scripts/bin/darwin-arm64/impeccable`, and four agent files into `.claude/agents/`. No `.claude/settings.local.json` was written, so no hooks exist. Nothing global was installed.
- Git: the whole `.claude/` directory shows as ignored; no Impeccable implementation file is tracked.
- `/impeccable` did not register in the session that ran the install. `init` and `shape` remain pending and are run in a new session per the restart handling below. No manual imitation was substituted.

## Files it creates or modifies

- `.claude/skills/impeccable/`: `SKILL.md`, `reference/*.md` (about 36 command references), `scripts/` (launcher, `bin/darwin-arm64/` engine binary, data, browser helper scripts, `command-metadata.json`, `VERSION`). About 14 MB. Untracked.
- `.claude/agents/impeccable-asset-producer.md`, `impeccable-documenter.md`, `impeccable-finish-reviewer.md`, `impeccable-manual-edit-applier.md`. Untracked.
- No hook manifest with `--no-hooks`. With hooks, it would write `.claude/settings.local.json` containing a `PostToolUse` hook on `Edit|Write` (5 s timeout) and a `Stop` hook (30 s deep pass); that file is machine-local and already git-ignored by `*.local`.
- `/impeccable init` writes `PRODUCT.md` (seeded from the drafted file) and may write `.impeccable/live/config.json`.
- `/impeccable shape` writes `.impeccable/surfaces/`, `.impeccable/questions/`, and `.impeccable/design.json`.
- `/impeccable hooks on` (not planned) would write `.impeccable/config.json`, `.impeccable/config.local.json`, and `.impeccable/hook.cache.json`.

## Third-party binary

The launcher resolves the engine in this order: `IMPECCABLE_BIN`, the platform package `@impeccable/cli-darwin-arm64`, `~/.impeccable/bin/<version>/`, then a one-time download of the pinned version into that cache. The project skill's `scripts/impeccable` launcher runs a self-contained binary that ships next to it or is downloaded on first run.

## Automatic hooks

None installed. Nothing runs automatically during later edits. `npx impeccable detect src/` is reserved for Phase 3 and does not replace `init` or `shape`.

## `.gitignore` additions (shown with the command)

```
# Impeccable: local skill implementation and binary (never committed)
.claude/skills/impeccable/
.claude/agents/impeccable-*.md
# Impeccable: documented per-developer and ephemeral files
.impeccable/config.local.json
.impeccable/hook.cache.json
.impeccable/questions/
.impeccable/live/
```

Kept tracked: `.impeccable/config.json`, `.impeccable/design.json`, `.impeccable/surfaces/`, `PRODUCT.md`, `DESIGN.md`. If the installer prints an official block that differs, it is shown before use.

## Restart handling

If `/impeccable` is not recognized after install, work stops with this continuation instruction: start a new Claude Code session in `provider-signal` and send "Continue Phase 1 step 5: run `/impeccable init` seeded from `PRODUCT.md`, then `/impeccable shape` for exception queue, case detail, evidence brief, human-decision surface, audit history." No manual imitation of `init` or `shape` is substituted.

## Authority

`reference/decision/Humana Final Adjudication_1.md` remains authoritative. If `PRODUCT.md` after `init` disagrees with it on the user, evidence, claim, product boundary, or prohibited claims, the adjudication wins. Phase 3 use of `critique`, `audit`, `polish`, and `harden` may improve hierarchy, density, consistency, accessibility, responsiveness, and resilience; it must not change the locked claim, evidence, workflow, or product boundary.

## Visual target and reference gathering

Credible internal provider-operations tool: dense but readable evidence presentation, restrained color, meaningful status semantics, accessible contrast, keyboard-friendly navigation, clear focus states, efficient tables and comparison views, visible "Concept Prototype" label. Public Humana surfaces only (provider-facing pages, public directory, developer portal, public accessibility or brand materials) may inform the design; `docs/DESIGN_REFERENCES.md` records which characteristics came from public references and which are original choices. No claim of access to Humana's internal design system; the result is Humana-inspired and unofficial.

Out of scope: `delight`, `animate`, `overdrive`, `bolder`, `colorize`; chat-first interaction; decorative AI imagery; purple-to-blue gradients; cards nested inside cards; gratuitous dashboards or charts; visual effects that compete with evidence review.

# Impeccable assessment

## Harness

This project is worked in Claude Code running inside the Claude desktop app's Code tab. Project skills at `.claude/skills/<name>/SKILL.md` with `user-invocable: true` register as `/<name>` commands. Impeccable's skill lists `init`, `shape`, `critique`, `audit`, `polish`, and `harden` among its sub-commands, and Impeccable documents Claude Code as a supported harness. `/impeccable init` and `/impeccable shape` are therefore supported here. This is not Cowork. Registration happens at session start, so a restart or a new session may be required after install; that is what happened here (see the session record).

## History before install

A project-local install existed in the sibling project `daybreak-tech-digest` (skill 4.2.2, engine 0.1.3) and was the basis of an earlier footprint estimate. That estimate has been replaced below by what this repository actually installed and what `init` and `shape` actually wrote. The npx cache held launcher 4.1.0; `~/.impeccable/` contained only update-check files and no engine binary.

## Approved parameters

Project-local; `--no-hooks`; no global install; skill implementation and binary untracked; shared design artifacts tracked; `init` and `shape` run interactively with the product owner present.

## Install command (pinned; shown for confirmation before execution)

```bash
npx impeccable@4.1.0 install -y --providers=claude --scope=project --no-hooks
```

## Install record (2026-09-12)

- First attempt pinned `impeccable@4.2.2` and failed: no such launcher version on npm. The 4.2.2 figure was the skill's internal version in the sibling project, not the launcher package version. The corrected pin (4.1.0, the latest published launcher, released 2026-09-08) was shown and approved before running.
- Result: launcher 4.1.0 installed skill version 4.3.1 into `.claude/skills/impeccable/` (14 MB) with the engine at `.claude/skills/impeccable/scripts/bin/darwin-arm64/impeccable` (12.8 MB), and four agent files into `.claude/agents/`. No `.claude/settings.local.json` was written, so no hooks exist. Nothing global was installed.
- Git: the whole `.claude/` directory shows as ignored; no Impeccable implementation file is tracked.
- `/impeccable` did not register in the session that ran the install. It registered in the next session, where `init` and `shape` ran as real commands. No manual imitation was substituted.

## Installed footprint (verified 2026-09-12 after `init` and `shape`)

- `.claude/skills/impeccable/SKILL.md`: frontmatter `version: 4.3.1`, `user-invocable: true`.
- `.claude/skills/impeccable/reference/`: 35 reference files (`adapt`, `adapt.native`, `android`, `animate`, `audit`, `audit.native`, `bolder`, `clarify`, `colorize`, `craft-floor`, `craft`, `critique`, `delight`, `distill`, `doctor`, `document`, `extract`, `harden`, `hooks`, `init`, `ios`, `layout`, `live-setup`, `live`, `new-work`, `onboard`, `operate`, `optimize`, `overdrive`, `polish`, `quieter`, `routing`, `shape`, `typeset`, `visualize`) plus `reference/degraded/` with four fallback files (`asset-producer`, `documenter`, `finish-reviewer`, `manual-edit-applier`) used only when a harness has no subagents.
- `.claude/skills/impeccable/scripts/`: the `impeccable` launcher and `impeccable.cmd`; `VERSION` containing `0.1.5`; `command-metadata.json`; `bin/darwin-arm64/impeccable` (12.8 MB); `data/font-index.json` and `data/font-index-failures.json`; `live-browser.js`, `live-browser-dom.js`, `live-browser-ignores.js`, `live-browser-session.js`; `modern-screenshot.umd.js`.
- Version reporting: the `VERSION` file says `0.1.5`, while `impeccable --version` prints `4.0.0`. The two numbers name different things (engine build file versus the binary's reported version); both are recorded here rather than reconciled.
- `.claude/agents/`: `impeccable-asset-producer.md`, `impeccable-documenter.md`, `impeccable-finish-reviewer.md`, `impeccable-manual-edit-applier.md`. Untracked.
- No hook manifest with `--no-hooks`. With hooks, it would write `.claude/settings.local.json` containing a `PostToolUse` hook on `Edit|Write` (5 s timeout) and a `Stop` hook (30 s deep pass); that file is machine-local and already git-ignored by `*.local`.
- The engine's top-level CLI (`impeccable --help`) lists `detect`, `ignores`, `help`, `install`, `link`, `update`, `check`; the skill's flow verbs (`context`, `concept-seed`, `serve-question`, `surface-brief`, `signals`, `detect`, `build-phase`, `comp-spec`, `comp-diff`, `font-match`, `generate-image`, `embed-prompt`, `pin`, `hooks`) are reached through the launcher as `scripts/impeccable <verb>`.

## Session record: `init` and `shape` (2026-09-12)

- `scripts/impeccable context` ran once. It resolved `PRODUCT.md`, reported no `DESIGN.md`, no surface brief, `platform: web`, `MANUAL_DETECTOR_REQUIRED` (no hook), `INCUMBENT_WORLD_UNDOCUMENTED` (scaffold defaults in code), and `IMAGE_TOOLS: sips` (a converter; no image generation). It did not report `IMAGE_GEN_AVAILABLE`, so the build path is code-led and no build-path question was asked or recorded.
- `init` treated the existing `PRODUCT.md` as a legacy record (no schema marker), interviewed for missing durable facts only, and rewrote `PRODUCT.md` with the `<!-- impeccable:product-schema 1 -->` marker, Product Principles, Evidence on Hand, and the owner's corrections. The full diff was shown and approved before `shape`. Live mode was deferred to Phase 2 by the owner; `.impeccable/live/config.json` was not created. `.impeccable/config.json` was not created (nothing to record without image generation).
- `shape` ran its discovery interview through the structured question tool in two rounds (eight questions, all answered), then entered new-work for the visual world because the scaffold's shadcn defaults are a template, not an identity.
- `scripts/impeccable concept-seed --scope direction --mode operate` contacted the Impeccable API ("source: api") and returned seed key `5c0fb3e7`, assigned index 7, and six catalog challengers with quality-bar image URLs on impeccable.style. It wrote nothing to disk.
- `scripts/impeccable serve-question --start --payload <file>` started a local daemon on `127.0.0.1:54677`, wrote `.impeccable/questions/4a8454db.log` and `.impeccable/questions/4a8454db.state.json` (pid, port, url, heartbeat), and printed a URL and key. The page was opened in the in-app browser and rendered; it closed before an answer (exit 4), so the same hand was re-presented once through the structured question tool as the reference directs. The owner chose the assigned direction. The daemon was stopped afterward; the two question files remain and are ignored by the existing `.impeccable/questions/` rule.
- The documented post-choice telemetry ping (`concept-seed --kind assigned --from 5c0fb3e7 ...`) was sent; it carries the card kind only. Opt-out for future rounds: `DO_NOT_TRACK` or `IMPECCABLE_NO_TELEMETRY`.
- `~/.impeccable/update-check.json` was refreshed by the launcher's update check. No engine binary was placed in `~/.impeccable/`.
- `shape` wrote no `.impeccable/surfaces/` file and no `.impeccable/design.json`. In skill 4.3.1, `shape` stops before persistence: the direction contract is written into `.impeccable/surfaces/<slug>.md` by the new-work flow at build start (`scripts/impeccable surface-brief write <target> <body-file>`, path resolved by `surface-brief path`, for example `.impeccable/surfaces/src-routes-queue-tsx.md`), and `DESIGN.md` plus `.impeccable/design.json` are written by the documenter at finish. The earlier statement that `shape` writes those files was wrong and is corrected here.
- Outputs of this session live in tracked documents: `PRODUCT.md`, `docs/UX_SHAPE.md`, `docs/DESIGN_DIRECTION.md`, `docs/DESIGN_REFERENCES.md`.

## Files Impeccable creates or modifies (corrected)

| Command | Writes |
|---|---|
| install | `.claude/skills/impeccable/` (14 MB), `.claude/agents/impeccable-*.md`; with hooks, `.claude/settings.local.json` |
| `context` | nothing in the project; may refresh `~/.impeccable/update-check.json` and `~/.impeccable/staleness-check.json` |
| `init` | `PRODUCT.md`; `.impeccable/config.json` (`buildPath`) only when image generation exists and the user answers; `.impeccable/live/config.json` only when live setup runs |
| `shape` | no project files; the brief is returned for confirmation |
| `concept-seed` | nothing; network call to the Impeccable API; telemetry ping after the choice |
| `serve-question` | `.impeccable/questions/<key>.log` and `<key>.state.json`; a local daemon |
| new-work build (Phase 2) | `.impeccable/surfaces/<slug>.md`; with image generation, `.impeccable/mocks/`; on comp-led builds, `.impeccable/build/` and `.impeccable/review/` |
| documenter (Phase 2 finish) | `DESIGN.md`, `.impeccable/design.json` |
| `hooks on` (not planned) | `.impeccable/config.json`, `.impeccable/config.local.json`, `.impeccable/hook.cache.json` |

## Third-party binary and network

The launcher resolves the engine in this order: `IMPECCABLE_BIN`, the platform package `@impeccable/cli-darwin-arm64`, `~/.impeccable/bin/<version>/`, then a one-time download of the pinned version into that cache. Here the binary ships next to the launcher inside the project skill. Network activity observed in this session: the concept-seed API call, the telemetry ping, the update check, and catalog image URLs on impeccable.style referenced by the decision page. No project content other than the card kind leaves the machine through these paths; the grounded candidates and product facts are authored locally.

## Automatic hooks

None installed. Nothing runs automatically during later edits. `scripts/impeccable detect --json <targets>` is the manual replacement in Phase 2 and Phase 3, run once per finished surface as `MANUAL_DETECTOR_REQUIRED` directs.

## `.gitignore` (in place)

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

Kept tracked when they come to exist: `.impeccable/config.json`, `.impeccable/design.json`, `.impeccable/surfaces/`, `PRODUCT.md`, `DESIGN.md`. `.impeccable/mocks/`, `.impeccable/build/`, and `.impeccable/review/` are Phase 2 decisions (they only appear on comp-led builds, which this harness cannot run without image generation).

## Restart handling

Resolved: the new session registered `/impeccable`, and `init` and `shape` ran as real commands. The instruction for any future restart is unchanged: start a new Claude Code session in `provider-signal` and name the exact step to continue.

## Authority

`reference/decision/Humana Final Adjudication_1.md` remains authoritative. After `init`, `PRODUCT.md` was compared against it on user, evidence, claim, product boundary, and prohibited claims; the one wording difference (the bounded attachment phrase "attached through the relevant location to a named 2026 plan") was raised, ruled a precision clarification consistent with the adjudication's definition, and applied to every headline reuse in the repository. The adjudication itself was not edited. Phase 3 use of `critique`, `audit`, `polish`, and `harden` may improve hierarchy, density, consistency, accessibility, responsiveness, and resilience; it must not change the locked claim, evidence, workflow, or product boundary.

## Visual target and reference gathering

Confirmed and recorded: direction in `docs/DESIGN_DIRECTION.md`, public references in `docs/DESIGN_REFERENCES.md`. Public Humana surfaces only informed the design; no claim of access to Humana's internal design system; the result is Humana-inspired and unofficial.

Out of scope: `delight`, `animate`, `overdrive`, `bolder`, `colorize`; chat-first interaction; decorative AI imagery; purple-to-blue gradients; cards nested inside cards; gratuitous dashboards or charts; visual effects that compete with evidence review.

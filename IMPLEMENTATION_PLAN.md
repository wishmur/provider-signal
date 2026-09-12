# ProviderSignal Implementation Plan (Phase 1)

Concept Prototype. Evidence review for directory operations. Not an official Humana product.

## Locked decision and claim

Provider Data is Mixed on C1; no candidate fully clears the strict rubric. Provider Data is built as the strongest exploratory take-home prototype. The investment thesis is unvalidated and is stated as such wherever the headline appears.

Headline (verbatim wherever used): In a pre-registered sample of 250 Family Medicine practitioners in Humana's public Medicare Advantage directory, 77 (30.8%, a substantive evidence-conflict rate, not a directory error rate) had at least one substantive evidence conflict across public records, and 76 were attached through the relevant location to a named 2026 plan.

Locked counts (never interchanged): 29 external-consensus B1; 46 multi-source B1; 0 overlap; 75 any B1 address conflict; 4 B2 (2 overlapping B1, 2 B2-only); 77 union; 76 plan-attached; 0 Lane A in 350.

Promise: The prototype reduces the effort required to investigate provider-data conflicts by assembling dated, cited evidence and preparing the next verification action while leaving directory truth and every downstream change under human authority.

Prohibited claims (full list in the adjudication, kept local under `reference/`): no error rate; no "correct address"; no independent corroboration between NPPES and Care Compare; no registry-hygiene or vendor claims from zero Lane A; no measured value, accuracy, or outcomes; no claim that R1 or R3 passed; 2027 network references are a data-model insight, not errors.

## Product boundary

Does: detect and classify evidence conflicts deterministically; assemble Humana, NPPES, Care Compare, and LEIE evidence with provenance and dates; explain disagreement and unknowns; show contrary evidence; rank verification urgency; recommend a verification step; draft outreach or escalation; record the human's action.

Does not: decide which value is correct; modify directory data; treat external agreement as truth; hide missing evidence; make clinical or utilization-management decisions. No write path exists in the code.

## Architecture

Stack: the existing TanStack Start + React 19 + TypeScript + Tailwind v4 + shadcn scaffold. One dependency to add in Phase 2: `@anthropic-ai/sdk`. No database, no authentication, no external infrastructure.

Layers (domain imports nothing from React; presentation imports domain and state only):

- `src/domain/` (pure TypeScript): types, normalization (port of the probe's `full_key`, `base_key`, `zip5`, `phone`), evidence-state classification (port of B1/B2/B3/B4, telehealth rule, Lane A), queue routing (current-plan-year filter), audit reducer. Unit-tested for parity with the probe.
- `src/data/`: curated fixture snapshot, provenance manifest, cached AI briefs, loader.
- `src/ai/`: zod input and output schemas, versioned system prompt, guards, limits, and one server function (`brief.server.ts`). The browser sends only an allowlisted `caseId`.
- `src/state/`: React context store for cases, briefs, and audit events; persisted to `localStorage`.
- `src/routes/`: `/queue`, `/cases/$caseId`, `/audit`. The root shell shows the Concept Prototype label.
- `scripts/build-fixtures.py`: reads the read-only probe-cache copy under `reference/empirical/` and writes the fixture snapshot with only NPI, specialty code, location fields, plan identifiers, source, and dates. The cache is never committed.

Embedded model: `ANTHROPIC_MODEL=claude-sonnet-5`, `ANTHROPIC_EFFORT=medium`, configurable by environment. Phase 2 compares medium and high on the hardest multi-source case; medium stays unless observed output justifies high. Claude Opus 5 is the builder model, not the product default. The application requires an Anthropic Console API key in `ANTHROPIC_API_KEY`, server-side only. The exact API model identifier is confirmed from official SDK documentation before Phase 2, never inferred from a display name.

Server boundary and public-demo cost controls: allowlisted fixture ids only; no user prompt or evidence payload from the browser; canonical fixture loaded and `CaseInput` validated on the server; bounded input size and `max_tokens`; per-case cached results; `AI_MODE` kill switch; a per-instance call ceiling as a courtesy control only; usage logging without secrets; key deleted or rotated in the Anthropic Console on 2026-09-15. Deployment posture (current constraint, see `docs/DEPLOYMENT_AND_SECRETS.md`): the public Lovable URL runs with no key in cached mode; live calls happen from the presenter's machine.

What is real, cached, mocked, synthetic:

| Element | Status |
|---|---|
| Humana FHIR, NPPES, Care Compare records for real cases | Real public records, cached snapshot (retrieved 2026-09-11) |
| LEIE check | Real exact-NPI match during the probe; result cached |
| Current-year plan attachment (directory relationship role → network → 2026 InsurancePlan reference; one representative identifier) | Real, computed from the cached InsurancePlan index; never participation |
| Deterministic classification | Real, recomputed in-app from the snapshot |
| Anthropic evidence brief | Real live call on demand from the presenter's machine; cached output labeled "Cached" elsewhere or on failure |
| Outreach send, escalation ticket, downstream proposal queue | Mocked (recorded in audit history only) |
| Authoritative-risk cases (deactivated NPI, LEIE match) | Synthetic, non-numeric identifiers, labeled, excluded from all figures |
| Access control, monitoring | Simulated labels only; documented in Phase 3 governance |

## Vertical workflow (six surfaces)

Exception queue → case detail (evidence comparison) → AI evidence brief → human action → audit history → uncertainty or failure state. Per-screen detail in `docs/UX_SHAPE.md` (confirmed through `/impeccable shape`); visual direction, tokens, and component inventory in `docs/DESIGN_DIRECTION.md`; public references in `docs/DESIGN_REFERENCES.md`.

## Deterministic baseline (rules only)

Normalize address, phone, and zip; join Humana PractitionerRole → Location → Organization → network → InsurancePlan and keep only current-plan-year MA networks; look up NPPES, Care Compare, and LEIE; compare full and base keys; classify each pair as match, format-only, single-source, external-consensus conflict, multi-source conflict, telehealth-uncertain, or unmeasured; flag B2 classification, B3 phone, B4 staleness, and Lane A registry signals; sort the queue by evidence class, current-year attachment, and external recency; write an audit event for every human action. This baseline is complete without the model and is the rollback state.

What the model adds on variable input: a dated, cited synthesis of what disagrees; competing plausible explanations labeled as hypotheses; contrary evidence; explicit missing evidence; a case-specific verification-urgency recommendation with reasons; a grounded outreach or escalation draft that asks for confirmation and never proposes a value. Rules and templates cannot reliably produce case-specific explanations or drafts across the multi-location, relocation, alias, and stale-record patterns in the 109 real pairs. The model ranks urgency, never truth.

## AI contract

Schemas, guards, and failure handling are in `docs/AI_CONTRACT.md`. Every summary item and every claim carries citations that the server resolves against the canonical input; the schema has no field for a correct, preferred, likely-correct, or recommended directory value; abstention is first-class; every attempt logs model id, prompt version, schema version, evidence hash, latency, and outcome. A committed record of at least one successful local live call proves the AI component functions.

## Fixtures

Eleven underlying records plus one simulated failure mode (see `docs/FIXTURE_PLAN.md`): three recent, current-year-attached, telehealth-clean consensus conflicts; one multi-source ambiguity case with a supporting classification conflict; one stale-consensus contrast; one clean match; one format-only case; one real missing-source abstention case; one real single-source case; two synthetic authoritative-risk cases. The simulated failure mode reuses EC-03. Synthetic cases never enter figures.

## Service design (C2)

Current-state and future-state maps with labeled assumptions are in `docs/SERVICE_DESIGN_ASSUMPTIONS.md`. We hold no verified evidence of Humana's internal workflow; every Humana-specific step is an assumption with a stated basis and a validation question.

## Phase 2 acceptance criteria

1. One real, variable case processed by a live Anthropic call with schema-valid, guard-passing output.
2. A primary demo case and a backup case, both real and cached.
3. A visible abstention case and a visible AI-failure state.
4. Every AI claim links to a source identifier and date shown on screen.
5. A human action recorded in audit history with evidence hash, model id, prompt and schema versions.
6. Deterministic evidence view fully usable when the AI is unavailable, invalid, or rejected.
7. Real, cached, mocked, and synthetic labels visible on every case and every brief.
8. No code path writes to any directory or source; proposals only.
9. Loading, empty, error, and recovery states work on all three routes.
10. Only the six surfaces exist; any expansion is raised, not built.

Prerequisite before any Phase 2 code: `.env` confirmed ignored, and one isolated API smoke test passes (exact Sonnet 5 identifier from official docs, one live request, `zodOutputFormat` parsing with non-null `parsed_output`, schema and boundary-guard validation, recorded latency and token usage, no secrets logged).

## Constraints preserved for Phase 3

Value model: monthly eligible exceptions × adoption × minutes saved × loaded labor cost − model, integration, and operating costs. Monthly volume is an assumption; low, base, and high scenarios with at least a 10× range; every input labeled measured, sourced, or assumed; no realized ROI.

Evaluation and governance thresholds are set after observing model output, covering citation faithfulness, unsupported claims, evidence completeness, conflict identification, uncertainty and abstention, latency and cost, countermetrics and segmentation, offline/shadow/pilot/live stages, access control, auditability, monitoring, correction and escalation, override, version logging, automation-bias safeguards, and rollback to the rules-only queue.

Deployment gate: before any public live endpoint, either verify a secure server-side secret path and enforceable platform-level rate limiting, or retain the cached-public / live-local split. In-memory per-isolate throttling is never represented as sufficient protection for a public endpoint.

## Impeccable

Assessment and session record in `docs/IMPECCABLE_ASSESSMENT.md`. Project-local install with `--no-hooks`; nothing global; skill implementation and binary untracked; shared design artifacts tracked. `init` and `shape` ran interactively on 2026-09-12: `PRODUCT.md` carries the Impeccable schema marker and the owner's confirmed additions; `docs/UX_SHAPE.md` is the confirmed six-surface brief; `docs/DESIGN_DIRECTION.md` records the chosen world (Public Registry Record, seed key `5c0fb3e7`), tokens, and component inventory; `docs/DESIGN_REFERENCES.md` records the public references. The direction contract is persisted to the Impeccable surface brief by the new-work flow at Phase 2 build start, and `DESIGN.md` is written by the Impeccable documenter at Phase 2 finish, never before the build.

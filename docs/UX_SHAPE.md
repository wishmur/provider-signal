# UX shape (confirmed)

Status: confirmed through `/impeccable shape` on 2026-09-12 with the product owner answering every interview round. Supersedes the provisional draft. Visitor mode for all six surfaces: Operate. Visual world and tokens: `docs/DESIGN_DIRECTION.md`. Public references: `docs/DESIGN_REFERENCES.md`. This document changes nothing in the locked claim, evidence, workflow, or product boundary; the adjudication under `reference/decision/` remains authoritative.

## 1. Job and audience

A Humana provider-data operations specialist works a directory-exception queue for Family Medicine practitioners on current-plan-year Medicare Advantage networks, at an office desk on a large monitor, for long stretches, keyboard in hand. They open a flagged practitioner-location pair, see every public record with its date and source, decide what verification to request, and record why. Secondary audience: take-home reviewers judging the workflow, evidence handling, and governance.

## 2. Outcome and proof

Primary task: reach a recorded, justified verification action on a pair without the system asserting directory truth. Proof on screen: dated, source-named records from Humana's public Plan-Net FHIR directory, NPPES, Care Compare, and LEIE; the deterministic evidence class with its rule names; a cited brief whose every claim resolves to a visible cell; an audit event for every human action. Whether this is faster than manual investigation is an unmeasured hypothesis and is never claimed in the interface.

## 3. Selected direction

Public Registry Record (Impeccable direction round, seed key `5c0fb3e7`, assigned card chosen). Structural thesis: every value on screen is a dated public record with its registry named, laid out the way the registries lay it out. Sequence: queue → case → brief → action → audit. Focal moment: the evidence comparison with citation-to-cell highlighting and character-aligned normalized keys. Implementation consequence: one ruled register grammar across all six surfaces; stamped provenance plates on every panel; tabular monospace for every identifier, key, and date; hatch texture wherever a state must not depend on color. Details and tokens in `docs/DESIGN_DIRECTION.md`.

## 4. Scope and boundaries

- Fidelity: production-quality screens for a concept prototype; six surfaces; three routes (`/queue`, `/cases/$caseId`, `/audit`) plus persistent shell chrome.
- The six surfaces are the Phase 2 scope ceiling. A seventh surface requires explicit approval.
- Shell chrome (not a surface): compact top bar with product name, "Concept Prototype" plate, Queue and Audit navigation, AI-mode indicator (Live / Cached / Off), and a provenance legend popover defining Real, Cached, Mocked, Synthetic. Nothing else: no dashboard, no statistics, no sample figures, no logos.
- The headline figure and the sample statistics never appear inside the product UI. They live in the presentation only, always with their complete boundary sentence.
- Untouched: the locked claim, counts, prohibited claims, the AI contract, the fixture plan, and the no-write-path boundary.
- Anti-goals: chat-first interaction; decorative AI imagery; purple-to-blue gradients; cards nested in cards; KPI tiles or charts; entrance animation; pill buttons; icon-only controls without labels; any marker that reads as "correct" or "wrong" on a value; any sort that hides the rules-only order.

## 5. States and ranges

Content ranges from `docs/FIXTURE_PLAN.md` and `docs/AI_CONTRACT.md`:

| Item | Minimum | Typical | Maximum |
|---|---|---|---|
| Real cases in the queue | 9 (fixed snapshot) | 9 | 9 |
| Synthetic edge cases | 2 | 2 | 2 |
| Simulated failure case | 1 (FAIL-01 on EC-03) | 1 | 1 |
| Humana records per case | 1 | 1 | 1 |
| NPPES practice locations per case | 0 (NOT_FOUND) | 1 | 2 |
| Care Compare rows per case | 0 (NOT_FOUND) | 1 | 3 |
| Phones per source | 0 | 1 | 2 |
| Address line 1 length | 10 chars | 25 chars | 45 chars |
| Brief summary items | 1 | 3 | 6 |
| Hypotheses | 0 (full abstention) | 2 | 4 |
| Contrary, missing evidence items | 0 | 2 | 4 |
| Urgency reasons | 1 | 2 | 4 |
| Draft body | 0 (kind none) | 600 chars | 1,200 chars |
| Audit events | 0 | 20 | 200 |
| Retry attempts on failure | 0 | 1 | unbounded, count shown |

Material states per surface are listed in section 6. Global: loading (skeleton, never spinners in content), empty, error with reason and retry, storage unavailable (in-memory fallback, labeled), AI disabled (cached only, labeled).

## 6. Interaction and layout by surface

### Surface 1: Exception queue (`/queue`)

- Objective: pick the next pair worth verifying.
- Register header (one line): frame, specialty, source directory, plan year 2026, snapshot retrieval date 2026-09-11, active ordering ("Rules-only: evidence class, 2026 attachment, external recency"), and counts "9 real cases · 2 synthetic edge cases, not counted".
- Fixed-column table, full width, no side rail. Columns in order: case id (typeable, monospace); NPI or "Synthetic NPI — not a real provider"; Humana-listed location (city, state, then line 1); evidence class (text chip); 2026 plan attachment (flag plus one representative identifier in monospace, captioned "directory relationship, not participation"); external recency (NPPES last_updated as a date; Care Compare shown as "dataset 2026-08-18"); flags (phone, stale, telehealth-uncertain, registry signal) as icon-plus-text chips; provenance plate; queue state (new, brief ready, abstained, actioned, failed); AI urgency (level plus a "drivers" disclosure when a brief exists; otherwise "no brief").
- Ordering: default and reset state is rules-only and labeled as such. Any column, including AI urgency, can be chosen as sort explicitly; the header then reads "Sorted by: AI urgency (model ranking of verification urgency, not truth)" with a one-click return to rules-only. The rules-only order is the rollback state.
- Filters: evidence class, flag, queue state. Filters never hide the synthetic section's heading.
- Synthetic section: a separate, always-visible section beneath the real rows, headed "Synthetic edge cases · not counted in any figure", rows hatched and plated SYNTHETIC, openable so the urgent registry-signal treatment can be shown.
- Row states: default, hover, focus (ring), selected (full-width selection field), actioned (muted with check), abstained or non-evaluable (hatch), synthetic (hatch plus plate).
- Error and uncertainty: empty queue ("No cases in the snapshot", reload); fixture load failure (error panel with reason, retry); AI urgency absent (rules-only ordering stays labeled).
- Keyboard: `j` and `k` move focus between rows; `Enter` opens; `/` focuses the filter input; `Esc` clears focus from the filter.
- Downstream: case detail.

### Surface 2: Case detail, evidence comparison (`/cases/$caseId`)

- Objective: understand exactly what disagrees.
- Layout at 1280px and wider: main column (comparison) plus a 380px right rail holding the brief panel above the action panel. Between 1024px and 1279px the rail stacks below the comparison at full width. The comparison table scrolls horizontally inside its own container when narrower than its columns; the page never scrolls horizontally.
- Case header: case id, NPI or synthetic label, specialty, evidence class with rule names, provenance plate, retrieval date, and the plan-attachment line: "Attached through this location to a named 2026 plan: yes · representative H0473-003-000-2026 · directory relationship, not participation", with the network references available on disclosure.
- Comparison table: sources as columns (Humana Plan-Net FHIR | NPPES | Care Compare | Registry: NPPES status, LEIE), fields as rows (address line 1, line 2, city, state, ZIP, normalized full key, normalized base key, phone, taxonomy or classification, telehealth, status, source date, retrieved). A source with several locations stacks them inside its column as labeled sub-cells (Location 1, Location 2). Each row carries a comparison marker relative to the Humana record: matches, differs, format-only, not available; always icon plus text.
- Normalized-key rows are rendered in tabular monospace with differing characters emphasized by weight and underline, so a differing character sits under its counterpart. No color-only difference.
- Missing source: the whole column becomes a "Not available" plate with the reason code (GONE, NOT_FOUND, REQUEST_FAILED) and hatch fill. Single-source pairs carry a banner "Not B1-evaluable: single source". Unmeasured telehealth carries a banner naming the unmeasured rule.
- Classification panel under the table: class, rule names, B1-evaluable flag, telehealth rule state, known unknowns, constraints (the boundary restated as it travels with the evidence).
- Actions: "Request evidence brief" (`b`; disabled with "Cached only" when AI mode is not live); "Go to action" (`a`). Nothing on this surface marks a value as correct or wrong.
- States: loading skeleton; not found (inside the shell); single-source; unmeasured; synthetic (hatched header plate).
- Downstream: brief panel.

### Surface 3: AI evidence brief (right-rail panel)

- Objective: get a cited explanation and a proposed next step.
- Panel header: plate (LIVE, CACHED, or SYNTHETIC), model id, prompt version, schema version, latency, short evidence hash.
- Sections in fixed order, matching the schema: abstention notice (partial or full, with reason and what would unblock); summary (each item with citation chips); disagreements by field; hypotheses (each labeled "Hypothesis", with kind, supporting and contrary citations, and how to test); contrary evidence; missing evidence with what it would resolve; verification urgency (level, scope label "verification urgency, not truth", reasons with citations); recommended verification step with rationale; draft preview (subject and body) with "Edit in action panel".
- Citation chip: source ref, field path, and the server-resolved canonical value or date. Hover or focus highlights the matching comparison cell; activation scrolls to it. The model never supplies quoted values; the chip shows what the server resolved.
- Controls: Request brief; Regenerate (live only); View cached; Accept into working view.
- States: idle (call to action, or "Cached only" when AI is not live); loading (skeleton, elapsed time, attempt count); live success; cached; abstained; failure (surface 6 replaces the panel body); disabled (cached brief served with its label).
- Downstream: action panel.

### Surface 4: Human action (right-rail panel below the brief)

- Objective: record what the specialist decides.
- Action type (radio): request provider outreach; escalate to contracting; mark reviewed, no action; defer pending evidence.
- Draft editor: inline editable text area, prefilled from the brief's draft for outreach or escalation, with the helper line "Drafts ask the provider to confirm; they never propose a value". Empty and editable when no brief exists.
- Rationale: required text area with helper text; confirm is blocked until an action type is chosen and the rationale has non-whitespace content; the error text names the missing field.
- Disagreement checkbox "I disagree with the brief's recommendation" appears only when an accepted brief exists and sets the override flag.
- Without an accepted brief the panel carries the notice "Rules-only: no accepted brief for this case" and remains fully usable.
- Confirm opens a dialog that restates the action type and rationale and says: "This records a proposal only. No directory data changes." Confirm writes the audit event, sets the queue state to actioned, and shows a toast "Proposal queued (mocked)". Cancel returns focus to the confirm button.
- Downstream: audit event; queue state; mocked proposal notice.

### Surface 5: Audit history (`/audit`, plus a per-case timeline at the bottom of the case detail main column)

- Objective: see what was shown and what was done.
- One ruled vertical time axis; every event pinned to its ISO timestamp in monospace. Event types: case opened; brief requested (model id, prompt version, schema version, evidence hash, outcome); brief invalid, rejected, failed, or abstained; action recorded (type, rationale, draft hash, override flag); data reset.
- Filters: case id, event type. Controls: Export JSON (mocked; shows a labeled notice, writes nothing); Reset prototype data (dialog; on confirm the new history begins with a data-reset event).
- States: empty ("No events yet"); storage unavailable (banner: history kept in memory for this session only, labeled).
- Terminal.

### Surface 6: Uncertainty and failure state (panel body within surface 3; reflected as a queue state)

- Objective: keep working when the AI cannot help.
- Kinds and copy: unavailable (API error, timeout, rate limit, or refusal stop reason); invalid (schema failure after one retry); rejected (guard failure with its reason class; violating content is never rendered); abstained (full abstention with reason and the evidence that would unblock); disabled (AI mode off, no key, or ceiling reached).
- Panel: kind plate, plain-language reason, attempt count, timestamp of the last attempt, and three controls: Retry (unlimited, count increments); Load cached brief (when one exists, labeled Cached); Proceed rules-only (focuses the action panel).
- The evidence comparison stays intact and interactive throughout. Retry failing again stays in the failure state with the incremented count. The queue row shows failed or abstained.
- Simulated: FAIL-01 applies a timeout to EC-03's record under a separate case id.
- Downstream: action panel remains available.

## 7. Vertical flow

Queue → open case → read comparison → request brief → read brief, or failure or abstention → choose action and rationale → confirm → audit event → back to queue with updated state.

## 8. Keyboard map

`j` and `k` move between queue rows; `Enter` opens; `/` focuses the queue filter; `b` requests a brief; `a` focuses the action panel; `Esc` closes dialogs and popovers. Every interactive element shows a visible focus ring; focus is never trapped except inside an open dialog.

## 9. Constraints and open decisions

- Platform: web, desktop-first, light theme only, usable to 1024px, WCAG reflow only below that. TanStack Start, React 19, Tailwind v4, shadcn primitives already in the scaffold.
- Accessibility: WCAG AA contrast on every text and state pair (verified values in `docs/DESIGN_DIRECTION.md`); keyboard operability; visible focus; no meaning by color alone; `prefers-reduced-motion` removes transitions.
- Localization: English only; dates ISO `YYYY-MM-DD`; no currency.
- Reusable components: inventory in `docs/DESIGN_DIRECTION.md`.
- Decisions a builder must not invent: any new surface; any figure or statistic in the UI; any marker implying a value is correct; any sort that hides the rules-only label; any write path; any Humana mark or logo.
- Deferred to Phase 2 start (not open for the builder to choose): the direction contract is written into the Impeccable surface brief by the new-work flow before the first build; DESIGN.md is written at finish by the Impeccable documenter from the built artifact.

## 10. Confirmed decisions log (2026-09-12)

1. Headline figure: not in the product UI at all.
2. Comparison layout: sources as columns, fields as rows.
3. Brief and action panels: persistent right rail beside the comparison on desktop, stacked below at narrower widths.
4. Scene: desktop-first, light theme, keyboard-driven, usable to 1024px, no phone-specific layout.
5. Ordering: rules-only default and reset state; AI urgency is a visible, explicitly selectable sort with its drivers shown.
6. Synthetic cases: separate always-visible section below the real queue, labeled not counted.
7. Shell: name, Concept Prototype plate, Queue and Audit navigation, AI-mode indicator, provenance legend popover. Nothing else.
8. Action panel: inline editable draft; confirm dialog restating proposal-only; unlimited retry with a visible count.
9. Visual world: Public Registry Record (the roll), seed key `5c0fb3e7`.

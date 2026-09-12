# Product

<!-- impeccable:product-schema 1 -->

<!-- Derived from the final adjudication (kept local under reference/). Where this file and the adjudication disagree on user, evidence, claim, product boundary, or prohibited claims, the adjudication wins. -->

## Platform

web

## Users

Primary: a Humana provider-data operations specialist working a directory-exception queue for Family Medicine practitioners on current-plan-year Medicare Advantage networks. They open a flagged practitioner-location pair, need to see every public record with its date and source, decide what verification to request, and record why. Escalation paths: provider outreach and contracting.

Secondary audience: take-home reviewers evaluating the workflow, evidence handling, and governance.

## Product Purpose

Reduce the effort required to investigate provider-data conflicts by assembling dated, cited evidence and preparing the next verification action, while leaving directory truth and every downstream change under human authority. Prototype session success means the specialist reaches a recorded, justified action without the system asserting directory truth. Whether this is faster than manual investigation is an unmeasured hypothesis for a future pilot.

## Positioning

Not a reconciliation engine, not a truth engine, not a chatbot. The deterministic layer detects and classifies evidence conflicts; the model explains disagreement, uncertainty, urgency, and next steps with citations; the human decides. Registry-verifiable Lane A exceptions were 0 of 350 across the two sampled specialty frames. This does not establish Humana-wide registry hygiene or vendor performance. The prototype focuses on ambiguous multi-source disagreements that public records cannot adjudicate.

## Evidence (locked)

In a pre-registered sample of 250 Family Medicine practitioners in Humana's public Medicare Advantage directory, 77 (30.8%, a substantive evidence-conflict rate, not a directory error rate) had at least one substantive evidence conflict across public records, and 76 were attached through the relevant location to a named 2026 plan. Counts: 29 external-consensus B1; 46 multi-source B1; no overlap between those B1 classes; 75 with any B1 address conflict; 4 with B2 classification conflicts, including 2 overlapping B1 and 2 B2-only; union 77; Lane A 0 of 350 across two specialty frames. C1 remains Mixed and the investment thesis is unvalidated.

## Operating Context

Concept prototype, single user, local state, curated cached public data with an optional live Anthropic call. No authentication, no database, no directory write path. Runs on TanStack Start. The public deployment runs in cached mode with no API key; the local presentation demonstrates the live model call from the presenter's machine.

Humana's internal workflow and design system are unknown. Every internal workflow step shown or described is a labeled assumption (`docs/SERVICE_DESIGN_ASSUMPTIONS.md`). The prototype has no connection to any internal Humana system.

## Capabilities and Constraints

- Six surfaces only: exception queue, case detail, evidence brief, human action, audit history, failure state. These six are the Phase 2 scope ceiling; a seventh surface requires explicit approval.
- Real, cached, mocked, and synthetic content are labeled on screen; synthetic never enters figures.
- Plan attachment is a directory relationship (role → network → 2026 InsurancePlan reference), shown as a flag plus one representative identifier, never as participation.
- Prohibited on any surface: stating an address is wrong or correct; showing 30.8% without "a substantive evidence-conflict rate, not a directory error rate" in the same sentence; presenting NPPES and Care Compare agreement as independent corroboration; claiming measured savings, accuracy, or outcomes; presenting 2027, employer, or Medicaid network references as errors; implying an official Humana product.
- Accessibility: WCAG AA contrast, keyboard operability, visible focus, no motion-dependent meaning.

## Terminology

Evidence conflict (what was measured); verification exception (a current-year-attached conflict); directory error (requires human adjudication; none exist in this run); hypothesis (a plausible explanation, never a finding); abstention (the model or rules decline to characterize); proposal (the only output of a human action).

## Voice

Plain, operational, specific. Dates and sources are named. No marketing register.

## Brand commitments

Humana-inspired internal tool, unofficial. No Humana marks or logos: this prohibits implying an official Humana product. Naming Humana as the public-directory data source is correct and expected, and restrained visual cues inspired by Humana's public interfaces are permitted. Visible "Concept Prototype" label on every surface.

Binding visual constraint (volunteered by the product owner, recorded without expansion): the prototype should resemble a credible internal operations tool for a specialist working a queue, with dense but readable evidence tables, restrained color, and meaningful status semantics. It is not a consumer health site or an executive dashboard.

## Evidence on Hand

- Empirical results, pair analyses, and the probe cache under `reference/empirical/` (gitignored; read-only; never committed). Every real case derives from these.
- The eleven pinned cases plus one simulated failure mode in `docs/FIXTURE_PLAN.md`.
- The final adjudication under `reference/decision/` (gitignored; authoritative).
- Explicit absences that future work must not fabricate: no testimonials, no measured outcomes, no verified Humana errors, no verified internal workflow, no internal design-system access, no logos, no official marks.

## Product Principles

1. Evidence before assertion: every evidence claim carries its source and date; the interface never states which value is true.
2. Human authority is structural: proposals are the only output, rationale is required, and no write path exists.
3. Uncertainty is a designed state: abstention, missing sources, and AI failure are first-class surfaces.
4. Rank urgency, never truth: ordering exposes its drivers and no value is marked likely-correct.
5. Provenance is always visible: real, cached, mocked, and synthetic content is labeled. The headline figure always carries its complete boundary in the same sentence. If a surface cannot accommodate that sentence, the figure must not appear there; the qualification cannot be moved to a caption, tooltip, footnote, or speaker notes.

# Product

<!-- Derived from the final adjudication (kept local under reference/). Where this file and the adjudication disagree on user, evidence, claim, product boundary, or prohibited claims, the adjudication wins. -->

## Platform

web

## Users

Primary: a Humana provider-data operations specialist working a directory-exception queue for Family Medicine practitioners on current-plan-year Medicare Advantage networks. They open a flagged practitioner-location pair, need to see every public record with its date and source, decide what verification to request, and record why. Escalation paths: provider outreach and contracting.

Secondary audience: take-home reviewers evaluating the workflow, evidence handling, and governance.

## Product Purpose

Reduce the effort required to investigate provider-data conflicts by assembling dated, cited evidence and preparing the next verification action, while leaving directory truth and every downstream change under human authority. Success for a session: the specialist reaches a recorded, justified action faster than by manual multi-system lookup, without the system ever asserting which value is true.

## Positioning

Not a reconciliation engine, not a truth engine, not a chatbot. The deterministic layer detects and classifies evidence conflicts; the model explains disagreement, uncertainty, urgency, and next steps with citations; the human decides. Registry-verifiable exceptions were rare in the sample (0 of 350); the product's value is on what remains after ordinary registry checks: ambiguous multi-source disagreement that no public registry can adjudicate.

## Evidence (locked)

In a pre-registered sample of 250 Family Medicine practitioners in Humana's public Medicare Advantage directory, 77 (30.8%, a substantive evidence-conflict rate, not a directory error rate) had at least one substantive evidence conflict across public records, and 76 were attached to a named 2026 plan. Counts: 29 external-consensus; 46 multi-source; 75 any address conflict; 4 classification; 0 Lane A. The investment thesis is unvalidated (C1 Mixed).

## Operating Context

Concept prototype, single user, local state, curated cached public data with an optional live Anthropic call. No authentication, no database, no directory write path. Runs on TanStack Start. The published URL runs in cached mode with no API key; live model calls occur only from the presenter's machine.

## Capabilities and Constraints

- Six surfaces only: exception queue, case detail, evidence brief, human action, audit history, failure state.
- Real, cached, mocked, and synthetic content are labeled on screen; synthetic never enters figures.
- Plan attachment is a directory relationship (role → network → 2026 InsurancePlan reference), shown as a flag plus one representative identifier, never as participation.
- Prohibited on any surface: stating an address is wrong or correct; showing 30.8% without "a substantive evidence-conflict rate, not a directory error rate" in the same sentence; presenting NPPES and Care Compare agreement as independent corroboration; claiming measured savings, accuracy, or outcomes; presenting 2027, employer, or Medicaid network references as errors; implying an official Humana product.
- Accessibility: WCAG AA contrast, keyboard operability, visible focus, no motion-dependent meaning.

## Terminology

Evidence conflict (what was measured); verification exception (a current-year-attached conflict); directory error (requires human adjudication; none exist in this run); hypothesis (a plausible explanation, never a finding); abstention (the model or rules decline to characterize); proposal (the only output of a human action).

## Voice

Plain, operational, specific. Dates and sources are named. No marketing register.

## Brand commitments

Humana-inspired internal tool, unofficial. No Humana marks or logos. Visible "Concept Prototype" label.

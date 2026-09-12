# Fixture plan (pinned)

Source of every real case: `reference/empirical/results_v3_1.json` (PB frame, Family Medicine) and the read-only probe-cache copy under `reference/empirical/cache/` with `analysis_ec_pairs.json` and `analysis_ms_pairs.json`. Those inputs are never modified, deleted, or committed. Only the minimum presentation-safe fields are extracted into committed fixtures.

Fields kept: NPI (real cases only), taxonomy code, Humana Location id (first eight characters as display id), Humana address fields and phone, NPPES location addresses and phones, NPPES `last_updated` and status, Care Compare rows (address, phone, telehealth flag), Care Compare dataset date (2026-08-18), LEIE result, current-year plan attachment (flag, representative identifier, network references), telehealth rule result, deterministic labels, retrieval date.

Excluded: practitioner and organization names, role ids, and anything not needed to render the comparison.

## Eleven underlying records plus one simulated failure mode

| Case id | Role | Provenance | Pinned record | Why chosen |
|---|---|---|---|---|
| EC-01 | Primary demo | Real, cached | NPI 1881622751, pair `c38178f2`, Paducah KY. Humana 1532 Lone Oak Rd Ste 305; NPPES and Care Compare 2407 New Holt Rd. NPPES 2025-08-13. Attached to a named 2026 plan through this location: yes, representative `H0473-003-000-2026`. No phone conflict. The practitioner's second pair is a clean match. | Clean, recent consensus conflict with one disagreement |
| EC-02 | Backup demo | Real, cached | NPI 1013274034, pair `8ed4f25a`, Toms River NJ. Humana 2360 Route 9; external 2360 Lakewood Rd (Care Compare adds Suite D01). NPPES 2024-11-11. Attached: yes, representative `H0473-003-000-2026`. Single pair. | Same street number, different street name; plausible alias; shows why the product must not declare error |
| EC-03 | Third real case | Real, cached | NPI 1952479701, pair `0a78467c`, Galveston TX. Humana 6710 Stewart Rd Ste 100; NPPES lists 2401 FM 646 Rd W Ste C (Dickinson) and 301 University Blvd; Care Compare 301 University Blvd. NPPES 2026-03-11. Attached: yes, representative `H0028-029-000-2026`. Phone conflict. The other pair matches. | Recent multi-location pattern with a supporting phone signal; hardest consensus case |
| MS-01 | Multi-source ambiguity | Real, cached | NPI 1417120569, pair `dd431c92`, Atlanta GA. Humana 5665 Peachtree Dunwoody Rd Ste G10; NPPES 1505 Northside Blvd Ste 1300 (Cumming) and 250 Chastain Rd NW Ste 210 (Kennesaw); Care Compare 1505 Northside Forsyth Dr Suite 1300. B2 family classification conflict on the role. Phone conflict. Attached: yes, representative `H0473-003-000-2026`. | Weakest evidence class with multiple supporting signals; the medium-versus-high effort comparison case |
| EC-STALE | Contrast, low urgency | Real, cached | NPI 1679969695, pair `d80e6a77`, Hallettsville TX. Humana 1406 vs external 1400 N Texana St. NPPES 2019-09-19. Attached: yes, representative `H0473-003-000-2026`. Phone conflict. | Stale consensus; Humana may hold the newer value; near-miss street number |
| MATCH-01 | Contrast | Real, cached | NPI 1295297430, pair `66db71a2`, Tucson AZ. Humana 3190 N Swan Rd; NPPES 3190 N Swan Rd (plus a second NPPES location on N Alvernon Way); Care Compare 3190 N Swan Rd. Single pair; label `address_match` only. Attached: yes, representative `H0028-021-000-2026`. NPPES not stale; non-virtual organization. | Exact full-key match on an attached, recent record; shows what never enters the queue |
| FMT-01 | Contrast | Real, cached | NPI 1659782829, pair `b1594e6d`, Nampa ID. Humana 215 E Hawaii Ave; NPPES 215 E Hawaii Ave # 140 (plus a Boise location); Care Compare lists Boise locations only. Single pair; label `fmt_address` only. NPPES not stale. Attached to a named 2026 plan through this location: yes, representative `H0473-003-000-2026` (verified against the complete cached InsurancePlan index; see definitions below). | Unit-only difference suppressed by base-key normalization; textbook format-only case |
| UNM-01 | Missing-source abstention | Real, cached | NPI 1790278653, pair `4e944abe`. Consensus conflict present, but the Organization returned 410 Gone, so the telehealth rule is unmeasured and the pair is not B1-evaluable. Attached: yes, representative `H0473-003-000-2026`. The other pair matches. | Deterministic abstention: conflict present but not evaluable |
| SS-01 | Single-source | Real, cached | NPI 1770601353, pair `77293b84`. Care Compare NOT_FOUND; NPPES stale. Attached: yes, representative `H0028-035-000-2026`. | Single-source disagreement, not evaluable; shown with its limitation |
| SYN-A2 | Synthetic registry signal | Synthetic | `npi: null`, `syntheticId: "SYN-A2-DEACTIVATED"`, displayed "Synthetic NPI — not a real provider". NPPES status deactivated. Address fields fabricated and labeled. | Lane A A2 signal shown as an urgent deterministic flag; excluded from figures |
| SYN-A3 | Synthetic registry signal | Synthetic | `npi: null`, `syntheticId: "SYN-A3-LEIE-MATCH"`, same display. LEIE exact match. | Lane A A3 signal; recommendation-with-registry-citation boundary; excluded from figures |
| FAIL-01 | Simulated failure mode | Mocked behavior on EC-03 (not a twelfth record) | `simulateAiFailure: "timeout"` flag applied to EC-03's record under a separate case id. | Demonstrates failure and recovery states reliably |

## Synthetic identifiers

Synthetic identifiers are non-numeric, cannot pass NPI Luhn validation, and the schema permits `npi: null` plus `syntheticId` only when `provenance === "synthetic"`; real cases require a ten-digit NPI. Synthetic rows are visually segregated in the queue, counted separately, and excluded from every metric and evaluation run.

## Plan attachment: definitions and traced calculations

Two different numbers appeared during planning. Both are traced here; neither is displayed as "plans the practitioner participates in."

- **Truncated per-role count (discarded).** `results_v3_1.json` stores on each pair a `plans` set that is the union, over the pair's roles and networks, of `sorted(idx["ma_nets"][network])[:6]`: only the alphabetically first six plan identifiers per MA network, all plan years mixed (2021 entries sort first). Any per-case count taken from that field is a storage artifact and is not used anywhere in the prototype.
- **2026 package reference count (internal only).** Computed from all 281 cached InsurancePlan pages: for every InsurancePlan resource whose `network[]` references an MA network that any PractitionerRole at the pair references, take `identifier.value` (Humana PlanId glossary, format contract-plan-segment-year, for example `H0473-003-000-2026`) and count distinct values ending in `-2026`. Results: EC-01 441, EC-02 440, EC-03 460, MS-01 443, EC-STALE 435, MATCH-01 443, FMT-01 439, UNM-01 440, SS-01 484. This counts distinct 2026 plan benefit packages that reference the pair's national networks. It is a network-level directory fact, not participation, and it is never displayed as "attached to N plans."

Definitions used in the prototype and the fixture manifest:

- **Attachment** is a directory-data relationship only: PractitionerRole at the pair → network Organization reference → at least one InsurancePlan resource for plan year 2026 that references that network. It never implies confirmed provider participation in any plan.
- `attachedCurrentYear: boolean` per pair, from the relationship above.
- `representativePlanId: string | null`: one consistently selected identifier, the lexicographically smallest 2026 PlanId among those referencing the pair's networks, used everywhere the pair is shown, with the adjudication's bounded wording "attached through the relevant location to a named 2026 plan."
- `planReferenceCount2026: number`: kept in the manifest as an internal, separately labeled field ("2026 plan benefit packages referencing the pair's networks; not participation"); not shown in the queue or case header.

Representative identifiers fixed now: EC-01 `H0473-003-000-2026`; EC-02 `H0473-003-000-2026`; EC-03 `H0028-029-000-2026`; MS-01 `H0473-003-000-2026`; EC-STALE `H0473-003-000-2026`; MATCH-01 `H0028-021-000-2026`; FMT-01 `H0473-003-000-2026`; UNM-01 `H0473-003-000-2026`; SS-01 `H0028-035-000-2026`. The build script copies these into the manifest and never derives or upgrades attachment from the truncated per-role field.

## Build process

`scripts/build-fixtures.py` (Phase 2) reads the read-only copies under `reference/empirical/`, extracts the pinned cases by NPI and Location id, strips names, records retrieval dates from cache metadata and the run log, and writes `src/data/fixtures/cases.json` and `src/data/fixtures/manifest.json`. Every case carries a provenance badge (Real cached, Real live, Mocked, Synthetic) and every brief carries a Live or Cached label. The queue header counts real cases separately from synthetic ones.

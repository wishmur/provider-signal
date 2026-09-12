# Service design assumptions (C2): current state and future state

Evidence tiers used throughout:

- **[Industry]** payer-industry evidence.
- **[Humana]** Humana-specific public evidence.
- **[Assumption]** unverified working premise, with its basis stated.
- **[Validate]** question to put to a Humana operator.

We hold no verified evidence of Humana's exact internal provider-data workflow. No inferred Humana process below is presented as observed fact.

## Evidence available

- [Industry] Consolidated research §10.3 simplified journey: recruit/contract → credential → create record → distribute across claims, directory, care management, and member systems → receive updates → re-verify → remove or correct stale records. §10.4: a bad record propagates to member misdirection, claim pricing, authorization routing, adequacy calculation, calls, grievances, compliance. §10.1: a master-data problem, not a directory-only problem.
- [Industry] §10.5: REAL Health Providers Act obligations from 2028 (verification, removal, standardization, audit, reporting); Provider Directory API already required. The adjudication adds the statutory citation (Pub. L. 119-75 §6220) and 42 CFR 422.111(m), in force since 2026-01-01.
- [Industry] §10.6: this area needs entity resolution more than generation; useful patterns include detecting stale entries, prioritizing records for human verification, and explaining why a record is suspect.
- [Industry, not in R, re-verify against the CMS PDF before any Phase 3 deliverable] CMS Online Provider Directory Review Report, Round 3 (November 2018): inaccuracies concentrated where group practices listed providers at every group location, and organizations lacked internal audit processes to detect such errors. Cited through the superseded decision document (which records the review method as scripted phone calls) and the LLM3 handoff. This finding is not in the consolidated research corpus; its evidence status is not upgraded until the primary source is re-read.
- [Humana] Veda partnership announced 2024-02-26 to analyze, verify, and standardize phone, address, and panel status (press release, cited in the decision document). Consequence: Humana has vendor verification; the product targets what remains after it.
- [Humana] Star Tribune, 2024-11-01: five Minnesota health systems listed in-network for 2025 after announced withdrawal; one system said it asked Humana in early October to fix it (decision document). Class: network-participation propagation, out of this prototype's scope; evidence that exceptions survive vendor verification and that corrections have latency.
- [Humana] The public Plan-Net FHIR directory already carries 2027 network assignments before 2027 InsurancePlan resources are published (probe finding). A data-model insight: the directory is fed ahead of plan publication. Not an error.
- [Humana] §10.7: Humana's directory-accuracy rate and provider-data stack are not public.

## Current state (assumed)

### Actors

| Actor | Tier | Basis |
|---|---|---|
| Provider-data operations specialist (exception worker) | Assumption | Consolidated research §10; adjudication's primary user |
| Provider relations / outreach staff | Assumption | Industry norm; the CMS 2018 review used phone verification (industry evidence outside R, pending primary-source re-verification) |
| Contracting / network management | Assumption | Star Tribune case concerned contract status |
| Credentialing | Assumption | §10.2 credentialing definition |
| Verification vendor (Veda) | Humana (engagement); Assumption (feed scope) | Press release |
| Provider office staff | Assumption | Someone answers outreach |
| Downstream consumers: member services, claims, care navigation, compliance | Industry | §10.4 |

### Systems

| System | Tier | Basis |
|---|---|---|
| Provider master-data platform | Assumption | §10.1 master-data framing |
| Directory publication: Plan-Net FHIR API and public finder | Humana | Observed endpoints |
| Vendor verification feed | Humana (engagement); Assumption (integration) | Press release |
| Outreach channels: phone, fax, email, portal attestation | Assumption | Industry norm |
| Work queue or ticketing | Assumption | Industry norm |
| Regulatory reporting | Industry | Statute |

### Trigger

Vendor score change or flag; provider roster or attestation update; member or provider complaint; CMS or regulatory review; periodic re-verification cycle. [Assumption; basis: §10.3 "receive ongoing updates", CMS 2018 review method]

### Handoffs and manual evidence gathering [Assumption unless noted]

1. A flag arrives in the queue carrying one field disagreement and little context.
2. The specialist opens the master record, then separately looks up NPPES, Care Compare or PECOS, and sometimes a practice website, transcribing values into notes. Basis: the sources are public and separate; no public evidence of an integrated view.
3. The specialist decides whether outreach is needed, drafts a message or call script by hand, and routes it to outreach.
4. The outreach outcome returns days later; the specialist updates the master record; the change reaches publication on its own cadence. Basis: the Star Tribune case shows weeks of latency.
5. Contract-status questions route to contracting; credential questions route to credentialing.

### Rework and exception paths

- The same practitioner re-flagged at multiple locations because group-level location lists propagate. [Industry, CMS 2018]
- Multi-location practitioners flagged repeatedly when each database lists a different subset of real locations. [Probe: the multi-source class is 46 of the 77 conflicted practitioners]
- Stale external records (199 of 250 sampled practitioners had NPPES records older than 24 months) produce flags where Humana may hold the newer value. [Probe]
- Unreachable provider offices; no response to attestation. [Assumption]
- Vendor-verified fields still disagreeing with public registries. [Inference from the probe]

### Escalations

Contracting for participation status; compliance for statutory removal duties; management for aged exceptions. [Assumption]

### Downstream consequences

Member misdirection, claims pricing, authorization routing, adequacy calculation, grievances, statutory accuracy exposure. [Industry, §10.4; statute]

### Likely sources of time and friction [Assumption unless noted]

- Multi-system lookup and manual transcription.
- Judging whether a disagreement is meaningful (formatting, alias, multi-location) without normalization help.
- Drafting outreach from scratch.
- No record of which evidence was seen when a decision was made. [Industry, outside R, pending primary-source re-verification: the CMS 2018 review noted missing internal audit processes]
- Waiting on outreach; re-flagging of the same case.

## Questions to validate with a Humana operator [Validate]

1. What creates an exception today (vendor score threshold, complaint, cycle), and at what monthly volume?
2. Which systems are open during a review, and is any external lookup integrated?
3. Median handling time per exception; share needing outreach; outreach response rate and latency.
4. Who can change a directory field, and what approval or propagation steps follow?
5. How are multi-location practitioners modeled; is a location-level attestation available?
6. What does the Veda feed cover, and which field classes fall out to manual work?
7. Is there an audit record of evidence reviewed per decision?

## Future state with the product

Unchanged: triggers, actors, downstream systems, and human authority over every field.

Changed, in order along the workflow:

1. The deterministic layer classifies the pair before a human sees it. Match and format-only pairs never enter the queue; single-source and unmeasured pairs are shown with their limitation.
2. All four sources are assembled in one comparison view with dates and provenance; no transcription.
3. The evidence brief explains the disagreement, contrary evidence, missing evidence, verification urgency with reasons, and a draft that asks the provider to confirm.
4. The specialist verifies, requests outreach, escalates, defers, or records no action, always with a rationale; disagreement with the brief is captured.
5. The action is a proposal queued to downstream systems (mocked in the prototype); the master-data change and directory publication remain on their existing human-controlled path.
6. Every decision records the evidence shown, model and prompt versions, and the human's rationale.
7. When the model is unavailable, invalid, or abstains, the specialist works from the deterministic view; the queue and audit log function without the model. This is the rollback state.

Where uncertainty is handled: abstention is a queue state; missing sources are explicit rows; the brief never marks a value likely-correct; urgency drivers are shown so the specialist can disagree with the ranking.

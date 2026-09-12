# UX shape (provisional)

Status: drafted manually from the adjudication; to be confirmed by `/impeccable shape` after installation. Primary user: provider-data operations specialist. Impeccable mode: Operate.

## Screen map

| # | Surface | User objective | Information required | Main action | Decision produced | Error and uncertainty states | Downstream |
|---|---|---|---|---|---|---|---|
| 1 | Exception queue (`/queue`) | Pick the next pair worth verifying | Case id, NPI (or synthetic label), specialty, Humana-listed location, evidence class, current-year attachment (yes/no) with the representative 2026 plan identifier, external recency (NPPES last_updated; Care Compare dataset date), flags (phone, stale, telehealth-uncertain, Lane A), provenance badge, queue state (new, brief ready, abstained, actioned), AI urgency if a brief exists | Open a case; sort or filter by class, flag, state | Which case to investigate now | Empty queue; fixture load failure; AI urgency absent (rules-only ordering, labeled); synthetic rows segregated | Case detail |
| 2 | Case detail: evidence comparison (`/cases/$caseId`) | Understand exactly what disagrees | Side-by-side rows per source: address, phone, taxonomy, telehealth, status; normalized keys; match/differs markers; source, retrieval date, source update date or "no per-record date"; plan attachment (current-year flag, representative plan identifier, network references, labeled as a directory relationship, not participation); deterministic classification with rule names | Request evidence brief; jump to action | None yet | Missing source rendered as an explicit "not available" row with reason (GONE, NOT_FOUND, REQUEST_FAILED); single-source pairs marked not B1-evaluable | Brief panel |
| 3 | AI evidence brief (brief panel) | Get a cited explanation and a proposed next step | Brief per schema; each citation resolves to a source row and date with the server-retrieved value; model id, prompt version, schema version, latency, live or cached label | Accept into working view; regenerate; view cached | Which verification step to take (still human) | Loading; live failure → deterministic view kept, cached brief offered with label; invalid output → rejection notice; abstention → reason and unblocking evidence; refusal stop reason → as failure; AI disabled → cached only | Action panel |
| 4 | Human action (action panel) | Record what the specialist decides | Options: request provider outreach (editable draft), escalate to contracting, mark reviewed with no action, defer pending evidence; required rationale; disagreement-with-brief checkbox | Confirm (dialog restates: proposal only, no directory change) | The human decision and rationale | Confirm without rationale blocked; action without a brief allowed and labeled rules-only | Audit event; queue state; mocked "proposal queued" notice |
| 5 | Audit history (`/audit` and per-case timeline) | See what was shown and what was done | Events: case opened; brief requested (model, prompt, schema versions, evidence hash, outcome); rejected or abstained; action recorded (type, rationale, draft hash, override flag); data reset | Filter by case; export JSON (mocked); reset prototype data | None | Empty history; storage unavailable (in-memory fallback, labeled) | Terminal |
| 6 | Uncertainty or failure state (panel within 3; queue state) | Keep working when the AI cannot help | Failure kind (unavailable, invalid, rejected, abstained, refused, disabled), reason, retry, cached availability, attempt count | Retry; load cached; proceed rules-only | Whether to proceed without the brief | Retry fails again → remains in failure with count | Action panel available |

## Vertical flow

Queue → open case → read comparison → request brief → read brief, or failure or abstention → choose action and rationale → confirm → audit event → back to queue with updated state.

## Keyboard

`j` and `k` move between queue rows; `Enter` opens; `b` requests a brief; `a` focuses the action panel; `Esc` closes dialogs. Every interactive element shows a visible focus ring.

## Visual target

Credible internal provider-operations tool: dense but readable evidence tables, restrained color, meaningful status semantics, accessible contrast, keyboard-friendly navigation, clear focus states, efficient comparison views, visible "Concept Prototype" label. Out of scope: delight, animate, overdrive, bolder, colorize; chat-first interaction; decorative AI imagery; purple-to-blue gradients; cards nested in cards; gratuitous dashboards or charts; effects that compete with evidence review.

## Pending

`/impeccable init` and `/impeccable shape` for exception queue, case detail, evidence brief, human-decision surface, and audit history. Their outputs supersede this document's layout guidance; they do not change the locked claim, evidence, workflow, or product boundary.

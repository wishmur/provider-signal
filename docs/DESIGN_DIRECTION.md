# Design direction, tokens, and component inventory

Status: selected through `/impeccable shape` on 2026-09-12. Direction round: `impeccable concept-seed --scope direction --mode operate`, seed key `5c0fb3e7`, assigned index 7 of the seven grounded candidates, six catalog challengers dealt and all declined after fusion. The product owner chose the assigned card. Build path: code-led (this harness has no image generation, so no comp round exists). Telemetry ping sent as the tool documents (card kind only).

What this document is: the durable direction and the proposed token and component system for Phase 2. What it is not: `DESIGN.md`. Impeccable writes `DESIGN.md` and `.impeccable/design.json` at Phase 2 finish from the built artifact; a rulebook written before the build would be defended against reality instead of describing it. The direction contract below is written into the Impeccable surface brief (`.impeccable/surfaces/`) by the new-work flow at Phase 2 build start, not by shape.

## The world: Public Registry Record

Lineage: the CMS public registry pages the specialist reads every day (NPPES NPI Registry, Care Compare) and the eCFR reading page where the governing rule (42 CFR 422.111(m)) lives. Public references and what was taken from each are recorded in `docs/DESIGN_REFERENCES.md`.

Thesis: every value on screen is a dated public record with its registry named, laid out the way the registries lay it out. The surface refuses the two category defaults: the SaaS admin dashboard (sidebar, KPI tiles, table inside a rounded card) and the dark operator console.

Raised by the declined hand (each line names its donor; the donor's clothes were not taken):

1. Selection commitment (racing league): the open case owns one full-width selection field shared by its queue row and its right rail; no half-tints.
2. Zone plates (starship terminal): every panel carries a stamped provenance plate (REAL, CACHED, MOCKED, SYNTHETIC, LIVE) in the same corner, so no region is unlabeled.
3. Keyed addressing (teletext): every case has a short typeable id and the queue is fully keyboard-routed.
4. Character-aligned data (datamatics): NPIs, dates, plan ids, and normalized address keys are set in tabular monospace so a differing character lines up under its counterpart.
5. Texture as state (industrial quote grammar): non-evaluable, abstained, and synthetic rows carry a hatch pattern in addition to color, so no state depends on color alone.
6. Pinned observations (deep dive): every brief claim carries its source and date inline; audit history runs on one ruled time axis with each event pinned to its timestamp.

Honest risk: reads as a government data page unless alignment, spacing, and state semantics carry the craft. The build must earn its finish through rhythm and precision, not decoration.

Alternates recorded for the log, not adopted: Audit Workpaper (my own top-ranked grounded candidate; declined by the owner in favor of the roll); the category standard (standing exit; not taken); the six catalog challengers (declined on both axes, kept lines above).

## Direction contract (draft; persisted by new-work at Phase 2 build start)

THESIS: Every value on screen is a dated public record with its registry named. The surface refuses the sidebar-and-KPI admin dashboard and the dark console alike; it is a ruled register.

OWN-WORLD: White ground, cool gray panels, near-black ink, one darkened Humana-family green for action and selection, one-pixel rules, 2px corners, uppercase stamped provenance plates, tabular monospace for every identifier, key, and date, hatch texture for non-evaluable states. With all content removed it is still recognizable: a ruled register with plates in its corners and one green selection field.

STORY: The specialist sees which pair to verify next, what disagrees and since when, what the model can and cannot say, records the decision, and sees it in the log. They are never told what is true.

FIRST VIEWPORT: The queue at 1440×900. Top bar 48px (name, Concept Prototype plate, Queue, Audit, AI mode, Legend). Register header 40px (frame, plan year, snapshot date, ordering, counts). A fixed-column table fills the width with roughly fourteen 32px rows visible; the nine real rows, then the hatched synthetic section. The primary action is opening a row (Enter or click). No side rail on the queue.

FORM: Public Registry Record, candidate 7 of 7 on the ordered grounded list; seed key `5c0fb3e7`; the assigned card; code-led. Signature interaction: citation-to-cell highlighting and the character-aligned key diff. Motion grammar: state-only transitions at 150 to 200ms; no entrance choreography.

FINISH: unreviewed and undocumented is unfinished; this build ends with the finish review, the verdict, DESIGN.md, and every shipping raster carrying its provenance.

## Color strategy and tokens

Strategy: Restrained (neutrals plus one accent), the Operate floor. Scene: an office desk, large monitor, daytime lighting, hours at a time; the answer is a light surface. Dark theme is out of scope for the prototype; the scaffold's inert `.dark` block is a Phase 2 cleanup decision.

Semantic tokens (light). Contrast ratios computed against WCAG 2.x relative luminance; AA text is 4.5:1, AA non-text (graphical objects, focus indicators, state-bearing strokes) is 3:1.

| Token | Value | Role | Verified pairs |
|---|---|---|---|
| `--ground` | `#FFFFFF` | page ground, table cells | ink 17.2; muted 5.5; accent 6.2; focus 8.4 |
| `--panel` | `#F1F3F5` | second neutral: rail, headers, plates | ink 15.5; muted 4.9; focus 7.6; hatch stroke 4.9 |
| `--ink` | `#1B1B1B` | primary text | on every tint 14.7 or better |
| `--ink-muted` | `#5B6B7A` | secondary text, captions, hatch stroke | on ground 5.5; panel 4.9; selection tint 4.8 |
| `--rule` | `#DFE1E2` | decorative separators only, never state-bearing | not required to meet 3:1 |
| `--rule-strong` | `#A9AEB1` | table header underline, decorative | not required to meet 3:1 |
| `--accent` | `#1F6F3F` | primary action, links, selected state, LIVE plate text | text on ground 6.2; white on accent 6.2; on selection tint 5.4 |
| `--accent-tint` | `#E6F2EA` | selection field, ok tint | ink 15.0 |
| `--focus` | `#1C4F82` | 2px focus ring, 2px offset | on ground 8.4; on panel 7.6 |
| `--warn` / `--warn-tint` | `#7A4B00` / `#FFF4D6` | stale, phone, telehealth-uncertain, MOCKED plate | text on tint 6.8; on ground 7.4 |
| `--danger` / `--danger-tint` | `#A3261C` / `#FBE9E7` | registry signal (Lane A), failure kinds, validation errors | text on tint 6.3; on ground 7.4; white on danger 7.4 |
| `--info` / `--info-tint` | `#1C4F82` / `#E8F0F8` | AI-mode Live indicator, informational banners | text on tint 7.3; on ground 8.4 |
| `--ok` / `--ok-tint` | same as accent / accent tint | matches marker | as accent |

The accent is a darkened green in the family of Humana's public-site green. The public site's own primary green (observed `#5C9A1B`) measures about 3.2:1 as text on white and is therefore not used for text or buttons; see `docs/DESIGN_REFERENCES.md`.

Hatch: 1px strokes of `--ink-muted` at 45 degrees every 8px over the region's own fill. It is always paired with a text label; the stroke itself meets 3:1 on ground, panel, and selection tint.

Status semantics (fixed vocabulary; text always accompanies the mark):

- Evidence class: neutral outline chip with the class name; no color coding by class.
- Registry signal (deactivated NPI, LEIE match): danger plate, white on `--danger`, icon plus "Registry signal".
- Stale, phone conflict, telehealth-uncertain: warn tint chip with text.
- Matches: ok tint chip "matches". Differs: neutral chip "differs". Format-only: neutral chip "format-only".
- Not available, unmeasured, abstained, synthetic: hatch plus text.
- Provenance plates: REAL (outline, ink), CACHED (panel fill), MOCKED (warn tint), SYNTHETIC (hatch), LIVE (accent tint, accent text). Uppercase, 11px, 0.04em tracking, 2px corners, same corner of every panel.
- Interactive states on every control: default, hover, focus, active, disabled, loading, error. Disabled is reduced ink, never a saturated accent.

## Typography

- One family for the interface: the system stack `system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif`. Humana's proprietary face is not used.
- One family for data: `ui-monospace, "SF Mono", Menlo, Consolas, "Liberation Mono", monospace` with `font-variant-numeric: tabular-nums`, used for case ids, NPIs, plan identifiers, dates, hashes, normalized keys, and citation refs.
- Fixed rem scale, base 14px, ratio about 1.125: 11 (plates, meta), 12 (captions, table meta), 13 (table cells), 14 (body), 16 (panel titles), 18 (section headings), 20 (page title, case header). Weights 400 and 600 only. Line height 1.35 for data and tables, 1.5 for prose. Brief prose measure at most 70ch.
- Headings carry more space above than below. No display faces, no fluid clamp sizes.

## Spacing, shape, and density

- 4px base; scale 4, 8, 12, 16, 24, 32. Table cell padding 6px 10px; row height 32px (meets the 24px minimum target size). Buttons 32px tall, 12px horizontal padding.
- Corners: 2px on plates, chips, buttons, inputs; 4px on popovers and dialogs. No pills, no large radii.
- Borders: 1px `--rule` separators; panel regions are rule-bounded areas on ground or panel neutral, never cards inside cards. Elevation: one subtle shadow token for popovers and dialogs only.
- Density: desktop-first at 1280 to 1600px. Right rail 380px at 1280px and wider; stacks below at 1024 to 1279px. The queue and comparison tables scroll horizontally inside their own containers below their minimum column widths; the page never scrolls horizontally.

## Motion and focus

- 150ms ease-out for hover, focus, selection, and disclosure; 200ms for panel content swaps. Motion conveys state only. No entrance choreography, no page-load sequences. `prefers-reduced-motion` removes transitions entirely.
- Loading is skeleton rows and blocks in place, never a spinner in the middle of content.
- Focus: 2px solid `--focus` ring with 2px offset on every interactive element, inset on table rows; never removed. Overlays render in portals so they escape scrolling containers.

## Iconography

`lucide-react` (already installed), 16px, 1.75 stroke, always paired with a text label. Icon-only controls are not used except with an `aria-label` and a visible tooltip, and none are planned.

## Component inventory

Existing shadcn primitives in `src/components/ui/` that Phase 2 uses: `button`, `badge` (extended with plate and hatch variants), `table`, `dialog`, `alert-dialog`, `popover`, `tooltip`, `textarea`, `input`, `checkbox`, `radio-group`, `label`, `select`, `separator`, `scroll-area`, `skeleton`, `alert`, `collapsible`, `sonner`. The remaining primitives in the scaffold stay untouched in Phase 2; pruning them is a deliberate later decision, not a side effect.

Product components to build (one responsibility each; every interactive one ships default, hover, focus, active, disabled, loading, and error states):

| Component | Responsibility | Surface |
|---|---|---|
| `AppShell`, `TopBar` | Shell chrome: name, Concept Prototype plate, Queue and Audit navigation, AI-mode indicator, legend trigger | shell |
| `ConceptPrototypePlate` | The visible unofficial label | shell |
| `AiModeIndicator` | Live / Cached / Off with reason on disclosure | shell |
| `ProvenanceLegend` | Popover defining Real, Cached, Mocked, Synthetic | shell |
| `ProvenancePlate` | REAL, CACHED, MOCKED, SYNTHETIC, LIVE plate | all |
| `StatePlate` | Hatched plate for not available, unmeasured, abstained | 1, 2, 3, 6 |
| `RegisterHeader` | Frame, plan year, snapshot date, ordering, counts | 1 |
| `QueueTable`, `QueueRow` | Fixed-column register with keyboard routing and selection field | 1 |
| `SortControl`, `FilterBar` | Explicit sort with rules-only reset; filters by class, flag, state | 1 |
| `UrgencyCell`, `DriversDisclosure` | AI urgency level with its stated drivers | 1 |
| `SyntheticSection` | Always-visible, hatched, "not counted" section | 1 |
| `CaseHeader`, `PlanAttachmentLine` | Case identity and the bounded attachment wording | 2 |
| `EvidenceComparisonTable`, `SourceColumnHeader`, `EvidenceCell` | Sources as columns, fields as rows, stacked sub-cells, comparison markers | 2 |
| `KeyDiff` | Character-aligned normalized keys with weight-and-underline emphasis | 2 |
| `NotAvailableColumn` | Whole-column plate with reason code | 2 |
| `ClassificationPanel` | Class, rule names, B1-evaluable, telehealth rule, known unknowns, constraints | 2 |
| `BriefPanel`, `BriefSection`, `CitationChip`, `HypothesisItem`, `UrgencyBlock`, `DraftPreview` | Schema-ordered brief with citation-to-cell highlighting | 3 |
| `ActionPanel`, `ActionTypeRadio`, `DraftEditor`, `RationaleField`, `DisagreeCheckbox`, `ConfirmProposalDialog` | Human decision with required rationale and proposal-only confirmation | 4 |
| `AuditTimeline`, `AuditEvent`, `AuditFilters`, `ResetDataDialog`, `ExportNotice` | Ruled time axis, filters, mocked export, reset | 5 |
| `FailurePanel` | Kind plate, reason, attempt count, Retry, Load cached, Proceed rules-only | 6 |
| `EmptyState`, `ErrorState`, `SkeletonRows` | Shared loading, empty, and error treatments | all |
| `KeyboardHint` | Discoverable key map | shell |

## Anti-goals carried into the build

No chat-first interaction; no decorative AI imagery; no gradients; no cards nested in cards; no KPI tiles or charts; no entrance animation; no pills; no icon-only controls; no marker that reads as correct or wrong on a value; no sort that hides the rules-only order; no figure or statistic anywhere in the UI; no Humana mark or logo.

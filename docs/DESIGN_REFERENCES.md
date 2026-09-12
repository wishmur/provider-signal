# Design references

Rule: only public surfaces inform this design. We hold no access to Humana's internal design system and make no claim to one. The result is Humana-inspired and unofficial; the "Concept Prototype" plate is visible on every surface, and no Humana mark or logo appears. Naming Humana as the public-directory data source is correct and expected.

## What was observed (2026-09-12, in-app browser, computed styles on the live pages)

Values are what the pages served that day; they can change and are recorded as observations, not as brand specifications.

| Public surface | Observed characteristics |
|---|---|
| humana.com (home) | White ground; body text `#3A3B3D`; a proprietary typeface stack ("FS Humana", Calibri, Helvetica, Arial); primary green `#5C9A1B` on buttons and marks; dark green `#114A21`; teal `#007481` on links and icons; light gray surfaces `#EFEFF1` and `#F8F8F8`; pill-shaped buttons; a leaf motif; consumer hero photography. |
| npiregistry.cms.hhs.gov (NPPES NPI Registry) | White ground; body `#212529`; Roboto / Helvetica Neue; a navy header bar; Bootstrap-style form controls with 6px corners; bold field labels; an "Effective" date notice at the top; the NPI as the key of every record; per-record "last updated" dates in results. |
| medicare.gov/care-compare | U.S. Web Design System classes; Rubik typeface stack; body `#404040` and ink `#323A45`; primary teal-green `#146A5D`; corner radii of 0 and 3px; the official-government banner; plain sectioning with a provider-type select; the dataset carries no per-record update date. |
| ecfr.gov (42 CFR 422.111) | White ground; text `#333333`; Roboto; a point-in-time line ("Displaying title 42, up to date as of 9/10/2026. Title 42 was last amended 8/13/2026"); a breadcrumb hierarchy Title, Chapter, Subchapter, Part, Subpart, section; editorial-note plates; section-number-led headings; a left tool rail (Table of Contents, Details, Display options); a "view historical versions" affordance. |

## What the design takes from each, and what it refuses

From Humana's public site:

- Taken: a green accent in the same family, darkened to `#1F6F3F` so text and buttons pass WCAG AA (the observed `#5C9A1B` measures about 3.2:1 as text on white and is not used for text or buttons); a white ground with dark gray text; overall restraint away from the hero.
- Refused: the proprietary typeface (not licensed); pill buttons, the leaf motif, teal, and hero photography (consumer-site devices); any logo or mark.

From the NPPES NPI Registry:

- Taken: the record-page idea of labeled fields with their dates; the NPI leading every row; plain, familiar form controls.
- Refused: the navy header and Bootstrap chrome.

From Care Compare:

- Taken: small corner radii in the 2 to 4px range; the practice of labeling a dataset date when no per-record date exists (Care Compare's dataset date 2026-08-18 is shown as such, never as a record date); the official banner, inverted honestly into the "Concept Prototype" plate that says the opposite.
- Refused: Rubik; the teal primary.

From the eCFR reading page:

- Taken: the point-in-time "as of" line, which becomes the register header's snapshot retrieval date; the breadcrumb lineage, which becomes the case header's chain (case, NPI, location, class); editorial-note plates, which become provenance and state plates; section-number-led headings, which become typeable case ids leading each row; the historical-versions affordance, which becomes the audit history's ruled time axis.
- Refused: the crowded top toolbar; Roboto.

## Original choices (not derived from any reference)

- The exact token values in `docs/DESIGN_DIRECTION.md`, including the second neutral `#F1F3F5`, the focus ring `#1C4F82`, and the semantic tints.
- Tabular monospace for every identifier, key, and date, with the character-aligned normalized-key diff.
- Hatch texture as a state carrier for not available, unmeasured, abstained, and synthetic, so no state depends on color alone.
- Citation-to-cell highlighting between the brief and the comparison table.
- The full-width selection field shared by the queue row and the right rail.
- The register header, the always-visible synthetic section, the six-surface topology, and the three-route structure.
- The system typeface stack for the interface; none of the reference faces are adopted.

## Provenance of the direction itself

The visual world was chosen through Impeccable's direction round (seed key `5c0fb3e7`), which dealt six catalog challengers from impeccable.style; all six were declined on audience identification and product clarity, and one discipline was kept from each as a named raise. Those raises are listed in `docs/DESIGN_DIRECTION.md`. The catalog challengers are not references for this design; their kept lines are.

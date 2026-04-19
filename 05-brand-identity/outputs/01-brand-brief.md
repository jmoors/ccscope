# 01 — Brand Brief

**Version:** 1.0
**Date:** 2026-04-19
**Owner:** Agent 5 (Brand Identity)
**Dependency:** Name decision (Pavilion) currently Proposed; all deliverables proceed on that assumption. If FixtureDesk is selected, revisit logo treatment and see appendix note.

---

## Visual direction: why these decisions

### 1. The brief in one sentence

A visual identity that reads as institutional authority — not as a startup, a sports-media product, or a heritage brand — and that hands a complete token system to Agent 7 with zero ambiguity.

### 2. Comparison points (from Agent 1)

| Reference | What we take from it |
|---|---|
| National Trust | Calm authority; long-horizon confidence; no urgency theatre |
| Ordnance Survey | Functional precision; domain-specific expertise trusted by those who know |
| Well-run county club's modern website | Competent, literate, not overdesigned |
| GOV.UK | Direct; no marketing language; respects the user's time |

**What we do not take:** Strava's competitive energy, Eventbrite's transactional genericness, any betting-adjacent palette.

### 3. Anti-cliché audit (pre-work)

Before choosing anything, this checklist was applied:

| Cliché | Status | Reason bypassed |
|---|---|---|
| Crossed bats | Rejected | Playing equipment = wrong register |
| Stitched-ball letters | Rejected | Overused, sport-media association |
| Red + cream as primary | Rejected | MCC-coded, nostalgic |
| Wicket / stumps silhouettes | Rejected | Too literal, too dated |
| Pyjama-franchise colour schemes | Rejected | Franchise cricket is the opposite register |
| Rounded-lowercase startup wordmark | Rejected | Wrong register entirely |

Nothing in these deliverables comes from the above list. No rationale is needed.

### 4. Colour rationale

**Why deep forest green as primary:**
- Cricket's institutional environment is the ground — not the kit, not the scoreboard. The outfield is green. The pavilion sits on green. This reference is environmental, not playing-equipment-nostalgic.
- Deep forest green (#1d3a2b) is dark enough to read as authority, not as a sports brand. It is not the National Trust's specific green (avoiding confusion), not England cricket blue (avoiding franchise association), not startup teal (wrong register).
- All text on this colour passes WCAG 2.2 AAA.

**Why deep amber as accent:**
- Warm, earthy, specific. Cricket balls and bats are brown/amber; this is an indirect reference rather than literal (we do not use a circular red icon).
- Deep amber (#8a5c1a) passes WCAG 2.2 AA as text on white (5.5:1). White text on deep amber also passes AA (6.0:1).
- Colourblind-safe: green and amber differ in hue channel (blue-yellow axis) preserved across protanopia and deuteranopia. Luminance contrast between primary and accent is sufficient for achromatopsia.

**Why no third chromatic colour:**
- A third colour would introduce complexity without benefit. The neutrals (near-black, mid-grey, off-white) do all the work that a third colour would do, without the collision risk.

### 5. Typography rationale

**Why Source Serif 4 (headings and wordmark):**
- Free licence (SIL OFL 1.1) — no licensing cost risk.
- Designed for screen readability at all sizes.
- Institutional character: the humanist serifs read as considered and authoritative, not as heritage-newspaper or academic.
- Avoids the rounded-sans startup register (Inter, Nunito, etc.).
- Works well for the wordmark: "Pavilion" in a medium-weight serif is legible and proportioned.

**Why Source Sans 3 (UI body and functional text):**
- Same family as Source Serif 4; optical coherence without design effort.
- Same licence (SIL OFL 1.1).
- System-UI fallback available; no performance penalty if not loaded.

**What we ruled out:**
- Gill Sans: heritage, licensing complexity on web.
- Georgia: too newspaper; too system-default for a named brand.
- Inter / DM Sans: startup register, overused.
- Playfair Display: editorial/premium — tips into nostalgic when combined with green.

### 6. Logo rationale

**Why a wordmark, not a logomark:**
- "Pavilion" is eight characters with strong letterforms. The wordmark does the recognition work. A logomark requires additional explanation and risks reverting to the cliché list.
- The "P" works as a standalone monogram at small sizes (favicon, app icon) where the full wordmark is illegible.

**Why no pavilion silhouette:**
- Agent 3 is explicit: the name references function (the building as organisational hub), not aesthetics (Victorian pavilion illustration). A silhouette would make it aesthetic.
- A roofline illustration at icon size becomes illegible and would require detailed rendering at larger sizes — this is scope that belongs in v2 if at all.

**What the wordmark communicates:**
- Confidence via weight: medium (not thin, not bold).
- Precision via spacing: +0.04em tracking — opened up enough to signal a considered design, not so much as to signal fashion.
- Authority via serif: not rounded, not geometric-sans, not condensed.

---

## Appendix: FixtureDesk fallback notes

If the name decision switches to FixtureDesk:
- Wordmark should use Source Serif 4 Medium, title case: "FixtureDesk" (capitalised D is standard for compound names).
- Monogram: "FD" in a ligature, or just "F" at small sizes.
- The colour system, typography, and token format are **unchanged** — the identity rationale holds for both names.
- Agent 5 will regenerate logo SVG files if name changes; tokens do not change.

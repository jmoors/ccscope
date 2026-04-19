# 04 — Logo Specification

**Version:** 1.0
**Date:** 2026-04-19
**Owner:** Agent 5 (Brand Identity)

---

## Files

| File | Use |
|------|-----|
| `05-logo-primary.svg` | Full wordmark — primary colour |
| `06-logo-monogram.svg` | P monogram — primary colour, app icon, favicons ≥ 48px |
| `07-favicon.svg` | Favicon-optimised mark — 32×32 reference |

**Production note:** All SVG text elements must be converted to paths before distribution. The source SVGs use referenced fonts for design-editing convenience; path-converted files are required for all production use to avoid font-loading dependency.

---

## Wordmark

### Construction

"Pavilion" set in Source Serif 4 Medium (weight 500), letter-spacing +0.04em, colour Forest `#1d3a2b`.

No bespoke letterform modifications. The typeface's natural forms are used without alteration. The even tracking opens the word to the right weight of whitespace for an institutional product — not condensed (brash), not extremely wide (fashion/luxury).

### Proportions

- Height of capital "P": reference unit (1x)
- Total word width: approximately 6.8x
- Clear space (all sides): minimum 1x (the height of the capital P)
- Minimum display size: 120px wide (at which legibility is maintained)

### Versions

| Version | When to use |
|---|---|
| Forest on white (`#1d3a2b` on `#ffffff`) | Primary. Default. |
| White on Forest (`#ffffff` on `#1d3a2b`) | Dark background applications |
| Forest on Parchment (`#1d3a2b` on `#f7f6f4`) | Card headers, warm-surface use |
| Ink on white (`#1a1a18` on `#ffffff`) | Print, where the primary green is impractical |
| Forest single-colour (no background) | Embossing, one-colour print |

**No amber wordmark.** The wordmark is Forest or monochrome. The accent colour is never used for the logotype.

### Monochrome operation (mandatory check)

The wordmark is designed monochrome-first. It works as:
- A single flat colour (Forest)
- Black on white (Ink version)
- White on dark backgrounds
- As a silhouette / reversed

No gradients, no effects, no drop shadows are ever applied.

---

## Monogram

The monogram is the "P" letterform from Source Serif 4 Medium, used as a standalone mark.

**Primary use:** App icons, favicons at 48px and above, profile avatars when the wordmark does not fit.

**Presentation options:**
1. "P" in Forest on white — for light context use
2. "P" in white on Forest square (corner radius 14% of width) — for app icon use

**Minimum size:** 24px (below this, the serif "P" becomes illegible; use a simplified geometric path instead if required at sub-24px sizes — flag to Agent 9 if needed).

---

## Favicon

**File:** `07-favicon.svg`

The favicon is the "P" monogram in white, on a Forest (`#1d3a2b`) rounded square. Corner radius is 6px at 32×32px reference size (scales proportionally).

**Production requirements:**
- `favicon.svg` (scalable, for modern browsers)
- `favicon-32x32.png` (fallback)
- `favicon-16x16.png` (legacy fallback)
- `apple-touch-icon.png` (180×180px — monogram on Forest background, no corner radius needed; iOS clips to circle)

**Note:** favicon.svg was designed first (as required) and then expanded to the wordmark. The monogram must work at 16×16 before the wordmark is finalised.

---

## Clear space

Clear space is the exclusion zone around the logo where no other visual element may appear.

- **Wordmark:** minimum 1× capital-P height on all sides
- **Monogram:** minimum 0.5× monogram height on all sides
- **Favicon:** inherent in container (no external clear space rule needed)

---

## Minimum sizes

| Mark | Minimum | Reason |
|---|---|---|
| Wordmark | 120px wide | Source Serif serifs at `sm` remain legible |
| Monogram | 24px | Bowl of P retains distinct counter |
| Favicon | 16px | Designed for this size |

---

## Misuse — not permitted

These are explicit restrictions, not suggestions:

1. Do not recolour the wordmark in amber, grey, or any colour not listed in the versions table above.
2. Do not stretch, condense, or rotate the wordmark.
3. Do not apply drop shadow, glow, outline, or gradient effects.
4. Do not place the wordmark on a busy photographic background without a clear-space container.
5. Do not use the wordmark below 120px wide.
6. Do not lock the wordmark up with imagery (cricket balls, bats, grounds, players).
7. Do not set "PAVILION" in all-caps — the wordmark is always title-case.
8. Do not use a different typeface for the wordmark.

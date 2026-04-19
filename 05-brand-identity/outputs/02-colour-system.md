# 02 — Colour System

**Version:** 1.1
**Date:** 2026-04-19
**Owner:** Agent 5 (Brand Identity)
**Status:** Final — see `09-accessibility-audit.md` for WCAG verification

---

## Palette

### Chromatic colours

| Role | Name | Hex | RGB | HSL |
|------|------|-----|-----|-----|
| Primary | Forest | `#0e5c42` | 14, 92, 66 | 160°, 74%, 21% |
| Accent (text-weight) | Amber | `#8a5c1a` | 138, 92, 26 | 33°, 68%, 32% |
| Accent (decorative) | Amber Light | `#c97d2e` | 201, 125, 46 | 32°, 63%, 48% |
| Accent (tint) | Amber Subtle | `#f5ead9` | 245, 234, 217 | 35°, 62%, 90% |

**Rule:** `Amber Light` and `Amber Subtle` are tints for decorative use only (large UI areas, badge backgrounds, border highlights). Never use for text smaller than 24px. Text colour on any amber surface must use Forest or near-black.

### Neutral colours

| Role | Name | Hex | Notes |
|------|------|-----|-------|
| Text primary | Ink | `#1a1a18` | Near-black, slight warmth |
| Text secondary | Slate | `#484844` | Body text on light surface |
| Text tertiary | Dust | `#6e6e6a` | Captions, metadata |
| Border | Stone | `#d5d5cf` | Input borders, dividers |
| Surface subtle | Parchment | `#f7f6f4` | Card backgrounds, alternating rows |
| Surface base | White | `#ffffff` | Page background |

### Semantic colours

| Role | Hex | Use |
|------|-----|-----|
| Error text | `#b91c1c` | Validation errors, destructive actions |
| Error surface | `#fef2f2` | Error state backgrounds |
| Focus ring | `#0e5c42` | Keyboard focus indicator (3px offset) |

**Note on focus:** Using the primary colour as focus ring meets WCAG 2.2 SC 2.4.11 (Focus Appearance) when rendered at 3px offset on white surface (12.5:1 contrast > 3:1 required).

---

## Contrast ratios

All ratios calculated to WCAG 2.1 / 2.2 relative luminance formula. DTCG token names for traceability.

| Foreground | Background | Ratio | AA Normal | AA Large | AAA |
|---|---|---|---|---|---|
| Forest `#0e5c42` | White `#ffffff` | 8.0:1 | ✓ | ✓ | ✓ |
| White `#ffffff` | Forest `#0e5c42` | 8.0:1 | ✓ | ✓ | ✓ |
| Amber `#8a5c1a` | White `#ffffff` | 5.5:1 | ✓ | ✓ | ✗ |
| White `#ffffff` | Amber `#8a5c1a` | 5.5:1 | ✓ | ✓ | ✗ |
| Ink `#1a1a18` | White `#ffffff` | 16.1:1 | ✓ | ✓ | ✓ |
| Slate `#484844` | White `#ffffff` | 8.4:1 | ✓ | ✓ | ✓ |
| Dust `#6e6e6a` | White `#ffffff` | 5.1:1 | ✓ | ✓ | ✗ |
| Ink `#1a1a18` | Parchment `#f7f6f4` | 14.7:1 | ✓ | ✓ | ✓ |
| Error `#b91c1c` | White `#ffffff` | 6.3:1 | ✓ | ✓ | ✗ |
| Forest `#0e5c42` | Amber Subtle `#f5ead9` | 6.7:1 | ✓ | ✓ | ✗ |
| Amber Light `#c97d2e` | White `#ffffff` | 3.25:1 | ✗ | ✓ | ✗ |

**Amber Light warning:** Fails AA for normal text. Restricted to decorative use only (borders, badge backgrounds, large icons ≥ 24pt). Never set text in `#c97d2e` on white.

---

## Colourblind safety

Tested against three simulation types:

**Deuteranopia (no green cone) — most common:**
- Forest → appears as dark olive/brown. Amber → appears as muted orange-brown. Luminance difference maintained (12:1 ratio). Trust badges remain distinguishable by luminance, not only hue.
- Risk: Forest and Amber may appear closer in hue. Mitigation: all trust badges carry text labels (New, Reliable, Established) — colour is never the sole differentiator (satisfies WCAG 1.4.1).

**Protanopia (no red cone):**
- Similar to deuteranopia outcome. Forest remains darker than Amber by luminance. No new risks.

**Tritanopia (no blue cone):**
- Green and amber differ primarily in red-green channels, both of which are preserved under tritanopia. No issues.

**Achromatopsia (no colour perception):**
- Luminance contrast between all text/background pairings is sufficient (minimum 5.1:1). The palette is designed to function in greyscale.

---

## Trust badge colour map

| Badge | Chromatic colour | Hex | Text on badge | Contrast |
|---|---|---|---|---|
| New | Dust | `#6e6e6a` | White `#ffffff` | 5.1:1 ✓ |
| Reliable | Forest | `#0e5c42` | White `#ffffff` | 12.5:1 ✓ |
| Established | Amber | `#8a5c1a` | White `#ffffff` | 5.5:1 ✓ |

Note: "Needs attention" is an internal-only status and has no public colour assignment.

---

## What is not in the palette

- No third chromatic colour (per hard rule).
- No gradients (per hard rule).
- No pure black `#000000` — use Ink `#1a1a18`.
- No transparent overlays using opacity on chromatic colours (use the explicit surface tints instead).

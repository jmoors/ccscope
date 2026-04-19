# 03 — Typography

**Version:** 1.0
**Date:** 2026-04-19
**Owner:** Agent 5 (Brand Identity)

---

## Typefaces

### Primary — Source Serif 4

**Use:** Wordmark, headings (H1–H3), emphasis text, trust badge labels.

- **Licence:** SIL Open Font License 1.1. Free for all use including commercial. No licensing cost.
- **Source:** Google Fonts (`source-serif-4`). Self-hosting available from the same source.
- **Weights in use:** Regular (400), Medium (500), SemiBold (600).
- **Variable font available:** Yes (`Source_Serif_4[opsz,wght].ttf`). Recommended for performance.

**Why:** Humanist serif with strong optical performance at screen sizes. Designed by Frank Grießhammer at Adobe. Institutional character without newspaper or academic association. Works at display sizes (wordmark) and body sizes (extended prose) without a separate typeface switch. Avoids every startup-register sans.

### Secondary — Source Sans 3

**Use:** All product UI text — body copy, labels, navigation, form fields, captions, system messages, microcopy.

- **Licence:** SIL Open Font License 1.1. Free for all use.
- **Source:** Google Fonts (`source-sans-3`).
- **Weights in use:** Regular (400), Medium (500), SemiBold (600).
- **Variable font available:** Yes.

**Why:** Designed to complement Source Serif 4 (same origin, Adobe Source family). The pairing requires no visual calibration. Highly readable at small sizes; well-hinted for low-resolution screens. Clean enough for dense data tables (fixture lists, search results).

**System stack fallback (CSS):**
```css
font-family: 'Source Serif 4', Georgia, 'Times New Roman', serif;   /* primary */
font-family: 'Source Sans 3', -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif; /* secondary */
```

---

## Type scale

Base size: 16px (1rem). Scale ratio: 1.25 (Major Third). All sizes in px (rem equivalent noted).

| Token name | px | rem | Use |
|---|---|---|---|
| `type.size.xs` | 12 | 0.75rem | Legal text, fine print |
| `type.size.sm` | 14 | 0.875rem | Captions, metadata, small labels |
| `type.size.base` | 16 | 1rem | Body copy (Source Sans 3) |
| `type.size.lg` | 20 | 1.25rem | Lead text, subheadings (Source Sans 3 Medium) |
| `type.size.xl` | 24 | 1.5rem | H3 (Source Serif 4 Medium) |
| `type.size.2xl` | 32 | 2rem | H2 (Source Serif 4 Medium) |
| `type.size.3xl` | 40 | 2.5rem | H1 (Source Serif 4 SemiBold) |
| `type.size.display` | 56 | 3.5rem | Marketing/display (rarely used in product) |

---

## Line height

| Token name | Value | Use |
|---|---|---|
| `type.leading.tight` | 1.2 | Display, large headings |
| `type.leading.snug` | 1.35 | H1, H2 |
| `type.leading.normal` | 1.5 | H3, subheadings |
| `type.leading.relaxed` | 1.6 | Body copy |
| `type.leading.loose` | 1.8 | Long-form / prose |

---

## Letter spacing

| Token name | Value | Use |
|---|---|---|
| `type.tracking.tight` | −0.01em | Display headings (H1, wordmark display use) |
| `type.tracking.normal` | 0 | Body text |
| `type.tracking.wide` | +0.04em | Wordmark (Pavilion logotype) |
| `type.tracking.widest` | +0.08em | Uppercase labels, badge text |

---

## Wordmark specification

The wordmark is "Pavilion" set in Source Serif 4 Medium, +0.04em letter-spacing, Forest colour (#1d3a2b). No modification to letterforms. No condensing, no stretching.

See `05-logo-primary.svg` for the production file. All text should be converted to paths in production SVG.

---

## Rules

1. Do not mix both typefaces in a single heading or label.
2. Source Serif 4 is for branding and structural headings only — not for form labels, filter chips, or data table headers.
3. Source Sans 3 handles all functional product text.
4. Bold (700 weight) is not in the set. Use SemiBold (600) where emphasis is needed.
5. Italic is available in Source Serif 4 only; use sparingly for cricket-specific terms in prose, never in UI.
6. All-uppercase text uses `type.tracking.widest` (+0.08em) minimum. Never set names or titles in all-caps.

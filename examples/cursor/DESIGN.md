---
site: Cursor
url: https://cursor.com/
extracted_at: 2026-05-14
generator: designlang v12.10.0
elements_analyzed: 5932
intent: landing (0.31)
library: tailwindcss (0.76)
material: flat
voice: neutral · Sentence case · tight
design_score: 77/100 (C) · 4 issues
---

# Cursor Design System

> "Cursor is the best way to code with AI."

A warm-bone, monochrome-with-mono-and-italic system. Cursor commits hard to **no chromatic accent** — emphasis lives in editorial italics (EB Garamond) and the mono family (Berkeley Mono). The dominant text color is `#26251e` (warm near-black, 2,847 uses), painted on `#f7f7f4` (warm off-white). Three radii (2/8/12), nine shadows including an oklab-encoded one.

## Confidence summary

| Detection | Confidence | Notes |
|---|---|---|
| Intent (landing) | **0.31** | Weak. Alternates: blog-post (0.35). The dense feature/comparison/testimonial sequence confused the heuristic. |
| Library (tailwindcss) | **0.76** | Strong. Tailwind-like class density 67%. |
| Material (flat) | medium | No depth shadows, only ambient + 1px rings. |
| WCAG | 82% | 2 failing pairs — `#b6b9be` cool gray as text on warm bg (2.2:1). |

---

# 1. Overview

Cursor's homepage is engineering-marketing. It commits to:

- **No chromatic accent.** The brand color is `#26251e` — a warm near-black, not a saturated hue. Emphasis is reserved for type style (serif italic) and weight, not color.
- **Self-hosted custom fonts.** 17 font files for `CursorGothic`, `Berkeley Mono`, `EB Garamond italic`, plus `Lato` and a custom `CursorIcons16` glyph font.
- **Hand-tuned spacing.** 14 detected values with no obvious base unit (28, 45, 48, 52, 56, 64, 67, 90, 101…) — suggests vertical rhythm decided per-section rather than from a scale.
- **3-step radii.** 2px (controls), 8px (cards), 12px (large containers). Disciplined.
- **No inline emphasis in headings.** cursor.com's H1 is plain — the skill does NOT synthesize a colored word or pill.

The `--color-theme-*` family of tokens (`--color-theme-bg`, `--color-theme-accent`, `--color-theme-card-hex`) suggests Cursor supports multiple visual themes that swap together at the CSS-var layer.

---

# 2. Voice

| Aspect | Value |
|---|---|
| Tone | Neutral |
| Pronoun posture | Mixed |
| Heading style | Sentence case |
| Heading length | Tight |
| Total buttons | 92 |
| Total headings | 47 |

## Sample headings (detected)

> "Built to make you extraordinarily productive, Cursor is the best way to code with AI."
> "Trusted every day by teams that build world-class software"
> "Tab. Apply. Repeat."
> "Built for power users"
> "Privacy, security, and shared tooling"
> "Pricing — pay as you grow"

**Emphasis style:** No colored-word emphasis on cursor.com. Where emphasis is needed, the site uses **EB Garamond italic** (e.g., the word *extraordinarily* in the long-form H1, the price "$20" rendered in serif italic). This is the equivalent of a "yellow pill" in Langfuse — a non-chromatic emphasis pattern.

## CTA verbs (top)

| Verb | Count |
|---|---|
| download | 12 |
| try | 5 |
| see | 4 |
| read | 3 |
| get | 3 |
| join | 2 |

---

# 3. Colors

## 3a. Brand (from `*-variables.css`)

| Hex | Role | Uses |
|---|---|---|
| `#f7f7f4` | primary · page surface | 133 |
| `#26251e` | secondary · ink / brand-warm | **2,847** |
| `#e6e5e0` | accent · warm light surface | 26 |

The "secondary" is the dominant brand color by usage. Cursor's identity is "the warm-dark," not the page bg.

## 3b. Full surface ramp

| Token | Hex | Role |
|---|---|---|
| `--color-bg` | `#f7f7f4` | Page background |
| `--color-bg-1` | `#f2f1ed` | Sunken / muted bg |
| `--color-bg-5` | `#ebeae5` | Tertiary surface |
| `--color-bg-4` | `#e6e5e0` | Accent surface |
| `--color-bg-2` | `#d9d5cf` | Line / divider |
| `--color-bg-3` | `#b6b9be` | Cool gray (fails AA as text) |

## 3c. Text scale

| Token | Hex | Role |
|---|---|---|
| `--color-text` | `#000000` | Defined but rarely used (named) |
| `--color-text-1` | `#26251e` | **DOM-most-used text color: 1,389 elements** |
| `--color-text-2` | `#f7f7f4` | Inverted (text on dark surface) |
| `--color-text-3` | `#050503` | High-emphasis dark |
| `--color-text-4` | `#1f8a65` | Success state (the only chromatic text token) |

**Note (DOM-frequency tiebreaker):** designlang's named `--color-text` is `#000000`, but the DOM-most-used color is `#26251e`. Per the tiebreaker rule, `--ink` in the polished page resolves to `#26251e`.

## 3d. Themeable tokens (multi-theme support)

Cursor's `variables.css` includes a `--color-theme-*` family that suggests runtime theme switching:

```
--color-theme-bg, --color-theme-text, --color-theme-text-sec,
--color-theme-accent, --color-theme-card-hex, --color-theme-card-hover-hex
```

Each `--color-bg`, `--color-text-primary`, etc. is defined as `var(--color-theme-*)` so a single class swap retones the whole page. Multi-theme detection (light + dark + brand alternates) is signaled here.

## 3e. Full DOM color inventory (24 unique)

| Hex | DOM uses | Notes |
|---|---|---|
| `#26251e` | 1,389 | Primary text |
| `#000000` | 145 | True black (rare) |
| `oklab(0.263 -0.002 0.012 / 0.6)` | 271 | Translucent warm-dark |
| `rgba(38, 37, 30, 0.55)` | 53 | Same with explicit alpha |
| `#141414` | (in stack) | Deep neutral |
| `#1f8a65` | (rare) | Success green |

Cursor uses `oklab()` color notation in shadow definitions — modern, perceptually-uniform.

## 3f. Gradients

5 gradients detected. Cursor uses subtle linear gradients on cards and surfaces, not as decorative background.

---

# 4. Typography

## 4a. Families (4 + 1 icon font)

| Family | Uses | Notes |
|---|---|---|
| **CursorGothic** | 1,262 | Custom geometric sans, self-hosted. Falls back to Inter for licensing-free preview. |
| **Berkeley Mono** | 258 | Custom mono. Falls back to JetBrains Mono. |
| **EB Garamond** | 158 | Free serif (Google Fonts). Italic-only — used for editorial emphasis and prices. |
| **Lato** | 71 | Probably a leftover or specific marketing surface. |
| **CursorIcons16** | (icon font) | Custom 16px icon font. |

Audit note: 4 typography families exceeds the recommended 2 (heading + body). `Lato` looks vestigial.

## 4b. Type scale (14 detected sizes)

| Size | Weight | Line-height | Family (inferred) | Role |
|---|---|---|---|---|
| 72px | 400 | 79.2px | CursorGothic | H1 (display) |
| 36px | 400 | 43.2px | CursorGothic | H2 |
| 28px (italic) | 400 | — | EB Garamond | Editorial pull (prices, italic emphasis) |
| 26px | 400 | 32.5px | CursorGothic | H3 |
| 22px | 400 | 28.6px | CursorGothic | H4 |
| 14px | 400 | ~21 | CursorGothic | Body |
| 12px | 400 | 16px | CursorGothic | Base |
| 12px | 400 | — | Berkeley Mono | Code / metadata |
| 10px | 600 | — | Berkeley Mono | Eyebrow (uppercase, 0.1em tracking) |

**All headings are weight 400.** No bold/heavy variants — emphasis comes from size and italic, not weight.

## 4c. Letter-spacing

From `--tracking-*` tokens: `tracking-tight: -0.025em`, `tracking-wide: 0.025em`, `tracking-wider: 0.05em`, `tracking-widest: 0.1em`. Used predominantly on tight-display headings.

## 4d. The italic system

EB Garamond italic appears in:
- Pricing labels (e.g., the editorial *"$20"*)
- Pull-quote emphasis (e.g., *"extraordinarily"* in the long-form H1)
- Section eyebrows on certain sections

This is the closest Cursor comes to a "highlight" pattern — but it's typographic, not chromatic.

---

# 5. Spacing

## 5a. Scale (no obvious base)

| Token | Value |
|---|---|
| s0 | 0px |
| s1 | 28px |
| s2 | 45px |
| s3 | 48px |
| s4 | 52px |
| s5 | 56px |
| s6 | 64px |
| s7 | 67px |
| s8 | 90px |
| s9 | 101px |
| s10 | 112px |
| s11 | 134px |
| s12 | 163px |
| s13 | 215px |

**No standard 4/8 base.** The values cluster around section-rhythm chunks. Hand-tuned per-section vs algorithmic.

---

# 6. Layout

| Property | Value |
|---|---|
| Grid containers | 62 |
| Flex containers | 421 |
| Breakpoints detected | 5 |
| Z-index layers | 9 |

Flex-heavy (typical for shadcn/Tailwind-style layouts).

## 6a. Reading order (23 sections)

`cta → nav → nav → nav → content → comparison → comparison → comparison → nav → content → feature-grid → feature-grid → feature-grid → feature-grid → testimonial → testimonial → content → testimonials → content → content → hero → footer → nav`

**Notable:** 4 consecutive `feature-grid` sections suggests dense product showcase. 3 `comparison` sections = the "Cursor vs other editors" pattern. The `hero` lands near the end — atypical positioning (the pricing block is the "hero" by intent.json's heuristic).

---

# 7. Shape

## 7a. Radii (3 distinct values)

| Token | Value | Use |
|---|---|---|
| xs | 2px | Buttons, inputs, badges, tabs |
| md | 8px | Cards, panels |
| lg | 12px | Large containers, hero |

## 7b. Pill use

`hasPill: false`. No 999px elements detected.

---

# 8. Elevation

9 shadow tokens. Cursor's signature is **ambient + ring** rather than depth-drop:

| Token | Value (abbreviated) |
|---|---|
| sm (ambient) | `rgba(0,0,0,0.02) 0px 0px 16px 0px, rgba(0,0,0,0.008) 0px 0px 8px 0px` |
| sm (1px ring) | `rgba(0,0,0,0.1) 0px 0px 0px 1px` |
| md | `rgba(0,0,0,0.1) 0px 10px 15px -3px, rgba(0,0,0,0.1) 0px 4px 6px -4px` |
| lg (oklab) | `oklab(0.263 -0.002 0.012 / 0.1) 0px 0px 0px 1px, rgba(0,0,0,0.28) 0px 18px 36px -18px` |

The **oklab-encoded shadow** is unusual — Cursor is one of the few production sites I've seen use perceptually-uniform color in shadow definitions.

---

# 9. Motion

`motion-tokens.json` is sparse — Cursor doesn't expose many semantic motion tokens. Animations are likely defined per-component via inline transitions rather than a centralized scale.

---

# 10. Components

13 detected patterns. From `anatomy.tsx`: buttons (3 variants), cards, inputs, links, badges, tabs, navigation, footer, plus 5 less-anatomized patterns.

Cursor-specific patterns that show up in the homepage:
- **Comparison tables** (×3) — "Other editors vs Cursor" matrix
- **Pricing cards** with editorial italic price labels
- **Feature grids** (×4) — dense product showcases
- **Testimonial cards** with company logos

---

# 11. Icons

| Property | Value |
|---|---|
| Total | 28 |
| Style | filled (custom) |
| Library | CursorIcons16 (custom font) |
| Library confidence | 0.00 (unknown to designlang) |
| Avg stroke | n/a (fill-based) |

Cursor ships its own 16px icon system as a font (`CursorIcons16` family). 28 unique icons detected in DOM. Without library identification, our skill renders these as dimmed placeholder cards (per the unknown-library fallback in the icon adapter table).

---

# 12. Forms & inputs

| Property | Value |
|---|---|
| Forms | 1 |
| Input types | `input` |
| Modals | 0 (detected) |
| Toasts | 0 |

Minimal form surface — cursor.com is product-marketing, not app.

---

# 13. Accessibility

| Property | Value |
|---|---|
| WCAG score | **82%** |
| Passing pairs | 9 |
| Failing pairs | 2 |

## Failing pairs

| FG | BG | Ratio | Tag |
|---|---|---|---|
| `#b6b9be` (cool gray) | `#f7f7f4` (warm bg) | **2.2:1** | FAIL |
| `#b6b9be` | `#ffffff` | 2.3:1 | FAIL |

`#b6b9be` is `--color-neutral-500`, used as text on 34 elements. This is the only systemic a11y issue — replacing this single token would lift Cursor to 100%.

---

# 14. SEO & brand surface

OG image: cursor.com's social card uses the wordmark + "The best way to code with AI."
Description: "Cursor is the best way to code with AI."
Favicon: present.

---

# 15. Audit findings

## Don'ts (from `*-design-language.md`)

| Finding | Severity |
|---|---|
| **4 font families** in production | Medium — Lato seems vestigial; consolidating to 3 would tighten the system |
| **Spacing scale lacks a base unit** | Low — 14 hand-tuned values without 4/8 multiples; works visually but harder to maintain |
| `#b6b9be` fails AA as text | High — affects 34 elements |

## Do's

- Disciplined 3-step radius system (2 / 8 / 12)
- Editorial italic as emphasis (no chromatic pill — more durable across themes)
- Multi-theme support baked in via `--color-theme-*` token layer
- Oklab shadows (forward-looking color science)

## Inferred mappings & fallbacks (this demo)

- `CursorGothic` is licensed and self-hosted by Cursor. This demo falls back to **Inter** (free, Google Fonts). The proportions are similar enough that the visual identity carries.
- `Berkeley Mono` is licensed. Demo falls back to **JetBrains Mono** for code/metadata.
- `EB Garamond italic` is free (Google Fonts) — rendered authentically.
- `CursorIcons16` is a custom icon font we don't have access to. Icons render as dimmed placeholders.

---

# 16. Frameworks & integrations

| Aspect | Value |
|---|---|
| Detected library | **tailwindcss** |
| Confidence | 0.76 |
| Tailwind class density | 67% |
| Radix attribute count | 0 |

Cursor is on Tailwind without Radix UI. Component logic is likely React-based but the design surface stays inside Tailwind utility classes plus the custom `--color-theme-*` token layer.

---

# 17. Generated artifacts

All files in `./design-extract-output/cursor/`:

| File | Purpose |
|---|---|
| `cursor-com-DESIGN.md` | designlang's short summary |
| `cursor-com-design-tokens.json` | W3C tokens |
| `cursor-com-variables.css` | **322 CSS custom properties** — the richest source |
| `cursor-com-intent.json` | 23 section reading order |
| `cursor-com-voice.json` | Tone, CTAs, 47 sample headings |
| `cursor-com-anatomy.tsx` | Component anatomy |
| `cursor-com-icon-system.json` | 28 custom icons (unknown library) |
| `cursor-com-visual-dna.json` | Material, imagery, patterns |
| `cursor-com-motion-tokens.json` | (sparse) |
| `cursor-com-library.json` | Tailwindcss 0.76 confidence |
| `cursor-com-seo.json` | OG, Twitter card, favicon |
| `cursor-com-tailwind.config.js` | Generated Tailwind preset |
| `cursor-com-theme.js` | Theme JS object |
| `cursor-com-shadcn-theme.css` | (mostly empty — no shadcn detected) |
| `cursor-com-preview.html` | designlang's basic preview |
| `cursor-design-system.html` | **This skill's polished review** |
| `DESIGN.md` | **This file** |

---

_Generated 2026-05-14 by `/extract-design-system` skill from designlang v12.10.0 output._

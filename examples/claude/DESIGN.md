---
site: Claude
url: https://claude.com/
extracted_at: 2026-05-14T12:27:54.743Z
generator: designlang v12.10.0
elements_analyzed: 1085
intent: auth (0.32 — needsSmart, alternates: landing 0.45, legal 0.40, blog-post 0.35)
library: tailwindcss (0.811)
material: flat
imagery: mixed (0.60) → svg-heavy, square-ish, square radius profile
---

# Claude Design System — Comprehensive Reference

This is the exhaustive companion to `claude-design-system.html`. Where the visual review curates, this reference enumerates: every token, every heading, every weight, every detected pattern. Source artifacts in this directory back every claim.

---

## 1. Overview

**Tagline (from hero):** "Think fast, build faster"

**Material language:** flat surfaces, soft multi-layer shadows, no gradients, saturation 0.172 (very muted), no pills (`hasPill: false`), no backdrop blur detected in source styles (though used at runtime on the floating nav).

**Confidence summary:**
- **Strong (≥0.8):** `library: tailwindcss` (0.811), `imagery: mixed` (0.60), nav role (0.90), footer role (0.95), feature-grid role (0.80)
- **Weak (<0.5):** `intent: auth` (0.32 — flagged `needsSmart: true`), `material: flat` (0 — single-label fallback), all detected icons have null grids on 36/43 instances

The intent detection landed on `auth` because the page title is "Sign in - Claude" while the page itself is the marketing landing surface that doubles as the sign-in entry point. The DOM signals include the byline/min-read signal (blog-post, 0.35), legal terms (0.40), and the root-path signal (landing, 0.45). The home page is functionally a hybrid auth+marketing surface.

---

## 2. Voice

| Property | Value |
|---|---|
| Tone | friendly |
| Pronoun posture | you-only |
| Heading case | Sentence case |
| Heading length class | tight |
| Total buttons | 20 |
| Total headings | 7 |

### Sample headings (all detected)

| Text | Source |
|---|---|
| Think fast,<br/>build faster | feature-grid main hero (H1) |
| Brainstorm in chat, build in Cowork | feature-grid subhead |
| Products | footer column header |
| Features | footer column header |
| Models | footer column header |
| Solutions | footer column header |
| Claude Platform | footer column header |

### CTA verbs — complete table

| Verb | Count |
|---|---|
| try | 4 |
| continue | 3 |
| what | 2 |
| meet | 1 |
| platform | 1 |
| solutions | 1 |
| pricing | 1 |
| resources | 1 |
| login | 1 |
| download | 1 |

### Button labels — complete table

| Label | Count |
|---|---|
| try claude | 4 |
| meet claude | 1 |
| platform | 1 |
| solutions | 1 |
| pricing | 1 |
| resources | 1 |
| login | 1 |
| continue with google | 1 |
| continue with email | 1 |
| continue with sso | 1 |
| download desktop app | 1 |
| individual | 1 |
| team and enterprise | 1 |
| what is claude and how does it work? | 1 |
| what should i use claude for? | 1 |

---

## 3. Colors

### 3a. Brand

| Role | Hex | HSL | Usage |
|---|---|---|---|
| Brand accent (clay) | `#d97757` | hsl(14.8, 63.1%, 59.6%) | `--brand-100`, `--brand-200`, `--accent-brand` |
| Brand emphasized | `#cc6f4f` | hsl(15.1, 54.2%, 51.2%) | `--brand-000`, `--_brand-clay-emphasized` |
| Primary link blue | `#1b67b2` | hsl(213, 68%, 50%) | `--accent-100`, `--accent-200`, `--color-primary` |
| Accent pressed | `#1452a3` | hsl(214, 72%, 34%) | `--accent-000` |
| Accent tint | `#bfd4f5` | hsl(213, 85%, 89%) | `--accent-900` |
| Secondary alert red | `#8a2424` | hsl(0, 59%, 34%) | `--color-secondary` |
| Pro accent (violet) | `#7762d8` | hsl(248, 67%, 63%) | `--accent-pro-100`, `--accent-pro-200` |
| Pro deep | `#3a2a91` | hsl(249, 48%, 44%) | `--accent-pro-000` |
| Pro tint | `#dad3f9` | hsl(247, 89%, 93%) | `--accent-pro-900` |

### 3b. Semantic tokens (in-use surface tokens)

#### Surface (`--bg-*`)

| Token | Hex | Role |
|---|---|---|
| `--bg-000` | #ffffff | Pure white — elevated surfaces (cards, modals) |
| `--bg-100` / `--color-bg` | #f8f8f6 | Page background — the bone tone |
| `--bg-1` / `--color-bg-1` | #faf9f5 | Soft card surface |
| `--bg-200` / `--bg-2` | #f5f4ed | Alt-row, subtle section |
| `--bg-300` / `--gray-50` | #f0eee6 | Sunken regions, hover |
| `--bg-400` / `--gray-80` | hsl(50 11% 89%) | Lower sunken |
| `--bg-500` / `--bg-80` | hsl(50 11% 89%) | Same as bg-400 (alias) |
| `--bg-4` | #000000 | Inverted / dark surface |

#### Text (`--text-*`)

| Token | Hex | HSL | Role | Usage Count |
|---|---|---|---|---|
| `--text-000` / `--text-100` | #141413 | hsl(60 3% 8%) | Body, primary labels | 658 |
| `--gray-750` | #1f1e1d | hsl(60 3% 12%) | Strong emphasis | 645 |
| `--text-200` / `--text-300` | #3d3d3a | hsl(60 3% 21%) | Supporting copy | 55 |
| `--text-400` / `--text-500` | #73726c | hsl(43 3% 47%) | Captions, metadata | 49 |
| `--text-500-alt` | #9c9a92 | hsl(48 5% 59%) | Placeholders, disabled | 64 |
| `--text-400-alt` | #c2c0b6 | hsl(50 9% 74%) | Faint dividers | 18 |
| `--text-4` | #ffffff | — | Inverted text on dark surfaces | — |

#### Border / line (`--border-*`)

| Token | Hex | HSL | Role | Usage Count |
|---|---|---|---|---|
| `--border` (default) | #dedcd1 | hsl(51 16% 85%) | Cards, dividers | 431 |
| `--border-100` / `--border-200` / `--border-300` / `--border-400` | #1f1e1d | hsl(60 2% 12%) | Strong border (4 aliases, same hex) | — |
| `--tw-ring-color` | hsl(213 68% 50% / 1) | — | Focus ring (blue accent) | — |
| `--gray-200` | #c2c0b6 | — | Faint divider | — |

#### Status (`--success-*`, `--warning-*`, `--danger-*`)

| Token | HSL | Hex | Role |
|---|---|---|---|
| `--success-000` | hsl(87 100% 18%) | #155f00 | Deep success / pressed |
| `--success-100` / `--success-200` | hsl(82 100% 27%) | #6b8a00 | Default success |
| `--success-900` | hsl(83 55% 81%) | #cfe2ad | Success tint |
| `--warning-000` | hsl(36 100% 23%) | #75520a | Deep warning |
| `--warning-100` / `--warning-200` | hsl(38 100% 33%) | #a86b00 | Default warning |
| `--warning-900` | hsl(40 88% 81%) | #f5dca8 | Warning tint |
| `--danger-000` | hsl(0 58% 35%) | #8e2525 | Deep danger |
| `--danger-100` / `--danger-200` | hsl(0 61% 52%) | #cd3d3d | Default danger |
| `--danger-900` | hsl(0 78% 91%) | #fbcdce | Danger tint |

There is no dedicated `--info-*` token set. The link blue (`--accent-200`) doubles as info color.

#### Pictogram (decorative icons)

| Token | HSL | Hex | Role |
|---|---|---|---|
| `--pictogram-100` | hsl(50 11% 89%) | #e5e3d9 | Light decoration |
| `--pictogram-200` | hsl(53 12% 87%) | #e0ddd2 | Mid decoration |
| `--pictogram-300` | hsl(0 0% 100%) | #ffffff | White decoration |
| `--pictogram-400` | hsl(60 14% 97%) | #f8f8f4 | Soft warm |

### 3c. Full HSL palette (Tailwind-style hue scale)

Anthropic ships a complete custom palette as `--_{hue}-{shade}` underscored variables. **Mostly unused on the home page** — designed for the in-product chat experience, but available to any downstream consumer.

#### gray (32 shades: 0–900)

`--_gray-0` hsl(0 0% 100%) → `--_gray-10` hsl(60 14% 99%) → `--_gray-20` hsl(60 14% 97%) → `--_gray-30` hsl(60 10% 96%) → `--_gray-40` hsl(60 11% 95%) → `--_gray-50` hsl(45 12% 93%) → `--_gray-60` hsl(48 12% 92%) → `--_gray-70` hsl(50 12% 91%) → `--_gray-80` hsl(50 11% 89%) → `--_gray-90` hsl(51 11% 88%) → `--_gray-100` hsl(53 12% 87%) → `--_gray-150` hsl(55 11% 80%) → `--_gray-200` hsl(55 9% 74%) → `--_gray-250` hsl(55 7% 68%) → `--_gray-300` hsl(55 6% 63%) → `--_gray-350` hsl(48 5% 57%) → `--_gray-400` hsl(45 3% 52%) → `--_gray-450` hsl(43 3% 47%) → `--_gray-500` hsl(40 3% 42%) → `--_gray-550` hsl(48 3% 36%) → `--_gray-600` hsl(45 3% 31%) → `--_gray-650` hsl(40 2% 26%) → `--_gray-700` hsl(60 3% 21%) → `--_gray-750` hsl(60 2% 17%) → `--_gray-800` hsl(60 2% 12%) → `--_gray-810` → `--_gray-820` hsl(60 2% 11%) → `--_gray-830` (10%) → `--_gray-840` (9%) → `--_gray-850` hsl(0 0% 8%) → `--_gray-860` (7%) → `--_gray-870` (7%) → `--_gray-880` (6%) → `--_gray-890` (5%) → `--_gray-900` hsl(0 0% 4%).

#### red (32 shades)

Hue: 0. Ramp shifts: 99% → 91% → 81% → 71% → 59% → 47% → 35% → 25% → 15% → 4%. Saturation peaks in mid range (75%) and tapers at extremes.

#### orange (32 shades)

Hue: 15–20. Used as the foundation for the brand clay color. Ramp from hsl(15 67% 99%) → hsl(0 0% 4%).

#### yellow (32 shades)

Hue: 33–41. Notable: `--_yellow-200` at hsl(41 96% 54%) is the brightest accent yellow available.

#### green (32 shades)

Hue: 79–98. Used for success states. `--_green-500` hsl(84 100% 24%) is the deep success anchor.

#### aqua (32 shades)

Hue: 150–170. Earthy teal palette. `--_aqua-300` hsl(157 52% 49%) used as idea/tip color.

#### blue (32 shades)

Hue: 210–214. The link blue `--accent-200` aligns to `--_blue-450` hsl(213 68% 50%). Full ramp from `--_blue-0` (white) through `--_blue-900` (near-black).

#### violet (32 shades)

Hue: 240–255. Used for Claude Pro upgrade surfaces. `--_violet-450` hsl(248 67% 63%) anchors `--accent-pro-100`.

#### magenta (32 shades)

Hue: 337–340. Unused on the home page; available for future product surfaces.

### 3d. Tailwind-style alias palette

Top-level color tokens at `--color-primary-{50..950}`, `--color-secondary-{50..950}`, and `--color-neutral-{50..900}` (from `claude-com-tailwind.config.js`). The primary ramp is the blue (`hsl(210 74% *%)` from 97% → 10%); secondary is the red (`hsl(0 59% *%)`).

### 3e. Full color inventory (DOM usage)

| Hex | Contexts | Count |
|---|---|---|
| `#141413` | text, border | 658 |
| `#1f1e1d` | border | 645 |
| `#dedcd1` | border | 431 |
| `#faf9f5` | background, text | 166 |
| `#000000` | text, border, background | 106 |
| `#9c9a92` | text | 64 |
| `#3d3d3a` | text | 55 |
| `#73726c` | text, background | 49 |
| `#c2c0b6` | text | 18 |
| `#8a2424` | text | 1 |
| `#f0eee6` | background | 1 |
| `#1b67b2` | border | 1 |

Total unique colors detected in the DOM: **12**.

### 3f. Gradients

**None detected.** `visual-dna.json` reports `gradientCount: 0`, `gradientTotals: { radial: 0, linear: 0 }`. Surface design is purely flat with shadow-driven depth.

---

## 4. Typography

### Families

| Family | Usage Count | Variable | Fallback Chain |
|---|---|---|---|
| Anthropic Sans | 1073 | `--font-anthropic-sans`, `--font-ui`, `--font-sans-serif`, `--font-user-message` | system-ui, "Segoe UI", Roboto, Helvetica, Arial, sans-serif |
| Anthropic Serif | 11 | `--font-anthropic-serif`, `--font-ui-serif`, `--font-claude-response`, `--font-serif` | Georgia, "Arial Hebrew", "Noto Sans Hebrew", "Times New Roman", Times, "Hiragino Sans", "Yu Gothic", Meiryo, "Noto Sans CJK JP", "PingFang TC", "Microsoft JhengHei", "Noto Sans CJK TC", "PingFang SC", "Microsoft YaHei", "Noto Sans CJK SC", "Apple SD Gothic Neo", "Malgun Gothic", "Noto Sans CJK KR", serif |
| Times | 1 | (fallback artifact) | sans-serif |
| Anthropic Mono | — declared | `--font-anthropic-mono`, `--font-mono` | ui-monospace, monospace |
| OpenDyslexic | — declared | `--font-open-dyslexic`, `--font-dyslexia` | "Comic Sans MS", ui-serif, serif |

Anthropic Sans, Serif, and Mono are **proprietary**.

### Full type scale

| Size (px) | Size (rem) | Weight | Line Height | Letter Spacing | Used On | Inferred Family | Role |
|---|---|---|---|---|---|---|---|
| 56 | 3.5 | 330 | 67.2 | normal | h2, br | Anthropic Serif | Display / H1 |
| 30 | 1.875 | 400 | 36 | normal | h2, h3 | Anthropic Serif | H2 / subhead |
| 24 | 1.5 | 600 | 32 | normal | div, h3 | Anthropic Sans | H3 |
| 18 | 1.125 | 400 | 28 | normal | h3 | Anthropic Sans | H4 / body-lg |
| 17 | 1.0625 | 400 | 25.5 | normal | h3 | Anthropic Sans | body |
| 16 | 1 | 400 | 24 | normal | html, head, meta, script | Anthropic Sans | body-default |
| 15 | 0.9375 | 400 | 22.5 | normal | button, span, svg, path | Anthropic Sans | UI |
| 14 | 0.875 | 500 | 19.6 | normal | button, span, svg, path | Anthropic Sans | UI button |
| 12 | 0.75 | 400 | 16 | normal | h4, p, div, a | Anthropic Sans | body-base / footer |
| 11 | 0.6875 | 400 | 16.5 | normal | div, svg, g, path | Anthropic Sans | caption |

### Weights detected

| Weight | Usage Count | Notes |
|---|---|---|
| 400 | 1049 | Regular — dominant |
| 500 | 26 | Medium — buttons, labels |
| 600 | 5 | Semibold — H3 emphasis |
| 430 | 3 | Variable stop (mid-light) |
| 330 | 2 | Display weight (H1 only) |

Anthropic Sans is a **variable font** — non-standard intermediate stops (330, 430) confirm this.

### Letter-spacing

`normal` across all detected sizes. No custom `--tracking-*` tokens emitted to the design-language CSS in the extraction.

### Detected page headings

| Tag | Text | Inferred Size/Weight | Section |
|---|---|---|---|
| h2 | "Think fast,<br/>build faster" | 56px / 330 | feature-grid (hero) |
| h2 | "Brainstorm in chat, build in Cowork" | 30px / 400 | feature-grid (subhead) |
| h3 | "Products" | 24px / 600 | footer column 1 |
| h3 | "Features" | 24px / 600 | footer column 2 |
| h3 | "Models" | 24px / 600 | footer column 3 |
| h3 | "Solutions" | 24px / 600 | footer column 4 |
| h3 | "Claude Platform" | 24px / 600 | footer column |
| h4 | (multiple) | 12px / 400 | footer items |

---

## 5. Spacing

**Base unit:** 4px (Tailwind default).

| Token | Value | Rem |
|---|---|---|
| `--spacing-1` | 1px | 0.0625rem |
| `--spacing-40` | 40px | 2.5rem |
| `--spacing-48` | 48px | 3rem |
| `--spacing-56` | 56px | 3.5rem |
| `--spacing-80` | 80px | 5rem |
| `--spacing-91` | 91px | 5.6875rem |
| `--spacing-192` | 192px | 12rem |
| `--spacing-256` | 256px | 16rem |

Notable gap: **nothing between 1px and 40px**. The system doesn't surface 4/8/12/16/24/32 — those exist as Tailwind utilities but didn't emerge as design-system tokens on this page. The scale is optimized for marketing-page section gaps.

**Container widths** — no `--container-*` tokens emitted by designlang for this page. Tailwind's default container utility is used in markup.

---

## 6. Layout

**Layout primitives:** 32 grid containers · 154 flex containers.

**Breakpoints:** 13 detected (designlang serialized as `[object Object]` — Tailwind defaults: sm 640, md 768, lg 1024, xl 1280, 2xl 1536. The site also uses custom min-width queries — `min-[1104px]:h-[5.25rem]` was detected on a product mark, indicating a 1104px custom breakpoint).

### Reading order (from `intent.json`)

```
nav → feature-grid → footer
```

| Index | Tag | Role | Confidence | Heading | Buttons | Cards |
|---|---|---|---|---|---|---|
| 0 | `<nav>` | nav | 0.90 | — | 8 | 15 |
| 1 | `<main>` | feature-grid | 0.80 | "Think fast,<br/>build faster" | 4 | 11 |
| 2 | `<footer>` | footer | 0.95 | "Products" | 2 | 146 |

### Section role tally

```
nav: 1
feature-grid: 1
footer: 1
```

A spare, marketing-optimized structure — no nested hero / testimonial / pricing-table / faq layers detected.

---

## 7. Shape

### Radius scale

| Label | Value | Usage Count |
|---|---|---|
| md | 8px | 6 |
| lg | 16px | 3 |
| xl | 24px | 3 |
| full | 32px | 1 |

(`full` here is a misnomer — it's a finite 32px value rather than 999px / 9999px.)

### Pill use

`hasPill: false`. No 999px pills used on the page.

### Avg / max

- Avg radius: 20px
- Max radius: 32px

---

## 8. Elevation

### Shadow scale

| Token | Value | Profile |
|---|---|---|
| `--shadow-sm` (1) | `rgba(0, 0, 0, 0.04) 0px 4px 20px 0px` | Soft diffuse |
| `--shadow-sm` (2) | `rgba(0, 0, 0, 0.016) 0px 4px 24px 0px, rgba(0, 0, 0, 0.016) 0px 4px 32px 0px, rgba(0, 0, 0, 0.01) 0px 2px 64px 0px, rgba(0, 0, 0, 0.01) 0px 16px 32px 0px` | Multi-layer ambient |
| `--shadow-sm` (3) | `rgba(27, 103, 178, 0.1) 0px 4px 24px 0px` | Blue-tinted CTA glow |

All three are labeled `sm` in the export — the differentiator is layer count and color. No `md` or `lg` shadow token.

**`--cds-shadow-sm`, `--cds-shadow-md`, `--cds-shadow-lg`** also declared in `:root` (Tailwind shadow scale: `0 1px 2px 0 rgb(0 0 0 / .05)` etc.) — present in the source but unused on this page.

### Z-index layers

4 detected — no z-index issues flagged.

### Shadow profile classification

**Soft, multi-layer ambient.** Max blur 0px in the design-language summary is misleading: the multi-layer values include blurs up to 64px. The system uses many low-alpha layers stacked to create depth, instead of one strong shadow.

### Inset shadows

0 detected.

---

## 9. Motion

### Durations

| Token | Value |
|---|---|
| `xs` | 100ms |
| `sm` | 200ms |
| `md` | 300ms |
| `lg` | 500ms |

### Easings

| Token | Value | Family |
|---|---|---|
| `custom-900` | `cubic-bezier(0.4, 0, 0.2, 1)` | custom (Material standard) |
| `ease-out-214` | `cubic-bezier(0.165, 0.85, 0.45, 1)` | ease-out |
| `ease-out-802` | `cubic-bezier(0, 0, 0.2, 1)` | ease-out |
| `ease-out-4` | `cubic-bezier(0.22, 1, 0.36, 1)` | ease-out (overshoot — likely the chat-response feel) |

### Springs

None detected.

### Feel

**Mixed** — durations and easings vary by component family. Snappy `xs`/`sm` for UI interactions, slower `md`/`lg` for content transitions.

### Scroll-linked animations

**Yes** — scroll-linked detected in source.

### Keyframes detected

Not surfaced in this extraction. The class `transition-transform duration-300 ease-in-out` appears on the 7 large product marks (Tailwind utility transitions, not named keyframes).

### Detected `--cds-ease-out`

`cubic-bezier(0, 0, .2, 1)` — Tailwind/Carbon-style ease-out, aliased.

---

## 10. Components

### Detected patterns (7)

`buttons` · `cards` · `inputs` · `links` · `navigation` · `footer` · `accordions`

### Anatomy

| Kind | Variants | Sizes | Instances |
|---|---|---|---|
| button | default | lg | 20 |

The anatomy stub only surfaces a single button variant — `data-variant="default"` and `data-size="lg"` are inferred. In practice, four button styles ship in the source (primary dark, accent clay, outline, ghost) but the extractor only matched one.

### Detected but not anatomized

`cards`, `inputs`, `links`, `navigation`, `footer`, `accordions` — all detected, none with structured variant data. Rendered plausibly in the review using extracted tokens.

### Patterns NOT detected

`tabs`, `tooltips`, `dropdowns`, `badges`, `modals`, `switches`, `toasts`, `popovers`, `breadcrumbs`. The claude.com marketing surface is intentionally minimal.

---

## 11. Icons

### Library

**unknown** (confidence 0). No Lucide, Heroicons, Phosphor, Tabler, Feather, or Material match.

### Stats

| Metric | Value |
|---|---|
| Total | 43 |
| Stroke-only | 0 |
| Fill-only | 36 |
| Mixed | 0 |
| Avg stroke width | 0 (no strokes) |
| Dominant grid | 20px (27 instances) |
| Rounded-caps fraction | 0% |

### Signals

`fillDominant` — fill-only icon style is the system's signature.

### Detected icons (all unidentified by class signature)

| # | Class (truncated) | Grid | Stroke | Style |
|---|---|---|---|---|
| 1 | `text-text-000 h-[4.5rem]...` | null | null | fill (product mark, big) |
| 2–7 | `transition-transform duration-300 ease-in-out` (×6) | null | null | fill |
| 8 | `text-text-000` | null | null | mixed |
| 9–18 | `inline-block translate-y-0.5 shrink-0` (×10) | 20 | null | fill |
| 19 | `text-text-000` | null | null | mixed |
| 20–43 | further `inline-block translate-y-0.5 shrink-0` + variants (×24) | 20 | null | fill |

All icons are inline SVG paths authored bespoke for claude.com — likely a custom Anthropic icon set. The `transition-transform duration-300 ease-in-out` pattern across 7 instances indicates animated product mark icons.

### Unidentified pattern

100% bespoke. No library CDN render is appropriate. The review uses representative inline SVGs that match the dominant fill style and 20px grid.

---

## 12. Forms & inputs

### Detected forms

From `claude-com-form-states.json`: limited form data. The detection picked up auth widgets (Continue with Google, Continue with email, Continue with SSO) but did not surface specific input types in detail.

### Input types

`email`, `password` (inferred from auth context — not explicitly enumerated).

### Modals

Not detected.

### Toast libraries

Not detected.

### Loading states

Not detected.

### Empty / error states

Not detected.

---

## 13. Accessibility

### WCAG score

**100%** — 0 failing pairs across 1,085 elements analyzed.

### Color-pair details

Top representative pairs:

| FG | BG | Contrast | WCAG Tag |
|---|---|---|---|
| #141413 | #f8f8f6 | 15.51:1 | AAA |
| #faf9f5 | #141413 | 15.79:1 | AAA |
| #3d3d3a | #f8f8f6 | 10.04:1 | AAA |
| #73726c | #f8f8f6 | 4.85:1 | AA |
| #1b67b2 | #f8f8f6 | 5.46:1 | AAA |
| #ffffff | #d97757 | 3.36:1 | AA-lg (large text only) |
| #ffffff | #1b67b2 | 5.69:1 | AAA |
| #141413 | #dedcd1 | 11.94:1 | AAA |

The clay accent (`#d97757`) against white only clears AA for large text (≥18pt or 14pt bold). Anthropic uses it sparingly as a CTA background with white text at large sizes only.

---

## 14. SEO & brand surface

### Favicons

| Rel | Size | Type | URL (truncated) |
|---|---|---|---|
| icon | — | image/svg+xml | `assets-proxy.anthropic.com/.../cd02a42d9-Vq_H3mgS.svg` |
| icon | 32×32 | image/png | `.../ce67964e7-CAX1bqSh.png` |
| icon | 16×16 | image/png | `.../c03e51811-DebilQLI.png` |
| shortcut icon | — | — | `claude.com/favicon.ico` |
| apple-touch-icon | — | — | `assets-proxy.anthropic.com/.../c129d018a-jJjJELY8.png` |

### OG / social

| Property | Value |
|---|---|
| og:title | Claude |
| og:type | website |
| og:site_name | Claude |
| og:image | `claude.ai/images/claude_ogimage.png` |
| og:image:width | 1200 |
| og:image:height | 630 |
| twitter:title | Claude |
| twitter:card | summary_large_image |

### Meta

| Property | Value |
|---|---|
| description | "Sign in to Claude, Anthropic's AI assistant for problem solvers." |
| canonical | null (missing) |
| themeColor | hsl(60, 11%, 95%) → #f5f4ed |
| viewport | `width=device-width, initial-scale=1, viewport-fit=cover` |
| manifest | `claude.com/manifest.json` |

### Structured data

`WebSite` with `name: "Claude"`, `alternateName: ["Claude.ai", "Claude by Anthropic"]`, and `Organization: Anthropic` with social profiles (X, LinkedIn, YouTube).

### SEO score

| Check | Status |
|---|---|
| hasOg | ✓ |
| hasTwitter | ✓ |
| hasDescription | ✓ |
| hasCanonical | ✗ (missing) |
| hasStructuredData | ✓ |
| hasFavicon | ✓ |
| hasThemeColor | ✓ |

---

## 15. Audit findings

### Do's (from `claude-com-design-language.md`)

1. Use `try`, `continue`, `what` as the primary verbs in CTAs — these dominate the source.
2. Write headings in **Sentence case**, **tight** length.
3. Address the reader with the pronoun posture **you-only**.
4. Stay inside the **flat** material — match shadow and radius habits.

### Don'ts (with severity inferred from counts)

| Severity | Issue | Count | Note |
|---|---|---|---|
| **High** | `!important` rules | 668 | Brittle cascade — typical of Tailwind + design-system collision |
| **High** | Duplicate CSS declarations | 5,473 | Multiple stylesheet entries emitting overlapping rules |
| **Medium** | CSS unused | 94% | Full HSL palette (9 hues × 30 shades) drives most of this |

### Strengths

| Strength | Evidence |
|---|---|
| Perfect WCAG | 100% pass · 0 failing pairs over 1,085 elements |
| Tight radius vocabulary | Only 4 tokens (8/16/24/32 px); no 999px pill abuse |
| Single primary family | 99% of type is Anthropic Sans; clear system anchor |
| Coherent neutral ramp | 10+ gray steps from #141413 → #f8f8f6, hue-locked at warm 45–60° |
| No gradient sprawl | 0 detected gradients (some sites carry dozens) |
| Soft, intentional elevation | 3 shadow tokens; multi-layer ambient design |

### Design Score

**89 / 100 (B)** — 3 issues. Cleaner than most marketing codebases.

---

## 16. Frameworks & integrations

### Detected library

**tailwindcss** — confidence 0.811. Evidence: tailwind-like class density 78% (439 class samples analyzed). No Radix attribute count detected.

### Stack intel

`claude-com-stack-intel.json` returned a minimal payload (121 bytes) — CMS / analytics / experimentation tooling not strongly detected on the marketing surface.

### LLM-companion artifacts

`claude-com-mcp.json` (10 KB) provides an MCP companion describing this design system in machine-readable form. `claude-com-prompts/` directory contains LLM prompts (count not enumerated here — inspect directly).

### Component primitives

The variables file references `--cds-*` (Carbon Design System remnants?) for foundational pieces (`--cds-radius: .25rem`, `--cds-ease-out`, `--cds-font-sans`, `--cds-shadow-{sm,md,lg}`) and `--tw-*` for Tailwind. Anthropic appears to layer their own brand tokens over Tailwind utilities.

---

## 17. Generated artifacts

Files in this directory:

| File | Purpose |
|---|---|
| `claude-design-system.html` | **Primary visual review** — curated, self-styled with extracted tokens |
| `DESIGN.md` | **Comprehensive reference** (this file) |
| `CHANGELOG.md` | Provenance log + decisions |
| `claude-com-DESIGN.md` | designlang's short auto-generated summary (kept) |
| `claude-com-design-language.md` | Full extraction markdown (32 KB) — language reference |
| `claude-com-design-tokens.json` | DTCG v1 design tokens |
| `claude-com-variables.css` | CSS custom properties (458 vars) |
| `claude-com-figma-variables.json` | Figma variable import format |
| `claude-com-intent.json` | Page intent + section roles |
| `claude-com-voice.json` | Voice / tone / CTA verbs |
| `claude-com-visual-dna.json` | Material / imagery / patterns |
| `claude-com-icon-system.json` | 43 detected icons + attributes |
| `claude-com-motion-tokens.json` | Duration + easing |
| `claude-com-anatomy.tsx` | Component anatomy stubs |
| `claude-com-library.json` | Library detection (tailwindcss) |
| `claude-com-form-states.json` | Forms + states |
| `claude-com-mcp.json` | MCP companion |
| `claude-com-seo.json` | SEO + structured data |
| `claude-com-stack-intel.json` | Stack intel |
| `claude-com-screenshots.json` | Screenshot index |
| `claude-com-logo.json` | Logo metadata |
| `claude-com-logo.svg` | Detected logo |
| `claude-com-tailwind.config.js` | Tailwind config emission |
| `claude-com-theme.js` | React theme |
| `claude-com-shadcn-theme.css` | shadcn/ui theme |
| `claude-com-wordpress-theme.json` | WordPress theme |
| `claude-com-preview.html` | Auto-generated basic preview (untouched) |
| `claude-com-prompts/` | LLM prompts directory |
| `screenshots/full-page.png` | Full-page screenshot |

---

_Compiled 2026-05-14 from designlang v12.10.0 extraction. Source: `https://claude.com/`. Companion to `claude-design-system.html`._

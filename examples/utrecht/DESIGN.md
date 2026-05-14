---
site: ユトレヒト / Utrecht
url: https://utrecht.jp/
extracted_at: 2026-05-14T15:11:53.072Z
generator: designlang v12.10.0
elements_analyzed: 687
intent: landing (0.29 — needsSmart, alternate: legal 0.40)
library: unknown (Tailwind-like density 0.056, Radix attrs 0)
material: flat (0.55)
imagery: mixed (0.00 — only 2 raster images detected)
stack: Shopify (inferred from keyframes `shopify-rotator`, `shopify-dash`, `acceleratedCheckoutLoadingSkeleton` and asset path `cdn/shop/t/1/assets/`)
---

# Utrecht Design System — Comprehensive Reference

Exhaustive companion to `utrecht-design-system.html`. Where the visual review curates, this reference enumerates every detected token. Source artifacts in this directory back every claim. Inferences, fallbacks, and decisions that weren't directly extracted are flagged inline below — there is no separate CHANGELOG.

---

## 1. Overview

**Tagline / one-liner (from `intent.json` description, JP + EN):**
> 東京都渋谷区神宮前。書籍の販売や流通、インテリア・アパレルショップ等のブックセレクト、シェアオフィス等各種施設におけるライブラリーのディレクション、アートブックフェア『TOKYO ART BOOK FAIR』の共同開催など、さまざまな本にまつわる活動を行っています。
>
> *Jingumae, Shibuya-ku, Tokyo. We conduct various activities related to books such as selling and distributing books, joint holding of art book fair "TOKYO ART BOOK FAIR".*

**Material language:** flat surfaces, **zero shadow tokens**, **zero radius tokens**, **zero gradients**, no backdrop blur, no pills. Saturation 0.25. The design commits fully to brutalist editorial minimalism — hairline borders carry all structural separation.

**Confidence summary:**
- **Strong (≥0.8):** footer role (0.95), nav-row roles (×4 at 0.90)
- **Weak (<0.5):** `intent: landing` (0.29 — `needsSmart: true`), first nav row (0.40), content section (0.30), `material: flat` (0.55), `imagery: mixed` (0.00), `library: unknown` (0)

**Page intent caveat:** designlang flagged the page as `landing (0.29)` but marked `needsSmart: true`. The alternate is `legal (0.40)`. In reality this is a **Shopify storefront landing page** with a multi-tier Japanese-style nav. The heuristic stretched because the content section is mostly product cards.

**Stack inference (not extracted directly):**
- `utrecht-jp-stack-intel.json` returned an empty payload (no CMS / analytics / experimentation tools detected).
- However, the keyframe names `shopify-rotator`, `shopify-dash`, `acceleratedCheckoutLoadingSkeleton` and asset paths under `cdn/shop/t/1/assets/` in `seo.json` confirm a Shopify storefront. This is an **inference**, not extracted as a stack signal.

**Review-chrome deviations (documented up front):**
- The source has only one effective type size (14px). The review's H1/H2 sizes (32–88px) are review-page navigability decisions, not source tokens. Utrecht's actual page renders everything at 14px.
- Subtle gray panel tints common in design system reviews are NOT used here — Utrecht's chrome is built on hairline-border separation only, and the review respects this commitment.

---

## 2. Voice

| Property | Value |
|---|---|
| Tone | friendly |
| Pronoun posture | third-person |
| Heading case | Sentence case |
| Heading length class | tight |
| Total buttons (detected) | 1 |
| Total headings (detected) | 2 |
| Bilingual | Yes — every heading pairs JP / EN |

### Sample headings (all detected)

| Text | Source section |
|---|---|
| おすすめ / Recommend | content section (main) |
| 再入荷商品 / Restock | content sub-heading |

### CTA verbs — complete table

| Verb | Count |
|---|---|
| submit | 1 |

That's the entire detected list. Almost every other interaction is a styled link with a literal label rather than a verb CTA.

### Button labels — complete table

| Label | Count |
|---|---|
| submit | 1 |

---

## 3. Colors

### 3a. Brand

| Role | Hex | HSL | Usage |
|---|---|---|---|
| Primary | `#db0000` | hsl(0, 100%, 43%) | 836 — text + border + background combined |

No secondary, no accent variant in `design-tokens.json`. Just one chromatic value carrying everything.

### 3b. Semantic tokens (from `*-variables.css`)

#### Surface (`--color-bg*`)

| Token | Hex | Role |
|---|---|---|
| `--color-bg` | #ffffff | Page background (245 uses) |
| `--color-bg-1` | #db0000 | Full-bleed red surface (footer band, CTA buttons) |

#### Neutrals (`--color-neutral-*`)

| Token | Hex | HSL | Usage |
|---|---|---|---|
| `--color-neutral-50` | #000000 | hsl(0, 0%, 0%) | 299 uses |
| `--color-neutral-100` | #ffffff | hsl(0, 0%, 100%) | 245 uses |
| `--color-neutral-200` | #808080 | hsl(0, 0%, 50%) | 20 uses |

(Note: only 3 neutrals — the smallest neutral ramp in this skill's extraction history. Datadog had 10, Claude had 10, Excalidraw had 6. Utrecht has 3 distinct neutrals.)

#### Text (`--color-text-*`)

| Token | Hex | Role |
|---|---|---|
| `--color-text` | #000000 | Body, headings — primary ink |
| `--color-text-1` | #db0000 | Links, brand emphasis (reuses primary) |
| `--color-text-2` | #808080 | Muted captions, metadata |
| `--color-text-3` | #ffffff | Reversed-out text on the red footer |

#### Status (`--success`, `--warning`, `--error`, `--info`)

The variables file declares all four but they serialize as `[object Object]` — the extractor could not read the values. **Treat status tokens as absent.** In practice the brand red likely doubles as the error / warning indicator and there are no dedicated success / info hues.

### 3c. Tailwind / framework palette

**None present.** `library.json` reports `unknown` with `tailwindLike: 0.056` — essentially no Tailwind utility class density. The Tailwind config emitted by designlang (`utrecht-jp-tailwind.config.js`) is a downstream artifact, not evidence of source-side Tailwind use.

### 3d. Framework-specific tokens

**None present.** No `--fd-*` (Fumadocs), `--shiki-*`, `--prism-*`, `--bs-*`, `--cds-*`, or `--ant-*` namespaces detected.

### 3e. Full color inventory (DOM usage)

| Hex | Contexts | Count |
|---|---|---|
| `#db0000` | text, border, background | 836 |
| `#000000` | text, border, background | 299 |
| `#ffffff` | background, text, border | 245 |
| `#808080` | text, border | 20 |

Total unique colors detected in the DOM: **4**. This is the smallest color count this skill has ever seen.

### 3f. Gradients

**None detected.** `gradientCount: 0`, `gradientTotals: { radial: 0, linear: 0 }`. The system uses no gradients.

---

## 4. Typography

### Families

| Family | Usage Count | Variable | Notes |
|---|---|---|---|
| GT America Standard | 536 | `--font-sans` | Primary face. Grilli Type commercial release. |
| Times | 145 | `--font-body` (#1) | Fallback artifact. |
| Arial | 4 | `--font-body` (#2) | Fallback artifact. |
| GTStandard-M | 2 | `--font-body` (#3) | Alternate weight of GT America, loaded as a separate family. |

**GT America Standard is proprietary** (Grilli Type, commercial license). This review falls back to **Inter** via Google Fonts. Sizes (14px) and weights (400, 700) are preserved.

**Font fallback in this review:**
- `--font-sans` → Inter (Google)
- Japanese text → Noto Sans JP (Google)
- Mono → JetBrains Mono (Google)

### Full type scale

| Size (px) | Size (rem) | Weight | Line Height | Letter Spacing | Used On |
|---|---|---|---|---|---|
| 14 | 0.875 | 400 | 14 | normal | html, head, meta, link, body, h1 |
| 13.3333 | 0.8333 | 400 | normal | normal | input |

Two sizes. Body and H1 are the same size. **The system has no display type tier.**

### Heading scale (from `design-language.md`)

```css
h1 { font-size: 14px; font-weight: 400; line-height: 14px; }
```

That's it. H2, H3, etc. were not detected as distinct sizes — they may exist in CSS but render at the body size on this page.

### Weights detected

| Weight | Usage Count |
|---|---|
| 400 | 647 — regular dominant |
| 700 | 40 — bold for emphasis |

### Letter-spacing

`normal` across all detected sizes. No `--tracking-*` tokens.

### Line-heights

`14px` on the body / h1 / link (literal 1:1 with size — extremely tight) and `normal` (browser default ~1.2) on input.

### Detected page headings

| Tag | Text | Size/Weight | Section |
|---|---|---|---|
| h1 | (no explicit heading — page title via `<title>` and og:title) | 14 / 400 | nav |
| h? | おすすめ / Recommend | 14 / 400 | content (main) |
| h? | 再入荷商品 / Restock | 14 / 400 | content sub |

---

## 5. Spacing

**Base unit:** designlang reports **no consistent base unit** detected. Values are arbitrary.

| Token | Value | Rem |
|---|---|---|
| `--spacing-4` | 4px | 0.25rem |
| `--spacing-29` | 29px | 1.8125rem |
| `--spacing-58` | 58px | 3.625rem |
| `--spacing-76` | 76px | 4.75rem |
| `--spacing-88` | 88px | 5.5rem |
| `--spacing-114` | 114px | 7.125rem |
| `--spacing-131` | 131px | 8.1875rem |
| `--spacing-158` | 158px | 9.875rem |
| `--spacing-233` | 233px | 14.5625rem |
| `--spacing-345` | 345px | 21.5625rem |
| `--spacing-497` | 497px | 31.0625rem |

11 values. The DESIGN.md summary surfaces "scale: [4, 29, 58, 76, 88, 114, 131, 158, 233, 345]" (10 values) but `variables.css` actually has 11 (the `497px` value is also declared). Documented here.

**Container widths:** none extracted. No `--container-*` tokens emitted.

---

## 6. Layout

**Layout primitives:** 0 grid containers, 29 flex containers.

**Flex direction breakdown:**
- row/nowrap: 6
- row/wrap: 21
- row-reverse/wrap: 2

**Breakpoints** (parsed from `design-language.md`; designlang serialized as `[object Object]` in the intent file):

| Name | Value | Type |
|---|---|---|
| xs | 374px | max-width |
| — | 413px | max-width |
| sm | 479px | max-width |
| md | 750px | max-width |
| md | 767px | max-width |
| lg | 1023px | max-width |
| xl | 1280px | max-width |
| — | 1700px | min-width |

8 breakpoints across the responsive matrix.

### Reading order

```
nav → nav → nav → nav → nav → content → footer → nav
```

| Index | Tag | Role | Confidence | Heading | Buttons | Cards | needsSmart |
|---|---|---|---|---|---|---|---|
| 0 | `<header>` | nav | 0.40 | — | 0 | 0 | yes |
| 1 | `<nav>` | nav | 0.90 | — | 0 | 0 | no |
| 2 | `<nav>` | nav | 0.90 | — | 0 | 0 | no |
| 3 | `<nav>` | nav | 0.90 | — | 0 | 0 | no |
| 4 | `<nav>` | nav | 0.90 | — | 0 | 0 | no |
| 5 | `<main>` | content | 0.30 | おすすめ / Recommend | 0 | 0 | yes |
| 6 | `<footer>` | footer | 0.95 | — | 0 | 0 | no |
| 7 | `<nav>` | nav | 0.90 | — | 0 | 0 | no |

### Section role tally

| Role | Count |
|---|---|
| nav | 6 |
| content | 1 |
| footer | 1 |

The 6 nav classifications cover: (1) outer header wrapper, (2–4) three primary menu rows (utility / news / shop), (5) login row, (6) the trailing newsletter form block.

---

## 7. Shape

### Radius scale

**Empty** — `design-tokens.json` `primitive.radius: {}`.

| Label | Value | Count |
|---|---|---|
| — | — | 0 |

Every component renders with `border-radius: 0`. The buttons, inputs, cards, modals — all sharp-cornered.

### Pill use

`hasPill: false`. No 999px radii anywhere.

### Avg / max

- Avg radius: 0px
- Max radius: 0px

---

## 8. Elevation

### Shadow scale

**Empty** — `design-tokens.json` `primitive.shadow: {}`.

| Token | Value |
|---|---|
| — | — |

Zero shadow tokens detected in the entire CSS surface. The material confidence (0.55 flat) is driven entirely by this absence.

### Z-index layers

8 unique values across 2 conceptual layers:

| Layer | Range | Elements |
|---|---|---|
| sticky | 10–12 | nav, js-modal |
| base | −100 to 9 | div, image-container, lozad-bg |

### Shadow profile classification

**None.** Avg blur 0px, max blur 0px, 0 inset shadows.

---

## 9. Motion

### Durations

| Token | Value |
|---|---|
| `lg` | 600ms |

A single duration token. No xs / sm / md detected.

### Easings

| Token | Value | Family |
|---|---|---|
| `linear` | linear | linear |
| `ease-out-5` | cubic-bezier(0.19, 1, 0.22, 1) | ease-out (expo-out) |

### Springs

None detected.

### Feel

**mechanical** (scroll-linked: yes).

### Detected transitions

```css
transition: all;
transition: linear;
transition: background-color 0.6s cubic-bezier(0.19, 1, 0.22, 1);
transition: transform 0.6s, -webkit-transform 0.6s;
transition: visibility linear, opacity 0.5s;
```

### Keyframes detected (3 named animations)

```css
@keyframes shopify-rotator { 0% { transform: rotate(0deg); } 100% { transform: rotate(270deg); } }
@keyframes shopify-dash    { 0% { stroke-dashoffset: 280; } 50% { stroke-dashoffset: 75; transform: rotate(135deg); } 100% { stroke-dashoffset: 280; transform: rotate(450deg); } }
@keyframes acceleratedCheckoutLoadingSkeleton {
  50%  { opacity: var(--shopify-accelerated-checkout-skeleton-animation-opacity-start, 1); }
  75%  { opacity: var(--shopify-accelerated-checkout-skeleton-animation-opacity-end, .5); }
  100% { opacity: var(--shopify-accelerated-checkout-skeleton-animation-opacity-start, 1); }
}
```

All three are Shopify defaults. Confirms the storefront platform.

---

## 10. Components

### Detected patterns (6)

`buttons` · `inputs` · `links` · `navigation` · `footer` · `modals`

### Anatomy (from `anatomy.tsx`)

| Kind | Variants | Sizes | Instances |
|---|---|---|---|
| button | default | md (inferred) | 1 in cluster data, 16 total reported in DESIGN summary |

Designlang's anatomy stub matches one variant. The component-clusters block in `design-language.md` enumerates 1 button cluster with 1 variant: red bg, white text, 0 radius, GT America 14/400.

### Detected pattern styles (from `design-language.md`)

#### Buttons (2 instances)
```css
background-color: rgb(219, 0, 0);
color: rgb(255, 255, 255);
font-size: 14px;
font-weight: 400;
border-radius: 0px;
```

#### Inputs (6 instances)
```css
background-color: rgb(255, 255, 255);
color: rgb(0, 0, 0);
border-color: rgb(0, 0, 0);
border-radius: 0px;
font-size: 13.3333px;
```

#### Links (94 instances)
```css
color: rgb(219, 0, 0);
font-size: 14px;
font-weight: 400;
```

#### Navigation (34 instances)
```css
background-color: rgb(255, 255, 255);
color: rgb(219, 0, 0);
padding: 0;
position: static;
```

#### Footer (6 instances)
```css
background-color: rgb(219, 0, 0);
color: rgb(255, 255, 255);
font-size: 14px;
```

#### Modals (13 instances)
```css
background-color: rgb(255, 255, 255);
border-radius: 0px;
padding: 0;
```

### Patterns NOT detected

`cards`, `badges`, `tabs`, `tooltips`, `dropdowns`, `accordions`, `switches`, `toasts`, `popovers`, `breadcrumbs`. Utrecht's surface is intentionally lean — text-driven, with structural separation by layout not by surface variants.

---

## 11. Icons

### Library

**unknown** (confidence 0). No Lucide, Heroicons, Phosphor, Tabler, Feather match.

### Stats

| Metric | Value |
|---|---|
| Total | 2 |
| Stroke-only | 0 |
| Fill-only | 2 |
| Mixed | 0 |
| Avg stroke width | 0 (no strokes) |
| Grid distribution | (none — no consistent grid detected) |
| Rounded-caps fraction | 0% |
| Size class | xl (both) |
| Colors | rgb(219, 0, 0), rgb(255, 255, 255) |

### Signals

`fillDominant`. The 2 detected icons are bespoke fills, likely the logo mark and a single decorative glyph.

### Detected icons (full list)

| # | Class | Grid | Stroke | Style |
|---|---|---|---|---|
| 1 | (empty) | null | null | fill |
| 2 | (empty) | null | null | fill |

---

## 12. Forms & inputs

### Detected forms

`form-states.json` reports a small payload (302 bytes). The only enumerated CTA verb is "submit" (1 use), and inputs were detected at 6 instances.

### Input types

`text`, `email` (inferred — Shopify newsletter signup).

### Modals

13 instances detected — these are likely Shopify product / cart / search modals.

### Toast / spinner / skeleton

The `acceleratedCheckoutLoadingSkeleton` keyframe is present (Shopify checkout) but no toast pattern was matched.

### Loading states

`shopify-rotator` + `shopify-dash` together form Shopify's standard loading spinner.

---

## 13. Accessibility

### WCAG score

**100%** — 1 passing pair, 0 failing pairs across 687 elements analyzed.

### Color-pair details

The extractor's a11y output enumerated only the one bilingual pair (`#ffffff` on `#db0000`). The full set of likely pairs (computed manually for this reference):

| FG | BG | Contrast | WCAG |
|---|---|---|---|
| `#ffffff` | `#db0000` | 5.23:1 | AA (extractor-reported) |
| `#000000` | `#ffffff` | 21.0:1 | AAA |
| `#db0000` | `#ffffff` | 5.23:1 | AA |
| `#808080` | `#ffffff` | 3.95:1 | AA-lg (large text only) |
| `#000000` | `#db0000` | ≈ 4.01:1 | AA-lg |

The muted gray on white (#808080 on #ffffff) only clears AA for large text — small body copy in that color would fail. Worth flagging if the gray is used for body-size captions.

---

## 14. SEO & brand surface

### Favicons

| Rel | Size | Type | URL |
|---|---|---|---|
| apple-touch-icon | 180×180 | — | `utrecht.jp/cdn/shop/t/1/assets/apple-touch-icon.png` |
| icon | 32×32 | image/png | `utrecht.jp/cdn/shop/t/1/assets/favicon-32x32.png` |
| icon | 16×16 | image/png | `utrecht.jp/cdn/shop/t/1/assets/favicon-16x16.png` |

All hosted on `cdn/shop/t/1/assets/` — Shopify's CDN path.

### OG / social

| Property | Value |
|---|---|
| og:site_name | Utrecht |
| og:url | https://utrecht.jp/ |
| og:title | ユトレヒト / Utrecht |
| og:type | website |
| og:image | `utrecht.jp/cdn/shop/t/1/assets/og.png` |
| og:image:secure_url | `https://utrecht.jp/cdn/shop/t/1/assets/og.png` |
| twitter:card | summary_large_image |
| twitter:title | ユトレヒト / Utrecht |

### Meta

| Property | Value |
|---|---|
| description | (full JP+EN bilingual paragraph — see §1 above) |
| canonical | null (missing) |
| themeColor | `#ffffff` |
| viewport | `width=device-width, initial-scale=1.0, height=device-height, minimum-scale=1.0, user-scalable=0` |
| manifest | `cdn/shop/t/1/assets/site.webmanifest` |

### Structured data

**None.** `structuredData: []`.

### SEO score

| Check | Status |
|---|---|
| hasOg | ✓ |
| hasTwitter | ✓ |
| hasDescription | ✓ |
| hasCanonical | ✗ (missing) |
| hasStructuredData | ✗ (missing) |
| hasFavicon | ✓ |
| hasThemeColor | ✓ |

### Fallback documentation

| Gap | Fallback used in this review |
|---|---|
| GT America Standard is proprietary (Grilli Type commercial license) | **Inter** (Google Fonts) for Latin, **Noto Sans JP** for Japanese. 14px/14px line-height preserved. |
| Status tokens declared in CSS but serialize as `[object Object]` | Documented as absent. The review's accent (red) doubles where a status color might appear. |
| No detected H2/H3 sizes (everything renders at 14px) | Review chrome uses 32–88px for navigability — flagged as a deliberate deviation in §1 and the typography section. |
| No native dark theme | Dark mode constructed by inverting the 4 detected colors. Link color shifts from `#db0000` → `#ff3030` for legibility on the dark background. |
| Library detection `unknown` | The Shopify stack is inferred from keyframe names and asset paths (see §1). |
| No `--container-*` tokens | Container widths not surfaced. |

---

## 15. Audit findings

### Do's (from `*-design-language.md`)

1. Use `submit` as the primary verb in CTAs.
2. Write headings in **Sentence case**, **tight** length.
3. Address the reader with the pronoun posture **third-person** (typical of Japanese commercial copy).
4. Stay inside the **flat** material — match the no-shadow, no-radius habits.

### Don'ts (with severity inferred from counts)

| Severity | Issue | Count | Note |
|---|---|---|---|
| Medium | 4 font families | 4 | Times, Arial, GTStandard-M are likely fallback artifacts. Consolidate to 2 (GT America + one fallback). |
| **High** | No consistent spacing base unit | — | Values 4 / 29 / 58 / 76 / 88 / 114 / 131 / 158 / 233 / 345 / 497 are arbitrary. Editorial authoring style rather than tokenized. |
| Medium | 34 `!important` rules | 34 | Below 100 — manageable. Common in Shopify themes. |
| Medium | 87% CSS unused | — | Purge step (Shopify theme cleanup) recommended. |
| High | 1,774 duplicate CSS declarations | 1,774 | Multiple stylesheet entry points emitting overlapping rules. Bundler-level dedupe recommended. |

### Strengths

| Strength | Evidence |
|---|---|
| Tight color palette | 4 colors. Color discipline 100/100. |
| Consistent border radii | 0 radius tokens, 0 detected radius uses. Radius discipline 100/100. |
| Clean elevation system | 0 shadows. Shadow consistency 85/100 (slightly penalized for the absence). |
| Strong accessibility | 1/1 passing pair, WCAG 100%. |
| Single primary face | GT America covers 99% of detected type usage. |
| Bilingual rigor | Every heading pairs JP / EN — a content-system decision rather than a CSS one. |

### Design Score

**74 / 100 (Grade: C)** — 5 issues.

Category breakdown:

| Category | Score |
|---|---|
| Color Discipline | 100/100 |
| Typography Consistency | 50/100 (penalty for 4 fonts) |
| Spacing System | 55/100 (penalty for arbitrary scale) |
| Shadow Consistency | 85/100 |
| Border Radius Consistency | 100/100 |
| Accessibility | 100/100 |
| CSS Tokenization | 50/100 (only 4 declared CSS vars in source) |

---

## 16. Frameworks & integrations

### Detected library

**unknown** — Tailwind-like density 0.056 (essentially zero), Radix attribute count 0, class sample size 132. The styling is hand-authored CSS / a Shopify theme without a recognized utility framework.

### Stack intel

`stack-intel.json` returned empty arrays for `cms`, `analytics`, `experimentation`. Only signal counts (scriptCount: 10, metaCount: 17). **Inferred stack: Shopify** based on:
- Keyframe names `shopify-rotator`, `shopify-dash`, `acceleratedCheckoutLoadingSkeleton`
- CDN asset paths `cdn/shop/t/1/assets/`
- Manifest at `cdn/shop/t/1/assets/site.webmanifest`

### LLM-companion artifacts

`utrecht-jp-mcp.json` (6.2 KB) provides an MCP companion. `utrecht-jp-prompts/` directory contains LLM prompts (count not enumerated here — inspect directly).

---

## 17. Generated artifacts

| File | Purpose |
|---|---|
| `utrecht-design-system.html` | **Primary visual review** — curated, brutalist self-styled with extracted tokens |
| `DESIGN.md` | **Comprehensive reference** (this file) |
| `utrecht-jp-DESIGN.md` | designlang's short auto-generated summary (kept) |
| `utrecht-jp-design-language.md` | Full extraction markdown (10.1 KB) |
| `utrecht-jp-design-tokens.json` | DTCG v1 design tokens (3.4 KB) |
| `utrecht-jp-variables.css` | CSS custom properties (1.1 KB — only 26 vars total in source) |
| `utrecht-jp-figma-variables.json` | Figma variable import format |
| `utrecht-jp-intent.json` | Page intent + section roles |
| `utrecht-jp-voice.json` | Voice / tone / CTA verbs |
| `utrecht-jp-visual-dna.json` | Material / imagery / patterns |
| `utrecht-jp-icon-system.json` | 2 detected icons + attributes |
| `utrecht-jp-motion-tokens.json` | Duration + easing |
| `utrecht-jp-library.json` | Library detection (unknown) |
| `utrecht-jp-form-states.json` | Forms + states |
| `utrecht-jp-mcp.json` | MCP companion |
| `utrecht-jp-seo.json` | SEO + structured data |
| `utrecht-jp-stack-intel.json` | Stack intel (empty payload) |
| `utrecht-jp-screenshots.json` | Screenshot index |
| `utrecht-jp-logo.json` | Logo metadata |
| `utrecht-jp-logo.svg` | Detected logo |
| `utrecht-jp-tailwind.config.js` | Tailwind config emission |
| `utrecht-jp-theme.js` | React theme |
| `utrecht-jp-shadcn-theme.css` | shadcn/ui theme |
| `utrecht-jp-wordpress-theme.json` | WordPress theme |
| `utrecht-jp-preview.html` | Auto-generated basic preview (untouched) |
| `utrecht-jp-prompts/` | LLM prompts directory |
| `screenshots/full-page.png` | Full-page screenshot |
| `screenshots/nav-0.png`, `nav-1.png` | Component screenshots |

---

_Compiled 2026-05-14 from designlang v12.10.0 extraction. Source: `https://utrecht.jp/`. Companion to `utrecht-design-system.html`. All inferences (Shopify stack, font fallback choices, computed contrast pairs, deviated review-chrome sizing) are flagged inline at point of mention rather than split into a separate CHANGELOG._

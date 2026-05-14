---
site: Ableton
url: https://www.ableton.com/
extracted_at: 2026-05-14
generator: designlang v12.10.0
elements_analyzed: 668
intent: landing (0.31, low confidence)
library: unknown (no shadcn/Radix/Tailwind signals)
material: flat (0.55) · 0 shadows · 0 radii
imagery: photography (0.219) · 7 photo-like images out of 16
voice: friendly · third-person · Title Case · balanced
design_score: 86/100 (B) · 3 issues
---

# Ableton Design System (corp site)

> "Creative tools for music makers." — page title

A **disciplined three-axis brutalist system**: black ink, Ableton blue (`#0000ff`), and a salmon-pink pop accent — used sparingly. No gradients, no shadows, no radii, no chromatic surfaces. Score: 100/100 for color discipline.

## Confidence summary

| Detection | Confidence | Notes |
|---|---|---|
| Intent (landing) | 0.31 | **Weak** — the homepage is so editorial it scans more like a magazine than a landing page |
| Library | 0.00 | **Unknown** — no shadcn, Radix, or Tailwind signals. Likely custom CSS |
| Material (flat) | 0.55 | Medium — supported by "0 shadows + 0 radii" but saturation 0.437 |
| Imagery (photography) | 0.22 | Weak. Alternates: icon-only |
| WCAG | 100% | Strong — all detected pairs pass AAA |

---

# 1. Overview

A disciplined editorial homepage for a music-software company. The visual language commits hard to:

- **Zero shadows.** The entire surface system is flat color blocks.
- **Zero radii.** Every corner is 90°. This is a brand signature.
- **Three-axis palette.** Black, white, and Ableton blue (#0000ff) carry the entire system. Salmon-pink and teal appear as pop accents.
- **Title-case Futura.** futura-pt PT does 92% of all type duty.
- **Third-person friendly voice.** Sentences describe rather than address the reader.

The detected page intent is "landing" but with very weak confidence (0.31) — the page reads more like a content portal (latest news, downloads, tutorials) than a marketing landing. This is consistent with Ableton's brand positioning as a community / editorial destination, not a sales funnel.

---

# 2. Voice

| Aspect | Value |
|---|---|
| **Tone** | friendly |
| **Pronoun posture** | third-person |
| **Heading style** | Title Case |
| **Heading length** | balanced |
| **Buttons detected** | 4 |
| **Headings detected** | 27 |

## Sample headings (all detected)

> *"More on Ableton.com:"* — appears 3× (navigation header pattern)
> *"More from Ableton:"* — appears 3× (related-content blocks)
> *"Live 12.4 is out now – with Link Audio, updated devices and more"* — feature announcement
> *"The latest from Ableton"* — section heading
> *"View posts in category: Downloads"* — taxonomy header
> *"Download the Live Set of Artefakt's New Track 'Undertow'"* — editorial post title

Repeated noun across editorial headings: **"Ableton"** itself. No single product noun dominates — fitting for a multi-product company whose homepage is a portal.

## CTA verbs (all detected)

| Verb | Count |
|---|---|
| more | 2 |
| close | 1 |
| accept | 1 |

The CTA vocabulary is **strikingly small** — only 4 CTAs total across 27 headings. This reinforces the editorial-portal feel: the page is for reading, not converting.

## Button labels (all detected)

| Label | Count |
|---|---|
| More | 1 |
| More info | 1 |
| Close | 1 |
| Accept | 1 |

The cookie banner accounts for half of all buttons. The page itself has 2 product CTAs.

---

# 3. Colors

## 3a. Brand

| Hex | Role | Uses | Description |
|---|---|---|---|
| `#0000ff` | secondary | 42 | **The dominant chromatic.** Pure RGB blue — Ableton's iconic link & emphasis color. |
| `#ff8389` | primary | 2 | Salmon pink — used very sparingly as a vibrant pop accent. |
| `#00d2be` | accent | 1 | Teal — tertiary accent, used minimally. |

The fact that `#0000ff` (literally `blue`) is used 21× more than the nominal "primary" is telling. Ableton's de-facto brand color is blue. The salmon and teal are reserved for occasional contrast moments.

## 3b. Semantic role tokens (from variables.css)

Ableton's `variables.css` is intentionally sparse — only 13 custom properties. The role separation is minimal:

### Background

| Token | Hex | Role |
|---|---|---|
| `--color-bg` | `#f3f3f3` | Page background (warm light grey) |
| `--color-bg-1` | `#ffffff` | Card / panel surface |
| `--color-bg-2` | `#eeeeee` | Sunken / divider zones |
| `--color-bg-3` | `#000000` | Inverted dark surface (footer, hero overlays) |

### Text

| Token | Hex | Role |
|---|---|---|
| `--color-text` | `#000000` | Primary text |
| `--color-text-1` | `#ffffff` | Text on dark surface (inverted) |
| `--color-text-2` | `#0000ff` | Link / accent text |
| `--color-text-3` | `#6dcbff` | Secondary link / on-dark accent (sky blue) |

### Neutrals (numbered scale)

| Token | Hex |
|---|---|
| `--color-neutral-50` | `#000000` |
| `--color-neutral-100` | `#ffffff` |
| `--color-neutral-200` | `#eeeeee` |

**Notably absent:** No `--surface-*`, `--line-*`, `--border-*`, `--callout-*`, `--shadow-*`, `--radius-*`, or status tokens. The system relies on raw color usage and the absence of borders/shadows for hierarchy.

## 3c. Tailwind palette

**Not detected.** No `--color-{slate,gray,blue,red,green,yellow,...}-{50..900}` tokens in `variables.css`. Tailwind class density is 5.8% — well below the 30% threshold. Ableton ships custom hand-written CSS.

## 3d. Framework-specific vars

**None detected.** No fumadocs, shiki, prism, or other framework tokens.

## 3e. Full color inventory (every detected hex)

Only **7 unique colors** across 668 elements — a remarkably tight palette.

| Hex | Roles | DOM uses | Notes |
|---|---|---|---|
| `#000000` | text, surface, border | dominant | Primary ink, also used for inverted surfaces |
| `#ffffff` | text, surface | high | Card surface, text on dark |
| `#f3f3f3` | background | high | Page background — warm rather than pure white |
| `#eeeeee` | surface, divider | medium | Sunken zones |
| `#0000ff` | link, accent | 42 | The only saturated color with meaningful presence |
| `#ff8389` | accent | 2 | Salmon pop |
| `#00d2be` | accent | 1 | Teal pop |
| `#6dcbff` | text | — | Sky blue, defined as `--color-text-3` but barely used in DOM |

## 3f. Gradients

**Zero gradients detected.** `gradientCount: 0` in `visual-dna.json`. Every surface is solid color. This is unusual for a 2020s marketing site — most sites have at least decorative hero gradients.

---

# 4. Typography

## 4a. Font families (all detected)

| Family | Uses | Coverage | Notes |
|---|---|---|---|
| **futura-pt** | 614 | 92% | Display + body. Licensed via Adobe Fonts / Typekit. |
| **Times** | 50 | 7% | Editorial italic — used for blog post bylines and emphasis. |
| **Arial** | 4 | <1% | Likely a system-font fallback that crept in. |

Audit recommendation: **3 families exceeds the suggested ceiling of 2.** Arial appears only 4 times and is probably an inherited fallback — removing it would tighten the system without visible impact.

## 4b. Font fallback chains

```css
--font-sans: 'futura-pt', sans-serif;
--font-body: 'Times', sans-serif;     /* unusual pairing — Times falls back to sans-serif */
--font-font-2: 'Arial', sans-serif;
```

The `--font-body` chain is curious: Times → sans-serif. If futura-pt fails to load, body text becomes a sans serif rather than the named Times.

## 4c. Type scale (full)

| Size | Weight | Line-height | Letter-spacing | Family | Detected role |
|---|---|---|---|---|---|
| **90px** | 700 | 90px (1.0) | — | futura-pt | H1 (hero display) |
| **40px** | 700 | 48px (1.2) | — | futura-pt | H2 |
| **30px** | 700 | 42px (1.4) | — | futura-pt | H3 |
| **24px** | — | — | — | futura-pt | Subhead |
| **20px** | 700 | 30px (1.5) | — | futura-pt | H4 / body |
| **16px** | 400 | — | — | futura-pt | Body |
| **14px** | 400 | — | — | futura-pt | Caption |
| **13.3333px** | 400 | — | — | futura-pt | Legal / fine print (likely 0.833rem at 16px root) |

**All headings are weight 700.** No 500 or 600 mid-weights detected. Ableton commits to a stark bold/regular split.

## 4d. Detected weights

`400`, `700`. Only two weights across the entire system. (For comparison: Langfuse used 400, 500, 600, 700.)

## 4e. Line-heights

| Value | Used at |
|---|---|
| `90px` (1.0×) | H1 (perfectly tight) |
| `48px` (1.2×) | H2 |
| `42px` (1.4×) | H3 |
| `30px` (1.5×) | Body (20px base) |

## 4f. Letter-spacing

No `--tracking-*` variables in `variables.css`. No explicit tracking adjustments — typography relies on Futura's native metrics.

## 4g. All headings rendered on the page

27 headings total. Top patterns:
- Section navigation: *"More on Ableton.com:"* / *"More from Ableton:"* (each appears 3×)
- Editorial titles: post headlines, video titles
- Section labels: *"The latest from Ableton"*, *"Tutorial videos"*, *"Free downloads"*

---

# 5. Spacing

## 5a. Scale

| Token | Value | Notes |
|---|---|---|
| `--spacing-1` | 1px | Hairline (borders) |
| `--spacing-27` | 27px | **No standard 4/8/12/16/20/24 steps** |
| `--spacing-30` | 30px | |
| `--spacing-40` | 40px | |
| `--spacing-50` | 50px | |
| `--spacing-53` | 53px | |
| `--spacing-60` | 60px | |
| `--spacing-107` | 107px | |
| `--spacing-140` | 140px | |
| `--spacing-180` | 180px | Section gap |

**Base:** 2px (not the standard 4px / 8px). This is unusual and suggests spacing is hand-tuned rather than systematic.

**Notable absences:** No small-step tokens (4, 8, 12, 16, 20, 24). Chrome spacing is presumably handled with raw values or non-tokenized rules.

## 5b. Container widths

Not detected as named tokens. Likely uses raw `max-width` values.

---

# 6. Layout

## 6a. Primitives

| Type | Count |
|---|---|
| Grid containers | **1** |
| Flex containers | 9 |

A single grid container is striking — the homepage layout is overwhelmingly flex-based.

## 6b. Breakpoints

**18 breakpoints detected** but their values are broken in designlang's output (renders as `[object Object]px`). The actual breakpoint values would need to be parsed from `variables.css` `--breakpoint-*` tokens, but no `--breakpoint-*` tokens are exported.

## 6c. Reading order

Detected section flow (from `intent.json`):

| # | Tag | Role | Confidence | Heading |
|---|---|---|---|---|
| 0 | header | nav | 0.40 | "More on Ableton.com:" |
| 1 | nav | nav | 0.90 | (same) |
| 2 | main | content | 0.30 | (same) |
| 3 | section | feature-grid | 0.80 | "More from Ableton:" |
| 4 | section | pricing | 0.40 | "Live 12.4 is out now…" |
| 5 | section | content | 0.30 | "The latest from Ableton" |
| 6 | section | content | 0.30 | "Tutorial videos" |
| 7 | section | pricing | 0.40 | "Free downloads" |
| 8 | section | content | 0.30 | — |
| 9 | footer | footer | 0.95 | "Education" |

⚠ **False positives:** sections 4 and 7 were classified as "pricing" but they're actually a release announcement and a downloads catalog. The "pricing" heuristic appears to be over-firing on dense card grids.

## 6d. Section role tally

`nav: 2 · content: 4 · feature-grid: 1 · pricing: 2 · footer: 1`

The page is content-heavy (4 content sections) with no detected hero, testimonial, or FAQ.

---

# 7. Shape

## 7a. Radii

**Zero radii detected.** `--radius-*` tokens absent. `avgRadius: 0`, `maxRadius: 0`.

Ableton commits totally to 90° corners. Every button, every card, every image — square. This is a brand signature and a rare commitment.

## 7b. Pill use

`hasPill: false`. No 999px elements detected.

---

# 8. Elevation

**Zero shadow tokens detected.** Flat material commitment is complete.

| Metric | Value |
|---|---|
| Shadow tokens | 0 |
| Avg shadow blur | 0 |
| Max shadow blur | 0 |
| Inset shadows | 0 |
| Shadow profile | `none` |
| Z-index layers | 5 |

Five z-index layers exist (likely modal, header, content, base, behind) but there are no detectable shadow boundaries between surfaces — separation is achieved purely through color contrast.

---

# 9. Motion

## 9a. Duration tokens

| Token | Value |
|---|---|
| xs | 150ms |
| md | 350ms |

No `sm`, `lg`, or `xl` durations. Two-tier motion.

## 9b. Easing

**No easing tokens explicitly extracted.** Likely uses CSS defaults.

## 9c. Springs

None detected.

## 9d. Meta

| Property | Value |
|---|---|
| Feel | mixed |
| Scroll-linked animations | **yes** |

Ableton uses scroll-linked animations (parallax, fade-in-on-scroll) but the motion vocabulary is restrained — only two durations.

## 9e. Named keyframes

Not surfaced by designlang. Manual inspection would be needed.

---

# 10. Components

## 10a. Detected patterns (all 7)

- **buttons** (anatomy data: 11 instances, 2 variants — outline, primary)
- **inputs**
- **links**
- **navigation**
- **footer**
- **modals**
- **badges**

## 10b. Anatomy

### Button

| Variant | Instances |
|---|---|
| outline | (mixed) |
| primary | (mixed) |
| **Total** | **11** |

No sizes detected — buttons are likely a single size.

### Other patterns

Inputs, links, navigation, footer, modals, badges are detected but **not anatomized**. No variant or size data.

## 10c. Cards (implicit)

Cards aren't in the detected-patterns list, but the homepage is clearly card-driven (post tiles, artist tiles, pack tiles). They're not being detected as a distinct component, possibly because they don't have a unifying class structure.

---

# 11. Icons

## 11a. Library

| Property | Value |
|---|---|
| Detected library | **unknown** (0.00 confidence) |
| Total icons | 7 |
| Stroke-only | 0 |
| Fill-only | 3 |
| Mixed | 4 |
| Avg stroke width | 0 (fill-based) |
| Dominant grid | **48px** |
| Rounded caps fraction | 0 |

Ableton uses **fill-based 48px icons** — unusual. Most modern systems use stroke icons on a 24px grid (Lucide / Heroicons style). Ableton's icons are likely custom SVGs.

## 11b. Named icons

| Class | Grid | Style |
|---|---|---|
| `main-nav__logo__image` | — | fill (the brand mark) |
| `abl-mix-blend-difference` | 48 | fill |
| (5 unnamed) | 48 | mixed |

The named icons follow a BEM-style naming pattern (`main-nav__logo__image`, `abl-mix-blend-difference`) — this is hand-rolled custom CSS, not a third-party icon library.

---

# 12. Forms & inputs

| Property | Value |
|---|---|
| Forms detected | 1 |
| Form families | 1 |
| Input types | `input` (10), `select` (2) |
| Modals | 0 detected (despite being in "detected patterns" — likely a discovery vs render-state mismatch) |
| Toast libraries | none |
| Skeleton loaders | 0 |
| Spinners | 0 |
| Empty states | 0 |
| Error states | 0 |

The only form is likely the search box (10 inputs + 2 selects implies filter UI somewhere on the page).

---

# 13. Accessibility

| Property | Value |
|---|---|
| WCAG score | **100%** |
| Passing pairs | all |
| Failing pairs | 0 |

## Full pair table

Only 2 production text/background combinations were detected:

| FG | BG | Ratio | WCAG | Sample |
|---|---|---|---|---|
| `#000000` | `#ffffff` | **21.00:1** | AAA | Black on white |
| `#000000` | `#f3f3f3` | **18.64:1** | AAA | Black on warm grey page bg |

This is the natural consequence of Ableton's two-color text system: black text everywhere, on either white or `#f3f3f3`. Contrast is enormous.

The blue (#0000ff) link color would also need testing: 8.59:1 against white (AAA). Both confirmed safe.

---

# 14. SEO & brand surface

| Property | Value |
|---|---|
| OG tags | yes (type: website) |
| Twitter card | yes (`summary_large_image`, @Ableton) |
| Description | "Ableton makes software, hardware and other creative tools for a global community of music makers." |
| Canonical URL | not set |
| Theme color | not set |
| Viewport | `width=device-width,initial-scale=1` |
| Manifest | not set |
| Structured data | none |

## Favicons

| URL | Type | Sizes |
|---|---|---|
| `https://cdn-resources.ableton.com/.../static/images/favicon.f83afbda6c78.ico` | image/ico | default |

Just one `.ico` favicon — no 16/32/180 SVG/PNG variants. Minimal SEO surface for a major site.

## OG image

`https://cdn-resources.ableton.com/.../static/images/og-images/default.83939b540f40.jpg`

A single default OG image is used site-wide (no per-page customization detected).

---

# 15. Audit findings

## ⚠ Don'ts (3 detected)

| # | Finding | Severity | Detail |
|---|---|---|---|
| 1 | **418 `!important` rules** | **High** | Heavy reliance on `!important` overrides indicates extensive ad-hoc theming or legacy CSS layered on top. Prefer specificity. |
| 2 | **96% of CSS is unused** | **High** | A global stylesheet is served to all routes. Per-route purging or critical-CSS extraction would dramatically reduce render-blocking weight. |
| 3 | **13,778 duplicate CSS declarations** | **High** | Run output through a CSS deduplicator (cssnano, csso). Most duplicates are likely identical typography rules across cascade overrides. |

All three Don'ts are severity-high (>100 occurrences).

## ✓ Do's (4 strengths)

| # | Finding | Detail |
|---|---|---|
| 1 | **Use "more", "close", "accept" as primary CTA verbs** | These dominate the source vocabulary |
| 2 | **Title Case headings, balanced length** | Consistent voice across 27 headings |
| 3 | **Third-person pronoun posture** | Editorial/portal feel rather than direct address |
| 4 | **Stay inside flat material** | Match the shadow (0) and radius (0) habits |

## Bonus strengths (derived from extraction)

- **Color discipline: 100/100.** Only 7 unique colors across 668 elements. The single chromatic accent (`#0000ff`) carries 42 uses; everything else is monochrome.
- **Radius consistency: 100/100.** Zero rounded corners. The brutalist commitment is total.
- **Accessibility: 100%.** All detected pairs pass AAA at 18:1 or higher.
- **Spacing scale: 85/100.** Section-scale tokens (27 → 180px) are crisp.

---

# 16. Frameworks & integrations

## Library detection

| Aspect | Value |
|---|---|
| Detected library | **unknown** |
| Confidence | 0.00 |
| Evidence | (none) |
| Tailwind-like class density | 5.8% (well below 30% threshold) |
| Radix attribute count | 0 |
| Class sample size | 243 |

Ableton is **not** built with shadcn, Radix, Tailwind, Material, Bootstrap, or any other detectable component library. The site appears to be **hand-rolled custom CSS** with BEM-style class naming (`main-nav__logo__image`, `abl-mix-blend-difference`).

## Stack intelligence

| Aspect | Detected |
|---|---|
| CMS | none |
| Analytics | none surfaced |
| Experimentation tools | none |
| Script count | 13 |
| Meta tag count | 15 |

Despite being a high-traffic commercial site, no CMS or analytics platforms were detected in the surface scan. They likely use server-side analytics (no client-side trackers in the HTML head).

## LLM prompts

`ableton-com-prompts/` directory was generated by designlang. Not enumerated here — see the folder directly.

---

# 17. Generated artifacts

All 25 files produced by designlang for this extraction:

| File | Type | Purpose |
|---|---|---|
| `ableton-com-DESIGN.md` | md | designlang's short summary (input to this comprehensive doc) |
| `ableton-com-design-language.md` | md | Long-form design report with audit |
| `ableton-com-design-tokens.json` | json | W3C tokens — colors, type, spacing, radii, shadows |
| `ableton-com-variables.css` | css | 13 CSS custom properties (sparse) |
| `ableton-com-intent.json` | json | Page intent + section reading order |
| `ableton-com-voice.json` | json | Tone, CTA verbs, headings, button labels |
| `ableton-com-anatomy.tsx` | tsx | Button anatomy (only component anatomized) |
| `ableton-com-icon-system.json` | json | 7 custom fill icons on 48px grid |
| `ableton-com-visual-dna.json` | json | Material, imagery, pattern classification |
| `ableton-com-motion-tokens.json` | json | 150ms / 350ms durations |
| `ableton-com-form-states.json` | json | 1 form, 10 inputs, 2 selects |
| `ableton-com-library.json` | json | Library detection (unknown) |
| `ableton-com-mcp.json` | json | MCP-formatted output for AI tools |
| `ableton-com-seo.json` | json | OG, Twitter, favicon, description |
| `ableton-com-stack-intel.json` | json | CMS / analytics detection |
| `ableton-com-logo.json` | json | Logo metadata |
| `ableton-com-logo.svg` | svg | Extracted logo |
| `ableton-com-screenshots.json` | json | Screenshot index |
| `ableton-com-shadcn-theme.css` | css | shadcn variable mapping (mostly empty — no shadcn detected) |
| `ableton-com-tailwind.config.js` | js | Tailwind preset (likely sparse — no Tailwind detected) |
| `ableton-com-theme.js` | js | Theme JS object |
| `ableton-com-figma-variables.json` | json | Figma Variables import format |
| `ableton-com-wordpress-theme.json` | json | WordPress theme.json mapping |
| `ableton-com-preview.html` | html | designlang's basic visual preview |
| `ableton-com-prompts/` | dir | LLM prompts generated for code-gen |
| `ableton-design-system.html` | html | **This skill's polished review page** |
| `DESIGN.md` | md | **This file** — comprehensive reference |
| `screenshots/` | dir | designlang component screenshots |

---

# Cross-system comparison: Ableton vs Langfuse

For reference, comparing the two demos produced by this skill so far:

| Dimension | Ableton | Langfuse |
|---|---|---|
| Colors | 7 unique | 16 unique |
| Brand chromatic | `#0000ff` (blue, 42 uses) | `#fbff7a` (yellow, 19 uses) |
| Font families | 3 (futura-pt + Times + Arial) | 4 (Inter + f37 Analog + Geist Mono + SF Mono) |
| Body face | futura-pt | Inter |
| Display face | futura-pt (same) | f37 Analog (separate) |
| Spacing base | 2px | 4px |
| Radii | **0** (none) | 2px + 6px |
| Shadows | **0** (none) | 7 tokens |
| Pills | no | no |
| Component patterns | 7 | 11 |
| Library | unknown (custom CSS) | shadcn/ui (0.65) |
| Voice | friendly, third-person | neutral, you-only |
| Heading case | Title Case | Sentence case |
| WCAG | 100% | 100% |
| Design score | 86/100 | not surfaced |

The two systems are nearly opposites: Langfuse is structured (shadcn + tokens), Ableton is hand-rolled and brutalist. Both work — and both produce coherent design-system pages from the same skill, demonstrating the de-Langfusified rules generalize.

---

_Generated 2026-05-14 by `/extract-design-system` skill from designlang v12.10.0 output._
_Source extraction: `./design-extract-output/ableton/`_

---
site: Mistral AI
url: https://mistral.ai/
extracted_at: 2026-05-14
generator: designlang v12.10.0
intent: landing (0.29)
library: shadcn/ui (0.65)
material: flat
voice: friendly · you-only · Sentence case · tight
design_score: 94/100 (A) · 2 issues
wcag: 100%
---

# Mistral Design System

> "Frontier AI. In your hands."

A warm-beige, monochrome-with-a-burning-accent system. Mistral commits hard to **one chromatic moment per page** — the six-stop "footer band" — and otherwise paints with black ink on a `#fffaeb` cream surface, reserving the orange `#fa520f` accent for CTAs and links. Material is **flat**. Radius defaults to `0` (brutalist). The lone shadow token is warm-tinted (`rgba(127, 99, 21, ...)`) so cards never throw a cool gray drop on the beige page.

## Confidence summary

| Detection | Confidence | Notes |
|---|---|---|
| Intent (landing) | **0.29** | Weak. Alternates: legal (0.40), blog-post (0.35). The dense feature/testimonial/section composition confused the heuristic. |
| Library (shadcn/ui) | **0.65** | Moderate. Detected via the `--foreground / --primary / --secondary / --muted / --accent / --destructive / --ring / --card / --popover` token shape in the cascade — Mistral has overlaid their own brand tokens on a shadcn scaffold. |
| Material (flat) | medium | Saturation 0.46. One soft shadow. Radius mostly 0. |
| WCAG | **100%** | 0 failing pairs. The black-on-beige base contrast (12.5:1) is the high-water mark. |

---

# 1. Overview

Mistral's homepage is engineering-marketing for an enterprise AI platform. It commits to:

- **One chromatic moment.** The six-stop **footer band** (`#ffe295 → #ffd900 → #ffae00 → #ff8205 → #fa520f → #e00400`) is the brand's identity stripe. Everywhere else the page is monochrome on beige.
- **Brutalist geometry.** Default radius is `0`. Cards, modals, even the hero card have sharp corners. The only radius token (`4px`) is reserved for inputs and chips.
- **Warm shadow.** The sole shadow token uses `rgba(127, 99, 21, ...)` — a deeply warm tint (almost golden-brown) — so cards rest on the beige page rather than feeling pasted on.
- **Display weight = 400.** All headings are weight 400. Hierarchy comes from size (82px → 56px → 48px → 32px), not boldness.
- **Sunshine-tinted lines.** Borders use `#ffe295` (mistral-sunshine-100), a warm yellow. The system never falls back to neutral gray dividers.

The `--color-theme-*` family isn't present — but the `--mistral-footer-band-*`, `--mistral-sunshine-*`, and `--mistral-black-*` token namespaces suggest Mistral has authored a complete brand palette on top of shadcn/ui's foundational tokens, rather than treating it as a swap-the-skin theme system.

---

# 2. Voice

| Aspect | Value |
|---|---|
| Tone | Friendly |
| Pronoun posture | you-only |
| Heading style | Sentence case |
| Heading length | Tight |
| Total buttons | 15 |
| Total headings | 16 |

## Sample headings (detected)

> "Frontier AI.\nIn your hands."
> "Your AI future belongs in your hands."
> "Deployed in production."
> "What Mistral AI can do for you."
> "Autonomous work."
> "Powered by a deeply configurable AI platform."
> "AI deployments designed for privacy."
> "Why Mistral"

**Emphasis style:** No colored-word emphasis on mistral.ai. The H1 is plain — Mistral uses the footer band as the page's color moment and lets headings stay monochromatic. The skill does **not** synthesize a pill or colored span here.

**Heading structure habit:** Mistral favors a two-line break — short subject sentence, then short claim. ("Frontier AI." / "In your hands.") This is a signature.

## CTA verbs (top)

| Verb | Count |
|---|---|
| discover | 6 |
| go | 2 |
| view | 1 |
| start | 1 |
| talk | 1 |
| products | 1 |
| company | 1 |

## Button patterns (signature)

The repeated "Discover <Product>" pattern is the system's strongest CTA convention:

- Discover Le Chat
- Discover Vibe
- Discover Studio
- Discover Forge
- Discover Applied AI
- Discover more

The verb pulls the user toward each product family; the verb itself is part of the brand.

---

# 3. Colors

## 3a. Brand (from `*-variables.css`)

| Hex | Role | Notes |
|---|---|---|
| `#fffaeb` | mistral-beige · page surface | The system's anchor |
| `#1f1f1f` | mistral-black-matt · ink | Body text (hsl 0 0% 12%) |
| `#fa520f` | mistral-orange · accent | Buttons, links (hsl 17 96% 52%) |

## 3b. Full sunshine ramp · beige → yellow

| Token | Hex | Role |
|---|---|---|
| `--color-bg` | `#fffaeb` | Page background |
| `--color-mistral-sunshine-50` | `#fff0c2` | Sunken card surface |
| `--color-mistral-sunshine-100` | `#ffe295` | Lines / dividers (replaces neutral gray) |
| `--color-mistral-sunshine-200` | `#ffdd8a` | — |
| `--color-mistral-sunshine-300` | `#ffd06a` | — |
| `--color-secondary` | `#ffd900` | Sun-yellow accent surface |

## 3c. Full orange & red ramp · the warm end

| Token | Hex | Role |
|---|---|---|
| `--color-accent` | `#ffae00` | Amber / deep-accent |
| `--color-mistral-sunshine-900` | `#ff8a00` | — |
| `--color-mistral-orange-bright` | `#ff8205` | Bright orange (block-3-color, used on hero illustration blocks) |
| `--color-mistral-orange` | `#fa520f` | The signature mistral orange (hsl 17 96% 52%) |
| `--color-bg-7 / mistral-red` | `#e00400` | Destructive · the band's final stop |
| `--color-black` | `#000000` | Deep-black · rare, reserved for highest-emphasis |

## 3d. Text scale

| Token | Hex | Role |
|---|---|---|
| `--color-mistral-black-matt` | `#1f1f1f` | Primary text · 12% black |
| `--color-mistral-black-matt-tint` | `#3c3c3c` | Muted text · 24% black |
| `--color-text-3 / mistral-orange` | `#fa520f` | Accent-as-text (links, eyebrow callouts) |
| `--color-white` | `#ffffff` | Inverted text on dark or accent surfaces |

## 3e. The footer band (the brand's identity stripe)

This is the system's chromatic moment. Six discrete tokens, **not** a smooth gradient:

```
--mistral-footer-band-1: hsl(45 100% 88%)   /* #ffe295 — beige-sun */
--mistral-footer-band-2: hsl(51 100% 50%)   /* #ffd900 — yellow */
--mistral-footer-band-3: hsl(41 100% 50%)   /* #ffae00 — amber */
--mistral-footer-band-4: hsl(30 100% 51%)   /* #ff8205 — bright orange */
--mistral-footer-band-5: hsl(17 96% 52%)    /* #fa520f — mistral orange */
--mistral-footer-band-6: hsl(1 100% 44%)    /* #e00400 — mistral red */
```

Each segment is an equal slice with a hard edge. That hard-edge construction is what makes the band feel printed (a flag, a thermal-gradient bar) rather than rendered (a smooth CSS gradient). It runs across the bottom of the footer, and Mistral occasionally caps hero blocks with a thin 6px stripe of the same.

## 3f. Block colors (illustration palette)

Mistral uses 7 numbered `--block-*-color` tokens for marketing-page hero blocks:

| Token | Hex |
|---|---|
| `--block-1-color` | `#ffe295` |
| `--block-2-color` | `#ffd900` |
| `--block-3-color` | `#ff8d06` |
| `--block-4-color` | `#fef2cb` |
| `--block-5-color` | `#ffe295` |
| `--block-6-color` | `#ffd900` |
| `--block-7-color` | `#ff8105` |

These overlap the band stops — the brand reuses the same warm tones across band and block tokens for visual cohesion.

## 3g. Total DOM color inventory

12 unique colors detected. The restraint is intentional: a designer working in Mistral's system has fewer choices to make, and those choices nearly always land somewhere on the sunshine→red ramp.

---

# 4. Typography

## 4a. Families (3 detected + 2 bespoke monos)

| Family | Uses | Notes |
|---|---|---|
| **Arial** | 977 | Display, body, UI — the entire visible system. System font; no licensing concern. |
| **Times** | 9 | Likely residual / browser fallback, not intentional. |
| **Rubik** | 1 | Vestigial. |
| **Pixelbasel** | (mono token) | Bespoke mono. Falls back to Consolas → Courier in the cascade. |
| **FragmentMono** ("font-vibe") | (mono token) | Bespoke mono. Used for "vibe-coded" decorative metadata in marketing surfaces. |

**Audit note:** Arial-as-display is a deliberate choice. The brand's confidence is "the type doesn't need to be fancy — the band and the orange do the work." This contrasts hard with the Claude/Cursor approach where custom display fonts carry identity.

## 4b. Type scale (11 detected sizes)

| Size | Weight | Line-height | Family | Role |
|---|---|---|---|---|
| 103px | 400 | 97.85px | Arial | H0-md (huge display) |
| 90px | 400 | 90px | Arial | H1-md |
| 82px | 400 | 82px | Arial | H1 |
| 72px | 400 | 72px | Arial | H0 |
| 56px | 400 | 53.2px | Arial | H2-md |
| 48px | 400 | 45.6px | Arial | H3-md |
| 40px | 400 | — | Arial | H2 |
| 38px | 400 | — | Arial | subtitle-md detected size |
| 32px | 400 | 36.8px | Arial | subtitle-md |
| 30px | 400 | 34.5px | Arial | H3 |
| 24px | 400 | 27.6px | Arial | subtitle |
| 16px | 400 | — | Arial | body |
| 14px | 400 | — | Arial | UI |
| 13.33px | 400 | — | Arial | rendered base |
| 13px | 400 | — | Arial | small |

**All headings are weight 400.** No bold variants in the heading scale. Hierarchy lives entirely in size and color. The `--font-weight-black: 900` token exists but is unused in detected DOM.

## 4c. Letter-spacing

From the `--tracking-*` tokens: `tracking-tight: -0.025em`, `tracking-wide: 0.025em`, `tracking-wider: 0.05em`, `tracking-widest: 0.1em`. Tight tracking is applied to display headings (82px+). Widest is used for eyebrow uppercase metadata.

## 4d. Mono surface

Mono is reserved for code samples, metadata labels, and eyebrow uppercase. The two bespoke monos (`Pixelbasel`, `FragmentMono`) aren't loaded in this demo — falls back to `ui-monospace`. The visual rhythm carries.

---

# 5. Spacing

## 5a. Scale (2px base, section-rhythm large stops)

| Token | Value |
|---|---|
| base | 2px |
| s1 | 32px |
| s2 | 48px |
| s3 | 64px |
| s4 | 72px |
| s5 | 80px |
| s6 | 98px |
| s7 | 173px |
| s8 | 392px |

**No middle range.** The scale jumps from 2px straight to 32px — Mistral's component-level spacing isn't algorithmic, it's per-component. Then large section-level chunks (64, 72, 80, 98) provide vertical rhythm. The 392px outlier is hero-height territory.

## 5b. Tailwind-derived scale (overlay)

Mistral also exposes a Tailwind/shadcn spacing scale via `--spacing-md (16px)`, `--spacing-xl (24px)`, `--spacing-3xl (48px)`, `--spacing-4xl (64px)`, `--spacing-5xl (96px)`, `--spacing-6xl (128px)`. This is the actively used vocabulary for component spacing — the larger numbered values are observed in production but not deliberately tokenized.

---

# 6. Layout

| Property | Value |
|---|---|
| Grid containers | 3 |
| Flex containers | 161 |
| Breakpoints detected | 4 |
| Z-index layers | 9 (1 issue) |

Flex-heavy. Typical for shadcn/Tailwind layouts.

## 6a. Reading order (8 sections)

`testimonial → logo-wall → nav → hero → content → hero → footer → nav`

**Notable:** The first detected section is `testimonial` (confidence 0.80), not `hero` — designlang reads the "Frontier AI. / In your hands." card as a testimonial-style claim because of its banner shape, dense CTA count (18), and supporting subheadings. This isn't wrong; it's a stylistic call by Mistral to frame the hero as social-proof-shaped.

The two `hero` sections lower in the page are the product-specific sections ("Deployed in production." and "AI deployments designed for privacy.") — each gets its own banner moment.

## 6b. Nav heights

`--nav-height: 100px` desktop · `--nav-height-mobile: 88px`. These are explicit tokens, suggesting the nav was intentionally sized — not a one-off `height: 100px` decoration.

---

# 7. Shape

## 7a. Radii (2 values · brutalist by default)

| Token | Value | Use |
|---|---|---|
| default | 0px | Cards, modals, buttons, hero, footer |
| sm | 4px | Inputs, chips, badges |

`--radius: 0rem` is the system root. Other "named" radius tokens in the cascade (`--radius-2xl: 1rem`, `--radius-3xl: 1.5rem`) exist in the Tailwind defaults but are not observed in painted DOM.

## 7b. Pill use

`hasPill: false`. No 999px elements detected.

---

# 8. Elevation

One detected shadow token — and it's distinctive:

```
--shadow-sm:
  rgba(127, 99, 21, 0.12) -8px 16px 39px 0px,
  rgba(127, 99, 21, 0.1)  -33px 64px 72px 0px,
  rgba(127, 99, 21, 0.06) -73px 144px 97px 0px,
  rgba(127, 99, 21, 0.02) -130px 256px 115px 0px,
  rgba(127, 99, 21, 0)    -203px 400px 126px 0px;
```

Five stacked layers, all the same warm-brown color (`rgb(127, 99, 21)` ≈ deep ochre), with descending alpha and increasing offset. The shadow falls **left** (negative x-offset) — most systems drop straight down or slightly right. This left-fall plus warm-tint is the most distinctive component-level identity move in the system after the band.

---

# 9. Motion

`motion-tokens.json` is minimal — Mistral doesn't expose semantic motion tokens. Animations are defined per-component (`--animate-pulse`, `--animate-accordion-down/up`, `--animate-spin`, `--animate-rotate-y`) rather than from a centralized scale. The `--default-transition-duration: 0.15s` and `--default-transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1)` are the only generic motion defaults.

---

# 10. Components

6 detected patterns. From `anatomy.tsx`: buttons (primary, outline · sm, md · 16 instances), inputs, links, navigation, footer, modals.

**Components that are notably absent:** tabs, segmented controls, badges (chips exist but aren't tokenized), accordion (the tokens exist but no detected accordion DOM), data tables, breadcrumbs, toast, drawer, switch. Mistral's component surface is intentionally narrow — the footer band carries chromatic identity and the orange CTAs carry interactive identity, so additional pattern variety isn't needed.

---

# 11. Icons

| Property | Value |
|---|---|
| Total | 42 |
| Style | filled (mixed) |
| Library | unknown |
| Library confidence | 0.00 |
| Avg stroke | n/a |

Icons are rendered via inline SVG with Tailwind utility classes (`size-3`, `size-4`, `size-8`, `text-mistral-orange`). Most usage is decorative chevrons and arrows for nav rotation states. No detected icon library — Mistral ships its own custom inline SVGs.

---

# 12. Forms & inputs

| Property | Value |
|---|---|
| Forms | 1 |
| Modals | 0 (detected) |
| Toasts | 0 |

Minimal form surface — mistral.ai is product-marketing, not the dashboard. The Studio/Le Chat surfaces would have substantially richer forms.

---

# 13. Accessibility

| Property | Value |
|---|---|
| **WCAG score** | **100%** |
| Passing pairs | 11 |
| Failing pairs | 0 |

## Passing pairs (highlights)

| FG | BG | Ratio | Tag |
|---|---|---|---|
| `#1f1f1f` | `#fffaeb` | **12.5:1** | AAA · body text |
| `#3c3c3c` | `#fffaeb` | 8.6:1 | AAA · muted text |
| `#ffffff` | `#fa520f` | 4.5:1 | AA · primary CTA |
| `#fffaeb` | `#1f1f1f` | 15.4:1 | AAA · inverted CTA |

The 100% score is not accidental — Mistral never paints accent-on-beige for body text. The orange is reserved for control surfaces (buttons, focus rings, links underline), where the system can guarantee the contrasting fill or border carries the contrast.

---

# 14. SEO & brand surface

| Property | Value |
|---|---|
| Title | "Frontier AI LLMs, assistants, agents, services \| Mistral AI" |
| Description | "The most powerful AI platform for enterprises. Customize, fine-tune, and deploy AI assistants, autonomous agents, and multimodal AI with open models." |
| Logo | Wordmark · 91 images detected |

---

# 15. Audit findings

## Don'ts (from `*-design-language.md`)

| Finding | Severity |
|---|---|
| **55 `!important` rules** in CSS | Medium — prefer specificity over overrides |
| **3,194 duplicate CSS declarations** | Medium — likely from utility framework + custom layer overlap |

## Do's

- Disciplined 2-radius scale (0 default, 4 for inputs) — the brutalist commitment is consistent
- 100% WCAG score · reserves accent for control surfaces, never as text on the page
- The footer band as a tokenized identity stripe — six discrete colors, not a smooth gradient, with stable role-numbered tokens (`band-1` through `band-6`)
- Warm-tinted shadow (`rgba(127, 99, 21, ...)`) keeps cards anchored on the beige page
- All headings weight 400 — restraint that lets size + color do hierarchy

## Inferred mappings & fallbacks (this demo)

- **Arial** is system-default; no licensing or self-hosting concern. The demo renders it 1:1 with the source.
- **Pixelbasel** and **FragmentMono** ("font-vibe") are bespoke mono fonts not loaded here — the demo falls back to `ui-monospace`. Mono is sparingly used (metadata, code), so the visual identity carries.

---

# 16. Frameworks & integrations

| Aspect | Value |
|---|---|
| Detected library | **shadcn/ui** |
| Confidence | 0.65 |
| Token scaffold | `--foreground`, `--primary`, `--secondary`, `--muted`, `--accent`, `--destructive`, `--ring`, `--card`, `--popover` |
| Brand overlay | `--mistral-*` token namespace (band, sunshine, black-matt, orange-bright, footer-band) layered on top |

Mistral runs shadcn/ui's canonical token names underneath but overrides with brand-specific tokens. The pattern (shadcn scaffold + branded overlay) is a forward-looking architecture choice — it means Mistral can pull from the shadcn component ecosystem without inheriting its default neutral aesthetic.

---

# 17. Generated artifacts

All files in `./design-extract-output/mistral/`:

| File | Purpose |
|---|---|
| `mistral-ai-DESIGN.md` | designlang's short summary |
| `mistral-ai-design-tokens.json` | W3C tokens |
| `mistral-ai-variables.css` | **294 CSS custom properties** — the richest source |
| `mistral-ai-intent.json` | 8-section reading order |
| `mistral-ai-voice.json` | Tone, CTAs, 16 sample headings |
| `mistral-ai-anatomy.tsx` | Component anatomy stubs |
| `mistral-ai-icon-system.json` | 42 inline SVG icons (unknown library) |
| `mistral-ai-visual-dna.json` | Material, imagery, patterns |
| `mistral-ai-motion-tokens.json` | (sparse) |
| `mistral-ai-library.json` | shadcn/ui detection · 0.65 |
| `mistral-ai-seo.json` | OG, meta tags |
| `mistral-ai-tailwind.config.js` | Generated Tailwind preset |
| `mistral-ai-shadcn-theme.css` | shadcn token mapping |
| `mistral-ai-wordpress-theme.json` | WordPress theme JSON (not applicable) |
| `mistral-ai-preview.html` | designlang's basic preview |
| `mistral-design-system.html` | **This skill's polished review** |
| `DESIGN.md` | **This file** |

---

_Generated 2026-05-14 by `/extract-design-system` skill from designlang v12.10.0 output._

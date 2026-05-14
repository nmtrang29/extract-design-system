---
site: Langfuse
url: https://langfuse.com/
extracted_at: 2026-05-14
generator: designlang v12.10.0
elements_analyzed: 1913
intent: landing (0.61)
library: shadcn/ui (0.65) · alternates: tailwindcss (0.30)
material: flat
imagery: flat-illustration (alternates: icon-only, photography)
voice: neutral · you-only · Sentence case · balanced
---

# Langfuse Design System

> "Open Source LLM Engineering Platform"

A **warm-beige flat system** anchored on near-black ink and signature near-white yellow (#fbff7a). Built on shadcn/ui with extensive semantic role tokens layered on top. WCAG 100%, near-monochrome (saturation 0.18), two-radius scale (2/6), no pills.

## Confidence summary

| Detection | Confidence | Notes |
|---|---|---|
| Intent (landing) | 0.61 | Medium. Alternates: blog-post (0.35) — the editorial density confused the heuristic |
| Library (shadcn/ui) | 0.65 | Strong. Evidence: shadcn CSS tokens. Tailwindcss as 0.30 fallback |
| Material (flat) | medium | metrics: shadowProfile=soft, saturation=0.179, gradientCount=1 |
| Imagery (flat-illustration) | 0.055 | Weak. SVG-dominated (67/118), icon-heavy (95/118) |
| WCAG | 100% | Strong — 90 passing, 0 failing |
| `hasPill` | false | Brutalist-leaning shape commitment |

---

# 1. Overview

A landing page for an open-source LLM engineering platform. The visual language commits to:

- **Tight two-radius scale**: 2px and 6px only. No pills.
- **Warm beige surface system**: page bg `#edede8`, card `#f6f6f3`, sunken `#e5e5e1`.
- **Near-monochrome palette**: saturation 0.18; the only chromatic emphasis is yellow (`#fbff7a`, 19 uses) and a single indigo link color (`#4f39f6`).
- **Editorial display face**: f37 Analog at 68px H1 — unusually large.
- **Inter for everything else**: body, UI, captions.
- **Shadcn/ui underneath**: detectable, but Langfuse overrides most shadcn tokens with their own `--surface-*`, `--text-*`, `--line-*`, `--callout-*` system.
- **Soft shadows but used sparingly**: 7 shadow tokens, most rounding to "sm" duplicates.
- **Scroll-linked motion**: yes. Three duration tokens (100/180/700ms).

---

# 2. Voice

| Aspect | Value |
|---|---|
| Tone | neutral |
| Pronoun posture | you-only |
| Heading style | Sentence case |
| Heading length | balanced |
| Total buttons | 34 |
| Total headings | 28 |

## Sample headings (from voice.json + intent.json)

- "Open Source LLM Engineering Platform" (hero, repeated 3×)
- "Gain deep visibility into your traces" (repeated 3×)
- "Launch, observe, improve — repeat."
- "All the tools, one integrated platform."
- "Works with any stack."
- "Open platform. Open source."
- "Made for developers, loved by agents."
- "Enterprise scale and security."
- "Why use Langfuse?"
- "Start improving your agents in under 5 minutes."
- "Questions & Answers"
- "What is Langfuse?"
- "What does Langfuse help me with?"
- "Can I use just tracing without the other features?"
- "What deployment options do exist?"

**Most-repeated noun**: "LLM" (appears in hero, "Why use Langfuse?", multiple feature sections). Selected for `<em>` emphasis.

## CTA verbs (all 10)

| Verb | Count |
|---|---|
| install | 8 |
| start | 4 |
| what | 4 |
| get | 3 |
| documentation | 2 |
| configure | 2 |
| is | 2 |
| langfuse | 1 |
| product | 1 |
| resources | 1 |

## Button labels (all 15)

| Label | Count |
|---|---|
| Start free | 4 |
| Documentation | 2 |
| Install via coding agent | 2 |
| Manual install | 2 |
| 🇯🇵 Langfuse Cloud Japan is live → | 1 |
| Product | 1 |
| Resources | 1 |
| Launch app | 1 |
| Get demo | 1 |
| See all integrations | 1 |
| Install skill | 1 |
| Configure CLI | 1 |
| Configure MCP | 1 |

---

# 3. Colors

## 3a. Brand

| Hex | Role | Uses |
|---|---|---|
| `#f6f6f3` | primary · brand surface | 155 |
| `#fbff7a` | secondary · signature highlight | 19 |
| `#edede8` | accent · page background | 20 |

The "primary" is a near-white, used as the elevated card surface. The yellow (secondary) is the only chromatic brand color and shows up sparingly as a CTA / highlight pill. Accent is the warm-beige page bg.

## 3b. Semantic tokens (from variables.css)

Langfuse has an extensive role-token system layered on top of shadcn. Each semantic token group documents a specific UI use.

### Surface (9)

| Token | Hex | Role |
|---|---|---|
| `--surface-1` | `#edede8` | Page background |
| `--surface-bg` | `#f6f6f3` | Primary card / panel |
| `--surface-2` | `#e5e5e1` | Sunken / hover |
| `--surface-beige-accent` | `#f1ede1` | Warm beige callouts |
| `--surface-cta-primary` | `#fbff81` | Signature yellow CTA |
| `--surface-code` | `#333333` | Code block bg |
| `--surface-code-grey` | `#3d3d3d` | Code surface secondary |
| `--surface-code-button` | `#51504f` | Code-block action buttons |
| `--surface-button-grey` | `#403d391a` | Translucent button tint |

### Text (6)

| Token | Hex | Role |
|---|---|---|
| `--text-primary` | `#222220` | Headings, body |
| `--text-secondary` | `#3d3d38` | Supporting copy |
| `--text-tertiary` | `#6b6b66` | Captions, metadata |
| `--text-disabled` | `#a7a7a0` | Placeholders, inactive |
| `--text-links` | `#4f39f6` | Inline links — only chromatic text token |
| `--text-code-secondary` | `#fffcf280` | Secondary code text (translucent) |

### Border & line (4)

| Token | Hex | Role |
|---|---|---|
| `--line-structure` | `#cfcfc9` | Default borders, dividers |
| `--line-cta` | `#404039` | Dark CTA outline |
| `--line-divider-dash` | `#bebeb6` | Dashed dividers |
| `--line-code-border` | `#333333` | Code block outline |

### Status & callout (5)

| Token | Hex | Role |
|---|---|---|
| `--callout-success` | `#538a2e` | Success states |
| `--callout-error` | `#cc3314` | Errors, destructive |
| `--callout-warning` | `#e09d00` | Warnings, quota |
| `--callout-info` | `#b3abef` | Informational |
| `--callout-idea` | `#119da4` | Tips |

### Code syntax (8)

| Token | Hex | Role |
|---|---|---|
| `--text-code-orange` | `#c17e2e` | Strings, identifiers |
| `--text-code-pink` | `#d05376` | Keywords |
| `--text-code-blue` | `#438aa5` | Functions |
| `--color-fd-diff-add-symbol` | `#0ac864` | Diff "+" marker |
| `--color-fd-diff-add` | `#0eb4641a` | Diff added line bg |
| `--color-fd-diff-remove-symbol` | `#e60a64` | Diff "−" marker |
| `--color-fd-diff-remove` | `#c80a641f` | Diff removed line bg |
| `--button-icon-color` | `#6b6b66` | Code-block icon buttons |

### Shadcn primitives (11 pairs)

| Token | Value | Role |
|---|---|---|
| `--primary` | hsl(222 47% 11%) → #0f172a | Primary button |
| `--primary-foreground` | hsl(210 40% 98%) → #f8fafc | Text on primary |
| `--secondary` | hsl(214 32% 91%) → #e1e7ef | Secondary surface |
| `--secondary-foreground` | hsl(222 47% 11%) → #0f172a | Text on secondary |
| `--accent` | hsl(214 32% 91%) → #e1e7ef | (collapses to same as secondary/muted) |
| `--muted` | hsl(214 32% 91%) → #e1e7ef | (collapses to same) |
| `--muted-foreground` | `#7a7a74` | Subdued text |
| `--destructive` | hsl(0 84% 60%) → #ef4444 | Delete buttons |
| `--destructive-foreground` | hsl(210 40% 98%) → #f8fafc | Text on destructive |
| `--background` | hsl(0 0% 99%) → #fcfcfc | Root page bg (shadcn override) |
| `--foreground` | hsl(222 84% 5%) → #020817 | Root text (shadcn override) |
| `--card / --popover` | hsl(0 0% 100%) → #ffffff | Card & popover |
| `--border / --input / --ring` | hsl(214 32% 91%) → #e1e7ef | Borders, inputs, focus rings |

## 3c. Tailwind palette (from variables.css)

Langfuse imports much of the Tailwind color layer, mostly unused in DOM. Detected in variables.css (lab() values converted to approximate hex):

`gray-50/100/200/300/400/500/600/700/800/900`, `slate-100..900`, `blue-50..900`, `red-50..900`, `green-50..900`, `purple-100..900`, `rose-100/300/800/900`, `pink-600`, `emerald-100..900`, `teal-600`, `amber-600`, `yellow-100/300/500/800/900`, `orange-100..900`, `indigo-600`

These are available to developers but rarely surface in the rendered DOM — semantic Langfuse tokens dominate.

## 3d. Framework-specific vars

Fumadocs detected (the `--color-fd-*` namespace). 16 fumadocs tokens including:
- `--color-fd-secondary`, `--color-fd-popover`, `--color-fd-foreground`, `--color-fd-background`, `--color-fd-card`, `--color-fd-muted`, `--color-fd-ring`, `--color-fd-overlay`, `--color-fd-accent`, `--color-fd-secondary-foreground`, `--color-fd-accent-foreground`, `--color-fd-muted-foreground`, `--color-fd-primary`, `--color-fd-primary-foreground`, `--color-fd-info`, `--color-fd-success`, `--color-fd-error`, `--color-fd-warning`, `--color-fd-idea`
- Plus `--color-fd-diff-add(-symbol)` and `--color-fd-diff-remove(-symbol)` (already covered in Code syntax)

## 3e. Full unique-hex inventory (16 colors detected in DOM)

| Hex | Roles | DOM uses |
|---|---|---|
| `#e1e7ef` | border, background | 1704 |
| `#020817` | text, border | 752 |
| `#6b6b66` | text, background | 406 |
| `#3d3d38` | text, border, background | 292 |
| `#222220` | text, background | 206 |
| `#cfcfc9` | border, background | 205 |
| `#f6f6f3` | background, text | 155 |
| `#000000` | text, background | 105 |
| `#0f172a` | text, background | 21 |
| `#edede8` | background | 20 |
| `#a7a7a0` | text | 19 |
| `#fbff7a` | background | 19 |
| `#ffffff` | text, background | 16 |
| `#374151` | text | 7 |
| `#9ca3af` | text | 2 |
| `#d8d8d8` | background | 1 |

## 3f. Gradients

1 gradient detected: a repeating-linear-gradient at 315° using `#f6f6f3` and `rgba(108, 103, 96, 0.1)` — the **line-grid** background pattern used in the hero and component preview frame.

`backgroundPatterns.labels = ["line-grid"]`. No dot grids, mesh, or noise.

---

# 4. Typography

## 4a. Families (all 4 detected)

| Family | Uses | Coverage |
|---|---|---|
| Inter | 1597 | 84% — body, UI, captions, eyebrow |
| f37 Analog | 277 | 14% — display (headings) |
| Geist Mono | 23 | 1% — code |
| SF Mono | 4 | <1% — fallback only |

Audit recommendation: 4 families exceeds the suggested 2. SF Mono is likely a system-font fallback that crept in and could be removed.

## 4b. Fallback chains (from variables.css)

```css
--font-sans:    'Inter', 'Inter Fallback', ui-sans-serif, system-ui, sans-serif, "Apple Color Emoji",
                "Segoe UI Emoji", "Segoe UI Symbol", "Noto Color Emoji"
--font-mono:    "geistMono", "geistMono Fallback", ui-monospace, SFMono-Regular, Menlo, Monaco,
                Consolas, "Liberation Mono", "Courier New", monospace
--font-analog:  "f37Analog", "f37Analog Fallback"
--font-serif:   ui-serif, Georgia, Cambria, "Times New Roman", Times, serif
```

## 4c. Type scale (full)

| Size | Weight | Line-height | Family (inferred) | Role |
|---|---|---|---|---|
| 68px | 500 | 71.4px (1.05) | f37 Analog | H1 (hero display) |
| 50px | 500 | 50px (1.0) | f37 Analog | H2 |
| 32px | 500 | 36.8px (1.15) | f37 Analog | H3 |
| 20px | 400 | 20px (1.0) | Inter | H4 |
| 16px | 400 | 24px (1.5) | Inter | Body |
| 15px | 400 | 22.5px (1.5) | Inter | Body-alt |
| 14px | 500 | 20px (1.43) | Inter | UI |
| 13px | 400 | 19.5px (1.5) | Inter | UI-small |
| 12px | 400 | 19.5px (1.625) | Geist Mono | Code (used in `<code>`, `<pre>`) |
| 11px | 400 | 11px (1.0) | Inter | Caption |
| 10px | 600 | 15px (1.5) | Inter | Eyebrow (uppercase, 0.08em tracking) |

**Tailwind text-* tokens detected** in variables.css (separate scale, less commonly used in DOM): text-xs/sm/base/lg/xl/2xl/3xl/4xl/5xl/6xl/7xl/8xl with computed `--text-*--line-height` ratios.

## 4d. All weights detected

`400` (normal), `500` (medium), `600` (semibold), `700` (bold)

From `--font-weight-*` tokens: `--font-weight-normal: 400`, `--font-weight-medium: 500`, `--font-weight-semibold: 600`, `--font-weight-bold: 700`.

## 4e. Line-heights detected

Both explicit pixel values (71.4px, 50px, 36.8px, 24px, 22.5px, etc.) and computed Tailwind ratios via `calc()`.

## 4f. Letter-spacing values (from variables.css)

| Token | Value |
|---|---|
| `--tracking-tight` | -0.025em |
| `--tracking-wide` | 0.025em |
| `--tracking-wider` | 0.05em |
| `--tracking-widest` | 0.1em |

Used predominantly: `tracking-tight` on display headings (H1/H2/H3), `tracking-widest` on eyebrows.

## 4g. All detected headings on the page

28 total headings. Sample (full set in §2 Voice):

H1: "Open Source LLM Engineering Platform" (×3 — appears in hero + reading order repetition)
H2: "Launch, observe, improve — repeat.", "All the tools, one integrated platform.", "Works with any stack.", "Open platform. Open source.", "Made for developers, loved by agents.", "Enterprise scale and security.", "Why use Langfuse?", "Start improving your agents in under 5 minutes.", "Questions & Answers"
H3+: FAQ questions

---

# 5. Spacing

## 5a. Scale (base 4px)

| Token | Value | Notes |
|---|---|---|
| s0 | 1px | Hairline |
| s1 | 24px | (no 4/8/12/16/20 tokens — chrome handled outside) |
| s2 | 32px | |
| s3 | 40px | |
| s4 | 60px | |
| s5 | 64px | |
| s6 | 80px | |
| s7 | 100px | |
| s8 | 120px | |

Tailwind base spacing (`--spacing: .25rem` = 4px) is present but used minimally — the macro section spacing (60/80/100/120) dominates.

## 5b. Container widths

| Token | Value |
|---|---|
| `--container-xs` | 20rem (320px) |
| `--container-sm` | 24rem (384px) |
| `--container-md` | 28rem (448px) |
| `--container-lg` | 32rem (512px) |
| `--container-xl` | 36rem (576px) |
| `--container-2xl` | 42rem (672px) |
| `--container-3xl` | 48rem (768px) |
| `--container-4xl` | 56rem (896px) |
| `--container-6xl` | 72rem (1152px) |
| `--container-7xl` | 80rem (1280px) |

---

# 6. Layout

## 6a. Primitives

| Type | Count |
|---|---|
| Grid containers | 19 |
| Flex containers | 597 |

Flex-dominated layout (a common pattern for shadcn/ui sites).

## 6b. Breakpoints

10 breakpoints reported by designlang but values rendered as `[object Object]px` (serialization bug).

From variables.css: `--breakpoint-sm: 40rem`, `--breakpoint-wide: 1440px`. The rest aren't exported as CSS vars — likely raw media queries in source.

## 6c. Reading order (20 sections)

| # | Tag | Role | Confidence | Heading |
|---|---|---|---|---|
| 0 | header | cta | 0.75 | (header bar) |
| 1 | nav | nav | 0.90 | "by ClickHouse · Product · Overview..." |
| 2 | aside | sidebar | 0.40 | "Community Stats" |
| 3 | nav | nav | 0.90 | (same as 1) |
| 4 | main | pricing-table | 0.90 | "Open Source LLM Engineering Platform" |
| 5 | main | pricing-table | 0.90 | (continued) |
| 6 | section | pricing-table | 0.90 | (continued) |
| 7 | section | content | 0.30 | "Gain deep visibility into your traces" |
| 8 | section | testimonial | 0.80 | "Launch, observe, improve — repeat." |
| 9 | section | feature-grid | 0.80 | "All the tools, one integrated platform." |
| 10 | section | hero | 0.40 | "Works with any stack." |
| 11 | section | feature-grid | 0.80 | "Open platform. Open source." |
| 12 | section | testimonial | 0.80 | "Made for developers, loved by agents." |
| 13 | section | pricing-table | 0.90 | "Enterprise scale and security." |
| 14 | section | pricing-table | 0.90 | "Why use Langfuse?" |
| 15 | section | pricing-table | 0.90 | "Start improving your agents in under 5 minutes." |
| 16 | section | faq | 0.85 | "Questions & Answers" |
| 17 | footer | footer | 0.95 | "Product" |
| 18 | aside | feature-grid | 0.80 | (on-this-page sidebar) |
| 19 | nav | nav | 0.90 | (on-this-page nav) |

## 6d. Role tally

`cta: 1 · nav: 3 · sidebar: 1 · pricing-table: 6 · content: 1 · testimonial: 2 · feature-grid: 3 · hero: 1 · faq: 1 · footer: 1`

⚠ 6 consecutive "pricing-table" sections (#4-6 + #13-15) — likely heuristic false positive on dense feature/card grids.

---

# 7. Shape

## 7a. Radii

| Token | Value | Use |
|---|---|---|
| `--radius-xs` | 2px | Controls (buttons sm, badges, focus rings) |
| `--radius-md` | 6px | Cards, panels, inputs |

Tailwind also defines `--radius-sm: calc(.5rem - 4px)`, `--radius-lg: .5rem`, `--radius-2xl: 1rem`, `--radius-xl: .75rem`, `--radius: .5rem`. These are largely unused — the system commits to the 2/6 vocabulary.

## 7b. Pill use

`hasPill: false`. No 999px elements detected in the DOM (despite Tailwind's `rounded-full` being available).

---

# 8. Elevation

7 shadow tokens. Many normalize to "sm".

| Name | Profile | Value |
|---|---|---|
| sh0 (`--shadow-sm`) | sm — 4/6 mid-soft | `0 4px 6px -1px rgba(0,0,0,0.1), 0 2px 4px -2px rgba(0,0,0,0.1)` |
| sh1 (`--shadow-sm` dup) | sm — 1/3 tight | `0 1px 3px 0 rgba(0,0,0,0.1), 0 1px 2px -1px rgba(0,0,0,0.1)` |
| sh2 (`--shadow-sm` dup) | none | (all transparent) |
| sh3 (`--shadow-sm` dup) | sm — 8/24 wide | `0 8px 24px -4px rgba(0,0,0,0.12), 0 4px 8px -2px rgba(0,0,0,0.06)` |
| sh4 (`--shadow-sm` dup) | sm — 4/8 floaty | `0 4px 8px 0 rgba(0,0,0,0.05), 0 4px 4px 0 rgba(0,0,0,0.03)` |
| sh5 (`--shadow-md`) | md | `0 4px 8px 0 rgba(0,0,0,0.05), 0 4px 4px 0 rgba(0,0,0,0.03)` |
| sh6 (`--shadow-xl`) | xl — directional | `-23px 51px 16px 0 rgba(0,0,0,0), -15px 33px 14px 0 rgba(0,0,0,0.01), -8px 18px 12px 0 rgba(0,0,0,0.02), -4px 8px 9px 0 rgba(0,0,0,0.03), -1px 2px 5px 0 rgba(0,0,0,0.04)` |

`visual-dna.json` `shadowProfile: soft`, `avgShadowBlur: 0` (designlang couldn't compute blur from the nested rgba(0,0,0,0) zero-layer stacks).

Z-index layers: **7**.

---

# 9. Motion

## 9a. Duration tokens

| Token | Value |
|---|---|
| xs | 100ms |
| sm | 180ms |
| lg | 700ms |

No md or xl tokens. Two-tier-plus-emphasis vocabulary.

## 9b. Easing

| Token | Family | Value |
|---|---|---|
| `custom-900` | custom | `cubic-bezier(0.4, 0, 0.2, 1)` (standard material-ish ease) |
| `ease-in-out` | ease-in-out | `ease` (CSS keyword) |
| `ease-out-802` | ease-out | `cubic-bezier(0, 0, 0.2, 1)` |

## 9c. Springs

None detected.

## 9d. Meta

| Property | Value |
|---|---|
| Feel | mixed |
| Scroll-linked | **yes** |

## 9e. Named keyframes (from variables.css)

| Animation | Value |
|---|---|
| `--animate-pulse` | pulse 2s cubic-bezier(.4,0,.6,1) infinite |
| `--animate-spin` | spin 1s linear infinite |
| `--animate-ping` | ping 1s cubic-bezier(0,0,.2,1) infinite |
| `--animate-fall` | fall 1.5s linear forwards |
| `--animate-accordion-down` | accordion-down .2s ease-out |
| `--animate-accordion-up` | accordion-up .2s ease-out |
| `--animate-fd-fade-in` / `-out` | fd-fade-* .3s ease |
| `--animate-fd-popover-in` / `-out` | fd-popover-* .1s ease |
| `--animate-fd-dialog-in` / `-out` | fd-dialog-* .3s cubic-bezier(.16, 1, .3, 1) |
| `--animate-fd-sidebar-in` / `-out` | fd-sidebar-* .25s ease |
| `--animate-fd-nav-menu-in` / `-out` | fd-nav-menu-* .2s ease |
| `--animate-fd-collapsible-down` / `-up` | .15s cubic-bezier(.45, 0, .55, 1) |
| `--animate-fd-enterFromLeft` / `-Right` / `exitTo*` | .25s ease |

Most named keyframes are from Fumadocs (the docs framework). Native Langfuse animations: pulse, spin, ping, fall, accordion-up/down.

---

# 10. Components

## 10a. Detected patterns (11)

`buttons` · `cards` · `inputs` · `links` · `navigation` · `footer` · `dropdowns` · `badges` · `tabs` · `accordions` · `tooltips`

## 10b. Anatomy

| Pattern | Variants | Sizes | Instances |
|---|---|---|---|
| **button** | outline, tertiary, primary, secondary | sm, md | 40 |
| **card** | tertiary | md | 4 |
| **link** | outline | md | 2 |

Other patterns (inputs, navigation, footer, dropdowns, badges, tabs, accordions, tooltips) are detected but not anatomized — no variant or size data available.

---

# 11. Icons

| Property | Value |
|---|---|
| Detected library | **unknown** (0.00 confidence) |
| Total icons | 39 |
| Stroke-only | 20 |
| Fill-only | 7 |
| Mixed | 0 |
| Avg stroke width | 1.93px |
| Grid distribution | 24px (21) · 16px (10) · 32px (1) |
| Rounded caps fraction | 0.82 |

**Lucide is the dominant set** despite the "unknown" library detection — class names like `lucide lucide-x`, `lucide lucide-chevron-down` etc. are present. The 24px grid + 2px stroke + 82% rounded caps signature matches Lucide exactly.

## Named Lucide icons (16 unique)

| Name | Notes |
|---|---|
| x | Close |
| chevron-down | ×2 (one in form, one in dropdown) |
| layout-grid | Product / Overview |
| activity | LLM Observability |
| message-square | Prompt Management |
| flask-conical | Evaluation |
| chart-no-axes-column | Metrics |
| book-open | Documentation |
| newspaper | Blog |
| scroll-text | Changelog |
| map | Roadmap |
| users | Customers |
| bookmark | (resources) |
| graduation-cap | Education / academy |
| circle-question-mark | Help (Lucide renamed to `circle-help`) |
| copy | ×3 (code-block copy buttons) |

## Unidentified (7)

- 16px mixed style ×7 (custom logo wall marks)
- 18px fill on 32 grid (likely a brand mark)
- 18px fill on 24 grid (likely a brand mark)
- No-grid stroke 1.2 ×2 (custom illustrations)

---

# 12. Forms & inputs

| Property | Value |
|---|---|
| Forms | 1 |
| Form families | 1 |
| Input types | input (1) |
| Modals | 0 |
| Toast libraries | none |
| Skeleton loaders | 0 |
| Spinners | 0 |
| Empty states | 0 |
| Error states | 0 |

Minimal form surface — the homepage has a single newsletter-style input. The actual app (`cloud.langfuse.com`) would have many more, but that's a separate domain not covered by this extraction.

---

# 13. Accessibility

| Property | Value |
|---|---|
| WCAG score | **100%** |
| Passing pairs | 90 |
| Failing pairs | 0 |

## Pair table (top 2 by usage)

| FG | BG | Ratio | WCAG | DOM uses |
|---|---|---|---|---|
| `#3d3d38` | `#f6f6f3` | **10.09:1** | AAA | 89 |
| `#222220` | `#f6f6f3` | **14.72:1** | AAA | 1 |

Both pairs use the same card surface (#f6f6f3). The primary text on card body color (#3d3d38, text-secondary) is the workhorse — 89 detected instances.

---

# 14. SEO & brand surface

| Property | Value |
|---|---|
| OG image | https://langfuse.com/api/og?title=... (dynamic generated) |
| OG title | "Langfuse" |
| OG description | "Traces, evals, prompt management and metrics to debug and improve your LLM application." |
| Twitter card | summary_large_image |
| Twitter site | langfuse.com |
| Description | (same as OG) |
| Theme color | not set |
| Viewport | width=device-width, initial-scale=1 |
| Manifest | not set |
| Structured data | none |

## Favicons

| URL | Sizes | Type |
|---|---|---|
| /favicon.ico | (default) | shortcut icon |
| /favicon.ico | any | icon |
| /favicon-16x16.png | 16×16 | image/png |
| /favicon-32x32.png | 32×32 | image/png |
| /apple-touch-icon.png | 180×180 | apple-touch-icon |

---

# 15. Audit findings

## ⚠ Don'ts (2)

| # | Finding | Severity |
|---|---|---|
| 1 | 127 `!important` rules | **High** — prefer specificity over overrides |
| 2 | 2,452 duplicate CSS declarations | **High** — Tailwind class fragmentation likely; bundler sweep recommended |

(Designlang originally also flagged "4 font families" but the rendering of that line was incomplete in the extraction.)

## ✓ Do's (4)

| # | Finding |
|---|---|
| 1 | Use `install`, `start`, `what` as primary CTA verbs |
| 2 | Write headings in Sentence case, balanced length |
| 3 | Address the reader with you-only pronoun posture |
| 4 | Stay inside flat material — match shadow and radius habits |

## Bonus strengths (derived)

- **WCAG 100%** — all 90 detected pairs pass AAA at 10:1 or higher
- **Tight radius scale** — committed 2px + 6px only
- **No pill usage** — disciplined corner aesthetic
- **Single chromatic text token** (`--text-links` indigo) — disciplined color hierarchy

## Inferred mappings & fallbacks

- **f37 Analog** is the display face but it's licensed (Adobe Fonts / Typekit). This review falls back to **Inter** for display headings since f37 Analog can't be free-hosted. If you have a Typekit kit, you can wire it in via `@font-face`.
- **Geist Mono** is loaded via Google Fonts as the mono — matches the detected `--font-mono` chain.
- The size→family mapping (largest 3 sizes → f37 Analog) is **inferred** from family-usage counts, not directly extracted. designlang counts family usage but doesn't pair sizes to families.

---

# 16. Frameworks & integrations

## Library detection

| Aspect | Value |
|---|---|
| Detected library | **shadcn/ui** |
| Confidence | 0.65 |
| Evidence | shadcn css tokens |
| Alternates | tailwindcss (0.30) — based on 67% tailwind-like class density |
| Tailwind class density | 66.8% |
| Radix attribute count | 0 |
| Class sample size | 483 |

The site uses **shadcn/ui on top of Tailwind**, with Langfuse's own semantic role-token system overlaid. Fumadocs is also present (for the docs subpath).

## Stack intelligence

Not detected in this extraction's `stack-intel.json` — minimal data.

## LLM prompts

A `langfuse-com-prompts/` directory was generated by designlang with downstream LLM prompts for code-gen tasks.

---

# 17. Generated artifacts

| File | Purpose |
|---|---|
| `langfuse-com-DESIGN.md` | designlang's short summary |
| `langfuse-com-design-language.md` | Long-form design report with audit |
| `langfuse-com-design-tokens.json` | W3C tokens — colors, type, spacing, radii, shadows |
| `langfuse-com-variables.css` | 400+ CSS custom properties — the richest source |
| `langfuse-com-intent.json` | Page intent + 20-section reading order |
| `langfuse-com-voice.json` | Tone, CTA verbs, 28 sample headings |
| `langfuse-com-anatomy.tsx` | Component anatomy (button, card, link) |
| `langfuse-com-icon-system.json` | 39 icons, 16 named Lucide |
| `langfuse-com-visual-dna.json` | Material classification, line-grid pattern, metrics |
| `langfuse-com-motion-tokens.json` | 3 durations · 3 easings · scroll-linked |
| `langfuse-com-form-states.json` | 1 form, 1 input |
| `langfuse-com-library.json` | shadcn/ui (0.65) |
| `langfuse-com-seo.json` | OG, Twitter, 5 favicon variants |
| `langfuse-com-stack-intel.json` | (minimal) |
| `langfuse-com-mcp.json` | MCP-formatted output |
| `langfuse-com-shadcn-theme.css` | Generated shadcn CSS theme |
| `langfuse-com-tailwind.config.js` | Generated Tailwind preset |
| `langfuse-com-theme.js` | Theme JS object |
| `langfuse-com-figma-variables.json` | Figma Variables import |
| `langfuse-com-wordpress-theme.json` | WordPress theme.json |
| `langfuse-com-preview.html` | designlang's basic preview |
| `langfuse-com-prompts/` | Generated LLM prompts |
| `langfuse-design-system.html` | **This skill's polished review** |
| `DESIGN.md` | **This file** |

---

_Generated 2026-05-14 by `/extract-design-system` skill from designlang v12.10.0 output. Per-site folder: `./design-extract-output/langfuse/`._

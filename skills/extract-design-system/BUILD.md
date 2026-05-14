# BUILD.md — Detailed page-structure spec

Read this before populating `TEMPLATE.html`. It defines what goes in each section, how to derive values from the extracted artifacts, and the token-snapping rules.

---

## 1. Theme variables → `:root` and `[data-theme="dark"]`

Map directly from `*-variables.css`. The placeholders in `TEMPLATE.html` are:

| Placeholder | Source variable | Fallback if missing |
|---|---|---|
| `{{BG}}` | `--surface-1` | lightest neutral |
| `{{PANEL}}` | `--surface-bg` | `--background` (shadcn) |
| `{{PANEL_2}}` | `--surface-2` | mid neutral |
| `{{LINE}}` | `--line-structure` | `--border` (shadcn) |
| `{{LINE_2}}` | `--line-divider-dash` | `--line-structure` |
| `{{INK}}` | `--text-primary` | `--foreground` (shadcn) |
| `{{INK_2}}` | `--text-secondary` | mid-dark neutral |
| `{{INK_3}}` | `--text-tertiary` | mid neutral |
| `{{INK_4}}` | `--text-disabled` | light neutral |
| `{{ACCENT}}` | `--surface-cta-primary` or brand secondary | brand secondary |
| `{{LINK}}` | `--text-links` | accent or info |
| `{{GOOD}}` | `--callout-success` | `#22c55e` |
| `{{WARN}}` | `--callout-warning` | `#eab308` |
| `{{BAD}}` | `--callout-error` | `#ef4444` |
| `{{INFO}}` | `--callout-info` | muted indigo |
| `{{IDEA}}` | `--callout-idea` | teal |
| `{{RADIUS_CARD}}` | `--radius-md` | `6px` |
| `{{RADIUS_CONTROL}}` | `--radius-xs` | `2px` |

**Dark theme:** If the source has a native dark theme (e.g., `--dark-*` tokens), use it. Otherwise, build a Langfuse-style dark from the **code-block surfaces** (`--surface-code`, `--surface-code-grey`, `--surface-code-button`, `--line-cta`, `--text-code-secondary`).

---

## 2. Sidebar (fixed left, 248px)

```
[Brand title]               ← {{SITE_NAME}} + " Design System"
{{SCOPE_LABEL}}             ← e.g. "Corp Site" — ask once if ambiguous, default to "Corp Site"

OVERVIEW
  At a glance               → #top

FOUNDATIONS
  Colors                    → #colors
  Typography                → #typography
  Spacing                   → #spacing
  Shadows & radii           → #shadows
  Motion                    → #motion
  Icons                     → #icons        ← important: icons belong in Foundations

COMPONENTS
  Buttons                   → #comp-buttons
  Cards                     → #comp-cards
  Inputs                    → #comp-inputs
  Links                     → #comp-links
  Badges                    → #comp-badges
  Tabs                      → #comp-tabs
  Accordions                → #comp-accordions
  Tooltips                  → #comp-tooltips
  Dropdowns                 → #comp-dropdowns
  Navigation                → #comp-navigation
  Footer                    → #comp-footer

VOICE & STRUCTURE
  Voice & content           → #voice
  Page anatomy              → #layout

AUDIT
  Accessibility             → #a11y
  Audit flags               → #flags

RESOURCES
  Generated files           → #files

[v<designlang-version>]                       [◐ Theme]
```

**Pattern sub-links:** include only patterns actually present in `*-DESIGN.md` "Detected patterns" or `*-anatomy.tsx`. Drop missing ones; don't invent.

**Active section highlighting:** scrollspy via `IntersectionObserver({ rootMargin: '-20% 0px -70% 0px' })`. Active link gets the accent-color vertical tick on the left edge.

**Mobile (≤960px):** sidebar `transform: translateX(-100%)`. Hamburger button at top-left toggles `body.nav-open`. Scrim overlay closes on tap.

---

## 3. Hero

- **H1:** `font-size: clamp(38px, 6vw, <largest-detected-size>); font-weight: 500;`
- Wrap a 1–2 word emphasis (the site's product noun) in `<em>`. Style it as a **yellow highlight pill**:
  ```css
  em { background: var(--accent); padding: 0 6px; border-radius: 2px; color: var(--ink); }
  ```
  **Never use the accent as text color** — it's typically near-white on white and unreadable.
- Source line (Geist Mono, 13px): `<url> · <element-count> elements · <date>`
- Badge row (6 outlined pills): intent · library · material · imagery style · voice tone · heading case
- Stats grid (8 cells): Colors, Font families, Spacing, Shadows, Radii, Components, Icons, WCAG score. WCAG cell uses `--callout-success` if ≥90%.
- **Background:** layer the line-grid pattern from `visual-dna.json` at low opacity (~0.08) over `--panel`, plus a radial-accent glow in the top-right at ~28% alpha.

---

## 4. Colors — two-layer view

### Layer 1: Primitive palette (existing)

- **Brand colors** as large 120px-chip swatches (primary, secondary, accent)
- **Neutrals** as compact 76px swatches with usage counts
- **Patterns & gradients** panel with the detected line-grid demo + visual-DNA kv (saturation, shadow profile, avg radius, pills, backdrop blur, gradients)

### Layer 2: Tokens by context (Carbon-style)

Intro panel with **quick-jump pills** to each group, then 6 panels:

| Group | Tokens to surface | Live example |
|---|---|---|
| **Surface** | `--surface-1`, `--surface-bg`, `--surface-2`, `--surface-beige-accent`, `--surface-cta-primary`, `--surface-code`, `--surface-code-grey`, `--surface-code-button`, `--surface-button-grey` | Nested-box layering demo (page → card → sunken, with accent/yellow/dark pills inside) |
| **Text** | `--text-primary`, `--text-secondary`, `--text-tertiary`, `--text-disabled`, `--text-links`, `--text-code-secondary` | Sample paragraph with each tone in hierarchy; call out the link color as the only chromatic text token |
| **Border & line** | `--line-structure`, `--line-cta`, `--line-divider-dash`, `--line-code-border` | 4 sample cards with each border treatment |
| **Status & callout** | `--callout-success/error/warning/info/idea` | 5 Carbon-style left-border callout blocks with sample copy |
| **Code syntax** | `--text-code-orange/pink/blue`, `--color-fd-diff-add(-symbol)`, `--color-fd-diff-remove(-symbol)`, `--button-icon-color` | A highlighted code snippet on dark surface + a diff block with `+`/`−` markers |
| **Shadcn primitives** | `--primary(-foreground)`, `--secondary/--accent/--muted` (these often collapse to the same hex), `--destructive`, `--background`, `--foreground`, `--card/--popover`, `--border/--input/--ring`, `--muted-foreground` | Paired fg/bg cards showing each combination; HSL captions |

**Each group has the same scaffold:**
1. Header — group name + token count + 1-line role description
2. Live example panel
3. Compact reference table: `[swatch · token name · hex · "used for"]`

**Skip any group whose tokens aren't in the extraction.**

---

## 5. Typography

- **Font families** as outlined pills (2px radius, NOT 999px) with usage counts and a tiny progress bar. Surface the audit recommendation if >2 families ("⚠ Audit recommends limiting to 2 families").
- **Type scale rows.** Grid `96px 1fr auto`:
  - Left column (stacked): size in mono + **font family** label underneath (e.g., `68px` / `f37 Analog · display`)
  - Middle: live sample text rendered at that size. Use actual site copy where possible.
  - Right: weight · line-height · semantic role (`500 · lh 71.4 · H1`)

**Font → size mapping** (inferred — designlang counts family usage but doesn't pair sizes to families):
- Largest 3 sizes → display face if detected (e.g., f37 Analog)
- Body / UI sizes → primary body face (e.g., Inter)
- 12px mono samples → detected mono face (e.g., Geist Mono)
- Caption / eyebrow → body face

Mark the mapping as **inferred** in the section description, not directly extracted.

---

## 6. Spacing, shadows, radii, motion

- **Spacing:** each token as `lbl | bar | ratio`. Bar width = 2× spacing (capped). Use 2px-radius accent gradient.
- **Shadows:** real cards with the actual `box-shadow` values on a contrasting surface so shadows are visible.
- **Radii:** each as an 80×80 box with accent gradient. Label as `xs`, `md`, etc.
- **Motion:** 3-card grid. Each card has name + value + demo ball that transitions from left to right on hover with the actual duration + easing. Caption: feel (mixed/bouncy/snappy) + scroll-linked (yes/no).

---

## 7. Icons

- **Stats grid (6 mini-cards):** total · stroke-only · fill-only · avg stroke width · dominant grid · rounded-caps fraction
- **Lucide CDN:**
  ```html
  <script src="https://unpkg.com/lucide@latest/dist/umd/lucide.min.js"></script>
  <script>lucide.createIcons();</script>
  ```
- **Each icon:** `<i data-lucide="<name>"></i>` inside an `.icon-card` at 24px / stroke-width 2 / ink color
- **Repeated icons** get a yellow count badge (2px radius, top-right corner)
- **Renamed Lucide icons:** map known renames (e.g., `circle-question-mark` → `circle-help`) but display the original detected name as the label
- **Unidentified icons:** dimmed placeholder cards labeled with their attributes ("16px · mixed style ×7")

---

## 8. Components (live rendered, all 11 patterns)

Render every detected pattern inside a **single preview frame** (the line-grid background). Each pattern becomes a `.comp-block` with `id="comp-<name>"`, a header (name + instance count + variants + sizes), and a live example.

Skip patterns not in the extraction. For patterns with anatomy data, mirror the variants. For patterns without anatomy data, render plausible examples using the same extracted tokens.

### 11 patterns

| # | Pattern | Live example uses |
|---|---|---|
| 1 | Buttons | 4 variants (primary, secondary, tertiary, outline) × 2 sizes. Use actual CTA verbs from `voice.json` as labels. |
| 2 | Cards | 3 sample cards in a grid. Brand surface bg, soft shadow. |
| 3 | Inputs | Default (with placeholder), focused (with accent-yellow focus ring), disabled. Labeled. |
| 4 | Links | Underlined, ink color, hover state. |
| 5 | Badges | 5+ variants (accent, solid, outline, muted, status dot). 2px radius. |
| 6 | Tabs | Segmented control with active state. Inset on brand surface. |
| 7 | Accordions | Use FAQ headings from `intent.json` if available. First item open. `<details>` with `+/−` indicator. |
| 8 | Tooltips | Solid ink tooltip above a button with a caret. Static + anchored. |
| 9 | Dropdowns | Trigger button + elevated menu with kbd shortcuts (from `voice.json` button patterns). |
| 10 | Navigation | Horizontal bar: brand mark + menu + sign-in + primary CTA. Use real nav items from `intent.json` sections. |
| 11 | Footer | 4-column grid (Brand + Product/Resources/Company + copyright). Real product names from voice patterns. |

---

## 9. Voice & content

Two-column layout:

- **Left:** 5 sample headings rendered at 32px / weight 500. Wrap noun emphasis (e.g., "LLM", "developers", "agents") in yellow-pill `<em>`.
- **Right (stacked):**
  - CTA verbs as 2px-radius outlined pills with counts
  - Common button labels as pills
  - Voice metadata kv list: tone · pronoun posture · heading case · heading length · total buttons · total headings

---

## 10. Page anatomy

Linear flow of sections from `intent.json` `readingOrder`. Each row:

```
[role badge — color-coded]  [heading text]  [confidence in mono]
```

Color-code roles: accent yellow for `pricing-table` / `feature-grid` / `cta`, neutral grey for `nav` / `content` / `testimonial`, light grey for `footer`.

Caption any obvious heuristic false positives ("⚠ 6 'pricing-table' sections in a row likely indicates dense card-grid misclassification").

---

## 11. Accessibility

- Big score number. Use `--callout-success` if ≥90%, `--callout-warning` if 70–90%, `--callout-error` if <70%.
- "X passing / Y failing color pairs"
- Top 5–10 color pairs by usage. Each row: sample text rendered with the actual fg/bg, hex pair in mono, contrast ratio, pass/fail tag (AAA / AA / fail)

---

## 12. Audit flags

Two-column grid of cards. Each card:
- Left border in matching callout color (`--warn` for warnings, `--good` for strengths)
- Eyebrow label in matching color (10/600/0.1em uppercase)
- Title + explanation in ink-secondary

Pull warnings directly from the "Don'ts" section of `*-design-language.md`:
- "X font families in use" → recommend ≤2
- "X !important rules" → prefer specificity
- "X duplicate CSS declarations" → bundler/optimizer

Always include at least one strength block ("✓ Strong contrast across the board" if a11y score is high).

---

## 13. Generated files

4-column responsive grid. Each tile: 2-letter extension chip (yellow bg, ink text, 2px radius) + filename as indigo link (`--link` color). One tile per file in the output directory.

---

## 14. Footer (page bottom)

Small `<div>` with designlang version + extraction date in Geist Mono, ink-muted, centered.

---

## Snapping rules (apply everywhere)

### Radii

- **Snap everything outside the component preview to the detected scale** (typically just 2px and 6px).
- Conversion table:
  - 18px → 6px
  - 12px–14px → 6px
  - 10px → 6px
  - 8px → 6px
  - 4px → 2px
  - **999px pills → 2px** (most modern systems report `hasPill: false` in `visual-dna.json`)
- **Exception:** tiny status dots inside `.lf-badge .pip` may stay 999px (legitimate inline indicators).

### Font sizes

- Every size must exist in the detected scale (typically 10/11/12/13/14/15/16/20/32/50/68).
- **No half-pixel sizes.** Bulk-convert:
  - `10.5 → 11`, `11.5 → 12`, `12.5 → 13`, `13.5 → 13`
- Map review-chrome elements:
  - Section H2 → 32 / 500 (the H3 token)
  - Stat values → 32 / 500
  - Quotes → 32 / 500
  - Hero H1 → largest detected size / 500
  - Eyebrow / panel sub-headings → 10 / 600 / uppercase / 0.1em letter-spacing
  - Body → 13 or 14 / 400
  - Mono captions → 11 or 12

### Fonts

- Load detected primary body font + detected mono via Google Fonts.
- Replace any default mono references in the template with the detected mono.
- If the system has a custom display face that's not free, **fall back to body** and note it in the type-scale section description.

### Accent treatment

- The brand accent is typically a near-white color (yellow, lime, etc.).
- Don't use it as text — it's unreadable on light backgrounds.
- Use it as a **background highlight pill** for emphasis (yellow bg + ink text + 2px radius + 0 6px padding).
- Apply to: hero H1 `<em>`, voice quote highlights, icon count badges, file extension chips.

### Pattern background

The line-grid pattern from `visual-dna.json` should appear:
- At full opacity inside the component preview frame
- At low opacity (~0.08) layered over the hero surface

```css
background-image: repeating-linear-gradient(
  315deg,
  var(--panel),
  var(--panel) 2px,
  rgba(108, 103, 96, 0.1) 4px,
  var(--panel) 4px
);
```

---

## Page-level behaviors

- **Click-to-copy hex** on every color swatch (small `Copied <hex>` tooltip in the top-right corner)
- **Theme toggle** in the sidebar footer (light ↔ dark, via `body[data-theme]`)
- **Scrollspy** with the IntersectionObserver settings above
- **Smooth scroll** (`html { scroll-behavior: smooth }`) + `scroll-margin-top: 80px` on every section
- **Mobile drawer** with hamburger + scrim, auto-close on link tap

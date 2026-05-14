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

**Dark theme:** If the source has native dark tokens (`--dark-*`, `.dark { ... }` block, or a media-query dark scheme), use them. Otherwise, build a **code-surface-derived dark** from whatever code-block tokens the source defines (look for `--surface-code*`, `--code-bg`, `--syntax-bg`, `.hljs`, `pre` styles, etc.). If the source has no code surfaces either, fall back to a neutral inverted ramp built from the ink/surface tokens.

---

## 2. Sidebar (fixed left, 248px)

```
[Brand title]               ← {{SITE_NAME}} + " Design System"
{{SCOPE_LABEL}}             ← Optional one-line scope. Only set if a clear scope is detectable
                              (e.g. "Docs" if the URL is /docs/*, "App" if the URL is app.*).
                              For corporate root pages, leave empty rather than guessing.

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

- **H1:** `font-size: clamp(38px, 6vw, <largest-detected-size>); font-weight: <detected H1 weight>;`
- Optionally wrap a 1–2 word emphasis (the site's product noun, derived from the most-repeated noun across detected headings) in `<em>`. **Choose the emphasis treatment based on the accent's luminance:**
  - **Low-contrast accent** (near-white: yellow, lime, pale cyan — luminance > 0.75): style as a background pill so it reads against the page bg.
    ```css
    em { background: var(--accent); padding: 0 6px; border-radius: var(--radius-control); color: var(--ink); }
    ```
  - **Saturated / dark accent** (blue, red, purple, deep teal — luminance < 0.75): use directly as text color.
    ```css
    em { color: var(--accent); font-style: normal; }
    ```
  If unsure, default to the safer pill treatment (works for both).
- Source line in the detected mono family, body-small: `<url> · <element-count> elements · <date>`
- Badge row: one outlined pill per detection that's present in the extraction. Skip any whose source data is missing (e.g., no `imagery` detection → no imagery pill).
- Stats grid: one cell per non-empty category. Auto-populate from `{Colors, Font families, Spacing, Shadows, Radii, Components, Icons, WCAG score}` — drop any with count 0. WCAG cell uses `--good` if ≥90%, `--warn` 70–90%, `--bad` <70%.
- **Background:** if `visual-dna.json` `backgroundPatterns.labels` contains a pattern, layer it at ~0.08 opacity over `--panel`. Otherwise just `--panel`. Add a radial glow only if the accent is low-contrast enough to read at 28% alpha.

---

## 4. Colors — two-layer view

### Layer 1: Primitive palette (existing)

- **Brand colors** as large 120px-chip swatches (primary, secondary, accent)
- **Neutrals** as compact 76px swatches with usage counts
- **Patterns & gradients** panel with the detected line-grid demo + visual-DNA kv (saturation, shadow profile, avg radius, pills, backdrop blur, gradients)

### Layer 2: Tokens by context

Intro panel with **quick-jump pills** to each non-empty group, then one panel per group. **Detect tokens by pattern, not by exact name.** Groups are populated by scanning `*-variables.css` for variables matching the patterns below; skip any group whose patterns match nothing.

| Group | Pattern to match in `*-variables.css` | Live example |
|---|---|---|
| **Surface** | `--surface-*`, `--bg-*`, `--background*`, `--canvas*`, plus any neutral color used >50× as a background in the DOM | Nested-box layering demo: outer (page bg) → middle (card surface) → inner (sunken / hover). If multiple "layered" surfaces detected, include all. |
| **Text** | `--text-*`, `--ink-*`, `--foreground*`, `--color-text-*`, `--*-foreground` (where the role is text) | Sample paragraph with each tone shown in visual hierarchy. Call out any text token that's clearly chromatic (saturated, not in the neutral ramp) — this is usually the link color. |
| **Border & line** | `--line-*`, `--border-*`, `--divider-*`, `--ring*`, `--outline*` | One sample card per distinct border treatment (default, strong, dashed, code, etc.). |
| **Status & callout** | `--callout-*`, `--status-*`, `--alert-*`, plus any token whose name contains `success`, `error`, `warning`, `info`, `danger`, `destructive`, `idea`, `tip` | One left-border callout block per status. Skip the group entirely if the source has no status tokens. |
| **Code syntax** | `--text-code-*`, `--syntax-*`, `--hl-*`, `--code-*`, framework-specific (e.g., `--color-fd-*` for Fumadocs, `--shiki-*` for Shiki, `--prism-*` for Prism), plus diff-add/remove tokens | A syntax-highlighted snippet (use any test code) + a diff block with `+`/`−` markers. Skip if no code tokens detected. |
| **Library primitives** | `--primary*`, `--secondary*`, `--accent*`, `--muted*`, `--destructive*`, `--card*`, `--popover*`, `--input*`, `--ring*` — the shadcn naming convention. Detect by checking `library.json` for shadcn/ui or by presence of these names. | Paired fg/bg cards showing each combination. Label captions with the raw value (HSL, hex, OKLCH — whatever the source uses). |

**Each group has the same scaffold:**
1. Header — group name + token count + 1-line role description
2. Live example panel
3. Compact reference table: `[swatch · token name · raw value · "used for"]`

**Hard rule:** if a group's pattern matches nothing, omit the group entirely (including its quick-jump pill). Don't render empty groups.

---

## 5. Typography

- **Font families** as outlined pills (use `--radius-control`, never 999px unless `visual-dna.json` reports `hasPill: true`) with usage counts and a tiny progress bar. Surface the audit recommendation if >2 families (pull text from `*-design-language.md` "Don'ts" if present, otherwise default to "Consider limiting to 2 families: heading + body.").
- **Type scale rows.** Grid `96px 1fr auto`:
  - Left column (stacked): size in detected mono + inferred font family label underneath (e.g., `<largest-size>` / `<display-family> · display`)
  - Middle: live sample text rendered at that size. Use actual site copy from `intent.json` heading samples where possible.
  - Right: weight · line-height · semantic role.

**Font → size mapping** (designlang counts family usage but doesn't pair sizes to families, so this is inferred):
- Largest 3 sizes → display face if a distinct one is detected (i.e., a family with a high "all"/"heading" coverage and lower count than the body face)
- Body / UI sizes → primary body face (the family with the highest usage count)
- Mono-coded sizes (12px range, when used in `<pre>`, `<code>`) → detected mono face
- Caption / eyebrow → body face

Mark the mapping as **inferred** in the section description.

---

## 6. Spacing, shadows, radii, motion

- **Spacing:** each token as `lbl | bar | ratio`. Bar width = 2× spacing (capped). Use 2px-radius accent gradient.
- **Shadows:** real cards with the actual `box-shadow` values on a contrasting surface so shadows are visible.
- **Radii:** each as an 80×80 box with accent gradient. Label as `xs`, `md`, etc.
- **Motion:** 3-card grid. Each card has name + value + demo ball that transitions from left to right on hover with the actual duration + easing. Caption: feel (mixed/bouncy/snappy) + scroll-linked (yes/no).

---

## 7. Icons

- **Stats grid (6 mini-cards):** total · stroke-only · fill-only · avg stroke width · dominant grid · rounded-caps fraction. Omit any cell whose source data is zero.
- **Render the actual icons.** Branch on `icon-system.json.library`:
  - `lucide` → load Lucide via CDN (`https://unpkg.com/lucide@latest/dist/umd/lucide.min.js`) and render each as `<i data-lucide="<name>"></i>` inside an `.icon-card`. Map known Lucide renames (e.g., `circle-question-mark` → `circle-help`) but display the original detected name.
  - `heroicons` → load Heroicons via the same pattern (CDN or inline SVG).
  - `phosphor` / `tabler` / `feather` / other detected → use the matching CDN or inline SVGs.
  - `unknown` / `null` → render dimmed placeholder cards labeled with each icon's detected attributes (grid, stroke width, style). No CDN call.
- **Size and weight:** match the detected dominant grid (24px is common but not assumed) and `avgStrokeWidth`. Color with `--ink`.
- **Repeated icons** get a count badge using the accent color (background pill if accent is low-contrast, solid swatch otherwise).

---

## 8. Components (live render every detected pattern)

Render every pattern detected in `*-DESIGN.md`'s "Detected patterns" line + `*-anatomy.tsx` inside a **single preview frame** (the line-grid background). Each pattern becomes a `.comp-block` with `id="comp-<name>"`, a header (name + instance count + variants + sizes), and a live example.

**The catalogue is the union of all known patterns** — render whichever are detected, skip the rest. Patterns with anatomy data mirror the variants; patterns without use a plausible templated example built from the extracted tokens.

### Full pattern catalogue (26 patterns)

Grouped by role so the page-level ordering matches mental model:

#### Atoms (single-element controls)

| # | Pattern | Detection cue | Live example |
|---|---|---|---|
| 1 | **Buttons** | `<button>` density, `anatomy.tsx` Button export | 4 variants (primary, secondary, tertiary, outline) × 2 sizes. CTA verbs from `voice.json` as labels. |
| 2 | **Links** | inline `<a>` with non-nav role | Underlined, ink color, hover state. |
| 3 | **Inputs** | `<input>` types, `form-states.json` | Default (placeholder), focused (accent ring), disabled. Labeled. |
| 4 | **Textareas** | `<textarea>` detected | Multi-line input with character count, 4-row default. |
| 5 | **Selects / Comboboxes** | `<select>` or `role="combobox"` | Trigger button + popover with options. |
| 6 | **Checkboxes** | `<input type="checkbox">` | Unchecked, checked, indeterminate states. |
| 7 | **Switches / Toggles** | `role="switch"` or `<input type="checkbox" class*="switch">` | On/off with sliding thumb. |
| 8 | **Radios** | `<input type="radio">` groups | A 3-option group with one selected. |
| 9 | **Sliders / Range** | `<input type="range">` or `role="slider"` | Single-value horizontal slider with track + thumb + value bubble. |
| 10 | **Badges / Pills** | repeated small bordered labels | 5+ variants (accent, solid, outline, muted, status dot). |
| 11 | **Tags / Chips** | dismissible `<span>` clusters | With remove `×` button, optional avatar prefix. |
| 12 | **Avatars** | `<img>` with circular crop near user-name text | 3 sizes (sm/md/lg), with status dot, monogram fallback. |

#### Composites (multi-element controls)

| # | Pattern | Detection cue | Live example |
|---|---|---|---|
| 13 | **Tabs** | `role="tablist"` or `[role="tab"]` cluster | Segmented control with active state. |
| 14 | **Accordions** | `<details>` or `role="region"` toggle pattern | Use FAQ headings from `intent.json` if available. First item open. |
| 15 | **Tooltips** | `role="tooltip"` or `data-tooltip` | Solid ink tooltip above a button with caret. |
| 16 | **Dropdowns / Menus** | `role="menu"` + trigger | Trigger + elevated menu with kbd shortcuts. |
| 17 | **Modals / Dialogs** | `<dialog>` or `role="dialog"` | Centered card with backdrop, title, body, action row. |
| 18 | **Drawers / Sheets** | `role="dialog"` with `aria-orientation` or side-slide animation | Right-side panel, slide-in. |
| 19 | **Toasts / Snackbars** | `role="status"` / `role="alert"` ephemeral elements | Bottom-anchored notification card with optional action button. |
| 20 | **Banners / Alerts** | `role="banner"` or top-of-content callouts | Page-width status strip with icon + dismissible. |

#### Structures (page-level patterns)

| # | Pattern | Detection cue | Live example |
|---|---|---|---|
| 21 | **Cards** | repeating `<article>` / `<div>` with `border-radius` + padding pattern | 3 sample cards in a grid. |
| 22 | **Data tables** | `<table>` with sortable headers / pagination | 4 rows × 5 columns with sort indicators + zebra striping. |
| 23 | **Pagination** | `[aria-label*="pagination"]` or numeric link sequence | Prev / 1-5 / Next + ellipsis. |
| 24 | **Breadcrumbs** | `[role="navigation"][aria-label*="breadcrumb"]` or chevron-separated link chain | Home / Section / Subsection / Current. |
| 25 | **Navigation** | top-of-page `<nav>` with brand + links + CTA | Horizontal bar: brand mark + menu + sign-in + primary CTA. |
| 26 | **Footer** | `<footer>` element | 4-column grid (Brand + Product/Resources/Company + copyright). |

#### Feedback & status patterns (often without anatomy data)

| # | Pattern | Detection cue | Live example |
|---|---|---|---|
| 27 | **Progress bar** | `role="progressbar"` (horizontal) | Determinate bar at 60% + indeterminate variant. |
| 28 | **Spinner / loader** | `role="status"` with animation | Rotating ring at 24px and 16px. |
| 29 | **Skeleton loaders** | `aria-hidden` placeholder bars with animation | 3 bars at different widths. |
| 30 | **Empty states** | `[role="status"][aria-live]` with icon | Centered illustration + headline + CTA. |
| 31 | **Stepper / Wizard** | `[role="tablist"]` ordered + step indicators | 4-step horizontal with completed / current / future states. |
| 32 | **Date pickers** | `<input type="date">` or `role="grid"` calendars | Inline calendar view, current day highlighted. |
| 33 | **Color pickers** | `<input type="color">` or color swatches grid | Hue strip + saturation/lightness square + hex input. |

### Rendering rules

- **Detection-driven inclusion**: only render patterns whose detection cue fires. The list above is the *catalogue*; the page renders the subset.
- **Anatomy-driven variants**: if `anatomy.tsx` declares variants (`outline | primary | secondary`), render each variant. Otherwise use 1 plausible variant.
- **Use real content** where possible: button labels from `voice.json.buttonPatterns`, nav links from `intent.json` sections, FAQ items from detected FAQ section headings.
- **Snap radii** to the detected scale per the standard rule.
- **Skip if no signal**: don't render an example for a pattern just because it's in the catalogue.

### Pattern templates location

Maintain a small folder of HTML snippets — one per catalogue entry — at `skills/extract-design-system/patterns/`:

```
patterns/
├── 01-buttons.html
├── 02-links.html
├── ...
├── 22-data-table.html
├── 27-progress.html
└── 33-color-picker.html
```

Each snippet uses CSS custom properties (`var(--ink)`, `var(--accent)`, `var(--radius-card)`, etc.) so it inherits the extracted theme automatically. The skill composes the final preview frame from the snippets the detection picks.

### Sidebar sub-links

When more than 11 patterns are rendered, the sidebar's `COMPONENTS` group could get crowded. Two acceptable layouts:

- **All inline** (current): list every detected pattern under `COMPONENTS`. Sidebar scrolls if needed.
- **Sub-grouped** (recommended for 15+): split into `Atoms`, `Composites`, `Structures`, `Feedback` sub-sections within `COMPONENTS`.

---

## 9. Voice & content

Two-column layout:

- **Left:** up to 5 sample headings (from `voice.json.sampleHeadings` deduplicated) rendered at the detected H3 size and weight. Wrap noun emphasis on the most-repeated nouns across detected headings in `<em>`, styled per the accent-treatment rule (background pill if accent is low-contrast, text color if saturated). If no clearly-repeated noun, render headings plain.
- **Right (stacked):**
  - CTA verbs as outlined pills (`--radius-control`) with counts
  - Common button labels as pills
  - Voice metadata kv list: tone · pronoun posture · heading case · heading length · total buttons · total headings

---

## 10. Page anatomy

Linear flow of sections from `intent.json` `readingOrder`. Each row:

```
[role badge — color-coded]  [heading text]  [confidence in mono]
```

**Color-code roles by class, not by exact name:**
- **Marketing / action** (any role matching `cta`, `hero`, `pricing*`, `feature*`, `signup`, `subscribe`) → accent color
- **Editorial / content** (`content`, `article`, `blog-post`, `testimonial`, `quote`, `gallery`) → ink-muted neutral
- **Structural** (`nav`, `header`, `footer`, `sidebar`, `aside`, `breadcrumb`) → light neutral
- **Unrecognized** → fall back to ink-tertiary

Caption any obvious heuristic false positives **when the same role appears 4+ times in a row** with no intervening role change — this typically indicates a misclassification (e.g., dense card grids being read as repeated pricing tables). Write the caption based on what's actually detected, not a hardcoded example.

---

## 11. Accessibility

- Big score number. Use `--callout-success` if ≥90%, `--callout-warning` if 70–90%, `--callout-error` if <70%.
- "X passing / Y failing color pairs"
- Top 5–10 color pairs by usage. Each row: sample text rendered with the actual fg/bg, hex pair in mono, contrast ratio, pass/fail tag (AAA / AA / fail)

---

## 12. Audit flags

Two-column grid of cards. Each card:
- Left border in matching callout color (`--warn` for warnings, `--good` for strengths, `--bad` for errors if any)
- Eyebrow label in matching color (eyebrow-token uppercase styling)
- Title + explanation in ink-secondary

**Render whatever is actually in the extraction:**
- Pull every entry from the "Don'ts" section of `*-design-language.md` and render one card per warning. Don't hardcode specific warning categories — the extractor decides what to surface.
- Pull strengths from the "Do's" section + any high scores (WCAG ≥ 90%, single font family, all radii in detected scale, etc.).
- If the source has no Don'ts, omit the warnings column and lead with strengths.
- If the source has no Do's and no warnings, omit the section entirely.

Suggested severity classification: counts >100 of any anti-pattern → severity high; 10–100 → medium; <10 → low.

---

## 13. Generated files

4-column responsive grid. Each tile: 2-letter extension chip (yellow bg, ink text, 2px radius) + filename as indigo link (`--link` color). One tile per file in the output directory.

---

## 14. Footer (page bottom)

Small `<div>` with designlang version + extraction date in Geist Mono, ink-muted, centered.

---

## Snapping rules (apply everywhere)

### Radii

- **Snap every chrome radius to the nearest value in the detected scale** (from `design-tokens.json` `radius`). The detected scale defines the system's vocabulary — any chrome radius outside it is a violation.
- For each radius the template specifies, pick the nearest detected token. Snap *down* for ambiguous distances (a 5px target with detected 2 and 6 → snap to 2) to bias toward the squarer end, which reads as more architectural.
- **Pills (`border-radius: 999px`):** check `visual-dna.json` `hasPill`.
  - `hasPill: false` → snap pills to the largest detected token (typically 6px) or to `--radius-card`.
  - `hasPill: true` → leave 999px.
- **Exception:** tiny inline status dots (e.g., `.pip` inside `.lf-badge`) may stay circular regardless — they're inline indicators, not shapes.

### Font sizes

- **Every size must exist in the detected scale** (from `design-tokens.json` `typography` / `*-variables.css` `--text-*` and explicit heading sizes). The detected scale defines what's allowed.
- **No half-pixel sizes** — round each to the nearest detected token.
- Map review-chrome elements **by role to the detected scale**, not by absolute number:
  - Hero H1 → largest detected size, detected H1 weight
  - Section H2 → 3rd-largest detected size (or detected H3 if there are fewer than 3 display sizes), detected heading weight
  - Stat values, voice quotes → same as section H2 (or one tier smaller if H2 is already very large)
  - Eyebrow / panel sub-headings → smallest detected size, weight 600+, uppercase with `tracking-wider` letter-spacing
  - Body → detected body size (usually 14–16)
  - Mono captions → smallest body-size token (usually 11–12)

### Fonts

- Load detected primary body font + detected mono via Google Fonts.
- Replace any default mono references in the template with the detected mono.
- If the system has a custom display face that's not free, **fall back to body** and note it in the type-scale section description.

### Accent treatment

**Decide by accent luminance:**

```
luminance(accent) = 0.2126·R + 0.7152·G + 0.0722·B   (normalized 0–1)
```

- **Low-contrast accent** (luminance ≥ 0.75 — yellow, lime, pale cyan, etc.): use as a **background highlight pill**.
  ```css
  .emphasis { background: var(--accent); color: var(--ink); padding: 0 6px; border-radius: var(--radius-control); }
  ```
  Apply to: hero H1 `<em>`, voice quote highlights, icon count badges, file extension chips.

- **High-contrast accent** (luminance < 0.75 — saturated blue/red/purple/teal, dark accents): use **directly as text color**.
  ```css
  .emphasis { color: var(--accent); }
  ```
  Apply to the same elements, but as text not background.

If unsure (e.g., medium luminance ~0.5), default to background pill — it's safer because it always has a contrasting `--ink` text on top.

### Pattern background

Check `visual-dna.json` `backgroundPatterns`. **Render whatever's detected — or nothing:**

- `line-grid` (samples will be `repeating-linear-gradient(...)`) → use the actual sample string at full opacity in the component preview frame, ~0.08 opacity over the hero.
- `dot-grid` → use the detected radial-gradient or SVG pattern at the same opacities.
- `noise` → apply the detected noise filter / SVG.
- `mesh` / `svg-pattern` → embed the source.
- **No pattern detected (`labels` is empty)** → leave both the preview frame and hero as solid `--panel`. Don't invent a pattern.

Always read the actual pattern value from `backgroundPatterns.samples` rather than hardcoding angles or colors.

---

## Page-level behaviors

- **Click-to-copy hex** on every color swatch (small `Copied <hex>` tooltip in the top-right corner)
- **Theme toggle** in the sidebar footer (light ↔ dark, via `body[data-theme]`)
- **Scrollspy** with the IntersectionObserver settings above
- **Smooth scroll** (`html { scroll-behavior: smooth }`) + `scroll-margin-top: 80px` on every section
- **Mobile drawer** with hamburger + scrim, auto-close on link tap

---

## 15. Comprehensive DESIGN.md (companion reference)

Alongside the HTML, the skill writes `./design-extract-output/<site>/DESIGN.md` — a markdown reference that captures **every token, every heading, every weight, every pattern** in the extraction. The HTML is curated for review; DESIGN.md is exhaustive for handoff and AI context.

**Hard rule: if it's in the extraction, it must be in DESIGN.md.** Organize hierarchically (`In use` → `Available but unused`) rather than filtering.

### Required sections (in this order)

#### YAML frontmatter

```yaml
---
site: <Site Name>
url: <source URL>
extracted_at: <ISO date>
generator: designlang v<version>
elements_analyzed: <count>
intent: <type> (<confidence>)
library: <name> (<confidence>)
material: <flat | depth | …>
imagery: <flat-illustration | photography | …>
---
```

#### 1. Overview
- Tagline / one-liner derived from page title or hero H1
- Confidence summary: which detections were strong (>0.8) vs weak (<0.5)

#### 2. Voice
- Tone, pronoun posture, heading case, heading length class
- **Sample headings — list ALL detected headings** (not 5 — every one in `voice.json` sampleHeadings + intent.json section headings). Show with detected size/weight/section.
- **CTA verbs — full table** with counts (every entry in `voice.json` ctaVerbs)
- **Button labels — full table** with counts (every entry in `voice.json` buttonPatterns)

#### 3. Colors

Multi-tier organization. Surface everything from `*-variables.css` (often 60+ colors), not just the 16 most-used.

- **3a. Brand** (primary, secondary, accent — large emphasis)
- **3b. Semantic tokens** (the 6 Carbon-style groups: Surface, Text, Border & line, Status, Code syntax, Shadcn primitives) — list every token in each group with hex + role description
- **3c. Tailwind palette** — if `variables.css` contains `--color-{gray,slate,blue,red,green,yellow,orange,purple,rose,pink,emerald,teal,indigo,amber}-{50..900}`, list them all (these come from a Tailwind layer underneath, often unused in DOM but available to developers)
- **3d. Fumadocs / framework-specific vars** — if present (`--color-fd-*`), list them
- **3e. Full color inventory** — every unique hex detected in the DOM with usage count and detected role (text / border / background)
- **3f. Gradients** — every detected gradient (linear, radial, repeating) with the full value string

#### 4. Typography

- **Families — all detected**, with usage counts and font fallback chains from `variables.css` (e.g., `--font-sans`, `--font-mono`, `--font-analog`)
- **Type scale — full table**: every detected size, with weight, line-height, letter-spacing, inferred family, and example use. Group by role (display / heading / body / UI / caption / eyebrow / mono).
- **All weights detected** — list every numeric weight in use
- **All line-heights detected** — explicit values from `*-variables.css` (`--text-*--line-height`) plus computed leading multipliers
- **All letter-spacing values** — from `--tracking-*` variables if present
- **All headings on the actual page** — every detected heading (h1..h6) with text + size + section context (from intent.json's section headings)

#### 5. Spacing
- Base unit + full scale from `design-tokens.json`
- Tailwind spacing base (`--spacing`) if different
- Container widths (`--container-{xs,sm,md,lg,xl,2xl,3xl,4xl,5xl,6xl,7xl}`)

#### 6. Layout
- Grid containers count + flex containers count (from `design-language.md`)
- **Breakpoints** — parse from `variables.css` (`--breakpoint-*`). If designlang's `DESIGN.md` shows `[object Object]px`, the data is in the CSS — extract the real values.
- Reading order: full list of detected sections in order with role + confidence (from `intent.json`)
- Section roles tally (cta, nav, hero, feature-grid, testimonial, faq, footer, etc.)

#### 7. Shape
- Full radius scale (every value detected)
- Pill use (boolean from `visual-dna.json`)

#### 8. Elevation
- Every shadow token with full `box-shadow` value
- Z-index layers count
- Shadow profile classification (soft / sharp / directional)

#### 9. Motion
- Every duration token (xs / sm / md / lg / xl if detected)
- Every easing function with cubic-bezier values
- Springs (if any)
- Feel classification (mixed / snappy / bouncy / smooth)
- Scroll-linked animations: yes / no
- Named keyframes detected (`@keyframes` listed in CSS — pulse, spin, fade, slide, etc.)

#### 10. Components
- Every detected pattern from `DESIGN.md`'s "Detected patterns" line
- For each: anatomy block (variants, sizes, instance count) if present in `anatomy.tsx`
- Mark patterns without anatomy data as "detected but not anatomized"

#### 11. Icons
- Library detection + confidence
- Stats: total, stroke-only, fill-only, mixed, avg stroke width, grid distribution, rounded-caps fraction
- Full named icon list (e.g., every Lucide name) with grid + stroke-width + style per icon
- Unidentified icons list with their detected attributes

#### 12. Forms & inputs
- Form count, families
- Input types detected
- Modals, toast libraries
- Loading states (skeleton/spinner counts)
- Empty states, error states

#### 13. Accessibility
- WCAG score
- Passing / failing pair counts
- **Full pair table** (not top 2): every detected fg/bg combination with contrast ratio, WCAG tag (AAA/AA/fail), and DOM usage count

#### 14. SEO & brand surface
- Favicons (every size from `seo.json`)
- OG image, Twitter card
- Description, theme color, manifest
- Apple touch icons

#### 15. Audit findings
- **Full "Do's"** list from `*-design-language.md` (not just the 4 we surfaced in flags)
- **Full "Don'ts"** list with severity inferred from counts (e.g., 127 !important = high; 4 fonts = medium; 2 unused tokens = low)
- Strengths (high WCAG score, etc.)

#### 16. Frameworks & integrations
- Detected library (shadcn confidence + evidence)
- Tailwind class density (from `library.json` signals)
- Tech stack (from `stack-intel.json` if present)
- LLM prompts available (count from `*-prompts/`)

#### 17. Generated artifacts
- Full list of every file in the per-site folder with one-line purpose

### Length expectation

For a typical marketing site, DESIGN.md should land in the **400–800 line range**. The langfuse extraction produces ~600 lines. If your output is under 200 lines, you're filtering too aggressively — re-read `*-variables.css` and surface what you missed.

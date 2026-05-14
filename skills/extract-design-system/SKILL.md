---
name: extract-design-system
description: "Extract a website's design language. Turn it into a polished, self-referential design system page"
allowed-tools: Bash, Read, Write, Edit, Glob
---

# Extract Design System

Run a full design-language extraction on a URL **and** generate a polished, self-styled review page. The output is one HTML file that documents the site's design system using that system's own tokens — so the page is its own evidence the system works.

## Process

**1. Run the raw extraction into a per-site folder.**

Each site gets its own folder under `./design-extract-output/` so artifacts from different runs never mix. Use the brand name (no TLD) as the folder name — `langfuse.com` → `langfuse/`, `vercel.com` → `vercel/`, `shopify.com` → `shopify/`.

```bash
npx designlang <url> --screenshots --out ./design-extract-output/<site>/
```

Add `--depth 3` for multi-page crawling. Add `--dark` for dark-mode parity.

**2. Read every relevant artifact in `./design-extract-output/<site>/`** before writing the review:

| File | What to extract |
|---|---|
| `*-DESIGN.md` | Intent, library, material, voice (high-level summary) |
| `*-design-tokens.json` | Type scale, spacing, radii, shadows, font families |
| `*-variables.css` | **The richest source** — semantic role tokens (surface, text, line, callout, code-syntax, shadcn primitives) |
| `*-intent.json` | Section roles + detected reading order |
| `*-voice.json` | Tone, headings, CTA verbs, button label patterns |
| `*-anatomy.tsx` | Component variants + instance counts |
| `*-icon-system.json` | Detected Lucide icons + attributes |
| `*-visual-dna.json` | Material language, imagery style, pattern detection |
| `*-motion-tokens.json` | Duration + easing tokens |
| `*-library.json` | Component library detection (shadcn, etc.) |
| `*-design-language.md` | Audit warnings (font count, !important, duplicate CSS) |

**3. Build the design-system HTML** by copying `TEMPLATE.html` to `./design-extract-output/<site>/<site>-design-system.html` and replacing every `{{TOKEN}}` placeholder with values from the extracted files. **Do not modify `*-preview.html`** — leave it in place as the basic reference.

The full page structure, token mapping, snapping rules, and copy decisions are in **[BUILD.md](./BUILD.md)** — read it before populating the template.

**4. Write a comprehensive `DESIGN.md`** at `./design-extract-output/<site>/DESIGN.md` (no `<site>-` prefix — the folder names the site). This is the canonical, machine-readable design-system reference. It must be **exhaustive** — surface every token from the extraction, not just curated highlights. designlang's `<slug>-DESIGN.md` is a short summary; ours is the full reference. See **[BUILD.md §15](./BUILD.md)** for the complete content spec.

The general rule: **if the extraction contains a token, color, heading, weight, breakpoint, or pattern, it must appear in DESIGN.md** — organized so "in use" data leads and "available but unused" data follows. Don't filter for top-N. The HTML page can curate; DESIGN.md cannot.

Any inferred mappings, font fallbacks, or other decisions that weren't directly extracted should be **noted inline in DESIGN.md** (typically in the §1 Overview, §14 fallbacks, or §15 Audit findings sections) — not split into a separate CHANGELOG file.

## What this skill never inserts

- **No logos, marks, or brand-glyphs anywhere.** No sidebar mark, no nav-brand swatch, no footer brand mark, no `<img>` of the source logo. Use the brand name as plain text. The site identity comes from tokens (color, type, spacing, radii) — not from a recreated wordmark.
- **No synthesized decoration on the hero** (radial accent glows, repeating staff lines, oblique stripes, conic shapes). Decoration must come from a detected source feature — see BUILD.md §3.
- **No invented inline emphasis** in headings. No "make one word colored" unless the source actually paints it that way — see SKILL.md Accent treatment.
- **No white card chrome** when the painted source doesn't use it. Surface tiebreaker in BUILD.md §4 decides.

## Core decisions (baked in — do not re-ask)

These are the choices that make the output a coherent design-system page rather than a token dump:

- **Sidebar:** fixed left, 248px, with grouped section labels. Active section highlighted via scrollspy. Mobile → hamburger drawer.
- **Default theme:** match the source site's detected default (light or dark, based on `body.classList`, `data-theme`, or `prefers-color-scheme`).
- **Pattern depth:** render every component pattern that's *actually detected* (anatomy.tsx + detected-patterns line), not a fixed list. Skip patterns the extractor didn't find.
- **Color organization:** primitive palette (Brand / Neutrals / Patterns) **plus** tokens-by-context. Detect groups by token-name pattern (`--surface-*`, `--text-*`, `--line-*`, etc.) — omit any group with zero matches.
- **Icons:** real rendered SVGs from whatever library `icon-system.json` detected. Fall back to dim placeholder cards if the library is unknown.
- **Type scale:** show font family per row, inferred from family usage counts. Mark the mapping as inferred.
- **Radii:** snap every chrome radius to the nearest value in the **detected** scale — don't hardcode 2/6. Replace 999px pills with the largest detected radius *only if* `visual-dna.json` reports `hasPill: false`.
- **Typography snap:** every font size must be in the detected scale. No half-pixel sizes. Map review-chrome by role (hero = largest, section h2 = 3rd-largest, eyebrow = smallest) rather than by absolute number.
- **Accent treatment:** the accent only appears where the *source* uses it (detected emphasis in headings, accent-colored buttons in the DOM, etc.) — don't synthesize emphasis. When the accent IS placed, pick between text-color vs background-fill by WCAG contrast ratio: whichever pairing passes AA wins; both pass → prefer text color (smaller footprint); neither passes → pick the higher and flag it.

## Painted-DOM-first principle

**Always look at what the source actually paints, not just at the named tokens.** A site can declare `--color-primary` and barely paint it; another can declare nothing and paint blue everywhere. The cascade is the contract; the painted DOM is the truth.

For every role token the demo needs (`--bg`, `--panel`, `--ink`, `--line`, `--accent`, hero surface, etc.), the resolution order is:

1. **Count what's painted** in the source DOM (`background-color`, `color`, `border-color`).
2. **Compare** the most-painted value for that role against the named token value.
3. **Prefer the painted value when they disagree** — and record the decision in DESIGN.md §15 with both counts so the call is auditable.

The detailed tiebreaker per role (surface, panel, ink, line, accent, hero surface) lives in **[BUILD.md §4 — DOM-frequency tiebreaker](./BUILD.md#4-colors--two-layer-view)**. The rules there are derived from the extraction — relative counts, painted-vs-named comparisons, saturation tests — not from hardcoded thresholds or site-specific values.

**Two consequences of this principle that the demos repeatedly need:**

- **No synthesized white card chrome.** If the painted DOM doesn't show a distinct elevated card surface, the demo's `--panel` resolves to `--bg`. Content sits flat. Pure white `#ffffff` is a *Notion-default*, not a universal.
- **No synthesized decoration.** Radial gradients, repeating-line patterns, oblique stripes, conic shapes — none of these belong in the demo unless they're detected as a real source pattern (in `visual-dna.json` `backgroundPatterns` or as a tokenized feature like Mistral's footer band). Generic "make the hero feel designed" flourishes are creative invention, not extraction.

## Trigger phrases

`extract design system`, `generate design system review`, `design system audit`, `review-grade design docs`, `/extract-design-system`, `turn this extraction into a design system page`, `make a Carbon-style design review`

## Files in this skill

- `SKILL.md` (this file) — entry point + core decisions
- `BUILD.md` — detailed page structure spec, section-by-section
- `TEMPLATE.html` — pre-built HTML scaffold with `{{TOKEN}}` placeholders

## Output

All output lives inside a per-site folder so multiple extractions never mix:

```
./design-extract-output/
└── <site>/                              ← brand name, no TLD
    ├── <site>-design-system.html        ← Primary visual output (curated)
    ├── DESIGN.md                        ← Comprehensive reference (every token)
    ├── <slug>-DESIGN.md                 ← designlang's short summary (kept)
    ├── <slug>-design-tokens.json
    ├── <slug>-variables.css
    ├── <slug>-preview.html              ← basic preview (untouched)
    └── ... (18 more designlang artifacts)
```

`<site>` is the brand name (e.g. `langfuse`). `<slug>` is designlang's prefix for individual artifacts (e.g. `langfuse-com`).

## What this skill does NOT do

- Does not modify `*-preview.html`. The basic preview stays in place.
- Does not invent tokens. If a category isn't in the extraction, that section is omitted.
- Does not load proprietary display fonts (e.g., custom-licensed faces). Falls back to the body font and flags the gap.

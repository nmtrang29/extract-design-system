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

**4. Write an optional `CHANGELOG.md`** alongside the review (at `./design-extract-output/<site>/CHANGELOG.md`) documenting which choices were derived from the extraction and which had to fall back (e.g., custom display fonts that aren't free-to-host). No `<site>-` prefix needed — the folder already names the site.

## Core decisions (baked in — do not re-ask)

These are the choices that make the output a coherent design-system page rather than a token dump:

- **Sidebar:** fixed left, 248px, with grouped section labels. Active section highlighted via scrollspy. Mobile → hamburger drawer.
- **Default theme:** match the source site (most marketing sites are light by default).
- **Pattern depth:** render *every* detected component pattern with live examples, not just the 3 with full anatomy data.
- **Color organization:** primitive palette (Brand / Neutrals / Patterns) **plus** Carbon-style tokens-by-context with 6 groups (Surface, Text, Border, Status, Code, Shadcn primitives).
- **Icons:** real rendered SVGs via the Lucide CDN, not a text list.
- **Type scale:** show font family per row (inferred from family usage counts).
- **Radii:** snap every chrome radius to the detected scale (typically 2px + 6px only). Replace all 999px pills with 2px.
- **Typography snap:** every font size must exist in the detected scale. Bulk-convert half-pixel sizes.
- **Accent treatment:** brand accent (typically a bright yellow) used as a **background highlight pill**, never as text color.

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
    ├── <site>-design-system.html        ← Primary output
    ├── <slug>-DESIGN.md                 ← designlang summary
    ├── <slug>-design-tokens.json
    ├── <slug>-variables.css
    ├── <slug>-preview.html              ← basic preview (untouched)
    ├── ... (18 more designlang artifacts)
    └── CHANGELOG.md                     ← optional provenance log
```

`<site>` is the brand name (e.g. `langfuse`). `<slug>` is designlang's prefix for individual artifacts (e.g. `langfuse-com`).

## What this skill does NOT do

- Does not modify `*-preview.html`. The basic preview stays in place.
- Does not invent tokens. If a category isn't in the extraction, that section is omitted.
- Does not load proprietary display fonts (e.g., custom-licensed faces). Falls back to the body font and flags the gap.

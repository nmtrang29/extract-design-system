# extract-design-system

A fork of [design-extract](https://github.com/Manavarya09/design-extract) that turns the raw extraction output into a **polished, self-referential design-system review page** — a single HTML file that uses the extracted tokens to style itself.

> **Principle:** a design-system page should be evidence of the system it documents.
> If the page uses 12px radii while documenting a 6px-only system, it contradicts itself. Snapping the chrome to the extracted tokens makes the page self-validating — every element you see is also a token in the reference table below it.

![Hero screenshot](docs/before-after/hero-after.png)

[**▶ See the live example: langfuse-design-system.html**](examples/langfuse-design-system.html)

---

## What's different from `design-extract`

| Topic | Change | Before | After |
|---|---|---|---|
| **Page styling** | Self-referential / dogfooded. The page chrome (background, borders, radii, type scale, mono font, accent treatment) is built from the *same tokens* it documents — proving the system works in production. | <img src="docs/before-after/page-styling-before.png" width="300" /> | <img src="docs/before-after/page-styling-after.png" width="300" /> |
| **Colors** | Two-layer view: primitive palette **+** Carbon-style tokens-by-context (Surface, Text, Border, Status, Code, Shadcn primitives — each with live examples + reference table). | <img src="docs/before-after/colors-before.png" width="300" /> | <img src="docs/before-after/colors-after.png" width="300" /> |
| **Nav** | Fixed left sidebar (Carbon / Polaris / shadcn convention). Active section highlighted via scrollspy. Mobile collapses to hamburger drawer with scrim. | <img src="docs/before-after/nav-before.png" width="300" /> | <img src="docs/before-after/nav-after.png" width="300" /> |
| **Icons (rendering)** | Real SVGs via the Lucide CDN, not text names. Repeated icons get a usage-count badge. Designers can finally evaluate stroke width, optical alignment, and style coherence. | <img src="docs/before-after/icons-before.png" width="300" /> | <img src="docs/before-after/icons-after.png" width="300" /> |
| **Icons (IA)** | Moved into the Foundations group (icons are foundational, not compositional). | — | see Nav screenshot |
| **Components** | Render *every* detected pattern (Langfuse: all 11 — Buttons, Cards, Inputs, Links, Badges, Tabs, Accordions, Tooltips, Dropdowns, Navigation, Footer), not just the 3 with full anatomy data. | <img src="docs/before-after/components-before.png" width="300" /> | <img src="docs/before-after/components-after.png" width="300" /> |
| **Naming** | Renamed sidebar group **Library → Components**, the term used by Carbon, Material, Polaris, and shadcn itself. | — | see Nav screenshot |
| **Typography** | Each type-scale row labels which font is used (display vs body vs UI vs code). Surfaces inconsistencies designers couldn't spot before. | <img src="docs/before-after/typography-before.png" width="300" /> | <img src="docs/before-after/typography-after.png" width="300" /> |
| **Theme** | Default theme matches the source site, not Claude's preference. Langfuse is light, so the review opens light. Dark mode rebuilt from the system's own code-block surfaces (`#222220`, `#333`, `#404039`) instead of generic devtools greys. | <img src="docs/before-after/theme-before.png" width="300" /> | <img src="docs/before-after/theme-after.png" width="300" /> |

---

## Installation

This is a Claude Code skill. Symlink it into your Claude config:

```bash
git clone https://github.com/nmtrang29/extract-design-system.git
cd extract-design-system
ln -s "$(pwd)/skills/extract-design-system" ~/.claude/skills/extract-design-system
```

Verify by typing `/extract-design-system` in Claude Code — the skill should appear in the available list.

**Prerequisites:**

- [`designlang`](https://www.npmjs.com/package/designlang) (`npm i -g designlang`, or use via `npx`)
- Network access for Lucide CDN + Google Fonts (Inter + Geist Mono)

---

## Usage

```bash
# In Claude Code
/extract-design-system https://yoursite.com/
```

This will:

1. Run `npx designlang <url> --screenshots` to produce 22 raw extraction artifacts
2. Read every relevant artifact (`*-variables.css`, `*-design-tokens.json`, `*-intent.json`, `*-voice.json`, etc.)
3. Populate `skills/extract-design-system/TEMPLATE.html` with the extracted values
4. Save the result as `<site>-design-system.html` (brand name only, no TLD — e.g. `langfuse-design-system.html`)
5. Optionally write a `CHANGELOG.md` documenting any inferred mappings or fallbacks

---

## Output

```
design-extract-output/
├── <site>-design-system.html   ← the polished design-system page (what this skill adds, e.g. langfuse-design-system.html)
├── <slug>-preview.html         ← the basic preview from designlang (left in place)
├── <slug>-DESIGN.md
├── <slug>-design-tokens.json
├── <slug>-variables.css        ← richest semantic-token source
├── <slug>-intent.json
├── <slug>-voice.json
├── <slug>-anatomy.tsx
├── <slug>-icon-system.json
├── <slug>-visual-dna.json
├── <slug>-motion-tokens.json
├── ... (12 more designlang artifacts)
└── CHANGELOG.md                ← optional provenance log
```

---

## How it works

The skill is composed of three files in `skills/extract-design-system/`:

| File | Role |
|---|---|
| [`SKILL.md`](skills/extract-design-system/SKILL.md) | Entry point. Defines the process, core decisions, and trigger phrases. |
| [`BUILD.md`](skills/extract-design-system/BUILD.md) | Detailed page-structure spec. Section-by-section content, token mapping table, snapping rules. |
| [`TEMPLATE.html`](skills/extract-design-system/TEMPLATE.html) | Pre-built HTML scaffold with `{{TOKEN}}` placeholders and `<!-- INSERT_*_HERE -->` regions. |

The AI (Claude Code) reads `SKILL.md`, follows the process, references `BUILD.md` for detailed rules, and populates `TEMPLATE.html` with the extracted values — instead of regenerating 2000+ lines of HTML from natural-language instructions every run.

---

## Locked-in choices (no clarifying questions)

These are decisions baked into the skill — running it always produces a coherent design-system page, not a token dump:

- **Sidebar**: fixed left, 248px, scrollspy active highlight, hamburger on mobile
- **Default theme**: matches the source site
- **Pattern depth**: render every detected component pattern with live examples
- **Colors**: primitive palette **+** Carbon-style tokens-by-context (6 groups)
- **Icons**: real SVGs via Lucide CDN, with usage counts
- **Type scale**: show font family per row
- **Radii**: snap chrome to the detected scale (typically 2px + 6px only); replace 999px pills with 2px
- **Typography**: bulk-snap half-pixel sizes to the detected scale
- **Accent**: use as a background highlight pill, never as text color

See [`SKILL.md`](skills/extract-design-system/SKILL.md) for the full list.

---

## Known limitations

- **Custom display fonts** (e.g., f37 Analog, GT America) aren't auto-loaded. Headings fall back to the primary body face. Wire them in via `@font-face` from the site's CDN if you want full fidelity.
- **Requires network** for the Lucide CDN and Google Fonts. For offline use, swap icon rendering for inline SVG paths and host the fonts locally.
- **The component preview** for patterns without anatomy data uses plausible examples — not extracted markup. Inputs, badges, tabs, etc. are rendered with the same tokens but the structure is templated.

---

## Credits

- Forked from [Manavarya09/design-extract](https://github.com/Manavarya09/design-extract) — the underlying `designlang` extractor.
- Colors-by-context layout inspired by [Carbon Design System](https://carbondesignsystem.com/elements/color/overview/).
- Reference output: built against [langfuse.com](https://langfuse.com/) during a multi-iteration design session — see [`examples/langfuse-design-system.html`](examples/langfuse-design-system.html) and [`examples/langfuse-CHANGELOG.md`](examples/langfuse-CHANGELOG.md).

---

## License

MIT — see [LICENSE](LICENSE). Inherits from the upstream `design-extract` project.

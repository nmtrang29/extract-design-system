# extract-design-system

A Claude Code skill built on top of [`designlang`](https://www.npmjs.com/package/designlang) that turns any website URL into a polished, self-referential design system page.

> **Principle:** a design-system page should be evidence of the system it documents. If the page uses 12px radii while documenting a 6px-only system, it contradicts itself. Snapping the chrome to the extracted tokens makes every element on the page also a token in the reference table below it.

**Two outputs per site:**
+ An HTML design system page styled with the extracted tokens
+ A `DESIGN.md` cataloguing every detected token, heading, weight, breakpoint, and pattern (400–800 lines)

---

## Live demos

[→ **nmtrang29.github.io/extract-design-system**](https://nmtrang29.github.io/extract-design-system/) — landing page

<table>
<tr>
<td width="25%" align="center"><a href="https://nmtrang29.github.io/extract-design-system/examples/langfuse/langfuse-design-system.html"><b>▶ Langfuse</b></a></td>
<td width="25%" align="center"><a href="https://nmtrang29.github.io/extract-design-system/examples/ableton/ableton-design-system.html"><b>▶ Ableton</b></a></td>
<td width="25%" align="center"><a href="https://nmtrang29.github.io/extract-design-system/examples/claude/claude-design-system.html"><b>▶ Claude</b></a></td>
<td width="25%" align="center"><a href="https://nmtrang29.github.io/extract-design-system/examples/utrecht/utrecht-design-system.html"><b>▶ Utrecht</b></a></td>
</tr>
<tr>
<td><a href="https://nmtrang29.github.io/extract-design-system/examples/langfuse/langfuse-design-system.html"><img src="docs/before-after/langfuse/hero-after.png" alt="Langfuse demo — warm beige, yellow accent, shadcn" /></a></td>
<td><a href="https://nmtrang29.github.io/extract-design-system/examples/ableton/ableton-design-system.html"><img src="docs/before-after/ableton/hero.png" alt="Ableton demo — brutalist, 0 radii, custom CSS" /></a></td>
<td><a href="https://nmtrang29.github.io/extract-design-system/examples/claude/claude-design-system.html"><img src="docs/before-after/claude/tokens-by-context.png" alt="Claude demo — tokens by context section" /></a></td>
<td><a href="https://nmtrang29.github.io/extract-design-system/examples/utrecht/utrecht-design-system.html"><img src="docs/before-after/utrecht/hero.png" alt="Utrecht demo — minimal red on white, gray hairlines, Shopify storefront" /></a></td>
</tr>
<tr>
<td align="center"><sub>shadcn · warm beige · yellow</sub></td>
<td align="center"><sub>brutalist · 0 radii · custom CSS</sub></td>
<td align="center"><sub>Source Serif · clay-orange · Tailwind</sub></td>
<td align="center"><sub>minimal · red on white · 4 colors</sub></td>
</tr>
</table>

Each demo ships with a [`DESIGN.md`](examples/langfuse/DESIGN.md) — the comprehensive token reference.

---

## Installation

**Prerequisite:** [`designlang`](https://www.npmjs.com/package/designlang) — `npm i -g designlang` (or use `npx designlang` on first run).

The skill is just three files (`SKILL.md` + `BUILD.md` + `TEMPLATE.html`). The path differs by AI agent:

### Claude Code (native plugin)

```
/plugin install nmtrang29/extract-design-system
```

Verify by typing `/extract-design-system` — should appear in the available skills list.

### Claude Code (manual fallback)

```bash
git clone https://github.com/nmtrang29/extract-design-system.git
ln -s "$(pwd)/extract-design-system/skills/extract-design-system" \
      ~/.claude/skills/extract-design-system
```

### OpenAI Codex / `AGENTS.md` convention

```bash
git clone https://github.com/nmtrang29/extract-design-system.git .skills/extract-design-system

# Then add to your project's AGENTS.md:
cat >> AGENTS.md <<'EOF'
## Skill: extract-design-system
When the user asks to "extract design system" or invokes
`/extract-design-system`, follow:
- `.skills/extract-design-system/skills/extract-design-system/SKILL.md`
- `.skills/extract-design-system/skills/extract-design-system/BUILD.md`
- `.skills/extract-design-system/skills/extract-design-system/TEMPLATE.html`
EOF
```

### Cursor / `.cursorrules`

```bash
git clone https://github.com/nmtrang29/extract-design-system.git .tmp-eds
cat .tmp-eds/skills/extract-design-system/SKILL.md >> .cursorrules
```

### Any AI coding agent (generic)

Point the agent at the SKILL.md URL:

```
@https://github.com/nmtrang29/extract-design-system/blob/main/skills/extract-design-system/SKILL.md

Please follow this skill to extract a design system from https://yoursite.com/.
```

---

## Usage

```bash
/extract-design-system https://yoursite.com/
```

This will:

1. Run `npx designlang <url> --screenshots` to produce the raw extraction artifacts into a per-site folder
2. Read every relevant artifact (`*-variables.css`, `*-design-tokens.json`, `*-intent.json`, `*-voice.json`, `*-anatomy.tsx`, `*-icon-system.json`, `*-visual-dna.json`, etc.)
3. Populate `TEMPLATE.html` with the extracted values per the rules in `BUILD.md`
4. Save the polished page at `./design-extract-output/<site>/<site>-design-system.html`
5. Write a comprehensive `DESIGN.md` (400–800 lines) alongside — every detected token, heading, weight, breakpoint, pattern. Inferred mappings and font fallbacks are noted inline.

---

## Output structure

Each website gets its own folder so artifacts from different runs never mix:

```
design-extract-output/
├── langfuse/
│   ├── langfuse-design-system.html    ← polished review (what this skill adds)
│   ├── DESIGN.md                      ← comprehensive reference (what this skill adds)
│   ├── langfuse-com-preview.html      ← basic designlang preview (left in place)
│   ├── langfuse-com-DESIGN.md
│   ├── langfuse-com-variables.css     ← richest semantic-token source
│   ├── langfuse-com-design-tokens.json
│   ├── ... (18 more designlang artifacts)
├── vercel/
└── shopify/
```

Folder name = brand only, no TLD (`langfuse.com → langfuse/`, `vercel.com → vercel/`).

---

## How it works

The skill is composed of three files in `skills/extract-design-system/`:

| File | Role |
|---|---|
| [`SKILL.md`](skills/extract-design-system/SKILL.md) | Entry point. Process steps, core decisions, trigger phrases. |
| [`BUILD.md`](skills/extract-design-system/BUILD.md) | Detailed page-structure spec — section-by-section content, token mapping table, snapping rules, 17 DESIGN.md required sections. |
| [`TEMPLATE.html`](skills/extract-design-system/TEMPLATE.html) | Pre-built HTML scaffold with `{{TOKEN}}` placeholders + `<!-- INSERT_*_HERE -->` regions. Claude fills it in instead of generating 2000+ lines from scratch each run. |

Claude reads `SKILL.md`, follows the process, references `BUILD.md` for detailed rules, populates `TEMPLATE.html` with the extracted values.

---

## What's different from designlang's basic preview

### Page styling

Self-referential. The page chrome (background, borders, radii, type scale, mono font, accent treatment) is built from the *same tokens* it documents. Fixed left sidebar with scrollspy. Mobile collapses to hamburger drawer.

<table>
<tr><td width="50%" align="center"><sub><b>Before</b></sub></td><td width="50%" align="center"><sub><b>After</b></sub></td></tr>
<tr>
<td><img src="docs/before-after/langfuse/page-styling-before.png" alt="Before — generic devtools dashboard styling" /></td>
<td><img src="docs/before-after/langfuse/page-styling-after.png" alt="After — styled with the extracted tokens" /></td>
</tr>
</table>

### Colors

Two-layer view: primitive palette **+** Carbon-style tokens-by-context (surface, text, border, status, code, library primitives — each with live examples + reference table).

<table>
<tr><td width="50%" align="center"><sub><b>Before</b></sub></td><td width="50%" align="center"><sub><b>After</b></sub></td></tr>
<tr>
<td><img src="docs/before-after/langfuse/colors-before.png" alt="Before — flat swatch grid sorted by usage count" /></td>
<td><img src="docs/before-after/langfuse/colors-after.png" alt="After — primitive palette plus Carbon-style tokens-by-context" /></td>
</tr>
</table>

### Components

Render *every* detected pattern with live examples that use the actual extracted tokens — not just the canonical 3 with full anatomy data.

<table>
<tr><td width="50%" align="center"><sub><b>Before</b></sub></td><td width="50%" align="center"><sub><b>After</b></sub></td></tr>
<tr>
<td><img src="docs/before-after/langfuse/components-before.png" alt="Before — empty components section" /></td>
<td><img src="docs/before-after/langfuse/components-after.png" alt="After — all 11 detected patterns rendered live with extracted tokens" /></td>
</tr>
</table>

### Icons

Real rendered SVGs (Lucide via CDN by default; adapters for Heroicons / Octicons / Material Symbols / Bootstrap / Tabler / Phosphor / Feather / Carbon / Spectrum / SLDS / Radix / Ant on open PR #3). Repeated icons get a usage-count badge.

<table>
<tr><td width="50%" align="center"><sub><b>Before</b></sub></td><td width="50%" align="center"><sub><b>After</b></sub></td></tr>
<tr>
<td><img src="docs/before-after/langfuse/icons-before.png" alt="Before — no rendered icons section" /></td>
<td><img src="docs/before-after/langfuse/icons-after.png" alt="After — real Lucide SVGs with usage badges" /></td>
</tr>
</table>

### Typography

Each type-scale row labels which font is used (display vs body vs UI vs code) — even when designlang doesn't pair sizes to families directly.

<table>
<tr><td width="50%" align="center"><sub><b>Before</b></sub></td><td width="50%" align="center"><sub><b>After</b></sub></td></tr>
<tr>
<td><img src="docs/before-after/langfuse/typography-before.png" alt="Before — type scale without font column" /></td>
<td><img src="docs/before-after/langfuse/typography-after.png" alt="After — type scale with font family per row" /></td>
</tr>
</table>

### Theme

Default theme matches the source site, not Claude's preference. Langfuse opens light; Ableton opens light; the skill detects from `body.classList`, `data-theme`, or `prefers-color-scheme`. Dark mode rebuilt from the source's own code-block surfaces when no native dark theme is detected.

---

## Baked-in decisions

Choices that make the output a coherent design-system page rather than a token dump:

- **Sidebar:** fixed left, 248px, scrollspy active highlight, hamburger on mobile
- **Default theme:** matches the source site's detected default
- **Pattern depth:** render every detected component pattern with live examples (not a fixed list)
- **Colors:** primitive palette + Carbon-style tokens-by-context across 6 role groups
- **Icons:** real rendered SVGs from whatever library is detected
- **Type scale:** show font family per row (inferred from family usage counts)
- **Radii:** snap every chrome radius to the **detected** scale — no hardcoded values
- **Typography:** snap to detected scale; no half-pixel sizes
- **Accent treatment:** decide by luminance — near-white accents → background pill, saturated accents → text color directly
- **Per-site folders:** outputs never mix between extractions

See [`SKILL.md`](skills/extract-design-system/SKILL.md) for the full list.

---

## Roadmap (open PRs)

Tested against the [Open UI design-systems list](https://open-ui.org/design-systems/) and found gaps. Four PRs open to broaden coverage:

| PR | What | Tested on |
|---|---|---|
| [#1](https://github.com/nmtrang29/extract-design-system/pull/1) | **Token-name pattern broadening + DOM-frequency tiebreaker** — handles Carbon (`--cds-*`), Spectrum (`--spectrum-*`), Material 3 (`--md-sys-*`), Primer (`--bgColor-*`), USWDS, Ant, MUI, etc. Plus a tiebreaker that prefers DOM-observed colors when named tokens disagree with what's painted. | primer.style, utrecht.jp |
| [#2](https://github.com/nmtrang29/extract-design-system/pull/2) | **Docs-site detection / audit mode** — when pointed at a design-system docs site (mui.com, carbondesignsystem.com), the skill enters audit mode with a banner + Detected-token-sources section instead of describing the docs UI as if it were the design system. | mui.com (simulated) |
| [#3](https://github.com/nmtrang29/extract-design-system/pull/3) | **14 icon-library adapters** — Octicons, Carbon Icons, Material Symbols, Bootstrap Icons, Ant Icons, Tabler, Phosphor, Feather, SLDS, Spectrum Workflow, Radix, Atlaskit. Currently only Lucide renders natively; others fall back to placeholders. | Primer, Material UI, Bootstrap |
| [#4](https://github.com/nmtrang29/extract-design-system/pull/4) | **Pattern catalogue 11 → 33** — adds toasts, data tables, pagination, switches, sliders, avatars, breadcrumbs, modals, drawers, skeletons, empty states, steppers, date pickers, color pickers, etc. Detection-driven inclusion. | (catalogue spec) |

After all four merge, the skill should produce credible output for ~22 of the 27 listed Open UI design systems.

---

## Known limitations

- **Custom display fonts** (e.g., f37 Analog, GT America, Söhne, Adobe Clean) aren't auto-loaded. Headings fall back to the primary body face — wire them in via `@font-face` from the source's CDN if you want full fidelity.
- **Requires network access** for the Lucide CDN and Google Fonts. For offline use, swap icon rendering for inline SVG paths and host fonts locally.
- **Component examples for patterns without anatomy data** use templated rendering — not extracted markup. Inputs, badges, tabs, etc. reflect the system's tokens but the structure is generic.
- **Not pixel-deterministic.** Re-running on the same site produces a structurally similar but not byte-identical output. See the [reproducibility discussion](https://github.com/nmtrang29/extract-design-system/pulls) for detail.
- **Design-system docs sites** (mui.com, carbondesignsystem.com) currently produce confused output — the skill describes the docs UI as if it were the system. PR #2 fixes this.
- **Non-shadcn token naming** produces empty tokens-by-context sections today. PR #1 fixes this.

---

## Credits

- Built on top of [`designlang`](https://www.npmjs.com/package/designlang) by [Manavarya09](https://github.com/Manavarya09/design-extract) — the upstream extractor that produces the raw artifacts this skill reads. This repo is technically a fork (preserved for upstream pulls) but ships none of designlang's code.
- Colors-by-context layout inspired by [IBM Carbon Design System](https://carbondesignsystem.com/elements/color/overview/).
- Demo subjects: [langfuse.com](https://langfuse.com/), [ableton.com](https://www.ableton.com/), [claude.com](https://claude.com/), [utrecht.jp](https://utrecht.jp/).

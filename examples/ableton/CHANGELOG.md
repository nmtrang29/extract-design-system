# CHANGELOG — Ableton design system review

Compiled 2026-05-14 from a designlang v12.10.0 extraction of <https://www.ableton.com/en/>.

## Choices derived directly from the extraction

| Choice | Source artifact | Value |
|---|---|---|
| Brand blue as link / CTA colour | `variables.css` → `--color-secondary` | `#0000FF` (42 uses — the dominant chromatic) |
| Salmon as highlight pill | `variables.css` → `--color-primary` | `#FF8389` (2 uses — vibrant + legible on black text) |
| Page background | `variables.css` → `--color-bg` | `#F3F3F3` |
| Panel / card surface | `variables.css` → `--color-bg-1` | `#FFFFFF` |
| All radii = 0px | `visual-dna.json` (`avgRadius: 0`, `maxRadius: 0`, `hasPill: false`) + `design-tokens.json` (`radius: {}`) | Brutalist / sharp commitment is total |
| All shadows = none | `visual-dna.json` (`shadowProfile: none`) + `design-tokens.json` (`shadow: {}`) | Flat material |
| Body font weight = 700 | `design-language.md` body rule (`font-weight: 700`) | Carried through into the live review chrome |
| Type scale: 90 / 40 / 30 / 24 / 20 / 16 / 14 / 13 | `design-language.md` heading scale | 13.3333px snapped to 13 per skill rules |
| Motion durations: 150ms (xs) / 350ms (md) | `motion-tokens.json` | Both shown live in the Motion section |
| Scroll-linked feel | `motion-tokens.json` `$meta.scrollLinked: true` | Surfaced in motion captions |
| Hero emphasis word | `intent.json` title + `voice.json` tone | "Creative tools for *music makers*" — uses Ableton's own homepage copy |
| Nav menu items | `intent.json` section 1 lede | Live · Push · Move · Note · Link · Shop · Packs · Help · More |
| CTA verb pills | `voice.json` ctaVerbs | more (×2), close (×1), accept (×1) |
| Component patterns rendered | `DESIGN.md` "Detected patterns" | Exactly the 7 detected: buttons, inputs, links, navigation, footer, modals, badges (+ cards as a logical grouping of post tiles) |
| WCAG hero badge | `design-language.md` Accessibility section | 100% — both pairs AAA |
| Audit flag warnings | `design-language.md` "Don'ts" + scores | 418 !important rules · 96% unused CSS · 13,778 duplicates · 3 font families |

## Fallbacks and gaps

| Area | Gap | Fallback |
|---|---|---|
| Display font | `futura-pt` is licensed (Adobe Fonts / Typekit) — not free to host on a static review page | Rendered in **Jost** (free, geometric Futura-alike) via Google Fonts. Original face is named explicitly in the families panel and called out as a substitution. |
| Mono font | No mono detected in the extraction | Defaulted to **IBM Plex Mono** for code captions, hex values, and metadata. |
| Semantic status colours | The source declares `success`, `warning`, `error`, `info` as `[object Object]` in `variables.css` — likely a Sass map serialisation failure during extraction | Inferred from brand palette: success `#00d2be` (accent), warning `#eab308`, error `#ff8389` (primary), info `#6dcbff` (text-3). Disclosed in the Status & callout panel. |
| Background pattern | `visual-dna.json` reports `lineGrid: 0`, `dotGrid: 0`, `noise: 0` (`labels: ["plain"]`) | Hero / preview frame use a subtle horizontal-line grid generated from the spacing scale (40px) — review chrome only; flagged in the Patterns panel. |
| Border / line tokens | No explicit border colour tokens in `variables.css` | Page chrome uses derived neutrals `#e5e5e5` / `#f0f0f0`. The brand-true hard border `#000` is surfaced in the Border & line group. |
| Text secondary / tertiary | No `--text-secondary` family in source | Derived greys `#444 / #777 / #aaa` for review hierarchy only. Disclosed in `:root`. |
| Icon library | `library: unknown`, `confidence: 0` — Ableton uses custom marks (logo + social glyphs) on a 48px grid | Rendered approximate Lucide icons (music, play, download, chevron-down, search, x, external-link) + placeholder cards for the 4 mixed-style marks the extractor couldn't identify. |
| Component anatomy | Only the `button` cluster has detailed anatomy (variants: outline, primary) | Cards, inputs, modals, links, badges, navigation, footer rendered with plausible examples that mirror the detected style rules (0px radius, 700 weight, blue solid / black outline). |
| Heading samples in source | `voice.json` `sampleHeadings` is dominated by the literal string "More on Ableton.com:" repeated 6× (a nav heading mis-classified as a section heading) | Voice quotes hand-picked from `intent.json` section headings (Live 12.4 release banner, The latest from Ableton, Free downloads, etc.) — more representative of the brand's editorial voice. |
| Pricing section misclassification | `intent.json` flags 2 sections as `pricing` (release banner + downloads grid) | Captioned in the Page anatomy section as a likely heuristic miss. |

## Snapping rules applied

- **Radii:** snapped to detected scale = `0px`. Single exception: status-pip dots inside `.lf-badge` use `999px` (legitimate inline indicator per skill rules).
- **Font sizes:** every size in the review chrome maps to the detected scale (90/40/30/24/20/16/14/13). The 13.3333px source value was snapped to 13.
- **Accent treatment:** `#ff8389` (salmon-pink primary) used **only** as a highlight pill background — never as text colour. Applied to hero H1 `<em>`, voice quote emphasis, file-extension chips, badge accent variant, and icon count badges.
- **Pill chrome:** all default pill backgrounds reverted to 0px per the brutalist commitment of the source.

## Layer 2 (tokens-by-context) panel — what was kept

Of the six standard groups (Surface · Text · Border & line · Status · Code syntax · Shadcn primitives), only four are populated for Ableton:

- **Surface** (4 tokens)
- **Text** (4 tokens)
- **Border & line** (no tokens in source — surfaced as hard / 1px / 2px / sunken patterns)
- **Status & callout** (no tokens in source — values inferred and explicitly disclosed)

The **Code syntax** group was omitted (no syntax-highlighting tokens exist in the source). The **Shadcn primitives** group was omitted (`shadcn-theme.css` exists but the Ableton site does not use shadcn — `library.json` confirms `unknown`).

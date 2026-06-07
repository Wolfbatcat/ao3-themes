---
description: "Use when writing, editing, or reviewing AO3 site skin CSS. Covers Archive of Our Own's CSS restrictions, allowed properties, font rules, custom properties, and skin file conventions."
applyTo: "themes/**/*.css, extras/**/*.css"
---
# AO3 Site Skin CSS Rules

AO3's CSS parser strips anything not on the allowlist. All generated CSS must comply with these rules.

## Allowed Property Families (shorthand and variations permitted)

`background`, `border`, `column`, `cue`, `flex`, `font`, `layer-background`, `layout-grid`, `list-style`, `margin`, `marker`, `outline`, `overflow`, `padding`, `page-break`, `pause`, `scrollbar`, `text`, `transform`, `transition`

## Additionally Allowed Specific Properties

`-replace`, `-use-link-source`, `accelerator`, `accent-color`, `align-content`, `align-items`, `align-self`, `alignment-adjust`, `alignment-baseline`, `appearance`, `azimuth`, `baseline-shift`, `behavior`, `binding`, `bookmark-label`, `bookmark-level`, `bookmark-target`, `bottom`, `box-align`, `box-direction`, `box-flex`, `box-flex-group`, `box-lines`, `box-orient`, `box-pack`, `box-shadow`, `box-sizing`, `caption-side`, `clear`, `clip`, `color`, `color-profile`, `color-scheme`, `content`, `counter-increment`, `counter-reset`, `crop`, `cue`, `cue-after`, `cue-before`, `cursor`, `direction`, `display`, `dominant-baseline`, `drop-initial-after-adjust`, `drop-initial-after-align`, `drop-initial-before-adjust`, `drop-initial-before-align`, `drop-initial-size`, `drop-initial-value`, `elevation`, `empty-cells`, `filter`, `fit`, `fit-position`, `float`, `float-offset`, `font-effect`, `font-emphasize`, `font-emphasize-position`, `font-emphasize-style`, `font-family`, `font-size`, `font-size-adjust`, `font-smooth`, `font-stretch`, `font-style`, `font-variant`, `font-weight`, `grid-columns`, `grid-rows`, `hanging-punctuation`, `height`, `hyphenate-after`, `hyphenate-before`, `hyphenate-character`, `hyphenate-lines`, `hyphenate-resource`, `hyphens`, `icon`, `image-orientation`, `image-resolution`, `ime-mode`, `include-source`, `inline-box-align`, `justify-content`, `layout-flow`, `left`, `letter-spacing`, `line-break`, `line-height`, `line-stacking`, `line-stacking-ruby`, `line-stacking-shift`, `line-stacking-strategy`, `mark`, `mark-after`, `mark-before`, `marks`, `marquee-direction`, `marquee-play-count`, `marquee-speed`, `marquee-style`, `max-height`, `max-width`, `min-height`, `min-width`, `move-to`, `nav-down`, `nav-index`, `nav-left`, `nav-right`, `nav-up`, `opacity`, `order`, `orphans`, `page`, `page-policy`, `phonemes`, `pitch`, `pitch-range`, `play-during`, `position`, `presentation-level`, `punctuation-trim`, `quotes`, `rendering-intent`, `resize`, `rest`, `rest-after`, `rest-before`, `richness`, `right`, `rotation`, `rotation-point`, `ruby-align`, `ruby-overhang`, `ruby-position`, `ruby-span`, `size`, `speak`, `speak-header`, `speak-numeral`, `speak-punctuation`, `speech-rate`, `stress`, `string-set`, `tab-side`, `table-layout`, `target`, `target-name`, `target-new`, `target-position`, `top`, `unicode-bibi`, `unicode-bidi`, `user-select`, `vertical-align`, `visibility`, `voice-balance`, `voice-duration`, `voice-family`, `voice-pitch`, `voice-pitch-range`, `voice-rate`, `voice-stress`, `voice-volume`, `volume`, `white-space`, `white-space-collapse`, `widows`, `width`, `word-break`, `word-spacing`, `word-wrap`, `writing-mode`, `z-index`

## Critical Rules

### One Declaration Per Property Per Ruleset
AO3 keeps only the **last** declaration when a property appears multiple times in the same ruleset. For vendor-prefixed values, split into separate single-property rulesets:

```css
/* WRONG — only the last line survives */
.class { background: -moz-linear-gradient(...); background: -webkit-linear-gradient(...); }

/* CORRECT — each prefix in its own ruleset */
.class { background: -moz-linear-gradient(...); }
.class { background: -webkit-linear-gradient(...); }
```

### Font
- **Never use the `font` shorthand property** — it is stripped. Specify every font property individually:
  ```css
  font-size: 1em;
  font-weight: bold;
  font-family: Georgia, serif;
  ```
- **Never use `@font-face`** — not allowed.
- Font names with spaces must use matching quotes: `'Gill Sans'` or `"Gill Sans"` (not mixed).
- Always include web-safe fallback fonts.

### Custom Properties (CSS Variables)
- **Site skins only** — variables do not work in work skins.
- Names must use only: lowercase `a-z`, `0-9`, `-`, `_`. Uppercase letters are auto-lowercased.
- Names must not contain quotes or URLs.
- Use `var(--property-name)` with **no fallback** — fallbacks are not allowed.
- `var()` works on all properties **except** `font-family` and `content`.

### URLs
- Only external image URLs are allowed, in JPG, GIF, or PNG format.
- Format: `url('https://example.com/image.jpg')`
- Skins with external images cannot be approved for public use.

### Colors
- Use hex (`#000000`), `rgb()`, `rgba()`, or standard CSS color names.

### Numeric Values
- Up to **two decimal places**.
- Allowed units: `cm`, `em`, `ex`, `in`, `mm`, `pc`, `pt`, `px`, or `%`.
- Prefer `em` for responsive layouts.

### Scale
- `transform: scale(n)` — numeric value up to two decimal places.

### Comments
- **All CSS comments are stripped** by AO3's parser. Do not rely on them.

## Skin File Conventions (this repo)

- Each theme lives in `themes/<theme-name>/`.
- Skins are split into separate files by breakpoint, typically chained together on AO3:
  - `base.css` / `desktop.css` — base/desktop styles
  - `tablet.css` — tablet overrides
  - `mobile.css` — mobile overrides
- Alternate color variants use a suffix (e.g., `base_v2.css`, `CTH_base_alt.css`).

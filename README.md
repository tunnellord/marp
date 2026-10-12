# omarchy-pixel — Marp themes

Pixel-look [Marp](https://marp.app) themes inspired by [Omarchy](https://omarchy.org) (Matte Black): blocky fonts, notched pixel borders, hard drop shadows, a Waybar-style top bar and Hyprland-style windows. Fonts are embedded as Base64, so every theme is a single self-contained CSS file.

## Themes

| Theme | File | Look |
| --- | --- | --- |
| `omarchy-pixel` | `MarpThemes/omarchy-pixel.css` | Matte Black, orange accent (base theme) |
| `omarchy-pixel-light` | `MarpThemes/omarchy-pixel-light.css` | Light paper, darkened orange |
| `omarchy-pixel-axians` | `MarpThemes/omarchy-pixel-axians.css` | Navy + magenta |
| `omarchy-pixel-axians-light` | `MarpThemes/omarchy-pixel-axians-light.css` | Light grey + magenta |

All variants `@import 'omarchy-pixel'` and only swap the palette, so the base theme must always be loaded alongside them.

## Usage

**Obsidian ([Marp Slides](https://github.com/samuatt/marp-slides)):** copy `MarpThemes/` into your vault and set the plugin's theme path to `MarpThemes`. Reopen the preview after adding new theme files.

**marp-cli:**

```bash
npx @marp-team/marp-cli --theme-set MarpThemes/ "Omarchy Pixel Demo.md"
```

Front matter:

```yaml
---
marp: true
theme: omarchy-pixel
paginate: true
header: 'centered in the bar'
footer: 'bottom left'
---
```

## Slide classes

Set per slide with `<!-- _class: name -->` or for the whole deck with `class: name`. Classes can be combined, e.g. `split small`.

| Class | Effect |
| --- | --- |
| `lead` | Title slide with pixel-art logo and extruded block lettering |
| `section` | Chapter divider; `# 01` becomes a huge outline number |
| `terminal` | Hyprland window with accent border and `❯` prompt |
| `split` | Two columns; `h1`/`h2` span both |
| `invert` | Inverted colors (light in dark themes, dark in light themes) |
| `small` / `tiny` | Shrink only the code blocks (16px / 13px) |
| `no-workspaces` | Hide the logo and workspace marker in the top bar |

The demo decks (`Omarchy Pixel * Demo.md`) show every class. Design notes (German) are in `Omarchy Pixel Theme – Notizen.md`.

## Credits & licenses

- Omarchy Matte Black palette from [basecamp/omarchy](https://github.com/basecamp/omarchy).
- The Axians variants use colors taken from the public Axians websites. This is an unofficial project and is not affiliated with or endorsed by Axians.
- Embedded fonts, all under the SIL Open Font License 1.1 (see `fonts/`): [Silkscreen](https://github.com/googlefonts/silkscreen), [VT323](https://fonts.google.com/specimen/VT323), [JetBrains Mono](https://github.com/JetBrains/JetBrainsMono).

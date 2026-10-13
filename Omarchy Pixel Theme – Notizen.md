# Omarchy Pixel Theme – Arbeitsstand

Stand: 2026-10-12 · Status: **funktioniert in Obsidian** ✅ (dunkel + hell, Code-Umbruch, `small`/`tiny` getestet)

## Ziel
Ein Marp-Theme, das den Stil von **Omarchy** nachahmt. Farben: **Matte Black**. Schwerpunkt: **Pixel-Look** mit Blockschrift, Pixel-Kanten, Waybar- und Hyprland-Optik.

## Dateien (Pfade relativ zum Vault)
| Datei | Zweck |
| --- | --- |
| `MarpThemes/omarchy-pixel.css` | Das Theme, etwa 245 KB, Schriften als Base64 eingebettet |
| `MarpThemes/omarchy-pixel-light.css` | Helle Variante, wenige KB, importiert `omarchy-pixel` und tauscht nur die Palette |
| `MarpThemes/omarchy-pixel-french-purple.css` | French-Purple-Variante (Navy + Magenta), importiert `omarchy-pixel` |
| `MarpThemes/omarchy-pixel-french-purple-light.css` | Helle French-Purple-Variante (Hellgrau + Magenta), importiert direkt `omarchy-pixel` |
| `Omarchy Pixel Demo.md` | Demo-Deck mit 12 Folien, zeigt alle Klassen inkl. `small`/`tiny` mit langen Codezeilen |
| `Omarchy Pixel Light Demo.md` | Dasselbe Deck mit `theme: omarchy-pixel-light` |
| `Omarchy Pixel French Purple Demo.md` | Dasselbe Deck mit `theme: omarchy-pixel-french-purple` |
| `Omarchy Pixel French Purple Light Demo.md` | Dasselbe Deck mit `theme: omarchy-pixel-french-purple-light` |
| `.obsidian/plugins/marp-slides/data.json` | Plugin-Einstellungen mit `"ThemePath": "MarpThemes"` |

**Plugin:** Marp Slides (samuele-cozzi) 0.46.1. `EnableHTML` ist **aus**, deshalb kommt der gesamte Look aus reinem CSS und das Deck enthält kein Inline-HTML.

## Benutzung
```yaml
---
marp: true
theme: omarchy-pixel
paginate: true
header: 'Text mittig in der Waybar'
footer: 'Fußzeile unten links'
---
```
Für die helle Variante setzt man `theme: omarchy-pixel-light`. Dort wird `invert` zur dunklen Matte-Black-Folie.

Folienklassen setzt man mit `<!-- _class: name -->`:
- `lead`: Titelfolie mit Pixel-Art-Logo und großer Blockschrift mit 3D-Pixel-Extrusion
- `section`: Kapiteltrenner. Mit `# 01` erscheint eine riesige Kontur-Nummer, `## Titel` steht darunter.
- `terminal`: ein Hyprland-Fenster mit Gaps und Akzentrahmen, Prompt `❯`, Schrift VT323
- `split`: zwei Spalten, `h1` und `h2` gehen über die ganze Breite
- `invert`: kehrt die Farben um (im dunklen Theme hell, im hellen Theme dunkel)
- `no-workspaces`: blendet Logo und Workspaces oben links in der Waybar aus, die Leiste selbst, Header und Seitenzahl bleiben. Für das ganze Deck `class: no-workspaces` ins Front-Matter.
- `small` / `tiny`: verkleinern nur die Codeblöcke einer Folie (20px → 16px bzw. 13px). Lassen sich kombinieren, z. B. `<!-- _class: split small -->`.

## Design-Entscheidungen
- **Farben:** offiziell aus `basecamp/omarchy` → `themes/matte-black/colors.toml`
  - bg `#121212`, bg-dark `#0d0d0d`, bg-darker `#090909`, bg-light `#1e1e1e`
  - fg `#bebebe`, fg-dim `#8a8a8d`, fg-dark `#555555`, fg-bright `#eaeaea`
  - accent `#e68e0d`, accent-bright `#f59e0b`, yellow `#FFC107`, red `#D35F5F`, brown `#631e1e`
- **Schriften** (alle SIL OFL): Silkscreen 400/700 für Überschriften, VT323 für Terminal und Waybar, JetBrains Mono für Fließtext und Code. JetBrains Mono ist eine Variable Font, 400 und 700 teilen sich also eine Datei.
  - Eingebettet sind nur die Subsets latin und latin-ext, das reicht für Deutsch. Kyrillisch und Griechisch fehlen.
  - Base64 statt `url(fonts/…)`, weil das Plugin die CSS als String einliest und relative Pfade dann vermutlich nicht aufgelöst werden.
- **Pixel-Raster:** Variable `--px: 4px`
- **Pixel-Rahmen mit ausgesparten Ecken:** vier versetzte `box-shadow`s ohne Blur plus ein harter Drop-Shadow. Wird für `pre`, `blockquote` und `table` benutzt, die Rahmenfarbe kommt aus der Variable `--frame`.
- **Waybar:** `section::before` ist die Leiste. Den Workspace-Strich unter der „1“ zeichnet ein Gradient an Position `45px 28px`, das hängt also von der Zeichenbreite von VT323 ab.
- **Seitenzahl:** `section::after` mit `[ n / total ]`. Wichtig: `padding: 0; bottom: auto;`, weil Marpit selbst `padding: inherit` setzt.
- **Terminal:** `section.terminal > :not(header):not(footer)` bekommt `position: relative`. Ohne das `:not` rutschen Header und Footer ins Fenster.
- **Helles Theme:** `@import 'omarchy-pixel';` und danach nur Variablen überschreiben. Das funktioniert, weil das Plugin alle CSS-Dateien aus `MarpThemes` in dasselbe Theme-Set lädt. Neue Theme-Dateien werden erst nach erneutem Öffnen der Vorschau erkannt.
  - Flächen-Variablen im Basis-Theme: `--grid-dot`, `--scan`, `--window-bg`, `--code-bg`, `--shadow`, `--bar-bg`. Neue Farben immer über Variablen einbauen und nicht hart codieren, sonst stimmt das helle Theme nicht mehr.
  - Helle Palette: bg `#ececec`, fg `#2b2b2b`. Der Akzent ist auf `#c26a00` abgedunkelt, damit er auf hellem Grund genug Kontrast hat. Statt Gelb gibt es Dunkelgold `#94560a`, statt Braun Hellbraun `#e3b98a` für die Pixel-Extrusion.
- **Codeblöcke:** `white-space: pre-wrap` und `overflow-wrap: anywhere`, damit lange Zeilen umbrechen und nicht rechts aus der Folie laufen.
- **French-Purple-Theme:** Palette: Magenta `#a20067`, Dunkelmagenta `#690043`, Blau `#005eb8`, Navy `#0d1628`/`#0a1220`, Anthrazit `#2f2f2f`, Hellgrau `#f8f8f8`.
  - Das Basis-Magenta hat auf Navy nur ca. 1,1:1 Kontrast, deshalb ist der Text-Akzent das hellere `#e6007e`. `--yellow` ist hier Hellblau `#5fa8f0`, `--brown` Dunkelmagenta.
  - Hell (`omarchy-pixel-french-purple-light`): bg `#f8f8f8`, fg `#2f2f2f`, Akzent ist das Basis-Magenta `#a20067`, Strings und Inline-Code in Blau `#005eb8`, Extrusion als Magenta-Tönung `#ecc0db`. Es importiert `omarchy-pixel` und nicht `omarchy-pixel-light`, damit `invert` eine Navy-Folie wird und kein Matte Black.
  - `invert` ergibt im dunklen French-Purple-Theme eine helle Folie (`#f8f8f8`, Akzent `#a20067`), Codeblöcke dort weiß.
- **Zu volle Folien:** `justify-content: safe center`. Läuft der Inhalt über, klebt er oben und verschwindet nicht unter der Leiste. Automatisch passend skalieren kann CSS nicht, dafür gibt es `small`/`tiny`. Die verkleinern nur die Schriftgröße und das Padding von `pre`.
- **Hintergrund:** Punktraster mit 24px Abstand plus Scanlines alle 4px
- **Kein `repeating-linear-gradient`:** Chromium schreibt den ins PDF als Shading mit PostScript-Funktion (FunctionType 4), und viele PDF-Viewer zeichnen das als durchgehende Fläche. Deshalb ist die h2-Linie gestrichelt nur noch als einzelne Kachel mit harten Kanten plus `background-repeat` gebaut, das gilt auch für `hr` und die Scanlines.

## Verifikation (lokal)
```bash
cd <vault>
CHROME_PATH=/usr/bin/chromium npx -y @marp-team/marp-cli@latest \
  --theme-set MarpThemes/ --images png -o /tmp/demo.png -- "Omarchy Pixel Demo.md"
```
Das dauert etwa 1–2 Minuten, also am besten im Hintergrund laufen lassen.

## Offene Punkte / Ideen
- [x] ~~Cursor fehlt auf der Titelfolie~~: Das war kein Bug. In Obsidian blinkt er. Wahrscheinlich hat der PNG-Export genau die Phase erwischt, in der er ausgeblendet ist.
- [x] Helles Theme (`omarchy-pixel-light`)
- [x] Lange Codezeilen laufen rechts raus → umbrechen jetzt
- [x] Zu volle Folien laufen unten raus → `safe center` + Klassen `small`/`tiny`, die nur Codeblöcke verkleinern. Eine erste Version hat per `zoom` die ganze Folie verkleinert. Das war nicht gewünscht, betroffen sein soll nur der Code.
- [x] French-Purple-Farbschema (`omarchy-pixel-french-purple`, dunkel). Dazu die helle Variante `omarchy-pixel-french-purple-light`.
- [ ] Weitere Omarchy-Farbschemata als eigene Theme-Dateien nach dem gleichen Muster wie das helle Theme, z. B. Tokyo Night, Gruvbox, Rosé Pine, Catppuccin
- [ ] Option: VT323 auch für den Fließtext, für mehr Pixel-Look
- [ ] Pixel-Fortschrittsbalken unten
- [x] Workspaces oben links optional ausblendbar (`no-workspaces`)
- [ ] Workspace-Markierung in der Waybar dynamisch machen. Ginge eventuell über eine Klasse pro Kapitel.

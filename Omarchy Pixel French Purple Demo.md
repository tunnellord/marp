---
marp: true
theme: omarchy-pixel-french-purple
paginate: true
header: '22:14  ·  Sat Oct 11'
footer: 'omarchy-pixel · marp theme'
---

<!-- _class: lead -->
<!-- _paginate: false -->
<!-- _footer: '' -->

# OMARCHY

## a pixel theme for marp

matte black · silkscreen · vt323

---

## Was ist drin?

- **Pixel-Schriften**: Silkscreen für Überschriften, VT323 für die Terminal-Optik
- Eckige Rahmen mit *ausgesparten Ecken* und harten Schatten
- Waybar oben mit Workspaces und Seitenzahl
- Sub-Bullets
  - hohle Pixel-Quadrate
  - für die zweite Ebene
- Inline-`code` und [Links](https://omarchy.org)

---

<!-- _class: section -->

# 01

## Komponenten

---

## Code

```bash
# install omarchy on a fresh arch box
wget -qO- https://omarchy.org/install | bash

omarchy-theme-set "matte-black"
hyprctl reload
```

> Keyboard first. Keine Maus nötig, kein Schnickschnack.

---

## Tabelle

| Theme          | Background | Accent    |
| -------------- | ---------- | --------- |
| Matte Black    | `#121212`  | `#e68e0d` |
| Tokyo Night    | `#1a1b26`  | `#7aa2f7` |
| Gruvbox        | `#282828`  | `#d79921` |
| Rosé Pine      | `#191724`  | `#ebbcba` |

---

<!-- _class: terminal -->

# omarchy-menu

## Ein Hyprland-Fenster mit Gaps und aktivem Rahmen

- super + space → launcher
- super + return → terminal
- super + alt + space → omarchy menu

```
❯ fastfetch --logo omarchy
```

---

<!-- _class: split -->

## Zwei Spalten

### Links

Der Text fließt in zwei Spalten. Überschriften `h1`/`h2` gehen über die ganze Breite.

- Pixel
- Grid
- Matte

### Rechts

```js
const theme = "matte-black";
console.log(`hello ${theme}`);
```

---

<!-- _class: small -->

## Codeblock: `small`

Lange Zeilen brechen um. `small` macht nur den Code kleiner (16px), der Text bleibt normal groß.

```bash
curl -fsSL https://example.com/a/very/long/path/that/goes/on/and/on/install.sh | sudo bash -s -- --with-extra-flags
yay -S hyprland waybar mako swayosd walker
omarchy-theme-set matte-black && hyprctl reload
```

---

<!-- _class: tiny -->

## Codeblock: `tiny`

Für richtig viel Code: 13px. Kombinierbar, z. B. `split tiny`.

```js
// omarchy-pixel: lots of code on one slide
const themes = ["matte-black", "tokyo-night", "gruvbox", "rose-pine", "catppuccin"];

function setTheme(name) {
  if (!themes.includes(name)) throw new Error(`unknown theme: ${name} — choose one of ${themes.join(", ")}`);
  document.documentElement.dataset.theme = name;
  localStorage.setItem("omarchy-theme", name);
  return name;
}

for (const t of themes) console.log(`[ ${t.padEnd(12)} ] ready`);
setTheme("matte-black");
```

---

<!-- _class: no-workspaces -->

## Ohne Workspaces

Die Klasse `no-workspaces` blendet das Logo und die Workspaces oben links aus. Die Waybar selbst, der Header und die Seitenzahl bleiben.

Für das ganze Deck setzt man `class: no-workspaces` im Front-Matter.

---

<!-- _class: invert -->

# Invert

## Helle Variante

Für Folien, die herausstechen sollen, mit dem gleichen **Pixel-Look** und dem Akzent in `#e68e0d`.

---

<!-- _class: lead -->
<!-- _paginate: false -->

# EOF

## danke fürs zuschauen

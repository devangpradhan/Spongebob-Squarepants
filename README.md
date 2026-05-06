# 🧽 SpongeBob SquarePants — Interactive Scene

A creative, interactive browser scene built with **HTML**, **CSS**, and **vanilla JavaScript** featuring SpongeBob SquarePants standing in front of his pineapple house in Bikini Bottom.

---

## ✨ Features

- **Eye Tracking** — SpongeBob's pupils follow your cursor in real time across both X and Y axes using layered SVG manipulation
- **Fish Cursor** — The default cursor is replaced with a smooth-follow fish image
- **Underwater Bubbles** — Continuously spawning animated bubbles rise up the screen for an authentic underwater atmosphere
- **Layered SVG Eyes** — Eyes are built from separate SVG layers (`1_eye_bg.svg`, `eb_l.svg`, `eb_r.svg`, `2_eye_shade.svg`) stacked precisely over the character body
- **Responsive Layout** — Scene adapts to all screen sizes with `clamp()`-based sizing
- **Touch Support** — Eye tracking also works on mobile touch devices

---

## 📁 Project Structure

```
Code/
├── index.html          # Main scene file
└── assets/
    ├── backgorund.jpg  # Bikini Bottom underwater background
    ├── body.png        # SpongeBob character body
    ├── fish.png        # Custom fish cursor image
    ├── 1_eye_bg.svg    # Eye white/base layer
    ├── eb_l.svg        # Left eyeball layer (tracked)
    ├── eb_r.svg        # Right eyeball layer (tracked)
    ├── 2_eye_shade.svg # Eye shade/gloss overlay layer
    ├── eyes.svg        # Full combined eyes reference SVG
    └── Spongebob_Set.jpg  # Reference composition image
```

---

## 🚀 Getting Started

1. Clone or download this repository
2. Open `index.html` in any modern browser
   - No build tools, no dependencies, no server required
3. Move your cursor around the screen — SpongeBob will watch it!

> **Note:** Because the eye layers are loaded as `<object>` SVG files, browsers block cross-origin access when opened directly via `file://`. Use a local server for best results:
> ```bash
> # Python
> python -m http.server 3000
>
> # Node.js (npx)
> npx serve .
> ```
> Then open `http://localhost:3000`

---

## 🛠 How It Works

### Eye Tracking
Each eyeball SVG (`eb_l.svg`, `eb_r.svg`) contains a named layer group (`Eye_Ball_Left`, `Eye_Ball_Right`). On every `pointermove` event, the pointer position is mapped into SVG viewBox coordinates and each eyeball group is translated using `setAttribute("transform", "translate(x y)")`, clamped to a max offset radius of 18 units.

### Bubble System
JavaScript spawns `<span>` elements with randomised size, horizontal position, drift direction, and duration. A CSS `@keyframes rise` animation floats each bubble from the bottom of the screen upward, fading in and out. Bubbles are removed from the DOM after their animation ends to keep memory clean.

### Asset Layering
```
z-index 1  →  body.png         (character body)
z-index 3  →  eyes-rig div     (all eye SVG layers stacked inside)
              ├── 1_eye_bg.svg  (whites)
              ├── eb_r.svg      (right eyeball, tracked)
              ├── eb_l.svg      (left eyeball, tracked)
              └── 2_eye_shade.svg (gloss overlay)
```

---

## 🎨 Reference

Scene composition is based on **Spongebob_Set.jpg** — the original Bikini Bottom set with SpongeBob centered on the road in front of his pineapple house.

---

## 📜 License

This project is for personal/educational creative use only.  
SpongeBob SquarePants and all related characters are property of **Nickelodeon / Paramount Global**.

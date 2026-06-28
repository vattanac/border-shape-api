# 🖊️ CSS `border-shape` API — The Complete Beginner's Guide

> **Draw wobbly, sketchy, hand-drawn borders with pure CSS — no images, no SVG hacks, no JavaScript.**

![border-shape demo banner](https://raw.githubusercontent.com/your-username/border-shape-demo/main/assets/banner.png)

---

## 📌 Table of Contents

- [What is `border-shape`?](#-what-is-border-shape)
- [Why should you care?](#-why-should-you-care)
- [Browser Support](#-browser-support)
- [How to Enable It](#-how-to-enable-it)
- [Basic Syntax](#-basic-syntax)
- [Shape Values You Can Use](#-shape-values-you-can-use)
- [Real Examples](#-real-examples)
- [Best Parts of This Technology](#-best-parts-of-this-technology)
- [Tips & Tricks](#-tips--tricks)
- [What's Coming Next](#-whats-coming-next)
- [Resources](#-resources)

---

## 🤔 What is `border-shape`?

`border-shape` is a **new CSS property** (currently in proposal/experimental stage) that lets you change the *shape* of an element's border — not just its color or thickness, but its actual outline path.

By default, CSS borders are always straight lines with square or rounded corners. With `border-shape`, you can make borders that look:

- 🌊 **Wavy** — like ocean waves
- ✏️ **Wobbly** — like hand-drawn pencil lines
- 📐 **Zigzag** — like a saw blade
- 🔵 **Custom path** — any SVG-style shape you can imagine

Think of it like giving your HTML elements a **hand-drawn notebook border** — all with just one line of CSS.

### Before vs. After

```
Without border-shape:          With border-shape:
┌──────────────────┐           ╭∿∿∿∿∿∿∿∿∿∿∿∿∿∿∿∿∿╮
│  Normal boring   │           ∿  Wobbly, sketchy  ∿
│  straight border │           ∿  hand-drawn feel  ∿
└──────────────────┘           ╰∿∿∿∿∿∿∿∿∿∿∿∿∿∿∿∿∿╯
```

---

## 💡 Why Should You Care?

Before `border-shape`, getting a "sketchy" or "hand-drawn" border required:

- ❌ SVG images as backgrounds — hard to maintain, not flexible
- ❌ JavaScript canvas tricks — heavy, not CSS-native
- ❌ Multiple `box-shadow` hacks — messy code
- ❌ Pseudo-elements (`::before`, `::after`) workarounds — complicated

Now with `border-shape`:

- ✅ **One CSS property** — clean and simple
- ✅ **Fully animatable** — transition between shapes with CSS animations
- ✅ **Responsive by default** — scales with your element
- ✅ **Works with `border-radius`** — combine both for richer shapes
- ✅ **No dependencies** — zero JavaScript, zero libraries

---

## 🌐 Browser Support

> ⚠️ **This is an experimental / emerging API.** Support is limited as of mid-2026.

| Browser | Support | Notes |
|---|---|---|
| Chrome / Edge | 🟡 Experimental | Enable via `chrome://flags` → *Experimental Web Platform Features* |
| Firefox | 🔴 Not yet | Under discussion in CSS Working Group |
| Safari | 🔴 Not yet | On the roadmap |
| Chrome Canary | 🟢 Available | Best place to test today |

**What to do right now:**
- Use `border-shape` in **Chrome Canary** for demos and experiments
- Use the **multi-value `border-radius` trick** (explained below) as a fallback for production
- Check [caniuse.com/border-shape](https://caniuse.com) regularly for updates

---

## ⚙️ How to Enable It

### In Chrome (Desktop)

1. Open Chrome and go to: `chrome://flags`
2. Search for **"Experimental Web Platform Features"**
3. Set it to **Enabled**
4. Restart Chrome
5. Done! Now `border-shape` works in your browser.

### In Chrome Canary

Chrome Canary already has many experimental features on by default.
Download it here: [google.com/chrome/canary](https://www.google.com/chrome/canary/)

---

## 📝 Basic Syntax

```css
.element {
  border: 2px solid black;   /* you still need a regular border */
  border-shape: <value>;     /* then add the shape */
}
```

That's it. Two lines. The `border-shape` property tells the browser *how* to draw that border — what path/shape to follow instead of a straight line.

---

## 🎨 Shape Values You Can Use

### 1. `squircle` — Smooth rounded square

```css
.card {
  border: 2px solid #333;
  border-shape: squircle;
}
```

Looks like a "super-ellipse" — smoother than `border-radius: 50%`, more circular than a regular rounded rectangle. Used by Apple in iOS icons.

---

### 2. `path()` — Custom SVG path

```css
.wobbly-box {
  border: 2px solid #333;
  border-shape: path('M 0,4 Q 25,0 50,4 Q 75,8 100,4 L 100,96 Q 75,100 50,96 Q 25,92 0,96 Z');
}
```

You write an SVG path string. The browser uses that path as the border outline. This is the most powerful option — you can make *any* shape.

**Path command cheatsheet:**

| Command | Meaning | Example |
|---|---|---|
| `M x,y` | Move to point | `M 0,0` — start at top-left |
| `L x,y` | Line to point | `L 100,0` — draw straight line right |
| `Q cx,cy x,y` | Quadratic curve | `Q 50,10 100,0` — gentle curve |
| `C` | Cubic curve | More control points, smoother curve |
| `Z` | Close path | Connect back to start |

---

### 3. Wavy border with `path()`

```css
.wavy-card {
  border: 2px solid steelblue;
  border-shape: path('M 0,5 Q 12,0 25,5 Q 37,10 50,5 Q 62,0 75,5 Q 87,10 100,5 L 100,95 Q 87,100 75,95 Q 62,90 50,95 Q 37,100 25,95 Q 12,90 0,95 Z');
}
```

This creates a wave pattern on all four sides. Adjust the Q (quadratic curve) control points to make the waves bigger or smaller.

---

### 4. Zigzag border

```css
.zigzag-box {
  border: 2px solid tomato;
  border-shape: path('M 0,0 L 10,5 L 20,0 L 30,5 L 40,0 L 50,5 L 60,0 L 70,5 L 80,0 L 90,5 L 100,0 L 100,100 L 0,100 Z');
}
```

---

## 💻 Real Examples

### Example 1 — Simple wobbly card

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .notebook-card {
      border: 2.5px solid #1a1a1a;
      border-shape: path('M 0,3 Q 25,0 50,3 Q 75,6 100,3 L 100,97 Q 75,100 50,97 Q 25,94 0,97 Z');
      padding: 20px;
      max-width: 300px;
      font-family: 'Patrick Hand', cursive;
      background: white;
      box-shadow: 4px 4px 0 #1a1a1a;  /* hard shadow for sketchbook feel */
    }
  </style>
</head>
<body>
  <div class="notebook-card">
    This card has a hand-drawn wobbly border! ✏️
  </div>
</body>
</html>
```

---

### Example 2 — Animated wobbly border

```css
@keyframes wobble {
  0%   { border-shape: path('M 0,3 Q 50,0 100,3 L 100,97 Q 50,100 0,97 Z'); }
  50%  { border-shape: path('M 0,6 Q 50,0 100,6 L 100,94 Q 50,100 0,94 Z'); }
  100% { border-shape: path('M 0,3 Q 50,0 100,3 L 100,97 Q 50,100 0,97 Z'); }
}

.animated-card {
  border: 2px solid #4a90d9;
  border-shape: path('M 0,3 Q 50,0 100,3 L 100,97 Q 50,100 0,97 Z');
  animation: wobble 2s ease-in-out infinite;
}
```

The border gently breathes in and out — no JavaScript needed at all!

---

### Example 3 — Button with sketchy border

```css
.sketchy-btn {
  border: 2px solid #1a1a1a;
  border-shape: path('M 0,4 Q 50,0 100,4 L 100,96 Q 50,100 0,96 Z');
  background: #1a1a1a;
  color: white;
  padding: 10px 24px;
  font-size: 16px;
  cursor: pointer;
  transition: border-shape 0.2s ease;
}

.sketchy-btn:hover {
  border-shape: path('M 0,6 Q 50,0 100,6 L 100,94 Q 50,100 0,94 Z');
}
```

---

### Example 4 — The `border-radius` fallback trick

While waiting for full browser support, fake the sketchy look using **multi-value `border-radius`**:

```css
/* Each corner gets a different radius value */
/* syntax: top-left top-right bottom-right bottom-left / vertical variants */

.fake-wobbly {
  border: 2px solid #333;
  border-radius: 4px 8px 5px 7px / 7px 4px 8px 5px;
  box-shadow: 3px 3px 0 #333;
}
```

This makes each corner slightly different — not a true wave, but gives a hand-drawn feeling that works in **all browsers today**.

---

## ⭐ Best Parts of This Technology

### 1. 🎨 Pure CSS — No Extra Tools Needed

You don't need Photoshop, Illustrator, or any image editor. You don't need JavaScript. Just write CSS and the browser draws the shape for you. It's as simple as adding `color: red` to change text color.

---

### 2. ✨ Fully Animatable

This is the big one. You can **animate between two shapes** using CSS `@keyframes` or `transition`. No other technique (SVG background images, pseudo-elements, box-shadow hacks) can do this cleanly. The browser interpolates the path points smoothly, so the border morphs from one shape to another like liquid.

```css
/* This is IMPOSSIBLE with old techniques — now it's just CSS */
.card {
  transition: border-shape 0.3s ease;
}
.card:hover {
  border-shape: path('...different wobbly path...');
}
```

---

### 3. 📐 Scales with the Element

The border path scales automatically when the element resizes. Make the browser window smaller? The wobbly border stays proportional. No media queries needed, no JavaScript resize listeners.

---

### 4. 🧩 Combines with Existing CSS

`border-shape` works alongside properties you already know:

```css
.element {
  border: 3px solid hotpink;     /* color, width — still works */
  border-radius: 12px;           /* can combine with border-shape */
  border-shape: squircle;        /* adds the shape on top */
  box-shadow: 4px 4px 0 #333;    /* shadows still work perfectly */
  transition: border-shape 0.3s; /* animatable */
}
```

---

### 5. 🎭 Endless Creative Possibilities

One property opens up a whole new category of UI design:

- Notebook / sketchpad UIs
- Children's app designs with playful borders
- Organic, natural-feeling layouts (leaves, blobs, waves)
- Game UIs with sharp zigzag health bars
- Artistic portfolio sites with irregular frames
- Loading skeletons that wobble instead of pulse

---

### 6. 🚀 Performance-Friendly

Because it's native CSS handled by the browser's rendering engine, it runs on the **GPU compositor** — the same layer as `transform` and `opacity` animations. It's far more performant than animating borders with JavaScript or repainting canvas elements.

---

## 💡 Tips & Tricks

**Tip 1 — Keep your paths between 0 and 100**
Write your SVG paths in a 0–100 coordinate space. The browser scales them to fit your element automatically.

```css
/* ✅ Good — uses 0-100 range */
border-shape: path('M 0,0 Q 50,5 100,0 L 100,100 Q 50,95 0,100 Z');

/* ❌ Harder to work with — arbitrary pixel values */
border-shape: path('M 0,0 Q 200,15 400,0 L 400,300 ...');
```

**Tip 2 — Always pair with `border` first**
`border-shape` does nothing on its own. You must declare a regular `border` (with width, style, color) first:

```css
/* ✅ Correct */
.box { border: 2px solid black; border-shape: squircle; }

/* ❌ Won't work */
.box { border-shape: squircle; }
```

**Tip 3 — Use `box-shadow` for extra depth**
A hard offset shadow (no blur) adds the "sticker" or "stamp" effect that makes sketchy borders pop:

```css
.card {
  border: 2px solid #1a1a1a;
  border-shape: path('...');
  box-shadow: 4px 4px 0 #1a1a1a;  /* ← the magic line */
}
```

**Tip 4 — Combine with `@property` for tweakable wobble intensity**

```css
@property --wobble {
  syntax: '<number>';
  initial-value: 4;
  inherits: false;
}

.card {
  --wobble: 4;
  border-shape: path('M 0,var(--wobble) Q 50,0 100,var(--wobble) L 100,96 Q 50,100 0,96 Z');
}

.card:hover {
  --wobble: 10;  /* more wobbly on hover */
}
```

**Tip 5 — Use the `::before` dashed ring trick as a design accent**

```css
.card { position: relative; }
.card::before {
  content: '';
  position: absolute;
  inset: -6px;
  border: 1.5px dashed #aaa;
  border-shape: path('...slightly larger path...');
  pointer-events: none;
}
```

This creates a "double border" effect — one solid, one dashed — that looks very hand-crafted.

---

## 🗺️ What's Coming Next

The CSS Working Group is actively discussing extensions to `border-shape`:

| Feature | Status | What it does |
|---|---|---|
| `border-shape: squircle` | 🟡 Proposed | Built-in super-ellipse shape keyword |
| Per-side shapes | 🔴 Discussion | Different shape for `border-top-shape` vs `border-left-shape` |
| `shape()` function | 🟡 Progressing | Cleaner syntax than `path()` |
| Animating between named shapes | 🔴 Planned | `squircle` → `circle` transition |

Follow the official spec discussion: [github.com/w3c/csswg-drafts](https://github.com/w3c/csswg-drafts)

---

## 📚 Resources

| Link | What it is |
|---|---|
| [W3C CSS Working Group Drafts](https://github.com/w3c/csswg-drafts) | Official spec proposals and discussions |
| [MDN Web Docs — border](https://developer.mozilla.org/en-US/docs/Web/CSS/border) | CSS border reference |
| [CSS-Tricks — border-radius deep dive](https://css-tricks.com/almanac/properties/b/border-radius/) | Great multi-value border-radius guide |
| [SVG Path Visualizer](https://svg-path-visualizer.netlify.app/) | Draw and preview SVG paths visually |
| [Fancy Border Radius Generator](https://9elements.github.io/fancy-border-radius/) | GUI tool for multi-value border-radius fallback |
| [Chrome Canary Download](https://www.google.com/chrome/canary/) | Browser to test border-shape today |
| [caniuse.com](https://caniuse.com) | Check current browser support status |

---

## 🤝 Contributing

Found a bug in the examples? Have a cool `border-shape` demo to share?

1. Fork this repo
2. Create a branch: `git checkout -b my-cool-demo`
3. Add your example in the `/examples` folder
4. Open a Pull Request — all skill levels welcome!

---

## 📄 License

MIT — use freely, share widely, teach others. That's the whole point. 🎉

---

<div align="center">

Made with ✏️ and CSS by the community

**Star ⭐ this repo if it helped you learn something new!**

</div>
# border-shape-api

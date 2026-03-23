# Escher · Droste Conformal Renderer

Implementation of the mathematics from:

> B. de Smit & H. W. Lenstra Jr. — "The Mathematical Structure of Escher's Print Gallery"  
> *Notices of the AMS*, Vol. 50, No. 4, April 2003

---

## Overview

This tool applies the conformal map derived by de Smit and Lenstra to reproduce the
self-referential loop in Escher's 1956 lithograph *Prentententoonstelling* (Print Gallery).
The renderer exposes the full three-step pipeline as interactive controls, shows source and
output side-by-side, and overlays the true conformal coordinate grid derived from the inverse map.

---

## The Mathematics

### Three-step pipeline

```
Step 1: log(w)           circles → lines; Droste image → doubly-periodic grid
Step 2: α · log(w)       rotate + scale so a diagonal path → vertical segment of height 2π
Step 3: exp(α · log(w))  vertical height-2π segment → circle; the loop closes
```

This simplifies to the power map `h(w) = w^α`, a conformal isomorphism:

```
h: ℂ*/⟨γ⟩  →  ℂ*/⟨N⟩

α = (2πi + log N) / (2πi)  =  1 − i·logN/(2π)
γ = exp(2πi · logN / (2πi + logN))
```

For Escher's N = 256:

| Value   | Result |
|---------|--------|
| `α`     | `≈ 1.0000 − 0.8826i` |
| `\|γ\|` | `≈ 22.584`  (scale factor of the self-similar copy) |
| `arg(γ)`| `≈ 157.63°` (clockwise rotation of the self-similar copy) |

**Why α must be complex:** a purely real α swaps the roles of rotation and scaling, producing
an open spiral that never closes. The imaginary part couples scale to rotation so one full output
loop equals exactly one source zoom level.

### Pixel mapping

For each output pixel at complex coordinate `w = x + iy`:

1. Pre-rotate: `w' = |w| · exp(i · (arg(w) + rotate + cutOffset))`
2. Log: `logW = ln|w'| + i·arg(w')`
3. Offset: `logW_mod = { re: logW.re + zoom,  im: logW.im + phase }`
4. Map: `z = exp(α · logW_mod)`
5. Normalize to source fundamental domain:
   - `u = (logZ.re × iterations / logN) mod 1`  — scale axis
   - `v = (logZ.im / 2π) mod 1`                 — rotation axis
6. Bilinear sample source image at `(u, v)`

### The source image

The source lives in **log-space** and must be doubly periodic:

- **Vertically** (v, period 2π) — rotation is periodic; any image satisfies this after wrapping
- **Horizontally** (u, period = logN) — the Droste scene must repeat under scaling by N

For a genuine result, `x = width` must look identical to `x = 0` but at N× the scale.
De Smit and Lenstra produced their source by inverse-mapping the original Escher lithograph
with help from two Dutch artists.

### The elliptic curve connection

`ℂ*/⟨δ⟩ ≅ ℂ/L_δ` where `L_δ = ℤ(2πi) + ℤ(log δ)`. The map h lifts to multiplication by α
on the universal cover, constrained by `α · L_γ = L_N`. This uniquely determines γ — specifying
the exact rotation and scale of what should fill the blank circle in Escher's lithograph.

---

## Setup

### Standalone (no install)

Open `index.html` directly in any modern browser. No server or build step required.

### Electron desktop app

```bash
npm install
npm start
```

### Build distributable

```bash
npm run build-win      # Windows NSIS installer → dist/
npm run build-mac      # macOS DMG              → dist/
npm run build-linux    # Linux AppImage          → dist/
```

Requires Node.js ≥ 18 and npm.

---

## Interface

### Split canvas

- **Top pane — source**: raw source image, updated immediately on load
- **Bottom pane — output**: conformal map result, updated on Render or auto-render

### Conformal Map Parameters

| Control | Effect |
|---------|--------|
| `scale (N)` | Periodicity factor. Paper: 256. N=16 is clearer for learning. Changing N changes α and γ. |
| `rotate` | Pre-rotation of input plane |
| `inner radius (r1)` | Central hole radius. Near-zero lets the spiral run to the origin. |
| `outer radius (r2)` | Outer boundary |
| `iterations` | Zoom-level periods sampled. Each step adds one nested self-similar layer. Also scales conformal grid density. |
| `output size` | Pixel resolution |

### Annular Mapping

| Control | Effect |
|---------|--------|
| `cut position` | Moves the atan2 branch-cut seam. Always present; this repositions it. Default π/2 = bottom of canvas. |
| `phase shift` | Translates log-polar angle — rotates spiral content |
| `zoom offset` | Translates log-polar radius — zooms spiral content |
| `angular fold` | Triangle-wave fold of the v axis. **Doubles angular sampling frequency.** Removes v=0/v=1 seam only if source top/bottom edges match. Creates a new kink at v=0.5 on arbitrary sources. |
| `overlay conformal grid` | True conformal coordinate lines via the inverse map. Amber = constant-v (angular spirals). Blue = constant-u (radial curves). Scales with iterations. |

### Color Treatment

| Mode | Description |
|------|-------------|
| `retain` | Original colours |
| `grayscale` | Luminosity-weighted (0.299R + 0.587G + 0.114B) |
| `sepia` | Standard sepia matrix |
| `invert` | 255 − channel |
| `warm` | Boosts red/green, reduces blue |
| `cool` | Reduces red, boosts blue |
| `red / green / blue` | Single channel isolation |

`intensity` blends between original and treated (0 = original, 1 = full treatment).

### Output Shape

| Shape | Description |
|-------|-------------|
| `circle` | Radial clip at r2. Dark corners. |
| `square` | No outer radial clip. Spiral fills to canvas corners. |
| `rect` | Height = width × aspect ratio. Crops without stretching. Six presets from 16:9 to 9:16 portrait. |

### Quick Presets

| Preset | Sets |
|--------|------|
| `N = 16` | scale=16, r1=0.005, iter=3 — clearer for learning |
| `N = 256 (Escher)` | scale=256, r1=0.005, iter=4 — paper's values |
| `open spiral` | r1=0.001, iter=6 — deep spiral, no hole |
| `annulus` | r1=0.15, iter=3 — visible inner hole |

---

## Known limitations

**Branch-cut seam:** `atan2` discontinuity at `arg = ±π` maps through α into a single radial
line. The cut-position slider moves it; elimination requires winding-number continuation across
scanlines (not implemented).

**Source image:** Built-in demos approximate a valid log-space source but do not satisfy strict
horizontal periodicity. A mathematically correct result requires the inverse-mapped log
representation of a genuine Droste image.

**Performance:** Pure JavaScript pixel loop with bilinear interpolation. At 1024px expect 2–5s.
A WebGL implementation would be 100–200× faster.

---

## Files

```
index.html    — Self-contained renderer: all math, UI, generators (~1150 lines)
main.js       — Electron main process: window creation, menu
package.json  — npm config + electron-builder packaging
README.md     — This file
```

---

## Audit history

Systematic code review and fix passes applied after initial build:

**Critical** — C1: inner radius slider unused in clip; C2: iterations slider unused in UV
normalization; C3: conformal grid drew plain polar grid, rewritten using correct inverse map.

**Functional** — F1: concurrent async renders corrupted shared pixel buffer (generation counter);
F2: duplicate `id` on grid checkbox; F3: reset used positional array (reordering = silent wrong
values); F4: mirror wrap folded wrong axis (u/radial not v/angular); F5: no error handlers on
FileReader/Image.

**Math** — M1: branch cut at canvas left edge (CUT_OFFSET, now user slider); M2: `C.log(z≈0)`
returned −Infinity, silent NaN pixels (isFinite guard); M3: `+ -0.8826i` display formatting.

**Quality** — Q1: outer clip 2.2× bled beyond rendered boundary (tightened to 2.0×);
Q2: progress-bar reset timer fired against subsequent renders (clearTimeout).

**Feature additions** — Cut position slider; color treatment + intensity; output shape
(circle/square/rect); split source/output canvas; quick presets; demo generators rewritten for
correct log-space periodicity; theory box updated to 3-step pipeline.

**Conformal grid audit** — CG1: `uvToScreen` ignored `p.iterations` (grid covered only
1/N of output at N iterations); CG2: outer clip 2.05× tolerance drew lines into dark background.

**Mirror wrap audit** — MW1: label "annular continuity" factually wrong (renamed);
MW2: claimed to remove branch-cut seam (incorrect — it removes v=0/v=1 seam on matching-edge
sources and adds a kink at v=0.5); MW3: silent frequency-doubling side effect undocumented.

---

## References

1. B. de Smit & H. W. Lenstra Jr., "The Mathematical Structure of Escher's Print Gallery,"
   *Notices of the AMS* 50:4 (2003), pp. 446–451.
2. J. Silverman, *The Arithmetic of Elliptic Curves*, Springer-Verlag, 1986.
3. Leiden project website: escherdroste.math.leidenuniv.nl

# TERRA · Line-Art Earth Observatory

线 · 观 · 测 — a single-file interactive 3D visualization of Earth rendered in the
style of a calm paper atlas, with live data layered on top.

![aesthetic: pencil-on-rice-paper line art](https://img.shields.io/badge/aesthetic-pencil%20on%20rice%20paper-f5f2ea?labelColor=1a1a1a)
![no build](https://img.shields.io/badge/build-none-f5f2ea?labelColor=1a1a1a)
![one file](https://img.shields.io/badge/files-1%20html-f5f2ea?labelColor=1a1a1a)

## 🌐 Live Demo

Visit: [https://rinshannkaihou.github.io/mono_earth/](https://rinshannkaihou.github.io/mono_earth/)

Or open `interactive-earth.html` directly in any modern browser — no build, no
bundler, no server.

## ✨ Features

### Cartography
- Real country borders from GeoJSON, merged into a single `LineSegments`
  draw call for frame-rate stability.
- Deterministic pencil-wobble jitter on every border for a hand-drawn feel.
- Latitude / longitude graticule with distinct equator, tropics, and polar
  circles.
- Back-face occlusion via a background-tinted solid sphere — lines on the far
  side of the globe correctly disappear.

### Live Data
- **Day / night terminator** computed from the UTC solar declination and hour
  angle, redrawn every frame as a dashed great-circle.
- **Night-side pencil hatching** via a custom GLSL fragment shader — discards
  sunlit pixels, draws screen-space diagonal hatching whose density and
  cross-hatching ramp up away from the terminator.
- **Seismic events** fetched from the USGS "all earthquakes, last 24 h" feed,
  plotted as magnitude-scaled pulse rings; refreshed every 10 minutes.
- **Great-circle air routes** between 12 major city pairs, animated with
  traveling particles along each slerp-interpolated arc.
- **Starfield** with real celestial-coordinate constellations (Orion, Big
  Dipper, Crux) rotating slowly relative to the Earth for parallax depth.

### Interaction
- Click anywhere on the globe for a **sonar ping** — two concentric ripples
  at the hit point.
- Drag the **time scrubber** to move the sun manually; Space returns to real
  time.
- **Layer toggles** for Grid / Borders / Terminator / Night hatch / Stars /
  Seismic / Routes — each with a keyboard shortcut.
- **Three modes**: Minimal, Standard, Detailed — differ in line opacity and
  which auxiliary elements render.
- **Postcard export** (P) — saves the current camera view as a timestamped
  PNG.
- Bilingual region hints (zh / en) in the pointer readout.

### Keyboard
| Key | Action |
|-----|--------|
| `R` | Toggle auto-rotation |
| `0` | Reset view |
| `+` / `−` | Zoom in / out |
| `P` | Export postcard PNG |
| `SPACE` | Scrub ⇄ real-time |
| `G` `B` `T` `N` `S` `Q` `A` | Toggle each layer |
| `M` | Cycle mode |
| `?` | Keyboard cheat sheet |

## 🛠 Built With

- [Three.js](https://threejs.org/) r128 — WebGL scene graph
- Custom GLSL — night hatching and starfield shaders
- GeoJSON world borders — from the [D3 graph gallery](https://github.com/holtzy/D3-graph-gallery)
- [USGS Earthquake Hazards Program](https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_day.geojson) — live seismic feed
- Space Mono + Noto Sans SC — typography

No bundler, no framework, no build step. One HTML file, two CDN scripts.

## 🚀 Deployed on GitHub Pages

`index.html` is served by GitHub Pages as the public site.
`interactive-earth.html` is the identical source-of-truth copy — edits are
mirrored between the two.
